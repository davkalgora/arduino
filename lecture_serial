int a=13; //braché ampoule
int c=12; //braché prise
int b;
void setup(){
  pinMode(a, OUTPUT);
  pinMode(c, OUTPUT);
  Serial.begin(9600);
}
void loop(){
  if(Serial.available()>0){
      b = Serial.read();
      Serial.println(b);
      if(b=='r'){
        digitalWrite(a, HIGH);
      }
      if(b=='s'){
        digitalWrite(a, LOW);
      }     
       if(b=='t'){
        digitalWrite(c, HIGH);
      }
      if(b=='u'){
        digitalWrite(c, LOW);
      }  
  }  
}
