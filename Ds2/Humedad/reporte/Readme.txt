Reporte Técnico: Monitor de Humedad
Sistema de Control e Indicación con Arduino UNO R3

1. Funcionamiento del Sistema
El sistema evalúa continuamente la humedad del suelo leyendo una señal analógica en la entrada A0. Mapea la lectura bruta ($0\text{–}1023$) a una escala porcentual ($0\%\text{–}100\%$).

Cuando el valor calculado es inferior al 40% (Umbral), el controlador entra en estado de alerta TIERRA SECA, encendiendo el LED del Pin 13 y enviando un aviso vía puerto serie. Si la humedad es igual o mayor al umbral, permanece en estado normal TIERRA HÚMEDA con el LED apagado.

2. Materiales Requeridos
Cantidad	Componente	Función Principal
1	Arduino UNO R3	Procesamiento e interpretación de señal analógica.
1	Sensor de Humedad del Suelo	Medición analógica del grado de humedad (Pin A0).
1	Cable USB Tipo A a B	Carga de programa y comunicación serie a 9600 baudios.
3	Cables Jumper	Conexión de líneas de voltaje (5V), tierra (GND) y señal (A0).
1	LED Integrado (Pin 13)	Indicador visual de estado de alerta por sequía.
3. Esquema de Conexión
Sensor VCC → Arduino 5V
Sensor GND → Arduino GND
Sensor AOUT → Arduino A0
4. Procedimiento de Instalación
Conexión: Enlaza el sensor a los pines 5V, GND y A0 del Arduino UNO R3 según el esquema de alimentación y señal.
Calibración rápida: Mide los valores analógicos extremos usando el Monitor Serie (registra la lectura al aire como VALOR_SECO y sumergido en agua como VALOR_MOJADO).
Carga y prueba: Sube el código optimizado al Arduino mediante el IDE y monitorea las lecturas e indicación visual por el LED.
