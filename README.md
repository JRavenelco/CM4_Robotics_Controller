# README - CM4 Robotics Controller

## Descripción del Proyecto

El CM4 Robotics Controller es una tarjeta portadora para el Raspberry Pi Compute Module 4, diseñada específicamente para aplicaciones robóticas. Esta placa integra un microcontrolador RP2040, drivers de motor, sensores de distancia y un hub USB, todo en un factor de forma compatible con la especificación Raspberry Pi HAT.

## Características Principales

- **Dimensiones**: 65mm x 56mm, siguiendo la especificación Raspberry Pi HAT
- **Diseño de 4 capas** para óptimo rendimiento y separación de señales
- **Soporte para Raspberry Pi Compute Module 4**
- **Microcontrolador RP2040** para control en tiempo real
- **Drivers de motor TB6612FNG** para control de hasta 4 motores
- **Sensores de distancia VL6180X** para detección de obstáculos
- **Hub USB de 4 puertos** para expansión de periféricos
- **Reguladores de voltaje** para 8V, 5V y 3.3V

## Estructura del Proyecto

El proyecto está organizado en la siguiente estructura:

```
CM4_Robotics_Controller/
├── CM4_Robotics_Controller.kicad_sch       # Esquemático principal
├── CM4_Robotics_Controller.kicad_pcb       # Layout PCB
├── schematics/                             # Esquemáticos jerárquicos
│   ├── Power_Subsystem.kicad_sch           # Subsistema de alimentación
│   ├── CM4_Subsystem.kicad_sch             # Subsistema del Compute Module 4
│   ├── RP2040_Subsystem.kicad_sch          # Subsistema del microcontrolador RP2040
│   ├── Motor_Driver_Subsystem.kicad_sch    # Subsistema de drivers de motor
│   ├── Sensor_Subsystem.kicad_sch          # Subsistema de sensores
│   └── USB_Subsystem.kicad_sch             # Subsistema USB
├── lib_symbols/                            # Bibliotecas de símbolos
│   └── custom/                             # Símbolos personalizados
├── lib_footprints/                         # Bibliotecas de footprints
│   ├── custom/                             # Footprints personalizados
│   └── cm4io_official/                     # Footprints oficiales del CM4
├── project_specifications.md               # Especificaciones detalladas del proyecto
├── netlist_generation.md                   # Guía para generación de netlist
├── pcb_layout_configuration.md             # Configuración del layout PCB
├── critical_routing_guide.md               # Guía de enrutamiento crítico
├── fabrication_files_guide.md              # Guía para generación de archivos de fabricación
└── README.md                               # Este archivo
```

## Documentación Técnica

El proyecto incluye la siguiente documentación técnica:

1. **project_specifications.md**: Especificaciones detalladas del proyecto, incluyendo requisitos eléctricos y mecánicos.
2. **netlist_generation.md**: Guía para la generación de la netlist completa del sistema.
3. **pcb_layout_configuration.md**: Configuración del layout PCB, incluyendo stackup de capas y reglas de diseño.
4. **critical_routing_guide.md**: Guía para el enrutamiento crítico de señales como USB, cristal y líneas de motor.
5. **fabrication_files_guide.md**: Guía para la generación de archivos de fabricación (Gerber, NC Drill, BOM, etc.).

## Subsistemas

### Subsistema de Alimentación
Implementa tres reguladores buck para generar +8V_MOT, +5V_SYS y +3V3_SYS a partir de la entrada de +12V.

### Subsistema CM4
Conectores y circuitos asociados para el Raspberry Pi Compute Module 4.

### Subsistema RP2040
Microcontrolador RP2040 con cristal de 12MHz y memoria flash QSPI de 16MB.

### Subsistema de Drivers de Motor
Cuatro drivers TB6612FNG para controlar hasta 4 motores DC, con conectores LPF2.

### Subsistema de Sensores
Cuatro sensores de distancia VL6180X conectados al bus I2C con pines de habilitación individuales.

### Subsistema USB
Hub USB de 4 puertos conectado al CM4, con tres puertos externos y uno interno para el RP2040.

## Reglas de Diseño

- **Ancho de Pista Mínimo**: 0.15mm (6 mil)
- **Aislamiento Mínimo**: 0.15mm (6 mil)
- **Diámetro Mínimo de Vía**: 0.3mm
- **Diámetro Mínimo de Anillo de Vía**: 0.15mm

## Consideraciones de Fabricación

Para la fabricación de esta placa, se recomienda:

1. Fabricante con capacidad para PCB de 4 capas
2. Acabado de superficie ENIG para mejor soldabilidad
3. Grosor de PCB estándar de 1.6mm
4. Máscara de soldadura verde o negra
5. Serigrafía blanca

## Próximos Pasos

Para completar el proyecto:

1. Finalizar el enrutamiento detallado siguiendo la guía de enrutamiento crítico
2. Generar los archivos de fabricación según la guía correspondiente
3. Verificar el diseño con DRC (Design Rule Check)
4. Generar el modelo 3D para verificación visual
5. Preparar los archivos para fabricación y ensamblaje

## Licencia

Este proyecto está disponible bajo licencia MIT.

## Autor

Desarrollado por Manus AI, 2025.
