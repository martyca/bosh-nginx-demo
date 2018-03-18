# bosh-nginxdemo-release
Vmug 2018 bosh demo

This demo is used in the NLVMUG talk deploying like google. http://sched.co/E1wN

## Prerequisites
if you wish to replicate the demo you will want to do the following:

1. install a bosh director on a vpshere instance. ive written a deployment assistent that can help with that:
https://github.com/martyca/bosh-initiator
2. install stemcells, preferably 2 one of which must be ubuntu version 3541.2 and the other must be ubuntu but newer, from http://bosh.cloudfoundry.org/stemcells/
3. at the time of writing this demo the nginx release does not make proper use of "links" my colleague Christiaan Roeleveld has remedied this and his pull request has been merged, unfortunately there has not yet been a build released with this merge included. you can buid your own initiating the included nginx-release submodule.
from within this repo run:
```
git submodule init 
git submodule update
```
cd into nginx-release, and build your own release by executing the following command:
```
bosh create-release --force --tarball=../nginx.tgz
```
this will create the nginx.tgz release build in the folder below the repository.
you can then upload the build by running:
```
bosh -e <your_environment> upload-release ./nginx.tgq
```

## Demo's
1. Deploying software:
Deploy by cloning this repository cd'ing into it and running:
```
bosh -e <your_environment> -d nginx deploy ./nginx.yml
```
2. Day 2 operations: 
edit the nginx.yml file, change the version of the ubuntu stemcell from ```3541.2``` to ```latest```
redeploy the deployment by rerunning the same deployment command as before:
```
bosh -e <your_environment> -d nginx deploy ./nginx.yml
```
3. Ressurector:
simply shutdown one of the vm's in your hypervisor and watch bosh repair the deployment by lovingly destroying the uncooperative vm and rebuilding it.

