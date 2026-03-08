

# 🛡️ SMB Penetration Testing Lab: Gravemind.vm

Este repositorio documenta una auditoría de seguridad completa realizada en un entorno controlado. El objetivo fue identificar, enumerar y validar vulnerabilidades en el protocolo **SMB (Server Message Block)** de un servidor objetivo dentro de una red local, siguiendo la metodología de Pentesting.

---

## 📋 Resumen del Proyecto

El laboratorio se centró en el host **10.6.6.23 (gravemind.vm)**. A través de este ejercicio, se demostró cómo una configuración permisiva en Samba puede exponer información crítica de la organización, como nombres de usuarios reales y estructuras de directorios confidenciales.

### 🛠️ Herramientas Utilizadas

* **Kali Linux:** OS Atacante.
* **Nmap:** Descubrimiento de red y escaneo de puertos.
* **Enum4linux:** Enumeración de usuarios, SIDs y recursos compartidos.
* **SMBClient:** Validación de explotación y testeo de permisos.

---

## 🚀 Estructura del Repositorio

El proyecto sigue un flujo lógico de ataque dividido en tres fases principales:

### [📁 01-reconnaissance-nmap]

**Fase de Descubrimiento:** * Escaneo de la subred para identificar hosts activos.

* Identificación del servidor objetivo `10.6.6.23` con los puertos **139 (NetBIOS)** y **445 (SMB)** abiertos.

### [📁 02-smb-enumeration]

**Fase de Enumeración:** * Extracción de metadatos del servicio Samba utilizando `enum4linux`.

* **Hallazgos:** Confirmación de **Null Sessions**, lista de usuarios (`masterchief`, `arbiter`) y detección del recurso compartido `workfiles`.

### [📁 03-exploitation-validation]

**Fase de Explotación:** * Intento de intrusión y prueba de carga de archivos (PoC).

* **Resultado:** Validación de acceso anónimo exitoso. Se confirmó política de **solo lectura** tras recibir error `NT_STATUS_ACCESS_DENIED` al intentar escribir.

---

## 📊 Matriz de Hallazgos

| Vulnerabilidad | Severidad | Descripción |
| --- | --- | --- |
| **SMB Anonymous Login** | **ALTA** | El servidor permite conexiones sin credenciales (Null Sessions). |
| **User Enumeration** | **MEDIA** | Exposición de nombres de usuario reales mediante técnicas de RID Cycling. |
| **Information Leakage** | **MEDIA** | Visibilidad de recursos compartidos confidenciales para usuarios no autenticados. |

---

## 🛡️ Recomendaciones de Mitigación

1. **Hardening de Samba:** Configurar `restrict anonymous = 2` en `smb.conf`.
2. **Políticas de Acceso:** Restringir el recurso `workfiles` solo a usuarios autenticados del grupo correspondiente.
3. **Seguridad de Contraseñas:** Implementar complejidad y longitud mínima mayor a 12 caracteres.

---

