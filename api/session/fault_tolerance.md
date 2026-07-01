# otp.FaultTolerance

### ``class FaultTolerance(*sockets)``

Bases: ``object``

Class representing configuration of client-side tick-server fault tolerance.
Tick servers in the fault tolerance list are selected according to their level of priority,
which is from left to right. Backup servers (servers after the first one, primary) are used only if the query
