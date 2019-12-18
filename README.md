# Hanocia-Bluetooth-
#include <Servo.h>
#define lightSensor A5
int lightLevel;

Servo joint1;
Servo joint2;

int b,q,teta,a =180;
 char i = 'N';
 boolean newData = false;
void setup() {
  Serial.begin(9600);
  joint1.attach(2);
  joint2.attach(3);
  joint1.write(0);
  joint2.write(0);
  for(int h=4;h<14;h++){
    pinMode(h, OUTPUT);
  }
  delay(400);
}

void loop() {
    recvOneChar();
    Light();
}
 void recvOneChar() {
 if (Serial.available() > 0) {
 i = Serial.read();
 q = int(i)-48;
// Serial.print(q);
 newData = true;
 }
 }
void Light() {
 if (newData == true) {
  if(q<9&&q>0){
 Serial.println("");
 digitalWrite(4, HIGH);
 Serial.print("This is ");
 Serial.print(q);
 Serial.println("rd day ");
 if(q == 1){  Serial.println("Sheichiano");}
 Serial.println("Bracha");
 
 delay(300);
 //for(int a = 80 ; a >0 ;a--){
        joint1.write(0); 
      delay(200);
      
    for(int j = 0 ; j < 53;j++){
        joint2.write(j); 
      delay(33);
    }
   delay(3000);
   digitalWrite(13, HIGH);
       for(int j = 53 ; j > 0;j--){
        joint2.write(j); 
      delay(33);
    }
        joint1.write(15); 

    delay(800);
  switch (q) {
 case 1:

    for(int j = 0 ; j < 53;j++){
        joint2.write(j); 
      delay(33);
    }
       delay(3000);
       digitalWrite(5, HIGH);
       for(int j = 53 ; j > 0;j--){
           joint2.write(j); 
           delay(33);
      }

     break;
     
     default:
     for(b = 0 ; b < q; b++){
            if(b>=1){
//              y = 0.3214x2 + 23.75x - 34.214 = 0.9996

              teta = 0.3214*(b+2)*(b+2)+23.75*(b+2) -34.214;
              joint1.write(teta);             //Teta = 0.3214x2 - 30.179x + 235.43
              delay(500);
             }
       
            for(int j = 0 ; j <52;j++){
              joint2.write(j); 
              delay(33);
             }                
       delay(3000);
       digitalWrite(b+5, HIGH);
       for(int j = 52 ; j > 0;j--){
        joint2.write(j);
        delay(33);
        }    
      }

     break;
  }

    joint1.write(90); 
    joint1.write(0); 
    delay(250);
    Serial.println("Shirim");
    delay(2000);
    digitalWrite(4, LOW);
    darkness();
    for(int h=4;h<14;h++){
    digitalWrite(h, LOW);
    }
  newData = false;
  delay(2000);
  }
 }
}
 
void darkness() {
  int a = 1,b=44;
  while( analogRead(lightSensor) < 500)
  {
     Serial.print("Estimated time remaining:  ");
     Serial.print(b);Serial.print(":");
     if(a<51){ Serial.println(60-a);  }
     else{Serial.print("0");Serial.println(60-a);     }
     delay(1000);
     if(a==60){ b--;a=0; }
     a++;   
  }
}
