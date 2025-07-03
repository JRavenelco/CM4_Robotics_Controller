# Guía de Enrutamiento Crítico para CM4 Robotics Controller

## Pares Diferenciales USB

El enrutamiento de los pares diferenciales USB es crítico para garantizar la integridad de la señal. Estos pares deben enrutarse con las siguientes consideraciones:

1. **Impedancia controlada**: 90Ω diferencial
2. **Longitud igualada**: Diferencia máxima de longitud <3.8mm
3. **Trazado paralelo**: Mantener los pares lo más paralelos posible
4. **Evitar vías**: Minimizar el uso de vías en estos pares
5. **Distancia a planos de masa**: Mantener una distancia constante al plano de masa

### Ruta recomendada:
- Desde el CM4 hasta el hub USB (USB2514B_Bi)
- Desde el hub USB hasta los conectores USB-A
- Desde el hub USB hasta el RP2040 para modo rpiboot

## Cristal y Circuito de Reloj

El enrutamiento del cristal para el RP2040 es crítico para la estabilidad del reloj:

1. **Pistas cortas**: Minimizar la longitud de las pistas entre el cristal y el RP2040
2. **Simetría**: Mantener las pistas lo más simétricas posible
3. **Anillo de guarda**: Rodear el área del cristal con un anillo de guarda conectado a GND
4. **Aislamiento**: Evitar rutas de señal cercanas al cristal
5. **Capacitores de carga**: Colocar los capacitores de carga lo más cerca posible del cristal

## Interfaz QSPI para Flash

La interfaz QSPI entre el RP2040 y la memoria flash requiere:

1. **Longitudes igualadas**: Todas las líneas QSPI deben tener longitudes similares
2. **Minimizar longitud**: Mantener las pistas lo más cortas posible
3. **Evitar cruces**: Minimizar cruces con otras señales
4. **Referencia a GND**: Mantener una referencia constante al plano de masa

## Líneas de Motor

Las salidas de los drivers de motor TB6612FNG a los conectores LPF2 deben:

1. **Usar pistas anchas**: >0.5mm para manejar la corriente del motor
2. **Minimizar longitud**: Reducir la resistencia de las pistas
3. **Considerar retorno de corriente**: Asegurar un buen camino de retorno a GND
4. **Separación de señales sensibles**: Mantener alejadas de señales sensibles como USB o cristal

## Planos de Potencia y Masa

### Plano de Masa (In1.Cu)
- Plano de GND sólido e ininterrumpido
- Evitar divisiones o cortes en el plano
- Asegurar buenas conexiones a todos los puntos de GND

### Planos de Potencia (In2.Cu)
- Polígonos de cobre para +5V_SYS y +3V3_SYS
- Pistas anchas (>1.5mm) para +8V_MOT
- Mantener separación adecuada entre diferentes dominios de potencia

## Consideraciones Generales

1. **Condensadores de desacoplamiento**: Colocar lo más cerca posible de los pines de alimentación
2. **Vías térmicas**: Usar múltiples vías para componentes de potencia
3. **Señales sensibles**: Mantener señales sensibles en la capa superior cuando sea posible
4. **Retorno de corriente**: Considerar los caminos de retorno de corriente para todas las señales
5. **Integridad de señal**: Evitar ángulos de 90° en pistas críticas

## Prioridades de Enrutamiento

1. Pares diferenciales USB
2. Cristal y circuito de reloj
3. Interfaz QSPI
4. Líneas de alimentación principales
5. Líneas de motor
6. Señales de control
7. Resto de señales

## Verificación Post-Enrutamiento

Después del enrutamiento, verificar:

1. Cumplimiento de reglas de diseño (DRC)
2. Longitudes igualadas en pares diferenciales
3. Integridad de los planos de masa y potencia
4. Separación adecuada entre señales críticas
5. Conexiones térmicas adecuadas para componentes de potencia
