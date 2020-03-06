# How it should work

The homing is done in two stages, which anyone can see when it is done successful:

1. all towers raise until any of the endstops trigger,
1. after that the towers are homed one by one in x-y-z order

# What is the problem

On the origiginal kossel , which is not protected agains electromagnetic interference (EMI), the EMI causes a false positive endstop reading, which triggers the second stage of the homing process too early.
This can happen on any endstop, but it is usually the y tower where the extruder is mounted.

EMI is mainly caused by
* the heated bed (high current)
* heated bed wiring (uses high current and PWM)
* stepper motors (high frequency PWM)
* stepper motor cables (high frequency PWM).

# Mitigation

## Solution

Use of a hardware noise filter is the only reliable solution.
Either build it in, or use a board (or endstop) which has one built in already.
This is also recommended by the Marlin endstop page (https://marlinfw.org/docs/hardware/endstops.html)

## Workarounds

* raise the head near the top before homing: this is limited, because moves are processed when the exact location of the head is not known - so it does not work always.
* disable extruder motor and heated bed before homing: these are the most notorious emi sources, but not the only ones
* twist the endstop cables, even shield them if you can.
* rearrange the cables. This mainly means to distance them from EMI sources.
  * pull them away from the heated bed,
  * route extruder motor cable and y endstop cable on different sides of the tower
  * etc
