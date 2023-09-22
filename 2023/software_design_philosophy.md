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

Deep modules hide information - advantage.

Information leakage - design decision is reflected in multiple modules.

Reflected in the interface - leaked.

Leakage is a red flag in design.

Temporal decomposition: structure of the system corresponds to time order in which operations will occur.

Information leakage: the same knowledge occurs in multiple places, e.g. two classes both understand a file type format.

When designing modules, focus on the knowledge that's needed to perform each task, not the order in which tasks occur.

Temporal decomposition issue: execution order is reflected in mutiple places, thus it's a leakage.

Information hiding can often be improved by making a class slightly larger.

API for a commonly used feature shouldn't include details about other rare features.
This would increase cognitive load: mostly of the users don't need to know about the rare features, thus no need to reflect this in interface.

Information hiding could happen within a class.

Some information should not be hidden: something should be exposed and reflected in interface.

You should minimize the amount of information that is needed for module usage, but it's important to recognize parts of information that are needed to be exposed.

## General-purpose modules are deeper

Over-specialization could cause complexity.

General purposes modules lead to deep API. The reason: information hiding.

Removing special cases in code is a way of code simplification.

Implement new modules in a somewhat general-purpose way.

Generality leads to better information hiding.

Relevant questions are:

*  What is the simplest interface that will cover all my current needs?
*  In how many situations will this method be used?
*  Is this API easy to use for my current needs?

Push specialization upwards and downwards.

*  Top level classes will be specialized for sure. But this might not be relevant to helpers.
*  Sometimes downwards pushing is a good idea, e.g. device drivers. They would hide complexity behind abstractions.

Eliminate special cases in code.

## Different layer - different abstraction

Pass-through methods might be an anti-pattern. This might indicate that there isn't a clear division of responsibility between classes.

There are exceptions for pass-through cases: dispatcher, decorator (maybe alternatives would be better).

Interface vs implementation. Implementation should be different from interface.

Pass-through variables. This adds complexity. It can be tricky to remove. Idea to solve: use context variable which is a global state representation.

## Pull complexity downwards

It's more important for a module to have a simple interface than a simple implementation.

When developing a module, look for opportunities to take a little bit of extra suffering upon yourself in order to reduce the suffering of your users.

## Better together or apart?

Separate general-purpose and special-purpose code.

If the same code appears over and over again: you might not have the right abstractions.

Each method should do one thing and do it completly.

It should be possible to understand each method independently. It's also relevant to pieces of code. It's bad to read implementation of another thingy, if you try to understand one thing.

Split/join -> base the decision on complexity.

Pick the structure that results in the best information hiding, the fewest dependencies, and the deepest interfaces.

## Define errors out of existence

Exceptions add complexity.

Classes with lots of exceptions have complex interfaces, and they are shallower than classes with fewer exceptions.

Reduce the number of places where exceptions have to be handled.

Define errors out of existence.

Making software simpler -> reducing bugs.

Exception aggregation idea.

Just crashing is an option.

## Design it twice

It improves both design and design skills. Over time it will become easier.

## Why write comments? Excuses

Process of writing comments, if done correctly, will actually improve a system's design.

Self-documenting excuse.

If users must read the code of a method in order to use it, then there is no abstraction.

Not enough time excuse.

Comments get out of date and become misleading excuse.

All the comments are worthless excuse.

The overall idea behind comments is to capture information that was in the mind of the designer but couldn't be represented in the code.

Well-written comments are not failures. They increase the value of code and serve a fundamental role in defining abstractions and managing system complexity.

## Comments should describe things that aren't obvious from the code

Developers should be able to understand the abstraction provided by a module without reading any code other than its externally visible declarations

Conventions for comments.

Don't repeat the code.

Use different words in the comment from those in the name of the entity being described.

Comments augment the code by providing information at a differnt level of detail.

High level comments enhance intuition.

Is you want code that presents good abstractions, you must document those abstractions with comments.

If interface comments must also describe the implementation, then the class or method is shallow.

Implementation comments: what and why, not how

The main goal of implementation comments is to help readers understand what the code is doing.

It's important to document cross-modules design decisions.

## Choosing names

Bad names cause bugs.

Create an image with name.

Names should be precise. Vague names can be misleading.

If it's hard to find a simple name for a variable/method that create a clear image of it, that's a hint: the design might be not clear.

Be consistent.

Aboid extra words.

Go style :)

## Write the comments first (use comments as part of the design process)

TBD
