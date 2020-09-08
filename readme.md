Apply the ARM template (ref: https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell)
This will give you a VM, NSG and so on.

Unfortunately the guest configuration is manual. Time permitting, I would have done something with chef, Azure extensions or a gold image kind of thing, depending on requirements.

Install postgres and go on the guest by running the following as root:
 apt update
 apt upgrade
 apt install postgresql

The version of go that is current for Ubuntu doesn't work with the app, so run the following as a regular user:

$ wget https://dl.google.com/go/go1.13.3.linux-amd64.tar.gz
$ tar xf ~/go1.13.3.linux-amd64.tar.gz
$ export PATH=$PATH:~/go/bin

Then clone and build the app. Use the conf.toml in this repo.
Set the password for postgres (to something other than the default :)
Then run it; port 3000 should already be open through the NSG.

Test by hitting $whatever_the_ip_address_is:3000 with a web browser; the app should appear