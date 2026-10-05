The system can automatically monitor soil and environmental conditions, predict the crop/irrigation requirement, control a water pump through an ESP32, log data to Google Sheets/ThingSpeak, and use an AI Agent through n8n to generate intelligent alerts and recommendations. LearnEngineering

I can provide the full project in the following structure:

1. Project Architecture



                  ┌─────────────────────────┐
                  │       FARM / FIELD      │
                  │                         │
                  │ Soil Moisture Sensor    │
                  │ Temperature Sensor      │
                  │ Humidity Sensor         │
                  │ Rain Sensor             │
                  │ Water Level Sensor      │
                  └───────────┬─────────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │      ESP32       │
                    │                  │
                    │ Sensor Reading   │
                    │ Decision Logic   │
                    │ Wi-Fi            │
                    └────────┬─────────┘
                             │
                 ┌───────────┼───────────────┐
                 │           │               │
                 ▼           ▼               ▼
          ┌──────────┐ ┌───────────┐ ┌─────────────┐
          │ Water    │ │ ThingSpeak│ │    n8n      │
          │ Pump     │ │ Dashboard │ │ Automation  │
          └──────────┘ └───────────┘ └──────┬──────┘
                                            │
                             ┌──────────────┼──────────────┐
                             ▼              ▼              ▼
                       ┌──────────┐  ┌───────────┐  ┌──────────┐
                       │ AI Agent │  │  Google   │  │ Telegram │
                       │          │  │  Sheets   │  │ Alerts   │
                       └────┬─────┘  └───────────┘  └────┬─────┘
                            │                            │
                            ▼                            ▼
                     Crop/Irrigation              Text / Voice
                       Analysis                     Notification
3. Main Objective
Discover more
Upgrade Your OS
Learn Engineering
Build Custom PCs
The objective is to develop an intelligent automated irrigation system that determines when irrigation is required by combining: LearnEngineering

Soil moisture

Temperature

Relative humidity

Rain detection

Water-tank level

Crop information

Crop growth stage

AI-based prediction

Historical irrigation data

Instead of continuously running the pump, the ESP32 and automation system determine whether irrigation is actually required.


Basic principle
Sensor Data
     ↓
ESP32
     ↓
Internet
     ↓
n8n Workflow
     ↓
AI Agent
     ↓
Analyze Crop + Environment
     ↓
Irrigation Decision
     ↓
ESP32
     ↓
Pump ON/OFF
     ↓
Cloud Logging
     ↓
Telegram Alert
3. Proposed Features
Discover more
Try Office Apps
Find Navigators
Try Dev Tools
Hardware
ESP32 development board CompareCPUs

Capacitive soil-moisture sensor

DHT22/DHT11 temperature-humidity sensor

Rain sensor

Water-level sensor

Relay module

DC water pump

External pump power supply

Optional flow sensor

Optional LCD/OLED

Wi-Fi connection

Software
Arduino IDE

ESP32 Arduino framework

n8n

Telegram Bot

Google Sheets

ThingSpeak

AI/LLM API

Optional web dashboard

4. Overall System Flow
Discover more
Store Big Data
Browse Reference
Source Parts



                    START
                      │
                      ▼
              ESP32 initializes
                      │
                      ▼
                Connect Wi-Fi
                      │
                      ▼
             Read all sensors
                      │
                      ▼
       ┌───────────────────────────┐
       │ Soil moisture sufficiently │
       │ high?                      │
       └─────────────┬─────────────┘
                     │
               YES   │   NO
                │    │
                ▼    ▼
             Pump   Check
             OFF    weather/
                    rain/tank
                     │
                     ▼
              Send data to n8n
                     │
                     ▼
                AI Agent
                     │
          ┌──────────┴──────────┐
          │                     │
      Irrigation              No
       required             irrigation
          │                     │
          ▼                     ▼
       Pump ON                Pump OFF
          │                     │
          └──────────┬──────────┘
                     ▼
               Record data
                     │
              ┌──────┴──────┐
              ▼             ▼
        Google Sheets   ThingSpeak
              │
              ▼
          Telegram
              │
              ▼
       Voice/Text Alert
              │
              ▼
           Repeat
6. Hardware Block Diagram
Discover more
Compare CPUs
Learn Sociology
Data


                     ┌───────────────┐
                     │     ESP32     │
                     │               │
                     │ GPIO / ADC    │
                     │ Wi-Fi         │
                     └───────┬───────┘
                             │
       ┌─────────────────────┼──────────────────────┐
       │                     │                      │
       ▼                     ▼                      ▼
┌────────────┐       ┌──────────────┐       ┌─────────────┐
│ Soil       │       │ DHT11/DHT22  │       │ Rain Sensor │
│ Moisture   │       │ Temp/Humidity │       │             │
└────────────┘       └──────────────┘       └─────────────┘
       │
       │
       ▼
┌───────────────┐
│ Water Level   │
│ Sensor        │
└───────────────┘

                     ESP32
                       │
                       ▼
                 ┌──────────┐
                 │  Relay   │
                 └────┬─────┘
                      │
                      ▼
                 ┌──────────┐
                 │   Pump   │
                 └────┬─────┘
                      │
                      ▼
                    FIELD
8. Example Electrical Schematic
Discover more
data
DATA
software
A typical low-voltage prototype can be wired approximately as follows:



                 ESP32
          ┌──────────────────┐
          │                  │
          │ 3.3V ─────────────── Sensor VCC
          │ GND  ─────────────── Sensor GND
          │                  │
          │ GPIO34 ◄──────────── Soil Moisture AO
          │ GPIO4  ◄──────────── DHT DATA
          │ GPIO35 ◄──────────── Rain Sensor
          │ GPIO32 ◄──────────── Water Level
          │                  │
          │ GPIO26 ───────────── Relay IN
          │                  │
          └──────────────────┘
                       │
                       ▼
                  ┌─────────┐
                  │ RELAY   │
                  │ MODULE  │
                  └────┬────┘
                       │
                       ▼
              ┌────────────────┐
              │ External       │
              │ Pump Supply    │
              └───────┬────────┘
                      │
                      ▼
                   DC PUMP
Discover more
Software
Try Cloud Tools
SOFTWARE
Important: The pump should normally have its own correctly rated power supply. Do not power a pump directly from an ESP32 GPIO pin. For mains-powered pumps, use an appropriately rated isolated switching arrangement and have the mains portion installed/tested by a qualified person. CompareCPUs

7. Suggested GPIO Assignment
Component	ESP32 Pin
Soil moisture analog output	GPIO 34
DHT22 data	GPIO 4
Rain sensor	GPIO 35
Water-level sensor	GPIO 32
Relay	GPIO 26
Optional flow sensor	GPIO 27
OLED SDA	GPIO 21
OLED SCL	GPIO 22
GPIO assignments can be changed depending on the ESP32 board and sensor modules used.

8. How the AI Component Works

The AI should not blindly control the pump.

Instead, the ESP32 collects measurements and sends a structured data packet.

Example:

{
  "soil_moisture": 31,
  "temperature": 34.2,
  "humidity": 48,
  "rain_detected": false,
  "water_level": 72,
  "crop": "Tomato",
  "growth_stage": "Flowering"
}
n8n receives this information. TryDev Tools

The AI Agent analyzes the data:

Discover more
Earn a CS Degree
Upgrade Your OS
Learn Engineering
Soil moisture = 31%
Temperature = 34.2°C
Humidity = 48%
Rain = No
Tank = 72%
Crop = Tomato
Stage = Flowering
It could return a structured decision such as:

{
  "irrigation_required": true,
  "duration_minutes": 8,
  "priority": "high",
  "reason": "Low soil moisture and high temperature",
  "alert_required": true
}
The n8n workflow can then validate this response before sending a pump command.

9. Crop Prediction Module
The crop-prediction component can operate at two levels.

Level 1 — Crop selection
The user supplies or selects:

Crop:
Tomato
or the AI predicts a likely crop from available agricultural/environmental information. BrowseReference

Level 2 — Crop-specific irrigation prediction
Different crops have different water requirements.

For example:

Crop
  ↓
Growth Stage
  ↓
Soil Moisture
  ↓
Temperature
  ↓
Humidity
  ↓
Rain Forecast/Detection
  ↓
Historical Irrigation
  ↓
AI Prediction
  ↓
Recommended Irrigation
For an academic project, I recommend making crop type + growth stage explicit inputs rather than claiming that an LLM itself is a scientifically validated crop classifier.

10. n8n Automation Architecture
The n8n workflow can be designed as:



                    ESP32 HTTP Request
                           │
                           ▼
                    ┌─────────────┐
                    │ Webhook     │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Validate    │
                    │ Sensor Data │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Google      │
                    │ Sheets Log  │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ AI Agent    │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Parse AI    │
                    │ Decision    │
                    └──────┬──────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │ Safety Validation│
                  └────────┬─────────┘
                           │
                  ┌────────┴────────┐
                  │                 │
                YES                 NO
                  │                 │
                  ▼                 ▼
             ESP32 Pump          Pump OFF
               Command               │
                  │                  │
                  └────────┬─────────┘
                           ▼
                    ┌─────────────┐
                    │ ThingSpeak  │
                    │ Update      │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Telegram    │
                    │ Notification│
                    └─────────────┘
12. n8n Nodes
A practical workflow can contain:

Webhook

Set/Edit Fields

IF – Validate Sensor Values

Google Sheets – Append Row

AI Agent

Structured Output Parser

IF – Irrigation Required

HTTP Request – ESP32 CompareCPUs

ThingSpeak HTTP Request

Telegram

Google Sheets – Update Result

Error/Alert branch

12. AI Agent Prompt
The AI Agent should receive structured sensor data rather than an unstructured paragraph.

Example system instruction:

You are an agricultural irrigation decision assistant.

Analyze the supplied crop, growth stage, soil moisture,
temperature, humidity, rainfall status, water level and
historical irrigation information.

Your job is to recommend whether irrigation is required.

Never recommend irrigation when:
1. The water tank is critically low.
2. Rain is currently detected.
3. Sensor values are invalid.
4. The system reports a hardware fault.

Return ONLY valid JSON using this schema:

{
  "irrigation_required": true,
  "duration_minutes": 5,
  "priority": "low",
  "reason": "string",
  "alert_required": true
}

Do not invent sensor values.
Do not directly claim that irrigation is scientifically optimal.
Treat your answer as a recommendation subject to safety validation.
This is an important architectural improvement: the AI makes a recommendation, while deterministic safety logic has the final authority over the pump.

13. ESP32 → n8n Data
The ESP32 can send an HTTP POST request: CompareCPUs

POST /webhook/irrigation
Content-Type: application/json
with:

{
  "device_id": "ESP32_FIELD_01",
  "soil_moisture": 28,
  "temperature": 33.5,
  "humidity": 51,
  "rain": false,
  "water_level": 78,
  "crop": "Tomato",
  "growth_stage": "Flowering"
}
14. ESP32 Arduino Code
Below is a starter implementation for the ESP32.

#include <WiFi.h>
#include <HTTPClient.h>
#include <DHT.h>

#define DHTPIN 4
#define DHTTYPE DHT22

#define SOIL_PIN 34
#define RAIN_PIN 35
#define WATER_LEVEL_PIN 32

#define RELAY_PIN 26

