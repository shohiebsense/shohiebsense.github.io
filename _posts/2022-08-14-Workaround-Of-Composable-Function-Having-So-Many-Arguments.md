1. Either you can use Interface and delegate (implement) it to viewModel (act as a Contract) or  
2. Make a class but initialize inside viewModel, `val` is much preferred 

viewModel itself has already been `remembered`, so the class no need to be `remembered` either  

Either I have to accept the fact that initialize `mutableState` is ugly inside a class or just get over it with those number of arguments
