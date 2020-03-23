
## Taller Clase 4 
                                     
**Alejandro Peña Tsukamoto**
**A00014140**


**PN°1**

Mostrar una tabla de procesos que incluya únicamente los nombres de los procesos, sus IDs, y 
si están respondiendo a Windows (la propiedad Responding muestra eso). Haga que la tabla tome el 
mínimo de espacio horizontal, pero no permita que la información se trunque.

` PS C:\Users\USUARIO> Get-Process | select name,id,responding | ft -Wrap `

Resultado: 

Name                                                              Id Responding
----                                                              -- ----------
aips                                                            3268       True
ApplicationFrameHost                                           11200       True
AppVShNotify                                                    3424       True
conhost                                                        14616       True
csrss                                                            772       True
csrss                                                            880       True
ctfmon                                                         10020       True
dasHost                                                         7188       True
dasHost                                                         7912       True
DAX3API                                                         4352       True
DAX3API                                                         6468       True
dllhost                                                         8380       True
dllhost                                                        13120       True
dwm                                                             1396       True
eclipse                                                          640       True
jhi_service                                                     5688       True
jusched                                                        14024       True
LMIGuardianSvc                                                  4464       True
LockApp                                                         4544       True
lsass                                                            964       True
Memory Compression                                              2624       True
Microsoft.Photos                                               13964       True
MicrosoftEdge                                                  13016      False
MicrosoftEdgeCP                                                 3704      False
MicrosoftEdgeSH                                                14668       True
MsMpEng                                                         8132       True
netcut_windows                                                  3584       True
NisSrv                                                         14060       True
NVDisplay.Container                                             2132       True
NVDisplay.Container                                             3956       True
NvTelemetryContainer                                            4392       True
OfficeClickToRun                                                1528       True
powershell_ise                                                 15184       True
winlogon                                                         112       True
WmiPrvSE                                                        6404       True
WUDFHost                                                        1100       True
WUDFHost                                                        1320       True
YourPhone                                                      11828       True
YourPhoneServer                                                10068       True

**PN°2**

Muestre una tabla de procesos que incluya los nombres de los procesos y sus IDs. También incluya 
columnas para uso de memoria virtual y física; exprese dichos valores en megabytes (MB).

`PS C:\Users\USUARIO> Get-Process | ft -Property name, id, @{n='VM (MB)'; e={$_.VM / 1MB -as [int]}}, @{n='PM (MB)' ; e={$_.PM / 1MB -as [int]}}`

`Name                                                              Id VM (MB) PM (MB)
----                                                              -- ------- -------
aips                                                            3268      78       4
ApplicationFrameHost                                           11200 2101521      27
AppVShNotify                                                    3424    4191       2
audiodg                                                         9240 2101361      13
chrome                                                          2012 2105755      28
chrome                                                          2684 2105767      18
chrome                                                         17232 2105702      12
CompPkgSrv                                                      1928 2101341       2
conhost                                                        13612 2101356       6
conhost                                                        14616 2101370       6
csrss                                                            772 2101341       2
csrss                                                            880 2101406       3
ctfmon                                                         10020 2101399       6
dasHost                                                         7188 2101336       5
dasHost                                                         7912 2101301       1
DAX3API                                                         4352    4677      26
DAX3API                                                         6468    4209       2
dllhost                                                         8380 2101596       3
dllhost                                                        13120 2101620       5
dwm                                                             1396 2101707      71
eclipse                                                          640   39987    1058
esif_uf                                                         4360 2101313       2
explorer                                                        8960 2102059      87
FMService64                                                     4208    4167       1
fontdrvhost                                                     1072 2101444       4
fontdrvhost                                                     1080 2101342       2`

**PN°3**

Emplee Get-EventLog para mostrar una lista de los logs de eventos disponibles (revise la ayuda para encontrar 
el parámetro que le permitirá obtener dicha información). Formatee la salida como una tabla que incluya el nombre 
de despliegue del log y el período de retención. Los encabezados de columna deben ser NombreLog y Per-Retencion.


`PS C:\Users\USUARIO> Get-EventLog -List | fl -Property @{n='nombreLog'; e={$_.Log}}, @{n='Per-Retencion';e={$_.minimumRetentionDays}}`