const char* WIFI_SSID = "YOUR_WIFI";
const char* WIFI_PASSWORD = "YOUR_PASSWORD";

const char* N8N_URL =
  "https://YOUR-N8N-DOMAIN/webhook/irrigation";

DHT dht(DHTPIN, DHTTYPE);

void setup() {

  Serial.begin(115200);

  pinMode(RELAY_PIN, OUTPUT);

  // Pump OFF initially
  digitalWrite(RELAY_PIN, LOW);

  dht.begin();

  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);

  Serial.print("Connecting to WiFi");

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println();
  Serial.println("WiFi connected");
}

void loop() {

  int soilRaw = analogRead(SOIL_PIN);
  int rainRaw = analogRead(RAIN_PIN);
  int waterRaw = analogRead(WATER_LEVEL_PIN);

  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();

  if (isnan(temperature) || isnan(humidity)) {
    Serial.println("DHT sensor error");
    delay(5000);
    return;
  }

  // These values must be calibrated for the actual sensors.
  int soilMoisture =
      map(soilRaw, 4095, 1500, 0, 100);

  soilMoisture = constrain(soilMoisture, 0, 100);

  int waterLevel =
      map(waterRaw, 1000, 3000, 0, 100);

  waterLevel = constrain(waterLevel, 0, 100);

  bool rainDetected = rainRaw < 1500;

  Serial.println("------ SENSOR DATA ------");

  Serial.print("Soil: ");
  Serial.println(soilMoisture);

  Serial.print("Temperature: ");
  Serial.println(temperature);

  Serial.print("Humidity: ");
  Serial.println(humidity);

  Serial.print("Rain: ");
  Serial.println(rainDetected);

  Serial.print("Water Level: ");
  Serial.println(waterLevel);

  if (WiFi.status() == WL_CONNECTED) {

    HTTPClient http;

    http.begin(N8N_URL);

    http.addHeader(
      "Content-Type",
      "application/json"
    );

    String json = "{";

    json += "\"device_id\":\"ESP32_FIELD_01\",";
    json += "\"soil_moisture\":" +
            String(soilMoisture) + ",";
    json += "\"temperature\":" +
            String(temperature) + ",";
    json += "\"humidity\":" +
            String(humidity) + ",";
    json += "\"rain\":" +
            String(rainDetected ? "true" : "false") + ",";
    json += "\"water_level\":" +
            String(waterLevel) + ",";
    json += "\"crop\":\"Tomato\",";
    json += "\"growth_stage\":\"Flowering\"";

    json += "}";

    Serial.println(json);

    int responseCode =
      http.POST(json);

    Serial.print("HTTP Response: ");
    Serial.println(responseCode);

    String response =
      http.getString();

    Serial.println(response);

    http.end();
  }

  delay(60000);
}
15. Important Sensor Calibration
Do not assume the map() values above represent your actual sensors.

For the soil sensor, record:

Completely dry soil → ADC value
Wet soil             → ADC value
For example:

Dry = 3500
Wet = 1500
Then calibrate:

int moisture = map(
    soilRaw,
    3500,
    1500,
    0,
    100
);
The exact values depend on the sensor, soil and ESP32 ADC configuration. CompareCPUs

16. Pump-Control Safety
A better architecture is:



                 AI Recommendation
                        │
                        ▼
               ┌─────────────────┐
               │ Safety Rules    │
               └────────┬────────┘
                        │
       ┌────────────────┼────────────────┐
       │                │                │
       ▼                ▼                ▼
 Tank OK?          Rain absent?     Sensor valid?
       │                │                │
       └────────────────┼────────────────┘
                        ▼
                 ALL CONDITIONS OK
                        │
                        ▼
                    Pump ON
Never allow an LLM response such as:

{"irrigation_required":true}
to directly energize the pump without validation.

17. Telegram Alert System
When irrigation starts:

🌱 IRRIGATION ALERT

Crop: Tomato
Growth Stage: Flowering

Soil Moisture: 28%
Temperature: 33.5°C
Humidity: 51%

Rain: No
Water Level: 78%

AI Recommendation:
Irrigation Required

Pump:
ON

Duration:
5 minutes
When irrigation finishes:

✅ IRRIGATION COMPLETED

Crop: Tomato

Pump Runtime: 5 minutes

System Status:
NORMAL

Data has been recorded in
Google Sheets and ThingSpeak.
18. Telegram Voice Alert
For a voice notification, the conceptual n8n flow is: TryDev Tools

AI Decision
    ↓
Generate Alert Text
    ↓
Text-to-Speech Service
    ↓
Audio File
    ↓
Telegram Bot
    ↓
Send Voice/Audio Message
Example spoken message:

"Irrigation alert. Soil moisture is low for the tomato crop. The system recommends five minutes of irrigation."

This makes the project particularly useful for a farmer who may not continuously monitor a dashboard.

19. Google Sheets Database
Create columns such as:

Timestamp	Device	Crop	Stage	Soil	Temp	Humidity	Rain	Water	AI Decision	Pump	Duration
2026-10-04 10:00	ESP32-01	Tomato	Flowering	28	33.5	51	No	78	Irrigate	ON	5
2026-10-04 11:00	ESP32-01	Tomato	Flowering	46	32.1	55	No	73	No irrigation	OFF	0
This gives you a historical dataset for later analysis and model development.

20. ThingSpeak Dashboard
ThingSpeak can be used for numerical visualization.

Possible channels:

Field 1 → Soil Moisture
Field 2 → Temperature
Field 3 → Humidity
Field 4 → Water Level
Field 5 → Rain Status
Field 6 → Pump Status
Field 7 → Irrigation Duration

Dashboard:



┌──────────────────────────────────────────┐
│       SMART IRRIGATION DASHBOARD         │
├──────────────────────────────────────────┤
│ Soil Moisture       ███████░░░  28%       │
│ Temperature                     33.5°C    │
│ Humidity                        51%       │
│ Water Tank                     78%        │
│ Rain                            NO        │
│ Pump                            ON        │
├──────────────────────────────────────────┤
│ Crop: Tomato                              │
│ Stage: Flowering                          │
│ AI: Irrigation Recommended                │
└──────────────────────────────────────────┘


21. Webpage / IoT Dashboard
You can also create a custom webpage:



              SMART FARM AI
        ─────────────────────────

        🌱 Crop: TOMATO
        🌿 Stage: FLOWERING

        Soil Moisture
        ███████░░░░ 28%

        Temperature
        33.5 °C

        Humidity
        51 %

        Tank Level
        78 %

        Rain
        ❌ NO

        Pump
        🟢 ON

        AI Recommendation
        ─────────────────
        Irrigation required

        Duration: 5 minutes

        ┌────────────────────────┐
        │ VIEW HISTORICAL DATA   │
        └────────────────────────┘
    
23. Complete Communication Architecture



                         INTERNET
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
          ThingSpeak       n8n          Web UI
                            │
                 ┌──────────┼───────────┐
                 │          │           │
                 ▼          ▼           ▼
             AI Agent   Google Sheets Telegram
                 │                      │
                 │                      ▼
                 │                 Voice Alert
                 │
                 ▼
             Decision
                 │
                 ▼
              ESP32
                 │
                 ▼
               Relay
                 │
                 ▼
               Pump
25. Agentic IoT Concept
The project becomes more than simple IoT when the AI Agent can: LearnSociology

OBSERVE
   ↓
Sensor data
   ↓
ANALYZE
   ↓
AI Agent
   ↓
REASON
   ↓
Determine irrigation recommendation
   ↓
ACT
   ↓
ESP32 / Pump
   ↓
OBSERVE AGAIN
   ↓
Verify result
   ↓
LOG
   ↓
Notify farmer
This creates an observe → reason → act → verify loop.

24. Example Agent Conversation
Farmer
Farmer:
How is the field?
AI Agent
AI:
The tomato field currently has 28% soil moisture.
The temperature is 33.5°C and no rain is detected.

The water tank is 78% full.

I recommend irrigation for approximately
5 minutes, subject to the system safety checks.
Farmer
Farmer:
Start irrigation.
Agent
AI:
The request was received.

Safety conditions:
✓ Tank level sufficient
✓ No rain detected
✓ Sensors responding

Irrigation can be started.
System
ESP32
   ↓
Relay ON
   ↓
Pump ON
Agent
AI:
Irrigation completed.

Pump runtime: 5 minutes.

The event has been recorded.
25. Manual Telegram Control
You can optionally implement commands:

/start
/status
/soil
/pump_on
/pump_off
/irrigation
/history
/ai
Example:

Farmer → /status

Bot →
🌱 Field Status

Soil: 31%
Temperature: 32.8°C
Humidity: 54%
Tank: 76%
Rain: No
Pump: OFF

AI:
Irrigation may be required soon.
For safety, manual /pump_on should still pass through maximum-runtime and sensor/tank checks.

26. n8n Workflow Logic
Pseudo-code:


RECEIVE SENSOR DATA


IF soil moisture < crop threshold
    AND rain = false
    AND water level > minimum
    AND sensor values valid

        SEND DATA TO AI

        AI → irrigation_required?

        IF YES
            duration = AI duration

            LIMIT duration to safe maximum

            SEND COMMAND TO ESP32

            LOG EVENT

            SEND TELEGRAM ALERT

        ELSE
            LOG "No irrigation"

ELSE
    Pump OFF
    LOG reason

    
27. Fault Detection
The system should also identify: LearnEngineering

Sensor failure
Wi-Fi failure
Low tank level
Unexpected pump state
Invalid AI response
Unexpected soil readings
Rain detected
ESP32 offline
Example:

🚨 SYSTEM FAULT

Soil moisture sensor returned
an invalid reading.

Pump operation has been disabled.

Please inspect the sensor.
28. Recommended Database/Data Model
A complete record can contain:

{
  "timestamp": "...",
  "device_id": "ESP32_FIELD_01",
  "crop": "Tomato",
  "growth_stage": "Flowering",
  "soil_moisture": 28,
  "temperature": 33.5,
  "humidity": 51,
  "rain": false,
  "water_level": 78,
  "ai_recommendation": "irrigate",
  "irrigation_duration": 5,
  "pump_status": "ON",
  "system_status": "NORMAL"
}


29. Project Development Phases
Phase 1 — Hardware
ESP32
 ↓
Soil Sensor
 ↓
DHT Sensor
 ↓
Rain Sensor
 ↓
Relay
 ↓
Pump
First prove that local sensing and pump control work.

Phase 2 — Internet
ESP32
 ↓
Wi-Fi
 ↓
HTTP
 ↓
n8n
Phase 3 — Cloud
ESP32
 ↓
n8n
 ├── Google Sheets
 └── ThingSpeak
Phase 4 — AI
n8n
 ↓
AI Agent
 ↓
Structured decision
Phase 5 — Telegram
n8n
 ↓
Telegram
 ├── Text
 └── Voice
Phase 6 — Automation
Sensor
 ↓
AI
 ↓
Safety
 ↓
Pump
 ↓
Verification
 ↓
