# Práctica: Actividades 2.52 – 2.56

## 2.52 – Búsqueda de dominios internacionalizados (IDN)
1. Investiga qué son los **IDN (Internationalized Domain Names)**.
2. Busca ejemplos reales de dominios que incluyan caracteres no ASCII (ñ, á, ü, ç, 中, 日本, etc.).
3. Anota varios ejemplos y explica cómo funcionan internamente usando **Punycode**.

---

## 2.53 – Ventajas de Windows Server 2019 respecto a versiones anteriores
1. Busca las principales novedades introducidas en **Windows Server 2019** comparado con 2016 y anteriores.
2. Resume ventajas relacionadas con:
   - Seguridad (Windows Defender ATP, protección avanzada).
   - Integración con Azure.
   - Rendimiento y contenedores.
   - Storage Spaces Direct y mejoras en almacenamiento.
   - Mejoras en administración y Windows Admin Center.
3. Añade una tabla comparativa si lo consideras útil.

---

## 2.54 – Instalación de un servidor web
1. En tu servidor Windows Server, abre **Administrador del Servidor**.
2. Instala la característica **IIS (Internet Information Services)**.
3. Verifica que el servicio esté activo.
4. Desde un cliente Windows 10, abre el navegador y accede mediante:
   ```
   http://IP_DEL_SERVIDOR
   ```
5. Comprueba que aparece la página por defecto de IIS.
6. Opcional: crea una página personalizada y súbela al directorio:
   ```
   C:\inetpub\wwwroot
   ```

---

## 2.55 – Descarga de apuntes y ejercicios de PowerShell
1. Entra a la web de la editorial y descarga el material detallado de PowerShell.
2. Revisa los comandos fundamentales:
   - `Get-Help`
   - `Get-Command`
   - `Get-Process`, `Stop-Process`
   - Gestión de servicios
   - Gestión de ficheros
3. Realiza los ejercicios incluidos y documenta resultados y capturas.

---

## 2.56 – Instalación de un cliente Windows 10 mediante WDS
1. En tu servidor Windows Server, asegúrate de tener instalado y configurado **WDS**.
2. Añade una imagen de instalación de Windows 10.
3. Crea una imagen de captura si es necesario.
4. Arranca una nueva máquina virtual en red (PXE Boot).
5. Instala Windows 10 automáticamente desde WDS.
6. Una vez instalado, añade software obligatorio:
   - Antivirus (Windows Defender, Avast, etc.).
   - Paquete ofimático (Microsoft Office u OpenOffice).
   - Adobe Reader.
7. Nombra la máquina como **Cliente3**.
8. Comprueba que se comunica correctamente con el dominio si es necesario.

---

## Entrega
Incluye:
- Capturas de cada paso.
- Comprobaciones del correcto funcionamiento.
- Comentarios o problemas encontrados.
