# ubuntu-cheatsheet

## PS with git branch and new line
```
$ cat ~/.bash_profile
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\]\n$ "
```
* Better move it to .bashrc to auto enable on terminal run from gui
* [look here why](https://askubuntu.com/questions/121073/why-bash-profile-is-not-getting-sourced-when-opening-a-terminal)
## Update VS Code
```
$ cat ~/update-code 
wget https://vscode-update.azurewebsites.net/latest/linux-deb-x64/stable -O /tmp/code_latest_amd64.deb
sudo dpkg -i /tmp/code_latest_amd64.deb
```
## Install local deb pkg with failed deps
```
$ sudo dpkg -i mysql-workbench-community-6.2.5-1ubu1404-amd64.deb 
error! (some deps missing)
ok
$ sudo apt-get update
$ sudo apt-get install -f
$ sudo dpkg -i mysql-workbench-community-6.2.5-1ubu1404-amd64.deb 
```
## view free ram
```
watch -n 5 free -m
```
Note that Linux likes to use any extra memory to cache hard drive blocks. So you don't want to look at just the free Mem. You want to look at the free column of the -/+ buffers/cache: row. 
