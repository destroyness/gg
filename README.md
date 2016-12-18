# gg
#include"U8glib.h"

#define buzzer_pin 6

#define buzzer_fre 6

#define crash_pin 10

int buttonState;

U8GLIB_SSD1306_128X64 u8g(U8G_I2C_OPT_NONE);

void draw()

{

int buttonState;

int n=0;

int h=0;

float m=0;

int a=0;

int d=0;

// 多定义几个变量备用……

for(int v=0;v<=64;v=v+5)

{

u8g.setFont(u8g_font_fixed_v0r);

u8g.drawStr(64,v,"*");

}//显示中间标准线

buttonState=digitalRead(crash_pin);

delay(10);

if(buttonState==0){

a=1;

}

if(a==1)

{

m=millis();

n=(m-h*701);//701为间隔时间

u8g.setFont(u8g_font_fixed_v0r);

u8g.setPrintPos(64+n,32);

u8g.print("x");

}

h=h+1;//标准间隔

}

void setup() {

pinMode(crash_pin,INPUT);

pinMode(buzzer_pin,OUTPUT);

Serial.begin(115200);

}

void loop() {

int n;

int buttonState;

int a;

int d;

u8g.firstPage();

do{

draw();

}while(u8g.nextPage());

digitalWrite(buzzer_pin,HIGH);

delay(1);

digitalWrite(buzzer_pin,LOW);

delay(500);//响铃

}
