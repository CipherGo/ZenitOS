# KernixOS

**KernixOS** es un sistema operativo básico y experimental diseñado para aprender sobre la programación de sistemas y el desarrollo de sistemas operativos. Este proyecto es un punto de partida ideal para explorar los conceptos fundamentales en la creación de un sistema operativo.

## Características

- **Bootloader Básico**: Un bootloader simple que imprime "KernixOS" en la pantalla y carga el núcleo del sistema.
- **Núcleo Básico**: Implementa la inicialización de la memoria, el sistema de archivos, y los controladores básicos. También gestiona la programación de procesos.
- **Programación de Procesos**: Implementa un planificador simple para ejecutar procesos en cola.
- **Interfaz de Línea de Comandos (CLI)**: Proporciona un prompt de comandos básico para la interacción con el sistema.

## Estructura del Proyecto

- **bootloader.asm**: Código fuente del bootloader.
- **kernel.c**: Código fuente del núcleo del sistema operativo.
- **scheduler.c**: Implementación del planificador de procesos.
- **scheduler.h**: Encabezado del planificador de procesos.
- **filesystem.c**: Implementación básica del sistema de archivos.
- **init.c**: Código para la inicialización del sistema.
- **bootloader.h**: Encabezado del bootloader.
- **README.md**: Documentación del proyecto.

## Cómo Compilar y Ejecutar

1. **Configura tu Entorno:**
   - Asegúrate de tener instalados los compiladores y herramientas necesarios, como `gcc`, `nasm`, y `qemu`.

2. **Compila el Bootloader:**
   - Usa `nasm` para compilar `bootloader.asm`.
   ```bash
   nasm -f bin bootloader.asm -o bootloader.bin
  ``` 
gcc -ffreestanding -c kernel.c -o kernel.o
gcc -ffreestanding -c scheduler.c -o scheduler.o
gcc -ffreestanding -c filesystem.c -o filesystem.o
gcc -ffreestanding -c init.c -o init.o
ld -o kernel.bin -Ttext 0x1000 kernel.o scheduler.o filesystem.o init.o --oformat binary
```
```
cat bootloader.bin kernel.bin > os_image.bin
```
```
qemu-system-x86_64 -drive format=raw,file=os_image.bin
