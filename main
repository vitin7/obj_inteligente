#include <ESP8266WiFi.h>
#include <PubSubClient.h>

// Definições para conexão Wi-Fi
const char* ssid = "SEU_SSID";
const char* password = "SUA_SENHA";

// Definições para conexão MQTT
const char* mqtt_server = "ENDERECO_DO_BROKER_MQTT";
const int mqtt_port = 1883;
const char* mqtt_user = "USUARIO_MQTT";
const char* mqtt_password = "SENHA_MQTT";

// Definições dos pinos do sensor
const int trigPin = 5; // GPIO 5 (D1)
const int echoPin = 4; // GPIO 4 (D2)

// Cliente Wi-Fi e MQTT
WiFiClient espClient;
PubSubClient client(espClient);

// Função para conectar ao Wi-Fi
void setup_wifi() {
  delay(10);
  Serial.println();
  Serial.print("Conectando a ");
  Serial.println(ssid);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("WiFi conectado");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

// Função para conectar ao broker MQTT
void reconnect() {
  while (!client.connected()) {
    Serial.print("Tentando conexão MQTT...");
    if (client.connect("ESP8266Client", mqtt_user, mqtt_password)) {
      Serial.println("conectado");
    } else {
      Serial.print("falhou, rc=");
      Serial.print(client.state());
      Serial.println(" tentando novamente em 5 segundos");
      delay(5000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  setup_wifi();
  client.setServer(mqtt_server, mqtt_port);
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop();

  // Leitura do sensor ultrassônico
  long duration, distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = (duration / 2) / 29.1;

  // Publica a distância no tópico MQTT
  char msg[50];
  snprintf(msg, 50, "Distância: %ld cm", distance);
  Serial.print("Publicando mensagem: ");
  Serial.println(msg);
  client.publish("car/sensor/ultrasonic", msg);

  delay(2000); // Aguarda 2 segundos antes de repetir a leitura
}
