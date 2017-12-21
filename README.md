# OpenWSN firmware scheduler
Some modification to the firmware that run on a mote in order to upgrade the scheduling function and the allocation process.

- UC Berkeley's OpenWSN project, http://www.openwsn.org/.

### Requirements:
To trigger: 
- Verify that there has been a change in the number of used against any fo the neighbours.
- For each neighbour, if it has changed the number of used cells from the previous slotframe:
-- Calculate the difference in the number of cells between timeslots: NEWCELL
-- Estimate the number of cells: NEWCELL+OVERPROVISION Even if NEWCELL is negative
- Execute de allocation policy:
-- Below the interval  If REQUIREDCELLS<(SCHEDULEDCELLS-SF0THRESH), delete one or more cells
-- Within the interval If (SCHEDULEDCELLS-SF0THRESH)<=REQUIREDCELLS<=SCHEDULEDCELLS, do nothing
-- Above the interval  If SCHEDULEDCELLS<REQUIREDCELLS, add one or more cells.
-- If new cells must be allocated, select a random number of cells from the available ones on the schedule; Call 6P to ADD cells.
-- If the order is to delete cells, select randomly from the currently allocated cells for the neighbour. call 6P to DELETE cells.

### Installation

Dillinger requires [Node.js](https://nodejs.org/) v4+ to run.

Install the dependencies and devDependencies and start the server.

```sh
$ cd dillinger
$ npm install -d
$ node app
```

For production environments...

```sh
$ npm install --production
$ NODE_ENV=production node app
```

### How to run it

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma test
```

### Based on
- overview: https://openwsn.atlassian.net/wiki/
- source code: http://openwsn-berkeley.github.io/firmware/
