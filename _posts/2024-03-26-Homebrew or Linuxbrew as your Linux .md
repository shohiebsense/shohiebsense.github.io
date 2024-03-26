One of the reason I choose homebrew or linuxbrew as the main package manager in my machine's OS is that  

The python has the latest possible of python3.  

Compared to package manager that relies on distros. Brew is superior bro.  

The cons of this is that it cannot run using root.

You have to add a user, make the user able to execute sudo.  

Install it, and after that, read the instructions to add the brew and all of them packages installed be added to `$PATH`  

Next if you want the root able to use homebrew's installed packages, just add their homebrew path in the user root's environment variables, let's say in `.bashrc`  

```.bashrc
export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"

export LD_LIBRARY_PATH="/home/linuxbrew/.linuxbrew/lib:$LD_LIBRARY_PATH"
```

just check it, or restart it for ensuring the effect 
