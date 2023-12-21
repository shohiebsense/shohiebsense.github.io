Ridiculus requirements / demands can be answered with ridiculous approach.  

So I had came accross the product increment, it is pdf merging, combining different pdf contents into one.  

[Ghostscript](https://www.ghostscript.com/) can do this, but it is not exactly like library and such.

Rather it is an executable command.  

Thankfully golang has this [beauty](https://pkg.go.dev/os/exec)  

Well obviously this is not exclusively in golang  

So the approach will be that you build some string script and make it an executable using `exec`, just like we execute something in our command/shell.

The sample is like this 

`gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=combine.pdf -dBATCH 1.pdf 2.pdf 3.pdf .... x.pdf`. 

so you build that thing.  

Don't forget to install the ghostscript before you ship it, e.g. in Dockerfile

```apk add --no-cache Ghostscript ghostscript-fonts```
