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
	- If getting below error `-bash: __git_ps1: command not found`
	  Fire -> `curl -o ~/.git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh`
	  Add in ~/.bashrc -> `source ~/.git-prompt.sh`
	
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
* `instramfs` happens because of corruption of memory. 
   To Fix `intramfs` error:
  - Type `df -h` or `blkid`
  - For each partition fire `fsck /dev/sdXX -y`
  - Or press `y` each time getting prompt.
  - Reboot
* Changing password in linux and setting expiration period.
  - `passwd`
  - Setting age of password[Days]`chage -M 9999999 root`
* Creating symbolic links.
  - Soft links: `ln -s /home/name/Documents/MyFolder /home/name/Desktop/MyFolder`
  - Hark links: `ln /home/name/Documents/MyFolder /home/name/Desktop/MyFolder`
  

