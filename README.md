# gpconnect-vagrant
See [https://github.com/nhs-digital/gpconnect](https://github.com/nhs-digital/gpconnect) for demonstrator project

```
cd /var/www/html
git clone https://github.com/nhs-digital/gpconnect
mkdir gpconnect/build
cp build/build.xml gpconnect/build
ant build
```

Wait a long time for the dependencies to download

```
ant run
```

Play with the app at http://192.168.20.81:19191
