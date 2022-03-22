# Linux
* Killing process by providing process ID: kill 1293
* Killing process by providing process name : pkill firefox
* Running process in background : firefox&
* Find if port is in use : netstat -apn | grep 7777
* scp file_name root@172.90.91.120:/tmp
* Displaying branch name in linux terminal:
  1. vim ~/.bashrc
  2. Paste in bashrc file
  	```
	export GIT_PS1_SHOWDIRTYSTATE=true
	export GIT_PS1_SHOWUNTRACKEDFILES=true
	export PS1='\[\033[32m\]\u@\h\[\033[00m\]:\[\033[34m\]\w\[\033[31m\]$(__git_ps1)\[\033[00m\]\$ '
  	```
  3. source ~/.bashrc
  4. Add cyclic reverse search in linux:
  	```
		add-apt-repository ppa:ultradvorka/ppa
		apt-get update
		apt-get install hstr
		hstr --show-configuration >> ~/.bashrc
	```
* Fixing broken dependencies in linux:
     `sudo apt --fix-broken install`
* Uninstalling/Removing packages:
  - List all the packages`apt list`
  - Remove package `apt remove package_name`
  - Remove related files to the package`apt purge pacakge_name`
  - Search for left out binaries `whereis firefox`
  - Automatically removing unused dependecies `apt auto-remove`
  - sudo apt update && sudo apt upgrade
* Killing process running on particular port:
  - fuser -k 80/tcp
* When writing data is not important redirect to `/dev/null`
