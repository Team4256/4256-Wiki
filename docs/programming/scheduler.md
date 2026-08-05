# States

now that we have created components and subsystems to group related compoents togethor we must tell the robot how to sequence and schedule these diffrent subsystems.
the Lib defines overall robot states that define a global state the robot can be in.
however unlike actions the robot may be able to consume multiple states at a time as they run concurrently.
A state is created fistly with a step object that defines the state's behavior.
the step object is a faux corotuine allowing it to be run concurrently with other states.
for example states are created staticly with:

```java
State state = State.withStep();
```

by defualt with step returns a coroutine that runs a single time and then finishes.
but using other step methods we can define more complex behavior with specific control.
using `Step.loop()` any runable provided will run indefinetly until the state is interupted.
using `Step.waitSeconds()` the coroutine will wait for a specified number of seconds before continuing.
using `Step.await()` the coroutine will wait until a specified condition is met before continuing.

using all of these methods together we can define complex behavior for our robot.

however only defining a state with a step leaves out information the robot needs to log data about the state and sequence multiple states together.

we can use `State.withStep().withName()` to define a state with a step and a name.
we can use `State.withStep().withCleanup(State)` to define a state with a step and a cleanup state that runs when the state is interupted.
we can use `State.withStep().withFinish()` to define a state with a step and a finish state that runs when the state is finished.
we can use `State.withStep().isInterruptible()` to define a state with a step and a boolean value indicating whether the state is interruptible or not.
we can use `State.withStep().withName()` to define a state with a step and a name.
we can use `State.withStep().withIgnoreDisabled()` to define a state with a step and a boolean value indicating whether the state can still be scheduled when the robot is disabled.
we can use `State.withStep().withRequirements(new ActionSubsystem())` to define a state and provide it with a requirement in the form of an action subsystem.

# Scheduler

the scheduler is responsible for sequencing and scheduling states on the robot.
