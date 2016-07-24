# ArduinoShiftIn
This is a small library for reading in values from a 74HC165 8 bit shift register.

The Arduino has only a limited amount of pins, therefore it might happen that you run out of pins.
For this case, the 74HC165 comes to the rescue. It is an 8 bit shift register. It allows you to read in 8 values by only using 4 pins on your Arduino. Furthermore you can daisy-chain several shift registers by still only using 4 Arduino Pins.

## Easy install (zip import)
The easiest way to install this library is by downloading the newest release and then importing it.
You don't have to unzip it. Just open your Arduino IDE and navigate to *Sketch* > *Include Library* > *Add .ZIP* and then select the zip file.

## Manual install
Of course you can also install this library manually. To do so, download the newest release and unzip it. Then you have to copy the ``ShiftIn`` folder (NOT the ``ShiftIn-x.y.z`` folder) and copy it to your Arduino library folder:
* Windows: ``My Documents\Arduino\libraries\``
* Mac and Linux: ``Documents/Arduino/libraries/``

After that you just have to restart your Arduino IDE.

## Usage
If you have installed this library, you can include it by navigating to *Sketch* > *Include Library* > *ShiftIn*. This will add the line ``#include <ShiftIn.h>`` to your sketch (of course you could also write this line manually).

Now you can actually use this library:
``` c++
#include <ShiftIn.h>

// Init ShiftIn instance with one chip.
// The number in brackets defines the number of daisy-chained 74HC165 chips
// So if you are using two chips, you would write: ShiftIn<2> shift;
ShiftIn<1> shift;

void setup() {
  Serial.begin(9600);
  // declare pins: pLoadPin, clockEnablePin, dataPin, clockPin
  shift.begin(8, 9, 11, 12);
}

void displayValues() {
  for(int i = 0; i < shift.getDataWidth(); i++)
    Serial.print( shift.state(i) ); // get state of button i
  Serial.println();
}

void loop() {
  if(shift.update()) // read in all values. returns true if any button has changed
    displayValues();
  delay(1);
}
```
![Breadboard layout](ShiftIn/examples/SingleShiftRegister/Layout1.png)
