#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11
#define LEDPIN 8          // pin donde conectas el LED
#define TEMP_LIMITE 25.0  // temperatura para prender el LED

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
  pinMode(LEDPIN, OUTPUT);
  digitalWrite(LEDPIN, LOW); // el LED empieza apagado
}

void loop() {
  delay(2000); // el DHT11 necesita al menos 2 seg entre lecturas

  float humedad = dht.readHumidity();
  float temperatura = dht.readTemperature(); // en Celsius por defecto

  if (isnan(humedad) || isnan(temperatura)) {
    Serial.println("Error al leer el sensor DHT11");
    return;
  }

  Serial.print("Humedad: ");
  Serial.print(humedad);
  Serial.print(" % | Temperatura: ");
  Serial.print(temperatura);
  Serial.print(" *C");

  // Control del LED
  if (temperatura > TEMP_LIMITE) {
    digitalWrite(LEDPIN, HIGH);
    Serial.println(" | LED: ENCENDIDO");
  } else {
    digitalWrite(LEDPIN, LOW);
    Serial.println(" | LED: APAGADO");
  }
}