`nombreLog     : Application
Per-Retencion : 0

nombreLog     : HardwareEvents
Per-Retencion : 0

nombreLog     : Internet Explorer
Per-Retencion : 7

nombreLog     : Key Management Service
Per-Retencion : 0

nombreLog     : OAlerts
Per-Retencion : 0

nombreLog     : PreEmptive
Per-Retencion : 7

nombreLog     : Security
Per-Retencion : 

nombreLog     : System
Per-Retencion : 0

nombreLog     : Windows Azure
Per-Retencion : 7

nombreLog     : Windows Power`

**PN°4**

Muestre una lista de servicios, de tal manera que aparezcan agrupados los servicios que están iniciados 
y los que están detenidos. Los que están iniciados deben aparecer primero.


`PS C:\Users\USUARIO> Get-Service |Sort-Object status | fl -GroupBy status`


`Name                : PerfHost
DisplayName         : DLL de host del Contador de rendimiento
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {RPCSS}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32OwnProcess

Name                : PushToInstall
DisplayName         : Servicio PushToInstall de Windows
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {rpcss}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32OwnProcess, Win32ShareProcess

Name                : RasAuto
DisplayName         : Administrador de conexiones automáticas de acceso remoto
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {RasAcd}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32ShareProcess

Name                : RemoteAccess
DisplayName         : Enrutamiento y acceso remoto
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {Http, RasMan, RpcSS, Bfe}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32ShareProcess

Name                : RemoteRegistry
DisplayName         : Registro remoto
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {RPCSS}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32ShareProcess`

**PN°5**

Mostrar una lista a cuatro columnas de todos los directorios que están en el raíz de la unidad C:


`PS C:\Users\USUARIO> ls -Path C:\ -Attributes directory| fw -Column 4`

`    Directorio: C:\



BIOS                           Drivers                        Intel                          PerfLogs                      
Program Files                  Program Files (x86)            Users                          Windows                       
`

**PN°6**

Cree una lista formateada de todos los archivos .exe del directorio C:\Windows. Debe mostrarse el nombre, la información 
de versión, y el tamaño del archivo. La propiedad de tamaño se llama length en Powershell, pero para mayor claridad,
la columna se debe llamar Tamaño en su listado.



`PS C:\Users\USUARIO> ls -Path C:\Windows |where -filter {$_.Name -like "*.exe"} | fl -Property name, @{n='tamaño';e={$_.length}}, versionInfo`

`
Name        : bfsvc.exe
tamaño      : 78848
VersionInfo : File:             C:\Windows\bfsvc.exe
              InternalName:     bfsvc.exe
              OriginalFilename: bfsvc.exe.mui
              FileVersion:      10.0.17763.1091 (WinBuild.160101.0800)
              FileDescription:  Utilidad de servicio de actualización del archivo de arranque
              Product:          Sistema operativo Microsoft® Windows®
              ProductVersion:   10.0.17763.1091
              Debug:            False
              Patched:          False
              PreRelease:       False
              PrivateBuild:     False
              SpecialBuild:     False
              Language:         Español (España, internacional)
              

Name        : explorer.exe
tamaño      : 4417008
VersionInfo : File:             C:\Windows\explorer.exe
              InternalName:     explorer
              OriginalFilename: EXPLORER.EXE.MUI
              FileVersion:      10.0.17763.1091 (WinBuild.160101.0800)
              FileDescription:  Explorador de Windows
              Product:          Sistema operativo Microsoft® Windows®
              ProductVersion:   10.0.17763.1091
              Debug:            False
              Patched:          False
              PreRelease:       False
              PrivateBuild:     False
              SpecialBuild:     False
              Language:         Español (España, internacional)
              
`


**PN°7**

Importe el módulo NetAdapter (empleando el comando Import-Module NetAdapter). Empleando el cmdlet Get-NetAdapter, 
muestre una lista de adaptadores no virtuales (adaptadores cuya propiedad Virtual sea falsa. 
El valor lógico falso es representado por Powershell como $False).


`PS C:\Users\USUARIO> Get-NetAdapter | Where -filter {$_.Virtual -eq $false} |fl`

