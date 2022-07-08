#include <EEPROM.h>
#define out1 2
#define out2 3
#define out3 4
#define out4 5
#define out5 6
#define out6 7
#define out7 8
#define out8 9
#define out9 10
#define out10 11
#define out11 12
#define out12 13

int de=500,y=500,x=500;
int th=30,la=500;
int temar=0,hh=0,mm=0,ss=0;

int set=A5,on=A1,low=A2,light=A3,temp=A4;

void setup(){
    Serial.begin(9600);
    
    pinMode(out1,OUTPUT);
    pinMode(out2,OUTPUT);
    pinMode(out3,OUTPUT);
    pinMode(out4,OUTPUT);
    pinMode(out5,OUTPUT);
    pinMode(out1,OUTPUT);
    pinMode(out6,OUTPUT);
    pinMode(out7,OUTPUT);
    pinMode(out8,OUTPUT);
    pinMode(out9,OUTPUT);
    pinMode(out10,OUTPUT);
    pinMode(out11,OUTPUT);
    pinMode(out12,OUTPUT);
    pinMode(light,INPUT_PULLUP);
    pinMode(on,INPUT_PULLUP);
    pinMode(set,INPUT_PULLUP);
    pinMode(low,INPUT_PULLUP);
    pinMode(temp,INPUT_PULLUP);
    if(EEPROM.read(0)==0){}
else{
      
   hh_write();
   mm_write();
    ss_write();          
EEPROM.write(0, 0);
}
 hh_read(); 
 mm_read();
 ss_read();
 }
