# Helm-2-to-Helm-3 

Prerequisites:
check for kubectl version `kubectl version` or `kubectl version --short`
check the helm version `helm version` or `helm version -short`

check the location of helm `which helm`

list the helm charts `helm list`
check the environment objective `kubectl get all`

from helm 2 to 3 upgrade tiller is not present in helm 3. If tiller is deployed in different namespace use `-t` when moving application packages.
check the repo list `helm repo list`

### Installation steps for helm 2to3

#### step 1:

refer to the release page [helm release](https://github.com/helm/helm/releases)

`wget 'paste the link from release page'` and unzip it. Move inside the directory of helm3 and move the helm folder to the appropriate folder follwed by `which helm` with sudo permissions. make sure you are not over riding the folder with helm, should be helm3(example).
example: `sudo mv helm /usr/local/bin/helm3`



check the helm3 version `helm3 version`

#### step 2: plugin installation 

check if any plugin already exist `helm plugin list` and `helm3 plugin list`

install the plugin from [helm 2to3](https://github.com/helm/helm-2to3)

input this command for installation `helm plugin install https://github.com/helm/helm-2to3`

list the plugin install by `helm list`

make sure you are in the right directory to execute the follwing commands.

* moving the configuration of repo list:

`helm3 2to3 help` to check the options for moving the repo.
`helm3 2to3 move --help` migrate v2 configuration in place to helm3.
`helm3 2to3 config --help`
`helm3 2to3 move config --dry-run` this command is to check the components getting configured.
`helm3 2to3 move config`

##### step 3: migration packages

if tiller is installed in different namespace, follow the steps with `-t namespace`.

`helm3 2to3 --help`
`helm3 2to3 convert --help`
`helm3 2to3 convert database --dry-run`
`helm3 2to3 convert database`
`helm list` and `helm3 list` should see the packages in both versions.

#### Test the environment

`kubectl get all` check environment running.
`helm repo update` update the repos.
`helm install wordpress stable/wordpress` check if it is download and installed package in helm3 version.

#### cleanup of helm2

`helm3 2to3 cleanup`
`helm list` list the packages.
`kubectl -n kube-system get pods` tiller will be removed from the list.
`sudo rm -rf /usr/local/bin/helm` remove the older version of helm.
`sudo mv /usr/local/bin/{helm3,helm}`
`which helm` to check the helm folder placed.
`helm version` 









