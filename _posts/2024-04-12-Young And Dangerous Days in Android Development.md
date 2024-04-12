# MyDevelopingJournal
Emm.. yeah.. emm.. hehe :)

Cases

1. Your home app displays Toolbar that can be scrolled, and there is a framelayout contains fragment. This fragment contains viewpagers (yes, multiple viewpager) which are displaying recyclerview. What you are gonna do is you wrapped the framelayoutin the activity inside NestedScrollview. Then in the layout fragment, wrapped entire layout with nestedscrollview again for scrolling those multiple viewpager. Put each viewpager absolute height neither wrap content nor match_parent. 

Like this
> activity_main
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.NestedScrollView 
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layout_behavior="@string/appbar_scrolling_view_behavior"
    android:fillViewport="true"
    tools:context=".view.page.home.MainActivity"
    tools:showIn="@layout/activity_main">

    <FrameLayout
        android:id="@+id/frameLayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior" />


</android.support.v4.widget.NestedScrollView>
```
> fragment_main

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.NestedScrollView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/scroll_root"
    android:background="@color/white_light"
    app:layout_behavior="@string/appbar_sc_view_behavior"
    >

        <android.support.constraint.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

        <android.support.design.widget.TabLayout
            android:focusable="true"
            android:focusableInTouchMode="true"
            android:id="@+id/tab_a_b"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            app:layout_constraintTop_toBottomOf="@+id/layout_point"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:tabIndicatorColor="@color/color_tab_indicator"
            app:tabSelectedTextColor="@color/color_tab_text_selected"
            app:tabTextColor="@color/color_tab_text"
            app:tabTextAppearance="@style/AppTheme.TextAppearance.Tab"
            >

            <android.support.design.widget.TabItem
                android:id="@+id/tab_item_a"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/promo" />

            <android.support.design.widget.TabItem
                android:id="@+id/tab_item_b"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/spot" />

        </android.support.design.widget.TabLayout>

        <ScrollableViewPager
            android:id="@+id/pager_a_b"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/tab_a_b"
            />

        <android.support.design.widget.TabLayout
            android:focusable="true"
            android:focusableInTouchMode="true"
            android:id="@+id/tab_c_d"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            app:tabIndicatorColor="@color/color_tab_indicator"
            app:tabSelectedTextColor="@color/color_tab_text_selected"
            app:tabTextColor="@color/color_tab_text"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/pager_a_b"
            >

            <android.support.design.widget.TabItem
                android:id="@+id/tab_item_b"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/news" />

            <android.support.design.widget.TabItem
                android:id="@+id/tab_item_c"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/event" />

        </android.support.design.widget.TabLayout>

        <ScrollableViewPager
            android:id="@+id/pager_c_d"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            android:nestedScrollingEnabled="true"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/tab_home_news_event"
            app:layout_constraintBottom_toBottomOf="parent"
            />


        </android.support.constraint.ConstraintLayout>
</android.support.v4.widget.NestedScrollView>
```

2. Use recyclerview and apply FlexBoxLayoutManager, like when you created items horizontally and wrapped to the width of device.

3. You have to set typeface programmatically to change Input Layout text/hint

