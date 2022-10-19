**On latency numbers (10 月曜日)**

I always forget this numbers

For quick reference:
- 1-10ns: L1 and L2 Cache
- 100-1000ns: System call
- 10-100micros: 1MB sequential read. 
- 100-1000micros: SSD Write. Intrazone (within AZ) network round trip. Redis
  get
- 1-10ms: Interzone (AZ to AZ) round trip
- 100-1000ms: TLS Handshake
- 1s: 1GB Transfer interzone

Source: [Latency Numbers Programmer Should Know](https://www.youtube.com/watch?v=FqR5vESuKe0)

**On Cloud Native Disaster Recovery**

@Considerations on Availability and Consistency

*Failure domains* are areas of an IT system in which the components within that
area may fail all at the same time due to a single event. When deploying a
distributed stateful workload, one should consider the various failure domains
at hand, and make sure that the various instances of the stateful workload are
positioned in different failure domains.

@High Availability

High Availability (HA) is a property of a system that allows it to continue
performing normally in the presence of failures. The foundational idea of HA is
that the Mean Time to Repair (MTTR), a failure must be much shorter than the
Mean Time Between Failures (MTBF) (MTTR << MTBF), allowing something or someone
to repair the broken component before another components breaks A proper
monitoring and alerting system must be in place. Otherwise, an HA system would
just keep functioning until the second failure occurs (~2xMTBF) and then still
be broken, defeating the initial purpose of HA. If a piece of software is
designed to keep working when the peers are unreachable, its state may become
inconsistent. On the other hand, if a piece of software is designed to stop
when the peers are unreachable, then it will maintain consistency, but will not
be available.

@Consistency

Consistency is the property of a distributed stateful workload where all the
instances of the workload “observe” the same state. Temporarily relaxing
consistency, building stateful workloads that horizontally scale to a
theoretically unlimited size, gave birth to an explosion of eventually
consistent workloads. Eventual consistency is not suitable in every scenario.
Eventual consistency does not mean eventual correctness.

@The CAP Theorem

- [CNDR for Stateful
  workloads](https://docs.google.com/document/d/10HcaLqPz8o8oXpbSNbPI0thVMoF3usTG3CAhq4Umz4w/edit#)

**On Building a second brain** 

The "cold storage" comment for projects resonated with me:
- "You don't need to make progress on everything all the time"

Practical steps
1. Decide what I want to capture
2. Setup P.A.R.A
3. Identify my (12) favourite problems
4. Automatically capture book highlights
5. Practice progressive summarization
6. Make progress on one deliverable
7. Schedule a weekly review

[Building a second
brain](https://www.audible.com/pd/Building-a-Second-Brain-Audiobook/B09MGHPVP4)

**On Terraform Cloud Workspaces (11 火曜日)**

Should there be a workspace per region?

**On Dev Principles by Id software (16 日曜日)**

This was a cool conf, want to watch it again and pull some reference

[Source](https://www.youtube.com/watch?v=IzqdZAYcwfY)

**On handling (c/cpp) dependencies (17 月曜日)**

tags: #security #rlbox #wasm

Most bugs, according to case [studies](https://www.chromium.org/Home/chromium-security/memory-safety/), 
are memory safety bugs, and just saying "Let's move everything to Rust" (or any
language)  is not easy as there are Billions of (reliable/time-tested) lines of code

IPC: Isolating everything with process sandboxing has a performance cost

In-process sandboxing isolates libraries in WASM sandboxes. 
The proposal, is to do it through RLBox, which:
- takes care of ABI convertions and data types marshalling
- tracks missing security checks

Already applied in Firefox

- [Source](https://www.youtube.com/watch?v=23rV-s3DKWM)
- [The Limits of Sandboxing and Next Steps](https://www.youtube.com/watch?v=vYirbKQ90IY)
- [RLBox](https://rlbox.dev/)


**On No silver bullet (19 水曜日)**

*For reference, this paper is from 1986 and it has aged like a fine wine.*

There is currently, no process, tool, paradigm, rule, etc, that ensures the
reliability of software. And even though there are attempts (and I would add,
cargo cults) around the problem, there's no actual solution.


The difficulties are divided in:
- Essence: Inherent in the nature of the software.
- Accidents: Difficulties that attend its production but that are not inherent.

The essence for software is representing any conceptual contruct with abstract concepts.
Some properties of this essence are:
- Complexity: A software entity size, the number of components and interactions
  between them, its constant change and growth
- Conformity: Software most interface with established infrastructure (be it
  hardware like CPU, software like an OS or regulations like PCI)
- Changeability: The *successful* usage of software demands extending it beyond
  its original capabilities (new use cases)
- Invisibility: Software has no physical representation. Diagrams help
  understand components/parts, which we may compose and try to see in layers
  (looking at you c4model.com), but it is not possible to see the entire system
  in a single diagram

Some attempts trying to fix the accidental difficulties:

- High-level languages: The abstraction of concrete machine concerns (bits,
  registers) allowing developers focus on abstract concepts (data structures, operations)
- Time-sharing: Being able to perform more than one operation with the CPU
- Unified programming environments: Extrapolating I think this includes package
  managers and using open-source software and libraries

@page 6 Hopes for the Silver

[Source](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf)
