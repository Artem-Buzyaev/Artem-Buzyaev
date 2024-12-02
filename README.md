#include "ESP8266WiFi.h"
#include "ESP8266WebServer.h"
ESP8266WebServer server(80);

const char* ssid = "Kvantorium75"; 
const char* password = "TechKvant75!";
byte tries = 10; 

void setup(){
  pinMode(D0, OUTPUT);
  WiFi.begin(ssid, password);
  Serial.begin(9600);
  while (--tries && WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.println(".");
  }
  if (WiFi.status() != WL_CONNECTED){
    Serial.println("Non Connecting to WiFi..");
  } else{
    Serial.println("");
    Serial.println("WiFi connected");
    Serial.println("IP address: ");
    Serial.println(WiFi.localIP());
  }

  server.on("/", HTTP_POST, []() {
      digitalWrite(D0, 1);
    // проверка запроса с ключем LED
    if (server.argName(0) == "LED") {
      digitalWrite(D0, 1);
    }
    
  });
  server.on("/", handleRootPath);
  server.begin();
}

void loop() {
  server.handleClient(); 
}

void handleRootPath() {
  server.send(200, "text/plain", "");
}
