# S.O.L.I.D

SOLID is an acronym for 5 **design** principles (coding principles). Those principles are intended mainly for OOP paradigm. They were introduced by Robert Martin in his `2000 paper: Design Principles & Design Patterns`.

* **S**ingle Responsibility principle.
* **O**pen-Closed principle.
* **L**iskov substitution principle.
* **I**nterface Segregation principle.
* **D**ependency Inversion principle.

## The Ugly Truth

What goes wrong with software? The design of many software applications begins as a vital image in the minds of its designers. At this stage it is clean, elegant, and compelling. It has a simple beauty that makes the designers and implementers itch to see it working. Some of these applications manage to maintain this purity of design through the initial development and into the first release.

But then something begins to happen. The software starts to rot. At first it isn’t so bad. An ugly wart here, a clumsy hack there, but the beauty of the design still shows through. Yet, over time as the rotting continues, the ugly festering sores and boils accumulate until they dominate the design of the application. The program becomes a festering mass of code that the developers find increasingly hard to maintain. Eventually the sheer effort required to make even the simplest of changes to the application becomes so high that the engineers and front line managers cry for a redesign project.

Such redesigns rarely succeed. Though the designers start out with good intentions, they find that they are shooting at a moving target. The old system continues to evolve and change, and the new design must keep up. The warts and ulcers accumulate in the new design before it ever makes it to its first release. On that fateful day, usually much later than planned, the morass of problems in the new design may be so bad that the designers are already crying for another redesign.

## Symptoms of rotten software

There are four primary symptoms that tell us that our designs are rotting. They are not
orthogonal, but are related to each other in ways that will become obvious. they are:
**rigidity**, **fragility**, **immobility**, and **viscosity**.

#### Rigidity
Rigidity is the tendency for software to be difficult to change, even in simple ways. Every change causes a cascade of subsequent changes in dependent modules. What begins as a simple two day change to one module grows into a multi-week marathon of change in module after module as the engineers chase the thread of the change through the application. 

When software behaves this way, managers fear to allow engineers to fix non-critical problems. This reluctance derives from the fact that they don’t know, with any reliability, when the engineers will be finished. If the managers turn the engineers loose on such problems, they may disappear for long periods of time. The software design begins to take on some characteristics of a roach motel -- engineers check in, but they don’t check out.

When the manager’s fears become so acute that they refuse to allow changes to software, official rigidity sets in. Thus, what starts as a design deficiency, winds up being adverse management policy.

#### Fragility
Closely related to rigidity is fragility. Fragility is the tendency of the software to break in many places every time it is changed. Often the breakage occurs in areas that have no conceptual relationship with the area that was changed. Such errors fill the hearts of managers with foreboding. Every time they authorize a fix, they fear that the software will break in some unexpected way.

As the fragility becomes worse, the probability of breakage increases with time. Such software is impossible to maintain. Every fix makes it worse, introducing more problems than are solved.

Such software causes managers and customers to suspect that the developers have lost control of their software. Distrust reigns, and credibility is lost.

####  Immobility
Immobility is the inability to reuse software from other projects or from parts of the same project. It often happens that one engineer will discover that he needs a module that is similar to one that another engineer wrote. However, it also often happens that the module in question has too much baggage that it depends upon. After much work, the engineers discover that the work and risk required to separate the desirable parts of the software from the undesirable parts are too great to tolerate.
And so the software is simply rewritten instead of reused.

#### Viscosity
Viscosity comes in two forms: viscosity of the design, and viscosity of the environment. When faced with a change, engineers usually find more than one way to make the change. Some of the ways preserve the design, others do not (i.e. they are hacks.) When the design preserving methods are harder to employ than the hacks, then the viscosity of the design is high. It is easy to do the wrong thing, but
hard to do the right thing.

Viscosity of environment comes about when the development environment is slow and inefficient. For example, if compile times are very long, engineers will be tempted to make changes that don’t force large recompiles, even though those changes are not optimal from a design point of view. If the source code control system requires hours to check in just a few files, then engineers will be tempted to make changes that require as few check-ins as possible, regardless of whether the design is
preserved.

These four symptoms are the tell-tale signs of poor architecture. Any application that
exhibits them is suffering from a design that is rotting from the inside out. But what
causes that rot to take place?

