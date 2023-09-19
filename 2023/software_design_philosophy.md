# A Philosophy of Software Design

It's all about complexity.

## Nature of complexity

Complexity is anything related to the structure of software system that makes it hard to understand and modify the system.

Complexity of the whole system depends on the complexity of its parts + factors the time spent on them.

Symptoms are:

*  Change amplification. Simple thingy turns out being huge.
*  Cogntive load. One needs to know a lot before making changes. Sometimes more LOC is simpler, since it might reduce the cogntive load.
*  Unknown unknowns.

Causes of complexity are:

*  Dependencies.
*  Obscurity.

Complexity is incremental. Stuff is accumulated over time, a single change is often fairly harmless.

## Strategic vs tactical programming

Tactical programming: focus on getting something working.
It would be hard to produce good design in this way.
It's short-sighted.
Adding complexity here an there -> bad system.
Tactical tornado developer.

Strategic programming: working code isn't enough.
It's not ok to introduce unneccessary complexity.
Primary goal is to produce a great design.
Investment mindset. Some investments might be proactive.
Some investments will be reactive: mistakes would happen -> extra time to fix it.

How much to invest? 10-20% is a good starting point. It's a good balance: not a big hindrance, but enough to make the system better.
Over time it would pay off: initially you might be a bit slower, but you would make faster progress in a better system.

Technical debt - problems caused by tactical programming.

Strategic programming payoff: the window is roughly 6-18 months.

Start ups - there is a good chance that strategic approach would be optimal there. There are counter examples for it.

## Deep modules

Modular design. Depedencies between modules. Interface vs implementation.

Best modules: interface is much simpler than implementation.

Interface should indicate what developers need to know for usage. It helps with unknown unknowns.

Abstraction is a simplified view of an entity, which omits unimportant details.

Deep modules: powerful functionality with a simple interface.

Module analysis as cost versus benefit: benefit is functionality and cost is interface.

Unix file system is a good example of a deep module. It's powerful yet simple.

Shallow modules. Example: java I/O. Red flag: interface is complicated relative to its functionality.

Problem with shallow module: small benefit (little functionality), hard to understand / learn / use (complicated interface).

Idea from OOP/clean code: classes/method should be small. It might be verbose and hard to follow.

## Information hiding and leakage

TBD