Notification
30. Testing Plan
Test	Input	Expected Result
Dry soil	Low moisture	Irrigation recommendation
Wet soil	High moisture	Pump remains OFF
Rain	Rain detected	Pump OFF
Low tank	Tank below limit	Pump OFF + alert
Normal temperature	Normal conditions	Normal operation
Sensor failure	Invalid reading	Pump disabled
Wi-Fi failure	Network unavailable	Local safe state
Telegram	Alert event	Notification delivered
Google Sheets	Sensor event	Row created
ThingSpeak	Sensor event	Fields updated
AI failure	Invalid AI output	Safe fallback
Manual OFF	Telegram command	Pump stops
31. Expected Results
The completed system should: LearnEngineering

Monitor field conditions continuously.

Measure soil moisture automatically.

Monitor temperature and humidity.

Detect rain.

Monitor available water.

Identify the selected crop and growth stage.

Generate an AI-assisted irrigation recommendation.

Apply deterministic safety rules.

Control the pump automatically.

Store historical data.

Display cloud graphs.

Send Telegram notifications.

Generate optional voice alerts.

Allow remote monitoring.

Provide a foundation for future predictive irrigation models.

32. Advantages
Traditional irrigation
Farmer
  ↓
Manual observation
  ↓
Manual pump
  ↓
Water consumption
Proposed system
Sensors
  ↓
ESP32
  ↓
Cloud
  ↓
AI Agent
  ↓
Safety validation
  ↓
Automatic irrigation
  ↓
Cloud logging
  ↓
Telegram alert
Advantages include:

Reduced unnecessary irrigation

Remote monitoring

Automated operation

Historical data collection BrowseReference

Crop-aware recommendations

Early fault notification

Voice-based alerts

Expandability to multiple fields

33. Limitations
For an academically honest project report, include these:

AI recommendations depend on the quality of sensor data.

Soil-moisture sensors require calibration.

A generic AI model is not automatically an agronomically validated irrigation model.

Internet connectivity may fail.

Crop-water requirements vary by soil, climate and growth stage.

The prototype should be validated against real agricultural measurements before being used for production irrigation.

Pump control requires appropriate electrical and mechanical safety measures.

34. Future Enhancements
The project can later be upgraded with:

Weather API
     ↓
Rain Forecast
     ↓
AI Agent
and:

Historical Data
      ↓
Machine Learning Model
      ↓
Crop Water Requirement
      ↓
Prediction
Other upgrades:

Multiple ESP32 field nodes CompareCPUs

Solar power

LoRa/LoRaWAN

Flow-rate monitoring

Fertilizer automation

Disease detection using camera

Leaf-image analysis

Weather prediction

Digital twin

Mobile application

Multi-crop support

Reinforcement-learning irrigation optimization

35. Final System Diagram



                         ┌──────────────────┐
                         │       FARM       │
                         │                  │
                         │ Soil Sensor      │
                         │ Temp/Humidity    │
                         │ Rain Sensor      │
                         │ Water Level      │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │      ESP32       │
                         │                  │
                         │ Sensor Processing│
                         │ Wi-Fi            │
                         │ Pump Interface   │
                         └───────┬──────────┘
                                 │
                         Internet / HTTP
                                 │
                                 ▼
                         ┌──────────────────┐
                         │       n8n        │
                         │ Automation       │
                         └────────┬─────────┘
                                  │
                     ┌────────────┼────────────┐
                     │            │            │
                     ▼            ▼            ▼
              ┌───────────┐ ┌──────────┐ ┌───────────┐
              │ AI Agent  │ │ Google   │ │ ThingSpeak│
              │           │ │ Sheets   │ │ Dashboard │
              └─────┬─────┘ └──────────┘ └───────────┘
                    │
                    ▼
             ┌───────────────┐
             │ Safety Rules  │
             └───────┬───────┘
                     │
             ┌───────┴────────┐
             │                │
             ▼                ▼
        Irrigation          No Water
         Required            Needed
             │                │
             ▼                ▼
          ESP32             ESP32
             │                │
             ▼                ▼
          Relay             OFF
             │
             ▼
           PUMP
             │
             ▼
           FIELD

                    n8n
                     │
                     ▼
                ┌──────────┐
                │ Telegram │
                └────┬─────┘
                     │
              ┌──────┴──────┐
              ▼             ▼
             Text          Voice
             Alert         Alert
37. Recommended Project Title
For a college/project report, I would use:

“AI-Powered Automated Irrigation System Using Crop Prediction and Agentic IoT with ESP32, n8n Automation, Telegram Voice Alerts, Google Sheets and ThingSpeak Cloud Monitoring” LearnEngineering

Short title
“AI-Based Smart Irrigation System Using ESP32 and n8n”

Core technologies
ESP32
+
IoT Sensors
+
Wi-Fi
+
n8n
+
AI Agent
+
Telegram
+
Google Sheets
+
ThingSpeak
=
Agentic Smart Irrigation System
If you want this as a complete project report, the next logical version is to turn this into a chapter-by-chapter document containing Abstract, Introduction, Literature Survey, Problem Statement, Objectives, Proposed Methodology, complete circuit/schematic, component specifications, ESP32 source code, n8n workflow configuration, AI prompt, Telegram bot setup, Google Sheets setup, ThingSpeak setup, database format, flowcharts, UML/use-case diagram, sequence diagram, testing tables, results, advantages, limitations, future scope, conclusion, and viva questions/answers.

 


Project Summary
AI-Powered Automated Irrigation System Using Crop Prediction is a smart agriculture project that combines ESP32, IoT sensors, AI Agent, n8n automation, Telegram alerts, Google Sheets, and ThingSpeak to automate irrigation. LearnEngineering

Core workflow
Soil/Weather Sensors
        ↓
      ESP32
        ↓
     Wi-Fi
        ↓
      n8n
        ↓
    AI Agent
        ↓
Safety Validation
        ↓
   Pump ON/OFF
        ↓
Google Sheets + ThingSpeak
        ↓
Telegram Text/Voice Alert
Main functions
Measures soil moisture, temperature, humidity, rain and water level.

Uses crop type and growth stage to make irrigation recommendations.

ESP32 communicates with the n8n automation server.

n8n sends sensor information to an AI Agent.

AI recommends whether irrigation is required and suggests a duration.

Deterministic safety rules verify the AI recommendation before the pump operates.

Relay controls the irrigation pump.

Data is stored in Google Sheets for historical analysis.

ThingSpeak provides cloud-based graphs and monitoring.

Telegram sends real-time text and optional voice alerts.

The system can support remote status checking and manual commands. LearnEngineering

Historical data can later be used to develop a dedicated machine-learning crop/irrigation prediction model.


Key architecture


┌──────────────┐
│ Farm Sensors │
└──────┬───────┘
       ↓
┌──────────────┐
│    ESP32     │
└──────┬───────┘
       ↓
┌──────────────┐
│     n8n      │
└──────┬───────┘
       ↓
┌──────────────┐
│   AI Agent   │
└──────┬───────┘
       ↓
┌──────────────┐
│ Safety Logic │
└──────┬───────┘
       ↓
┌──────────────┐
│ Pump / Relay │
└──────────────┘

       n8n
        ├── Google Sheets
        ├── ThingSpeak
        └── Telegram
              ├── Text
              └── Voice
Main components
Hardware: ESP32, capacitive soil-moisture sensor, DHT22/DHT11, rain sensor, water-level sensor, relay, water pump and suitable power supply. CompareCPUs

Software: Arduino IDE, ESP32 firmware, n8n, AI/LLM API, Telegram Bot, Google Sheets and ThingSpeak.

Important design principle
The AI should recommend irrigation, not directly control the pump. Sensor validation, tank-level checks, rain detection, maximum pump runtime and other safety rules should be enforced independently before the ESP32 activates the pump.

Final concept:

Sense → Analyze → Predict → Validate → Irrigate → Log → Notify → Verify

This makes the project an Agentic IoT smart irrigation system rather than simply an automatic moisture-based pump controller.

 

on October 04, 2026 No comments: 
Email This
BlogThis!
Share to X
Share to Facebook
Share to Pinterest
AI Accident Alert & Vehicle Tracking using IoT Analytics

AI Accident Alert & Vehicle Tracking Using IoT, ESP32, n8n, AI Agent, Telegram, Google Sheets & ThingSpeak
Below is a complete reference implementation you can use as a final-year project, mini-project, prototype, GitHub project, or technical documentation.

The system combines: LearnEngineering

ESP32

MPU6050 accelerometer/gyroscope

GPS module

optional buzzer/SOS button

Wi-Fi

n8n automation

AI Agent

Telegram bot

Telegram voice alerts

Google Sheets

ThingSpeak cloud dashboard

accident detection

vehicle tracking

event logging

AI-based accident analysis

The architecture deliberately keeps fast accident detection on the ESP32 and uses the cloud/AI layer for analysis, notification and logging. ESP32 supports Wi-Fi station mode for Internet connectivity, while ThingSpeak provides REST APIs for writing channel data. Espressif Systems+1

1. Project title
AI Accident Alert & Vehicle Tracking Using IoT Analytics
Alternative project titles
You can use any of these for your report:

Option 1

AI-Powered Accident Detection and Vehicle Tracking System Using ESP32, IoT Analytics and n8n Automation LearnEngineering

Option 2

Agentic IoT Vehicle Safety System Using ESP32, AI Agent, n8n and Telegram Voice Alerts

Option 3

Smart Vehicle Accident Detection, GPS Tracking and AI Emergency Alert System

Option 4

AI-Powered ESP32 Vehicle Monitoring System with n8n, Telegram, Google Sheets and ThingSpeak

2. Abstract
Road accidents require rapid detection and communication because the driver or passengers may be unable to manually contact emergency contacts after a serious collision.

This project proposes an AI-powered IoT accident detection and vehicle tracking system based on an ESP32 microcontroller. The ESP32 continuously monitors vehicle motion using an MPU6050 accelerometer and gyroscope and obtains the vehicle's geographical position using a GPS receiver.

When an abnormal impact or accident-like motion is detected, the ESP32 generates an accident event containing acceleration, gyroscope, GPS coordinates, speed and device information. The event is transmitted through Wi-Fi to an n8n automation workflow.

n8n acts as the orchestration layer. It receives the IoT event, validates and enriches the data, sends the event to an AI Agent for interpretation, records the event in Google Sheets, updates ThingSpeak and generates an emergency notification.

The notification can be delivered to a predefined Telegram user or group as both a text message and a voice alert. Telegram's Bot API supports sending voice messages, while n8n provides built-in Telegram automation functionality. Telegram+1

The system therefore creates an integrated pipeline:

Physical vehicle → Sensors → ESP32 → Internet → n8n → AI Agent → Google Sheets + ThingSpeak + Telegram Voice Alert

3. Main objectives
The project has the following objectives:

Detect possible vehicle accidents.

Measure vehicle acceleration and angular motion.

Determine the vehicle's GPS position.

Track the vehicle remotely.

Send sensor data to a cloud platform. BrowseReference

Automatically analyze accident events using AI.

Generate emergency Telegram notifications.

Generate Telegram voice alerts.

Maintain an accident/event history in Google Sheets.

Visualize vehicle telemetry through ThingSpeak.

Provide an extensible agentic IoT architecture.

Reduce dependence on manual emergency reporting.


