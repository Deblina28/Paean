## Inspiration
We all saw how everyone started to panic during the onset of the pandemic and it was because of the lack of solid information and the spread of fake news. And this is how people fall under the misconception and get confused about the symptoms of a disease. That is why we wanted to build a project that will allow people to check whether they are COVID positive or not. Also, we didn't want our project to only be limited to a COVID test, but instead, we wanted to make an inexpensive monitoring device that will come in handy even when (or if) the pandemic ends. 


## What it does
Paean is a device built by us that monitors the three essential body parameters of a human being, namely, the heart rate, SPO2 level, and temperature. Along with that it also stores the data collected from the user into the software for future access. The three mentioned parameters that Paean can measure are crucial and potent to reveal several secrets of one's health condition.    


## How we built it
The Project has three main parts, BPM reading, Oxygen saturation level, temperature measurement. Along with that, the data needed to be plotted and stored in computer. For that we designed a simple GUI software in JAVA using Swing.
The signals read by the ADC were very noisy and the data were very jittery. We needed to filter out the high frequency noise. For that we used recursive fileter and moving average algorithm to smooth out the readings. And finally able to get the cream signal, which can be viewed in the monitor(pics attached). It even had the diastolic peaks and the dichrotic notch, making our optical measurement very accurate and upto the mark, with just scratch components.
The main controller of the system is the atmega328p microcontroller. All the sensors are interfaced with it. It basically reads the signals from the sesors via the 10bit ADCand applies the digital filters and the simple algorithms to get the accurate data. Along with that a FTDI chip is used to send the data to the computer, which can be read by the JAVA program, by the serial port. 
To measure the Heart Rate, i.e the beats per minute, for that we placed a Infrared Led(980nm) beside a Photodiode, and made it a compact capsule so that they dont move  while taking readings, and placed a black cover around them, to protect it from ambient light. As soon as we encounter a peak, a timer gets started and measures the transit time until the next peak. This transit time is the time period of the heart beat, by inversing it we get the frequency and by multiplying it with 60 we get the BPM. We took similar 10 readings and averaged it to get better readings.
To measure the SpO2, i.e the oxygen saturation level in the blood, we took a RED led(650nm) and again put a photodiode beside it, the difference from the IR is that is, blood is capable of absorbing light of this wavelength proportional to the oxygen content inside the blood. Now to calculate the SpO2 we obtained the AC rms swing of the signal from the RED led and the AC rms of the signal from the Infrared Led. After that we averaged all the samples one at a time from both the signal to get the DC value from the signal. The SpO2 calculation is then done by the ratio of (((AC rms of Red)/(DC of RED))/((AC rms of IR)/(DC of IR))). To get the AC values we used local min max algorithm to find the crest and the trough values of the signals. With the difference we get the AC value. 
To mesure the Temperaure we used a LM35 sensor and with a simple conversion formula we get the temperature from the voltage read by the ADC. Its simply temperature=(mV/10);
Coming to the software part, we built a simple GUI software in JAVA using the SWING framework. We used simple canvas and few buttons to make the GUI. The readings are transmitted by the microcontroller over the UART communication via the Serial port. The data packets are then parsed by java and plotted to the canvas. The whole software is built with the Eclipse IDE.




## Challenges we ran into
The biggest challenge was being able to calculate the SPO2 level. Other than that some more challenges that we faced were making the IR sensor for it was a bit troublesome. At first, it was not providing as smooth readings as we desired to achieve, and instead, the sensor was causing some random noises that affected the readings. Finding the filter coefficients for accurate readings took a lot of trial and error. The algorithm for auto-calibration was a tough one.

## Accomplishments that we're proud of


## What we learned
We learned about the SPO2 level and how we can achieve that using the red light, in addition to achieving the photoplethysmogram with optical sensors like photodiodes and IR LEDs. We also learned about the digital filters, which we can implement into our future projects, and being the most helpful. We were pretty amazed by knowing that we are surrounded by so many signals, and it contains data. Even when we saw the signal from the sensor read by the ADC, it was such a mess and very noisy reading. After filtering, we were able to get the desired reading.

## What's next for Paean
Next, we will try to build an app that will display all the data recorded from the person using Paean. If in the future we are successful to build the app, then it will also be able to analyze and express if the user has any health condition using algorithms. Along with focusing on the COVID test, this hack will also help people in general to monitor their well-being and learn about the factors that affect their health. We will try to turn this device into a commercial product that can also be used for educational purposes in institutes and hospitals.
