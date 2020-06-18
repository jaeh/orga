# cert authority setup

## internal

these are the internal certificates,
registered in the grund.stein namespace.

api.grund.stein etc.

better name for namespace?

1. generate root certificate locally.
    * airgapped machine,
    * keys on 3 usb sticks
    * certificate backup on 3 usb sticks
2. generate derivative cert for online use
3. build step uploads the derivative.

## letsencrypt

use certbot to generate certificates for each of the services.


## certificate share

for now, all our services run on one pod, so we can just access the local filesystem and certificates.

### server:

the cert share server will do two things:

1. serve all public certificates via mem-store and https
2. send the private certificates to the servers indicated in grundstein-config, once their http services have started, those services will then restart their servers in https mode.

the second part sounds risky, have to investigate if i find a better solution,
the benefit would be that gps can build the first cache without certificates being distributed,
the negative would be that this first connections are unsafe.


#### threats:

##### hack
someone gets access to signing certificate: regen root and restart cloud. problem is detecting this access.

##### lose root

We lose the root cert

not too bad, we just recreate it, then relaunch the cloud,
it's the internal cert authority after all.