void loop(){
    int set= digitalRead(A5);
    int on= digitalRead(A1);
    int low= digitalRead(A2);
    int light= analogRead(A3);
    int temp= analogRead(A4);
    if(temp<200){
     digitalWrite(out8,HIGH);
        delay(100);
        }
      else{
       digitalWrite(out8,LOW);
        }
    
    delay(100);
    Serial.println(temp);
    delay(200);
    if(on==0){
        if(temar<20){temar=temar+1;
            
        }
        if(temar==20){
            digitalWrite(out9,HIGH);
            Serial.println(temar);
            if(set==0){
          digitalWrite(out12,HIGH);
           delay(100);
          digitalWrite(out12,LOW);   
           delay(100);  
        hh+1;
        hh++;
        hh+2;
        hh++;
        delay(100);
        hh=hh;
           hh_write();    
        
       }     
    }
       
    }
    
    if(on==0){
        
        if(temar<20){temar=temar+1;
            
        }
        if(temar==20){
            Serial.println(temar);
            
    if(low==0){
        hh=0;
           digitalWrite(out12,HIGH);
           delay(100);
          digitalWrite(out12,LOW);   
           delay(100);
         hh=hh;
          digitalWrite(out2,LOW);
          digitalWrite(out3,LOW); 
          digitalWrite(out4,LOW);
          digitalWrite(out5,LOW); 
          digitalWrite(out6,LOW);
          digitalWrite(out7,LOW); 
          digitalWrite(out8,LOW);
          digitalWrite(out9,LOW); 
          digitalWrite(out10,LOW);
          digitalWrite(out11,LOW); 
          digitalWrite(out12,LOW);        
          hh_write(); 
            
    }
    }
      }
    else{
            delay(100);
        digitalWrite(out9,LOW);
            temar=0;
        }
    
    if(light<500){
        hh+1;
        hh++;
        delay(100);
        hh=hh;
        
        hh_write();
        
    }
    switch(hh){
        
        
        case 0:
        digitalWrite(out2,HIGH);
        digitalWrite(out1,true);
        delay(250);
        digitalWrite(out1,false);
        delay(250);
        break;
        
        case 1: //j.j.m
        for(int i=1;i<=2;i++){   
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        delay(de);
        if(temp<th){
        digitalWrite(out11,HIGH);
            }
        delay(de);
        delay(la);
        for(int i=1;i<=10;i++){
        digitalWrite(out1,HIGH);
        delay(250);
        digitalWrite(out1,LOW);
         delay(250);
            }
        delay(y);
        
        delay(de);
        while(mm<60){
        mm_write();
       Serial.println(mm);
            
        hh=2;
        hh_write();
        digitalWrite(out2,LOW);
        digitalWrite(out3,HIGH);
        for(int i=1;i<=3;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        break;
        
            
        case 2:
        
            
        
        digitalWrite(out1,HIGH);
        digitalWrite(out10,LOW);
        digitalWrite(out11,LOW);  
        break;
        case 3://j.a.r
        for(int i=1;i<=3;i++){   
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        delay(la);
        if(temp<th){
        digitalWrite(out11,HIGH);
            }
        delay(de);
        hh=4;
        hh_write();
          digitalWrite(out3,LOW);
         digitalWrite(out4,HIGH);
        for(int i=1;i<=4;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        digitalWrite(out1,HIGH);
        
        delay(de);
        delay(de);
        delay(de);
        break;
        case 4:
        digitalWrite(out1,HIGH);
        digitalWrite(out10,LOW);
        digitalWrite(out11,LOW);
        break;
        case 5://j.m.b
        for(int i=1;i<=4;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        if(temp<th){
        digitalWrite(out11,HIGH);
            }
        delay(de);
        hh=6;
        hh_write();
         digitalWrite(out4,LOW);
         digitalWrite(out5,HIGH);
        for(int i=1;i<=5;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        break;
        case 6:
        digitalWrite(out1,HIGH);
        digitalWrite(out10,LOW);
        digitalWrite(out11,LOW);
        break;
        case 7://j.e.sh
        for(int i=1;i<=5;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        delay(de);
        if(temp<th){
        digitalWrite(out11,HIGH);
            }
        delay(de);
        delay(de);
        delay(y);
        
        hh=8;
        digitalWrite(out1,HIGH);
        delay(1000);
        hh_write();
            digitalWrite(out5,LOW);
            digitalWrite(out6,HIGH);
            digitalWrite(out1,LOW);
        delay(1000);
        break;
        case 8:
        
        digitalWrite(out1,HIGH);
        digitalWrite(out10,LOW);
        digitalWrite(out11,LOW);
        break;
            case 9: //j.f.r
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        delay(de);//15mint
        delay(y); //5mint
        delay(y);
        delay(y);
        if(temp<th){
        digitalWrite(out11,HIGH);//f
            }
        delay(de); //15mint
        delay(y);//5mint
        hh=10;
        hh_write();
            digitalWrite(out6,LOW);
            digitalWrite(out7,HIGH);
        for(int i=1;i<=2;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        break;
        case 10:
        digitalWrite(out10,LOW);
        digitalWrite(out1,HIGH);
        digitalWrite(out11,LOW);
        break;
            
        //juma off
        
        case 11://h.f.r
        digitalWrite(out1,HIGH);
        digitalWrite(out10,HIGH);
        delay(de);//15mint
        delay(de); //15mint
        if(temp<th){
        digitalWrite(out11,HIGH);
            }
        delay(de);
        delay(de);//5mint
        delay(de);
            
            
        hh=12;
        hh_write();
            digitalWrite(out7,LOW);
            digitalWrite(out2,HIGH);
        for(int i=1;i<=2;i++){
        digitalWrite(out1,HIGH);
        delay(x);
        digitalWrite(out1,LOW);
        delay(x);
        }
        break;
        case 12:
        digitalWrite(out10,LOW);
        digitalWrite(out1,HIGH);
         
            delay(100);
            
            
              mm++;
            mm_write();
            }     
        break; 
        hh=0;
        
        digitalWrite(out2,HIGH);
        delay(1000);
        hh_write();
        
        break;
        default :
        hh=0;
        for(int i=1;i<=5;i++){
        digitalWrite(out1,HIGH);
        delay(500);
         
        digitalWrite(out1,LOW);
        delay(500);
            }
        
        
    }
       
  }  

void hh_write(){ 
    Serial.println(hh);
EEPROM.write(1,  hh%10);
EEPROM.write(2, (hh/10)%10);
EEPROM.write(3, (hh/100)%10);
EEPROM.write(4, (hh/1000)%10);
}
void hh_read(){
hh=EEPROM.read(4)*1000+EEPROM.read(3)*100+EEPROM.read(2)*10+EEPROM.read(1);
}
void mm_write(){ 
    Serial.println(mm);
EEPROM.write(5,  mm%10);
EEPROM.write(6, (mm/10)%10);
EEPROM.write(7, (mm/100)%10);
EEPROM.write(8, (mm/1000)%10);
}
void mm_read(){
mm=EEPROM.read(8)*1000+EEPROM.read(7)*100+EEPROM.read(6)*10+EEPROM.read(5);
}

void ss_write(){ 
    Serial.println(ss);
EEPROM.write(9,  ss%10);
EEPROM.write(10, (ss/10)%10);
EEPROM.write(11, (ss/100)%10);
EEPROM.write(12, (ss/1000)%10);
}
void ss_read(){
ss=EEPROM.read(12)*1000+EEPROM.read(11)*100+EEPROM.read(10)*10+EEPROM.read(9);
}
