#include <EEPROM.h>
#include <SoftwareSerial.h>
SoftwareSerial bt(0,2);
String inputs;

#define stop A0//0push
#define start A1//0push
#define on A2
#define off A3
#define Send A5//outpt waire
int value = A5; //moter reding waire
//newturn pins 4 7 10
int values=0,sete=0;

#define bling 10//mode
#define Relay1 6//mode led

#define bazar 8 //bazar
#define r2 9 //timer start send > A4
#define moter 11 //on relay man time
#define r1 11 //on relay man time
#define r3 12 //off relay
#define dipar 13 //dipar

int re1 = 0,re2 = 0,re3 = 0,time=0;

int Load = 0, Mode=0;
int de=0,count=0,mm=0,ss=0,hh=0,timer=0;

void setup() {
bt.begin(9600);
Serial.begin(9600);

digitalWrite(moter,LOW);
pinMode(dipar, OUTPUT);
pinMode(bazar, OUTPUT);
pinMode(moter, OUTPUT);

digitalWrite(moter,LOW);
pinMode(Relay1, OUTPUT);
pinMode(bling, OUTPUT);
pinMode(r1, OUTPUT);
pinMode(r2, OUTPUT);
pinMode(r3, OUTPUT);
pinMode(start, INPUT_PULLUP);
pinMode(stop, INPUT_PULLUP);
pinMode(Send, INPUT_PULLUP);

pinMode(off, INPUT_PULLUP);

pinMode(value, INPUT_PULLUP);
pinMode(on,INPUT_PULLUP);
delay(5000);
re1 = EEPROM.read(11);

re2 = EEPROM.read(12);
re3 = EEPROM.read(13);
digitalWrite(r1, re1);
digitalWrite(r2, re2);
digitalWrite(r3, re3);

if (EEPROM.read(0) == 0) {
} else {

de_write();
count_write();
values_write();
sete_write();
EEPROM.write(0, 0);
EEPROM.write(1, 1);
}
de_read();
count_read();
read_eeprom();
values_read();
sete_read();
}
void read_eeprom() {
Mode = EEPROM.read(1);
}
void loop() {

int value = analogRead(A5);
value = value -1;
value = value + sete;

if (digitalRead(stop) == 0) {
digitalWrite(r1,0);

    delay(300);
     
    digitalWrite(bling,LOW);
   digitalWrite(dipar,LOW); 
        digitalWrite(r3,0);
        EEPROM.write(13,0);
    
delay(200);
if (hh == 0) {
  hh = 1;
  Mode = !Mode;
  EEPROM.write(1, Mode);
  delay(100);
}
} else {
hh = 0;
}
if (Mode == 1) {

digitalWrite(Relay1, HIGH);
    //LOWshuru
    

      

       
    
    
     if(timer<60){timer=timer+1;
        if(timer<50){
        bt.print(value);  //send
        bt.print(";");  
        digitalWrite(dipar, HIGH);
        bt.print(timer); 
        bt.print(";"); 
      }
        if(timer==2){
           digitalWrite(r1,0);
           EEPROM.write(11,0); 
           digitalWrite(r3,0);
            EEPROM.write(12,0); 
                  
                
            }
        delay(500);
        if(timer==60){
           
        digitalWrite(dipar,LOW);      
          bt.print(value);  //send
           bt.print(";");  
         timer=58;   
        
      
      if (value<values) {
                
        if(time<20){time=time+1;
                    delay(200);
                 if(time==1) {
       digitalWrite(bazar, HIGH); 
                        
                    }
                    if(time==20){
       digitalWrite(bazar, LOW);  
                    }
                    }
        
                    delay(2000);
                                
                      
       digitalWrite(moter, HIGH);
        digitalWrite(r3,0);
        EEPROM.write(13,0); 
                   
        }
       else if(value<310){
digitalWrite(bazar, LOW);
digitalWrite(moter, LOW);
}

    else if(value<0){
   if(time<20){time=time+1;
                    delay(200);
                 if(time==1) {
       digitalWrite(bazar, HIGH); 
                        
                    }
                    if(time==20){
       digitalWrite(bazar, LOW);  
                    }
                    }
                     
digitalWrite(bazar, LOW);  
digitalWrite(moter,HIGH);
 
 }     
Serial.println(value);

 }
    }
    
    
    
        while (Serial.available())
{

delay(10);
char c = Serial.read();
  

inputs += c;
if (inputs.length() > 0) {
  Serial.println(inputs);
    if(inputs == "@") {
           values=values+1;      
           delay(200);
       
        values_write();
    for(int t=1;t<=5;t++){   
       delay(100);                         
       bt.print(values);
       bt.print(";");
}

        }
        
      
        else if(inputs == "&") {
          
          values=values-1;
  delay(200);
        values_write();
       for(int t=1;t<=5;t++){   
       delay(100);                         
       bt.print(values);
       bt.print(";");
}
}

        else if(inputs == "X") {
           sete=sete+1;
  
       for(int t=1;t<=5;t++){               
delay(100);
bt.print(sete);
bt.print(";");
}
Serial.println("+1 ");

        }
        
      
        else if(inputs == "x") {
          
       sete=sete-1;
  
        sete_write();
       for(int t=1;t<=5;t++){               
delay(100);
bt.print(sete);
bt.print(";");
}
}

        else if(inputs == "E") {
           digitalWrite(r1,0);
           EEPROM.write(11,0); 
        digitalWrite(bling,HIGH);
            
        }    
        else if(inputs == "S") {
          
       sete=0;
       values=10;
                    
        sete_write();
       values_write();   
                           
          for(int t=1;t<=10;t++){  
         delay(100);                        
       bt.print(values);
       bt.print(";");

     
       bt.print(sete);
       bt.print(";");
        }        
          
          
          
        }        
            
     
    inputs = "";
    
  }             

}      
    
               
//LOWpaste
}

else {

digitalWrite(Relay1, LOW);
    //highshuru
    
    
if (digitalRead(Send) == 0) {
  
  
        
digitalWrite(dipar, HIGH);
delay(400);
digitalWrite(dipar, LOW);
delay(400);
count = count + 1;
 count_write();         
   if(timer<60){timer=timer+1;
             if(timer==2)  {
               delay(100);
           digitalWrite(r1,0);
           digitalWrite(r3,0);   
    
                
            }
             
             bt.print(value);  //send
              bt.print(";");  
        
            
           if(timer<50){
        
        bt.print(timer); 
        bt.print(";"); 
      } 
        
     
        if(timer==60){
            digitalWrite(r1,0);
            digitalWrite(r3,0);    
             timer=58;       
             
               
                
           if (value<values) {
           
        if(time<20){time=time+1;
                    delay(200);
                 if(time==1) {
       digitalWrite(bazar, HIGH); 
                        
                    }
                    if(time==20){
       digitalWrite(bazar, LOW);  
                    }
                    }
        
          
       digitalWrite(moter, HIGH);
        digitalWrite(r3,0);
        EEPROM.write(13,0);    
        }
       else if(value<310){
     
                       
digitalWrite(bazar, LOW);
digitalWrite(moter, LOW);
                    
 }  
    else if(value<0){
  if(time<20){time=time+1;
                    delay(200);
                 if(time==1) {
       digitalWrite(bazar, HIGH); 
                        
                    }
                    if(time==20){
       digitalWrite(bazar, LOW);  
                    }
                    }
                          
digitalWrite(bazar, LOW);
digitalWrite(moter,HIGH);
 
 }      
  }
            
}
           

bt.print(count);  
bt.print(";");      
 
 
if (count > de) {
            
 digitalWrite(bling,HIGH);
                    
  count = 0;
   count_write();  
                
    digitalWrite(bazar, HIGH); 
            delay(1000);
   digitalWrite(r1, 1);//offrelay
   
   digitalWrite(r2, 0);
   
   digitalWrite(r3,0);
   
             
  digitalWrite(bazar, LOW);  
}
}

if(digitalRead(start)==0){
count=0;
count_write();
timer=0;
digitalWrite(bazar, HIGH);
delay(200);
//only on
digitalWrite(r1,0);

   digitalWrite(r2,1);
                
        
        
    
}

else{
    delay(200);
    digitalWrite(bazar,LOW); 
   
}
      
if(digitalRead(on)==0) {
 digitalWrite(bazar, HIGH);
       timer=0; 
    delay(200);
      
   count = 0;
   count_write();
       
   digitalWrite(r1,0);
   EEPROM.write(11,0);
   digitalWrite(r3,1);
   EEPROM.write(13,0);
   digitalWrite(r2,1);
   EEPROM.write(12,0);
     
   
        delay(1000);
   
   digitalWrite(bazar,LOW);
   digitalWrite(r3,0);
   EEPROM.write(13,0);
  
    }
if (digitalRead(off) == 0) {
digitalWrite(dipar, HIGH);
delay(200);
digitalWrite(dipar, LOW);
delay(200);

    digitalWrite(bazar, HIGH); 
         
                
        digitalWrite(r1, 1);
         EEPROM.write(11, 0);  
        digitalWrite(r2, 0);
         EEPROM.write(12,0); 
                
                
       

                delay(1000);
        
        digitalWrite(bazar, LOW);
                
            } 
//HIGHpaste
}

while (Serial.available())

{

delay(10);
char c = Serial.read();
  

inputs += c;
if (inputs.length() > 0) {
  Serial.println(inputs);
   if(inputs == "A") {
  
    digitalWrite(bazar, HIGH);
      timer=0;      
     count=0;  
     count_write();            
   digitalWrite(r1,0);
   
  digitalWrite(r2,1); //onrelay
              
    digitalWrite(r3,1);
             
            delay(2000);
         //only on
    digitalWrite(r3,0);
            
   
   
      delay(500);
    digitalWrite(bazar,LOW);        
  }
 
 else if(inputs == "a") {
    digitalWrite(bazar, HIGH);
   digitalWrite(r1,1);
     
    digitalWrite(r3,0);
      
   digitalWrite(r2,0); //onrelay time
                     
            delay(100);
         //only on
              
   
   
      delay(500);
    digitalWrite(bazar,LOW);         
        
        }     
        
               
               
  else if(inputs == "B") {
    
        
     digitalWrite(r2,1); //onrelay
     EEPROM.write(12,1);
        
              
            
        }   
        else if(inputs == "b") {
   
   
   digitalWrite(r2, 0);//onrelay
   
   EEPROM.write(12,0);  
   digitalWrite(r3,0); //onrelay          
   EEPROM.write(13,0);//TIMER on          
            
        }
        
        
        
        else if(inputs == "C") {
       digitalWrite(r1, 0);//offrelay
       EEPROM.write(11, 0);  
       digitalWrite(r2,1);
       EEPROM.write(12,1);     
       digitalWrite(r3,1); //onrelay
       EEPROM.write(13,1);//TIMER on
        
              
            
        }   
        
   else if(inputs == "c") { //onlyoff
   digitalWrite(r1,1);//offrelay
   EEPROM.write(11, 1);
   digitalWrite(r2,0);
   EEPROM.write(12,0);
   digitalWrite(r3,0);
   EEPROM.write(13,0);
            
        }   
     
    
        
        else if(inputs == "E") {
          
           digitalWrite(r1,0);
           EEPROM.write(11,0);   
            
        digitalWrite(bling,HIGH);
            
        }
        
        
        else if(inputs == "Y") {
           
digitalWrite(dipar, HIGH);
delay(200);
digitalWrite(dipar, LOW);
delay(200);
   if(mm<10){mm=mm+1;
            if(mm==10){
                     
   digitalWrite(bazar,HIGH);
                delay(500);
           
     digitalWrite(bazar,LOW);
                mm=0;
            }
            }
de=de +60;

   de_write();
   for(int t=1;t<=5;t++){
     delay(100);           
    bt.print(de);
    bt.print(";");
        
            }         
   Serial.println(de);

    Serial.println("+59 ");



            
        }
        
        else if(inputs == "y") {
          digitalWrite(dipar, HIGH);
       delay(200);
    digitalWrite(dipar, LOW);
delay(200);
 
 
if (de > 0) {
if(mm<10){mm=mm+1;
if(mm==10){

   digitalWrite(bazar,HIGH);
                delay(500);
           
     digitalWrite(bazar,LOW);
                mm=0;
            }
            }
       de=de-60;
    de_write();            
                
  for(int t=1;t<=5;t++){
    delay(100);                
    bt.print(de);
    bt.print(";");
        
            }        
        
       Serial.println(de);

        Serial.println("-60 ");

  

        }    
        }
        else if(inputs == "W"){
           de=60;
          de_write();
        for(int t=1;t<=5;t++){
        delay(100);        
       bt.print(de);
        bt.print(";");
         
            }    
        }
        
     else if(inputs == "@") {
           values=values+1;
  delay(200);
        values_write();
         for(int t=1;t<=5;t++){ 
            delay(100);    
       bt.print(values);
       bt.print(";");
       } 

            
        }
        
      
        else if(inputs == "&") {
          
          values=values-1;
         delay(200);
        values_write();
      for(int t=1;t<=5;t++){   
        delay(100);         
       bt.print(values);
       bt.print(";");
        }
        }    
        
        
        else if(inputs == "X") {
           sete=sete+1;

        sete_write();
      for(int t=1;t<=5;t++){ 
            delay(100); 
       bt.print(sete);
       bt.print(";");
        }        
        Serial.println("+1 ");


            
        }
        
      
        else if(inputs == "x") {
          
       sete=sete-1;
  
        sete_write();
        for(int t=1;t<=5;t++){   
          delay(100);       
       bt.print(sete);
       bt.print(";");
         } 
        }    
        
        else if(inputs == "S") {
          
       sete=0;
       values=10;
          
        sete_write();
       values_write();   
       for(int t=1;t<=10;t++){
       delay(100);         
       bt.print(sete);
       bt.print(";");   
       bt.print(values);
       bt.print(";");              
                
            }     
                      
          
          
        }        
        
     
    inputs = "";
    
  }             

} 
}

