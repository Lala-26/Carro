#include<SoftwareSerial.h>                            //incluir libreria para utilizar los comandos del modulo bluetooth.

SoftwareSerial myBT(10,11);                           //Pin de conexión RX-->pin 11, TX-->pin 10.
char dato = 0;                                        //Declarar variable dato como tipo char para almacenar el caracter enviado.
int IN1 = 2;                        //Asignar pines de IN en las respectivas terminales del arduino.
int IN2 = 3;
int IN3 = 4;
int IN4 = 5;
int time=0;
int diagonal=500;
int lados=1000;

void setup(){
  Serial.begin(9600);                                 //Inicializar comunicación serial para ver y enviar los comandos AT(debe estar en 9600 baudios en el serial monitor)
  Serial.print("Monitor serial preparado.");          //Mensaje para confirmar comunicación serie.
  myBT.begin(9600);                                   //Inicializar velocidad de comunicación del modulo bluetooth. (Con modulo HC05 se maneja una comunicación de 38400 baudios, con HC06 se maneja una comunicación de 9600)
  pinMode(IN1,OUTPUT);                                //Configurar los pines del como salida para enviar la señal correspondiente al motor.
  pinMode(IN2,OUTPUT);
  pinMode(IN3,OUTPUT);
  pinMode(IN4,OUTPUT);
}

void loop(){
  if(myBT.available()){                               //Condición para verificar información en el monitor serial, si es verdadero almacena el caracter en la variable dato.
    dato = myBT.read();                               //Alamcenar el caracter enviado en la variable dato.
    delay(30);                                        //Tiempo para recepción de señal y almacenamiento de variable. 
    Serial.print(dato);     
                         
    if(dato =='a'){
      detener();
      delay(25);                                   
      arriba();
    }
    if(dato =='c'){
      detener();
      delay(20);
      char c = myBT.read();      
      myBT.print(c);
      abajo();
    }
    if(dato =='d'){
      char c = myBT.read();      
      myBT.print(c);
      izquierda();
    }
    if(dato =='e'){
      char c = myBT.read();      
      myBT.print(c);
      derecha();
    }
    if(dato=='b'){
      detener();
    }
  }
}
void abajo(){
  detener();
  digitalWrite(IN1,1);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN2,0);
  digitalWrite(IN3,1);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN4,0);
  delay(time);
}
void izquierda(){
  detener();
  digitalWrite(IN1,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN2,0);
  digitalWrite(IN3,1);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN4,0);
  delay(time);
}
void derecha(){
  detener();
  digitalWrite(IN3,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN4,0);
  digitalWrite(IN1,1);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN2,0);
  delay(time);
}
void arriba(){
  detener();
  digitalWrite(IN1,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN2,1);
  digitalWrite(IN3,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN4,1);
  delay(time);
}
void detener(){
  digitalWrite(IN1,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN2,0);
  digitalWrite(IN3,0);              //Enviar estado alto para realizar un giro en el motor A.
  digitalWrite(IN4,0);
}