4. For applying different colors in text, use foregroundcolorspan
SpanableString(string)
ForegroundColorSpan(
StyleSpan(

5. LRUCache is flexible in terms of data type compared to SharedPreferences, but LRUCache accepts thread safe only.

6. Don't use ListAdapter when it is so many user interactions, user recyclerview.adapter instead. submitlist still has an issue.

7. StartActivityForResult In Stacks
https://medium.com/@douglas.iacovelli/android-send-result-back-through-multiple-activities-finished-or-not-4c2ba9e95112

https://www.google.com/search?client=firefox-b-d&q=FLAG_ACTIVITY_FORWARD_RESULT
FLAG_ACTIVITY_FORWARD_RESULT

8. Look upon this link if your generating signed apk error
https://stackoverflow.com/questions/24098494/error-when-generate-signed-apk/52403664

9. Consider to know the difference between SharedPreference.Editor.apply() and commit(). Commit() does the job immediately.

10. To sync-to not sync strategy:
Using timestamp as flags, store the latest timestamp in SharedPreference
- Using last upload time & last download time. When it's more often to interact.
- Using last update.... if it's less often to interact.. like. Master Data.

https://coderwall.com/p/gt_rfa/simple-data-synchronisation-for-web-mobile-apps-working-offline

- last_update_on
- created_on
- deleted_on

https://dzone.com/articles/how-to-make-mobile-app-work-offline

- sync it using time stamp

https://medium.com/mindorks/to-synk-or-not-to-synk-fcc6e4c56e14

https://github.com/google/iosched

https://github.com/karntrehan/Posts

Read more 

https://www.reddit.com/r/androiddev/comments/6bh31s/offlinefirst_with_sync_best_way_to_approach_this/

11. Clear Logs when in the release mode with proguard
https://support.brightcove.com/removing-android-log-messages

12. Analyze the error when signed build apk
https://stackoverflow.com/questions/24098494/error-when-generate-signed-apk

13. Use getText().clear() instead of setText("") to clear.

13. Always check permission list 
https://developer.android.com/guide/topics/permissions/overview

14. Adding filter list instead of replacinag
```java
 InputFilter[] filterList = editText.getFilters();
 InputFilter[] newFilterList = new InputFilter[filterList.length + 1];
 System.arraycopy(filterList, 0, newFilterList, 0, filterList.length);
 ```
 then applies the edittext / textview the new filters.  
 

15. USING SELECT COUNT(WHEN ..'CLAUSE'.. THEN 1 END) If you wanted to search by criteria.
https://stackoverflow.com/questions/6350154/selecting-count-from-different-criteria-on-a-table
      
      
      
16. #### Converting Excel Into CSV MYSQL #####

https://lenashore.com/2012/04/how-to-add-quotes-to-your-cells-in-excel-automatically/

Let's assume you have added quotes to each of your cells 

Copy paste to notepad

Replace the spaces as with semicolon 

save as .csv

there you go

17. Regarding Intent, TOP means foreground, (Current displayed Activity) Developer.Android states that the TOP intent may have more than one Activity.

https://stackoverflow.com/questions/8076939/what-is-the-difference-between-intent-flag-activity-clear-top-and-finish-in-andr  

18. You cannot run delayed functions (timer/postdelayed) in the background thread.

19. If conflicts come out between androidx and appcompat, consider checking gradle.properties
> android.useAndroidX = true  
> android.enableJetifier=true

20. Set Default Locale
https://stackoverflow.com/a/61572489
``` java
    @Override
    protected void attachBaseContext(Context newBase) {
        Context newContext = updateBaseContextLocale(newBase);
        super.attachBaseContext(newContext);
        applyOverrideConfiguration(newContext.getResources().getConfiguration());
    }


    private Context updateBaseContextLocale(Context context) {
        Locale locale = new Locale("id");
        Locale.setDefault(locale);
        return updateResourcesLocale(context, locale);
    }

    private Context updateResourcesLocale(Context context, Locale locale) {
        Configuration configuration = context.getResources().getConfiguration();
        configuration.setLocale(locale);
        return context.createConfigurationContext(configuration);
    }
```

21. Handle When a view is at the bottom of a viewpager
```xml
<CoordinatorLayout>
    <VariousView>
    </VariousView>
    <LinearLayout
        app:layout_behavior="@string/appbar_scrolling_view_behavior">
            <ViewPager2
                android:layout_width="match_parent"
                android:layout_height="0dp"
                android:fitsSystemWindows="true"
                android:layout_weight="1/>
                                       
            <Button
                android:id="@+id/button_submit"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_alignParentBottom="true"
                app:layout_behavior="@string/appbar_scrolling_view_behavior"/>
    </LinearLayout>
</CoordinatorLayout>
```

22. When you put CoordinatorLayout, attribute app:layout_scrollFlags="scroll|enterAlwaysCollapsed" makes the layout collapsed and scroll slightly to the bottom,
you want your layout scroll to the top first.
```xml
    <com.google.android.material.appbar.CollapsingToolbarLayout
            android:id="@+id/layout_toolbar_collapsing"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:layout_scrollFlags="scroll|enterAlwaysCollapsed"
            >
            
          
            ...
            
    </com.google.android.material.appbar.CollapsingToolbarLayout

```

```kotlin
layout_toolbar_collapsing.scrollTo(0, view.bottom) //or 0
```
23. Toolbar overlaps its contents, the theme is no action bar or 
```xml
   <item name="windowActionBar">false</item>
   <item name="windowNoTitle">true</item>
```
add margin Top to the size of  toolbar height. =>
```xml
    <androidx.coordinatorlayout.widget.CoordinatorLayout
     android:fitsSystemWindows="true"
     android:background="@drawable/green"
     android:fitsSystemWindows="true">
      <com.google.android.material.appbar.AppBarLayout
        android:id="@+id/layout_appbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/AppTheme.AppBarOverlay">    
           <androidx.appcompat.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:textAppearance="@style/ToolbarStyle"
            android:textColor="@color/White"
            app:layout_scrollFlags="scroll|enterAlwaysCollapsed"
            />

        <com.google.android.material.appbar.CollapsingToolbarLayout
            android:id="@+id/layout_toolbar_collapsing"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:layout_behavior="@string/appbar_scrolling_view_behavior"
            app:layout_scrollFlags="scroll|enterAlwaysCollapsed">
            
            <!-- or ConstraintLayout -->
            <LinearLayout
                    android:id="@+id/layout_desc_header"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="?attr/actionBarSize"
                    android:background="@drawable/bg_stroke_rounded_corner"
                    android:orientation="vertical"
                    app:layout_behavior="@string/appbar_scrolling_view_behavior"
                    android:padding="@dimen/padding_small">
                    
                ,,,,contents
                
            </LinearLayout>
            
            
         </com.google.android.material.appbar.CollapsingToolbarLayout>
      </com.google.android.material.appbar.AppBarLayout>
        ...body contents..
       
    </androidx.coordinatorlayout.widget.CoordinatorLayout>
```

24. When you put autocompletetextview to show dropdown right after a new page is open. App can crash, delay the view then show dropdown. (view.postdelayed)  

25. Updating the app needs REQUEST_INSTALL_PACKAGES permission (normal not runtime) manifest.xml

26. Not All places are supported with 3d Buildings on Google Map, oer 2021/06/02

27. Android Studio is currently not stable for Mac Big Sur with M1 Chip. It affects Emulator and the Terminal. Use the Arctic Fox. Still Beta per 2021 June 25'

28. Use Emulator with arm64 processor when you are using Mac with M1 Chip.

29. Another issue on using Room with M1 Chip Android Studio per 2021/06/28

https://issuetracker.google.com/issues/174695268?pli=1

https://www.reddit.com/r/androiddev/comments/lotgzg/room_database_in_intellij_idea_apple_silicon/

https://youtrack.jetbrains.com/issue/DBE-12342 

30. Use STABLE Version of Gradle to integrate with Dependency Injection Libraries like Hilt

31. ```git rm --cached path/to/file``` is to remove committed file that is in .gitignore

32. Use `mutableStateListOf<T>` to make your composables recompose.
