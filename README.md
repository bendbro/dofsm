# dofsm
Database oriented finite state machine

### What do you mean by database?
For my purposes, a database holds arrays of data representing some state of the world at a certain time.

### What do you mean by finite state machine?
What it usually means: a machine expressed as states, and transitions between states, non-deterministic.

### What do you mean by database oriented?
States are more than just occupied or not-occupied. A state may be any value. Upon the change of a state, a turing-complete transition may be configured to fire, updating other states.

### What is the motivation?
Create a language for complex systems that model the world with data. The language should make it easy to validate how data has changed and how data will react to change.

Ex: An advertising firm has a number of separate teams that develop and deploy advertisements. The teams each share some parts of their software stacks, but often each have an isolated pool of data. Business needs cause code to be written that pulls from each of those isolated pools of data. That code may drive changes back into each pool of data. Without a language expressing how data from one pool relates to another, it is complicated to operate on the data. What may change the data is obscured (the code that affects the data is in a number of separate repositories), why the data changed is lost (a database write from system A is stored the same as one from system B), and reuse of query/update logic is weakly enforced.

The world has a state. When the state of the world changes, an effect, there is a cause. Causes are triggered by changes to the state of the world. When the state of the world changes, the effect it has is predictable and consistent.

The ultimate purpose of software is to model the state of the world and how the world changes. Data is commonly used to model the world's state. Programs are commonly used to model how that data changes, they model the relationship between cause and effect. In this view, programs should be treated as predictable and consistent relationships between pieces of data representing parts of the state of the world.

Existing programming languages fail to accomplish this. 
<br>This failure is because existing programming languages encourage an approach that does not model reality:
<br><BLOCKQUOTE>*The next step of a program is decided by considering the meaning of the previous step.*</BLOCKQUOTE>
<br>Rather than:
<br><BLOCKQUOTE>*The next step of a program is decided by the contents of the state of the world.*</BLOCKQUOTE>

### What it should do:
* Store states as the following list of data: name, value, time, revision id, transition, transition call id.
* Store transitions as first class citizens. Changes to the system (ie. deployments) should be supported natively, seamlessly, programatically.
* Enable investigation features: tracebacks (what caused a state to have a given value), forward simulation (what happens if I set a state to a given value), backward simulation (what could happen to make a state take a given value), and formal verification capabilities.
* Transparently model asynchrony and parallelism.
* Support forks, merges with other database oriented finite state machine instances (for testing, security, etc)
* Support arbitrary storage mechanisms
* Support arbitrary execution mechanisms

### What it should not do:
* Strive to ensure the language itself is turning complete. It should include the capacity to embed turing complete languages.
