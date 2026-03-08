

# Fase 1 y 2: Reconocimiento y Descubrimiento de Superficie (SMB)

## 🔍 Introducción

Esta etapa inicial se centra en la preparación del kit de herramientas técnico y el descubrimiento activo de objetivos dentro del segmento de red asignado (`10.6.6.0/24`).

---

## 🛠️ Parte 1: Evaluación de Capacidades de Enum4linux

Se validó la herramienta `enum4linux`, esencial para extraer información de sistemas que implementan el protocolo SMB.

### Verificación del Entorno

Se ejecutó el comando de ayuda para mapear los flags de auditoría:

```bash
enum4linux -h

```

**Flags identificados para la auditoría:**

* `-U`: Enumeración de usuarios.
* `-S`: Listado de recursos compartidos.
* `-P`: Información de políticas de contraseñas.
* `-a`: Análisis exhaustivo.

---

## 🛰️ Parte 2: Identificación de Servidores SMB con Nmap

El objetivo de esta fase es localizar hosts con servicios de archivos activos (puertos **139** y **445**).

### Escaneo de Red Ejecutado

Se realizó un barrido sobre la subred buscando específicamente puertos en estado `open`:

```bash
nmap -p 139,445 --open 10.6.6.0/24

```

### Resultados 

El escaneo en vivo identificó un único host objetivo con servicios SMB expuestos:

| Hostname | Dirección IP | Puertos Abiertos | Estado |
| --- | --- | --- | --- |
| **gravemind.vm** | **10.6.6.23** | 139/tcp, 445/tcp | Up |

**Análisis de los resultados:**

1. El host **10.6.6.23** es identificado como el vector principal de ataque.
2. A pesar de que la red cuenta con 256 IPs y 7 hosts activos, solo uno expone directamente el servicio de archivos, lo que lo convierte en un punto de interés crítico para la siguiente fase de enumeración.
   

El escaneo identificó al host gravemind.vm (10.6.6.23) con los servicios NetBIOS-SSN y Microsoft-DS en estado abierto. Técnicamente, esto confirma que el sistema está configurado para compartir recursos en red, lo cual es el requisito previo para realizar una enumeración de usuarios y recursos compartidos. La detección del puerto 445 sugiere que el objetivo es susceptible a ataques de sesión nula (Null Sessions), lo que valida el paso a la siguiente fase de la auditoría.

---


## 📸 Evidencias (Screenshots)
Imagen 1. Verificar que enum4linux esté instalado y vea el archivo de ayuda.
<img width="1156" height="563" alt="Captura de pantalla 2026-03-08 a la(s) 11 21 10" src="https://github.com/user-attachments/assets/f3f3b08e-e356-41b3-bb2c-e6a9dfc197e2" />
Imagen 2. Escaneo de red.
<img width="1180" height="674" alt="Captura de pantalla 2026-03-08 a la(s) 11 37 01" src="https://github.com/user-attachments/assets/6337bce6-782f-470a-85bf-e8bcf3284603" />
