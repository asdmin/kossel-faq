When the printed object is not accurate on the x-y plane, the length of the diagonal rods are not correct.

The problems can be classified in two groups:

- difference of length between firmware and reality,
- the 6 diagonal rods are not exacly the same long.

### Difference of length between firmware and reality

In this case, on x and y axis, all dimensions will be equally off.
This can be mitigated by multiplying diagonal rod length and delta radius in the firmware with the inverse of the error.

### The 6 diagonal rods are not exacly the same long

This prevents the effector from moving in a plane, and also twists and twirls it on the way.

Direct results are:

- leveling problems (which the bed leveling routine usually hides),
- dimensional inaccuracy on x-y plane, where the error on x and y is not the same,
- accelerated wear on rods and joings, which in extreme cases can simply snap.

This type of problem is best resolved by replacing the arms of the printer.
