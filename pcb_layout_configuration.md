# Configuración del Layout PCB para CM4 Robotics Controller

## Dimensiones y Forma
- Dimensiones: 65mm x 56mm
- Forma: Siguiendo la especificación Raspberry Pi HAT
- Agujeros de montaje: Según especificación Raspberry Pi HAT

## Stackup de 4 Capas
1. **F.Cu (Capa Superior)**: Señales
   - Uso principal: Señales de alta velocidad, componentes SMD
   - Grosor de cobre: 35μm (1oz)

2. **In1.Cu (Capa Interna 1)**: Plano de Masa Sólido
   - Uso principal: Plano GND ininterrumpido
   - Grosor de cobre: 35μm (1oz)

3. **In2.Cu (Capa Interna 2)**: Plano de Potencia
   - Uso principal: Polígonos para +5V_SYS y +3V3_SYS
   - Pistas anchas para +8V_MOT (>1.5mm)
   - Grosor de cobre: 35μm (1oz)

4. **B.Cu (Capa Inferior)**: Señales
   - Uso principal: Señales generales, componentes THT
   - Grosor de cobre: 35μm (1oz)

## Reglas de Diseño
- Ancho de Pista Mínimo: 0.15mm (6 mil)
- Aislamiento Mínimo (Clearance): 0.15mm (6 mil)
- Diámetro Mínimo de Vía: 0.3mm
- Diámetro Mínimo de Anillo de Vía (Annular Ring): 0.15mm

## Reglas de Enrutamiento Críticas

### Par Diferencial USB
- Redes: USB_DP y USB_DN
- Impedancia: 90Ω diferencial
- Diferencia máxima de longitud: <3.8mm
- Configurar clase de red específica para este par

### Cristal
- Pistas desde X_RP2040 a los pines del RP2040 con la menor longitud posible
- Rodear esta área con un anillo de guarda de masa

### QSPI
- Pistas entre el RP2040 y la memoria flash con longitudes similares
- Mantener lo más cortas posible

### Líneas de Motor
- Pistas anchas (>0.5mm) para las salidas de los drivers TB6612FNG a los conectores LPF2

## Colocación de Componentes

### Prioridades de Colocación
1. **Conectores CM4**: Centrados en la placa
2. **Componentes de Potencia**: Agrupados y alejados de la antena del CM4
3. **RP2040, Flash y Cristal**: Muy próximos entre sí
4. **Sensores VL6180X**: Distribuidos en los bordes de la placa
5. **Conectores USB**: En un borde accesible de la placa
6. **Conectores LPF2**: En bordes accesibles para conexión de motores

### Consideraciones Especiales
- Condensadores de desacoplamiento cerca de los pines de alimentación de su respectivo IC
- Mantener las pistas de cristal lo más cortas posible
- Asegurar que los componentes no interfieran con los agujeros de montaje
- Considerar el flujo de corriente para los componentes de potencia

## Zonas de Cobre
- Plano de GND sólido en In1.Cu
- Polígonos de cobre para +5V_SYS y +3V3_SYS en In2.Cu
- Pistas anchas (>1.5mm) para +8V_MOT en In2.Cu

## Próximos Pasos
1. Importar la netlist en el editor PCB
2. Configurar el stackup y reglas de diseño
3. Definir el contorno de la placa según especificación Raspberry Pi HAT
4. Colocar componentes siguiendo las prioridades establecidas
5. Proceder con el enrutamiento crítico



## 5. Modificaciones del Layout de PCB para la Versión 2 (V2)

Debido a las limitaciones en la manipulación programática directa de los archivos `.kicad_pcb` para la adición y conexión de footprints complejos, las siguientes modificaciones deben realizarse manualmente en KiCad.

### 5.1. Integración del Conector USB Tipo-C

El conector USB Tipo-C para el CM4 debe ser añadido y conectado en el layout de la PCB. Este conector reemplazará la funcionalidad de los conectores USB-A existentes o se añadirá como un nuevo puerto principal.

**Pasos para la Integración Manual en KiCad:**

1.  **Abrir el Proyecto en Pcbnew**: Abra el archivo `CM4_Robotics_Controller.kicad_pcb` en el Editor de Layout de PCB de KiCad (Pcbnew).
2.  **Añadir el Footprint del Conector USB Tipo-C**: 
    -   Vaya a `Herramientas > Añadir Footprint` (o presione `A`).
    -   Busque un footprint adecuado para un conector USB Tipo-C de montaje superficial (SMD) que soporte USB 2.0. Ejemplos de footprints comunes pueden ser `Connector_USB:USB_C_Receptacle_USB2.0` o similar, dependiendo de las bibliotecas disponibles. Si no encuentra uno adecuado, deberá importar o crear un footprint personalizado.
    -   Coloque el footprint en una ubicación apropiada en el borde de la placa, considerando la accesibilidad y el enrutamiento.
