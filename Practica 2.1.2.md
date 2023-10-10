# Depto de Sistemas y Computación
# Ing. En Sistemas Computacionales

![](Sistemas.png)

# SISTEMAS PROGRAMABLES 23a

# OBJETIVO:

Practica De inicio es la básico de desplegar algo en pantalla en el OLED Display.

# CÓDIGO

import network
import urequests
import utime
from machine import Pin, I2C
import ssd1306
#Conectar a la red WiFi
def conectar_wifi(ssid, password):
    sta_if = network.WLAN(network.STA_IF)
    if not sta_if.isconnected():
        print('Conectándose a la red WiFi...')
        sta_if.active(True)
        sta_if.connect(ssid, password)
        while not sta_if.isconnected():
            pass
    print('Conexión WiFi exitosa')
    print('Dirección IP:', sta_if.ifconfig()[0])
#Obtener la hora desde un servicio de tiempo en línea
def obtener_hora():
    url = "http://worldtimeapi.org/api/ip"
    response = urequests.get(url)
    datos = response.json()
    return datos['datetime']
#Configurar el display OLED
def configurar_oled():
    i2c = I2C(0, sda=Pin(0), scl=Pin(1))
    oled = ssd1306.SSD1306_I2C(128, 64, i2c)
    return oled
#Mostrar la hora en la pantalla OLED
def mostrar_hora_en_oled(oled, hora):
    oled.fill(0)
    oled.text("Hora actual:", 0, 0)
    oled.text(hora, 0, 16)
    oled.show()
#Programa principal
def main():
    ssid = "TecNM-ITT-Docentes"
    password = "tecnm2022!"
    conectar_wifi(ssid, password)
    oled = configurar_oled()
    while True:
        hora = obtener_hora()
        print("Hora actual:", hora)
        mostrar_hora_en_oled(oled, hora)
        utime.sleep(60)  # Espera 60 segundos antes de actualizar nuevamente
if _name_ == '_main_':
    main()


# PRUEBAS

![](P2_1_1.png)

# CONCLUSIONES

Dentro de esta practica se aprendio lo basico del uso de un raspberryb pi pico w con un display OLED.
