#include <SPI.h>
#include <Ethernet.h>
byte mac[] = { 
  0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
IPAddress ip(192,168,1,177);
EthernetServer server(80);

void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  Serial.begin(9600);
   while (!Serial) {
  }
  Ethernet.begin(mac, ip);
  server.begin();
  Serial.print("server is at ");
  Serial.println(Ethernet.localIP());
}


void loop() {
  EthernetClient client = server.available();
  if (client) {
    Serial.println("new client");
    String currentLine = "";   
    boolean currentLineIsBlank = true;
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        Serial.write(c);
        if (c == '\n') {
          if (currentLine.length() == 0) {    
            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println();
            client.print("Click <a href=\"/H\">here</a> Allumer l'ampoule<br>");
            client.print("Click <a href=\"/L\">here</a> Eteindre l'ampoule<br>");
            client.print("Click <a href=\"/B\">here</a> Bracher la prise<br>");
            client.print("Click <a href=\"/A\">here</a> Débrancher la prise");
            client.println();
            break;         
          } 
          else {    
            currentLine = "";
          }
        }     
        else if (c != '\r') {  
          currentLine += c;     
        }
        if (currentLine.endsWith("GET /H")) {
          digitalWrite(2, HIGH);
        }
        if (currentLine.endsWith("GET /L")) {
          digitalWrite(2, LOW);
        }
        if (currentLine.endsWith("GET /B")) {
          digitalWrite(3, HIGH);               
        }
        if (currentLine.endsWith("GET /A")) {
          digitalWrite(3, LOW);                
        }
      }
    }
    client.stop();
    Serial.println("client disonnected");
  }
}
