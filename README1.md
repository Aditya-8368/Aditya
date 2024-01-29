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
