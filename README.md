# stage-1------------------------------------------------------------<br>

# problem-1 : Design a schematic of circuit controlling a servo motor using a potentiometer. Also Simulate the circuit on tinkercad

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





# stage-2------------------------------------------------------------<br>

# problem-1 : Controlling LED intensity using PWM registers directly. (without using analogWrite/digitalWrite function)

this is a link for my tinkercad file for stage-2 problem-1 (https://www.tinkercad.com/things/dcMnIvQHpTa-magnificent-amberis)

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

# problem-2 : Sweep a servo without using the Servo library controlled with IR remote. (Press 1 for right sweep ie from 0 to 180 degree and 2 for reverse)

this is a link for my tinkercad file for stage-2 problem-2 (https://www.tinkercad.com/things/60p1n9k2j1E-sizzling-blad)

Arduino code :
# NOTE : This code is not working in tinkercad dut to "IRRemote configuration of buttons" but compilation is going well and it will run on another remote or hardware

#include <IRremote.h>

#define IR_PIN 11 
#define SERVO_PIN 9

IRrecv irrecv(IR_PIN);
decode_results results;

int servoPos = 0;

void setup() {
  pinMode(SERVO_PIN, OUTPUT);
  irrecv.enableIRIn();
}

void loop() {
  if (irrecv.decode(&results)) {
    if (results.value == 0xFF30CF) { 
      sweepServo(0, 180, 1);
    } else if (results.value == 0xFF18E7) { 
      sweepServo(180, 0, -1);
    }
    irrecv.resume();
  }
}

void sweepServo(int from, int to, int step) {
  for (int i = from; i != to; i += step) {
    servoPos = i;
    updateServo();
    delay(15);
  }
}

void updateServo() {
  
  int pulseWidth = map(servoPos, 0, 180, 500, 2500);
  
  digitalWrite(SERVO_PIN, HIGH);
  delayMicroseconds(pulseWidth);
  digitalWrite(SERVO_PIN, LOW);
}





# stage-3------------------------------------------------------------<br>

# problem-1 : Design a PCB on Kicad. The PCB will contain an AtMega328P chip (SMD), IR receiver(for receiving signals from remote), Buck converter (for powering servo and Nano), a connector for servo, and a connector for 12V power supply
