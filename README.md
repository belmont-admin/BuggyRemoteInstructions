# Remote control a MOVE:mini Mk1

## Introduction @unplugged

In this session you will code a second @boardname@ to act as a remote control for the MOVE:mini robot buggy so you can drive it in a race. 

Code is already loaded onto the MOVE:mini and you have been given a printout of that code. Your first job is to look at the code for the buggy and understand how it works so that you can use that knowledge to program your remote control @boardname@.

## Step 1 - Radio Group

Your buggy has your name on one wheel. On the other wheel is a number. This is the **Radio Group** that your buggy is listening for messages on. Your remote control needs to use the same **Radio Group** number.

Use an ``||basic:on start||`` block together with a ``||radio:radio set group (N)||`` block to set the right **Radio Group** for your buggy.

Also add a ``||basic:show arrow||`` block to display and arrow on your remote control @boardname@ so that you can see it's turned on and ready to use.

```blocks
radio.setGroup(100)
basic.showArrow(ArrowNames.North)
```
## Step 2 - Program an emergency stop!

If you make a mistake in your code then it's possible your buggy will drive and not stop so you'll be chasing around trying to catch it and you could break it. For this reason it's sensible to program an emergency stop. Simply shake your remote at any time and your buggy should stop.
```blocks
input.onGesture(Gesture.Shake, function () {
    radio.sendNumber(0)
})
```
Make sure you understand why sending a **0** stops the buggy by looking at the buggy's code.

## Step 3 - Send a command to the buggy to drive forwards

The most sensible  way for the remote to work is:

`
Buttons A+B together  - drive forwards
Button A only         - turn left
Button B only         - turn right
`

Look at the code for the buggy and you can see that the buggy will drive forwards if it receives the **number** 1.

Add a ``||basic:forever||`` block to continually check to see if the A+B buttons are pressed at the same time using a ``||input:button A+B is pressed||`` test. You will need a ``||logic:if then||`` block inside your ``||basic:forever||`` block. Use a ``||radio:radio send number (N)||`` block to send the **1** to the buggy.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        radio.sendNumber(1)
    }
})
```

Now click the **+** sign at the bottom of the ``||logic:if||`` block so that you get an ``||logic:else||`` section. In this section send a **0** to the buggy using a ``||radio:radio send number (N)||`` block so the buggy will stop if the buttons are not pressed.

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        radio.sendNumber(1)
    } else {
        radio.sendNumber(0)
    }
})
```
## Step 4 - Send commands to the buggy to turn left and right

Now click the **+** sign again so you get an ``||logic:else if||`` section. In this section add the ``||input:button A is pressed||`` test to check for button ``||A||`` being pressed and then the ``||radio:radio send number (N)||`` block with the correct number to make the buggy turn left.


```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        radio.sendNumber(1)
    } else if (input.buttonIsPressed(Button.A)) {
    	
    } else {
        radio.sendNumber(0)
    }
})

```
Now add a ``||radio:radio send number (N)||`` block to send the correct number to make the buggy turn left.

### ~hint

#### Remember the numbers the buggy understands

`
0   - stop
1   - drive forwards
2   - turn left
-2  - turn right
`

### ~

Finally click the **+** on the ``||logic:if||`` block once more to get another ``||logic:else if||`` section where you can add the test for button ``||B||`` being pressed and sending the correct number to the buggy to make it turn right.

Once your code is complete use it to drive you buggy along the race track.

## Step 5 - Add some colour

Look at your sheet with code for the buggy and see if you can add some ``||radio:radio send string ("Text")||`` blocks to your program which will turn the neopixels on in different colours while you are driving.