void de_write() {

EEPROM.write(2, de % 10);
EEPROM.write(3, (de / 10) % 10);
EEPROM.write(4, (de / 100) % 10);
EEPROM.write(5, (de / 1000) % 10);
}
void de_read() {
de = EEPROM.read(5) * 1000 + EEPROM.read(4) * 100 + EEPROM.read(3) * 10 + EEPROM.read(2);
}

void count_write() {

EEPROM.write(6, count % 10);
EEPROM.write(7, (count / 10) % 10);
EEPROM.write(8, (count / 100) % 10);
EEPROM.write(9, (count / 1000) % 10);
}
void count_read() {
count = EEPROM.read(9) * 1000 + EEPROM.read(8) * 100 + EEPROM.read(7) * 10 + EEPROM.read(6);
}

void values_write() {

EEPROM.write(15, values % 10);
EEPROM.write(16, (values / 10) % 10);
EEPROM.write(17, (values / 100) % 10);
EEPROM.write(18, (values / 1000) % 10);
}
void values_read() {
values = EEPROM.read(18) * 1000 + EEPROM.read(17) * 100 + EEPROM.read(16) * 10 + EEPROM.read(15);
}

void sete_write() {

EEPROM.write(19, sete % 10);
EEPROM.write(20, (sete / 10) % 10);
EEPROM.write(21, (sete / 100) % 10);
EEPROM.write(22, (sete / 1000) % 10);
}
void sete_read() {
sete = EEPROM.read(22) * 1000 + EEPROM.read(20) * 100 + EEPROM.read(21) * 10 + EEPROM.read(19);
}
