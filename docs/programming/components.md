# Components

components are an encapsulation of defined ideas of robot behavior
think of components like lego pieces of resuable code that can be assembled to define the structure of a robot
for example to create a simple motor component that does not require feedback control

```java
private final MotorComponent component = motorComponent(
  "Component Name",
  new MotorIOTalonFXConfiguration("name", 0, new TalonFXConfiguration(), 1.0);
);
```

this creates a new motor component with the name "Component Name" and a MotorIOTalonFXConfiguration object

this motor component can now be used to control a talonFX motor by applying setpoints the topic of the next chapter

as well as allowing setpoint control the motor component with automaticly log a set of pre-defined motor inputs

```java
/** Telemetry snapshot for one motor, logged by AdvantageKit each cycle. */
  @AutoLog
  public class MotorInputs {

    /** Voltage applied to the motor windings. */
    public double motorVoltage = 0.0;

    /** Bus voltage supplied to the motor controller. */
    public double supplyVoltage = 0.0;

    /** Current drawn from the bus by the motor controller. */
    public double supplyCurrent = 0.0;

    /** Current through the motor windings. */
    public double statorCurrent = 0.0;

    /** Measured rotor position. */
    public double position = 0.0;

    /** Measured rotor velocity. */
    public double velocity = 0.0;

    /** Measured rotor acceleration. */
    public double acceleration = 0.0;

    /** Motor controller temperature. */
    public double temperature = 0.0;

    /** Active setpoint in the base units of the current {@link #mode}. */
    public double setpoint = 0.0;

    /** Control mode the motor is currently running in. */
    public Setpoint.Mode mode = Setpoint.Mode.NEUTRAL;

    /** Whether the motor controller is currently responding on the bus. */
    public boolean connected = true;
  }
```

these inputs will be automatically logged by AdvantageKit each cycle in the defined `UpdateInputs()` method and can be viewed on the network tables live and in the AdvantageKit log file later
