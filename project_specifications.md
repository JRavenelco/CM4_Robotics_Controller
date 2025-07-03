# CM4 Robotics Controller - Especificaciones del Proyecto

## 1. Configuración Global del Proyecto y la Placa
* **Nombre del Proyecto**: CM4_Robotics_Controller
* **Configuración de la Placa**:
  * **Dimensiones**: 65mm x 56mm, con la forma y los agujeros de montaje de la especificación Raspberry Pi HAT
  * **Capas**: 4 capas
  * **Apilamiento de Capas (Stackup)**:
    * F.Cu (Capa Superior, Señal)
    * In1.Cu (Capa Interna 1, Plano de Masa Sólido)
    * In2.Cu (Capa Interna 2, Plano de Potencia)
    * B.Cu (Capa Inferior, Señal)
  * **Reglas de Diseño (Mínimas)**:
    * Ancho de Pista Mínimo: 0.15mm (6 mil)
    * Aislamiento Mínimo (Clearance): 0.15mm (6 mil)
    * Diámetro Mínimo de Vía: 0.3mm
    * Diámetro Mínimo de Anillo de Vía (Annular Ring): 0.15mm

## 2. Estructura de Esquemáticos Jerárquicos
* **Hoja Raíz (Root Sheet)**: Muestra los bloques jerárquicos y las conexiones de alto nivel entre ellos
* **Power_Subsystem.kicad_sch**: Circuitos de alimentación con los tres reguladores buck
* **CM4_Subsystem.kicad_sch**: Conexiones del Compute Module 4
* **RP2040_Subsystem.kicad_sch**: Microcontrolador RP2040 y componentes asociados
* **Motor_Driver_Subsystem.kicad_sch**: Drivers TB6612FNG y conexiones a los conectores LPF2
* **Sensor_Subsystem.kicad_sch**: Sensores VL6180X y bus I2C
* **USB_Subsystem.kicad_sch**: Hub USB y conectores

## 3. Redes Principales
* **Alimentación**:
  * +12V_IN: Entrada de alimentación
  * +8V_MOT: Alimentación para motores
  * +5V_SYS: Alimentación principal del sistema
  * +3V3_SYS: Alimentación lógica
  * GND: Masa común

* **Comunicación**:
  * CM4_TX_RP2040_RX: UART desde CM4 a RP2040
  * CM4_RX_RP2040_TX: UART desde RP2040 a CM4
  * I2C_SENS_SDA: Línea de datos I2C para sensores
  * I2C_SENS_SCL: Línea de reloj I2C para sensores
  * USB_DP/USB_DN: Líneas diferenciales USB

## 4. Consideraciones de Diseño Críticas
* **Pares Diferenciales USB**: Impedancia controlada de 90Ω
* **Cristal RP2040**: Pistas cortas con anillo de guarda
* **QSPI Flash**: Longitudes similares para todas las líneas
* **Líneas de Motor**: Pistas anchas (>0.5mm) para manejar corriente
* **Planos de Potencia**: Separación adecuada entre dominios de potencia



## 5. Actualizaciones para la Versión 2 (V2)

### 5.1. Nuevos Componentes y Adaptaciones

*   **Conector USB Tipo-C para CM4**: Se reemplazará el conector USB existente por un conector USB Tipo-C para el CM4, permitiendo una conexión más moderna y versátil. Este conector debe soportar la funcionalidad de datos y alimentación.
*   **Adaptación para Disco NVMe**: Se incluirá un conector M.2 (Key M) para un disco de estado sólido NVMe, aprovechando la interfaz PCIe del CM4. Esto requerirá la adición de un subsistema PCIe/NVMe y la gestión de las señales de alta velocidad.
*   **Compatibilidad con Cámara OAK-D-Lite**: Se asegurará la compatibilidad con la cámara OAK-D-Lite. Esto implicará la provisión de alimentación adecuada y la conexión de datos (posiblemente a través de USB o PCIe, dependiendo de la interfaz de la cámara y el diseño).

### 5.2. Modificaciones en Subsistemas Existentes

*   **USB_Subsystem.kicad_sch**: Se actualizará para incorporar el conector USB Tipo-C. Esto puede implicar la adición de componentes para la negociación de potencia (Power Delivery) si se requiere, aunque inicialmente se enfocará en la conectividad de datos.
*   **CM4_Subsystem.kicad_sch**: Se revisará para asegurar que las conexiones PCIe del CM4 estén disponibles y correctamente enrutadas hacia el nuevo conector NVMe.

### 5.3. Nuevo Subsistema (PCIe/NVMe)

*   **PCIe_NVMe_Subsystem.kicad_sch**: Se creará una nueva hoja esquemática jerárquica para gestionar la interfaz PCIe del CM4 y el conector M.2 para el NVMe. Esto incluirá la adaptación de impedancia y el enrutamiento de las líneas diferenciales PCIe.

### 5.4. Consideraciones de Diseño Adicionales para V2

*   **Enrutamiento PCIe/NVMe**: Las líneas PCIe son de alta velocidad y requerirán un enrutamiento diferencial con impedancia controlada (generalmente 85Ω o 100Ω, a verificar con la especificación PCIe y el stackup de la PCB). Se deberá prestar especial atención a la igualdad de longitud y al acoplamiento.
*   **Alimentación NVMe**: Se deberá proporcionar la alimentación adecuada (generalmente 3.3V) al conector NVMe.
*   **Conectividad OAK-D-Lite**: Se definirán los pines y la interfaz (USB o PCIe) para la conexión de la cámara OAK-D-Lite, y se asegurará que las redes necesarias estén disponibles y enrutadas correctamente.

