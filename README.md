#include <Ultrasonic.h>
#include <Servo.h>

#define INT_A_PIN 2
#define INT_B_PIN 3
#define SIG_A_PIN 4
#define SIG_B_PIN 5

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

long rightCount = 0;
long leftCount = 0;

uint32_t myTimer1;
Servo myservo1;

Ultrasonic ultrasonic1(9, 10);                     // левый датчик
int distance1;
Ultrasonic ultrasonic2(13, 12);                   // датчик по середине
int distance2;

void setup() {
myservo1.attach(8);
pinMode(INT_A_PIN, INPUT);
pinMode(INT_B_PIN, INPUT);
pinMode(SIG_A_PIN, INPUT);
pinMode(SIG_B_PIN, INPUT);

Serial.begin(9600);

attachInterrupt(digitalPinToInterrupt(INT_A_PIN), EncA, RISING);
attachInterrupt(digitalPinToInterrupt(INT_B_PIN), EncB, RISING);
for (int i = 4; i < 8; i++) {     
pinMode(i, OUTPUT);
}
}

void loop()
{

servo1();  //сервопривод переводится в крайне левое положение
 
go1(); //вперед 60 секунд

go2(); //влево

go3(); //вперед 81 секунду

go4(); //вправо

go5(); //вперед 30 секунд

servo2();  //открытие крышки и ее закрытие через 5 секунд

}

   void go1(){
distance2 = ultrasonic2.read();
while (distance2 > 70){                         // цикл, пока дистанция больше 50, выполняй тело цикла 
distance2 = ultrasonic2.read();               // чтение уз датчика   
    
           
if (millis() - myTimer1 >= 60000){            // таймер на 5 с      
myTimer1 = millis();                          // сброс таймера
Serial.println("ого");                        // проверка работы тайиера 
distance2 = ultrasonic2.read();               // чтение уз датчика
    
    
break;
delay(60000);
        
}
else{ 
digitalWrite(DIR_1, LOW);                    // езжай вперед
digitalWrite(SPEED_1, 255); 
digitalWrite(DIR_2, HIGH);
digitalWrite(SPEED_2, 255);
    
if (rightCount > leftCount){
digitalWrite(DIR_1, LOW);  
for (int i = 255; i >= 110; i--) {   //правый
analogWrite(SPEED_1, i);
delay(10);
}  
}
Serial.print("Right Count: ");
Serial.println(rightCount);
Serial.print("Left Count: ");
Serial.println(leftCount);
Serial.println(distance2);
delay(100);   
}                            
while (distance2 < 70){                  // выход из цикла если дистанция меньше 50

distance2 = ultrasonic2.read();
digitalWrite(DIR_1, LOW);              // остановка               
digitalWrite(SPEED_1, LOW);
digitalWrite(DIR_2, LOW);                                
digitalWrite(SPEED_2, LOW);
delay(100);
}
} 
}

   void go2(){
distance2 = ultrasonic2.read();
while (distance2 > 1){                         // цикл, пока дистанция больше 50, выполняй тело цикла 
distance2 = ultrasonic2.read();               // чтение уз датчика   
    
            
if (millis() - myTimer1 >= 1900){            // таймер на 2 с      
myTimer1 = millis();                          // сброс таймера
Serial.println("ого");                        // проверка работы тайиера 
distance2 = ultrasonic2.read();               // чтение уз датчика
    
    
break;
delay(1900);
        
}
    
else{ 
distance2 = ultrasonic2.read();   
digitalWrite(DIR_1,LOW);                    // корректировка для левого мотора
digitalWrite(SPEED_1, 255);
digitalWrite(DIR_2, LOW);                   //левый мотор
digitalWrite(SPEED_2, 255); 
}        
}    
}

   void go3(){
distance2 = ultrasonic2.read();
while (distance2 > 70){                         // цикл, пока дистанция больше 50, выполняй тело цикла 
distance2 = ultrasonic2.read();               // чтение уз датчика   
    
           
if (millis() - myTimer1 >= 81000){            // таймер на 5 с      
myTimer1 = millis();                          // сброс таймера
Serial.println("ого");                        // проверка работы тайиера 
distance2 = ultrasonic2.read();               // чтение уз датчика
    
    
break;
delay(81000);
        
}
else{ 
digitalWrite(DIR_1, LOW);                    // езжай вперед
digitalWrite(SPEED_1, 255); 
digitalWrite(DIR_2, HIGH);
digitalWrite(SPEED_2, 255);
    
if (rightCount > leftCount){
digitalWrite(DIR_1, LOW);  
for (int i = 255; i >= 110; i--) {   //правый
analogWrite(SPEED_1, i);
delay(10);
}  
}
Serial.print("Right Count: ");
Serial.println(rightCount);
Serial.print("Left Count: ");
Serial.println(leftCount);
Serial.println(distance2);
delay(100);   
}                            
while (distance2 < 70){                  // выход из цикла если дистанция меньше 50

distance2 = ultrasonic2.read();
digitalWrite(DIR_1, LOW);              // остановка               
digitalWrite(SPEED_1, LOW);
digitalWrite(DIR_2, LOW);                                
digitalWrite(SPEED_2, LOW);
delay(100);
}
} 
}

   void go4(){
distance2 = ultrasonic2.read();
while (distance2 > 1){                         // цикл, пока дистанция больше 50, выполняй тело цикла 
distance2 = ultrasonic2.read();                // чтение уз датчика   
    
            
if (millis() - myTimer1 >= 1900){             // таймер на 2 с      
myTimer1 = millis();                          // сброс таймера
Serial.println("ого");                        // проверка работы тайиера 
distance2 = ultrasonic2.read();               // чтение уз датчика
    
    
break;
delay(1900);
        
}
    
else{ 
distance2 = ultrasonic2.read();              // корректировка для левого мотора   
digitalWrite(DIR_1,HIGH);                    // правый мотор
digitalWrite(SPEED_1, 255);
digitalWrite(DIR_2, HIGH);                   // левый мотор
digitalWrite(SPEED_2, 255); 
}   
}    
}

   void go5(){
distance2 = ultrasonic2.read();
while (distance2 > 70){                         // цикл, пока дистанция больше 50, выполняй тело цикла 
distance2 = ultrasonic2.read();               // чтение уз датчика   
    
           
if (millis() - myTimer1 >= 30000){            // таймер на 5 с      
myTimer1 = millis();                          // сброс таймера
Serial.println("ого");                        // проверка работы тайиера 
distance2 = ultrasonic2.read();               // чтение уз датчика
    
    
break;
delay(30000);
        
}
else{ 
digitalWrite(DIR_1, LOW);                    // езжай вперед
digitalWrite(SPEED_1, 255); 
digitalWrite(DIR_2, HIGH);
digitalWrite(SPEED_2, 255);
    
if (rightCount > leftCount){
digitalWrite(DIR_1, LOW);  
for (int i = 255; i >= 110; i--) {   //правый
analogWrite(SPEED_1, i);
delay(10);
}  
}
Serial.print("Right Count: ");
Serial.println(rightCount);
Serial.print("Left Count: ");
Serial.println(leftCount);
Serial.println(distance2);
delay(100);   
}                            
while (distance2 < 70){                  // выход из цикла если дистанция меньше 50

distance2 = ultrasonic2.read();
digitalWrite(DIR_1, LOW);              // остановка               
digitalWrite(SPEED_1, LOW);
digitalWrite(DIR_2, LOW);                                
digitalWrite(SPEED_2, LOW);
delay(100);
}
} 
}

void EncA()
{
if ( digitalRead(SIG_A_PIN) )
{
rightCount--;
} else {
rightCount++;
}
}

void EncB()
{
if ( digitalRead(SIG_A_PIN) )
{
leftCount--;
} else {
leftCount++;
}
}

void servo1 (){
  myservo1.write(90);
}


void servo2 (){
int i = 0;
while (i <= 1){
  myservo1.write(180);
  delay(1500);
  myservo1.write(90);
  delay(5000);
  myservo1.write(180);
  delay(1500);
  i=1;
  break;
}
}
