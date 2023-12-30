OVERVIEW:

This program loads a keyframe animation from an .anim file (described below) and plays it back on a skinned character. The program should be able to load any .skin, .skel, and .anim file given to it, and should accept them as command line arguments. For example: project3 monster.skel monster.skin monster_walk.anim

.anim FILE DESCRIPTION:

The .anim file contains an array of channels, each channel containing an array of keyframes. For a simple example, see sample.anim. The sample is just a very basic example of an anim file and doesn't correspond to any useful animation.

The structure of the anim file is as follows:

animation {
    range [time_start] [time_end]
    numchannels [num]
    channel {
        extrapolate [extrap_in] [extrap_out]
        keys [numkeys] {
            [time] [value] [tangent_in] [tangent_out]
            ...
        }
    }
    channel {
       ...
    }
    ...
}

The [time_start] and [time_end] describe the time range in seconds that the animation is intended to play. This range doesn't necessarily correspond to the times of the first and last keyframes.

The number of channels [num] will be 3 times the number of joints in the character, plus an additional 3 for the root translation. The channels are listed with the 3 root translations first in x,y,z order, followed by the x,y,z rotation channels for each joint in depth-first order.

The extrapolation modes [extrap_in] and [extrap_out] will be one of the following: "constant", "linear", "cycle", "cycle_offset", or "bounce". [numkeys] specifies the number of keyframes in the channel.

The keys themselves will be listed in increasing order based on their time. Each key specifies its [time] and [value] in floating point. The tangent types [tangent_in] and [tangent_out] will be one of the following: "flat", "linear", "smooth", or it will be an actual floating point slope value indicating the fixed tangent mode.

PROGRAM OBJECTIVES:

- Loads an animation and stores it internally
- Ability to evaluate channel within key ranges
- All tangent types working properly
- All extrapolation modes working properly
