There is already a python in xcode, but it is not included in $PATH.  

In short, u choose the one(s) that are installed on homebrew.  

then when it comes to confusing which pip you use, just use the project based, the `.venv` one.  

if you use the python plugin on vscode, it provides the initialization.  

or initialize it using bash. 

```sh
python3 -m venv .venv
```

then you can execute the `.venv` activation  

```sh
source .venv/bin/activate 
# or
.venv\Scripts\activate.bat  

```

then install import you would like. 


then deactivate when you are done.  

```sh
deactivate
```

also keep in mind that if you use `python3`, then u use `pip3` as well. 
