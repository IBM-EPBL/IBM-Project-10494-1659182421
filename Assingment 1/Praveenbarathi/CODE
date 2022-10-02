// C++ code
//
#include<Servo.h>

#define LED 13
#define FAN 10
#define TEMP A0
#define BUZZER 11
#define PIR 12
#define DOOR 5
#define TRIGGER 6
#define ECHO 7
#define TRIGGER1 9
#define ECHO1 8

Servo S;

void setup()
{
  Serial.begin(9600);
  pinMode(LED,OUTPUT);
  pinMode(FAN,OUTPUT);
  pinMode(BUZZER,OUTPUT);
  pinMode(PIR,INPUT);
  pinMode(DOOR,OUTPUT);
  pinMode(TRIGGER,OUTPUT);
  pinMode(ECHO,INPUT);
  pinMode(TRIGGER1,OUTPUT);
  pinMode(ECHO1,INPUT);
  S.attach(DOOR);
  S.write(90);
  
  
}

void loop()
{
  //Car Garage
  digitalWrite(TRIGGER,0);
  digitalWrite(TRIGGER,1);
  delayMicroseconds(10);
  digitalWrite(TRIGGER,0);
  float d = pulseIn(ECHO,1);
  float l = (d*0.0343)/2;
  int m = map(l,0,330,0,255);
  
  if(m<=50)
  {
    tone(BUZZER,294,700);
    delay(1000);
    noTone(BUZZER);
    Serial.println("Buzzer horn when Car parked");
  }
  else
    analogWrite(BUZZER,0);
  
  
  //Door Open
  int z = digitalRead(PIR);
  delay(1000);
  if(z==1)
  {
    S.write(0);
    Serial.println("Door Opened");
    delay(3000);
    S.write(90);
    delay(1000);
  }
    else
    {
    S.write(90);
    delay(1000);
    }
  digitalWrite(TRIGGER1,0);
  digitalWrite(TRIGGER1,1);
  delayMicroseconds(10);
  digitalWrite(TRIGGER1,0);
  float d1 = pulseIn(ECHO1,1);
  float l1 = (d1*0.0343)/2;
  if(l1<330)
    {
      //IN ROOM
    Serial.println("Person in Room");
    digitalWrite(LED,1);
    double a = analogRead(TEMP);
    double t = (((a/1024)*5)-0.5)*100;
    int s = map(t,-40,120,0,255);
    if(s>100)
      analogWrite(FAN,s);
      delay(2000);
   }
  else
  {
     digitalWrite(LED,0);
     analogWrite(FAN,0);
  }
}
