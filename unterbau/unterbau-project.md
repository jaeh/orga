# unterbau

## objective

### server

1U and 3 or 4U configurations of raspberry pi clusters.


## hosting

nessus.at has 2 server centers in vienna, they also are metalab related (and wizard knows them well)

we can place 1u at both centers for now, with a minimal setup of one raspberry 4,
would be enough to host all static properties for magic.gs, grundstein.it and webboot.org.

optimal hosting for now would probably be:

1u in each center, one nvme cluster and one pi cluster in each slice.

-----------------------------------------------

## vendor

semaf electronics seem very well sourced and is an official raspberry partner,
should also be a good viennese partner for long-time (and maybe automated...) hardware procurement.

-----------------------------------------------

## hardware


-----------------------------------------------h

### raspberry pi

* RPI-4 Specs:
  https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/
* RPI-Z Specs:
  https://www.raspberrypi.org/products/raspberry-pi-zero-w/


--------------------------------

## modules:

modules are separate parts of the infrastructure.

One slice is made up of multiple modules, for example compute and storage modules.

raspberry zero, and raspberry 4 describe a product group and are placeholders for brevity.

--------------------------------


### clusters:

### raspi Zero or equivalent cluster:

as many zeroes as possible (ram speed vs bandwidth of switch),
load-balanced and raid-controlled by a pi 4.

#### software:

the pi4 runs a load balancer for the zeroes, invoking javascript lambdas stored on the zeroes.
the lambdas are lightweight and usually do not need to talk to storage,
if they do, a rack-internal request is made loading or writing the data to storage.

--------------------------------

### carry

toughbook case with raspberry cluster that runs webboot.

Includes simcard and wifi, controlled by a separate pi [dmz](https://hackmd.io/8XUOi-w3Tgagzhpu6hDHFg)
Has a bright red led and a switch on the outside to toggle them.

--------------------------------


### webboot cube

* raspberry 4
* nvme cluster
* in a box

--------------------------------


### NVME raid:
4+ nvme drives and a cpu that raids them.

https://en.wikipedia.org/wiki/NVM_Express
https://en.wikipedia.org/wiki/RAID

#### ???

* how do we get the bandwidth the nvme provides (~3gb sec read) through our cluster to the ethernet?
* maybe we could use a minimal cpu chip that just provides a ethernet switch and use one nvme per cpu core?

* nvme drives (256gb are enough for the webboot rack, for now.)
* cpu (raspberry 4?)

--------------------------------

### minimal ethernet switch

would be awesome to have a minimal hardware that only controls ethernet switching,
with 4 or 12 ports.

--------------------------------

### controller

server controller, connects to the server via ethernet that leads to the DMZ pi

* lcd touchscreen
* bluetooth lenovo keyboard or mac keyboard
* raspberry pi with private key

--------------------------------

## Hardware list and links

What follows is a list of various hardware parts that solve separate, yet connected, problems.

Once that Lists grow we will separate them into more categories.

---------------------------------------

### Boards

a collection of various boards, clusters and other interesting things.

not limited to raspberry pi, meant to include all boards that are of interest.

| euro | part | link |
| ---- | ---- | ---- |
| 80 | board pi4 8gb | https://electronics.semaf.at/Raspberry-Pi-4-B-4x-15GHz-CPU-8GB-DDR4-RAM-BLE5-WLAN?rel=gzh |
| 120 | zero cluster | https://electronics.semaf.at/Cluster-HAT-v23-Kit-with-4x-Raspberry-Pi-Zero-W-4x-16GB-MicroSDHC |

---------------------------------------

### Lcds

(Touch)screens for our systems,
will usually come with a

| euro | part | link |
| ---- | ---- | ---- |
| 70 | lcd | https://electronics.semaf.at/Raspberry-Pi-7-Touch-Screen-Display-with-10-Finger-Capacitive-Touch |

-------------------------------------

### Casings

| euro | part | link |
| ---- | ---- | ---- |
| 13.5 | gehaeuse | https://electronics.semaf.at/Gehaeuse-fuer-Raspberry-Pi-7-LCD-Display-und-Raspberry-Pi-4 |

----------------------------------------

### Fans

| euro | part | link |
| ---- | ---- | ---- |
| 11 | dual fan | https://electronics.semaf.at/Dual-Fan-with-Heatsink-for-Rasperry-Pi |

---------------------------------------
