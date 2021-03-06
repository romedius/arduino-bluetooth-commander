CommandInterpreter is a shell-like command interpreter that parses one 
command + two arguments per line from char buffer of a serial connection,
which is a Bluetooth Smart (low energy) UART in this case.
One command is limited to 20 chars as the UART nRf8001 Bluefruit hardware cannot process more
than that in one UART message/packet. Return messages can be assembled by the
software on the phone to larger messages.

Example commands:
  * "blink" with argument "on" or "off": blink [ on | off ]
  * "dwrite A1 H"  ... digitalWrite(A1, HIGH)
  * "pmode A2 O"   ... pinMode(A1, OUTPUT)
  * "awrite 3 128" ... analogWrite(3, 128)

Download and install the dependent library [Adafruit_nRF8001](http://github.com/adafruit/Adafruit_nRF8001)
then copy CatsCommandInterpreter/* to your libraries folder and restart the 
Arduino SDK. Open the example as sketch and study it.

Use an UART Serial App like this: https://itunes.apple.com/at/app/nrf-toolbox/id820906058?mt=8

USAGE:

    #define CMD_MAX_COMMANDS 7
    #include "CatsCommandInterpreter.h"
    CatsCommandInterpreter commandInterpreter = CatsCommandInterpreter();

    boolean command_blink(char* arg1) {...}
    
    setup() { commandInterpreter.addCommand("blink", command_blink); }
    
    rx() 
    {
      if(commandInterpreter.interpretCommand(buffer, len)) // check if command can be interpreted
        return;  // do not echo if command was a success
    }

![](https://raw.githubusercontent.com/katzlbt/arduino-bluetooth-commander/master/pictures/ArduinoProBluefruit.jpg)
