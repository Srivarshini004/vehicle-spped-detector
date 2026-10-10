# vehicle-spped-detector
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x3f, 16, 2); //Enter your address of your I2C Module it will be different for you
int timer1;
int timer2;
float Time;
int flag1 = 0;
int flag2 = 0;
float distance = 5.0;
float speed;
int ir_s1 = 34;
int ir_s2 = 35;
int buzzer = 13;
void setup()
{
serial.begin(115200);  
  pinMode(ir_s1, INPUT);
  pinMode(ir_s2, INPUT);
  pinMode(buzzer, OUTPUT);
  
  lcd.begin();
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print(" Welcome To  My ");
lcd.setCursor(0,1);
  lcd.print("YouTube  Channel");
  delay(2000);
  lcd.clear();
}
void loop() {
if(flag1==1 && flag2==1){
     if(timer1 > timer2){Time = timer1 - timer2;}





else if(timer2 > timer1){Time = timer2 - timer1;}
 Time=Time/1000;//convert millisecond to second
 speed=(distance/Time);//v=d/t
 speed=speed*3600;//multiply by seconds per hr
 speed=speed/1000;//division by meters per Km 
 }
if(speed==0){ 
lcd.setCursor(0, 1); 
if(flag1==0 && flag2==0){lcd.print("No car  detected");}
                    else{lcd.print("Searching...    ");} 
}
else{
    lcd.clear(); 
    lcd.setCursor(0, 0); 
    lcd.print("Speed:");
   lcd.print(speed,1);
    lcd.print("Km/Hr  ");
    lcd.setCursor(0, 1); 
  if(speed > 50){lcd.print("  Over Speeding  "); 
digitalWrite(buzzer, HIGH);}
            else{lcd.print("  Normal Speed   "); }    
    delay(3000);
    digitalWrite(buzzer, LOW);
    speed = 0;
    flag1 = 0;
    flag2 = 0;    
 }
}
