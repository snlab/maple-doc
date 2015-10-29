
# Fault Tolerance design of Maple

Maple system consists of a few (e.g. five) controllers. One of them is master and others backup.
Maple system should be able to recover when the following bad things happen:

 1. Master is down.
 2. One or more backup controllers leave or join in at run time.
 3. Connections between master and backup controllers are unstable.
 4. All controllers (including master and backups) are down.

## A rudimentary fault tolerance design

 * Leader election algorithm in Chubby can be used to elect Master controller in a environment where controller may leave and join in randomly.
 * Master handle messages from switches and configuration from GUI/users.
 * Update on Trace Tree and other internal states in Master will be broadcast to backup controller, using a strong-consistency model, for example, Two-Phrase Commit algorithm.
 
Now we can handle issue 1 and 2.
