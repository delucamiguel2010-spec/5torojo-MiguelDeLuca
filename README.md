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


# Actividades de Logica y Algoritmos

## Actividad 23/10

---

### Centro de Atencion para Estudiantes

#### 1. Descomposicion en subproblemas

* **Llegada y registro:** Capturar los datos iniciales del estudiante (identificacion, tipo de tramite y si presenta alguna condicion de prioridad).
* **Gestion de prioridades y colas:** Organizar a los estudiantes en estructuras de datos adecuadas (cola regular para atencion en orden de llegada y cola prioritaria para casos especiales).
* **Atencion en ventanilla:** Asignar el turno libre al siguiente estudiante siguiendo la jerarquia de colas y realizar el tramite correspondiente.
* **Cierre y estadisticas:** Finalizar la atencion registrando metricas de desempeno (tiempos de espera, cantidad de personas atendidas y reportes diarios).

#### 2. Datos necesarios para representar a cada estudiante

* `id_estudiante` (Texto o entero: Numero de identificacion o carnet).
* `tipo_tramite` (Entero/Texto: 1 = Entrega de documentos, 2 = Solicitud de constancia, 3 = Consulta general).
* `hora_llegada` (Marca de tiempo: Hora exacta de ingreso al centro para mantener el orden FIFO).
* `es_prioritario` (Booleano: Verdadero / Falso segun condiciones especiales como movilidad reducida o emergencias).
* `tiempo_estimado` (Entero: Minutos aproximados de duracion segun el tipo de tramite).

#### 3. Algoritmo en pseudocodigo

```text
Inicio
    Definir cola_regular como Cola vacia
    Definir cola_prioritaria como Cola vacia
    
    Mientras el centro de este abierto Hacer
        Si llega_estudiante() Entonces
            Leer datos (id_estudiante, tipo_tramite, es_prioritario)
            Si es_prioritario == Verdadero Entonces
                Agregar_a_cola(cola_prioritaria, estudiante)
            Sino
                Agregar_a_cola(cola_regular, estudiante)
            FinSi
        FinSi
        
        Si ventanilla_disponible() Y (no_vacia(cola_prioritaria) O no_vacia(cola_regular)) Entonces
            Si no_vacia(cola_prioritaria) Entonces
                estudiante_actual = extraer(cola_prioritaria)
            Sino
                estudiante_actual = extraer(cola_regular)
            FinSi
            Atender(estudiante_actual)
        FinSi
    FinMientras
    
    Mostrar reporte_del_dia()
Fin

```

#### 4. Criterio de prioridad elegido y justificacion

* **Criterio:** Atencion mixta (Atencion preferencial para casos de prioridad + Orden FIFO estricto para el resto).
* **Justificacion:** Mantiene la equidad y el respeto por el orden de llegada de la mayoria de los estudiantes, garantizando a su vez una respuesta rapida ante emergencias o necesidades especiales sin saturar la ventanilla unica.

---

### Ruta del Autobus Escolar

#### 1. Representacion de paradas y distancias

Se representan 6 paradas (P1 a P6) y la Escuela (E) mediante la siguiente tabla de distancias y carga de estudiantes:

| Parada | Estudiantes | Conexiones y distancias (km) |
| --- | --- | --- |
| **Parada 1 (P1)** | 4 | P1 hacia P2 (2 km), P1 hacia P3 (5 km) |
| **Parada 2 (P2)** | 6 | P2 hacia P3 (3 km), P2 hacia P5 (6 km) |
| **Parada 3 (P3)** | 3 | P3 hacia P4 (2 km), P3 hacia P6 (7 km) |
| **Parada 4 (P4)** | 5 | P4 hacia P5 (4 km), P4 hacia P6 (3 km) |
| **Parada 5 (P5)** | 2 | P5 hacia P6 (2 km), P5 hacia Escuela (5 km) |
| **Parada 6 (P6)** | 4 | P6 hacia Escuela (3 km) |

#### 2. Algoritmo paso a paso para construir la ruta

1. **Inicio:** Salir desde la ubicacion inicial hacia la primera parada con estudiantes.
2. **Evaluacion:** Desde la posicion actual, evaluar la distancia hacia todas las paradas pendientes por visitar.
3. **Seleccion:** Elegir la parada no visitada que represente la menor distancia recorrida (Estrategia del vecino mas cercano).
4. **Recoleccion:** Avanzar a la parada seleccionada, embarcar a los estudiantes y marcar la parada como completada.
5. **Cierre:** Repetir los pasos 2 a 4 hasta completar las 6 paradas y finalizar el trayecto en la Escuela.

#### 3. Aplicacion del algoritmo y ruta propuesta

* **Secuencia de la ruta:** P1 -> P2 -> P3 -> P4 -> P5 -> P6 -> Escuela
* **Total de estudiantes recogidos:** 4 + 6 + 3 + 5 + 2 + 4 = 24 estudiantes
* **Distancia total recorrida:** 2 + 2 + 3 + 2 + 4 + 2 + 3 = 18 km

#### 4. Comparacion con ruta alternativa

