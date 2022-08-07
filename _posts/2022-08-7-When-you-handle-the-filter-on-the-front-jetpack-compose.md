Say there is a Product that you want to implement. Each can have different type one to another, also has different status. Summary the product can have:
1. Different Product Type
2. Different Status 

you are assigned to make a filter, on the front, not back.  

so you can mix up those two filters.  

Conditions:
1. Mix both `productType` and `status`
2. The `productType` includes `All Type`
3. The `status` includes `All Status`
4. The default filter is `All Type` and `All Status`
5. The Filter is never `empty`, if none `productType` filter is clicked then `All Type` is active
6. Same with `status`, named `All Status` is active.
7. Can select more than one for `productTtype` filter
8. Can select more than one for `status` filter

So I need some trigger event after user submit its filter preference.
It's doesnt make any difference whether the product to be filtered first or the status,
Say I want the `productType` to be checked first,  
every event triggered, if the list is as same as the default (all products - all status)
if not then I need to clear the list, then `addAll` from the all list that has been memorized in a variable.
Thus I also need a variable that holds the default state (all products & all statuses)
I can use it as a source data of reference

Steps:  
1. Provide two variables contain same list, one acts as a source data of reference, the another is to be displayed for UI that can be manipulated.
2. Add them from the source (say it's from backend)
3. Provide a variable which can be used as a trigger for filter event (after Filter UI is closed, applied)
4. Look at the filter UI, if it's like a button style item, then provide a list that contains which ones have been chosen to be filtered, say you name it `addedFilterList<String>`.  
If it is a checkbox style, you need a list that contains which ones have been checked (list of boolean is enough, can use index as a key). say you name it `isCheckedStateList`   
5. If filter candidate item is clicked, add to `addedFilterList` if it's unclicked, remove that.   
6. For the checkbox style, is similar `true` for active (checked), `false` for inactive
7. We implement three kind of event whenever Filter UI is shown there,  
one is that when all filter candidates is clicked (all product type in filter is clicked, excluding `all type`),
the next is when user clicks `all type`.  
the last is the other way around, when user clicks one of the product types
7a. If all filter candidates is clicked, then you can remove all of them, then add the `all type` filter.
```kotlin
addedFilterList.map { it.lowercase() }.containsAll(arrayListOf(
  PRODUCT_TYPE_A, PRODUCT_TYPE_B, ... PRODUCT_TYPE_X
)){
  addedFilterList.clear()
  addedFilterList.add("all type")
}
```  
7b. If `all type` is clicked, negate all other candidates if the fliteredList contains any of productType,  
remove them,, then add the `all type`.  

7c. If `one of the product types` is clicked, remove the `all type` if it is on the addedFilterList beforehhand.

Recap for Filter UI click events:
for the `checkbox` case
```kotlin
LaunchedEffect(isAllStatusFilterCandidateClicked){
  if(isAllStatusFilterCandidateClicked){
     isCheckedStateList.replaceAll { false }
     isCheckedStateList[0] = true
  }
}

statusList.forEachIndexed { index, isChecked ->

//onCheckedChange =
  if (index > 0 && it && isAllStatusAndOtherClicked()) {
    handleWhenAllAndCriteriaClicked()
} else if (index == 0 && it && isAnyCriteriaClicked()) {
    handleWhenSemuaStatusClicked()
} else if (index == 0 && !it && isAllStatusNotClicked()) {
    handleWhenSemuaStatusUnclickedAndCriteriaEmpty()
    return@EdufundCheckBox
}

isCheckedStateList[index] = it
}
```  

for the button styled item case  

```kotlin
//Your "All Type" Button
Modifier.clickable {
  if (
    addedFilterList
        .subList(1, addedFilterList.size)
        .isNotEmpty() ||
        addedFilterList[0] !=
            BuildConfig.FILTER_LOAN_PRODUCT_SEMUA
) {
    addedFilterList.clear()
}

addedFilterList.add(allTypeText)
}

if (isAllTypeClicked(addedFilterList)) {
    LaunchedEffect(isAllTypeClicked(addedFilterList)) {
        addedFilterList.clear()
        addedFilterList.add(allTypeText)
    }
} else if (
    isAllAndAnyProductTypeClicked(
        filterByProductOptionTextFieldState.addedFilterList,
        semuaProdukText
    )
) {
    LaunchedEffect(
        isAllTypeAndAnyProductTypeClicked(
            filterByProductOptionTextFieldState.addedFilterList,
            allTypeText
        )
    ) { addedFilterList.remove(allTypeText) }
}

```

8. The Event after filter is submitted (closed)  

```kotlin
@Composable
private fun FilterLaunchedEffect(
    isFilterSubmitted: MutableState<Boolean>,
    addedFilterList: ArrayList<String>,
    isCHeckedStateList: ArrayList<Boolean>,
    filterByStatusOptionTextFieldState: FilterByLoanStatusOptionTextFieldState,
    loanTransactionList: SnapshotStateList<Loan>,
    allLoanTransactionList: ArrayList<Loan>,
    onFilterSubmitted: () -> Unit
) {
    LaunchedEffect(
        isFilterSubmitted.value,
        addedFilterList.isNotEmpty() ||
            isCheckedStateList.any { true }
    ) {
        if (
            isFilterSubmitted.value &&
                (addedFilterList.isNotEmpty() ||
                    isCheckedStateList.any { true })
        ) {

            onFilterSubmitted()

            val filterProductCandidateList = arrayListOf<((String) -> Boolean)>()
            val filterStatusCandidateList = arrayListOf<((String) -> Boolean)>()

            if (
                addedFilterList.contains(
                    FILTER_ALL_TYPE
                ) && isCheckedStateList[0]
            ) {
                if (transactionList != allTransactionList) {
                    transactionList.clear()
                    transactionList.addAll(allTransactionList)
                }
            } else {
                transactionList.clear()

                val filteredList = arrayListOf<Loan>()
                filteredList.addAll(loanTransactionList)

                addFilterByProductCandidateList(
                    isAllProductTypeSelected,
                    addedFilterList,
                    filterProductCandidateList,
                    filteredList
                )

                addFilterByStatusCandidateList(
                    itemList, //status list 
                    isAllStatusChecked: Boolean,
                    isCheckedStateList: ArrayList<Boolean>,
                    filterStatusCandidateList,
                    filteredList
                )

                loanTransactionList.addAll(filteredList)
            }
        }

        isFilterSubmitted.value = false
    }
}


private fun addFilterByProductCandidateList(
    isAllProductTypeSelected: Boolean,
    addedFilterList: ArrayList<String>,
    filterProductCandidateList: ArrayList<(String) -> Boolean>,
    filteredList: ArrayList<Loan>
) {
    if (!isAllProuctTypeSelected()) {
        addedFilterList.forEach {
            filterProductCandidateList.add { 
              value -> value == it 
            }
        }
    }

    if (filterProductCandidateList.isNotEmpty()) {
        filteredList.filterAndUpdateList { loan ->
            filterProductCandidateList.any { product ->
                product(loan.getProductTypeEdu())
            }
        }
    }
}


private fun addFilterByStatusCandidateList(
    itemList: ArrayList<String>,
    isAllStatusChecked: Boolean,
    isCheckedStateList: ArrayList<Boolean>,
    filterStatusCandidateList: ArrayList<(String) -> Boolean>,
    filteredList: ArrayList<Loan>
) {
    if (!isSemuaChecked) {
        isCheckedStateList.forEachIndexed { index, isChecked ->
            if (isChecked) {
                filterStatusCandidateList.add {
                    it == itemList[index]
                }
            }
        }
    }

    if (filterStatusCandidateList.isNotEmpty()) {
        filteredList.filterAndUpdateList { loan ->
            filterStatusCandidateList.any { statusName ->
                status(
                    statusName
                )
            }
        }
    }
}

```

I make use of kotlin `filter{}` extension function, so it can mingle with:
```kotlin
  val filterProductCandidateList = arrayListOf<((String) -> Boolean)>()
  val filterStatusCandidateList = arrayListOf<((String) -> Boolean)>()
```

`list.any{obj -> }` can act as a OR in the database so.... it helps a lot, can be convenient with these.  


for the `filterAndUpdateList{}` ext function you can take a look [here](https://gist.github.com/shohiebsense/d96789d17c704b7602afb96c5d8899f7):  

