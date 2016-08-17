# RoboLib
Arduino library to transfer arrays of data from Processing.

This is a simple one file Arduino library to allow accurate transmission of data. `Serial` `read` and `write` are useful enough to transfer just one variable. More than that and the Arduino may loose packets of data or mix values up. Consider the following situation:

Processing reads data from joystick controller and sends two values every 20ms `(leftMotorPower, rightMotorPower)`. The Arduino will receive both values, but how will it differentiate between the two? Setting the right motor power to `leftMotorPower` would be disastrous in most cases. To solve this problem, many have used letter tags to help the Arduino tell which value is for which variable. This library provides an easy to use object that will keep track of multiple values of data in a single array.

## How to use RoboLib
1. Include the RoboLib library: `#include <RoboLib.h>`

2. Create the RoboLib object: `RoboLib myBot(dataSizeConst, totalchar);`
    - `dataSizeConst` is the **number of variables** you want to transfer
    - `totalchar` is the **number of characters** being transmitted at one time

3. In `void Setup()`, initialize RoboLib: `myRobot.begin(baudRate);`

4. In `void serialEvent()`, save the data: `myBot.saveData();`

5. In `void loop()`, get the data and save it to a local variable: `processedData = myBot.getData();`

Send all your data at once semicolon delimited:
```c
string = var1 + ";" + var2 + ";" + var3 + ";" + var4 + ";" + var5 + ";\n";
port.write(string);
```
**Note:** There can be more than five variables. [Example of sending data](https://github.com/neilhazra/2014Bot/blob/master/_2014BotController/_2014BotController.pde#L85).

[A full example of RoboLib at work](https://github.com/neilhazra/2014Bot/blob/master/2014BotArduino/src/2014Bot.ino).

## How it works
1. Arduino reads all the data at once until a newline.
2. Using string split and `toCharArray` C commands, each variable is isolated and casted to a double.
3. Methods used to get processed values.
4. Arduino reads all the data at once until a newline is reached.
