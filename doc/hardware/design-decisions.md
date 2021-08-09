---
title: Design decisions
parent: Hardware
---
# Hardware design decisions
## Microcontroller choice
**TODO**

## Sensor choice
**TODO**

## Multiplexing
LiBoard uses a photoresistor in each square in order to determine which squares
are occupied. Each photoresistor needs to be connected to 5 V and an analog input.  
Because wiring each photoresistor to an individial input would need more inputs than
commonly available and would result in messy wiring, the photoresistors should be multiplexed:  
![](/assets/images/3x3-multiplexing.png)
Due to the  layout of a chessboard, 8x8 multiplexing is the most natural way.
However, if you have fewer than 8 analog inputs available, you should be able to do 16x4 multiplexing.

## Shift-register
While I had 8 digital outputs available,
I chose to use a shift register to reduce the number of outputs needed.  
**TODO**  
The diodes after the shift register are not strictly necessary.

## Pull down resistors
**TODO**
