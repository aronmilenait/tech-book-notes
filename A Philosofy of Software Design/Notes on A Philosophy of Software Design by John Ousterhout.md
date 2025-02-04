# Notes on A Philosophy of Software Design by John Ousterhout

# About these notes

This file contains fragments of _Notes on A Philosophy of Software Design_ by John Ousterhout, which serve as a summary. I follow this approach to make note-taking easier and faster, as well as to preserve the author's exact words.

I've gathered the concepts I consider the most important from the book and organized them using the same headings as the author, so it's easier to know where they come from.

I strongly recommend reading the entire book—it's amazing, and I learned a lot from it. However, if you just want to read a summary to incorporate the most important concepts, these notes are for you! They are also useful if you have already read it and want to have some notes to check whenever you need them.

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

# Chapter 4: Modules Should Be Deep

## Modular Design

In **modular design**, a software system is decomposed into a collection of modules
that are relatively independent. Modules can take many forms, such as **classes, subsystems, or services**. In an ideal world, each module would be completely independent of the others: a developer could work in any of the modules without knowing anything about any of the other modules.

This ideal is not achievable. Modules must work together by calling each others’s functions or methods. There will be **dependencies** between the modules: if one module changes, other modules may need to change to match.

In order to manage dependencies, we think of each module in two parts: an interface and an implementation. The **interface** consists of everything that a developer working in a different module must know in order to use the given module. The **implementation** consists of the code that carries out the promises made by the interface. 

The best modules are those whose interfaces are much simpler than their implementations. Such modules have two advantages. First, a simple interface minimizes the complexity that a module imposes on the rest of the system. Second, if a module is modified in a way that does not change its interface, then no other module will be affected by the modification.

##  What’s in an interface?

The **interface** to a module contains two kinds of information: formal and
informal. The **formal** parts of an interface are specified explicitly in the code, and
some of these can be checked for correctness by the programming language.  The
**informal** parts of an interface include its high-level behavior, such as the fact that
a function deletes the file named by one of its arguments.

## Abstractions

An **abstraction** is a simplified view of an entity, which omits unimportant details. 

In modular programming, each module provides an abstraction in form of its interface. The interface presents a simplified view of the module’s functionality: the more unimportant details that are omitted from an abstraction, the better. 

An abstraction can go wrong in two ways. First, it can include details that are not really
important. The second error is when an abstraction omits details that really are important. An abstraction that omits important details is a false abstraction: it might appear simple, but in reality it isn’t. 

## Deep modules

The best modules are those that provide powerful functionality yet have simple interfaces. I use the term deep to describe such modules.

**Module depth** is a way of thinking about cost versus benefit. The benefit provided by a module is its functionality. The cost of a module is its interface. A module’s interface represents the complexity that the module imposes on the rest of the system. The best modules are those with the greatest benefit and the least cost. 

## Shallow modules

A **shallow module** is one whose interface is complicated relative to the functionality it provides. Shallow modules don’t help much in the battle against complexity, because the benefit they provide is negated by the cost of learning and using their interfaces. 

## Classitis

The extreme of the “classes should be small” approach is a syndrome I call **classitis**, which stems from the mistaken view that “classes are good, so more classes are better.” In systems suffering from classitis, developers are encouraged to minimize the amount of functionality in each new class. Classitis may result in classes that are individually simple, but it increases the complexity of the overall system.

# Chapter 5: Information Hiding (and Leakage)

## Information hiding

The most important technique for achieving deep modules is **information hiding**. Each
module should encapsulate a few pieces of knowledge, which represent **design decisions**. The knowledge is embedded in the module’s implementation but does not appear in its interface, so it is not visible to other modules.

The information hidden within a module usually consists of details about how to implement some mechanism. Here are some examples:

- How to implement the TCP network protocol.
- How to parse JSON documents.

The hidden information includes data structures and algorithms related to the mechanism. It can also include lower-level details, and it can include higher-level concepts that are more abstract.

Information hiding reduces complexity in two ways. First, it simplifies the interface to a module. The interface reflects a simpler, more abstract view of the module’s functionality and hides the details; this reduces the cognitive load on developers who use the module. Second, information hiding makes it easier to evolve the system. If a piece of information is hidden, there are no dependencies on that information outside the module containing the information, so a design change related to that information will affect only the one module.

Hiding variables and methods in a class by declaring them private isn’t the same thing as information hiding.  However, information about the private items can still be exposed through public methods such as getter and setter methods. 

The best form of information hiding is when information is totally hidden within a module, so that it is irrelevant and invisible to users of the module.

## Information leakage

**Information leakage** occurs when a design decision is reflected in multiple modules. This creates a dependency between the modules: any change to that design decision will require changes to all of the involved modules.

If you encounter information leakage between classes, ask yourself “How can I reorganize these classes so that this particular piece of knowledge only affects a single class?” If the affected classes are relatively small and closely tied to the leaked information, it may make sense to merge them into a single class. Another possible approach is to pull the information out of all of the affected classes and create a new class that encapsulates just that information.

## Temporal decomposition

One common cause of information leakage is a design style I call **temporal decomposition**. In temporal decomposition, the structure of a system corresponds to the time order in which operations will occur. Consider an application that reads a file in a particular format, modifies the contents of the file, and then writes the file out again. With temporal decomposition, this application might be broken into three classes: one to read the file, another to perform the modifications, and a third to write out the new version. Both the file reading and file writing steps have knowledge about the file format, which results in information leakage. The solution is to combine the core mechanisms for reading and writing files into a single class.

When designing modules, focus on the knowledge that’s needed to perform each task, not the order in which tasks occur.

## Information hiding within a class

Try to design the private methods within a class so that each method encapsulates some information or capability and hides it from the rest of the class. In addition, try to minimize the number of places where each instance variable is used. If you can reduce the number of places where a variable is used, you will eliminate dependencies within the class and reduce its complexity.

## Taking it too far

Information hiding only makes sense when the information being hidden is not needed outside its module. If the information is needed outside the module, then you must not hide it. 