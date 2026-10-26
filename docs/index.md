<p align="center">
  <img src="img/favicon.ico" alt="UniOS Logo" width="200">
</p>

# Welcome to the UniOS docs

### What are we doing here?  
Our goal is to provide the Greek student community with a Linux distribution that will be tailored to their needs. That's why we made UniOS a free and open source Arch Linux distribution and many apps to go along with it. 

In those docs you will find the technical explanation for our project; we will explain the architecture and the building pipeline of the OS and of the apps that go along with it. If you want something a bit more light-hearted that targets to explain to a non-technical friend or colleague, you can visit our <a href="https://unios-project.eu" target="_blank">webpage</a>.

### Current list of projects
As of now we have developed the following projects:  

* <a href="https://github.com/open-source-uom/unios-iso" target="_blank">unios-iso</a> – The archiso profile that hosts our ISO code
* <a href="https://github.com/open-source-uom/UniBackpack" target="_blank">UniBackpack</a> – Our downloader for the software used by the departments of the Greek universities to teach each subject.
* <a href="https://github.com/open-source-uom/UniDesk" target="_blank">UniDesk</a> – Our welcomer and helper app that runs on startup to greet the user and make them engage with our community.
* <a href="https://github.com/open-source-uom/UniMate" target="_blank">UniMate</a> – Our web app that serves as a bulk downloader for general use Linux apps.
* <a href="https://github.com/open-source-uom/UniNews" target="_blank">UniNews</a> – Our app that acts as a news aggregator for university news.
* <a href="https://github.com/open-source-uom/unios-update" target="_blank">unios-update</a> – An interactive update notifier & applier for UniOS that assists you with important pre / post update tasks (including a systray applet and extensive CLI).
* <a href="https://github.com/open-source-uom/unios-calamares" target="_blank">unios-calamares</a> – Our system installer
* <a href="https://github.com/open-source-uom/unios-desktop-settings" target="_blank">unios-desktop-settings</a> – Our scripts to make KDE feel like UniOS
* <a href="https://github.com/open-source-uom/UniOS-keyring" target="_blank">UniOS-keyring</a> – The PGP keyring that pacman uses to verify our packages.
* <a href="https://github.com/open-source-uom/unios-applications-meta" target="_blank">unios-applications-meta</a> – A meta package used to ship new apps and urgent fixes between ISO updates.
* <a href="https://github.com/open-source-uom/unios-pkgs" target="_blank">unios-pkgs</a> – The pacman repository (`unios-repo`) that hosts all of our packages.
* <a href="https://github.com/open-source-uom/unios-pkgs-nightly" target="_blank">unios-pkgs-nightly</a> – The testing channel of our pacman repository.
* <a href="https://github.com/open-source-uom/unios-build-automation-scripts" target="_blank">unios-build-automation-scripts</a> – The scripts that build our packages and the ISO on `build.unios-project.eu`.
* <a href="https://unios-project.eu" target="_blank">Our Webpage</a> – This is our landing page that does a less technical introduction for our ecosystem.  
* <a href="https://docs.unios-project.eu" target="_blank">The webpage that you are currently on</a> – This is our documentation page that should be considered part of the workflow if you want to write for us, which we dearly suggest.



### Current list of packages available
The list of packages that are currently maintained in our [repo](https://github.com/open-source-uom/unios-pkgs) is: 
```sh 
unios-repo unibackpack 1.1.0.r17.gc6cd814-1 [installed: 1.1.0.r31.g5bbe803-1]
unios-repo unidesk 1.0-1 [installed]
unios-repo uninews 0.2.1-1 [installed]
unios-repo unios-applications-meta 1.0.0-1 [installed]
unios-repo unios-calamares 3.4.3-1
unios-repo unios-desktop-settings 1.0.0-8
unios-repo unios-keyring 2026.09-1 [installed]
unios-repo unios-update 1.0.0-1
unios-repo unios-update-debug 1.0.0-1
```

### Our current repo: 
Our current repository that runs on GitHub is [unios-repo](https://github.com/open-source-uom/unios-pkgs) and you can add it in your current Linux installation following the guide in our [unios-repo](unios-repo.md) page. 
