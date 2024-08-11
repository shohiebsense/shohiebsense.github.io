you have to add EDITOR or VISUAL, or else you got:

```bash
No $VISUAL or $EDITOR to open file in. Assign one like this:

VISUAL="mate --wait" bin/rails credentials:edit

For editors that fork and exit immediately, it's important to pass a wait flag;
otherwise, the file will be saved immediately with no chance to edit.
```

for `EDITOR` you can use `nano, vim, joe, micro`  

for `VISUAL` example: `code` (`vscode`), just put in the .zshrc or system environment variables, it wouldn't hurt  

```bash
export EDITOR="code --wait"
```

if you also didnt install the code as bash, it just saves without opening the decrypted `credentials.yml.enc`  

```bash
user@usernoMacBook-Pro my_project % EDITOR="code --wait" rails credentials:edit
Editing config/credentials.yml.enc...
File encrypted and saved.
```

just pops up like that and nothing happened.  

so, make sure you already installed the `Shell command: Install 'code' command in PATH` (`command+shift+p`) 

`master.key` and `credentials.yml.enc` are located in rootProject/config/ directory  

put the master.key as an env variable. 

```
RAILS_MASTER_KEY=0abcdefghi5f0b17f6496c80f6b2fd40b
```

if you got the wrong key, or using your newly generated master.key, it would show like this

```bash
user@usernoMacBook-Pro my_project % rails credentials:edit
Adding config/master.key to store the encryption key: 3bace003d61bf398862707f7d53750da

Save this in a password manager your team can access.

If you lose the key, no one, including you, can access anything encrypted with it.

      create  config/master.key

Editing config/credentials.yml.enc...
Couldn't decrypt config/credentials.yml.enc. Perhaps you passed the wrong key?
```

