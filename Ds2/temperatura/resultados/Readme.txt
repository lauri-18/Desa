Control de LED según la temperatura con sensor DHT11
Reporte de práctica con Arduino

1. Resumen

En esta práctica se utiliza un Arduino junto con el sensor DHT11 para medir la temperatura y la humedad del ambiente. Los valores se muestran cada 2 segundos en el Monitor Serial. Además, se agregó un LED que funciona como indicador: se enciende cuando la temperatura es mayor a 25 °C y se apaga cuando es de 25 °C o menos.

2. Materiales

Cantidad	Material	Uso
1	Arduino UNO (o compatible)	Procesa la lectura y controla el LED
1	Sensor DHT11	Mide temperatura y humedad
1	LED (cualquier color)	Indicador de temperatura alta
1	Resistencia de 220 Ω	Limita la corriente del LED
1	Protoboard	Para armar el circuito
Varios	Cables jumper	Conexiones entre componentes
1	Cable USB	Alimentación y comunicación con la PC

3. Conexiones

Componente	Pin del componente	Conexión en Arduino
DHT11	VCC (+)	5V
DHT11	DATA (señal)	Pin digital 2
DHT11	GND (−)	GND
LED	Pata larga (+)	Pin digital 8 (a través de la resistencia de 220 Ω)
LED	Pata corta (−)	GND

4. Funcionamiento del código

Configuración (setup): se inicia la comunicación serial a 9600 baudios, se arranca el sensor DHT11 y se declara el pin 8 como salida para el LED, que empieza apagado.

Ciclo principal (loop): cada 2 segundos el Arduino lee la humedad y la temperatura. Si la lectura falla, muestra un mensaje de error y vuelve a intentar. Si la lectura es correcta, imprime los valores y compara la temperatura con el límite de 25 °C: si es mayor, enciende el LED (HIGH); si no, lo apaga (LOW). El estado del LED también se muestra en el Monitor Serial.

5. Resultado

Al cargar el programa y abrir el Monitor Serial (9600 baudios) se obtienen lecturas como las siguientes:

Humedad: 58.00 % | Temperatura: 24.00 *C | LED: APAGADO
Humedad: 57.00 % | Temperatura: 25.00 *C | LED: APAGADO
Humedad: 55.00 % | Temperatura: 26.00 *C | LED: ENCENDIDO
Humedad: 54.00 % | Temperatura: 27.00 *C | LED: ENCENDIDO

El sistema funcionó correctamente: con temperaturas de 25 °C o menos el LED permanece apagado, y al superar los 25 °C se enciende. Esto se puede comprobar acercando la mano o una fuente de calor al sensor.

6. Conclusión

Se logró leer la temperatura y humedad con el sensor DHT11 y usar ese dato para tomar una decisión en el Arduino, encendiendo un LED como alerta de temperatura alta. Este mismo principio se puede aplicar para activar un ventilador, un buzzer o un relevador cuando la temperatura rebase un límite.
