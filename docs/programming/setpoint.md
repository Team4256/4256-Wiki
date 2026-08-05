# Setpoint

setpoints are objects that defined the desired output of a motor.
for example a setpoint that tells a motor to apply 6 volts would look like this:

```java
public Setpoint setpoint = Setpoint.withVoltage(6.0);
```

a motor component can then use this action by calling the `applySetpoint()` method:

```java
public Setpoint setpoint = Setpoint.withVoltage(6.0);
component.applySetpoint(setpoint);
```

setpoints contian information about what type of control the motor should apply, such as voltage, position, or velocity.
by defualt all motor components can consume every type of control.
ultimately deciding which setpoint mode to use is specific to the type of mechanism being controlled.
for example an arm mechanism might use a position setpoint while a shooter mechanism might use velocity setpoint and a roller mechanism might use voltage setpoint.
in summary setpoints allow the user to define the desired control mode of the motor and also the desired output value.
