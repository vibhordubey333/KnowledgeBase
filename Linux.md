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
	- If getting below error `-bash: __git_ps1: command not found` <br/>
	  Fire -> `curl -o ~/.git-prompt.sh https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh` <br/>
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
* Removing Unused libraries/packages
  ``` 
   sudo apt-get autoclean #to clean up outdated package deb files
   sudo apt-get autoremove #to remove any unused dependencies
   sudo apt-get clean #to clean up apt cache
   ```
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
  
* Installing applications in Linux
  - Download .tgz / archive
  - Untar it.
  - cp -vfr some_dir/our_inteneded_file /usr/local/ /usr/bin/
  - Add entry in ~/.bashrc or profile file. [I prefer .bashrc]
    `# Adding JMeter path
     export PATH=$PATH:/usr/local/apache-jmeter-5.1.1/bin/`
  - Exit terminal then re-launch again.
* Enabling SSH server in Debian
  - sudo apt update 
  - sudo apt install openssh-server
  - sudo systemctl status ssh
  - sudo ufh allow ssh
  - ip a
* .vimrc File Creation. Launch Vim then create accordingly
   ```
     :e $HOME/.vimrc  " on Unix, Mac or OS/2
     :e $HOME/_vimrc  " on Windows
     :e s:.vimrc      " on Amiga
   ```
* Provide admin access to existing user
   - su root 
   - nano /etc/sudoers
   - Then add the user below admin user like below syntax.
   - user_name ALL=(ALL)  ALL
 
