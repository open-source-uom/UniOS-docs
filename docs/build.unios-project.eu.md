<p align="center">
  <img src="../img/favicon.ico" alt="build.unios-project.eu" width="200">
</p>

# build.unios-project.eu
As mentioned in [general workflow](generalworkflow.md) this is our build server, it is our way to maintain a coherence among the building environments of our developers and contributors. This doc is mostly directed at our core members but who knows, you might need it one day.

## How to access the server 
if you want to get your greedy little hands to our supreme computing powerhouse (20EUR VPS) you'll need to talk with the core team through the channels listed [here](generalworkflow.md) and get yourself an SSH key, after that sends the `YOUR_SSH_KEY.pub` and we'll add it in the ssh keys that can access the server. 

## General overview of the server 
The build server has three accounts 

- root (We don't mess with him)

- pkgbuilder (The account that handles the building of the packages)

- isobuilder (The account that triggers the ISO update every month)

You will mostly interface with the `pkgbuilder@build.unios-project.eu` since the root is off limits and the isobuilder is mostly automated.

## pkgbuilder 
Here we explain the workflow to build or test the changes that you made in our repos through the server. There is a repo called `unios-build-automation-scripts` that contains a few scripts that automate the building process of the packages. 

To update a package in `unios-repo` with recent changes you will utilize `unios-build-automation-scripts/src/pkgbuilder/build.sh` you will append the name of the package that you want to update and the process will go through mostly automatically, the only thing that you will need is the passphrase for the signing key that will be given to you upon issuing access to the server.

To test a branch of package that you are making, well more specifically to test the binary `.pkg.tar.zst` you will use `unios-build-automation-scripts/src/pkgbuilder/test.sh` instead. You append the name of the package and then the branch that you want to build (`test.sh <package-name> <branch-name>`). The script checks out that branch and builds the package with `makepkg`, but it does **not** upload anything to `unios-repo`, so you can safely install and test the result.

### **REMEMBER**: Once you use the `build.sh` you are actually uploading directly to production (`unios-repo`) and your changes will be directly available to our users, so please make sure that you tested your package and utilize the `test.sh` alongside with repo-specific testing procedures. 

## isobuilder 
The `isobuilder` account builds the UniOS ISO from the [unios-iso](https://github.com/open-source-uom/unios-iso) repo, which is an `archiso` profile (the `archlive/` folder). The scripts for it live in `unios-build-automation-scripts/src/isobuilder/`:

- `build-iso.sh` pulls the `main` branch of `unios-iso`, builds the ISO with `mkarchiso` and uploads it to the server that hosts our downloads. The ISO is not public yet at that point, someone with access to the download server still has to move it to the serving directory.

- `create-test-iso.sh` does the same build but does not upload the ISO, so you can test your changes before they are released. The ISO ends up in `/home/isobuilder/unios-iso/out/`.

The ISO pulls our own packages from `unios-repo`, so if you changed a package make sure it was built with `build.sh` before you build an ISO.
