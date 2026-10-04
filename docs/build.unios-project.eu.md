<p align="center">
  <img src="../img/favicon.ico" alt="build.unios-project.eu" width="200">
</p>

# build.unios.project.eu
As mentioned in [general workflow](generalworkflow.md) this is out build server, it is our way to maintain a coherence among the building environments of our developers and contributors. This doc is mostly directed at our core members but who knows, you might need it one day.

## How to access the server 
if you want to get your greedy little hands to our supreme computing powerhouse (20EUR VPS) you'll need to talk with the core team throught the channels listed [here](generalworkflow.md) and get your self an SSH key, after that sends the `YOUR_SSH_KEY.pub` and we'll add it in the ssh keys that can access the server. 

## General overview of the server 
The build server has three accounts 

- root (We don't mess with him)

- pkgbuilder (The account that handles the building of the packages)

- isobuilder (The account that triggers the ISO update every month)

You will mostly interface with the `pkgbuilder@build.unios-project.eu` since the root is off limits and the isobuilder is mostly automated.

## pkgbuilder 
Here we explain the workflow to build or test the changes that you made in our repos through the server. There is a repo called `unios-build-autmation-scripts` that contains a few scripts that automate the building process of the packages. 

To update a package in `unios-repo` with recent changes you will utilize `unios-build-automation-scripts/src/build.sh` you will append the name of the package that you want to update and the process will go through mostly automatically, the only thing that you will need is the passphrase for the sighning key that will be given to you upon issueing access to the server.

To test a branch of package that you are making, well more specifically to test the binary `.pkg.tar.zst` you will follow the same exacty process but you will appened the branch that you want to build and then the process will continue the same as above.

### **REMEMBER**: Once you use the `build.sh` you are actually uploading directly to production (`uios-repo`) and your changes will be directly avaiable to our users, so please make sure that you tested your package and utilize the `test.sh` alongside with repo-specific testing procedures. 

## isobuilder 
*to be written*
