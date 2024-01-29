# salto-level-sensor
An ESP Home / Home Assistant based level sensor for the salt bin of our Water Purification system.
<br><br>
About 2 years ago we had a water filtration system installed to reduce the high level of calcium attacking our appliances and bathroom. The system works really well, but is not equipped with any sensors and works without any power source. The only maintenance besides a bi-yearly visit from the company to flush the filters and check the settings is that we need to make sure the system never runs without the regenerative salt. This salt is maintained in a contained, out of which the system melts the bottom tablets and ingests them. No worries; we had set a reminder in our calendars to check the level every 5 weeks. This is usually fine, but there is little room for error here; the salt container is not that big and if you are not able to check immediately or more water is used than expected, it might run empty, which according to the supplier would be bad...
<br><br>
<i>Let me state: I am not a programmer. But scripting stuff through ESP Home and Home Assistant gets me quite far.</i>
<br><br>
My idea was to find a sensor that I could mount to the lid of the container and which would then basically measure the distance to the salt. This info would be enough to translate this into an indication of how full the container is (in %) and the possibility to include this in a dashboard and notifications to my mobile. There are several types of sensors that could be used and I chose for the one that I think will be the least vulnerable to the quite corrosive environment in that salt container; a time-of-flight sensor. This is a sensor that emits light and measure distance based on how long it takes for the light to reflect back. This type of sensor is really small and the actual sensor is protected by a lens, whilst the rest can easily be covered in a nice layer of hot-glue.
<br><br>
<b>Shopping list:</b>
<lu>
<li>Microcontroller: ESP8266 D1-mini</li>
<li>Case: I had one printed for a completely different project by a friend a while back that fit this one perfectly</li>
<li>TOF Sensor: What I <i>should have</i> ordered was the VL53L0X, but what I <i>actually</i> ordered was the VL53L1X.  
<li>Buzzer: The buzzer was part of a stock I have since I once thought I ordered 5 buzzers, but actually ordered 5 times 10 buzzers ;-)</li> 
<li>LED: This is a standard RGB LED</li>
</lu>
<br>
<b>Assembly:</b>
<br>
After creating the configuration in ESP Home and connecting the sensors, LED and buzzer, I used a hot-glue gun to fix everything in place and it has been working fine like that for a few weeks now.
<br><br>
<b>Intepretation of the data:</b>
<br>
The difference between the VL53L1X and VL53L0X is range, which I used when selecting the VL53L1X as my main driver. However, as it turned out, the driver is totally different and the VL53L0X works out-of-the-box with ESP Home (and would have worked in my application too), where the VL53L1X does not. This has caused me, as a non-programmer, quite an issue. I had to look for other projects where someone created a custom component in ESP Home. Eventually I found one and got it to work. The LED reflects the salt level from the sensor itself (controlled via HA), so even when you open the cupboard it is located in, you will immediately see how full it is.
<br><br>
In Home Assistant I am converting the distance between lid and salt to a percentage remaining. There are obviously some fluctuations as the salt is actually moving and the blocks themselves are a few cm in diameter, so alarms should only be triggered after everything has settled. For now I decided to wait until the salt level is below 20% for 2 hours, which seems to do the trick.
<br><br>
If you have any questions, please let me know so I can improve on my documentation and writing skills and add whatever you feel is missing.
