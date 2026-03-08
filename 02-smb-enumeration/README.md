

# Fase 3: Enumeración Detallada de SMB (Scanning for Vulnerabilities)

## 🎯 Objetivo de la Fase

Una vez identificado el host activo **10.6.6.23 (gravemind.vm)**, el objetivo es realizar una enumeración profunda utilizando `enum4linux` para extraer información sensible que permita planificar un vector de entrada.

---

## 🛠️ Ejecución Técnica

Se utilizó el modo de enumeración completa (`-a`) para interrogar al servicio Samba del objetivo.

**Comando ejecutado:**

```bash
enum4linux -a 10.6.6.23

```

---

## 📊 Análisis de Resultados (Hallazgos Críticos)

El análisis del output de la terminal reveló múltiples configuraciones inseguras:

### 1. Confirmación de "Null Sessions" (Sesión Nula)

El servidor permite la conexión sin proporcionar un nombre de usuario o contraseña válidos.

* **Evidencia:** `[+] Server 10.6.6.23 allows sessions using username '', password ''`
* **Riesgo:** Esto permite a cualquier atacante en la red listar usuarios y recursos compartidos de forma anónima.

### 2. Diccionario de Usuarios Identificados

A través de la técnica de **RID Cycling**, se extrajeron cuentas de usuario reales:

* `masterchief` (RID: 1000)
* `arbiter` (RID: 1001)
* `labuser` (RID: 1002)
* **Análisis:** Estos nombres de usuario ahora pueden ser utilizados para ataques de fuerza bruta dirigidos.

### 3. Enumeración de Recursos Compartidos (Shares)

Se localizaron carpetas compartidas en el servidor, destacando una de alta sensibilidad:

* **Recurso:** `workfiles`
* **Comentario:** *Confidential Workfiles*
* **Permisos detectados:** `Mapping: OK`, `Listing: OK`.
* **Riesgo:** La carpeta "Confidential" es accesible de forma gratuita para cualquier usuario anónimo, lo que representa una **fuga de información** inminente.

### 4. Debilidad en Políticas de Seguridad (Password Policy)

* **Longitud mínima de contraseña:** 5 caracteres.
* **Complejidad de contraseña:** Desactivada (Disabled).
* **Riesgo:** Las políticas son extremadamente permisivas, facilitando el descifrado de contraseñas por ataques de diccionario.

---

## 🛡️ Conclusión de la Fase

El host **10.6.6.23** es altamente vulnerable. La combinación de sesiones nulas permitidas y una carpeta confidencial con acceso de lectura (`workfiles`) lo convierte en el objetivo principal para la fase de explotación (transferencia de archivos).

---

## 📸 Evidencias

Imagen 1. Acceso Anónimo y Usuarios
<img width="1180" height="823" alt="Captura de pantalla 2026-03-08 a la(s) 15 00 08" src="https://github.com/user-attachments/assets/f69b7a5e-0c1f-46a7-9346-014a60f3f652" />



Imagen 2. Lista de Carpetas (Shares)
<img width="1170" height="808" alt="Captura de pantalla 2026-03-08 a la(s) 15 03 19" src="https://github.com/user-attachments/assets/ca90ca41-15a3-4c0c-a481-689b2c1b2d2c" />


