#include <Arduino.h>
#include <TM1637Display.h>

const int CLK = 8; // set CLK pin
const int DIO = 9; // set DIO pin
const byte numDigits = 4; // number of digits
TM1637Display display(CLK, DIO, numDigits);

unsigned long previousTime = 0;
unsigned long currentTime = 0;
int fruits = 0;
int points = 0;

void setup() {
 Serial.begin(9600);
 display.setBrightness(0x0f); // set the diplay brightness
 display.showNumberDec(points); // display initial points
}

void loop() {
 currentTime = millis();
 if (currentTime - previousTime >= 1000) {
    previousTime = currentTime;
    fruits = random(0, 10); // generate random fruits count
    points += fruits; // calculate points
    display.showNumberDec(points); // display updated points
    Serial.print("Points: ");
    Serial.println(points);
 }
}
