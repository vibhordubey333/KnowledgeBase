# Kubernetes Commands Cheat Sheet

A comprehensive reference guide for all Kubernetes commands used in this project and general Kubernetes operations.

---

## Table of Contents

1. [Basic Commands](#basic-commands)
2. [Context & Configuration](#context--configuration)
3. [Namespace Operations](#namespace-operations)
4. [Pod Operations](#pod-operations)
5. [Deployment Operations](#deployment-operations)
6. [Service Operations](#service-operations)
7. [Resource Inspection](#resource-inspection)
8. [Logs & Debugging](#logs--debugging)
9. [Scaling & Updates](#scaling--updates)
10. [Resource Management](#resource-management)
11. [Label & Selector Operations](#label--selector-operations)
12. [Port Forwarding](#port-forwarding)
13. [Exec & Shell Access](#exec--shell-access)
14. [Events & Monitoring](#events--monitoring)
15. [Job & CronJob Operations](#job--cronjob-operations)
16. [Node Operations](#node-operations)
17. [RBAC & Security](#rbac--security)
18. [ConfigMap & Secrets](#configmap--secrets)
19. [EKS-Specific Commands](#eks-specific-commands)
20. [Additional Useful Commands](#additional-useful-commands)
21. [Useful One-Liners](#useful-one-liners)

---

## Basic Commands

### Get Resources
```bash
# Get all resources in current namespace
kubectl get all

# Get all resources in specific namespace
kubectl get all -n goapp

# Get specific resource type
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get namespaces

# Get with wide output (more columns)
kubectl get pods -o wide

# Get in all namespaces
kubectl get pods --all-namespaces
kubectl get pods -A

# Get with custom columns
kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName

# Get in YAML format
kubectl get pod <pod-name> -o yaml

# Get in JSON format
kubectl get pod <pod-name> -o json

# Get with labels
kubectl get pods --show-labels

# Get with label selector
kubectl get pods -l app=goapp
kubectl get pods -l 'app in (goapp,myapp)'
kubectl get pods -l 'app=goapp,version=v1'
```

### Describe Resources
```bash
# Describe a pod
kubectl describe pod <pod-name>
kubectl describe pod <pod-name> -n goapp

# Describe a deployment
kubectl describe deployment goapp
kubectl describe deployment goapp -n goapp

# Describe a service
kubectl describe service goapp
kubectl describe svc goapp -n goapp

# Describe a namespace
kubectl describe namespace goapp

# Describe all resources of a type
kubectl describe pods -l app=goapp
```

### Current Context
```bash
# Show current context
kubectl config current-context

# List all contexts
kubectl config get-contexts

# Switch context
kubectl config use-context <context-name>

# Set default namespace for current context
kubectl config set-context --current --namespace=goapp
```

---

## Context & Configuration

### View Configuration
```bash
# View current config
kubectl config view

# View specific context
kubectl config view --context=<context-name>

# Get cluster info
kubectl cluster-info

# Get cluster version
kubectl version

# Check if kubectl can connect
kubectl get nodes

# List API resources
kubectl api-resources

# List API versions
kubectl api-versions

# Explain resource fields
kubectl explain pod
kubectl explain pod.spec
kubectl explain pod.spec.containers
```

### Namespace Context
```bash
# Set namespace for current context
kubectl config set-context --current --namespace=goapp

# View current namespace
kubectl config view --minify | grep namespace

# Create alias for namespace (add to ~/.bashrc or ~/.zshrc)
alias kg='kubectl get'
alias kga='kubectl get all'
alias kd='kubectl describe'
alias kl='kubectl logs'
alias ke='kubectl exec'
```

---

## Namespace Operations

### Create & Delete
```bash
# Create namespace
kubectl create namespace goapp
kubectl apply -f k8s/namespace.yaml

# Delete namespace (deletes all resources in it!)
kubectl delete namespace goapp

# Get namespaces
kubectl get namespaces
kubectl get ns

# Describe namespace
kubectl describe namespace goapp
```

### Switch Namespace
```bash
# Set default namespace
kubectl config set-context --current --namespace=goapp

# Use namespace flag
kubectl get pods -n goapp

# Create namespace context alias
kubectl config set-context goapp-context --namespace=goapp --cluster=<cluster> --user=<user>
```

---

## Pod Operations

### Get Pods
```bash
# List pods
kubectl get pods
kubectl get pods -n goapp

# List pods with more info
kubectl get pods -o wide

# List pods with labels
kubectl get pods --show-labels

# List pods by label
kubectl get pods -l app=goapp
kubectl get pods -l 'app in (goapp,myapp)'

# List pods in all namespaces
kubectl get pods -A

# Watch pods (real-time updates)
kubectl get pods -w
kubectl get pods -w -n goapp
```

### Pod Details
```bash
# Describe pod
kubectl describe pod <pod-name>
kubectl describe pod <pod-name> -n goapp

# Get pod YAML
kubectl get pod <pod-name> -o yaml

# Get pod JSON
kubectl get pod <pod-name> -o json

# Get pod status
kubectl get pod <pod-name> -o jsonpath='{.status.phase}'

# Get pod IP
kubectl get pod <pod-name> -o jsonpath='{.status.podIP}'

# Get pod node
kubectl get pod <pod-name> -o jsonpath='{.spec.nodeName}'
```

### Pod Actions
```bash
# Delete pod
kubectl delete pod <pod-name>
kubectl delete pod <pod-name> -n goapp

# Delete pods by label
kubectl delete pods -l app=goapp

# Force delete pod (if stuck)
kubectl delete pod <pod-name> --grace-period=0 --force

# Restart pod (delete and let deployment recreate)
kubectl delete pod <pod-name>
```

---

## Deployment Operations

### Get Deployments
```bash
# List deployments
kubectl get deployments
kubectl get deploy
kubectl get deploy -n goapp

# List with labels
kubectl get deployments --show-labels

# List by label
kubectl get deployments -l app=goapp
```

### Deployment Details
```bash
# Describe deployment
kubectl describe deployment goapp
kubectl describe deploy goapp -n goapp

# Get deployment YAML
kubectl get deployment goapp -o yaml

# Get deployment status
kubectl get deployment goapp -o jsonpath='{.status.conditions}'

# Get deployment selector
kubectl get deployment goapp -o jsonpath='{.spec.selector.matchLabels}'

# Get deployment replicas
kubectl get deployment goapp -o jsonpath='{.spec.replicas}'
kubectl get deployment goapp -o jsonpath='{.status.replicas}'
```

### Deployment Actions
```bash
# Create deployment
kubectl apply -f k8s/deployment.yaml
kubectl create -f k8s/deployment.yaml

# Update deployment
kubectl apply -f k8s/deployment.yaml

# Delete deployment
kubectl delete deployment goapp
kubectl delete deployment goapp -n goapp

# Scale deployment
kubectl scale deployment goapp --replicas=3
kubectl scale deployment goapp --replicas=3 -n goapp

# Rollout status
kubectl rollout status deployment/goapp
kubectl rollout status deploy/goapp -n goapp

# Rollout history
kubectl rollout history deployment/goapp

# Rollback to previous version
kubectl rollout undo deployment/goapp

# Rollback to specific revision
kubectl rollout undo deployment/goapp --to-revision=2

# Pause rollout
kubectl rollout pause deployment/goapp

# Resume rollout
kubectl rollout resume deployment/goapp

# Restart deployment (rolling restart)
kubectl rollout restart deployment/goapp
```

### Update Deployment
```bash
# Update image
kubectl set image deployment/goapp goapp=myimage:v2.0

# Update environment variable
kubectl set env deployment/goapp ENV_VAR=value

# Update resource limits
kubectl set resources deployment/goapp --limits=cpu=500m,memory=256Mi

# Update replicas
kubectl scale deployment goapp --replicas=5
```

---

## Service Operations

### Get Services
```bash
# List services
kubectl get services
kubectl get svc
kubectl get svc -n goapp

# List with labels
kubectl get services --show-labels

# List by label
kubectl get services -l app=goapp
```

### Service Details
```bash
# Describe service
kubectl describe service goapp
kubectl describe svc goapp -n goapp

# Get service YAML
kubectl get service goapp -o yaml

# Get service selector
kubectl get service goapp -o jsonpath='{.spec.selector}'

# Get LoadBalancer external IP
kubectl get service goapp -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'
kubectl get service goapp -o jsonpath='{.status.loadBalancer.ingress[0].ip}'

# Get service endpoints
kubectl get endpoints goapp
kubectl get ep goapp -n goapp
```

### Service Actions
```bash
# Create service
kubectl apply -f k8s/service.yaml
kubectl create -f k8s/service.yaml

# Delete service
kubectl delete service goapp
kubectl delete svc goapp -n goapp

# Expose deployment as service
kubectl expose deployment goapp --type=LoadBalancer --port=80 --target-port=8080
```

---

## Resource Inspection

### Get All Resources
```bash
# Get all resources in namespace
kubectl get all -n goapp

# Get all resources with labels
kubectl get all --show-labels -n goapp

# Get all resources in all namespaces
kubectl get all -A
```

### Resource Details
```bash
# Get resource in YAML
kubectl get <resource-type> <name> -o yaml

# Get resource in JSON
kubectl get <resource-type> <name> -o json

# Get resource with custom format
kubectl get <resource-type> <name> -o jsonpath='{.spec.replicas}'

# Get multiple resources
kubectl get pod,svc,deploy -n goapp
```

### Resource Types
```bash
# Common resource types
kubectl get pods (po)
kubectl get services (svc)
kubectl get deployments (deploy)
kubectl get replicasets (rs)
kubectl get namespaces (ns)
kubectl get nodes (no)
kubectl get configmaps (cm)
kubectl get secrets
kubectl get persistentvolumes (pv)
kubectl get persistentvolumeclaims (pvc)
kubectl get endpoints (ep)
kubectl get ingress (ing)
kubectl get jobs
kubectl get cronjobs
kubectl get daemonsets (ds)
kubectl get statefulsets (sts)
kubectl get horizontalpodautoscalers (hpa)
kubectl get networkpolicies (netpol)
kubectl get roles
kubectl get rolebindings
kubectl get clusterroles
kubectl get clusterrolebindings
kubectl get serviceaccounts (sa)
```

---

## Logs & Debugging

### View Logs
```bash
# Pod logs
kubectl logs <pod-name>
kubectl logs <pod-name> -n goapp

# Logs from all pods with label
kubectl logs -l app=goapp
kubectl logs -l app=goapp -n goapp

# Follow logs (stream)
kubectl logs -f <pod-name>
kubectl logs -f <pod-name> -n goapp

# Follow logs from all pods with label
kubectl logs -f -l app=goapp

# Previous container logs (if crashed)
kubectl logs <pod-name> --previous

# Logs from specific container in pod
kubectl logs <pod-name> -c <container-name>

# Last N lines
kubectl logs <pod-name> --tail=100

# Logs since time
kubectl logs <pod-name> --since=1h
kubectl logs <pod-name> --since=10m

# Logs with timestamps
kubectl logs <pod-name> --timestamps
```

### Debug Pods
```bash
# Get pod events
kubectl get events -n goapp --sort-by='.lastTimestamp'

# Describe pod (shows events)
kubectl describe pod <pod-name>

# Check pod status
kubectl get pod <pod-name> -o jsonpath='{.status.containerStatuses[0].state}'

# Check pod conditions
kubectl get pod <pod-name> -o jsonpath='{.status.conditions}'

# Check why pod is pending
kubectl describe pod <pod-name> | grep -A 5 Events
```

### Debug Command (Interactive Debugging)
```bash
# Create interactive debugging session in pod
kubectl debug <pod-name> -it --image=busybox

# Create copy of pod with debug container
kubectl debug <pod-name> -it --image=busybox --copy-to=<debug-pod-name>

# Create debugging session on node
kubectl debug node/<node-name> -it --image=busybox

# Debug with specific container
kubectl debug <pod-name> -it --image=busybox --container=<container-name>

# Debug with shared process namespace
kubectl debug <pod-name> -it --image=busybox --share-processes
```

---

## Scaling & Updates

### Scale Resources
```bash
# Scale deployment
kubectl scale deployment goapp --replicas=5
kubectl scale deployment goapp --replicas=5 -n goapp

# Scale with current replicas
kubectl scale deployment goapp --replicas=3 --current-replicas=2

# Scale replicaset
kubectl scale replicaset <rs-name> --replicas=3

# Scale statefulset
kubectl scale statefulset <sts-name> --replicas=3
```

### Autoscaling (HorizontalPodAutoscaler)
```bash
# Create autoscaler for deployment
kubectl autoscale deployment <deployment-name> --min=2 --max=10 --cpu-percent=80

# Create autoscaler for replicaset
kubectl autoscale replicaset <rs-name> --min=2 --max=5 --cpu-percent=80

# Get autoscalers
kubectl get hpa
kubectl get horizontalpodautoscaler

# Describe autoscaler
kubectl describe hpa <hpa-name>

# Delete autoscaler
kubectl delete hpa <hpa-name>

# Get autoscaler YAML
kubectl get hpa <hpa-name> -o yaml
```

### Rolling Updates
```bash
# Check rollout status
kubectl rollout status deployment/goapp

# View rollout history
kubectl rollout history deployment/goapp

# View specific revision
kubectl rollout history deployment/goapp --revision=2

# Rollback to previous
kubectl rollout undo deployment/goapp

# Rollback to specific revision
kubectl rollout undo deployment/goapp --to-revision=2

# Pause rollout
kubectl rollout pause deployment/goapp

# Resume rollout
kubectl rollout resume deployment/goapp

# Restart deployment (rolling restart)
kubectl rollout restart deployment/goapp
```

### Update Resources
```bash
# Apply changes
kubectl apply -f k8s/deployment.yaml
kubectl apply -k k8s/

# Replace resource
kubectl replace -f k8s/deployment.yaml

# Edit resource interactively
kubectl edit deployment goapp
kubectl edit pod <pod-name>

# Patch resource
kubectl patch deployment goapp -p '{"spec":{"replicas":5}}'
```

---

## Resource Management

### Apply & Delete
```bash
# Apply manifest
kubectl apply -f k8s/deployment.yaml
kubectl apply -k k8s/

# Delete resource
kubectl delete -f k8s/deployment.yaml
kubectl delete -k k8s/

# Delete by label
kubectl delete pods -l app=goapp
kubectl delete all -l app=goapp

# Delete all in namespace
kubectl delete all --all -n goapp
```

### Dry Run
```bash
# Dry run (see what would be created)
kubectl apply -f k8s/deployment.yaml --dry-run=client
kubectl apply -f k8s/deployment.yaml --dry-run=server

# Validate YAML
kubectl apply -f k8s/deployment.yaml --validate=true
```

### Diff
```bash
# See differences
kubectl diff -f k8s/deployment.yaml
```

---

## Label & Selector Operations

### View Labels
```bash
# Show labels
kubectl get pods --show-labels
kubectl get pods -L app,version

# Get label value
kubectl get pod <pod-name> -o jsonpath='{.metadata.labels.app}'
```

### Add/Update Labels
```bash
# Add label to pod
kubectl label pod <pod-name> app=goapp

# Add label to deployment
kubectl label deployment goapp version=v1

# Update existing label
kubectl label pod <pod-name> app=myapp --overwrite
```

### Remove Labels
```bash
# Remove label
kubectl label pod <pod-name> app-
```

### Annotations
```bash
# Add annotation
kubectl annotate pod <pod-name> description="My pod"

# Update annotation
kubectl annotate pod <pod-name> description="Updated description" --overwrite

# Remove annotation
kubectl annotate pod <pod-name> description-

# View annotations
kubectl get pod <pod-name> -o jsonpath='{.metadata.annotations}'
```

### Selector Queries
```bash
# Get by label
kubectl get pods -l app=goapp
kubectl get pods -l 'app in (goapp,myapp)'
kubectl get pods -l 'app=goapp,version=v1'
kubectl get pods -l 'app!=goapp'
kubectl get pods -l 'app in (goapp,myapp),version=v1'
```

---

## Port Forwarding

### Forward Ports
```bash
# Forward pod port
kubectl port-forward <pod-name> 8080:8080
kubectl port-forward <pod-name> 8080:8080 -n goapp

# Forward deployment port (picks a pod)
kubectl port-forward deployment/goapp 8080:8080

# Forward service port
kubectl port-forward service/goapp 8080:80

# Forward in background
kubectl port-forward <pod-name> 8080:8080 &

# Forward multiple ports
kubectl port-forward <pod-name> 8080:8080 9090:9090
```

---

## Exec & Shell Access

### Execute Commands
```bash
# Execute command in pod
kubectl exec <pod-name> -- ls -la
kubectl exec <pod-name> -n goapp -- ls -la

# Execute in specific container
kubectl exec <pod-name> -c <container-name> -- ls -la

# Get interactive shell
kubectl exec -it <pod-name> -- /bin/sh
kubectl exec -it <pod-name> -- /bin/bash

# Execute from all pods with label
kubectl exec -l app=goapp -- ls -la
```

---

## Events & Monitoring

### View Events
```bash
# Get events
kubectl get events
kubectl get events -n goapp

# Get events sorted by time
kubectl get events -n goapp --sort-by='.lastTimestamp'

# Watch events
kubectl get events -w

# Get events for specific resource
kubectl get events --field-selector involvedObject.name=<pod-name>
```

### Resource Usage
```bash
# Top nodes
kubectl top nodes

# Top pods
kubectl top pods
kubectl top pods -n goapp

# Top pods with labels
kubectl top pods -l app=goapp

# Top containers
kubectl top pod <pod-name> --containers
```

### Wait for Conditions
```bash
# Wait for pod to be ready
kubectl wait --for=condition=Ready pod/<pod-name> --timeout=60s

# Wait for deployment to be available
kubectl wait --for=condition=Available deployment/goapp --timeout=300s

# Wait for pod deletion
kubectl wait --for=delete pod/<pod-name> --timeout=60s

# Wait for job completion
kubectl wait --for=condition=complete job/<job-name> --timeout=300s
```

---

## Job & CronJob Operations

### Jobs
```bash
# Create job
kubectl create job <job-name> --image=<image> -- <command>
kubectl create job myjob --from=cronjob/my-cronjob

# Get jobs
kubectl get jobs
kubectl get job <job-name>

# Describe job
kubectl describe job <job-name>

# Delete job
kubectl delete job <job-name>

# View job logs
kubectl logs job/<job-name>
kubectl logs -l job-name=<job-name>
```

### CronJobs
```bash
# Create cronjob
kubectl create cronjob <cronjob-name> --image=<image> --schedule="0 0 * * *" -- <command>

# Get cronjobs
kubectl get cronjobs
kubectl get cj

# Describe cronjob
kubectl describe cronjob <cronjob-name>

# Suspend cronjob
kubectl patch cronjob <cronjob-name> -p '{"spec":{"suspend":true}}'

# Resume cronjob
kubectl patch cronjob <cronjob-name> -p '{"spec":{"suspend":false}}'

# Delete cronjob
kubectl delete cronjob <cronjob-name>
```

---

## Node Operations

### Get Nodes
```bash
# List nodes
kubectl get nodes
kubectl get nodes -o wide

# Describe node
kubectl describe node <node-name>

# Get node resources
kubectl top node <node-name>
```

### Node Management
```bash
# Cordon node (mark as unschedulable)
kubectl cordon <node-name>

# Uncordon node (mark as schedulable)
kubectl uncordon <node-name>

# Drain node (evict pods)
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data

# Taint node
kubectl taint nodes <node-name> key=value:NoSchedule

# Remove taint
kubectl taint nodes <node-name> key:NoSchedule-

# View taints
kubectl describe node <node-name> | grep Taint
```

---

## RBAC & Security

### Check Permissions
```bash
# Check if user can perform action
kubectl auth can-i create pods
kubectl auth can-i delete pods --namespace=goapp
kubectl auth can-i '*' '*'

# Check permissions for specific user
kubectl auth can-i create pods --as=system:serviceaccount:default:my-sa
```

### Roles & RoleBindings
```bash
# Get roles
kubectl get roles
kubectl get rolebindings

# Get cluster roles
kubectl get clusterroles
kubectl get clusterrolebindings

# Describe role
kubectl describe role <role-name>
kubectl describe rolebinding <rolebinding-name>

# Create role
kubectl create role <role-name> --verb=get,list --resource=pods

# Create rolebinding
kubectl create rolebinding <rolebinding-name> --role=<role-name> --user=<user-name>
```

### Service Accounts
```bash
# Get service accounts
kubectl get serviceaccounts
kubectl get sa

# Create service account
kubectl create serviceaccount <sa-name>

# Describe service account
kubectl describe serviceaccount <sa-name>

# Delete service account
kubectl delete serviceaccount <sa-name>
```

---

## ConfigMap & Secrets

### ConfigMaps
```bash
# Get configmaps
kubectl get configmaps
kubectl get cm

# Create configmap from file
kubectl create configmap <cm-name> --from-file=<file-path>

# Create configmap from literal
kubectl create configmap <cm-name> --from-literal=key1=value1 --from-literal=key2=value2

# Describe configmap
kubectl describe configmap <cm-name>

# Get configmap YAML
kubectl get configmap <cm-name> -o yaml

# Delete configmap
kubectl delete configmap <cm-name>
```

### Secrets
```bash
# Get secrets
kubectl get secrets

# Create secret from file
kubectl create secret generic <secret-name> --from-file=<file-path>

# Create secret from literal
kubectl create secret generic <secret-name> --from-literal=username=admin --from-literal=password=secret

# Create docker-registry secret
kubectl create secret docker-registry <secret-name> --docker-server=<server> --docker-username=<user> --docker-password=<pass>

# Describe secret
kubectl describe secret <secret-name>

# Get secret value (base64 encoded)
kubectl get secret <secret-name> -o jsonpath='{.data.password}' | base64 -d

# Delete secret
kubectl delete secret <secret-name>
```

---

## EKS-Specific Commands

### Cluster Management
```bash
# List clusters
eksctl get cluster

# Get cluster info
eksctl get cluster --name goapp-eks --region us-east-1

# Update kubeconfig
aws eks update-kubeconfig --name goapp-eks --region us-east-1

# List nodegroups
eksctl get nodegroup --cluster goapp-eks --region us-east-1

# Scale nodegroup
eksctl scale nodegroup --cluster goapp-eks --name goapp-ng --nodes 3 --region us-east-1
```

### ECR Commands
```bash
# Login to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com

# List repositories
aws ecr describe-repositories --region us-east-1

# List images
aws ecr list-images --repository-name goapp --region us-east-1

# Describe images
aws ecr describe-images --repository-name goapp --region us-east-1
```

### IAM & Access
```bash
# Update kubeconfig with IAM role
aws eks update-kubeconfig --name goapp-eks --region us-east-1 --role-arn <role-arn>

# Test access
kubectl get nodes
kubectl get pods
```

---

## Additional Useful Commands

### Explain Resources
```bash
# Explain resource structure
kubectl explain pod
kubectl explain pod.spec
kubectl explain pod.spec.containers
kubectl explain deployment.spec.template.spec.containers

# Get API resource details
kubectl api-resources
kubectl api-resources --namespaced=true
kubectl api-resources --verbs=list,get
```

### Run Pods (Deprecated - Use Deployments Instead)
```bash
# Run a pod (deprecated in favor of deployments)
kubectl run <pod-name> --image=<image> --restart=Never
kubectl run <pod-name> --image=<image> --restart=Always  # Creates deployment

# Run with command
kubectl run <pod-name> --image=<image> --restart=Never -- <command>

# Run with environment variables
kubectl run <pod-name> --image=<image> --env="KEY=value" --restart=Never
```

### Certificate Management
```bash
# Approve certificate signing request
kubectl certificate approve <csr-name>

# Deny certificate signing request
kubectl certificate deny <csr-name>

# Get certificate signing requests
kubectl get csr
```

### Shell Completion
```bash
# Setup bash completion
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc

# Setup zsh completion
source <(kubectl completion zsh)
echo "source <(kubectl completion zsh)" >> ~/.zshrc

# Generate completion script
kubectl completion bash > /etc/bash_completion.d/kubectl
kubectl completion zsh > "${fpath[1]}/_kubectl"
```

### Debugging & Troubleshooting
```bash
# Get resource YAML with status
kubectl get pod <pod-name> -o yaml

# Get resource JSON
kubectl get pod <pod-name> -o json | jq

# Get resource with custom output
kubectl get pod <pod-name> -o jsonpath='{.status.phase}'

# Get all resources of a type
kubectl get all --all-namespaces

# Check resource events
kubectl get events --field-selector involvedObject.name=<pod-name> --sort-by='.lastTimestamp'
```

---

## Useful One-Liners

### Quick Checks
```bash
# Get all pods with their status
kubectl get pods -o wide -n goapp

# Get all resources in namespace
kubectl get all -n goapp

# Get LoadBalancer URL
kubectl get svc goapp -n goapp -o jsonpath='{.status.loadBalancer.ingress[0].hostname}'

# Get pod IPs
kubectl get pods -n goapp -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.podIP}{"\n"}{end}'

# Count pods by status
kubectl get pods -n goapp -o jsonpath='{range .items[*]}{.status.phase}{"\n"}{end}' | sort | uniq -c

# Get all pod names
kubectl get pods -n goapp -o name

# Delete all pods in namespace
kubectl delete pods --all -n goapp

# Get pods on specific node
kubectl get pods -n goapp -o wide --field-selector spec.nodeName=<node-name>
```

### Debugging
```bash
# Get events for failed pods
kubectl get events -n goapp --sort-by='.lastTimestamp' | grep -i fail

# Check pod logs from all pods
kubectl logs -l app=goapp -n goapp --tail=50

# Describe all pods
kubectl describe pods -l app=goapp -n goapp

# Get pod status summary
kubectl get pods -n goapp -o custom-columns=NAME:.metadata.name,STATUS:.status.phase,RESTARTS:.status.containerStatuses[0].restartCount
```

### Resource Management
```bash
# Apply all YAMLs in directory
kubectl apply -f k8s/

# Delete all resources with label
kubectl delete all -l app=goapp -n goapp

# Get resource usage
kubectl top pods -n goapp | sort -k2 -rn

# Export deployment to file
kubectl get deployment goapp -o yaml > deployment-backup.yaml
```

### Service Discovery
```bash
# Get service endpoints
kubectl get endpoints goapp -n goapp

# Test service from pod
kubectl exec <pod-name> -n goapp -- curl http://goapp:80

# Get service cluster IP
kubectl get svc goapp -n goapp -o jsonpath='{.spec.clusterIP}'
```

### Image Management
```bash
# Update deployment image
kubectl set image deployment/goapp goapp=myimage:v2.0 -n goapp

# Get current image
kubectl get deployment goapp -n goapp -o jsonpath='{.spec.template.spec.containers[0].image}'

# List images in all deployments
kubectl get deployments -n goapp -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.template.spec.containers[0].image}{"\n"}{end}'
```

---

## Tips & Best Practices

### Aliases (add to ~/.bashrc or ~/.zshrc)
```bash
alias k='kubectl'
alias kg='kubectl get'
alias kd='kubectl describe'
alias kl='kubectl logs'
alias ke='kubectl exec'
alias ka='kubectl apply'
alias kdel='kubectl delete'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias kgd='kubectl get deployments'
alias kga='kubectl get all'
```

### Output Formats
```bash
# YAML output
kubectl get pod <name> -o yaml

# JSON output
kubectl get pod <name> -o json

# Custom columns
kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase

# JSONPath
kubectl get pod <name> -o jsonpath='{.status.podIP}'

# Go template
kubectl get pods -o go-template='{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
```

### Resource Shortcuts
```bash
# Common shortcuts
po = pods
svc = services
deploy = deployments
rs = replicasets
ns = namespaces
no = nodes
cm = configmaps
ep = endpoints
ing = ingress
```

---

## Quick Reference Card

### Most Used Commands
```bash
# Get resources
kubectl get all -n goapp
kubectl get pods -n goapp
kubectl get svc -n goapp
kubectl get deploy -n goapp

# Describe
kubectl describe pod <name> -n goapp
kubectl describe svc goapp -n goapp

# Logs
kubectl logs -l app=goapp -n goapp -f

# Exec
kubectl exec -it <pod-name> -n goapp -- /bin/sh

# Apply
kubectl apply -k k8s/
kubectl apply -f k8s/deployment.yaml

# Delete
kubectl delete -k k8s/
kubectl delete pod <name> -n goapp

# Scale
kubectl scale deployment goapp --replicas=3 -n goapp

# Rollout
kubectl rollout status deploy/goapp -n goapp
kubectl rollout undo deploy/goapp -n goapp

# Port forward
kubectl port-forward svc/goapp 8080:80 -n goapp
```

---

## Troubleshooting Commands

```bash
# Check pod status
kubectl get pods -n goapp
kubectl describe pod <pod-name> -n goapp

# Check events
kubectl get events -n goapp --sort-by='.lastTimestamp'

# Check logs
kubectl logs <pod-name> -n goapp
kubectl logs <pod-name> -n goapp --previous

# Check service endpoints
kubectl get endpoints goapp -n goapp

# Check deployment status
kubectl rollout status deploy/goapp -n goapp
kubectl rollout history deploy/goapp -n goapp

# Check resource usage
kubectl top pods -n goapp
kubectl top nodes
```

---

---

## Notes

- [Official Kubernetes kubectl Command Reference](https://kubernetes.io/docs/reference/kubectl/)
- [Official Kubernetes kubectl Quick Reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- [Official Kubernetes kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- Kubernetes v1.31 (EKS compatible)

