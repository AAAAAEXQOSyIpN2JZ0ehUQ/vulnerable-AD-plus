# Vuln ad plus :octocat:
Vulnerable-AD-Plus

## :information_source: Descripción
Cree un directorio activo vulnerable que le permita probar la mayoría de los ataques al directorio activo en el laboratorio local.

## :star2: Características principales

- Ataques aleatorios
- Cobertura total de los ataques mencionados.
- necesita ejecutar el script en DC con Active Directory instalado 
- Algunos de los ataques requieren una estación de trabajo del cliente.
- 
## :bookmark_tabs: Redacción

Ahora incluye una sección de reseñas [**WriteUp**](WriteUp).

## :computer: Ataques admitidos

- Abusar de las ACL/ACE
- Kerberoasting
- Tostado AS-REP
- Abuso de DnsAdmins (...)
- Contraseña en el comentario del usuario AD
- Pulverización de contraseñas
- DCSincronización (...)
- Billete Plata (...)
- Billete Dorado (...)
- Pasar el hash (...)
- Pase el billete (...)
- Firma SMB deshabilitada
- Mal permiso de WinRM
- Consulta LDAP anónima
- Participación pública de PYMES
- Zerologon (Verificar versión)

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
IEX((new-object net.webclient).downloadstring("https://raw.githubusercontent.com/kvlx-alt/vulnerable-AD-plus/master/vulnadplus.ps1")); Invoke-VulnAD -UsersLimit 20 -DomainName "vuln.internal "
```

### Modo de dominio

Aquí está la lista completa de los valores de -DomainMode que corresponden a cada versión de Windows Server y su numeración interna:

- Windows 2000 Server: "Win2000" (Valor 0)
- Windows Server 2003: "Win2003" (Valor 2)
- Windows Server 2008: "Win2008" (Valor 3)
- Windows Server 2008 R2: "Win2008R2" (Valor 4)
- Windows Server 2012: "Win2012" (Valor 5)
- Windows Server 2012 R2: "Win2012R2" (Valor 6)
- Windows Server 2016: "Win2016" (Valor 7)
- Windows Server 2019: "Win2019" (Valor 8)
- Windows Server 2022: "Win2022" (Valor 9)

Estos valores se utilizan para configurar el nivel funcional del dominio, asegurando la compatibilidad y las funcionalidades de Active Directory adecuadas para cada versión del servidor.
