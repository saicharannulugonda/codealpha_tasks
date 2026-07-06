#include <Servo.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

#define TRIG_PIN 7
#define ECHO_PIN 6
#define SERVO_PIN 9

Servo radarServo;

const int centerX = 64;
const int centerY = 63;     // baseline sits at the bottom row
const int maxRadius = 60;
const int maxDistanceCM = 40; // furthest distance we plot on the radar

int angle = 15;
int direction = 1;

long readDistanceCM() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duration = pulseIn(ECHO_PIN, HIGH, 30000); // 30ms timeout
  if (duration == 0) return maxDistanceCM + 10;   // nothing in range

  long distance = duration * 0.0343 / 2; // cm
  return distance;
}

void drawRadarBackground() {
  display.clearDisplay();

  // range rings (half circles)
  for (int r = 20; r <= maxRadius; r += 20) {
    for (int a = 0; a <= 180; a += 3) {
      float rad = a * PI / 180.0;
      int x = centerX - r * cos(rad);
      int y = centerY - r * sin(rad);
      if (x >= 0 && x < SCREEN_WIDTH && y >= 0 && y < SCREEN_HEIGHT) {
        display.drawPixel(x, y, SSD1306_WHITE);
      }
    }
  }

  // baseline
  display.drawLine(0, centerY, SCREEN_WIDTH - 1, centerY, SSD1306_WHITE);
}

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  radarServo.attach(SERVO_PIN);

  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);
  display.clearDisplay();
  display.display();
}

void loop() {
  radarServo.write(angle);
  delay(30); // give the servo time to move before pinging

  long distance = readDistanceCM();

  drawRadarBackground();

  // sweep line at current angle
  float rad = angle * PI / 180.0;
  int lineX = centerX - maxRadius * cos(rad);
  int lineY = centerY - maxRadius * sin(rad);
  display.drawLine(centerX, centerY, lineX, lineY, SSD1306_WHITE);

  // plot detected object as a dot along the sweep line
  if (distance > 0 && distance <= maxDistanceCM) {
    int objR = map(distance, 0, maxDistanceCM, 0, maxRadius);
    int objX = centerX - objR * cos(rad);
    int objY = centerY - objR * sin(rad);
    display.fillCircle(objX, objY, 2, SSD1306_WHITE);
  }

  // text readout
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(0, 0);
  display.print("A:");
  display.print(angle);
  display.print(" D:");
  if (distance <= maxDistanceCM) {
    display.print(distance);
    display.print("cm");
  } else {
    display.print("--");
  }

  display.display();

  // advance sweep
  angle += direction * 2;
  if (angle >= 165) { angle = 165; direction = -1; }
  if (angle <= 15)  { angle = 15;  direction = 1; }
}
