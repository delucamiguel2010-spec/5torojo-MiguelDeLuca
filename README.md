# 5torojo-MiguelDeLuca
Pensamiento computacional 
Clase1 verificación de git hub
clase 16/10
Paso 1
Problema: indicador de puerta abierta o cerrada
Paso2
Problema: En muchos hogares, oficinas o locales comerciales, es común dejar puertas,
portones o casilleros mal cerrados por descuido, lo que puede comprometer la seguridad,
dejar escapar la climatización o dejar objetos expuestos. A simple vista, a veces no es fácil
notar el estado exacto desde la distancia.
Beneficiario: Propietarios de viviendas, encargados de seguridad, o cualquier persona que
necesite verificar de manera rápida y visual el estado de acceso a una habitación o
depósito.
Solucion: El prototipo funcionará como un panel de control visual. Mediante un interruptor o
botón que simula el sensor de la puerta, encendera una luz roja cuando este abierta.
Circuit design Incredible Snaget-Kup - Tinkercad
// Configuración: se ejecuta una vez al iniciar
void setup() {
  pinMode(LED_BUILTIN, OUTPUT); // Configura el pin del LED integrado como salida
}
 
// Bucle principal: se repite infinitamente
void loop() {
  digitalWrite(LED_BUILTIN, HIGH); // Enciende el LED
  delay(1000);                     // Espera 1 segundo (1000 milisegundos)
  digitalWrite(LED_BUILTIN, LOW);  // Apaga el LED
  delay(1000);                     // Espera 1 segundo
}