4. Overall system architecture



                         ┌───────────────────────┐
                         │      VEHICLE          │
                         │                       │
                         │  MPU6050              │
                         │  Accelerometer/Gyro   │
                         │                       │
                         │  GPS NEO-6M          │
                         │  Latitude/Longitude   │
                         │                       │
                         │  SOS Button           │
                         │  Buzzer/LED           │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │        ESP32           │
                         │                       │
                         │ Sensor acquisition    │
                         │ Accident detection    │
                         │ GPS processing        │
                         │ Event generation      │
                         └───────────┬───────────┘
                                     │
                                  Wi-Fi
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │     n8n WEBHOOK       │
                         │                       │
                         │ Receive IoT JSON      │
                         │ Validate data         │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │      AI AGENT         │
                         │                       │
                         │ Accident assessment   │
                         │ Severity classification│
                         │ Response generation   │
                         └──────┬─────┬─────┬────┘
                                │     │     │
                   ┌────────────┘     │     └─────────────┐
                   ▼                  ▼                   ▼
          ┌────────────────┐ ┌───────────────┐ ┌──────────────────┐
          │ Google Sheets  │ │  ThingSpeak   │ │    Telegram      │
          │ Event database │ │ Cloud graphs  │ │ Text + Voice     │
          └────────────────┘ └───────────────┘ └──────────────────┘
6. Hardware requirements
Required components
Component	Purpose
ESP32 DevKit	Main IoT controller
MPU6050	Accelerometer + gyroscope
NEO-6M GPS	Location and speed
Buzzer	Local accident warning
Push button	Manual SOS
LED	Status indication
Breadboard	Prototyping
Jumper wires	Connections
5 V power source	Vehicle/project power
USB cable	Programming
Optional components
OLED display

vibration sensor

temperature sensor

current sensor

GSM/LTE module

SD card

camera

ESP32-CAM

relay

emergency cancellation button

6. Recommended hardware architecture


                       +----------------------+
                       |       VEHICLE        |
                       +----------------------+

             +----------------+
             |    MPU6050     |
             | Accel + Gyro   |
             +-------+--------+
                     |
                 I2C |
                     |
                     v
              +-------------+
              |    ESP32    |
              |             |
              | Wi-Fi       |
              | Processing  |
              +------+------+ 
                     |
          +----------+-----------+
          |                      |
       UART GPS               GPIO
          |                      |
          v                      v
   +-------------+        +-------------+
   |   NEO-6M    |        | SOS Button  |
   | GPS Module  |        +-------------+
   +-------------+
                     |
                     v
                  Buzzer
8. Schematic diagram
A simple prototype wiring can be arranged as follows.

MPU6050 → ESP32
MPU6050	ESP32
VCC	3.3 V
GND	GND
SDA	GPIO 21
SCL	GPIO 22
GPS → ESP32
NEO-6M	ESP32
VCC	Appropriate module supply
GND	GND
TX	GPIO 16
RX	GPIO 17
Use a proper voltage level arrangement for the particular GPS module you purchase.

Buzzer
ESP32 GPIO 25
      |
      +---- Buzzer
      |
     GND
For a higher-current buzzer, drive it through a transistor rather than directly from the ESP32 GPIO. CompareCPUs

SOS button
GPIO 27
  |
  +-------- Push Button -------- GND
Configure the pin with INPUT_PULLUP.

8. Complete electrical block diagram


                  +-------------------+
                  |     5V INPUT      |
                  +---------+---------+
                            |
                     +------+------+
                     |   ESP32     |
                     |             |
                     | 3.3V        |
                     +--+----------+
                        |
             +----------+----------+
             |                     |
             v                     v
        +---------+           +---------+
        | MPU6050 |           |  GPS    |
        | I2C     |           | NEO-6M  |
        +---------+           +---------+
             |                     |
             |                     |
             +----------+----------+
                        |
                        v
                  Sensor Processing
                        |
                        v
                    Accident?
                    /       \
                  NO         YES
                  |           |
                  |           v
                  |      Create Event
                  |           |
                  +-----------+
                              |
                              v
                         Wi-Fi Upload
                              |
                              v
                          n8n Webhook
10. How accident detection works
The MPU6050 provides:

X acceleration

Y acceleration

Z acceleration

X angular velocity

Y angular velocity

Z angular velocity

Acceleration magnitude can be calculated as:

A=Ax2+Ay2+Az2A=\sqrt{A_x^2+A_y^2+A_z^2}

During stationary conditions, the acceleration magnitude is approximately close to:

1g≈9.81m/s21g \approx 9.81m/s^2

A collision can produce a sudden acceleration spike.

However, do not use a single acceleration threshold as a production accident detector.

A better prototype algorithm combines:

Acceleration spike
       +
Gyroscope spike
       +
Sudden change in motion
       +
Vehicle speed/GPS state
       +
Short confirmation window
Example:

Acceleration > threshold
          |
          v
   Possible impact
          |
          v
Check gyro
          |
          v
Check GPS speed
          |
          v
Calculate confidence
          |
          v
Accident confidence > 70% ?
       /             \
     NO               YES
     |                 |
 Normal event      ACCIDENT
                       |
                       v
                 Send emergency
10. Accident confidence calculation
For a prototype you can use:

Acceleration score = 40%
Gyroscope score    = 25%
Speed score        = 20%
Motion change      = 15%
Example:

acceleration = 85%
gyro         = 70%
speed        = 80%
motion       = 90%

confidence =
0.40(85) +
0.25(70) +
0.20(80) +
0.15(90)

confidence = 81.75%
The ESP32 can classify: CompareCPUs

0–39%   → NORMAL
40–69%  → SUSPICIOUS
70–100% → POSSIBLE ACCIDENT
For a student prototype, these thresholds should be experimentally calibrated rather than presented as medically or automotive-certified thresholds.

11. GPS tracking
The GPS module supplies:

{
  "latitude": 17.3850,
  "longitude": 78.4867,
  "speed_kmph": 42.5
}
The coordinates can be converted into a map URL:

https://www.google.com/maps?q=17.3850,78.4867
Your Telegram alert can therefore contain:

🚨 POSSIBLE ACCIDENT

Vehicle: CAR-001

Location:
17.3850, 78.4867

Speed:
42.5 km/h

Map:
https://www.google.com/maps?q=17.3850,78.4867
In the actual implementation, n8n should construct the map URL dynamically.

12. ESP32-to-n8n communication
The ESP32 sends JSON. CompareCPUs

Example:

{
  "device_id": "CAR-001",
  "event": "ACCIDENT",
  "timestamp": 1727979000,
  "accel_x": 3.21,
  "accel_y": 2.75,
  "accel_z": 16.42,
  "accel_magnitude": 17.01,
  "gyro_x": 12.4,
  "gyro_y": 9.8,
  "gyro_z": 21.3,
  "latitude": 17.385044,
  "longitude": 78.486671,
  "speed_kmph": 58.2,
  "accident_confidence": 86.4
}
13. n8n architecture
n8n is particularly suitable because it connects APIs, applications and AI workflows. n8n documents built-in Telegram functionality and AI capabilities. n8n Docs+1


The main workflow:


ESP32
  |
  | HTTP POST
  v
Webhook
  |
  v
Validate JSON
  |
  v
Normalize Data
  |
  +---------------------+
  |                     |
  v                     v
ThingSpeak          Google Sheets
  |
  v
AI Agent
  |
  v
Severity decision
  |
  +----------------------+
  |                      |
 NORMAL                ACCIDENT
  |                      |
  v                      v
Log only          Telegram text
                         |
                         v
                    Generate voice
                         |
                         v
                  Telegram voice
                         |
                         v
                  Send GPS location
14. n8n workflow nodes
Create the following nodes:

01 Webhook
       ↓
02 Code - Validate Payload
       ↓
03 IF - Accident?
       ↓
04 Google Sheets
       ↓
05 ThingSpeak HTTP Request
       ↓
06 AI Agent
       ↓
07 IF - Emergency?
       ↓
08 Telegram Text
       ↓
09 Text-to-Speech
       ↓
10 Telegram Voice
       ↓
11 Telegram Location
You can also split this into two workflows:

Workflow A — telemetry
ESP32
 ↓
Webhook
 ↓
Validation
 ↓
ThingSpeak
 ↓
Google Sheets
Workflow B — emergency
ESP32 Accident Event
 ↓
Webhook
 ↓
AI Agent
 ↓
Severity
 ↓
Telegram
 ↓
Voice
 ↓
Location
That architecture is easier to maintain.

15. n8n Webhook
Create:

Node: Webhook

Method:

POST
Example endpoint:

/webhook/vehicle-alert
ESP32 sends: CompareCPUs

POST https://YOUR-N8N-DOMAIN/webhook/vehicle-alert
Content-Type: application/json
with the JSON payload.

Do not expose an unprotected production webhook. Use authentication, a secret token/signature, rate limiting and HTTPS. n8n itself provides security auditing functionality that can identify issues such as unprotected webhooks. n8n Docs

16. n8n validation node
Use a Code node after the webhook.

Example:

const d = $json.body ?? $json;

const required = [
  "device_id",
  "latitude",
  "longitude",
  "accident_confidence"
];

for (const field of required) {
  if (d[field] === undefined || d[field] === null) {
    throw new Error(`Missing field: ${field}`);
  }
}

return [{
  json: {
    device_id: String(d.device_id),
    event: d.event || "TELEMETRY",
    latitude: Number(d.latitude),
    longitude: Number(d.longitude),
    speed_kmph: Number(d.speed_kmph || 0),
    accel_x: Number(d.accel_x || 0),
    accel_y: Number(d.accel_y || 0),
    accel_z: Number(d.accel_z || 0),
    accel_magnitude: Number(d.accel_magnitude || 0),
    gyro_x: Number(d.gyro_x || 0),
    gyro_y: Number(d.gyro_y || 0),
    gyro_z: Number(d.gyro_z || 0),
    accident_confidence:
      Number(d.accident_confidence || 0),

    map_url:
      `https://www.google.com/maps?q=${Number(d.latitude)},${Number(d.longitude)}`,

    received_at: new Date().toISOString()
  }
}];
n8n's Code node is intended for data transformation and logic within workflows. n8n Docs TryDev Tools

17. Google Sheets database
Create a spreadsheet called:

AI Vehicle Accident Monitoring
Create columns:

Column	Description
Timestamp	Event time
Device ID	Vehicle ID
Event	NORMAL/ACCIDENT
Latitude	GPS latitude
Longitude	GPS longitude
Speed	km/h
Accel X	X acceleration
Accel Y	Y acceleration
Accel Z	Z acceleration
Accel Magnitude	Total acceleration
Gyro X	X rotation
Gyro Y	Y rotation
Gyro Z	Z rotation
Confidence	Accident confidence
Severity	AI classification
AI Analysis	Explanation
Notification	Sent/Failed
n8n has a Google Sheets integration available for document/sheet operations. n8n Docs

18. ThingSpeak configuration
Create a ThingSpeak channel:

Channel name:
AI Vehicle Accident Monitoring
Suggested fields:

Field 1 = Acceleration
Field 2 = Gyroscope
Field 3 = Speed
Field 4 = Accident Confidence
Field 5 = Latitude
Field 6 = Longitude
Field 7 = Accident Status
Field 8 = Battery Voltage
ThingSpeak supports REST-based channel updates through api.thingspeak.com/update, including fields, latitude and longitude. MathWorks+1

Example:

https://api.thingspeak.com/update
Parameters:

