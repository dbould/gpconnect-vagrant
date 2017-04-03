# gpconnect-vagrant
See [https://github.com/nhs-digital/gpconnect](https://github.com/nhs-digital/gpconnect) for demonstrator project

Install [Vagrant](https://www.vagrantup.com/downloads.html)
Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

```
cd /var/www/html
git clone https://github.com/nhs-digital/gpconnect
cp build/ gpconnect/build
ant build
```

Wait a long time for the dependencies to download

```
ant run
```

Play with the app at http://192.168.20.81:19191
