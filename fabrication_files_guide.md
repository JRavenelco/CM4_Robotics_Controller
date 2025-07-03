# Generación de Archivos de Fabricación para CM4 Robotics Controller

Este documento describe el proceso para generar todos los archivos de fabricación necesarios para la producción del CM4 Robotics Controller.

## Archivos Gerber

Los archivos Gerber son el estándar de la industria para la fabricación de PCB. Se deben generar los siguientes archivos:

1. **Capas de cobre**:
   - F.Cu - Capa superior de cobre
   - In1.Cu - Capa interna 1 (plano de masa)
   - In2.Cu - Capa interna 2 (plano de potencia)
   - B.Cu - Capa inferior de cobre

2. **Capas de máscara de soldadura**:
   - F.Mask - Máscara de soldadura superior
   - B.Mask - Máscara de soldadura inferior

3. **Capas de serigrafía**:
   - F.SilkS - Serigrafía superior
   - B.SilkS - Serigrafía inferior

4. **Capas de pasta de soldadura**:
   - F.Paste - Pasta de soldadura superior
   - B.Paste - Pasta de soldadura inferior

5. **Borde de la placa**:
   - Edge.Cuts - Contorno de la placa

### Configuración de Exportación Gerber

En KiCad, usar la siguiente configuración para la exportación de archivos Gerber:

- Formato: Gerber X2
- Unidades: mm
- Precisión: 4.6 (4 dígitos para la parte entera, 6 para la decimal)
- Incluir información de atributos extendidos
- Usar extensiones de archivo Protel (.GTL, .GBL, etc.)

## Archivo de Taladros NC (NC Drill)

El archivo de taladros NC contiene la información para todos los agujeros y vías en la placa:

- Formato: Excellon
- Unidades: mm
- Precisión: 2:4
- Generar un mapa de taladros en formato PDF
- Incluir tanto taladros chapados como no chapados

## Lista de Materiales (BOM)

La lista de materiales debe incluir todos los componentes necesarios para el ensamblaje:

- Formato: CSV
- Incluir: Designador, Valor, Footprint, Fabricante, Número de Parte, Cantidad
- Agrupar componentes idénticos
- Ordenar por referencia

## Archivo de Pick and Place

El archivo de Pick and Place (también conocido como archivo de posicionamiento o centroide) es necesario para el ensamblaje automatizado:

- Formato: CSV
- Unidades: mm
- Origen: Esquina inferior izquierda de la placa
- Incluir: Designador, Valor, Footprint, Posición X, Posición Y, Rotación, Capa

## Modelo 3D

El modelo 3D de la placa ensamblada es útil para verificación visual y documentación:

- Formato: STEP
- Incluir todos los componentes con sus modelos 3D
- Exportar con colores y texturas
- Resolución: Media-alta para equilibrar detalle y tamaño de archivo

## Proceso de Generación en KiCad

1. **Archivos Gerber y NC Drill**:
   - En el editor de PCB, ir a "File > Plot"
   - Seleccionar las capas necesarias
   - Configurar según las especificaciones anteriores
   - Hacer clic en "Plot" para generar los archivos Gerber
   - En la misma ventana, hacer clic en "Generate Drill File" para crear el archivo NC Drill

2. **Lista de Materiales (BOM)**:
   - En el editor de esquemáticos, ir a "Tools > Generate BOM"
   - Seleccionar el plugin "bom_csv_grouped_by_value"
   - Configurar las columnas necesarias
   - Generar el archivo CSV

3. **Archivo de Pick and Place**:
   - En el editor de PCB, ir a "File > Fabrication Outputs > Footprint Position (.pos) File"
   - Configurar según las especificaciones anteriores
   - Generar el archivo CSV

4. **Modelo 3D**:
   - En el editor de PCB, ir a "File > Export > STEP"
   - Configurar según las especificaciones anteriores
   - Exportar el modelo 3D

## Estructura de Carpetas para Archivos de Fabricación

Organizar los archivos de fabricación en la siguiente estructura:

```
CM4_Robotics_Controller_Fabrication/
├── Gerber/
│   ├── CM4_Robotics_Controller-F_Cu.gtl
│   ├── CM4_Robotics_Controller-In1_Cu.g2
│   ├── CM4_Robotics_Controller-In2_Cu.g3
│   ├── CM4_Robotics_Controller-B_Cu.gbl
│   ├── CM4_Robotics_Controller-F_Mask.gts
│   ├── CM4_Robotics_Controller-B_Mask.gbs
│   ├── CM4_Robotics_Controller-F_SilkS.gto
│   ├── CM4_Robotics_Controller-B_SilkS.gbo
│   ├── CM4_Robotics_Controller-F_Paste.gtp
│   ├── CM4_Robotics_Controller-B_Paste.gbp
│   └── CM4_Robotics_Controller-Edge_Cuts.gm1
├── Drill/
│   ├── CM4_Robotics_Controller.drl
│   └── CM4_Robotics_Controller-drl_map.pdf
├── Assembly/
│   ├── CM4_Robotics_Controller_BOM.csv
│   └── CM4_Robotics_Controller_PnP.csv
└── 3D/
    └── CM4_Robotics_Controller.step
```

## Verificación Final

Antes de enviar los archivos a fabricación, verificar:

1. Que todos los archivos Gerber se abran correctamente en un visor Gerber
2. Que el archivo de taladros contenga todos los agujeros necesarios
3. Que la BOM incluya todos los componentes con sus números de parte correctos
4. Que el archivo de Pick and Place tenga las coordenadas correctas
5. Que el modelo 3D muestre correctamente todos los componentes en sus posiciones
