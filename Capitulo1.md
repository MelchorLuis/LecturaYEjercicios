# Capitulo 1: Introducción al ensamblador

**Características generales de la arquitectura ARM**

ARM es una arquitectura RISC de 32 bits, salvo la versión del core ARMv8-A que es mixta 32/64 bits (bus de 32 bits con registros de 64 bits)..
Se trata de una arquitectura licenciable, quiere decir que la empresa desarrolladora ARM Holdings diseña la arquitectura, pero son otras compañías 
las que fabrican y venden los chips, llevándose ARM Holdings un pequeño porcentaje por la licencia.

El chip en concreto que lleva la Raspberry Pi es el BCM2835, se trata de un SoC (System on a Chip=Sistema en un sólo chip) que contiene además de 
la CPU otros elementos como un núcleo GPU (hardware acelerado OpenGL ES/OpenVG/OpenEGL/OpenMAX y decodificación H.264 por hardware) y un núcleo DSP (Digital
signal processing=Procesamiento digital de señales) que es un procesador más pequeño y simple que el principal, pero especializado en el procesado y representación
de señales analógicas.

|             **Familia**                |   Arquitectura   |  Bits |     Ejemplos de dispositivos    |
|:--------------------------------------:|:----------------:|:-----:|:-------------------------------:|
| ARM1                                   | ARMv1            | 32/26 | Segundo procesador BBC Micro    |
| ARM2, ARM3, Amber                      | ARMv2            | 32/26 | Acorn Archimedes                |
| ARM6, ARM7                             | ARMv3            | 32    | Apple Newton Serie 100          |
| ARM8, StrongARM                        | ARMv4            | 32    | Apple Newton serie 2x00         |
| ARM7TDMI, ARM9TDMI                     | ARMv4T           | 32    | Game Boy Advance                |
| ARM7EJ, ARM9E, ARM10E, XScale          | ARMv5            | 32    | Samsung Omnia,  Blackberry 8700 |
| ARM11                                  | ARMv6            | 32    | iPhone 3G, Raspberry Pi         |
| Cortex-M0/M0+/M1                       | ARMv6-M          | 32    |                                 |
| Cortex-M3/M4                           | ARMv7-M ARMv7E-M | 32    | Texas Instruments Stellaris     |
| Cortex-R4/R5/R7                        | ARMv7-R          | 32    | Texas Instruments TMS570        |
| Cortex-A5/A7/A8/A9 A12/15/17, Apple A6 | ARMv7-A          | 32    | Apple iPad                      |
| Cortex-A53/A57, X-Gene, Apple A7       | ARMv8-A          | 64/32 | Apple iPhone 5S                 |

Tabla 1.1: Lista de familias y arquitecturas ARM


**El lenguaje ensamblador**
