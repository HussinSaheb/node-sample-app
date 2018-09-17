# Hussin's changes
# Sparta Node Sample App

## Description

This app is intended for use with the Sparta Global Devops Stream as a sample app. You can clone the repo and use it as is but no changes will be accepted on this branch.

To use the repo within your course you should fork it.

The app is a node app with three pages.

### Homepage

``localhost:3000``

Displays a simple homepage displaying a Sparta logo and message. This page should return a 200 response.

### Blog

``localhost:3000/posts``

This page displays a logo and 100 randomly generated blog posts. The posts are generated during the seeding step.

This page and the seeding is only accessible when a database is available and the DB_HOST environment variable has been set with it's location.

### A fibonacci number generator

``localhost:3000/fibonacci/{index}``

This page has be implemented poorly on purpose to produce a slow running function. This can be used for performance testing and crash recovery testing.

The higher the fibonacci number requested the longer the request will take. A very large number can crash or block the process.


### Hackable code

``localhost:3000/hack/{code}``

There is a commented route that opens a serious security vulnerability. This should only be enabled when looking at user security and then disabled immediately afterwards

## Usage

To set up a development environment first head to [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) and download it.

Following that, download vagrant from their website at [https://www.vagrantup.com/downloads.html](www.vagrantup.com/downloads.html)

to run the already setup environment run
```
vagrant up
```

then use the command
```
vagrant ssh
```
which will enter the virtual machines ssh command line.
run
```
sudo apt-get update
```
to update any packages that might need to be updated.

then install nginx on the virtual machine by running the command
```
sudo apt-get install nginx
```

then exit the ssh by using
```
exit
```
Finally use your browser to navigate to the url [development.local/](development.local/)or [192.168.10.100](192.168.10.100)
### If you'd like to install your own environment please follow the bellow instructions

Once both Virtualbox and Vagrant are downloaded. Using your terminal and navigate to your chosen folder and run the command bellow
```
vagrant init ubuntu/xenial64
```
This will initialise a vagrant file in your current directory where you can specify what settings configuration you'd like to specify for your development environment.

Open the file Vagrantfile, and you'll find generated code and comments about how to use the vagrant file to configure the environment. If you ran the above command, then you don't need to change anything as the configurations are correct for our purposes.

Next we need to install any plugins we might need to use. This is done by using the command

```
vagrant plugin install PLUGIN-NAME
```
In our case we'll be using the vagrant-hostsupdater to add new entries to our host file.
```
vagrant plugin install vagrant-hostsupdater
```
Then we need to once again access the Vagrantfile to configure our host address and name.

```
config.vm.network("private_network", ip: "ip_address")
config.hostsupdater.aliases = ["name_address"]
```
The ip_address and name_address can be anything specified, and can be used to access the vm.
these go inside the Vagrant.configure method like so
```
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.network("private_network", ip: "192.168.10.100")
  config.hostsupdater.aliases = ["development.local"]

end
```
Finally, you can run

```
vagrant up
```
From the terminal to actually run the virtual machine.

Then in order to access the virtual machines command line you just have to run
```
vagrant ssh
```
As you're navigated to the ssh terminal, you need to make sure you run an update by using the command
```
sudo apt-get update
```
once the update is complete, you then have to download nginx on the virtual machine and this is done by running the command

```
sudo apt-get install nginx
```


Clone the app
```
npm install
npm start
```

You can then access the app on port 3000 at one of the urls given above.

## Tests

There is a basic test framework available that uses the Mocha/Chai framework

```
npm test
```

The test for posts will fail ( as expected ) if the database has not been correctly setup.
