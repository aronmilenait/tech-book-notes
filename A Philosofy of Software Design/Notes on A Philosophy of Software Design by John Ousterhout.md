# Notes on A Philosophy of Software Design by John Ousterhout

# Chapter 1: Introduction

Writing computer software is one of the purest creative activities in the history of the human race. Programmers aren’t bound by practical limitations such as the laws of physics; we can create exciting virtual worlds with behaviors that could never exist in the real world. 
## Two general approaches to fight complexity:

1. Making code simpler and more obvious.
2. To encapsulate it, so that programmers can work on a system without being exposed to all of its complexity at once. This approach is called **modular design**. 
## Waterfall and Agile

In the **waterfall model**, a project is divided into discrete phases such as requirements definition, design, coding, testing, and maintenance. Each phase completes before the next phase starts. The entire system is designed at once, during the design phase.

The waterfall model rarely works well for software. Software systems are intrinsically more complex than physical systems; it isn’t possible to visualize the design for a large software system well enough to understand all of its implications before building anything. As a result, the initial design will have many problems.

Most software development projects today use an incremental approach such as **agile development**, in which the initial design focuses on a small subset of the overall functionality. By spreading out the design in this way, problems with the initial design can be fixed while the system is still small; later features benefit from experience gained during the implementation of earlier features, so they have fewer problems.

As a software developer, you should always be on the lookout for opportunities to improve the design of the system you are working on.

# Chapter 2: The Nature of Complexity

**Complexity** is anything related to the structure of a software system that makes it hard to understand and modify the system. In a complex system, it takes a lot of work to implement even small improvements. In a simple system, larger improvements can be implemented with less effort.

Complexity is determined by the activities that are most common. If a system has a few parts that are very complicated, but those parts almost never need to be touched, then they don’t have much impact on the overall complexity of the system.

 Your job as a developer is not just to create code that you can work with easily, but to create code that others can also work with easily.

## Symptoms of complexity

1. **Change amplification:** a seemingly simple change requires code modifications in many different places.
2. **Cognitive load:** refers to how much a developer needs to know in order to complete a task. A higher cognitive load means that developers have to spend more time learning the required information, and there is a greater risk of bugs because they have missed something important.
3. **Unknown unknowns:** is not obvious which pieces of code must be modified to complete a task, or what information a developer must have to carry out the task successfully.

Of the three manifestations of complexity, unknown unknowns are the worst. An unknown unknown means that there is something you need to know, but there is no way for you to find out what it is, or even whether there is an issue. The only way to be certain is to read every line of code in the system.

One of the most important goals of good design is for a system to be obvious. An obvious system is one where a developer can make a quick guess about what to do, without thinking very hard, and yet be confident that the guess is correct.

## Causes of complexity

Complexity is caused by two things: dependencies and obscurity.

A **dependency** exists when a given piece of code cannot be understood and modified in isolation; the code relates in some way to other code, and the other code must be considered and/or modified if the given code is changed.

One of the goals of software design is to reduce the number of dependencies and to make the dependencies that remain as simple and obvious as possible.

**Obscurity** occurs when important information is not obvious. A simple example is a variable name that is so generic that it doesn’t carry much useful information (e.g., time). Or, the documentation for a variable might not specify its units, so the only way to find out is to scan code for places where the variable is used.

If we can find design techniques that minimize dependencies and obscurity, then we can reduce the complexity of software.

## Complexity is incremental

Complexity isn’t caused by a single catastrophic error; it accumulates in lots of small chunks.

It’s easy to convince yourself that a little bit of complexity introduced by your current change is no big deal. However, if every developer takes this approach for every change, complexity accumulates rapidly. Once complexity has accumulated, it is hard to eliminate.

# Chapter 3: Working Code Isn’t Enought (Strategic vs. Tactical Programming)

## Tactical Programming

The problem with **tactical programming** is that it is short-sighted. If you’re programming tactically, you’re trying to finish a task as quickly as possible. As a result, planning for the future isn’t a priority. You don’t spend much time looking for the best design; you just want to get something working soon. This is how systems become complicated.

The **tactical tornado** is a prolific programmer who pumps out code far faster than others but works in a totally tactical fashion. In some organizations, management treats tactical tornadoes as heroes. However, tactical tornadoes leave behind a wake of destruction. Typically, other engineers must clean up the messes left behind by the tactical tornado, which makes it appear that those engineers are making slower progress than the tactical tornado.

## Strategic Programming

The first step towards becoming a good software designer is to realize that working code isn’t enough.

The most important thing is the long-term structure of the system. Most of the code in any system is written by extending the existing code base, so your most important job as a developer is to facilitate those future extensions.

Your primary goal must be to produce a great design, which also happens to work. This is **strategic programming**.

Strategic programming requires an investment mindset. Rather than taking the fastest path to finish your current project, you must invest time to improve the design of the system. These investments will slow you down a bit in the short term, but they will speed you up in the long term.

Try to imagine a few ways in which the system might need to be changed in the future and make sure that will be easy with your design. Writing good documentation is another example of a proactive investment.

## Startups and investment

Many startups take a tactical approach, spending little effort on design and even less on cleanup when problems pop up. They rationalize this with the thought that, if they are successful, they’ll have enough money to hire extra engineers to clean things up. If you are in a company leaning in this direction, you should realize that once a code base turns to spaghetti, it is nearly impossible to fix.