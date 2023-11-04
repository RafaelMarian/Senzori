# Senzori Project

## Student Information
- **Student:** Vanca Rafael Marian
- **Group:** 2142/3

## Project Theme
The chosen theme for this project revolves around the presentation and utilization of the TEMT6000 ambient light sensor. This sensor was selected based on its affordability and versatility. The TEMT6000 sensor finds applications in various projects, such as lighting effects in games or as ambient lighting in modern vehicles.

## TEMT6000 Sensor

The TEMT6000 is an ambient light sensor compatible with Arduino. Functioning similarly to a transistor, its analog signal voltage increases with higher luminosity. The sensor comprises a TEMT6000 NPN phototransistor, small in size yet high in performance, designed to adapt to human eyes.

- **Technical Specifications:**
  - Collector-Emitter Voltage: Vceo 6V
  - Emitter-Collector Voltage: Veco 1.5V
  - Maximum Collector Current: Ic 20mA
  - Operating Voltage: 3.3-5V
  - Maximum Sensitivity: 570nm
  - Sensitivity Angle: +/- 60 degrees
  - Dimensions: 14 x 8 mm

Datasheet: [TEMT6000 Datasheet](file:///C:/Users/chita/Downloads/SEN-11-052_Datasheet.pdf)

## Circuit Configuration

For wiring, the power pin was connected to 5V, the ground pin to the ground, and the encoding pin to A0. The board was powered through a USB cable from the laptop. Initially, the code was tested using the Arduino IDE to verify the sensor's functionality. Subsequently, the code was transferred to Microchip Studio to experiment with C programming language.

## Arduino Code

```C
// Arduino code snippet
#define LIGHT_SENSOR A0 // define input pin

void setup() {
  Serial.begin(9600);
}

void loop() {
  int Lvalue = analogRead(LIGHT_SENSOR); // read the light
  int mVolt = map(Lvalue, 0, 1023, 0, 5000); // map analogue reading to 5000mV
  int percent = map(Lvalue, 0, 1023, 0, 100); // map analogue reading to 100%
  float volt = (double)mVolt / 1000; // convert millivolt to volt

  Serial.print(mVolt); // print millivolt
  Serial.print("mV ...... ");
  Serial.print(volt, 3); // print volts with 3 decimal places
  Serial.print("V ...... ");
  Serial.print(percent); // print percentage
  Serial.println("%");
  delay(1000); // wait for 1000 milliseconds
}
// C code snippet
#include <stdio.h>
#include <avr/io.h>
#include <util/delay.h>

#define light 0 // define input pin as 0

void setup() {
  // TEMT6000 sensor code
  // Initialize serial communication at 9600 baud
  UBRR0H = 0;
  UBRR0L = 103;
  UCSR0B = (1 << TXEN0) | (1 << RXEN0);
  UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);
}

void loop() {
  // TEMT6000 sensor code
  ADMUX = light; // select the input pin
  ADCSRA = (1 << ADEN) | (1 << ADPS2) | (1 << ADPS1) | (1 << ADPS0) | (1 << ADSC);
  while (ADCSRA & (1 << ADSC)); // wait for conversion to finish

  // ... [The complete C code snippet needs to be included here] ...

  _delay_ms(1000); // wait for 1000 milliseconds
  // TEMT6000 sensor code
}
Experimental Results

Experimental light values obtained:

    Light values in the room:
    Light values when switched off:
    Light values in strong light:

References

    Optimus Digital - TEMT6000 Ambient Light Sensor
