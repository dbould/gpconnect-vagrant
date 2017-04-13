# gpconnect-vagrant

This project contains a complete environment for the GP Connect Demonstrator project.  It runs Ubuntu complete with required installed packages (Java8, Tomcat, Maven etc), so you'll only need to run a few commands to go from no environment to being able to use the app.

See [https://github.com/nhs-digital/gpconnect](https://github.com/nhs-digital/gpconnect) for demonstrator project

Install [Vagrant](https://www.vagrantup.com/downloads.html)
Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Start the Vagrant box by typing this in this in the project root:
```
vagrant up
```

Now navigate to the mapped webserver directory and checkout the GP Connect project
```
cd html
git clone https://github.com/nhs-digital/gpconnect
```

Jump into the vagrant box
```
vagrant ssh
```

Move to build folder and build
```
cd /var/www/html/gpconnect/build
ant build
```

Wait a long time for the dependencies to download

```
ant run
```

Play with the app at http://192.168.20.81:19191

## Known Issues
There seems to be an intermittent issue where the JS doesn't build correctly. If you continue to get the Spring error page, it's probably worth deleting the gpconnect folder and re-cloning it.
