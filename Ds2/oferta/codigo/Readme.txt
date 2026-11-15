// ====== PINES Y CONFIGURACIÓN ======
const int PIN_DEMANDA = A0;
const int PIN_OFERTA  = A1;

bool enEscasez = false;

void setup() {
  // Inicializamos la comunicación serial con la PC
  Serial.begin(9600);
  Serial.println("Iniciando sistema local de Oferta y Demanda...");
}

void loop() {
  // Leemos los potenciómetros y mapeamos los valores de 10 a 90
  int demanda = map(analogRead(PIN_DEMANDA), 0, 1023, 10, 90);
  int oferta  = map(analogRead(PIN_OFERTA), 0, 1023, 10, 90);

  // Modelo lineal: demanda P = a - Q ; oferta P = Q - b
  int a = 100 + demanda;
  int b = oferta - 50;
  int precio = ((a - b) / 2) + 4;  // pesos por kilo

  // Imprimimos los valores calculados en el Monitor Serie
  Serial.print("Demanda: "); 
  Serial.print(demanda);
  Serial.print(" | Oferta: "); 
  Serial.print(oferta);
  Serial.print(" | Precio: $"); 
  Serial.println(precio);

  // Evaluamos si hay escasez (diferencia mayor o igual a 25)
  bool escasez = (demanda - oferta) >= 25;
  
  if (escasez && !enEscasez) {
    Serial.println("--> ¡ALERTA! Situación de escasez detectada.");
  } else if (!escasez && enEscasez) {
    Serial.println("--> Situación normalizada.");
  }
  
  enEscasez = escasez;
  
  // Pausa de medio segundo entre cada lectura
  delay(500);
}
