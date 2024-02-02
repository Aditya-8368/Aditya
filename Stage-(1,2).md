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


#define DECODE_NEC

#if !defined(RAW_BUFFER_LENGTH)
#define RAW_BUFFER_LENGTH 100                                                                                              \
// #define RAW_BUFFER_LENGTH  112   
#endif

#define EXCLUDE_UNIVERSAL_PROTOCOLS  
#define EXCLUDE_EXOTIC_PROTOCOLS


# include <IRremote.hpp>

int ir_pin = 11; 
int servopin = 9;
IRrecv recv(ir_pin);
decode_results results;

int Position = 0;

void setup(){ 
  delay(1000);
  recv.enableIRIn();
  
  IrReceiver.begin(ir_pin, ENABLE_LED_FEEDBACK);
  printActiveIRProtocols(&Serial);
  Serial.println(ir_pin);
  
  pinMode(ir_pin, INPUT_PULLUP);
  pinMode(servopin, OUTPUT);
}

void loop(){
 if (IrReceiver.decode()) {
   	if(IrReceiver.decodedIRData.command==0x10) {        
        servoclock(0,180,1);
    }
          
   else if(IrReceiver.decodedIRData.command==0x11){
        servoanticlock(180,0,1);
    }		
 
   else{
        IrReceiver.printIRResultShort(&Serial);
    } 
    IrReceiver.resume();
  }
 }

void servoclock (int from, int to, int step) {
  for (int i = from; i <= to; i += step) {
    Position = i;
    
    int pulseWidth = map(Position, 0, 180, 500, 2500);

      digitalWrite(servopin, HIGH);
      delayMicroseconds(pulseWidth);
      digitalWrite(servopin, LOW);
    delay(20);
  }
}
void servoanticlock(int from, int to, int step) {
  for (int i = from; i >= to; i -= step) {
    Position = i;
    int pulseWidth = map(Position, 0, 180, 500, 2500);
   
      digitalWrite(servopin, HIGH);
      delayMicroseconds(pulseWidth);
      digitalWrite(servopin, LOW);
    delay(20);
  }
}