Projeto: Sensor de Sensoriamento e Atuação para Veículos com ESP8266 e MQTT
Resumo do Projeto
Este projeto utiliza um ESP8266 para medir distâncias usando um sensor ultrassônico e enviar esses dados para um broker MQTT. O objetivo é implementar um sistema de sensoriamento e atuação para veículos, permitindo a coleta e envio de dados de proximidade que podem ser usados para evitar colisões ou para outras funcionalidades automotivas.

Componentes Necessários
ESP8266 (NodeMCU ou outra variante)
Sensor Ultrassônico HC-SR04
Jumpers para conexões
Fonte de alimentação adequada para o ESP8266
Broker MQTT (por exemplo, Mosquitto)
Circuito
Sensor Ultrassônico HC-SR04:
VCC -> 3.3V no ESP8266
GND -> GND no ESP8266
TRIG -> GPIO 5 (D1) no ESP8266
ECHO -> GPIO 4 (D2) no ESP8266
Código Fonte
Inclusão de Bibliotecas
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
client.publish("vehicle/sensor/ultrasonic", msg);

delay(2000); // Aguarda 2 segundos antes de repetir a leitura
}

Explicação do Código
Conexão Wi-Fi:

O ESP8266 se conecta à rede Wi-Fi utilizando as credenciais fornecidas.
Conexão MQTT:

O ESP8266 tenta se conectar ao broker MQTT. Se falhar, ele espera 5 segundos e tenta novamente.
Leitura do Sensor Ultrassônico:

O pino TRIG é ativado por 10 microssegundos para enviar um pulso ultrassônico.
O tempo que leva para o pulso refletido ser recebido pelo pino ECHO é medido.
A distância é calculada com base na duração do pulso.
Publicação dos Dados:

A distância medida é publicada no tópico MQTT vehicle/sensor/ultrasonic.
Possíveis Melhorias
Atuação Baseada nos Dados:

Adicionar atuadores (como LEDs, buzzer, ou motores) que respondem aos dados de distância, acionando alarmes ou tomando ações corretivas quando uma determinada distância mínima for alcançada.
Segurança e Confiabilidade:

Implementar SSL/TLS para a comunicação MQTT para garantir segurança.
Adicionar reconexões automáticas e tolerância a falhas mais robusta.
Integração com Outros Sistemas:

Integrar o sistema com uma interface web ou aplicação mobile para monitoramento em tempo real.
Utilizar serviços de armazenamento na nuvem para histórico de dados e análise.

Conclusão
Este projeto fornece uma base para criar um sistema de sensoriamento e atuação para veículos, usando o ESP8266, um sensor ultrassônico, e MQTT. Este tipo de sistema pode ser usado em diversas aplicações automotivas, como assistência ao estacionamento, detecção de obstáculos, e prevenção de colisões. Com melhorias e integrações adicionais, pode se tornar uma solução poderosa e versátil para diversas necessidades automotivas.
