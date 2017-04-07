# gpconnect-vagrant
See [https://github.com/nhs-digital/gpconnect](https://github.com/nhs-digital/gpconnect) for demonstrator project

Install [Vagrant](https://www.vagrantup.com/downloads.html)
Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Start the Vagrant box by type this in this checked out directory:
```
vagrant up
```

Now navigate to the webserver defaul directory, clone gpconnect demonstrator and build the project
```
cd html
git clone https://github.com/nhs-digital/gpconnect
mv build/ gpconnect/build
```

Jump into vagrant box
```
vagrant ssh
```

Move to build script and build
```
cd /var/www/html
ant build
```

Wait a long time for the dependencies to download

```
ant run
```

Play with the app at http://192.168.20.81:19191
