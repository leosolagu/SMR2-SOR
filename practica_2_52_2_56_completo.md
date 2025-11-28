# Práctica: Actividades 2.52 – 2.56

> **Resumen:** Este documento explica paso a paso las actividades 2.52 a 2.56. Donde hace falta información de internet (ejemplos y novedades) se han buscado y citan las fuentes.

---

## 2.52 — Ejemplos de dominios internacionalizados (IDN)

**Qué son (resumen):**  
Los *Internationalized Domain Names* (IDN) son dominios que contienen caracteres fuera del conjunto ASCII (por ejemplo: ñ, á, ü, caracteres cirílicos, chinos, árabes, etc.). Internamente se codifican en ASCII usando **Punycode** y se representan en DNS con el prefijo `xn--`. (Ver fuentes).  

**Ejemplos reales y su forma Punycode (ejemplos para probar):**
- `bücher.example` → `xn--bcher-kva.example` (ejemplo con ü).  
- `niño.ws` → `xn--nio-8ma.ws` (ejemplo con ñ).  
- `tølløse.dk` → `xn--tllse-vuac.dk` (ejemplo con ø).  
- `测试假域名.com` → `xn--sxqv5g23dyr3a428a.com` (ejemplo con caracteres chinos).  

**Cómo comprobar / convertir:**  
- Usa un conversor Punycode (por ejemplo: punycoder.com) para obtener la forma `xn--...`.  
- En el navegador moderno puedes escribir el dominio en Unicode; el navegador lo convertirá a Punycode para la resolución DNS.  

**Dónde leer más (fuentes):** artículo general sobre IDN y Punycode y ejemplos.  

---

## 2.53 — Ventajas y novedades de Windows Server 2019 (comparado con 2016 y anteriores)

**Resumen de los puntos clave (resumido):**
1. **Nube híbrida y Azure integration** — mejoras para conectar servicios on‑premises con Azure (Azure Network Adapter, almacenamiento híbrido, Azure Backup/DR).  
2. **Seguridad** — Windows Defender Advanced Threat Protection (ATP) integrado, características de protección mejoradas y Windows Defender Exploit Guard.  
3. **Mejoras en HCI (Hyper-Converged Infrastructure) y Storage Spaces Direct** — mayor escalabilidad y rendimiento (mejor monitorización desde Windows Admin Center).  
4. **Soporte y mejoras para contenedores** — imágenes de Windows Server más ligeras y mejoras en la compatibilidad con Kubernetes/Docker.  
5. **Windows Admin Center** — nueva consola web para administración y monitorización local y remota.  
6. **Rendimiento y límites ampliados** — mejoras en almacenamiento máximo y rendimiento en escenarios HCI.  

**Recomendación:** revisa la documentación oficial para detalles y notas de versión antes de desplegar en producción.  

**Fuentes oficiales y resumen técnico:** documentación "What's new in Windows Server 2019" y guía en MS Learn.

---

## 2.54 — Instalar un servidor web (IIS) en el servidor y comprobar desde un cliente Windows 10

### 1) Instalar IIS en Windows Server 2019 (PowerShell / GUI)

**PowerShell (modo rápido, con consola Administrador):**
```powershell
# Instala IIS (rol Web-Server) y herramientas de gestión
Install-WindowsFeature -Name Web-Server -IncludeManagementTools

# Comprobar estado
Get-WindowsFeature Web-Server
```

**Desde Server Manager (GUI):**
- Abrir *Server Manager* → *Add roles and features* → seleccionar *Web Server (IIS)* → instalar.

### 2) Verificar que IIS está funcionando en el servidor
- En el servidor abre un navegador y visita `http://localhost`. Debe verse la página por defecto de IIS.
- Comprobar servicio:
```powershell
Get-Service W3SVC
```

### 3) Permitir acceso desde el cliente (si hay firewall)
```powershell
# Permitir HTTP (puerto 80)
New-NetFirewallRule -DisplayName "IIS HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

### 4) Desde Cliente (Windows 10)
- En el navegador del cliente escribe: `http://IP_DEL_SERVIDOR` (o `http://NOMBRE_SERVIDOR` si DNS resuelve).
- Deberías ver la página por defecto de IIS. Si no, comprobar conectividad (ping / Test-NetConnection) y reglas de firewall.

