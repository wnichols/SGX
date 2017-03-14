# SGX
SGX Getting Started project

To get started go to the SGXStarterKit/vagrant dir and do "vagrant up".
Providing that you have vagrant installed it will create a virtual machine (ubuntu) and install everything you 
need to work with and learn the SGX SDK. The steps that the vagrant up script takes:
1) install an ubuntu (14LTS) 64 box
2) install a bunch of packages needed for compiling and running eclipse
3) setup and start a remote desktop server so you can access it in GUI mode
4) clone the SGX SDK from github
5) build SGX
6) download and install eclipse 4.5.1 in /opt/eclipse
7) install the CDT feature on /opt/eclipse
8) build the SGX eclipse plugin.  I havent't figured out how to install an archive P2 repo yet... but if you want to play with this
   its built in Linux_SGXEclipsePlugin/build_directory/updatesite/sgx-eclipse-plugin/ and you can install it using the eclipse gui.  It isn't
   necessary because we're running the whole SDK in emulation mode.  
9) set up the LD_LIBRARY_PATH so that the samples will run

Now you can "vagrant ssh" to log into the machine.  At this point you should be able to build and run the samples with these instructions:

1) cd /home/vagrant/git/github.com/linux-sgx/sgxsdk/SampleCode/SampleEnclave
2) source /home/vagrant/git/github.com/linux-sgx/sgxsdk/environment
2) SGX_SDK=/home/vagrant/git/github.com/linux-sgx/sgxsdk SGX_MODE=SIM make clean all

This should result in the message: The project has been built in debug simulation mode

Run this app :   ./app

It will produce some debugging output and ask you to enter a char to exit.

To use the vm's desktop to visually debug the samples in eclipse:
If your desktop can run X applications you just need to start eclipse via "/opt/eclipse/eclipse" to have it reflected on your desktop 
via X11forwarding. 
If not connect to the vm at localhost:13389 using the uid/pwd of vagrant/vagrant to see an xfce desktop.  Its pretty minimalistic but
 it has an xterm client whch you can use to start eclipse.

Once eclipse is up:
1) import the general project at /home/vagrant/git/github.com/linux-sgx/sgxsdk/SampleCode/SampleEnclave
2) create a "C++ Application" debug configuration for the app.  Make sure that the LD_LIBRARY_PATH is set to 
   /home/vagrant/git/github.com/linux-sgx/sgxsdk/sdk_libs

Once launched you can debug the SGX application at the application level.  Debugging the SGX libraries is probably pointless in emulation mode.

wcn


