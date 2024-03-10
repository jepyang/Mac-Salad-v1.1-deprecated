(please note, this version of mac salad is officially deprecated. no additional
updates will ever be made, no additional documents will ever be posted. this
material is posted here purely for reference.)

# Mac-Salad
A utilities module for eurorack

## First off, some labeling conventions

Inputs have a white line and are grouped to the left. If there is a
signal normalized to the input, it is listed next to the jack with a dotted
line.

Outputs have a silver line and a silver arrow and are grouped to the right

Seven jacks have a little flower growing on them. The six inputs with
the flower, in addition to their regular function, form a mixer routed
to the output jack with a flower, “Da Kine” (more on this later).

## Now the controls…

There is a big knob and an input jack labeled “Scoop”. The signal at the
jack (bipolar signals are fine) is summed with the knob’s offset (+/-5V).
The result (I’ll just call it Scoop from here on out) is used internally
in several locations, either as a normalled connection or a control signal.

## Next is the panner/fader.

This section has four inputs: right, left, fade, and offset. Right and left
are normalled to +5V and -5V respectively. Fade is normalled to
Scoop. There is also a knob for attenuating the signal at Fade.

It’s got two outputs: right and left.

Essentially, it’s two crossfaders that work in opposition to one another.

So with Fade at -5V, you get 100% of the left input and 0% right at the left output, and 100% right, 0% left at the right output.

As you increase the voltage into Fade, each output fades from one input to
the other. So at 0V, you should get equal parts left and right inputs at
both the left and right outputs. And at +5V, you get 100% of right in the
left output, and vice versa.

So using 2 inputs and 1 output is a crossfader; 1 input and 2 outputs is a
panner; or 1 input and 1 output is a VCA!

The fourth input is Offset, it simply sends signal to both inputs.

There is also a trimmer around back for adding offset to the Fade control.
This is usually gonna be at or near zero, but it’s an adjust-to-taste situation.

One last note on the fader section… It’s made of four vactrol-based VCAs.
So the response is a little weird and nonlinear, and they don’t turn off as
fast as they turn on.

It’s not a bug, it’s a feature!

They definitely aren’t mathematically ideal VCAs. But they have some
character! They work mostly like how you expect them to, but when they
don’t, they usually do it in a musically interesting way.

There are a bunch of trimmers to help match all the VCA levels.

## Next section: analog logic!

We have an OR circuit and an AND circuit, both w/ two inputs, one output.

Analog logic can be weird if you’re used to digital logic, but it’s
exactly the same. For OR, if either one input or the other is high, the
output is high. The only difference here is that you can use analog input
to get analog output. Whichever OR input has high*er* voltage at any
given moment is the signal you’ll see at the output.

AND works similarly, except that it always outputs whichever signal has
lower voltage at any given moment.

You can maybe see how the two outputs here would be complementary. As such,
the first AND input is normalled to the first OR input, and both second
inputs are normalled to Scoop. With a signal going into OR(1), OR out will
always show any part of the signal above Scoop, and AND out will show
whatever portion of the signal falls below Scoop.

## Rectify

Rectify is a simple one. One input, one output. It’s a full wave rectifier!

Basically, whatever goes in, you get the absolute value out. Any part of
the signal that falls below 0V gets flipped positive.

Something fun: if you put in a saw wave, you get a glitchy triangle wave
out. If you put in a triangle wave, you get another triangle wave at
double the frequency out.

## Follow

Follow is an envelope follower based on the one in the ARP2600. It has no
input of its own—it takes its input from the Rectify input jack.

Basically if you feed it audio, it generates an envelope/control voltage
according to the volume of the input.

So feed it, for instance, a kick drum. Every hit of the drum would generate a
little envelope at the Follow jack, which could open a filter. Or you
could invert the output and send it to a VCA and you have a basic
sidechain compressor effect!

## Puka

Puka is a weird one. It’s a sort-of wavefolder…

Basically, anytime the input is positive, Puka adds a -5V offset to
the output; and when the input is negative, a +5V offset is added. The
result is a 10V discontinuity at every zero-crossing.

It’s kinda hard to grok without looking at the result. But if you
send a sweep from -5V to +5V, the output starts at 0V, will climb to
+5V until the input hits 0V…at which point the output swings
instantaneously from +5 to -5V, then climbs again till 0V.

## Then we have Holoholo...
**...(which means “wander aimlessly”).**

This is the most idiosyncratic circuit in the module—I’m not aware
of any other eurorack module besides Cold Mac that includes anything
similar. (I think there’s some Buchla or maybe Serge modules that have
something similar?)

One output, takes input at the Puka jack.

This is actually an analog computing circuit. The output is the integral
of the input…if calculus is your thing.

If calc isn’t your thing…

Basically anytime the input is positive, the output will climb; and
when the input is negative, the output will fall. The amplitude of
the input, either positive or negative, determines the rate at
which the output moves.

So if the input is 1V, the out will sloooowly drift up, no matter its
current value. If the input goes to 5V, the out will drift up much
faster. And if the input goes to 0V, the out remains at its current level.

Everything else in Mac Salad can technically be replicated with other
modules. Even Puka can be put together with a comparator, an
inverter, and a mixer. It’s more about how it’s all pre-connected that
makes it so useful.

But Holoholo… you can’t really build it from other blocks! As a function,
it can’t really be broken down into simpler bits. It’s, uh, not super
useful, but it is really neat.

One cool function for it though: I realized you could combine two of
these with a joystick controller to control the X and Y coordinates of a
point. The further you push the joystick in a direction, the faster
the point will move in that direction. If you let the joystick
snap back to center (0V), the point will stop where it is. Neat! Analog
video games on your modular synth!

## Da Kine

Ok so I mentioned the jacks with the little flowers before—the Da Kine
circuit—now a little more detail.

There are six inputs with flowers. Besides the regular functions they go
to, they’re also sent to Da Kine. First they’re AC-coupled (removes any
DC offsets, which makes this circuit audio-only, no CV), then sent to a
unity mixer, and then finally sent to a VCA. Scoop controls the VCA.

Simple, and gives you a handy way to use inputs that would otherwise be
left unused in a patch!

## And finally, Mauna

As I worked up the schematic, I ended up with an extra VCA. Very simple,
one in, one out, controlled by Scoop.

It is normalled to Right…for no real reason 😅 I thought maybe there could
be creative ways to use it alongside the crossfader/panner, but I haven’t
come up with any specific applications beyond “hey, free VCA.”

That said, Right is itself normaled to +5V, the effect of which is that a
bipolar signal going into Scoop and out Mauna will be scaled to fit between 0-5V

## And that’s it!

There are a lot of interesting ways to use this module. Some are more
apparent than others. 

You put one CV signal into Scoop and right off the bat you get nine
different variations on it. And the big ol knob can add even more flavor
by messing with the offset.

Or you can use it like six or seven totally separate utility modules!


Combine multiples for wildly complex patching.

Fun stuff :) I’m excited. 😁



cc-by-nc-sa

no part of this project may be used, for training or otherwise, in conjunction with
AI algorithms or any machine-learning without the express permission of the author

absolutely, strictly, 100% non-commercial
