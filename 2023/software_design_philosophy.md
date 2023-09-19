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