api_key = YOUR_WRITE_API_KEY
field1 = 17.01
field2 = 21.3
field3 = 58.2
field4 = 86.4
field5 = 17.385044
field6 = 78.486671
field7 = 1
19. n8n ThingSpeak HTTP Request
Use:

Node: HTTP Request

Method:

POST
URL:

https://api.thingspeak.com/update.json
Body:

api_key={{ $env.THINGSPEAK_WRITE_KEY }}

field1={{ $json.accel_magnitude }}

field2={{ $json.gyro_z }}

field3={{ $json.speed_kmph }}

field4={{ $json.accident_confidence }}

field5={{ $json.latitude }}

field6={{ $json.longitude }}

field7={{ $json.event === "ACCIDENT" ? 1 : 0 }}
ThingSpeak returns an entry ID when the update succeeds and 0 on failure. MathWorks

20. AI Agent architecture
This is where the project becomes an Agentic IoT system instead of merely an IoT notification system. LearnSociology

The AI Agent receives:

Sensor data
+
GPS data
+
Vehicle state
+
Accident confidence
and determines:

Is this probably an accident?
What is the severity?
What action should be taken?
What message should be sent?
21. AI Agent prompt
Use a prompt similar to this:

You are an IoT Vehicle Safety AI Agent.

You receive telemetry from an ESP32 vehicle monitoring device.

Analyze:
- acceleration
- gyroscope
- speed
- GPS position
- accident confidence
- event type

Classify the event as one of:

NORMAL
SUSPICIOUS
ACCIDENT

If the event is an accident, classify severity:

LOW
MEDIUM
HIGH
CRITICAL

Rules:

1. Never claim that an accident is medically confirmed.
2. Treat sensor detection as a possible accident.
3. High acceleration combined with abnormal rotation increases accident likelihood.
4. A vehicle moving at significant speed before a large impact should increase severity.
5. If confidence is low, recommend monitoring rather than emergency escalation.
6. Always provide a concise emergency message.
7. Include GPS coordinates.
8. Include a Google Maps URL.

Return JSON only.
Expected output:

{
  "classification": "ACCIDENT",
  "severity": "HIGH",
  "confidence": 0.91,
  "reason": "Large acceleration spike combined with abnormal rotational motion.",
  "action": "SEND_EMERGENCY_ALERT",
  "telegram_message": "Possible high-severity vehicle accident detected.",
  "voice_message": "Emergency alert. A possible high-severity accident has been detected. Vehicle CAR-001 is located at the reported GPS position."
}
22. Important AI design principle
Do not allow the AI Agent to be the only accident detector.

Use:

ESP32 deterministic detection
             +
AI interpretation
rather than:

ESP32 → AI decides everything
Why?

Because Internet connectivity or AI response time could fail immediately after an accident.

The ESP32 should therefore detect the event locally and store/queue the event if necessary. CompareCPUs

23. Agentic decision architecture


             SENSOR DATA
                  |
                  v
          +---------------+
          | ESP32 Rules   |
          +-------+-------+
                  |
                  v
          Possible Accident
                  |
                  v
             n8n Webhook
                  |
                  v
          +---------------+
          |   AI AGENT    |
          +-------+-------+
                  |
       +----------+----------+
       |          |          |
       v          v          v
    NORMAL     SUSPICIOUS   ACCIDENT
       |          |          |
       |          |          v
       |          |     Severity
       |          |          |
       |          |          v
       |          |     Take Action
       |          |          |
       +----------+----------+
                  |
                  v
          Automation Tools
          /       |       \
         /        |        \
        v         v         v
   Sheets     ThingSpeak Telegram
25. Telegram Bot
Create a Telegram bot using Telegram's official bot creation mechanism.

Obtain:

BOT_TOKEN
and determine the target:

CHAT_ID
Keep the token secret.

n8n provides a Telegram node with operations for sending messages, audio, locations and other Telegram content. n8n Docs TryDev Tools

25. Telegram emergency message
Example:

🚨 VEHICLE ACCIDENT ALERT 🚨

Vehicle: CAR-001

Possible accident detected.

Severity: HIGH
Confidence: 91%

Speed: 58.2 km/h

Acceleration: 17.01 m/s²

Location:
17.385044, 78.486671

Open location:
https://www.google.com/maps?q=17.385044,78.486671

AI assessment:
Large acceleration spike combined with abnormal rotational motion.

Please check the vehicle immediately.
26. Telegram voice alert
The workflow should generate:

"Emergency alert. A possible high severity accident has been detected. Vehicle CAR-001 is currently at the reported GPS location. Please check the vehicle immediately."
Then convert the text to speech.

The resulting audio is passed to Telegram as a voice message.

Telegram's Bot API distinguishes voice messages from ordinary audio files and provides the sendVoice method for voice messages. Telegram

27. Voice workflow
AI Agent
   |
   v
voice_message
   |
   v
Text-to-Speech API
   |
   v
MP3/OGG audio
   |
   v
n8n Binary Data
   |
   v
Telegram Send Voice
   |
   v
Emergency recipient
Depending on the TTS service and Telegram integration version, you may use either a built-in n8n audio capability or an HTTP Request node to a TTS API. TryDev Tools

28. Telegram location
After the text alert, send the GPS location.

Telegram
   |
   +-- Send Message
   |
   +-- Send Voice
   |
   +-- Send Location
Latitude:

{{ $json.latitude }}
Longitude:

{{ $json.longitude }}
This makes the alert much more useful than sending coordinates as plain text.

29. ESP32 firmware
Below is a prototype firmware implementation using:

ESP32

MPU6050

TinyGPS++

Wi-Fi

HTTPClient

JSON payload

local accident detection

The ESP32 Arduino Wi-Fi and HTTPClient libraries support connecting to an access point and making HTTP requests. Espressif Systems+1 CompareCPUs

Arduino libraries
Install:

Adafruit MPU6050
Adafruit Unified Sensor
TinyGPSPlus
ArduinoJson
30. ESP32 code
#include <WiFi.h>
#include <HTTPClient.h>
#include <Wire.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <TinyGPSPlus.h>
#include <ArduinoJson.h>

// =====================================================
// WIFI
// =====================================================

const char* WIFI_SSID = "YOUR_WIFI";
const char* WIFI_PASSWORD = "YOUR_PASSWORD";

// n8n production webhook
const char* N8N_WEBHOOK =
    "https://YOUR-N8N-DOMAIN/webhook/vehicle-alert";

// =====================================================
// DEVICE
// =====================================================

const char* DEVICE_ID = "CAR-001";

// =====================================================
// GPS
// =====================================================

HardwareSerial GPSSerial(2);

#define GPS_RX 16
#define GPS_TX 17

TinyGPSPlus gps;

// =====================================================
// MPU6050
// =====================================================

Adafruit_MPU6050 mpu;

// =====================================================
// GPIO
// =====================================================

#define BUZZER_PIN 25
#define SOS_PIN    27
#define LED_PIN    2

// =====================================================
// TIMING
// =====================================================

unsigned long lastTelemetry = 0;

const unsigned long TELEMETRY_INTERVAL = 5000;

// =====================================================
// ACCIDENT PARAMETERS
// =====================================================

// Prototype values only.
// Calibrate using controlled experiments.

const float ACCEL_THRESHOLD = 18.0;
const float GYRO_THRESHOLD  = 15.0;
const float SPEED_THRESHOLD = 20.0;

// =====================================================
// WIFI
// =====================================================

void connectWiFi()
{
    Serial.print("Connecting to WiFi");

    WiFi.begin(WIFI_SSID, WIFI_PASSWORD);

    int attempts = 0;

    while (WiFi.status() != WL_CONNECTED &&
           attempts < 30)
    {
        delay(500);
        Serial.print(".");
        attempts++;
    }

    Serial.println();

    if (WiFi.status() == WL_CONNECTED)
    {
        Serial.println("WiFi connected");
        Serial.print("IP: ");
        Serial.println(WiFi.localIP());
    }
    else
    {
        Serial.println("WiFi connection failed");
    }
}

// =====================================================
// GPS UPDATE
// =====================================================

void updateGPS()
{
    while (GPSSerial.available())
    {
        gps.encode(GPSSerial.read());
    }
}

// =====================================================
// SEND EVENT TO N8N
// =====================================================

bool sendToN8N(
    String eventType,
    float ax,
    float ay,
    float az,
    float acceleration,
    float gx,
    float gy,
    float gz,
    float speed,
    float confidence
)
{
    if (WiFi.status() != WL_CONNECTED)
    {
        Serial.println("WiFi unavailable");
        return false;
    }

    HTTPClient http;

    http.begin(N8N_WEBHOOK);
    http.addHeader(
        "Content-Type",
        "application/json"
    );

    float latitude = 0;
    float longitude = 0;

    if (gps.location.isValid())
    {
        latitude = gps.location.lat();
        longitude = gps.location.lng();
    }

    StaticJsonDocument<1024> doc;

    doc["device_id"] = DEVICE_ID;
    doc["event"] = eventType;

    doc["timestamp"] = millis();

    doc["accel_x"] = ax;
    doc["accel_y"] = ay;
    doc["accel_z"] = az;
    doc["accel_magnitude"] = acceleration;

    doc["gyro_x"] = gx;
    doc["gyro_y"] = gy;
    doc["gyro_z"] = gz;

    doc["speed_kmph"] = speed;

    doc["latitude"] = latitude;
    doc["longitude"] = longitude;

    doc["gps_valid"] = gps.location.isValid();

    doc["accident_confidence"] = confidence;

    String payload;

    serializeJson(doc, payload);

    Serial.println("Sending:");
    Serial.println(payload);

    int httpCode = http.POST(payload);

    Serial.print("HTTP response: ");
    Serial.println(httpCode);

    http.end();

    return httpCode >= 200 &&
           httpCode < 300;
}

// =====================================================
// CALCULATE ACCELERATION
// =====================================================

float calculateAcceleration(
    sensors_event_t& accel
)
{
    return sqrt(
        accel.acceleration.x *
        accel.acceleration.x +

        accel.acceleration.y *
        accel.acceleration.y +

        accel.acceleration.z *
        accel.acceleration.z
    );
}

// =====================================================
// ACCIDENT CONFIDENCE
// =====================================================

float calculateConfidence(
    float acceleration,
    float gyro,
    float speed
)
{
    float score = 0;

    // Acceleration contribution
    if (acceleration > ACCEL_THRESHOLD)
        score += 40;

    // Gyroscope contribution
    if (gyro > GYRO_THRESHOLD)
        score += 30;

    // Speed contribution
    if (speed > SPEED_THRESHOLD)
        score += 20;

    // Combined condition
    if (acceleration > ACCEL_THRESHOLD &&
        gyro > GYRO_THRESHOLD)
    {
        score += 10;
    }

    if (score > 100)
        score = 100;

    return score;
}

// =====================================================
// BUZZER
// =====================================================

void accidentAlarm()
{
    digitalWrite(LED_PIN, HIGH);

    for (int i = 0; i < 5; i++)
    {
        digitalWrite(BUZZER_PIN, HIGH);
        delay(200);

        digitalWrite(BUZZER_PIN, LOW);
        delay(200);
    }

    digitalWrite(LED_PIN, LOW);
}

// =====================================================
// SETUP
// =====================================================

