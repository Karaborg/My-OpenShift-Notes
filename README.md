# Welcome
This is me taking notes on GitHub while learning `OpenShift`. I will probably be going to need this document when I forget how docker works. If you find something useful, be my guest. I will try to update this whenever I study.

# Setup
- Download VirtualBox
- Download Minishift from [here](https://github.com/minishift/minishift/releases)
- Open console and go path where you download Minishift
- Enter the command below:
  `minishift.exe start --vm-driver virtualbox`
- After the command is done, you will be able to see web conlose IP, user and password.

> Make sure your ***VT-X/AMD-v*** is enabled on your bios.
> If you still have an issue after enabling ***VT-X/AMD-v***, you also need to enable `Virtual Machine Platform` and `Windows Hypervisor Platform` from ***Windows Features***.
> If that didn't work, open console, enter the command `bcdedit` and check if `hypervisorlaunchtype` is auto or on. If so, disable it by entering the command `bcdedit /set hypervisorlaunchtype off` and restart your computer.

# Manage OpenShift
You can manage OpenShift by ***Web Console***, ***CLI*** and ***REST API***

> To access web console, default port is **8443**.

## Basic OpenShift CLI Commands:
```
# To login
oc login <OPENSHIFT_URL>

# To login with username and password
oc login <OPENSHIFT_URL> -u <USERNAME> -p <PASSWORD>

# To logout
oc logout

# To login with octool, set the oc path
minishift oc-env # will return SET command, run the command and then
oc login -u system:admin

# get user token
oc whoami -t

# list projects
oc get projects

# list users
oc get users

# to create administor user
# create a user by loginnig with the username from web console
oc get users
oc adm policy add-cluster-role-to-user cluster-admin <USER>

# to rollback
oc rollout latest dc/<DEPLOYMENT_NAME>

oc rollout history dc/<DEPLOYMENT_NAME>

oc rollout describe dc <DEPLOYMENT_NAME>

oc rollout undo dc/<DEPLOYMENT_NAME>

# get pod IP's
oc get pods -o wide
```

## OpenShift REST API
You can access it by using the below command:
```
curl https://<IP>:<PORT>/oapi/v1/users \
    -H "Authorization: Bearer <TOKEN>"
```

> To get the token, use the command `oc whoami -t` on CLI.
