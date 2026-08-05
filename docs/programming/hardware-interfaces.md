# Hardware Interfaces

when writing robot code, we use hardware interfaces to seperate hardware logic from robot logic.
this is useful to create a divide between simulated and real hardware, as well as allowing for hardware from diffrent vendors to be swapped out easily.
the robot library included in the template repository comes with hardware interfaces already setup
when writting robot code, all you have to do is choose which vendor's hardware you want to use and pass in the correct configuration object.

heres and example of creating a TalonFX configuration object

```java
MotorIOTalonFXConfiguration config = new MotorIOTalonFXConfiguration("name", 0, new TalonFXConfiguration(), 1.0);
```

this creates a new MotorIOTalonFXConfiguration with a name "name", can ID 0, a TalonFX configuration, and a simulation settling time of 1.0 seconds.

this MotorIO object will determine at runtime wether to constructed a simulated motor
`new MotorIOSim()` or a real motor `new MotorIOTalonFX()` object

to summarize hardware interfaces define standard behaviors and interactions for written robot logic to communicate with hardware creating a standard interface for hardware communication.
