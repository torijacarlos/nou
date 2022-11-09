# Cloud
 
======================================================================================================

## Cloud Native DRP

tags: #drp #cloud #wip

- [CNDR for Stateful
  workloads](https://docs.google.com/document/d/10HcaLqPz8o8oXpbSNbPI0thVMoF3usTG3CAhq4Umz4w/edit#)

## Considerations on Availability and Consistency

*Failure domains* are areas of an IT system in which the components within that
area may fail all at the same time due to a single event. When deploying a
distributed stateful workload, one should consider the various failure domains
at hand, and make sure that the various instances of the stateful workload are
positioned in different failure domains.

### High Availability

High Availability (HA) is a property of a system that allows it to continue
performing normally in the presence of failures. The foundational idea of HA is
that the Mean Time to Repair (MTTR), a failure must be much shorter than the
Mean Time Between Failures (MTBF) (MTTR << MTBF), allowing something or someone
to repair the broken component before another components breaks A proper
monitoring and alerting system must be in place. 

Otherwise, an HA system would just keep functioning until the second failure
occurs (~2xMTBF) and then still be broken, defeating the initial purpose of HA.
If a piece of software is designed to keep working when the peers are
unreachable, its state may become inconsistent. On the other hand, if a piece
of software is designed to stop when the peers are unreachable, then it will
maintain consistency, but will not be available.

### Consistency

Consistency is the property of a distributed stateful workload where all the
instances of the workload “observe” the same state. Temporarily relaxing
consistency, building stateful workloads that horizontally scale to a
theoretically unlimited size, gave birth to an explosion of eventually
consistent workloads. Eventual consistency is not suitable in every scenario.
Eventual consistency does not mean eventual correctness.

### The CAP Theorem

Simply put, the CAP theorem states in case of network partitioning (P), one can
choose between consistency (C) or availability (A), but cannot have both. 

So, in terms of HA, if there are three or more instances of a stateful
workload, for the CAP theorem we can have both availability and consistency. 

In general, if the stateful workload is deployed across three or more failure
domains, it can be designed to be always available and consistent with respect
to the failure of one of those failure domains.

### Disaster Recovery

Given a failure domain, DR can be thought of as answering the question: What
happens to the workload when all of the components of this failure domain
break?

Disaster recovery is usually associated with two metrics:
- Recovery Time Objective (RTO): the time it takes to have systems back online
  after a datacenter fails.
- Recovery Point Objective (RPO): time interval of state loss from the last
  saved state to the time the datacenter fails.

## Anatomy of a Stateful application


======================================================================================================
