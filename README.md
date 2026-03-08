# EthicalHacking-Lab-Enum4linux
# Auditoría de Seguridad SMB: Enumeración y Análisis de Vulnerabilidades

## 🛡️ Resumen del Proyecto
Este repositorio documenta una auditoría técnica realizada sobre el protocolo **SMB (Server Message Block)** en un entorno de red empresarial simulado. El objetivo es identificar configuraciones inseguras, enumerar activos críticos y validar vectores de ataque que podrían permitir el movimiento lateral o el compromiso de datos sensibles.

> **Certificación relacionada:** Basado en los laboratorios prácticos del curso de **Cisco Ethical Hacking**.

## 📊 Metodología Aplicada
El análisis se dividió en cuatro fases críticas, alineadas con los estándares de la industria:

### [Fase 1: Reconocimiento de Herramientas](01-recon-and-discovery/)
* **Objetivo:** Evaluación de capacidades de `enum4linux`.
* **Competencia:** Configuración de herramientas de auditoría en entorno Kali Linux.

### [Fase 2: Escaneo y Descubrimiento de Superficie](01-recon-and-discovery/)
* **Objetivo:** Localización de hosts con servicios SMB activos (Puertos 139/445).
* **Herramienta:** Nmap con técnicas de filtrado de hosts vivos.

### [Fase 3: Enumeración Profunda de Objetivos](02-smb-enumeration/)
* **Objetivo:** Extracción de SIDs, nombres de usuario, grupos y políticas de contraseñas.
* **Técnica:** Explotación de "Null Sessions" para recolección de metadatos.

### [Fase 4: Validación de Acceso y Post-Explotación](03-exploitation-validation/)
* **Objetivo:** Interacción con recursos compartidos y prueba de transferencia de archivos.
* **Herramienta:** Smbclient.

## 🛠️ Tecnologías Utilizadas
* **OS:** Kali Linux (Rolling Edition)
* **Scanner:** Nmap v7.9x
* **Enum:** Enum4linux (Samba enumeration tool)
* **Access:** Smbclient

## ⚖️ Descargo de Responsabilidad (Disclaimer)
Este proyecto tiene fines exclusivamente educativos. El análisis se realizó en un entorno controlado y autorizado. No se incluye material protegido por derechos de autor de terceros; toda la documentación y análisis son de autoría propia basada en la experiencia práctica.

---
**Contacto:** CARLOS NOBOA  
**Especialización:** Estudiante de Ciberseguridad / Aspirante a Analista de Seguridad.
