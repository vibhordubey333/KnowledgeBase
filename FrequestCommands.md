# Package Management In Golang.
* go mod init project_name [Initializes project.]
* go get package_name
* go list -m all [List all the dependencies .]
* go list -m version dependency_name [Will list the dependency version being used.]
* go mod tidy [Remove unsed dependencies]
* GO111MODULE=on/off/auto [To turn off/on/auto GOMOD. In auto mode similary to GO111MODULE=on when you're outside of GOPATH, similarly to GO111MODI ] 
* GOOS=linux GOARCH=amd64 go build -o main main.go
* To fix issue "410 Gone" in GO mod
   `export GO111MODULE=on && export GOPROXY=direct && export GOSUMDB=off`

# MongoDB.
* Checkout this solution but first try below command: https://askubuntu.com/questions/856073/mongod-unrecognized-service-mongod-service-is-present-already
* Start mongodb : sudo mongod --fork --logpath /var/log/mongodb.log

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

## Session in Linux
* Check session : who 
* Detailed information : w
* If multiple users are using like liteide then : pkill liteide
* To crash other people session identify shell they are using then: pkill bash
* Delete bash history: rm ~/.bash_history

## Removing and Installing packages in Linux.
* sudo apt-get remove golang-1.6-src
* dpkg --list | grep golang-1.6-src
* dpkg -i package_to_install

## Grep and Find
* grep -inr "search_tring"
* grep -inrw "search_string"
* find / -name "file_name_to_search"

## Dpkg fix.
* sudo dpkg --configure -a   [Instruct dpkg to fix iteself.]
  - sudo apt-get -f install  [Correct dependecies problem.]
  - sudo apt install libavahi-glib1 --reinstall [Reinstall the problamatic package.]

## Installing minikube on VirtualMachine(Os: Antix) , Host : windows 7

* Disable virtualization(VT-X/AMD-v) and PA-NX in virtual machine . As windows 7 doesn't have VT-X flag if it has in your case disable it.
* sudo apt install conntrack
* sudo minikube start --driver=none

## K8s commands.

* kubectl exec -tin test mongoPodName -- mongo
* kubectl port-forward -n test service/sfc-service 10128:10128 --address=0.0.0.0
* kubectl get po --all-namespaces |  grep auth
* kubectl get pods --namespace namespace_name  [To search in a particular namespace]
* kubectl describe pods --namespace namespace_name [To describe all pods from a namespace]
* kubectl describe pods pod-name --namespace namespace-name [To describe a specific pod.] 
* kubectl get pods --namespace namespace_name --watch  [To search in a particular namespace and watch them as there status change]
* kubectl delete pv -n imec-test [Deleting persistant volume.]
* kubectl delete pod pod-name --namespace namespace_name
* kubectl delete pod pod_name
* Kubernetes error "The connection to the server <host>:6643 was refused:"
  - sudo -i && swapoff -a && exit
  - strace -eopenat kubectl version
* kubectl logs pod_name -n namespace_name > log.txt
* Notes:
  - If pods status is in eviceted status, deleting pod may fix it. <span style="color:red">`kubectl delete po -n name_space pod_name`</span>

# HelmChart
* helm uninstall test -n test && helm uninstall test -n imec-test

# Docker.
* To save an Image locally as tar : docker save hello-world > hello-world.tar 
* To extract above tar : tar -xfv hello-world.tar'
* docker images
* docker rmi -f image_name
* docker container ls -a
* docker container stop container_name
* docker container prune
* docker-compose up
* docker-compose up [Detached Mode]
* docker exec -it container_name /bin/bash
* docker build -f build/Dockerfile -t tag_name
* docker-compose ps [To List All The Containers]
* docker-compose -f build/docker-compose.yml up -d 
* docker run -d -p 127.0.0.1:7777 filemgmt:latest
* docker-compose rm
* Push images to private docker registry.
  - docker tag ubuntu altimauthserver.com:6010/ubuntu
  - docker push altimauthserver.com:6010/ubuntu
* docker info
* docker tag image_name new_image_tag_name
* Debug mongodb inside container 
  - docker exec -it mongoservice mongo
  
# Kompose Tool.
* chmod +x kompose_binary_name
* ./kompose -f ./build/docker-compose.yml convert .

# Swagger.
* ./swagger_windows_amd64 generate server -f ./api/sfc_swagger.yml -A sfc

# Windows Commands(Win 10)

* For checking if the port is being used by another process it returns with PID -> netstat -a -n -o | findstr :8085
* Fireup powershell 
  - Get-NetTCPConnection -LocalPort 9091 | Format-Table -Property LocalAddress, LocalPort, State, OwningProcess
  - taskkill /F /PID 17484

# VSCode [Golang Settings For Faster Suggestions.]
* Paste below settings in settings.json, important is language server settings.
  {
    "editor.formatOnPaste": true,
    "editor.formatOnSave": true,
    "window.zoomLevel": 3,
    "go.useLanguageServer": true
   }
* For setting up bash as your default terminal, mention settings in settings.json
  {
  //   "go.toolsManagement.autoUpdate": true,
  "terminal.integrated.profiles.windows": {
    "My Bash": {
      "path": "D:\\1. Installed_Software\\Git\\bin\\bash.exe",
    }
  },
  "terminal.integrated.defaultProfile.windows": "My Bash",
}
#Linux Tweaks
* Configuring nameserver if ubuntu server is not rechable.
  https://askubuntu.com/questions/91543/apt-get-update-fails-to-fetch-files-temporary-failure-resolving-error
  
# Termux
  pkg install wget      
       
# Installing Kali Linux WSL2
  - 1. Install kali linux from microsoft store.
  - 2. sudo apt update && sudo apt upgrade -y
  - 3. sudo apt install kali-desktop-xfce -y
  - 4. sudo apt install xrdp -y
  - 5. sudo service xrdp start
  - 6. ip addr
  - 7. Use RDP to connect. 
# Metasploit
  - sudo apt install metasploit-framework postgresql
  - msfconsole
  
