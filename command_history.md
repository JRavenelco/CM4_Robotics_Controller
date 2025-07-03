# Historial de Comandos - CM4 Robotics Controller

Este archivo contiene el historial de comandos de terminal utilizados durante el desarrollo del proyecto CM4 Robotics Controller.

## Configuración Inicial del Proyecto

```bash
# Crear directorio del proyecto
mkdir -p /home/ubuntu/CM4_Robotics_Controller

# Crear estructura de directorios
mkdir -p /home/ubuntu/CM4_Robotics_Controller/schematics
mkdir -p /home/ubuntu/CM4_Robotics_Controller/lib_symbols/custom
mkdir -p /home/ubuntu/CM4_Robotics_Controller/lib_footprints/custom

# Descargar footprints oficiales del CM4
wget -P /home/ubuntu/CM4_Robotics_Controller/lib_footprints/ https://datasheets.raspberrypi.com/cm4io/CM4IO-KiCAD.zip

# Extraer footprints oficiales
unzip -o /home/ubuntu/CM4_Robotics_Controller/lib_footprints/CM4IO-KiCAD.zip -d /home/ubuntu/CM4_Robotics_Controller/lib_footprints/cm4io_official
```

## Inicialización del Repositorio Git

```bash
# Inicializar repositorio Git
cd /home/ubuntu/CM4_Robotics_Controller && git init

# Configurar usuario Git
cd /home/ubuntu/CM4_Robotics_Controller && git config --global user.email "manus@example.com" && git config --global user.name "Manus AI"

# Primer commit con la estructura básica
cd /home/ubuntu/CM4_Robotics_Controller && git add .
cd /home/ubuntu/CM4_Robotics_Controller && git commit -m "Commit inicial: Estructura del proyecto, esquemáticos jerárquicos y bibliotecas personalizadas"

# Añadir archivo .gitignore
cd /home/ubuntu/CM4_Robotics_Controller && git add .gitignore && git commit -m "Añadir archivo .gitignore para excluir archivos temporales y de fabricación"
```

## Desarrollo de Esquemáticos

```bash
# Commits de los diferentes subsistemas
cd /home/ubuntu/CM4_Robotics_Controller && git add schematics/RP2040_Subsystem.kicad_sch && git commit -m "Añadir esquemático detallado del subsistema RP2040"

cd /home/ubuntu/CM4_Robotics_Controller && git add schematics/Motor_Driver_Subsystem.kicad_sch && git commit -m "Añadir esquemático detallado del subsistema de drivers de motor"

cd /home/ubuntu/CM4_Robotics_Controller && git add schematics/Sensor_Subsystem.kicad_sch && git commit -m "Añadir esquemático detallado del subsistema de sensores"

cd /home/ubuntu/CM4_Robotics_Controller && git add schematics/USB_Subsystem.kicad_sch && git commit -m "Añadir esquemático detallado del subsistema USB"
```

## Desarrollo del Layout PCB

```bash
# Añadir archivo PCB y guías
cd /home/ubuntu/CM4_Robotics_Controller && git add CM4_Robotics_Controller.kicad_pcb critical_routing_guide.md fabrication_files_guide.md && git commit -m "Añadir archivo PCB base, guía de enrutamiento crítico y guía de archivos de fabricación"

# Añadir README
cd /home/ubuntu/CM4_Robotics_Controller && git add README.md && git commit -m "Añadir README con descripción completa del proyecto"
```

## Preparación para Entrega

```bash
# Crear paquete ZIP del proyecto
cd /home/ubuntu/CM4_Robotics_Controller && mkdir -p CM4_Robotics_Controller_Package && cp -r * .git .gitignore CM4_Robotics_Controller_Package/ && cd CM4_Robotics_Controller_Package && zip -r ../CM4_Robotics_Controller_Package.zip *
```

## Comandos para Verificación

```bash
# Verificar estado del repositorio
git status

# Ver historial de commits
git log --oneline

# Ver estructura de archivos
ls -la
```

## Notas Adicionales

Estos comandos representan las operaciones principales realizadas durante el desarrollo del proyecto. Para el uso con GitKraken, la mayoría de estas operaciones se pueden realizar a través de la interfaz gráfica, sin necesidad de utilizar la línea de comandos.
