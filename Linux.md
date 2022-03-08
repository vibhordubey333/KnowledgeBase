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
  - apt list
  - apt remove package_name
  - apt purge pacakge_name
  - apt auto-remove
  - apt update
* Killing process running on particular port:
  - fuser -k 80/tcp