void setup()
{
    Serial.begin(115200);

    pinMode(BUZZER_PIN, OUTPUT);
    pinMode(SOS_PIN, INPUT_PULLUP);
    pinMode(LED_PIN, OUTPUT);

    digitalWrite(BUZZER_PIN, LOW);
    digitalWrite(LED_PIN, LOW);

    Wire.begin(21, 22);

    // MPU6050
    if (!mpu.begin())
    {
        Serial.println(
            "MPU6050 not found!"
        );

        while (true)
        {
            delay(1000);
        }
    }

    Serial.println(
        "MPU6050 initialized"
    );

    mpu.setAccelerometerRange(
        MPU6050_RANGE_8_G
    );

    mpu.setGyroRange(
        MPU6050_RANGE_500_DEG
    );

    // GPS
    GPSSerial.begin(
        9600,
        SERIAL_8N1,
        GPS_RX,
        GPS_TX
    );

    connectWiFi();
}

// =====================================================
// LOOP
// =====================================================

void loop()
{
    updateGPS();

    // Manual SOS
    if (digitalRead(SOS_PIN) == LOW)
    {
        Serial.println("SOS BUTTON");

        accidentAlarm();

        sendToN8N(
            "MANUAL_SOS",
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            gps.speed.isValid()
                ? gps.speed.kmph()
                : 0,
            100
        );

        delay(3000);
    }

    if (millis() -
        lastTelemetry <
        TELEMETRY_INTERVAL)
    {
        return;
    }

    lastTelemetry = millis();

    sensors_event_t accel;
    sensors_event_t gyro;
    sensors_event_t temp;

    mpu.getEvent(
        &accel,
        &gyro,
        &temp
    );

    float acceleration =
        calculateAcceleration(accel);

    float gyroMagnitude =
        sqrt(
            gyro.gyro.x *
            gyro.gyro.x +

            gyro.gyro.y *
            gyro.gyro.y +

            gyro.gyro.z *
            gyro.gyro.z
        );

    float speed =
        gps.speed.isValid()
            ? gps.speed.kmph()
            : 0;

    float confidence =
        calculateConfidence(
            acceleration,
            gyroMagnitude,
            speed
        );

    String eventType =
        confidence >= 70
            ? "ACCIDENT"
            : "TELEMETRY";

    Serial.println("------------------");

    Serial.print("Acceleration: ");
    Serial.println(acceleration);

    Serial.print("Gyro: ");
    Serial.println(gyroMagnitude);

    Serial.print("Speed: ");
    Serial.println(speed);

    Serial.print("Confidence: ");
    Serial.println(confidence);

    Serial.print("Event: ");
    Serial.println(eventType);

    if (eventType == "ACCIDENT")
    {
        accidentAlarm();
    }

    sendToN8N(
        eventType,

        accel.acceleration.x,
        accel.acceleration.y,
        accel.acceleration.z,

        acceleration,

        gyro.gyro.x,
        gyro.gyro.y,
        gyro.gyro.z,

        speed,

        confidence
    );
}
31. Important improvement: don't send every event as an accident
A real implementation should have a state machine.

NORMAL
  |
  | impact detected
  v
POSSIBLE_IMPACT
  |
  | confirmation
  v
ACCIDENT_PENDING
  |
  | confirmed
  v
ACCIDENT
  |
  | alert sent
  v
ALERTED
  |
  | reset
  v
NORMAL
This prevents multiple Telegram alerts for the same accident.

32. Better accident algorithm
Use a sliding window.

For example:

Sample rate = 50 Hz

Maintain last 2 seconds:

100 sensor samples
Calculate:

maximum acceleration
maximum gyro
change in acceleration
change in orientation
vehicle speed
Then:

IF

maxAcceleration > threshold
AND
maxGyro > threshold

THEN

possible accident
After that:

Wait 1–3 seconds

IF movement remains abnormal
OR
second sensor condition confirms impact

THEN

ACCIDENT
This is significantly better than a single sensor reading.

33. n8n AI workflow in detail

    
Create the workflow:


┌──────────────┐
│   Webhook    │
└──────┬───────┘
       │
       ▼
┌──────────────────┐
│ Validate Payload │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Prepare Location │
└────────┬─────────┘
         │
         ├─────────────────┐
         │                 │
         ▼                 ▼
┌──────────────┐   ┌───────────────┐
│ Google Sheets│   │  ThingSpeak   │
└──────────────┘   └───────────────┘
         │
         ▼
┌─────────────────┐
│     AI Agent    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Parse AI Result │
└────────┬────────┘
         │
         ▼
   ┌───────────────┐
   │ Severity?     │
   └──────┬────────┘
          │
       HIGH/CRITICAL
          │
          ▼
   ┌───────────────┐
   │ Telegram Text │
   └──────┬────────┘
          │
          ▼
   ┌───────────────┐
   │ Text to Speech│
   └──────┬────────┘
          │
          ▼
   ┌───────────────┐
   │Telegram Voice │
   └──────┬────────┘
          │
          ▼
   ┌───────────────┐
   │Telegram GPS   │
   │Location       │
   └───────────────┘
34. Google Sheets record
The n8n Google Sheets node should append something like: TryDev Tools

2026-10-04 21:45:23
CAR-001
ACCIDENT
17.385044
78.486671
58.2
3.21
2.75
16.42
17.01
12.4
9.8
21.3
86.4
HIGH
Large acceleration + abnormal rotation
SENT
This gives you a permanent project log.

35. ThingSpeak dashboard
Configure charts for:

Chart 1
Acceleration vs Time
Chart 2
Vehicle Speed vs Time
Chart 3
Accident Confidence vs Time
Chart 4
Gyroscope vs Time
Map
Use:

Latitude
Longitude
ThingSpeak supports channel data visualization and map-related channel functionality through its APIs/platform. MathWorks+1 BrowseReference

36. Complete data flow


                   VEHICLE
                      |
          +-----------+-----------+
          |                       |
          v                       v
      MPU6050                    GPS
          |                       |
          +-----------+-----------+
                      |
                      v
                   ESP32
                      |
             Accident Algorithm
                      |
          +-----------+-----------+
          |                       |
        NORMAL                 ACCIDENT
          |                       |
          +-----------+-----------+
                      |
                      v
                    Wi-Fi
                      |
                      v
                 n8n Webhook
                      |
                      v
                Data Validation
                      |
             +--------+--------+
             |                 |
             v                 v
        ThingSpeak       Google Sheets
             |                 |
             +--------+--------+
                      |
                      v
                   AI Agent
                      |
             +--------+---------+
             |        |         |
             v        v         v
           LOW     MEDIUM     HIGH
             |        |         |
             |        |         v
             |        |     Telegram
             |        |         |
             |        |     +---+---+
             |        |     |       |
             |        |     v       v
             |        |   Text    Voice
             |        |
             |        v
             |      Log
             |
             v
            Log
38. Telegram conversation example
Accident event
System → Telegram LearnEngineering

🚨 VEHICLE ACCIDENT ALERT

System:

Vehicle: CAR-001
Status: Possible Accident
Severity: HIGH
Confidence: 91%
Speed: 58.2 km/h

System:

📍 Location: 17.385044, 78.486671

System:

🗺 Open vehicle location

System:

Sensor analysis indicates a large acceleration spike combined with abnormal rotational motion.

System → Voice

"Emergency alert. A possible high-severity accident has been detected. Vehicle CAR-001 is currently at the reported GPS location. Please check the vehicle immediately."

38. Manual SOS operation
The project should also have a manual emergency button.

Driver presses SOS
        |
        v
ESP32 detects button
        |
        v
Generate MANUAL_SOS event
        |
        v
n8n
        |
        v
AI Agent
        |
        v
Telegram
        |
        +---- Text
        |
        +---- Voice
        |
        +---- Location
This is useful even if no accident occurs.

For example:

Medical emergency
Vehicle breakdown
Threat/security problem
Driver assistance
39. Vehicle tracking mode
Apart from accident detection, send periodic telemetry.

For example:

Every 5 seconds:

GPS
Speed
Acceleration
Gyroscope
Battery
The system becomes: LearnEngineering

Vehicle
   |
   v
ESP32
   |
   v
n8n
   |
   +---- ThingSpeak
   |
   +---- Google Sheets
ThingSpeak's REST API is designed for reading and writing channel data, so it is suitable for this telemetry layer. MathWorks

40. Recommended ThingSpeak fields
Use:

FIELD 1 → Acceleration
FIELD 2 → Gyroscope
FIELD 3 → Speed
FIELD 4 → Accident Confidence
FIELD 5 → Latitude
FIELD 6 → Longitude
FIELD 7 → Accident Flag
FIELD 8 → Battery
Example:

Field 1 = 17.01
Field 2 = 21.30
Field 3 = 58.20
Field 4 = 86.40
Field 5 = 17.385044
Field 6 = 78.486671
Field 7 = 1
Field 8 = 3.92
41. Security architecture
Do not hard-code all production secrets directly into firmware.

Avoid:

const char* API_KEY = "my-secret-key";
when the code will be published.

Instead use:

ESP32
   |
   | device authentication
   v
n8n
   |
   +-- Telegram credential
   +-- Google credential
   +-- ThingSpeak key
   +-- AI API credential
   +-- TTS credential
n8n credentials should be stored in n8n rather than exposed in the ESP32 payload. TryDev Tools

42. Recommended authentication
Add an authentication header:

X-DEVICE-TOKEN: YOUR_DEVICE_SECRET
ESP32:

http.addHeader(
    "X-DEVICE-TOKEN",
    DEVICE_SECRET
);
n8n validation:

const token =
    $headers["x-device-token"];

if (token !== $env.DEVICE_SECRET) {
    throw new Error("Unauthorized device");
}
For production, consider stronger mechanisms such as signed requests, rotating credentials and HTTPS certificate validation.

43. Failure handling
The system should be designed around failures.

Case 1 — Wi-Fi unavailable
ESP32
 ↓
No Wi-Fi
 ↓
Store event locally
 ↓
Reconnect
 ↓
Upload later
Add EEPROM/NVS or SD storage for queued events.

Case 2 — n8n unavailable
ESP32
 ↓
HTTP failure
 ↓
Save event
 ↓
Retry
Case 3 — Telegram unavailable
n8n
 ↓
Telegram error
 ↓
Log failure
 ↓
Retry
Case 4 — GPS unavailable
Use:

"gps_valid": false
and send:

GPS unavailable
Last known location:
...
Case 5 — AI unavailable
The workflow should still send a deterministic alert:

ESP32 confidence > threshold
        |
        v
AI unavailable
        |
        v
Fallback emergency notification
This is extremely important.

44. AI fallback
Use an n8n IF node: TryDev Tools

AI Agent
   |
   +---- success → AI decision
   |
   +---- error → deterministic decision
Fallback:

const confidence =
    Number($json.accident_confidence || 0);

let severity = "LOW";

if (confidence >= 90) {
    severity = "CRITICAL";
}
else if (confidence >= 80) {
    severity = "HIGH";
}
else if (confidence >= 70) {
    severity = "MEDIUM";
}

