# OpenWSN firmware scheduler
Some modification to the firmware that run on a mote in order to upgrade the scheduling function and the allocation process.

- UC Berkeley's OpenWSN project, http://www.openwsn.org/.

### Requirements:
To trigger: 
- Verify that there has been a change in the number of used against any fo the neighbours.
- For each neighbour, if it has changed the number of used cells from the previous slotframe:
    - Calculate the difference in the number of cells between timeslots: NEWCELL
    - Estimate the number of cells: NEWCELL+OVERPROVISION Even if NEWCELL is negative
- Execute de allocation policy:
    - Below the interval  If REQUIREDCELLS<(SCHEDULEDCELLS-SF0THRESH), delete one or more cells
    - Within the interval If (SCHEDULEDCELLS-SF0THRESH)<=REQUIREDCELLS<=SCHEDULEDCELLS, do nothing
    - Above the interval  If SCHEDULEDCELLS<REQUIREDCELLS, add one or more cells.
    - If new cells must be allocated, select a random number of cells from the available ones on the schedule; Call 6P to ADD cells.
    - If the order is to delete cells, select randomly from the currently allocated cells for the neighbour. call 6P to DELETE cells.

### Installation



Install the dependencies to  start the server.

```sh
$ sudo apt-get update
$ mkdir openwsn
$ sudo apt-get install -y git
$ cd ./openwsn/
$ git clone https://github.com/openwsn-berkeley/openwsn-fw.git
$ git clone https://github.com/openwsn-berkeley/openwsn-sw.git
$ git clone https://github.com/openwsn-berkeley/coap.git
$ cd ./openwsn-fw/
$ sudo apt-get install -y python-dev
$ sudo apt-get install -y scons
$ cd ../openwsn-sw/
$ sudo apt-get install -y python-pip
$ sudo apt-get install -y python-tk
$ sudo pip install -r requirements.txt
$ cd ../coap/
$ sudo pip install -r requirements.txt
$ sudo apt-get install -y gcc-arm-none-eabi
$ sudo apt-get install -y gcc-msp430
$ sudo apt-get install python-dev
$ sudo apt-get install scons
$ sudo pip install PySerial
```

Clone proyects.

```sh
$ mkdir openwsn
$ cd openwsn/
$ git clone https://github.com/densjac/openwsn-fw.git
$ git clone https://github.com/openwsn-berkeley/openwsn-sw.git
$ git clone https://github.com/openwsn-berkeley/coap.git

```


Prepare website environments 

```sh
$ cd ~
$ cd openwsn/
$ cd openwsn-sw/
$ sudo pip install -r requirements.txt
```



Compile the firmware.

```sh
$ cd ~
$ cd openwsn/
$ cd openwsn-fw/
$ scons board=python toolchain=gcc oos_openwsn
```




### How change sixtop

Go to folder
```sh
$ cd ~
$ cd openwsn/
$ cd openwsn-fw/
$ cd openstack/02b-MAChigh
```

Edit Files:
```sh
$ vi neighbors.c
$ vi sf0.c
```

Test changes :
```sh
$ cd ~
$ cd openwsn/
$ cd openwsn-sw/
$ cd software/openvisualizer
$ sudo scons runweb --sim --simCount=10
```
Check website in ip address:8080
