![logo](https://github.com/AAAAAEXQOSyIpN2JZ0ehUQ/vulnerable-AD-plus/blob/master/Imagenes/vulnerable-AD-plus.png)

# Vulnerable AD Plus :octocat:
Vuln ad plus

## :information_source: Descripción
Crea un directorio activo vulnerable que le permite probar la mayoría de los ataques al directorio activo en el laboratorio local.

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

## :globe_with_meridians: Modo de dominio

Aquí está la lista completa de los valores de -DomainMode que corresponden a cada versión de Windows Server y su numeración interna:

| :computer: Windows Server Version | :gear: Nombre Interno | :hash: Valor | :link: Enlace de Descarga                       |
|-----------------------------------|-----------------------|--------------|---------------------------------------------|
| Windows 2000 Server               | "Win2000"              | Valor 0      | [Descargar Windows 2000 Server](#)          |
| Windows Server 2003               | "Win2003"              | Valor 2      | [Descargar Windows Server 2003](#)          |
| Windows Server 2008               | "Win2008"              | Valor 3      | [Descargar Windows Server 2008](#)          |
| Windows Server 2008 R2            | "Win2008R2"            | Valor 4      | [Descargar Windows Server 2008 R2](#)       |
| Windows Server 2012               | "Win2012"              | Valor 5      | [Descargar Windows Server 2012](#)          |
| Windows Server 2012 R2            | "Win2012R2"            | Valor 6      | [Descargar Windows Server 2012 R2](https://www.microsoft.com/es-es/evalcenter/download-windows-server-2012-r2)       |
| Windows Server 2016               | "Win2016"              | Valor 7      | [Descargar Windows Server 2016](https://www.microsoft.com/es-mx/evalcenter/download-windows-server-2016)          |
| Windows Server 2019               | "Win2019"              | Valor 8      | [Descargar Windows Server 2019](https://www.microsoft.com/es-mx/evalcenter/download-windows-server-2019)          |
| Windows Server 2022               | "Win2022"              | Valor 9      | [Descargar Windows Server 2022](https://www.microsoft.com/es-mx/evalcenter/download-windows-server-2022)          |

Estos valores se utilizan para configurar el nivel funcional del dominio, asegurando la compatibilidad y las funcionalidades de Active Directory adecuadas para cada versión del servidor.

## :gear: Configuración del Dominio

- **`-DomainMode "7"`**: Establece el nivel funcional del dominio en Windows Server 2016, garantizando que las características del dominio sean compatibles con esta versión.
- **`-DomainName "vuln.internal"`**: Define el nombre completo del dominio en formato FQDN (Fully Qualified Domain Name). En este caso, el dominio será vuln.internal.
- **`-DomainNetbiosName "vuln"`**: Configura el nombre NetBIOS, que es una versión corta del nombre del dominio utilizada para compatibilidad con sistemas que no admiten nombres FQDN.
- **`-ForestMode "7"`**: Establece el nivel funcional del bosque en Windows Server 2016, habilitando las características específicas de esta versión y anteriores.
- **`-UsersLimit 100`**: Especifica un límite máximo de usuarios en el dominio. Aquí, se establece un máximo de 100 usuarios.

## :computer: Comandos en Windows Server 2016 

Si aún no ha instalado Active Directory, puede probar

**Instalar la característica de AD DS:** 
```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

**Importar el módulo ADDSDeployment:**
```powershell
Import-Module ADDSDeployment
```

## :gear: Configuración del Bosque y Dominio
```textplain
New-ADForest `
    -ForestMode "7" ` # Nivel funcional del bosque (Windows Server 2016)
    -DomainMode "7" ` # Nivel funcional del dominio (Windows Server 2016)
    -DomainName "vuln.internal" ` # Nombre completo del dominio (FQDN)
    -DomainNetbiosName "vuln" ` # Nombre NetBIOS del dominio
    -UsersLimit 100 # Límite máximo de usuarios en el dominio (recomendado de usuarios entre 20 y 40)
```

**Instalar el directorio activo:**
```powershell
Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath "C:\\Windows\\NTDS" -DomainMode "7" -DomainName "vuln.internal " -DomainNetbiosName "vuln" -ForestMode "7" -InstallDns:$true -LogPath "C:\\Windows\\NTDS" -NoRebootOnCompletion:$false -SysvolPath "C:\\Windows\\SYSVOL" -Force:$true
```

Si ya instalaste Active Directory, ¡simplemente ejecuta el script!

**Forzar TLS:**
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

**Ejecutar script:**
```powershell
IEX((new-object net.webclient).downloadstring("https://raw.githubusercontent.com/AAAAAEXQOSyIpN2JZ0ehUQ/vulnerable-AD-plus/refs/heads/master/vulnadplus.ps1")); Invoke-VulnAD -UsersLimit 20 -DomainName "vuln.internal "
```

:warning: Disclaimer: Este script es solo para uso educativo y personal. No lo utilices para acceder a redes de terceros sin autorización, ya que esto es ilegal y contrario a los términos de uso de este proyecto.

## :email: Contacto 
* :busts_in_silhouette: **Hossam**: [GitHub](https://github.com/safebuffer/vulnerable-AD) - Desarrollador Vuln ad plus
* :busts_in_silhouette: **WaterExecution**: [GitHub](https://github.com/WaterExecution/vulnerable-AD-plus) - Actualización de versión
* :busts_in_silhouette: **kvlx-alt**: [YouTube](https://www.youtube.com/watch?v=s9dD_nINnkc&t=876s) - Contribución Video tutorial
* :busts_in_silhouette: **Dzhoni**: [GitHub](https://github.com/AAAAAEXQOSyIpN2JZ0ehUQ/vulnerable-AD-plus?tab=readme-ov-file) - Contribución Readme

☆ https://t.me/AAAAAEXQOSyIpN2JZ0ehUQ [  ⃘⃤꙰✰ ] ☆
