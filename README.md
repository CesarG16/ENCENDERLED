## CESAR AUGUSTO GONZALEZ INFANTE
## ENCENDIDO LED CON NODE RED
## Material Necesario

Para realizar esta practica se usaran los siguientes elementos:

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- RELAY
- [NODERED](http://localhost:1880/)



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <WiFi.h>
#include <PubSubClient.h>

const char* ssid = "Wokwi-GUEST";
const char* password = "";
const char* mqttServer = "52.29.234.128";
const int mqttPort = 1883;
const char* mqttUser = "CESARGONZALEZ";
const char* mqttPassword = "1234";
const char* mqttTopic = "LED";

WiFiClient espClient;
PubSubClient client(espClient);

int ledPin = 13; // Pin del LED

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqttServer, mqttPort);
  client.setCallback(callback);
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop();
}

void setup_wifi() {
  delay(10);
  Serial.println();
  Serial.print("Conectando a: ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("Conectado a la red WiFi");
}

void reconnect() {
  while (!client.connected()) {
    Serial.print("Intentando conexión MQTT...");
    if (client.connect("ESP32Client", mqttUser, mqttPassword)) {
      Serial.println("Conectado");
      client.subscribe(mqttTopic);
    } else {
      Serial.print("Error de conexión, rc=");
      Serial.print(client.state());
      Serial.println(" Intentando de nuevo en 5 segundos");
      delay(5000);
    }
  }
}

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Mensaje recibido: [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  if (strcmp(topic, mqttTopic) == 0) {
    if ((char)payload[0] == '1') {
      digitalWrite(ledPin, HIGH);
    } else {
      digitalWrite(ledPin, LOW);
    }
  }
}

```

2. Instalar las siguientes librerias:

- PubSubClient


### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
4. Abrir Simbolo de sistema como administrador tras instalar el programa node red y escribir  node-red en la terminal del sistema tras esto ir a un navegador web y escribir: (http://localhost:1880/) y estaremos en node red.

5. Juntar los elementos siguientes mostrados en la pantalla:

![](https://github.com/CesarG16/ENCENDERLED/blob/main/I1.png?raw=true)

6. Los elementos puestos son : mqtt in, json, function, gauge y chart.
7. Después abrir Dashboard en la esquina superior de la derecha como se ve en la siguiente imagen:

![](https://github.com/CesarG16/DHT22RED/blob/main/EJE4.png?raw=true)

8. Dar click en +tab.
9. Dar click en +group y añadir dos. 
10. De alli tanto en tab como en el grupo se les da en los botones de editar de cada uno y en la seccion de name se le asigna un nombre a cada uno.
![](https://github.com/CesarG16/ENCENDERLED/blob/main/I4.png?raw=true)

11. de alli se da click a cada uno de los elementos unidos anteriormente y se editan empezando por el primero, hasta el ultimo como se ven en las siguientes imágenes:

![](https://github.com/CesarG16/ENCENDERLED/blob/main/I2.png?raw=true)
![](https://github.com/CesarG16/ENCENDERLED/blob/main/I3.png?raw=true)


12. Tras esto se da en el boton rojo de arriba a la derecha que dice Deploy y cuando esté listo se le da en el siguiente boton que esta abajo de Deploy para que abra una nueva página y se visualice el resultado:

![](https://github.com/CesarG16/DHT22RED/blob/main/EJE12.png?raw=true)

## Resultados


Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen y en la página creada por node - red.

![](https://github.com/CesarG16/ENCENDERLED/blob/main/I5.png?raw=true)
![](https://github.com/CesarG16/ENCENDERLED/blob/main/I6.png?raw=true)



## Evidencias

[Página](https://wokwi.com/projects/367827749848573953)


# Créditos

Desarrollado por Ing. Cesar Augusto Gonzalez Infante

- [GitHub](https://github.com/CesarG16)