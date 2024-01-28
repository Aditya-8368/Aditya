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