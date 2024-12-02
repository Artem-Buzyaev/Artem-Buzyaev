#include "Esp8266Wifi.h" // подключаем библиотек ESP
#include "ESP8266WebServer.h"
ESP8266WebServer server(80) // что то типо порта

const char* ssid = "Kvantorium75"; // имя сети
const char* password = "TechKvant75!" // пароль

void setup() {
  pinMode(D0, OUTPUT);

}

void loop() {
  digitalWrite(D0, 1);
}
