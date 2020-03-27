# Symptoms

Occassionally,
when the printer homes (especially when a print has just finished),
only the x tower seems to be raised.

As result,
the effector is crashed into the X tower,
and the homing routine reports failure.

# How it should work (background)

The homing is done in two stages, which anyone can see when it is done successful:

1. all towers raise until any of the endstops trigger, after that
1. the towers are homed one, by one in x-y-z order

# What is the problem

The original Anycubic Kossel,
is not properly protected against electromagnetic interference (EMI).

The EMI causes a false positive endstop reading on one of the towers (any of them really),
which triggers the second stage of the homing process too early.

When this happens,
the effector always crashes into the X tower,
because the prematurely triggered second phase starts with homing the X tower.

The EMI can trigger a false positive endstop reading on any of the endstops,
but the affected endstop is usually the X tower's,
because it's where the extruder motor is mounted.

EMI is mainly caused by
* the heated bed (high current and PWM)
* heated bed wiring (uses high current and PWM)
* stepper motors (high frequency PWM)
* stepper motor cables (high frequency PWM).

# Mitigation

## Solution

Use of a hardware noise filter is the only reliable solution.
Either build it in, or use a board (or endstop) which has one built in already.
This is also recommended by the Marlin endstop page (https://marlinfw.org/docs/hardware/endstops.html).

## Workarounds, helping

These are only workarounds, because they do not _eliminate_ the problem, but reduce the frequency of the problem occuring. Some of them may be combined to reduce the chance of occurance even further.

* use g-code (G0, G1) to raise the head near the top before homing: this is limited in use, because G0 and G1 moves are only processed when the exact location of the head is known. The move command will not be executed (head raised before homing) if 
  * the printer was just turned on (position was never known), or
  * after the steppers were disabled (position was lost), or
  * geometry of the printer has changed (position became invalid).
* disable extruder motor and heated bed before homing: these are the most notorious emi sources, but not the only ones
* twist the endstop cables (see https://en.wikipedia.org/wiki/Twisted_pair)
* use EMI shielded endstop cables 
* rearrange the cables. This mainly means to distance them from EMI sources.
  * pull them away from the heated bed, and its high current wiring
  * route extruder motor cable and y endstop cable on different sides of the tower
  * prevent routing power cables from PSU close to endstop cables

## Workarounds, not helping

These are the workarounds which seemingly help, but cause other problems, therefore should not be used.

* Enabling the software noise filter (ENDSTOP_NOISE_FILTER): This helps cartesian printer, which is not sensitive to shifts in X and Y planes, but due to the +/- 0.2mm inaccuracy it adds (https://marlinfw.org/docs/hardware/endstops.html#software-filtering) it utterly interferes with a delta printer.
