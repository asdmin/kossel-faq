### My prints are too big / too small in x-y dimensions, but completely OK in Z, why?

When the printed object is not accurate on the x-y plane, the length of the diagonal rods are not correct.

The problems can be classified in two groups:

- difference of length between firmware and reality,
- the 6 diagonal rods are not exacly the same long.

### Difference of length between firmware and reality

In this case, on x and y axis, all dimensions will be equally off.
This can be mitigated by multiplying diagonal rod length and delta radius in the firmware with the inverse of the error.

This problem is usually paired with different levels of **over- or underextrusion**, because the printer calculates the extruded material for the volume which shall be printed, but since it _actually_ prints a smaller or bigger piece, the material will be too much (too little) respectively. 

### The 6 diagonal rods are not exacly the same long

This prevents the effector from moving in a plane, and also twists and twirls it on the way.

Direct results are:

- leveling problems (which the bed leveling routine usually hides),
- dimensional inaccuracy on x-y plane, where the error on x and y is not the same,
- straight lines aren't really straight (slightly bent, usually detectable with a caliper),
- accelerated wear on rods and joings, which in extreme cases can simply snap.

This type of problem is best resolved by replacing the arms of the printer.

As workaround, one could

- rearrange the rods so, that rods going to the same tower are very similar in length, and
- follow up with complicated changes in firmware to compensate the differences between rod-pairs.

Generally speaking, the effort required for this usually exceeds the effort and cost required to order new sets of rods.
