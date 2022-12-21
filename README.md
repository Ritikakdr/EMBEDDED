# EMBEDDED

## blink an LED
![image](https://user-images.githubusercontent.com/116477443/208901150-f824dd24-1731-40e7-9b0a-459ee5dfb4fd.png)
## control a LED with a button
![image](https://user-images.githubusercontent.com/116477443/208914670-cd550f2b-280a-4d4a-94c9-e8523fdf9744.png)
! #define LED_PIN 8
#define BUTTON_PIN 7

byte lastButtonState = LOW;
byte ledState = LOW;

unsigned long debounceDuration = 50; // millis
unsigned long lastTimeButtonStateChanged = 0;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}

void loop() {
  if (millis() - lastTimeButtonStateChanged > debounceDuration) {
    byte buttonState = digitalRead(BUTTON_PIN);
    if (buttonState != lastButtonState) {
      lastTimeButtonStateChanged = millis();
      lastButtonState = buttonState;
      if (buttonState == LOW) {
        ledState = (ledState == HIGH) ? LOW: HIGH;
        digitalWrite(LED_PIN, ledState);
      }
    }
  }
}

