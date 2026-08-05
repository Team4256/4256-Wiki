# Subsystems

Subsystems are defined systems that represent a specific and self-contained part of the robot.
Subsystems in code defined by a `periodic()` method that is called every loop iteration and a `periodicAfterScheduler()` method that is called after the scheduler.
They also contain a `disable()` method that is called when the subsystem is disabled.

they are typically created using the `Subsystem` class to extend a new class.

```java
public class UserSubsystem extends Subsystem {
}
```

they are useful to define methods that need to be called periodically in the `Robot.java` file.

## Action Subsystems

The base subsystem class is useful for defining periodic behavior but when these subsystems need to take some defined action on the robot, the `ActionSubsystem` class is useful.
The component architecture is designed to work primarily with action subsystems.

```java
public class UserActionSubsystem extends ActionSubsystem {
}
```

Action Subsystems still contain a `periodic()` method that is called every loop iteration and a `periodicAfterScheduler()` method that is called after the scheduler since they extend the `Subsystem` class.

```java
public class ActionSubsystem extends Subsystem {

}
```

the `periodic()` method now updates all the inputs of the components registered to the subsystem.
the `periodicAfterScheduler()` method now applies the given action of the subsystem.

An important design consideration is that action subsystems can only be given a single action at a time.
This is implemented to keep subsystems on the robot safe and prevent multiple actions from being applied simultaneously creating undefined behvior.

## Actions

Actions are defined as objects that contain a name for loggind and a Runnable that defines the action to be taken.

The `ActionSubsytem` contains a helper method `action()` that returns an `Action` object that is registered to the subsystem.

```java
/**
   * Creates an {@link Action} bound to this subsystem.
   *
   * @param name   name used for AdvantageKit logging
   * @param action runnable executed when the action runs
   * @return the newly created action
   */
  public Action action(String name, Runnable action) {
    return new Action(name, this, action);
  }
```

in this method the keyword this refers to the `ActionSubsystem` instance that the method is called on and is used by the `Action` constructor to associate the action with the subsystem.

an example of creating an action with the `action()` method:

```java
public Action action = action("name", () -> {
    //runnable code here
  });
```

this creates a new action stored in the variable `action` with the name `name`.

## Action Subsystem Example

```java
public class UserActionSubsystem extends ActionSubsystem {

  private final MotorComponent component = motorComponent(
    "Component Name",
    new MotorIOTalonFXConfiguration("name", 0, new TalonFXConfiguration(), 1.0);
  );

  public Action action = action("name", () -> {
    component.applySetpoint(Setpoint.netural());
  });

  public UserActionSubsystem() {

  }
}
```

this is a created action subsystem that defines a motor component and an action that applies a neutral setpoint to the motor.