### 5) Publicar una página simple
- En el servidor, guarda un `index.html` en `C:\inetpub\wwwroot\index.html` con contenido simple para comprobar que tu página se sirve.

**Fuentes y notas sobre instalación y resolución de problemas** se indican al final.

---

## 2.55 — Descargar apuntes y ejercicios sobre PowerShell y realizar ejercicios

**Dónde buscar y descargar material:**
- Sitio oficial de documentación y tutoriales de PowerShell (Microsoft Learn) para referencia y ejemplos.  
- Buscar en la web de la editorial indicada por el profesor para descargar los apuntes y ejercicios (si la editorial requiere acceso con clave, usa las credenciales de la asignatura).  

**Comandos y temas a practicar (ejercicios recomendados):**
- `Get-Help`, `Get-Command`, `Get-Process`, `Stop-Process`.  
- Gestión de servicios: `Get-Service`, `Start-Service`, `Stop-Service`.  
- Gestión de archivos: `Get-ChildItem`, `Copy-Item`, `Move-Item`, `Remove-Item`.  
- Variables, bucles y condicionales básicos en scripts `.ps1`.  
- Uso de `Get-Help <cmdlet> -Examples` y `Update-Help` para obtener la ayuda actualizada.

**Cómo documentar los ejercicios:**
- Para cada ejercicio incluye: objetivo, comandos ejecutados, salida obtenida (pegar texto o capturas), y conclusión/errores encontrados.

**Fuentes de referencia para ejercicios y tutoriales:** Microsoft Learn, libros y guías prácticas (ver sección Fuentes).

---

## 2.56 — Instalar Cliente3 mediante WDS con software adicional

### Requisitos previos en el servidor
- Windows Deployment Services (WDS) instalado y configurado.
- Imagen de instalación de Windows 10 añadida a WDS (install.wim).
- Si quieres preinstalar aplicaciones, crea una **imagen de referencia (captura)** con las aplicaciones instaladas y convierte a imagen WIM para desplegar (opcional).

### Proceso (resumen)
1. **Preparar una VM** para instalación por red (configurar arranque PXE).  
2. **Arrancar la VM y seleccionar la imagen** de Windows 10 desde WDS.  
3. **Instalación básica** y nombre de equipo: `Cliente3`.  
4. **Instalar aplicaciones** (post‑instalación):
   - Antivirus (ej. Windows Defender ya viene activado; si usas otro, instala el instalador offline).
   - Paquete ofimático: instalar OpenOffice (gratis) o Microsoft Office si tienes licencia.
   - Adobe Reader: ejecutar instalador `AdbeRdr*.exe` o usar distribución MSI si la tienes.
5. **Captura opcional para futuras instalaciones (crear imagen personalizada):**
   - Monta y generaliza la imagen con `sysprep /generalize` y luego captura con WDS para crear una imagen lista para desplegar.
6. **Comprobar conectividad y dominio:** unir `Cliente3` al dominio si es necesario y verificar acceso.

---

## Capturas / Imágenes
- Se recomienda incluir capturas de cada paso: instalación de roles, la página IIS desde el cliente, resultados de PowerShell y los instaladores del software.  
- En el repositorio GitHub coloca la carpeta `images/` y nombra las capturas como `2.54_iis_server.png`, `2.55_powershell_ex1.png`, `2.56_cliente3_install.png`, etc.

---

## Entrega
Sube a tu repositorio GitHub:
- Este fichero `practica_2_52_2_56.md`.  
- Carpeta `images/` con capturas.  
- Un ZIP opcional con scripts `.ps1` usados.

---

## Fuentes (consultadas)
- Definición y ejemplos de IDN / Punycode. citeturn0search0turn0search8  
- Documentación oficial: *What's new in Windows Server 2019* (Microsoft). citeturn0search1turn0search3  
- PowerShell – Documentación oficial (MS Learn). citeturn1search0  
- Instalación de IIS y procedimientos comunes (MS Learn / ServerFault). citeturn2search6turn2search12

