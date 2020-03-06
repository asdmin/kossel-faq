# How it should work

The homing is done in two stages, which anyone can see when it is done successful:

1. all towers raise until any of the endstops trigger, after that
1. the towers are homed one, by one in x-y-z order

# What is the problem

On the original kossel,
which is not properly protected against electromagnetic interference (EMI),
the EMI causes a false positive endstop reading,
which triggers the second stage of the homing process too early.
This can happen on any endstop,
but it is usually happening to the Y tower endstop,
because it's where the extruder is mounted.

EMI is mainly caused by
* the heated bed (high current and PWM)
* heated bed wiring (uses high current and PWM)
* stepper motors (high frequency PWM)
* stepper motor cables (high frequency PWM).

# Mitigation

## Solution

Use of a hardware noise filter is the only reliable solution.
Either build it in, or use a board (or endstop) which has one built in already.
This is also recommended by the Marlin endstop page (https://marlinfw.org/docs/hardware/endstops.html)

## Workarounds

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
