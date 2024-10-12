 <h1 align="center">
  Vulnerable-AD-Plus
  <br>
</h1>

# Vuln AD Plus :octocat:

## Información
Vulnerable-AD-Plus es un entorno de laboratorio diseñado para simular un Directorio Activo vulnerable, permitiendo practicar y probar diversos ataques en un entorno controlado. Ideal para pruebas de penetración y formación en seguridad.

## Características Principales
- Escenario de pruebas para ataques aleatorios al Directorio Activo.
- Cobertura completa de los ataques comunes en AD.
- Requiere ejecutar el script en un Controlador de Dominio con AD instalado.
- Algunos ataques necesitan una estación de trabajo de cliente adicional.

## Redacción
Incluye una sección dedicada a reseñas y soluciones: WriteUp.

## Ataques Admitidos
- Abuso de ACL/ACE
- Kerberoasting
- AS-REP Roasting
- Abuso de DnsAdmins (...)
- Contraseñas en comentarios de usuarios de AD
- Pulverización de contraseñas
- Sincronización de DC (DCSync) (...)
- Ataques de Ticket Plata (...)
- Ataques de Ticket Dorado (...)
- Pass-the-Hash (...)
- Pass-the-Ticket (...)
- Firma SMB deshabilitada
- Permisos inseguros de WinRM
- Consultas LDAP anónimas
- Compartición pública de SMB
- Zerologon (verificar versión)

## Configuración del Dominio
- -DomainName: "vuln.internal"
- -DomainNetbiosName: "vuln"

## Comandos para Configurar en Windows Server 2016
### Si aún no has instalado Active Directory, ejecuta los siguientes comandos:

Instalar la Función de AD DS:
```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

Importar el Módulo de AD DS:
```powershell
Import-Module ADDSDeployment
```

Instalar el Directorio Activo:
```powershell
Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath "C:\Windows\NTDS" -DomainMode "7" -DomainName "vuln.internal" -DomainNetbiosName "vuln" -ForestMode "7" -InstallDns:$true -LogPath "C:\Windows\NTDS" -NoRebootOnCompletion:$false -SysvolPath "C:\Windows\SYSVOL" -Force:$true
```

### Si ya tienes Active Directory instalado, simplemente ejecuta el script:

Forzar TLS:
```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

Ejecutar el Script:
```powershell
IEX((new-object net.webclient).downloadstring("https://raw.githubusercontent.com/kvlx-alt/vulnerable-AD-plus/master/vulnadplus.ps1")); Invoke-VulnAD -UsersLimit 20 -DomainName "vuln.internal"
```

## Valores para Modo de Dominio
Los valores de -DomainMode que corresponden a cada versión de Windows Server son:
- Windows 2000 Server: "Win2000" (Valor 0)
- Windows Server 2003: "Win2003" (Valor 2)
- Windows Server 2008: "Win2008" (Valor 3)
- Windows Server 2008 R2: "Win2008R2" (Valor 4)
- Windows Server 2012: "Win2012" (Valor 5)
- Windows Server 2012 R2: "Win2012R2" (Valor 6)
- Windows Server 2016: "Win2016" (Valor 7)
- Windows Server 2019: "Win2019" (Valor 8)
- Windows Server 2022: "Win2022" (Valor 9)

Estos valores configuran el nivel funcional del dominio para garantizar la compatibilidad y las funciones adecuadas para cada versión de Windows Server.
