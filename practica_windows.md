# Práctica Completa de Administración Windows Server 2019 + Windows 10

## 2.21. Modificar colores de PowerShell, título y prompt

``` powershell
notepad $PROFILE
New-Item -Type File -Path $PROFILE -Force
$Host.UI.RawUI.BackgroundColor = "DarkBlue"
$Host.UI.RawUI.ForegroundColor = "White"
Clear-Host
$Host.UI.RawUI.WindowTitle = "Mi PowerShell"
function prompt { "PS [$env:USERNAME] > " }
```

## 2.22. Crear máquina virtual Windows 10 (Cliente1)

Configuración de VM: Windows 10, 4GB RAM, 2 CPU, 60GB disco.

## 2.23. Comprobar conexión Cliente1--Servidor

``` powershell
ping servidor
Test-NetConnection servidor
```

## 2.24. Crear usuario local

``` powershell
New-LocalUser "usuariolocal" -Password (ConvertTo-SecureString "Contraseña123" -AsPlainText -Force) -UserMayNotChangePassword $true
Add-LocalGroupMember -Group "Users" -Member "usuariolocal"
```

## 2.25. Unir Cliente1 al dominio

``` powershell
Add-Computer -DomainName midominio.local -Credential midominio\Administrador -Restart
```

## 2.26. Crear OU y mover objetos

``` powershell
New-ADOrganizationalUnit -Name "departamento"
New-ADUser usuario1 -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force) -Enabled $true
Move-ADObject (Get-ADUser usuario1).DistinguishedName -TargetPath "OU=departamento,DC=midominio,DC=local"
Move-ADObject (Get-ADComputer Cliente1).DistinguishedName -TargetPath "OU=departamento,DC=midominio,DC=local"
```

## 2.27. Restringir usuario1 a Cliente1

``` powershell
Set-ADUser usuario1 -LogonWorkstations "Cliente1"
```

## 2.28. Crear usuario2

``` powershell
New-ADUser usuario2 -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force) -Enabled $true
```

## 2.29. Modificar usuario2

``` powershell
Set-ADUser usuario2 -PasswordNeverExpires $true -CannotChangePassword $true
```

## 2.30. Crear usuario3 basado en usuario2

``` powershell
Copy-ADUser usuario2 -NewName usuario3 -SamAccountName usuario3 -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force) -Enabled $true
```

## 2.31. Crear grupo global

``` powershell
New-ADGroup grupo1 -GroupScope Global -GroupCategory Security
```

## 2.32. Agregar usuario3 al grupo

``` powershell
Add-ADGroupMember grupo1 usuario3
```

## 2.33. Mover usuario3 a la OU

``` powershell
Move-ADObject (Get-ADUser usuario3).DistinguishedName -TargetPath "OU=departamento,DC=midominio,DC=local"
```

## 2.34. Eliminar usuario3

``` powershell
Remove-ADUser usuario3
```

## 2.35. Eliminar grupo

``` powershell
Remove-ADGroup grupo1
```

## 2.36. Instalar Cliente2 vía WDS

Configurar VM → arranque PXE → instalación vía red.

## 2.37. DHCP en Cliente1 y Cliente2

``` powershell
Set-NetIPInterface -InterfaceAlias "Ethernet" -Dhcp Enabled
```

## 2.38. Comprobar conexión

``` powershell
ping servidor
Test-NetConnection servidor
```

## 2.39. Añadir Cliente2 al dominio y moverlo

``` powershell
Add-Computer -DomainName midominio.local -Credential midominio\Administrador -Restart
Move-ADObject (Get-ADComputer Cliente2).DistinguishedName -TargetPath "OU=departamento,DC=midominio,DC=local"
```

## 2.40. Rol de impresión

``` powershell
Get-WindowsFeature Print-Server
Install-WindowsFeature Print-Server
Add-Printer -Name "Impresora1" -DriverName "Microsoft Print To PDF" -PortName "PORTPROMO1"
```

## 2.41. Crear usuario4 con restricciones

``` powershell
New-ADUser usuario4 -Enabled $true -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force)
Set-ADUser usuario4 -LogonWorkstations "Cliente1"
```

## 2.42. Variables de entorno

``` powershell
setx Minombre "Tu Nombre Completo"
setx PATH "$env:PATH;C:\temp"
echo $env:Minombre
echo $env:PATH
```

## 2.43. Listar discos

    diskpart
    list disk

``` powershell
Get-Disk
```

## 2.44. Listar volúmenes y particiones

    list volume
    list partition

``` powershell
Get-Volume
Get-Partition
```

## 2.45. MMC personalizada

MMC → Agregar complementos → Administrador de dispositivos +
Administración de equipos.

## 2.46. Renovar IP

``` powershell
ipconfig /renew
```

## 2.47. Ver IP y probar interfaz local

``` powershell
ipconfig
Get-NetIPAddress
ping 127.0.0.1
Test-NetConnection 127.0.0.1
```

## 2.48. Crear usu1 y usu2

``` powershell
New-ADUser usu1 -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force) -Enabled $true
New-ADUser usu2 -AccountPassword (ConvertTo-SecureString "Pass123." -AsPlainText -Force) -Enabled $true
```

## 2.49. Crear ficheros de usuario

-   Escritorio → fichero1.txt\
-   Documentos → fichero2.txt

## 2.50. Ver perfiles generados

Revisar `C:\Users\usu1` y `C:\Users\usu2`.

## 2.51. Intentar iniciar sesión con usu1 en el servidor

El mensaje indica restricciones de inicio.\
Solución → permitir en directiva "Iniciar sesión localmente".
