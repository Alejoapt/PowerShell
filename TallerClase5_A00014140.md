## Taller Clase 5 
                                     
**Alejandro Peña Tsukamoto**
**A00014140**


**PN°1**

¿Cuál clase puede emplearse para consultar la dirección IP de un adaptador de red? ¿Posee dicha clase algún método para liberar un préstamo de dirección (lease) DHCP?

La clase que puede emplearse para consultar la dirección ip de un adaptador red es  win32_NetworkAdapterconfiguration. Esta clase no posee un metodo predefinido, sin embargo, 
podemos definirlo con el siguiente cmdlet

`PS C:\Users\USUARIO> Get-CimInstance win32_networkadapterconfiguration | Select-Object IP` 

```
Description             : Microsoft Kernel Debug Network Adapter
Index                   : 0
IPAddress               : 
IPConnectionMetric      : 
IPEnabled               : False
IPFilterSecurityEnabled : 

Description             : Realtek 8822BE Wireless LAN 802.11ac PCI-E NIC
Index                   : 1
IPAddress               : {192.168.0.16, fe80::d5f8:1e0b:fb06:4c9d}
IPConnectionMetric      : 50
IPEnabled               : True
IPFilterSecurityEnabled : False

Description             : Bluetooth Device (Personal Area Network)
Index                   : 2
IPAddress               : 
IPConnectionMetric      : 
IPEnabled               : False
IPFilterSecurityEnabled : 
```


**PN°2**

Despliegue una lista de parches empleando WMI (Microsoft se refiere a los parches con el nombre quick-fix engineering). Es diferente el listado al que produce el cmdlet Get-Hotfix?

`PS C:\Users\USUARIO> Get-WmiObject win32_quickfixengineering`


```
Source        Description      HotFixID      InstalledBy          InstalledOn              
------        -----------      --------      -----------          -----------              
DESKTOP-SR... Update           KB4534131     NT AUTHORITY\SYSTEM  22/02/2020 12:00:00 a. m.
DESKTOP-SR... Update           KB4465065     NT AUTHORITY\SYSTEM  21/06/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4470788     NT AUTHORITY\SYSTEM  30/03/2019 12:00:00 a. m.
DESKTOP-SR... Update           KB4480056     NT AUTHORITY\SYSTEM  30/03/2019 12:00:00 a. m.
DESKTOP-SR... Update           KB4486153     NT AUTHORITY\SYSTEM  25/08/2019 12:00:00 a. m.
DESKTOP-SR... Update           KB4486161     NT AUTHORITY\SYSTEM  1/10/2019 12:00:00 a. m. 
DESKTOP-SR... Security Update  KB4493510     NT AUTHORITY\SYSTEM  10/04/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4499728     NT AUTHORITY\SYSTEM  17/05/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4504369     NT AUTHORITY\SYSTEM  21/06/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4509095     NT AUTHORITY\SYSTEM  1/08/2019 12:00:00 a. m. 
DESKTOP-SR... Security Update  KB4512577     NT AUTHORITY\SYSTEM  11/09/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4512937     NT AUTHORITY\SYSTEM  13/08/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4516115     NT AUTHORITY\SYSTEM  12/09/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4521862     NT AUTHORITY\SYSTEM  8/10/2019 12:00:00 a. m. 
DESKTOP-SR... Security Update  KB4523204     NT AUTHORITY\SYSTEM  13/11/2019 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4537759     NT AUTHORITY\SYSTEM  22/02/2020 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4539571     NT AUTHORITY\SYSTEM  13/03/2020 12:00:00 a. m.
DESKTOP-SR... Security Update  KB4538461     NT AUTHORITY\SYSTEM  22/03/2020 12:00:00 a. m.
```

**PN°3**

Empleando WMI, muestre una lista de servicios, que incluya su status actual, su modalidad de inicio, y las cuentas que emplean para hacer login.

`PS C:\Users\USUARIO> Get-WmiObject win32_service | Select-Object status, startmode, systemname`

```
status  startmode systemname     
------  --------- ----------     
OK      Auto      DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Auto      DESKTOP-SRK1PNA
OK      Auto      DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Manual    DESKTOP-SRK1PNA
OK      Auto      DESKTOP-SRK1PNA
```


**PN°4**

Empleando cmdlets de CIM, liste todas las clases del namespace SecurityCenter2, que tengan product como parte del nombre.

`PS C:\Users\USUARIO> Get-CimClass -Namespace root/SecurityCenter2 | where -Filter {$_.CimClassName -like "*product*"}`

```
   NameSpace: ROOT/SecurityCenter2

CimClassName                        CimClassMethods      CimClassProperties                                                
------------                        ---------------      ------------------                                                
AntiSpywareProduct                  {}                   {displayName, instanceGuid, pathToSignedProductExe, pathToSigne...
AntiVirusProduct                    {}                   {displayName, instanceGuid, pathToSignedProductExe, pathToSigne...
FirewallProduct                     {}                   {displayName, instanceGuid, pathToSignedProductExe, pathToSigne...

```

**PN°5**

Empleando cmdlets de CIM, y los resultados del ejercicio anterior, muestre los nombres de las aplicaciones antispyware instaladas en el sistema. 
También puede consultar si hay productos antivirus instalados en el sistema.

`PS C:\Users\USUARIO> Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntiVirusProduct | Select-Object displayName`

```
displayName     
-----------     
Windows Defender
```