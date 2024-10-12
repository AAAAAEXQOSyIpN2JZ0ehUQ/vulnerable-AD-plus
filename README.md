﻿![logo](https://github.com/AAAAAEXQOSyIpN2JZ0ehUQ/vulnerable-AD-plus/blob/main/Imagenes/vulnerable-AD-plus.png)

# Vuln ad plus :octocat:
Vulnerable-AD-Plus

## :information_source: Descripción
Cree un directorio activo vulnerable que le permita probar la mayoría de los ataques al directorio activo en el laboratorio local.

## :star2: Características principales

- Ataques aleatorios
- Cobertura total de los ataques mencionados.
- necesita ejecutar el script en DC con Active Directory instalado 
- Algunos de los ataques requieren una estación de trabajo del cliente.

## :bookmark_tabs: Redacción

Ahora incluye una sección de reseñas [**WriteUp**](WriteUp).

## :computer: Ataques admitidos

- Abusing ACLs/ACEs
- Kerberoasting
- AS-REP Roasting
- Abuse DnsAdmins (...)
- Password in AD User comment
- Password Spraying
- DCSync (...)
- Silver Ticket (...)
- Golden Ticket (...)
- Pass-the-Hash (...)
- Pass-the-Ticket (...)
- SMB Signing Disabled
- Bad WinRM permission
- Anonymous LDAP query
- Public SMB Share
- Zerologon (Check version)

### Modo de dominio

Aquí está la lista completa de los valores de -DomainMode que corresponden a cada versión de Windows Server y su numeración interna:

| :computer: Windows Server Version | :gear: Nombre Interno | :hash: Valor |
|-----------------------------------|-----------------------|--------------|
| Windows 2000 Server               | "Win2000"              | Valor 0      |
| Windows Server 2003               | "Win2003"              | Valor 2      |
| Windows Server 2008               | "Win2008"              | Valor 3      |
| Windows Server 2008 R2            | "Win2008R2"            | Valor 4      |
| Windows Server 2012               | "Win2012"              | Valor 5      |
| Windows Server 2012 R2            | "Win2012R2"            | Valor 6      |
| Windows Server 2016               | "Win2016"              | Valor 7      |
| Windows Server 2019               | "Win2019"              | Valor 8      |
| Windows Server 2022               | "Win2022"              | Valor 9      |

Estos valores se utilizan para configurar el nivel funcional del dominio, asegurando la compatibilidad y las funcionalidades de Active Directory adecuadas para cada versión del servidor.

## Configuración del Dominio

- -DomainName "vuln.internal "
- -DomainNetbiosName "vuln"
- -UsersLimit 20

### Comandos en Windows Server 2016 

Si aún no ha instalado Active Directory, puede probar

# Instalar la característica de AD DS: 
```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

# Importar el módulo ADDSDeployment:
```powershell
Import-Module ADDSDeployment
```

# Instalar el directorio activo:
```powershell
Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath "C:\\Windows\\NTDS" -DomainMode "7" -DomainName "vuln.internal " -DomainNetbiosName "vuln" -ForestMode "7" -InstallDns:$true -LogPath "C:\\Windows\\NTDS" -NoRebootOnCompletion:$false -SysvolPath "C:\\Windows\\SYSVOL" -Force:$true
```

if you already installed Active Directory, just run the script !

# Forzar TLS:
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

# Ejecutar script:
```powershell
IEX((new-object net.webclient).downloadstring("https://raw.githubusercontent.com/AAAAAEXQOSyIpN2JZ0ehUQ/vulnerable-AD-plus/refs/heads/master/vulnadplus.ps1")); Invoke-VulnAD -UsersLimit 20 -DomainName "vuln.internal "
```

:warning: Disclaimer: Este script es solo para uso educativo y personal. No lo utilices para acceder a redes de terceros sin autorización, ya que esto es ilegal y contrario a los términos de uso de este proyecto.

## :email: Contacto 
* :busts_in_silhouette: **Hossam**: [GitHub](https://github.com/safebuffer/vulnerable-AD) - Desarrollador Vuln ad plus
* :busts_in_silhouette: **WaterExecution**: [GitHub](https://github.com/WaterExecution/vulnerable-AD-plus) - Actualización de versión
* :busts_in_silhouette: **Dzhoni_dev**: [GitHub](https://github.com/AAAAAEXQOSyIpN2JZ0ehUQ/Wifite-Utility) - Contribución Readme

☆ https://t.me/AAAAAEXQOSyIpN2JZ0ehUQ [  ⃘⃤꙰✰ ] ☆
