# Lista de Tareas para el Proyecto CM4 Robotics Controller

- [X] **Paso 1: Analizar Requerimientos y Configurar Proyecto KiCad**
  - [X] Crear directorio principal del proyecto
  - [X] Documentar especificaciones globales
  - [X] Crear estructura de carpetas para bibliotecas y salidas

- [X] **Paso 2: Crear Estructura de Esquemáticos Jerárquicos**
  - [X] Crear archivo principal del proyecto KiCad
  - [X] Generar hoja raíz con bloques jerárquicos
  - [X] Crear archivos base para cada subsistema
  - [X] Definir conexiones de alto nivel entre subsistemas

- [X] **Paso 3: Definir Bibliotecas y Footprints Personalizados**
  - [X] Obtener footprints del CM4 de la documentación oficial
  - [X] Crear símbolos esquemáticos para componentes específicos
  - [X] Definir footprints personalizados para conectores LPF2
  - [X] Organizar bibliotecas para uso en el proyecto

- [ ] **Paso 4: Generar Esquemáticos y Netlist Completa**
  - [ ] Desarrollar esquemático del subsistema de alimentación
  - [ ] Desarrollar esquemático del subsistema CM4
  - [ ] Desarrollar esquemático del subsistema RP2040
  - [ ] Desarrollar esquemático del subsistema de control de motores
  - [ ] Desarrollar esquemático del subsistema de sensores
  - [ ] Desarrollar esquemático del subsistema USB
  - [ ] Generar netlist completa del proyecto

- [ ] **Paso 5: Crear Layout PCB con Stackup y Reglas**
  - [ ] Configurar stackup de 4 capas
  - [ ] Definir reglas de diseño según especificaciones
  - [ ] Importar netlist al PCB
  - [ ] Definir contorno de la placa según especificación Raspberry Pi HAT
  - [ ] Colocar componentes según directrices de diseño

- [ ] **Paso 6: Aplicar Enrutamiento Crítico y Optimizado**
  - [ ] Enrutar pares diferenciales USB con impedancia controlada
  - [ ] Enrutar cristal y QSPI con longitudes optimizadas
  - [ ] Crear planos de potencia y masa en capas internas
  - [ ] Enrutar líneas de motor con pistas anchas
  - [ ] Completar enrutamiento general de la placa

- [ ] **Paso 7: Generar Archivos de Fabricación y Modelo 3D**
  - [ ] Generar archivos Gerber para todas las capas
  - [ ] Generar archivo de taladros NC
  - [ ] Crear BOM en formato CSV
  - [ ] Generar archivo de Pick and Place
  - [ ] Exportar modelo 3D en formato STEP

- [ ] **Paso 8: Entregar Paquete de Proyecto al Usuario**
  - [ ] Organizar todos los archivos en estructura coherente
  - [ ] Comprimir proyecto completo
  - [ ] Proporcionar documentación de uso y fabricación
  - [ ] Entregar paquete final al usuario


- [ ] **Paso 9: Actualizaciones para la Versión 2 (V2)**
  - [X] **Modificaciones de Esquemáticos para V2**
    - [X] Actualizar `USB_Subsystem.kicad_sch` para conector USB Tipo-C
    - [X] Crear `PCIe_NVMe_Subsystem.kicad_sch` para NVMe
    - [X] Asegurar compatibilidad con OAK-D-Lite en esquemáticos (alimentación, datos) - [ ] **Modificaciones de Layout de PCB para V2**
    - [ ] Integrar conector USB Tipo-C en el layout de PCB
    - [ ] Adaptar layout para conector M.2 NVMe
    - [ ] Enrutar líneas PCIe/NVMe con impedancia controlada
    - [ ] Considerar colocación y enrutamiento para OAK-D-Lite