## Changing Requirements
The immediate cause of the degradation of the design is well understood. The requirements have been changing in ways that the initial design did not anticipate. Often these changes need to be made quickly, and may be made by engineers who are not familiar with the original design philosophy. So, though the change to the design works, it somehow violates the original design. Bit by bit, as the changes continue to pour in, these violations accumulate until malignancy sets in.

However, we cannot blame the drifting of the requirements for the degradation of the
design. We, as software engineers, know full well that requirements change. Indeed,
most of us realize that the requirements document is the most volatile document in the project. If our designs are failing due to the constant rain of changing requirements, it is our designs that are at fault. We must somehow find a way to make our designs resilient to such changes and protect them from rotting.

## Dependency Management
What kind of changes cause designs to rot? Changes that introduce new and unplanned implementations to dependencies. Each of the four symptoms mentioned above is either directly, or indirectly caused by improper dependencies between the modules of the software. It is the dependency architecture that is degrading, and with it the ability of the software to be maintained.

In order to forestall the degradation of the dependency architecture, the dependencies between modules in an application must be managed. This management consists of the creation of dependency firewalls.A cross such firewalls, dependencies do not propogate.

Object Oriented Design is replete with principles and techniques for building such firewalls, and for managing module dependencies.

## Single Responsibility Principle (SRP) 

`A class should have only a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class.`

## Open-Closed Principle (OCP)

`A module should be open for extension but closed for modification.`

## Liskov Substitution Principle (LSP)

`Subclasses should be substitutable for their base classes.`

## Interface Segregation Principle (ISP)

`Many client specific interfaces are better than one general purpose interface`

## Dependency Inversion Principle ()

`Depend upon Abstractions. Do not depend upon concretions.`




## Single Responsibility Principle (SRP)

`A class should have only a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class.`

#What does this mean ?
Imagine a typical business organization. There is a CEO at the top. Reporting to that CEO are the C-level executives: the CFO, COO, and CTO among others. The CFO is responsible for controlling the finances of the company. The COO is responsible for managing the operations of the company. And the CTO is responsible for the technology infrastructure and development within the company.

Now consider this bit of Java code:

`public class Employee {
  public Money calculatePay();
  public void save();
  public String reportHours();
}`


The calculatePay method implements the algorithms that determine how much a particular employee should be paid, based on that employee’s contract, status, hours worked, etc.
The ‘save’ method stores the data managed by the Employee object onto the enterprise database.
The reportHours method returns a string which is appended to a report that auditors use to ensure that employees are working the appropriate number of hours and are being paid the appropriate compensation.
Now, which of those C-Level executives reporting to the CEO is responsible for specifying the behavior of the calculatePay method? Which of them would be fired[1] by the CEO if that method were catastrophically mis-specified? Clearly the answer is the CFO. Specifying the pay of employees is a financial responsibility. If all the employees were paid double for a year because someone in the CFOs organization mis-specified the rules for calculating pay, the CFO would likely be fired.

A different C-Level executive is responsible for specifying the format and content of the string returned from the reportHours method. That executive manages the auditors and reviewers, and that’s an operations responsibility. So if there were a catastrophic mis-specification of that report, the COO would be fired.

Finally, it should be obvious which of the C-Level executives would be fired if there were a catastrophic mis-specification of the save method. If the enterprise database were to be corrupted by such a horrific mis-specification, the CTO would likely be fired.

So it stands to reason that when changes are made to the algorithm within the calculatePay method, the request for those changes will originate from the organization headed by the CFO. Similarly it will be the COO’s organization that will request changes to the reportHours method, and the CTOs organization that will request changes to the save method.

And this gets to the crux of the Single Responsibility Principle. This principle is about people.

When you write a software module, you want to make sure that when changes are requested, those changes can only originate from a single person, or rather, a single tightly coupled group of people representing a single narrowly defined business function. You want to isolate your modules from the complexities of the organization as a whole, and design your systems such that each module is responsible (responds to) the needs of just that one business function.

Why? Because we don’t want to get the COO fired because we made a change requested by the CTO. Nothing terrifies our customers and managers more that discovering that a program malfunctioned in a way that was, from their point of view, completely unrelated to the changes they requested. If you change the calculatePay method, and inadvertently break the reportHours method; then the COO will start demanding that you never change the calculatePay method again.

Imagine you took your car to a mechanic in order to fix a broken electric window. He calls you the next day saying it’s all fixed. When you pick up your car, you find the window works fine; but the car won’t start. It’s not likely you will return to that mechanic because he’s clearly an idiot.
