## Circuito de proteccion de conexion poaridad inversa
# 

Let's say you have a 12 volt power source like a battery and you want to power something.

It doesn't matter what it is. Let's say it draws 2 amperes.
When the battery is connected the right way around everything works fine.

But if you've had a little too much to drink and you plug it in backwards...

BOOM! Your circuit blows up.

The simplest way to protect yourself here is to use a diode.

If the power is connected backwards, no current can flow through the diode,

so your circuit is safe.

But there's a downside to doing this.

As you'll remember from my diode tutorial, the heat generated in a diode

is given by the forward voltage multiplied by the current.

So for example with this 1N5401T diode

you've got a forward voltage drop of about 0.85 volts.

0.85 volts multiplied by 2 amperes = 1.7 watts of heat

that you have to deal with. And that's bad.

Now let's try to make that a little more efficient.

Let's use a schottky diode which will give us a lower forward voltage.

This STPS2L60 should work.

At two amperes it has a forward voltage of about 0.55 volts.

The other reason why I chose this diode is because it has a low reverse leakage current

of under 100 microamperes.

You have to be careful with schottky diodes because a lot of them will have

high reverse leakage currents

of several milliamps, making them a bad choice for reverse voltage protection.

Okay let's do the math again. 0.55 volts multiplied by 2 amperes = 1.1 watts of hear.

That's better than the 1.7 watts of heat that we had with the

regular diode.

But we can do even better and not everyone knows this technique.

First, get yourself a P channel MOSFET like this FQP47P06.

Pay very close attention to which pins are "gate", "drain" and "source".

Next, put it in your circuit like this.

Now when the battery is connected the right way around the transistor will

turn on allowing current to flow through it.

And when the battery is connected backwards, the transistor turns off,

and your circuit gets protected. So you can be as drunk and irresponsible as you want.

This protection circuit is a lot more efficient and I'll show you the numbers

later in the video.

First let's talk about how it works.

Let's do an analysis when the battery is connected the right way around.

A P channel MOSFET will turn on when the voltage between the "gate" and

the "source" is around -4 volts, or more negative than that.

The exact "gate" threshold voltage will depend on what MOSFET you're using.

The MOSFET has a parasitic body diode. So when we first connect the battery,

there will be a small voltage drop across that diode.

It will be roughly a 1 volt drop.

So 12 volts minus 1 volt means that the "source" pin is at 11 volts

with respect to the circuit's ground.

Now what about the "gate" voltage?

Well we connected the "gate" directly to the circuit's ground, so the "gate" voltage is 0.

So, the voltage between the MOSFET's "gate" and "source" is 0 volts minus 11 volts

which is -11 volts. And like I said earlier, since this is a

P channel MOSFET

if Vgs -4 volts or less, the transistor will turn on.

And once it's on, you don't have to worry about that parasitic diode anymore,

because the resistance between "drain" and "source" drops to almost nothing.

Now let's do an analysis where the battery is connected backwards.

Since we're keeping the ground symbol in the same place,

that means that this node in the circuit is 12 volts less than ground.

So it's -12 volts.

And just like before, the "gate" is at zero volts.

Now, you know the MOSFET is supposed to be off in this situation because I

told you so.

But how do we prove it?

Well, let's pretend for a second that the MOSFET is on.

If the MOSFET is on, the resistance between "drain" and "source" is almost zero.

So that means that the voltage at the "source" is going to be almost the same as

the voltage of the "drain".

So we've got -12 volts at the source assuming that the MOSFET is on.

Now let's calculate Vgs again.

Vgs is zero volts minus -12 volts

so Vgs is 12 volts.

Wait a minute...

Vgs has to be -4 volts or less for the MOSFET to turn on

and we just calculated Vgs to be +12 voltswhen the transistor is on.

What we've got here is an impossible contradiction.

So our initial assumption of the MOSFET being on has to be incorrect.

So what this means is when you've got the battery connected backwards it's

impossible for the P channel MOSFET to turn on so your circuit is safe.

Now let's talk about the power loss in the circuit.

Earlier I mentioned that when the transistor is on the resistance between

"drain" and "source" is almost nothing.

But to be more accurate,

the resistance is a parameter called "Rds(on)" and you can find it out from

the transistor's datasheet.

The exact value will vary depending on the "gate" voltage and temperature

but for the sake of simplicity you can just estimate it with the maximum value

they give you. So let's say it's 26 milliohms.

When you have steady DC flowing through the MOSFET the power loss is

given by current*current*resistance.

So 2 amperes multiplied by 2 amperes multiplied by 0.026 ohms = 0.104 watts.

That's seventeen times less than what we had with the initial diode.

So now you can design more efficient killing machines.

Finally I want to talk a little more about how to choose the right P channel MOSFET for

your application.

The first and most obvious thing is that the "drain-source voltage rating" has to

be higher than your power supply's voltage.

In this video I used a 12 volt battery so 60 volts is more than

enough.

Next, you want "Rds(on)" to be as low as possible to minimize the resistive power

losses.

Finally, you need to pay very close attention to the maximum "gate-source voltage".

One of the reasons why I chose the FQP47P06 for the video

is that it has an unusually large "gate-source" breakdown voltage range.

+/- 25 volts.

However, other MOSFETs may have a maximum "gate-source voltage" of only 15 volts

or less.

So here's how you can get the P MOSFET to work with a higher voltage input.

Let's say our input voltage is exactly 30 volts.

If we add a resistor and a 10 volt zener diode to the circuit

we can clamp the "gate-source voltage" to a maximum of -10 volts.

So now the transistor is safe.

Something like this 1N5240 would do the trick.

It doesn't have to be exactly a 10 volt zener diode... something in the 6 volt to 12 volt

range would probably be fine depending on the MOSFET.

Alright you are now an expert at reverse voltage protection!

Check out my other videos for more stuff about electronics!