3.  **Conectar las Redes**: Una vez colocado el footprint, deberá conectar sus pines a las redes correspondientes:
    -   **VBUS**: Conectar a la red de alimentación de +5V (probablemente `+5V_SYS`).
    -   **GND**: Conectar a la red de masa (`GND`).
    -   **D+ (Data Plus)**: Conectar a la red `USB_DP` proveniente del CM4.
    -   **D- (Data Minus)**: Conectar a la red `USB_DM` proveniente del CM4.
    -   **CC1/CC2 (Configuration Channel)**: Estos pines son cruciales para la detección de la orientación del cable y la negociación de potencia. Para una implementación básica de USB 2.0, se suelen conectar a tierra a través de resistencias pull-down (5.1kΩ) para indicar que es un dispositivo DFP (Downstream Facing Port) o UFP (Upstream Facing Port) o simplemente dejarlos flotando si solo se usa para datos y la negociación de potencia se maneja externamente. Consulte la hoja de datos del conector USB-C específico y las guías de diseño de USB-C para la configuración correcta.
    -   **SBU1/SBU2 (Sideband Use)**: Para USB 2.0, estos pines suelen dejarse sin conectar o se usan para funciones alternativas si el conector soporta modos alternativos (Alt Modes), lo cual no es el caso para una simple adaptación a CM4.
    -   **Shield**: Conectar a la red de masa (`GND`) a través de un punto de conexión a tierra cercano al conector.
4.  **Enrutamiento**: Enrute las pistas de datos (D+ y D-) como un par diferencial, manteniendo la impedancia controlada (90Ω) y la igualdad de longitud. Las pistas de alimentación (VBUS y GND) deben ser lo suficientemente anchas para manejar la corriente esperada.

### 5.2. Adaptación para Disco NVMe (Conector M.2 Key M)

La integración de un conector M.2 Key M para un disco NVMe requiere la conexión de las líneas PCIe del CM4 a este conector. Esto es crítico debido a las altas velocidades de las señales PCIe.

**Pasos para la Integración Manual en KiCad:**

1.  **Abrir el Proyecto en Pcbnew**: Asegúrese de tener el archivo `CM4_Robotics_Controller.kicad_pcb` abierto.
2.  **Añadir el Footprint del Conector M.2 Key M**: 
    -   Vaya a `Herramientas > Añadir Footprint` (o presione `A`).
    -   Busque un footprint para un conector M.2 Key M (por ejemplo, `Connector_M.2:M.2_NGFF_A-E_2x34_P0.5mm_Vertical` o similar, asegurándose de que sea Key M). Si no encuentra uno, deberá importarlo o crearlo.
    -   Coloque el footprint en una ubicación adecuada en la PCB, considerando el espacio para el módulo NVMe y la facilidad de enrutamiento de las líneas PCIe.
3.  **Conectar las Redes PCIe**: Conecte los pines del conector M.2 a las redes PCIe correspondientes del CM4. Las redes críticas son:
    -   **PETp0/PETn0 (PCIe Transmit Pair 0)**: Conectar a las redes `PCIE_TX_P` y `PCIE_TX_N` del CM4.
    -   **PERp0/PERn0 (PCIe Receive Pair 0)**: Conectar a las redes `PCIE_RX_P` y `PCIE_RX_N` del CM4.
    -   **CLKp/CLKn (PCIe Clock Pair)**: Conectar a las redes `PCIE_CLK_P` y `PCIE_CLK_N` del CM4.
    -   **3.3V**: Conectar a la red de alimentación de +3.3V (probablemente `+3V3_SYS`).
    -   **GND**: Conectar a la red de masa (`GND`).
    -   Otros pines (como PERST#, WAKE#, CLKREQ#, etc.) deben conectarse según la especificación PCIe y los requisitos del CM4.
4.  **Enrutamiento Crítico de PCIe**: El enrutamiento de las líneas PCIe es la parte más desafiante y crítica:
    -   **Pares Diferenciales**: Enrute `PETp0/PETn0`, `PERp0/PERn0` y `CLKp/CLKn` como pares diferenciales. Configure una clase de red específica para PCIe con una impedancia controlada (generalmente 85Ω o 100Ω, consulte la hoja de datos del CM4 y las guías de diseño de PCIe para el valor exacto y el espaciado/ancho de pista).
    -   **Igualdad de Longitud**: Asegure que las longitudes de las pistas dentro de cada par diferencial sean lo más iguales posible. Utilice herramientas de ajuste de longitud (length tuning) en KiCad.
    -   **Acoplamiento**: Mantenga un acoplamiento estrecho entre las pistas de cada par diferencial y entre los pares para minimizar la diafonía.
    -   **Vías**: Minimice el uso de vías en los pares diferenciales y, si son necesarias, asegúrese de que estén acopladas y compensadas adecuadamente.
    -   **Planos de Referencia**: Asegure que haya un plano de masa sólido de referencia debajo de las pistas PCIe para mantener la impedancia constante.

### 5.3. Consideraciones para la Cámara OAK-D-Lite

La compatibilidad con la cámara OAK-D-Lite se basa en las interfaces USB o PCIe ya provistas. No se requiere un footprint o enrutamiento adicional específico para la cámara en la PCB, más allá de asegurar que los puertos USB Tipo-C o el conector NVMe estén correctamente implementados.

-   Si la OAK-D-Lite se conecta vía USB, utilizará el puerto USB Tipo-C implementado.
-   Si se conecta vía PCIe (a través de un adaptador M.2 a OAK-D-Lite), utilizará el conector NVMe.

**Verificación**: Asegúrese de que las redes de alimentación (+5V_SYS, +3V3_SYS) y GND estén disponibles y sean robustas para soportar el consumo de energía de la cámara si se conecta directamente a la placa.

Una vez que haya realizado estas modificaciones en KiCad, podrá generar la netlist actualizada y proceder con el enrutamiento completo de la placa.

