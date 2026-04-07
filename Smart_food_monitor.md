#Food spoilage simulation
I chose this because many people forget to throw the expired foods until they cause unusual smell.I have attached temperature and gas sensors.This is an approximate calculation. 
#code
int tempPin = A0;
int gasPin = A1;

int greenLED = 3;
int yellowLED = 4;
int redLED = 5;

float temperature;
int gasValue;

void setup() {
  Serial.begin(9600);
  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);
}

void loop() {
  int tempReading = analogRead(tempPin);
  float voltage = tempReading * (5.0 / 1023.0);
  temperature = (voltage - 0.5) * 100;
  gasValue = analogRead(gasPin);

  Serial.print("Temp: ");
  Serial.print(temperature);
  Serial.print(" C | Gas: ");
  Serial.println(gasValue);

  if (gasValue < 300 && temperature < 25) {
    digitalWrite(greenLED, HIGH);
    digitalWrite(yellowLED, LOW);
    digitalWrite(redLED, LOW);
    Serial.println("Status: Fresh");
  }
  else if (gasValue < 600 && temperature < 35) {
    digitalWrite(greenLED, LOW);
    digitalWrite(yellowLED, HIGH);
    digitalWrite(redLED, LOW);
    Serial.println("Status: Moderate");
  }
  else {
    digitalWrite(greenLED, LOW);
    digitalWrite(yellowLED, LOW);
    digitalWrite(redLED, HIGH);
    Serial.println("Status: Spoiled");
  }
  delay(1000);
}
#Tinkercad Link
https://www.tinkercad.com/things/6deA4FWv42q/editel?returnTo=%2Fdashboard&sharecode=u-o6L7LBuRHU3k4YGaKVmMtXQeBWp5ELoZ2T5M-nx4A
#Working
1.The temperature sensor reads the temperature value and converting the value in the 0-1023 scale to the actual scale.
2.Similarly, the gas sensor senses the amount of gases released by the food material.
3.On considering these, the freshness can be calculated and the corresponding LED will glow.   