return [{
    json: {
        ...$json,
        severity,
        ai_status: "FALLBACK"
    }
}];
45. State diagram


                 +---------+
                 | START   |
                 +----+----+
                      |
                      v
                 +---------+
                 | NORMAL  |
                 +----+----+
                      |
               Impact detected
                      |
                      v
             +----------------+
             | POSSIBLE IMPACT|
             +-------+--------+
                     |
              Confirm sensors
                     |
              +------+------+
              |             |
             NO            YES
              |             |
              v             v
           NORMAL        ACCIDENT
                            |
                            v
                      SEND EVENT
                            |
                            v
                       AI ANALYSIS
                            |
                  +---------+---------+
                  |                   |
                 LOW               HIGH
                  |                   |
                  v                   v
                 LOG              ALERT
                                      |
                         +------------+------------+
                         |            |             |
                         v            v             v
                       TEXT         VOICE         GPS
                         |            |             |
                         +------------+-------------+
                                      |
                                      v
                                   ALERTED
                                      |
                                      v
                                   RESET
                                      |
                                      v
                                   NORMAL


46. Software architecture



+-----------------------------------------------------+
|                    SOFTWARE                         |
+-----------------------------------------------------+
|                                                     |
| Arduino IDE                                         |
|      |                                              |
|      v                                              |
| ESP32 Firmware                                      |
|      |                                              |
|      +---- MPU6050 driver                           |
|      +---- GPS driver                               |
|      +---- Accident algorithm                       |
|      +---- Wi-Fi                                    |
|      +---- HTTP/JSON                                |
|                                                     |
+-----------------------------------------------------+

                    INTERNET
                       |
                       v

+-----------------------------------------------------+
|                     n8n                             |
+-----------------------------------------------------+
|                                                     |
| Webhook                                             |
|      |                                              |
| Validation                                          |
|      |                                              |
| Data transformation                                 |
|      |                                              |
| AI Agent                                            |
|      |                                              |
| +----+----------+-------------+                     |
| |               |             |                     |
| v               v             v                     |
| Sheets       ThingSpeak    Telegram                 |
|                                                     |
+-----------------------------------------------------+
47. AI Agent tools
A more advanced version can give the AI Agent tools such as:

Tool 1:
Get latest vehicle telemetry

Tool 2:
Get previous accident records

Tool 3:
Write incident to Google Sheets

Tool 4:
Send Telegram alert

Tool 5:
Send vehicle location

Tool 6:
Get ThingSpeak history

Then the AI Agent becomes:



                 AI AGENT
                    |
       +------------+-------------+
       |            |             |
       v            v             v
Telemetry       Incident       Notification
Tool            History Tool   Tool
       |            |             |
       +------------+-------------+
                    |
                    v
               Decision
n8n's AI tooling is designed to allow integrations and tools to participate in AI workflows. n8n Docs TryDev Tools

48. Example AI reasoning
Input:

{
  "speed_kmph": 72,
  "accel_magnitude": 24.2,
  "gyro_z": 32.1,
  "accident_confidence": 94
}
AI response:

{
  "classification": "ACCIDENT",
  "severity": "CRITICAL",
  "confidence": 0.96,
  "reason": "High-speed vehicle combined with a large acceleration spike and extreme rotational movement.",
  "action": "SEND_EMERGENCY_ALERT"
}
The automation then executes:

Send Telegram
Send Voice
Send Location
Write Sheet
Update ThingSpeak
49. Project flowchart


             START
               |
               v
       Initialize ESP32
               |
               v
        Initialize MPU6050
               |
               v
         Initialize GPS
               |
               v
          Connect Wi-Fi
               |
               v
        Read sensor data
               |
               v
        Calculate motion
               |
               v
        Calculate speed
               |
               v
       Accident detected?
          /          \
        NO            YES
        |              |
        v              v
   Send telemetry   Activate buzzer
        |              |
        |              v
        |          Create event
        |              |
        +------+-------+
               |
               v
          Send to n8n
               |
               v
        AI Agent analysis
               |
               v
       Determine severity
               |
               v
      Log Google Sheets
               |
               v
       Update ThingSpeak
               |
               v
        Emergency alert?
          /          \
        NO            YES
        |              |
        v              v
      Finish      Telegram text
                       |
                       v
                  Voice message
                       |
                       v
                  GPS location
                       |
                       v
                     END
50. Complete technology stack
Layer	Technology
Controller	ESP32
Motion sensor	MPU6050
Location	NEO-6M GPS
Programming	Arduino C++
Connectivity	Wi-Fi
API protocol	HTTP/JSON
Automation	n8n
AI	n8n AI Agent + LLM
Notification	Telegram
Voice	TTS
Database/logging	Google Sheets
IoT dashboard	ThingSpeak
Mapping	Google Maps URL
Cloud workflow	n8n
Visualization	ThingSpeak
51. Required n8n credentials
You will need credentials for:

1. AI/LLM provider
2. Telegram Bot
3. Google Sheets
4. TTS provider
5. ThingSpeak API key
ThingSpeak uses channel-specific write API keys for channel updates. MathWorks

52. n8n environment variables
For a self-hosted deployment, conceptually maintain:

DEVICE_SECRET
THINGSPEAK_WRITE_KEY
TELEGRAM_CHAT_ID
N8N_WEBHOOK_URL
API credentials should preferably be stored in the credential manager rather than ordinary workflow fields.

53. Testing procedure
Do not begin by simulating a real road accident.

Use controlled tests.

Test 1 — Normal operation
Move the MPU6050 gently.

Expected:

EVENT = TELEMETRY
ACCIDENT = FALSE
Test 2 — GPS
Move the GPS outdoors.

Expected:

GPS valid = true

latitude ≠ 0
longitude ≠ 0
Test 3 — Manual SOS
Press the button.

Expected:

ESP32
 ↓
n8n
 ↓
Google Sheets
 ↓
Telegram text
 ↓
Telegram voice
 ↓
GPS location
Test 4 — Artificial impact
Perform a safe controlled sensor test.

Expected:

Acceleration spike
       +
Gyroscope spike
       ↓
Possible accident
Test 5 — Wi-Fi failure
Turn off Wi-Fi.

Expected:

ESP32 detects failure
and, if local queueing has been implemented:

Event stored
Test 6 — n8n failure
Stop n8n. TryDev Tools

Expected:

HTTP request fails
and the ESP32 should not crash.

Test 7 — Telegram failure
Disable Telegram credentials temporarily.

Expected:

Incident remains in Google Sheets
and failure is logged.

54. Expected project output
When an accident is detected:

ESP32
ACCIDENT DETECTED
Confidence: 91%
n8n
Webhook received
Data validated
AI analysis completed
Severity = HIGH
Google Sheets
Incident record inserted
ThingSpeak
Telemetry updated
Telegram
🚨 VEHICLE ACCIDENT ALERT
followed by:

🔊 Voice alert
and:

📍 Vehicle location
55. Example complete incident record
{
  "device_id": "CAR-001",
  "event": "ACCIDENT",
  "timestamp": "2026-10-04T16:15:22Z",

  "sensor": {
    "accel_x": 3.21,
    "accel_y": 2.75,
    "accel_z": 16.42,
    "magnitude": 17.01,
    "gyro_x": 12.4,
    "gyro_y": 9.8,
    "gyro_z": 21.3
  },

  "vehicle": {
    "speed_kmph": 58.2
  },

  "gps": {
    "latitude": 17.385044,
    "longitude": 78.486671
  },

  "analysis": {
    "confidence": 0.91,
    "classification": "ACCIDENT",
    "severity": "HIGH"
  },

  "notifications": {
    "telegram_text": true,
    "telegram_voice": true,
    "location": true
  }
}
56. Advantages
Hardware advantages
Low-cost

Compact

Wi-Fi enabled

Easy to program

Expandable

Software advantages
n8n provides visual automation TryDev Tools

AI adds contextual analysis

Google Sheets is easy to inspect

ThingSpeak provides visualization

Telegram provides instant notification

AI advantages
The AI can interpret several sensor values simultaneously instead of relying on one threshold.

57. Limitations
This is important for your project report.

The system is a prototype and not a certified automotive safety system.

Potential limitations include:

GPS may be unavailable indoors.

GPS location can have several meters of error.

Wi-Fi may not be available everywhere.

MPU6050 readings depend on mounting orientation.

Sensor thresholds require calibration.

False positives are possible.

False negatives are possible.

AI decisions can be imperfect.

Internet latency can delay cloud alerts.

Telegram requires Internet access.

The system should not replace certified vehicle safety equipment or emergency services.

58. Future enhancements
You can list these in your project presentation.

1. GSM/LTE
Add:

SIM7600 / LTE module
so alerts can work without Wi-Fi.

2. Camera
Add:

ESP32-CAM
or another camera to capture accident images.

3. Cloud database
Replace Google Sheets with:

PostgreSQL
Supabase
Firebase
MongoDB
4. Advanced ML model
Train an accident classifier using:

Acceleration
Gyroscope
Speed
Orientation
Time-series windows
5. Driver monitoring
Add:

Camera
Drowsiness detection
Face detection
Eye closure detection
6. OBD-II
Read:

Vehicle speed
RPM
Engine temperature
Diagnostic codes
7. Multi-vehicle fleet
Architecture:

CAR-001 ─┐
CAR-002 ─┤
CAR-003 ─┼──> n8n ──> AI Agent
CAR-004 ─┤
CAR-005 ─┘
8. Emergency-service integration
Future version could integrate authorized emergency-response APIs.

59. Multi-vehicle architecture


             VEHICLE 1
             ESP32 #001
                 |
                 |
             VEHICLE 2
             ESP32 #002
                 |
                 |
             VEHICLE 3
             ESP32 #003
                 |
                 |
                 v
          +--------------+
          |     n8n      |
          | Central IoT  |
          +------+-------+
                 |
        +--------+---------+
        |        |         |
        v        v         v
       AI     Database   Alerts
       |        |         |
       v        v         v
    Analysis  Sheets   Telegram
                         |
                         v
                     Operator
61. Suggested project folder structure
    
AI-Vehicle-IoT/


│
├── README.md
│
├── firmware/
│   └── esp32_vehicle_monitor/
│       └── esp32_vehicle_monitor.ino
│
├── n8n/
│   ├── telemetry-workflow.json
│   └── accident-workflow.json
│
├── docs/
│   ├── architecture.md
│   ├── hardware.md
│   ├── software.md
│   ├── testing.md
│   └── screenshots/
│
├── diagrams/
│   ├── block-diagram.png
│   ├── flowchart.png
│   ├── circuit.png
│   └── sequence-diagram.png
│
└── examples/
    └── accident-payload.json
63. Sequence diagram
ESP32          n8n          AI Agent       Sheets     ThingSpeak    Telegram
  |              |              |             |            |            |
  |---JSON------>|              |             |            |            |
  |              |              |             |            |            |
  |              |---validate-->|             |            |            |
  |              |              |             |            |            |
  |              |--------------------------->|            |            |
  |              |---------------------------------------->|            |
  |              |              |             |            |            |
  |              |---sensor data------------->|            |            |
  |              |              |             |            |            |
  |              |              |--analysis-->|            |            |
  |              |              |             |            |            |
  |              |<--decision---|             |            |            |
  |              |              |             |            |            |
  |              |--------------------------------------------------->|
  |              |              |             |            |            |
  |              |--------------------------------------------------->|
  |              |              |             |            |            |
  |              |              |             |            |<--voice----|
  |              |              |             |            |            |
