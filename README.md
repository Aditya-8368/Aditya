# stage-1<br>
PCB DESIGN PROJECT(ZINE)

link to tinker cad for my project of stage-1 (https://www.tinkercad.com/things/lVUwzbY1CdB-stage-1)

code of Arduino:

#include <Servo.h>

int val = 0;

int servo = 0;

int outval = 0;

Servo servo_9;

void setup()
{
  pinMode(A1, INPUT);
  servo_9.attach(9, 500, 2500);
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop()
{
  val = analogRead(A1);
  outval = map(val, 0, 1023, 0, 180);
  servo_9.write(outval);

  digitalWrite(LED_BUILTIN, HIGH);
  delay(10); // Delay a little bit to improve simulation performance
}





#stage-2<br>

#problem-1

this is a link for my tinkercad file for stage-2 (https://www.tinkercad.com/things/dcMnIvQHpTa-magnificent-amberis)

Arduino code :

// C++ code

const int ledPin = 9;

void setup() {
  
  pinMode(ledPin, OUTPUT);

  
  TCCR1A |= (1 << WGM11) | (1 << COM1A1);
  TCCR1B |= (1 << WGM12) | (1 << WGM13) | (1 << CS10);

  OCR1A = 255;

  OCR1B = 0;
}

void loop() {
  
  for (int brightness = 0; brightness <= 255; brightness++) {
    OCR1B = brightness;
    delay(10);
  }

  for (int brightness = 255; brightness >= 0; brightness--) {
    OCR1B = brightness;
    delay(10);
  }
}
