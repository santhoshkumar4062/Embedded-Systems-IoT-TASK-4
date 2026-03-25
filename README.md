# # 🌐 Smart Temperature IoT Monitoring System (Task-4)

## 📌 Overview

This project upgrades a basic automation system into a cloud-connected IoT device using ESP32 and ThingSpeak.
It sends real-time temperature data to the cloud and displays it on a live dashboard.

---

## 🎯 Objective

* Learn IoT cloud integration
* Send real-time data to cloud
* Create live dashboards
* Understand device-to-cloud communication

---

## 🧰 Components

* ESP32
* LM35 Temperature Sensor
* Breadboard & Wires

---

## 🔌 Circuit Diagram

### Connections:

* LM35 VCC → 3.3V
* LM35 GND → GND
* LM35 OUT → GPIO34

<img width="1536" height="1024" alt="ESP32 IoT temperature monitor setup" src="https://github.com/user-attachments/assets/e8aaf943-8424-4545-b276-f17405c0dc9d" />

<img width="1536" height="1024" alt="E-commerce dashboard overview and metrics" src="https://github.com/user-attachments/assets/5f3538dd-7989-42e1-8718-d0cc047ca103" />


---

## 🌐 Cloud Platform

* ThingSpeak
* Field1 → Temperature Data

---

## 💻 Code

```cpp id="r7zkpn"
#include <WiFi.h>

const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_PASSWORD";
String apiKey = "YOUR_API_KEY";

const char* server = "api.thingspeak.com";
int sensorPin = 34;

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
}

void loop() {

  int sensorValue = analogRead(sensorPin);
  float voltage = sensorValue * (3.3 / 4095.0);
  float temperature = voltage * 100;

  WiFiClient client;

  if (client.connect(server, 80)) {
    String url = "/update?api_key=" + apiKey + "&field1=" + String(temperature);

    client.print(String("GET ") + url + " HTTP/1.1\r\n" +
                 "Host: " + server + "\r\n" +
                 "Connection: close\r\n\r\n");
  }

  client.stop();
  delay(15000);
}
```

---

## ⚙️ Working

1. ESP32 reads temperature
2. Connects to WiFi
3. Sends data to ThingSpeak
4. Dashboard updates in real-time

---

## 📊 Output

* Live temperature values
* Graph visualization
* Cloud-based monitoring

---

## 🚀 Future Improvements

* Add mobile alerts (Blynk)
* Use relay for real AC control
* Multi-sensor dashboard
* AI-based prediction

---

## 🏁 Conclusion

This project demonstrates real-world IoT architecture where embedded systems communicate with cloud platforms for remote monitoring and automation.


