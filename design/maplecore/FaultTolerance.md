
# Fault Tolerance design of Maple

Maple system consists of a few (e.g. five) controllers. One of them is master and others backup.
Maple system should be able to recover when the following bad things happen:

 1. Master is down.
 2. One or more backup controllers leave or join in at run time.
 3. Connections between master and backup controllers are unstable.
 4. All controllers (including master and backups) are down.

## What need to be backup?

 1. Hard state must be stored in persistent storage.
    Q: What is hard state?
 
 2. Soft state (trace tree) has two options. I'm using option 2 in my design.
    * stored in persistent storage.
    * duplicate data and store a copy on each controllers.
   

## A rudimentary fault tolerance design

 * Leader election algorithm (Paxos) can be used to elect Master controller in a environment where controller may leave and join in randomly.
 * Update on soft state (Trace Tree) on Master will be propergated to backup controllers using a strong-consistency model, for example, two-phrase commit algorithm. After all of the controllers have uptodate TT, the master sends Openflow rules to switches to reflect the change on TT.
 * Update on hard state (e.g. user configuration) on Master will be first stored in persistent storage and then takes effect.
 
 * When a backup controller becomes online, it first loads hard start from persistent storage, and then pull soft state (trace tree) from one of other backup controllers (to avoid overkilling Master) and then receives update from master.
 
 * When a backup controller becomes Master, it first loads hard start from persistent storage and then takeover.
 
 * When a server become online and is then **immediately** elected as Master (didn't receive any soft state), it knows issue 4 happens. Hence the Master initializes both controllers and switches and run the network from scratch.

## State machine of MapleProgram
 * offline
 * slave
 * master
 
