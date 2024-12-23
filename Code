#include <WiFi.h>
#include <PubSubClient.h>

// Wi-Fi and MQTT Configuration
const char* ssid = "Your_SSID"; // Replace with your Wi-Fi SSID
const char* password = "Your_PASSWORD"; // Replace with your Wi-Fi Password
const char* mqttServer = "industrial.api.ubidots.com"; // Ubidots MQTT Broker
const int mqttPort = 1883;
const char* mqttUser = "Your_Ubidots_Token"; // Replace with Ubidots token
const char* mqttPassword = "";

// Relays GPIO Pins
const int relay1 = 25;
const int relay2 = 26;
const int relay3 = 27;
const int relay4 = 14;

WiFiClient espClient;
PubSubClient client(espClient);

// Callback Function
void callback(char* topic, byte* payload, unsigned int length) {
  String message = "";
  for (int i = 0; i < length; i++) {
    message += (char)payload[i];
  }

  if (String(topic) == "/v1.6/devices/esp32/relay1") {
    digitalWrite(relay1, message == "1" ? LOW : HIGH);
  } else if (String(topic) == "/v1.6/devices/esp32/relay2") {
    digitalWrite(relay2, message == "1" ? LOW : HIGH);
  } else if (String(topic) == "/v1.6/devices/esp32/relay3") {
    digitalWrite(relay3, message == "1" ? LOW : HIGH);
  } else if (String(topic) == "/v1.6/devices/esp32/relay4") {
    digitalWrite(relay4, message == "1" ? LOW : HIGH);
  }
}

// Setup Function
void setup() {
  Serial.begin(115200);

  // Wi-Fi Connection
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to Wi-Fi...");
  }
  Serial.println("Connected to Wi-Fi");

  // MQTT Connection
  client.setServer(mqttServer, mqttPort);
  client.setCallback(callback);

  while (!client.connected()) {
    Serial.println("Connecting to MQTT...");
    if (client.connect("ESP32Client", mqttUser, mqttPassword)) {
      Serial.println("Connected to MQTT");
    } else {
      Serial.print("Failed with state ");
      Serial.println(client.state());
      delay(2000);
    }
  }

  // Subscribing to MQTT Topics
  client.subscribe("/v1.6/devices/esp32/relay1");
  client.subscribe("/v1.6/devices/esp32/relay2");
  client.subscribe("/v1.6/devices/esp32/relay3");
  client.subscribe("/v1.6/devices/esp32/relay4");

  // Initializing Relay Pins
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);
  pinMode(relay3, OUTPUT);
  pinMode(relay4, OUTPUT);

  // Relays OFF Initially
  digitalWrite(relay1, HIGH);
  digitalWrite(relay2, HIGH);
  digitalWrite(relay3, HIGH);
  digitalWrite(relay4, HIGH);
}

// Loop Function
void loop() {
  client.loop();
}
