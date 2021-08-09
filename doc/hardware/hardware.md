---
title: Hardware
nav_order: 2
---
# Hardware
## Components
These are the components I used, but you should be able to find alternatives
for most of them if necessary.
I've included some replacement suggestions where applicable.
- **SparkFun Pro Micro (5V, 16MHz)**  
  - Alternatives: any ATmega32u4-based Arduino-compatible microcontroller
  with sufficient (ideally >=8) analog inputs
- **64 photoresistors**  
  Alternatives:
  - Reed switches (need magnetic pieces)
  - Hall sensors (need magnetic pieces and different wiring)
  - Induction sensors (need weighted pieces)
- **64 diodes**
- **Shift register**
  - Can be omitted if enough digital outputs are available
- **8 resistors**
- **Cables and soldering supplies**

## Circuit board
![Circuit board](/assets/images/circuit-board.png)

## Board wiring

## Basics
### Sensor choice
**TODO**

### Multiplexing
LiBoard uses a photoresistor in each square in order to determine which squares
are occupied. Each photoresistor needs to be connected to 5 V and an analog input.  
Because wiring each photoresistor to an individial input would need more inputs than
commonly available and would result in messy wiring, the photoresistors should be multiplexed:  
![](/assets/images/3x3-multiplexing.png)
Due to the  layout of a chessboard, 8x8 multiplexing is the most natural way.
However, if you have fewer than 8 analog inputs available, you should be able to do 16x4 multiplexing.

### Shift-register
While I had 8 digital outputs available,
I chose to use a shift register to reduce the number of outputs needed.  
**TODO**  
The diodes after the shift register are not strictly necessary.

### Pull down resistors
**TODO**
