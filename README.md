# RoboLib
Arduino library to transfer arrays of data from processing. 

This is a simple one file Arduino library to allow accurate transmission of data. Serial read and write are useful enough to transfer just
one variable. More than that, the arduino may loose packets of data or mix values up. Consider the following situation:

Processing reads data from joystick controller and sends two values every 20 ms (leftMotorPower, rightMotorPower). The Arduino will recieve
both values, but how will it differentiate between the two. Putting the leftMotorPower to the right motor would be disastarous in most cases.
To solve this problem, many have used letter tags to help the arduino tell which value is for what variable. This library provides an easy
to use object that will keep track of multiple values of data in a single array. 

How to use RoboLib:

Include the RoboLib Library: #include <RoboLib.h>

Create the RoboLib Object: RoboLib myBot(dataSizeConst,totalchar);
**dataSizeConst is the number of variables you want to transfer
**totalchar is the number of characters being transmitted at one time

In void Setup() initialize robotlib: myRobot.begin(baudRate);

In void serialEvent() save the data: myBot.saveData()

In void loop get the data and save it to a local variable: processedData = myBot.getData();

For a full example of RoboLib in work view: https://github.com/neilhazra/2014Bot/blob/master/2014BotArduino/src/2014Bot.ino

What data to send. Send all your data at once semicolon delimited:
 string = var1 + ";" + var2 + ";" + var3 + ";" + var4 + ";" + var5 + ";\n";
  port.write(string);
  **Note: can be more than 5 variables
View https://github.com/neilhazra/2014Bot/blob/master/_2014BotController/_2014BotController.pde for a full example

How it works:
Arduino reads all the data at once until a newline. 
Using string split and toCharArray C commands, each variable is isolated, and casted to a double.
Methods used to get processed values.

Neil Hara


Arduino reads all the data at once until a newline

