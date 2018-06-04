[This repo is deprecated. Use this example instead https://github.com/cf-platform-eng/pcf-examples](https://github.com/cf-platform-eng/pcf-examples)
# sample-boshrelease

A sample BOSH Release for Sample Java Hello world Application

* Run submodule init & update to sync up the routing-release from cloudfoundry-incubator
```
git submodule update --init --recursive
```

* Edit the final.yml and create a private.yml if you want to use s3 instead of local blobstore

* Download the blobs for openjdk, tomcat
```
wget https://java-buildpack.cloudfoundry.org/tomcat/tomcat-8.5.5.tar.gz
wget https://java-buildpack.cloudfoundry.org/openjdk-jdk/trusty/x86_64/openjdk-1.7.0_51.tar.gz
wget https://storage.googleapis.com/golang/go1.6.3.linux-amd64.tar.gz
```
* Add the blobs so the packages can refer to them
```
bosh add blob <path-to-openjdk-1.7.0_51.tar.gz> openjdk
bosh add blob <path-to-apache-tomcat-8.*tar.gz> tomcat
bosh add blob <path-to-go1.6.3.linux-amd64.tar.gz> golang
bosh add blob <sample.war> sample
bosh -n upload blobs
```


* Create the release tarball with specific release number or it would just bump the version numbers
```
bosh create release --with-tarball --version 0.1 --force
```

* Upload the release if workng with local bosh director or connected to bosh director
```
bosh upload release
```

* Upload stemcell (Download latest bosh-lite warden stemcell from bosh.io)
``` 
bosh upload stemcell
```

* Deploy the manifest if using bosh-lite
```
bosh deployment  sample-manifest.yml
bosh -n deploy
```
