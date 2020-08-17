# Package Management.
* go mod init project_name [Initializes project.]
* go get package_name
* go list -m all [List all the dependencies .]
* go list -m version dependency_name [Will list the dependency version being used.]
* go mod tidy [Remove unsed dependencies]
* GO111MODULE=on/off/auto [To turn off/on/auto GOMOD. In auto mode similary to GO111MODULE=on when you're outside of GOPATH, similarly to GO111MODI ] 

# MongoDB.
* Checkout this solution but first try below command: https://askubuntu.com/questions/856073/mongod-unrecognized-service-mongod-service-is-present-already
* Start mongodb : sudo mongod --fork --logpath /var/log/mongodb.log

# Git Commands.
* git branch -v
* git checkout -b new_branch_name  
* git checkout branch_to_switch
* git status
* git log
* git add .
* git commit -m "your_message"
* git push origin branch_name
* git diff

# Linux
* Killing process by providing process ID: kill 1293
* Killing process by providing process name : pkill firefox
* Running process in background : firefox&
* Find if port is in use : netstat -apn | grep 7777

## Grep and Find
* grep -inr "search_tring"
* grep -inrw "search_string"
* find / -name "file_name_to_search"

## Installing minikube on Antix , host : windows 7

* Disable virtualization(VT-X/AMD-v) and PA-NX in virtual machine . As windows 7 doesn't have VT-X flag if it has in your case disable it.
* sudo apt install conntrack
* sudo minikube start --driver=none