64. One-line project explanation for viva
The system uses an ESP32 to detect abnormal vehicle motion and obtain GPS coordinates, sends the event to n8n through an HTTP webhook, uses an AI Agent to analyze accident severity, logs the incident in Google Sheets, visualizes telemetry on ThingSpeak, and automatically sends Telegram text, voice and location alerts. LearnEngineering

65. 30-second presentation explanation
“Our project is an AI-powered IoT accident detection and vehicle tracking system. An ESP32 collects acceleration and gyroscope data from an MPU6050 and GPS information from a GPS module. When abnormal vehicle motion is detected, the ESP32 sends the event to an n8n webhook. n8n acts as the automation and agentic layer. An AI Agent analyzes the sensor data and determines the possible accident severity. The incident is stored in Google Sheets and telemetry is sent to ThingSpeak. For high-severity events, n8n automatically sends a Telegram emergency message, voice alert and GPS location to the configured recipient.”

66. Final system architecture


                     ┌───────────────────────┐
                     │       VEHICLE         │
                     │                       │
                     │  MPU6050              │
                     │  GPS                  │
                     │  SOS                  │
                     │  Buzzer               │
                     └──────────┬────────────┘
                                │
                                ▼
                     ┌───────────────────────┐
                     │        ESP32          │
                     │                       │
                     │ Sensor Processing     │
                     │ Accident Detection    │
                     │ GPS Processing        │
                     │ Wi-Fi Communication   │
                     └──────────┬────────────┘
                                │
                              HTTPS
                                │
                                ▼
                     ┌───────────────────────┐
                     │     n8n WEBHOOK       │
                     └──────────┬────────────┘
                                │
                                ▼
                     ┌───────────────────────┐
                     │ DATA VALIDATION       │
                     └──────────┬────────────┘
                                │
              ┌─────────────────┼──────────────────┐
              │                 │                  │
              ▼                 ▼                  ▼
        Google Sheets      ThingSpeak          AI Agent
              │                 │                  │
              │                 │                  ▼
              │                 │            Severity
              │                 │                  │
              │                 │          ┌───────┴───────┐
              │                 │          │               │
              │                 │        NORMAL        ACCIDENT
              │                 │          │               │
              │                 │          │               ▼
              │                 │          │        Telegram Text
              │                 │          │               │
              │                 │          │               ▼
              │                 │          │        Text-to-Speech
              │                 │          │               │
              │                 │          │               ▼
              │                 │          │        Telegram Voice
              │                 │          │               │
              │                 │          │               ▼
              │                 │          │        Telegram GPS
              │                 │          │
              └─────────────────┴──────────┴───────────────┘
68. Recommended implementation order
Build it in this order rather than trying everything simultaneously:

ESP32 + MPU6050 CompareCPUs

Confirm acceleration and gyro readings.

ESP32 + GPS

Confirm latitude, longitude and speed.

ESP32 accident algorithm

Display confidence on Serial Monitor.

ESP32 + Wi-Fi

Confirm Internet connectivity.

n8n Webhook

Receive a manually generated JSON payload first.

ESP32 → n8n

Send actual sensor data.

Google Sheets

Log every event.

ThingSpeak

Display sensor charts.

Telegram

Send text alerts.

AI Agent

Add classification and severity.

TTS

Convert AI-generated emergency message to speech.

Telegram Voice

Send the generated voice alert.

GPS location

Send the vehicle's location.

Failure/retry logic

Handle Wi-Fi, n8n, Telegram and GPS failures. TryDev Tools

Final enclosure

Mount the ESP32 and sensors securely in the vehicle.

This staged approach makes troubleshooting much easier.

Official references
ESP32 Arduino Wi-Fi documentation

ESP32 HTTPClient source/documentation

ThingSpeak Write Data API

ThingSpeak REST API reference

n8n documentation

n8n Telegram node documentation

Telegram Bot API

Important: For an academic prototype, this design is complete enough to implement and demonstrate. For a real vehicle/emergency deployment, the accident classifier, electrical design, enclosure, connectivity, cybersecurity and emergency escalation would need substantially more validation and safety engineering.



Project Summary
AI Accident Alert & Vehicle Tracking Using IoT Analytics is an IoT-based vehicle safety system that combines ESP32, MPU6050, GPS, n8n automation, AI Agent, Telegram, Google Sheets, and ThingSpeak. LearnSociology

Core workflow
MPU6050 + GPS
      ↓
    ESP32
      ↓
Accident Detection
      ↓
 Wi-Fi / HTTP
      ↓
   n8n Webhook
      ↓
    AI Agent
      ↓
 ┌────┼───────────────┐
 ↓    ↓               ↓
Sheets ThingSpeak   Telegram
                     ↓
               Text + Voice
                     ↓
                GPS Location
Main functions
ESP32 collects vehicle motion data.

MPU6050 measures acceleration and gyroscope movement.

GPS provides latitude, longitude and vehicle speed.

ESP32 calculates an accident confidence score.

n8n receives and processes the IoT event.

AI Agent classifies the event as Normal, Suspicious or Accident and estimates severity.

Google Sheets stores accident and telemetry records.

ThingSpeak provides cloud telemetry visualization.

Telegram sends emergency text notifications.

Text-to-Speech generates an emergency voice message.

Telegram Voice delivers the voice alert.

GPS coordinates are sent so the recipient can locate the vehicle.

A physical SOS button can manually trigger an emergency alert.

Key architecture principle
The ESP32 performs the initial accident detection locally, while the AI Agent performs higher-level analysis. This prevents the system from depending entirely on AI or Internet connectivity for the initial detection. CompareCPUs

Main hardware
ESP32 DevKit

MPU6050

NEO-6M GPS

Buzzer

SOS push button

LED

Power supply

Main software
Arduino IDE / ESP32 Arduino framework

C++

n8n

AI/LLM

Telegram Bot API

Google Sheets

ThingSpeak

Text-to-Speech service

Example emergency event
🚨 POSSIBLE VEHICLE ACCIDENT

Vehicle: CAR-001
Severity: HIGH
Confidence: 91%
Speed: 58.2 km/h

Location:
17.385044, 78.486671

AI analysis:
Large acceleration spike combined
with abnormal rotational movement.

Voice alert: SENT
GPS location: SENT
Google Sheets: LOGGED
ThingSpeak: UPDATED
Project objective
The overall goal is to create an agentic IoT vehicle-monitoring platform that can automatically: LearnSociology

Sense → Detect → Analyze → Log → Decide → Notify → Track

It is suitable as a final-year engineering project, IoT project, AI project, ESP32 project, or n8n automation project, with further development required before any real-world safety-critical deployment.

 

AI Accident Alert & Vehicle Tracking — Mind Map


                           ┌──────────────────────────────┐
                           │ AI ACCIDENT ALERT &          │
                           │ VEHICLE TRACKING SYSTEM      │
                           └──────────────┬───────────────┘
                                          │
        ┌─────────────────────────────────┼─────────────────────────────────┐
        │                                 │                                 │
        ▼                                 ▼                                 ▼
 ┌───────────────┐                 ┌───────────────┐                 ┌───────────────┐
 │    HARDWARE   │                 │   ESP32 IoT   │                 │    CLOUD      │
 └───────┬───────┘                 └───────┬───────┘                 └───────┬───────┘
         │                                 │                                 │
   ┌─────┼─────┐                    ┌─────┼─────┐                    ┌──────┼──────┐
   │     │     │                    │     │     │                    │      │      │
   ▼     ▼     ▼                    ▼     ▼     ▼                    ▼      ▼      ▼
 MPU6050 GPS  SOS                 Wi-Fi  JSON  HTTP                 n8n  ThingSpeak Sheets
   │     │     │                    │     │     │                     │      │      │
   │     │     │                    └─────┴─────┘                     │      │      │
   │     │     │                          │                           │      │      │
   ▼     ▼     ▼                          ▼                           │      │      │
Accel  GPS  Button                  n8n Webhook                        │      │      │
Gyro   Speed Buzzer                       │                            │      │      │
                                         ▼                            │      │      │
                                  Data Validation                     │      │      │
                                         │                            │      │      │
                                         ▼                            │      │      │
                                    AI AGENT ◄────────────────────────┘      │      │
                                         │                                   │      │
                              ┌──────────┼──────────┐                        │      │
                              │          │          │                        │      │
                              ▼          ▼          ▼                        │      │
                           NORMAL   SUSPICIOUS  ACCIDENT                     │      │
                                                   │                         │      │
                                                   ▼                         │      │
                                             SEVERITY                        │      │
                                                   │                         │      │
                                    ┌──────────────┼──────────────┐          │      │
                                    │              │              │          │      │
                                    ▼              ▼              ▼          │      │
                                  LOW           HIGH          CRITICAL       │      │
                                    │              │              │          │      │
                                    └──────────────┼──────────────┘          │      │
                                                   │                         │      │
                                                   ▼                         │      │
                                             NOTIFICATION                    │      │
                                                   │                         │      │
                              ┌────────────────────┼─────────────────┐       │      │
                              │                    │                 │       │      │
                              ▼                    ▼                 ▼       │      │
                         Telegram Text      Telegram Voice      GPS Location│      │
                              │                    │                 │       │      │
                              └────────────────────┼─────────────────┘       │      │
                                                   │                         │      │
                                                   ▼                         │      │
                                             Emergency User                 │      │
                                                                             │      │
                                                                             └──────┘
Simplified Concept Map
AI VEHICLE SAFETY
│
├── 1. SENSING
│   ├── MPU6050
│   │   ├── Acceleration
│   │   └── Gyroscope
│   ├── GPS
│   │   ├── Latitude
│   │   ├── Longitude
│   │   └── Speed
│   └── SOS Button
│
├── 2. ESP32
│   ├── Sensor Reading
│   ├── Accident Algorithm
│   ├── Confidence Score
│   ├── Wi-Fi
│   └── JSON/HTTP
│
├── 3. ACCIDENT DETECTION
│   ├── Acceleration Spike
│   ├── Gyroscope Spike
│   ├── Speed
│   ├── Motion Change
│   └── Confidence
│
├── 4. n8n AUTOMATION
│   ├── Webhook
│   ├── Validation
│   ├── Data Processing
│   ├── AI Agent
│   └── Decision Logic
│
├── 5. AI AGENT
│   ├── Event Classification
│   │   ├── Normal
│   │   ├── Suspicious
│   │   └── Accident
│   ├── Severity
│   │   ├── Low
│   │   ├── Medium
│   │   ├── High
│   │   └── Critical
│   └── Recommended Action
│
├── 6. CLOUD
│   ├── Google Sheets
│   │   └── Incident Database
│   └── ThingSpeak
│       ├── Charts
│       ├── Telemetry
│       └── Location
│
├── 7. ALERT SYSTEM
│   └── Telegram
│       ├── Text Alert
│       ├── Voice Alert
│       └── GPS Location
│
├── 8. RELIABILITY
│   ├── Wi-Fi Failure
│   ├── n8n Failure
│   ├── Telegram Failure
│   ├── GPS Failure
│   ├── AI Failure
│   └── Retry / Local Storage
│
└── 9. FUTURE
    ├── GSM/LTE
    ├── Camera
    ├── OBD-II
    ├── Machine Learning
    ├── Driver Monitoring
    └── Multi-Vehicle Fleet