* **Ruta Alternativa B:** P6 -> P5 -> P4 -> P3 -> P2 -> P1 -> Escuela
* **Distancia total de la Alternativa B:** 21 km
* **Conclusion:** La Ruta Propuesta es optima bajo el criterio de menor distancia recorrida (18 km frente a 21 km), reduciendo el consumo de combustible y el tiempo total en transito.

---

### Correccion de Pseudocodigo (Promedio de Notas)

#### 1. Errores o limitaciones identificados

* **Error matematico en el calculo:** El codigo original realizaba la suma de las notas (nota1 + nota2 + nota3), pero no dividia el resultado entre 3, almacenando la suma total en lugar del promedio.
* **Ausencia de validacion de entradas:** No verificado si los valores ingresados se encontraban en un rango de notas valido (por ejemplo, entre 0 y 100).
* **Falta de salida informativa:** No mostraba al usuario el valor numerico obtenido en la variable promedio.

#### 2 y 3. Pseudocodigo corregido con validacion (0 a 100)

```text
Inicio
    Escribir "Ingrese la nota 1 (0 a 100):"
    Leer nota1
    Escribir "Ingrese la nota 2 (0 a 100):"
    Leer nota2
    Escribir "Ingrese la nota 3 (0 a 100):"
    Leer nota3
    
    Si (nota1 >= 0 Y nota1 <= 100) Y (nota2 >= 0 Y nota2 <= 100) Y (nota3 >= 0 Y nota3 <= 100) Entonces
        
        promedio = (nota1 + nota2 + nota3) / 3
        
        Escribir "El promedio obtenido es: ", promedio
        
        Si promedio >= 60 Entonces
            Escribir "Estado: Aprueba"
        SiNo
            Escribir "Estado: No aprueba"
        FinSi
        
    SiNo
        Escribir "Error: Una o mas notas ingresadas estan fuera del rango permitido (0 a 100)."
    FinSi
Fin

```

#### 4. Mejora adicional propuesta

Se incorpora un estado intermedio de recuperacion para estudiantes con promedio entre 50 y 59 puntos:

```text
Si promedio >= 60 Entonces
    Escribir "Estado: Aprueba"
SinoSi promedio >= 50 Y promedio < 60 Entonces
    Escribir "Estado: Requiere prueba de recuperacion"
SiNo
    Escribir "Estado: No aprueba"
FinSi

```

---

## Actividad 02/10

### Tabla de Datos

| Cantidad de arepas (n) | Precio total (P) |
| --- | --- |
| 1 | 10 |
| 2 | 18 |
| 3 | 24 |
| 4 | 28 |
| 5 | 30 |

---

### 1. Patron del precio e incremento por unidad

Se calcula la variacion del precio total por cada unidad adicional agregada:

* De 1 a 2 arepas: 18 - 10 = +8 USD
* De 2 a 3 arepas: 24 - 18 = +6 USD
* De 3 a 4 arepas: 28 - 24 = +4 USD
* De 4 a 5 arepas: 30 - 28 = +2 USD

**Analisis del patron:** El costo marginal por cada arepa adicional se reduce en 2 unidades de forma constante respecto al incremento anterior.

---

### 2. Formula matematica (n vs P)

Dado que las segundas diferencias son constantes (-2), el modelo corresponde a una funcion cuadratica:

P(n) = A*n^2 + B*n + C

Como P(0) = 0, C = 0. Resolviendo el sistema con los puntos (1, 10) y (2, 18):

1. A(1)^2 + B(1) = 10 -> A + B = 10
2. A(2)^2 + B(2) = 18 -> 4A + 2B = 18

Restando 2 por (A + B = 10) a la segunda ecuacion:
2A = -2 -> A = -1
-1 + B = 10 -> B = 11

**Formula resultante:**

P(n) = -n^2 + 11n  (o expresada como P(n) = n(11 - n))

---

### 3. Prediccion para 10 arepas

Sustituyendo n = 10 en la formula obtenida:

P(10) = -(10)^2 + 11(10)
P(10) = -100 + 110
P(10) = 10

El precio calculado para 10 arepas bajo el modelo matematico es de 10.

---

### 4. Abstraccion y formula general

Definiendo a como el precio de la primera unidad (a = 10) y d como la reduccion del incremento por unidad (d = 2), el precio total P(n) para cualquier cantidad n se expresa como:

P(n) = n * [ a - (d / 2) * (n - 1) ]

Para el caso particular donde d = 2:

P(n) = n * (a + 1 - n)

---

### 5. Reflexion

* **Razon de la variacion en el incremento:** Responde al principio de economias de escala y estrategias comerciales de descuento por volumen, incentivando a mayor consumo reduciendo el costo marginal de cada unidad adicional.
* **Impacto ante un cambio de patron:** Si el incremento fuera lineal y constante (P(n) = 10n), no existiria un incentivo economico por compra al mayor. Por otro lado, la continuidad indefinida de un patron decreciente genera inconsistencias numericas a partir de ciertos volumenes, haciendo necesaria la fijacion de un costo minimo por unidad en entornos reales.