`
Name                       : Ethernet 2
InterfaceDescription       : TAP-Windows Adapter V9
InterfaceIndex             : 21
MacAddress                 : 00-FF-E9-C4-4C-99
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Down
AdminStatus                : Up
LinkSpeed(Mbps)            : 100
MediaConnectionState       : Disconnected
ConnectorPresent           : False
DriverInformation          : Driver Date 2016-04-21 Version 9.0.0.21 NDIS 6.1

Name                       : Ethernet
InterfaceDescription       : Realtek PCIe GbE Family Controller
InterfaceIndex             : 20
MacAddress                 : E8-6A-64-49-A5-C5
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Down
AdminStatus                : Up
LinkSpeed(Mbps)            : 0
MediaConnectionState       : Disconnected
ConnectorPresent           : True
DriverInformation          : Driver Date 2018-03-28 Version 10.26.328.2018 NDIS 6.40

Name                       : Npcap Loopback Adapter
InterfaceDescription       : Npcap Loopback Adapter
InterfaceIndex             : 18
MacAddress                 : 02-00-4C-4F-4F-50
MediaType                  : 802.3
PhysicalMediaType          : Unspecified
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Gbps)            : 1.2
MediaConnectionState       : Connected
ConnectorPresent           : True
DriverInformation          : Driver Date 2006-06-21 Version 10.0.17763.1 NDIS 6.30`

**PN°8**

Importe el módulo DnsClient. Empleando el cmdlet Get-DnsClientCache, muestre una lista de los registros A y AAAA 
que estén en el caché. Sugerencia: Si el caché está vacío, visite algunos sitios web para poblarlo.


`PS C:\Users\USUARIO> Get-DnsClientCache | where -filter {$_.Type -eq (28 ) -or $_.Type -eq 1} |fl`

`
Entry      : bid.g.doubleclick.net
RecordName : ads-bid.l.doubleclick.net
RecordType : A
Status     : Success
Section    : Answer
TimeToLive : 33
DataLength : 4
Data       : 173.194.217.156

Entry      : sync.outbrain.com
RecordName : sadc1.outbrain.org
RecordType : A
Status     : Success
Section    : Answer
TimeToLive : 290
DataLength : 4
Data       : 66.225.223.127

`

**PN°9**

Genere una lista de todos los archivos .exe del directorio C:\Windows\System32 que tengan más de 5 MB.


`C:\Users\USUARIO> ls -Path C:\Windows\System32 | where -filter {$_.Name -like "*exe"} | WHERE -filter {$_.length/1MB -gt 5}`


`
    Directorio: C:\Windows\System32


Mode                LastWriteTime         Length Name                                                                      
----                -------------         ------ ----                                                                      
-a----    12/03/2020  10:55 p. m.      121542864 MRT.exe                                                                   
-a----     15/09/2018  2:28 a. m.        6784512 mspaint.exe                                                               
-a----    12/03/2020  10:53 p. m.        9672208 ntoskrnl.exe                                                              
-a----     31/03/2019  1:21 a. m.        5732352 VsGraphicsDesktopEngine.exe                                               

`

**PN°10**

Muestre una lista de parches que sean actualizaciones de seguridad.


`PS C:\Users\USUARIO> Get-HotFix | where -filter {$_.description -like "*security*"} |fl`

`

Description         : Security Update
FixComments         : 
HotFixID            : KB4470788
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 30/03/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4493510
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 10/04/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4499728
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 17/05/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4504369
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 21/06/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4509095
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 1/08/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4512577
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 11/09/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4512937
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 13/08/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4516115
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 12/09/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4521862
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 8/10/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4523204
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 13/11/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4537759
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 22/02/2020 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4539571
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 13/03/2020 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4538461
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 22/03/2020 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 
`

**PN°11**

Muestre una lista de parches que hayan sido instalados por el usuario Administrador, que sean actualizaciones. 
Si no tiene ninguno, busque parches instalados por el usuario System. Note que algunos parches no tienen valor
en el campo Installed By.



`PS C:\Users\USUARIO> Get-HotFix | where -filter {$_.installedBy -like "*SYSTEM*"} |fl`

`
Description         : Update
FixComments         : 
HotFixID            : KB4534131
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 22/02/2020 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Update
FixComments         : 
HotFixID            : KB4465065
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 21/06/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 

Description         : Security Update
FixComments         : 
HotFixID            : KB4470788
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 30/03/2019 12:00:00 a. m.
Name                : 
ServicePackInEffect : 
Status              : 
`

**PN°12**

Genere una lista de todos los procesos que estén corriendo con el nombre Conhost o Svchost.


`PS C:\Users\USUARIO> Get-Process | where -filter {$_.Name -eq "Conhost" -or $_.Name -eq "Svchost"} | fl`

`
Id      : 13612
Handles : 150
CPU     : 
SI      : 0
Name    : conhost

Id      : 14616
Handles : 122
CPU     : 
SI      : 1
Name    : conhost

Id      : 992
Handles : 85
CPU     : 
SI      : 0
Name    : svchost

Id      : 1048
Handles : 1255
CPU     : 
SI      : 0
Name    : svchost
`
