# bosh-nginxdemo-release
Vmug 2018 bosh demo

This demo is used in the NLVMUG talk deploying like google. http://sched.co/E1wN

## Prerequisites
if you wish to replicate the demo you will want to do the following:

1. install a bosh director on a vpshere instance. ive written a deployment assistent that can help with that:
https://github.com/martyca/bosh-initiator
2. install stemcells, preferably 2, from http://bosh.cloudfoundry.org/stemcells/
3. at the time of writing this demo the nginx release does not make proper use of "links" my colleague Christiaan Roeleveld has remedied this and his pull request has been merged, unfortunately there has not yet been a build released with this merge included. you can buid your own by cloning the nginx-release repository,
https://github.com/cloudfoundry-community/nginx-release
cd'ing into the repo dir, and building your own release by executing the following command:
```
bosh create-release --force --tarball=../nginx.tgz
```
this will create the nginx.tgz release build in the folder below the repository.
you can then upload the build by running:
```
bosh -e <your_environment> upload-release ./nginx.tgq
```

## Demo's
1. Deploy the deployment by cloning this repository cd'ing into it and running:
```
bosh -e <your_environment> -d nginx deploy ./nginx.yml
'''
2. edit the nginx.yml file to 
