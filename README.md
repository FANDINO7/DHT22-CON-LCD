# Practica con un sensor DHT22 en una placa de desarrollo ESP32 y un LCD

**Introducción**
Descripción: La ESP32 la utilizamos en un entorno de adquision de datos, en esta practica ocuparemos un sensor DHT22 para adquirir temperatura y humedad del entorno, como tambien un LCD de 12c para visualizar los datos opotenidos, todo siendo simulado en una pagina llamda WOKWI

**MaterialU Herramientas**
Para realizar esta practica necesitas lo siguiente:
-1WOKWI
-Tarjeta ESP32
-Sensor DHT22
-LCD (16x2) 
**Requisitos previos**
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

**Instrucciones**
1.-Abrir la terminal de programación y colocar la siguente codigo 


```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("DIPLOMADO V");
  lcd.setCursor(2, 1);
  lcd.print("Mecatronica");
  delay(2000);

  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("ALBERTO FANDINO ");
  lcd.setCursor(2, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(2, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(2000);
}
```

**RESULTADOS**


![]()
