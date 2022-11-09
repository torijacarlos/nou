# Thoughts/Papers

======================================================================================================

## The only unbreakable law

tags: #talks #practices #principles

[Source](https://www.youtube.com/watch?v=5IUj1EZwpJY)

Basically points to Conway's Law [How committees
invent?](https://www.melconway.com/Home/pdf/committees.pdf) as a good candidate
for a Software Architecture law agree. He also mentions:
- Brooke's Law which addresses Communication constraints [The mythical
  man-month](https://www.amazon.com.mx/Mythical-Man-Month-Essays-Software-Engineering/dp/0201835959/ref=sr_1_1)
- Amdahl's Law which addresses non parallelizable dependencies

Communication within a team has (or at least should have) close-to-zero
overhead. The only communication that has zero overhead is with oneself.
Anywhere there is a need for communication, there are constraints that need to
be addressed:
- How much can I communicate. I literally mean volume of information
- Am I communicating effectively? Can the other person/team understand what we
  are saying?
- Are our goals aligned? Do we want the same things?

If there is any divide within an organization, you are creating the need for
communication channels with varying bandwidth. 

This adds complexity/friction which determines the kind of system you are
capable of designing as an team. 

If there is a need for a communication channel between two teams (let's say
infrastructure and development) there is inevitably going to be some sort of
responsibility segregation given it removes the need for given communication
channel, or at least reduces the amount of information that has to go through

Any kind of organizational structure created (for the orgchart or the codebase)
comes from the need of simplifying a problem that may be too complex to solve
with the current capabilities available. Divide and conquer as some may say.
But its adding accidental complexity to the actual problem.

======================================================================================================

## No silver bullet

tags: #paper #thought #wip

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

As for the proposed solutions to fix the essence so far:

- More high level languages won't solve the problem, they just simplify the
  abstractions for data flow and structures
- Paradigms do not solve the problem (if they did, there wouldn't be a
  discussion between using oop or functional or whatever)
- On artificial inteligence, expert systems and automatic programming, I'll
  quote verbatim this: *"the hard thing about building software is deciding
  what to say, not saying it"* and here's a
  [demo](https://www.youtube.com/watch?v=Xw_qbJp52cY) that shows the status
  quo. How would it handle actual complexity?
- For graphical programming I guess the "state of the art" is Unreal Engine's
  Blueprint Visual Scripting but
  [here](https://forums.unrealengine.com/t/how-tidy-multiple-line-traces/242770/7)
  is why I think that is a step in the wrong direction 
- I don't comments on the rest but to summarize
    - Program Verification: Automated testing? I dunno ¯\_(ツ)_/¯ 
    - Environments and tools: The newer tools seem to be going backwards,
      adding even more unnecessary complexity
    - workstations: Computers are way more powerful than we know. We just got
      used to lousy and slow software.


@Promising Attacks on the Conceptual Essence Page 12

[Source](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf)

======================================================================================================

