---
title: "attività di avvio aaaCommon per i servizi Cloud | Documenti Microsoft"
description: "Vengono forniti alcuni esempi comuni delle attività di avvio è tooperform nel ruolo web di servizi cloud o del ruolo di lavoro."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>Attività di avvio comuni del servizio cloud
In questo articolo vengono forniti alcuni esempi comuni delle attività di avvio è tooperform nel servizio cloud. È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo. Le operazioni che è possibile tooperform includono l'installazione di un componente, la registrazione dei componenti COM, impostano le chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata. 

Vedere [questo articolo](cloud-services-startup-tasks.md) toounderstand funzionamento delle attività di avvio, e in particolare come toocreate hello voci che definiscono un'attività di avvio.

> [!NOTE]
> Attività di avvio non sono applicabili tooVirtual macchine, solo tooCloud servizio Web e ruoli di lavoro.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Definire le variabili di ambiente prima dell'avvio di un ruolo
Se è necessario variabili di ambiente definite per un'attività specifica, utilizzare hello [ambiente] elemento all'interno di hello [attività] elemento.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Le variabili possono anche utilizzare un [valore XPath di Azure valido](cloud-services-role-config-xpath.md) tooreference qualcosa sulla distribuzione di hello. Anziché utilizzare hello `value` attributo, definire un [RoleInstanceValue] elemento figlio.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Configurare l'avvio IIS con AppCmd.exe
Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) strumento da riga di comando può essere utilizzato toomanage le impostazioni di IIS all'avvio in Azure. *AppCmd.exe* fornisce le impostazioni di tooconfiguration ideale della riga di comando di accesso per l'utilizzo nelle attività di avvio in Azure. Tramite *AppCmd.exe*è possibile aggiungere, modificare o rimuovere impostazioni per applicazioni e siti Web.

Tuttavia, esistono alcuni aspetti toowatch, out per uso hello di *AppCmd.exe* come attività di avvio:

* Le attività di avvio possono essere eseguite più di una volta tra un riavvio e l'altro. Ad esempio, quando un ruolo viene riciclato.
* Se eseguita più volte, l'azione *AppCmd.exe* potrebbe generare un errore. Ad esempio, il tentativo di troppo tooadd una sezione*Web. config* due volte è stato possibile generare un errore.
* Le attività di avvio danno esito negativo se restituiscono un codice di uscita o un valore di **errorlevel**diverso da zero. Ad esempio, quando *AppCmd.exe* genera un errore.

È un hello toocheck buona norma **errorlevel** dopo la chiamata *AppCmd.exe*, che è facile toodo se si esegue il wrapping di chiamate hello troppo*AppCmd.exe* con un *cmd*  file. Se si rileva un valore di **errorlevel** noto, è possibile ignorarlo oppure restituirlo.

Hello errorlevel restituito da *AppCmd.exe* sono elencati nel file Winerror hello e possono essere visualizzati anche nel [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Esempio di gestione a livello di errore hello
In questo esempio aggiunge una sezione di compressione e una voce di compressione per JSON toohello *Web. config* file, con la gestione e registrazione degli errori.

le sezioni pertinenti di hello Hello [Servicedefinition] file riportati di seguito, che includono l'impostazione di hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attributo troppo`elevated` toogive *AppCmd.exe*  sufficiente toochange hello le impostazioni delle autorizzazioni in hello *Web. config* file:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Hello *Startup.cmd* batch utilizza file *AppCmd.exe* tooadd una sezione di compressione e una voce di compressione per JSON toohello *Web. config* file. Hello previsto **errorlevel** di 183 viene impostato utilizzando hello verificare toozero. Programma della riga di comando eseguibile. Valori di ERRORLEVEL imprevisti vengono registrati tooStartupErrorLog.txt.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>Aggiungere regole di firewall
In Azure sono disponibili due firewall. Hello prima controlla le connessioni tra macchine virtuali hello e hello world di fuori. Questo firewall è controllato da hello [endpoint] elemento hello [Servicedefinition] file.

Hello secondo controlla le connessioni tra macchine virtuali hello e processi hello all'interno di tale macchina virtuale. Questo firewall può essere controllato dal hello `netsh advfirewall firewall` strumento da riga di comando.

Azure crea regole del firewall per hello processi avviati nei ruoli. Ad esempio, quando si avvia un servizio o un programma, Azure crea automaticamente tooallow di regole firewall necessarie hello toocommunicate tale servizio con hello Internet. Tuttavia, se si crea un servizio che viene avviato da un processo esterno al ruolo (ad esempio, un servizio COM+ o un'attività pianificata di Windows), è necessario toomanually creare un servizio di toothat firewall regola tooallow accesso. Queste regole di firewall possono essere create usando un'attività di avvio.

In un'attività di avvio che crea una regola di firewall l'attributo [executionContext][attività] deve essere impostato su **elevato** diverso da zero. Aggiungere hello dopo l'avvio attività toohello [Servicedefinition] file.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

regola del firewall hello tooadd, è necessario utilizzare hello appropriato `netsh advfirewall firewall` comandi nel file batch di avvio. In questo esempio, attività di avvio hello richiede protezione e crittografia per la porta TCP 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Bloccare un indirizzo IP specifico
È possibile limitare un set di tooa accesso ruolo web di Azure di indirizzi IP specificati modificando il server IIS **Web. config** file. È inoltre necessario disporre di un file di comando che consente di sbloccare hello toouse **ipSecurity** sezione di hello **applicationHost. config** file.

toodo sbloccare hello **ipSecurity** sezione di hello **applicationHost. config** file, creare un file di comando che viene eseguita all'avvio del ruolo. Creare una cartella a livello di radice hello del ruolo web chiamato **avvio** e, in questa cartella, creare un file batch denominato **startup.cmd**. Aggiungere il progetto di Visual Studio tooyour file e impostare le proprietà di hello troppo**Copia sempre** tooensure viene incluso nel pacchetto.

Aggiungere hello dopo l'avvio attività toohello [Servicedefinition] file.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

Aggiungere questo toohello comando **startup.cmd** file:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Questa attività, hello **startup.cmd** batch toobe file eseguito ogni volta che viene inizializzato ruolo web hello, assicurando che hello necessario **ipSecurity** sezione è sbloccata.

Infine, modificare hello [sezione System. webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) del ruolo web **Web. config** file tooadd un elenco di indirizzi IP autorizzati ad accedere, come illustrato nell'esempio seguente hello:

Questa configurazione di esempio **consente** tutti gli indirizzi IP tooaccess hello server ad eccezione del fatto hello due definite

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

Questa configurazione di esempio **Nega** tutti gli indirizzi IP di accedere ai server hello tranne hello due definito.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>Creare un'attività di avvio di PowerShell
Script di Windows PowerShell non possono essere chiamati direttamente dal hello [Servicedefinition] file, ma possono essere richiamati da un file batch di avvio.

Per impostazione predefinita, in PowerShell non vengono eseguiti script non firmati. A meno che non si firma lo script, è necessario tooconfigure PowerShell toorun script non firmati. toorun script non firmati, hello **ExecutionPolicy** deve essere impostato troppo**Unrestricted**. Hello **ExecutionPolicy** impostazione uso si basa sulla versione di hello di Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Se si utilizza un sistema operativo Guest che viene eseguito PowerShell 2.0 o 1.0 è possibile forzare toorun versione 2 e se non è disponibile, utilizzare la versione 1.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Creare file nell'archiviazione locale da un'attività di avvio
È possibile utilizzare un toostore risorse di archiviazione locale i file creati dall'attività di avvio a cui si accede in un secondo momento dall'applicazione.

toocreate hello risorsa di archiviazione locale, aggiungere un [LocalResources] sezione toohello [Servicedefinition] file e quindi aggiungere hello [LocalStorage] elemento figlio. Assegnare un nome univoco e una dimensione appropriata risorsa di archiviazione locale hello per le attività di avvio.

toouse una risorsa di archiviazione locale nell'attività di avvio, è necessario un percorso risorse di archiviazione locale di ambiente tooreference variabile hello toocreate. Quindi hello attività di avvio e un'applicazione hello sono in grado di tooread e scrivere file di risorse di archiviazione locale toohello.

le sezioni pertinenti di hello Hello **Servicedefinition** file riportati di seguito:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

Ad esempio, questo **Startup.cmd** file batch utilizza hello **PathToStartupStorage** file hello toocreate variabile di ambiente **MyTest.txt** nell'archiviazione locale hello percorso.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

È possibile accedere dalla hello Azure SDK cartella di archiviazione locale tramite hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metodo.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Esecuzione nell'emulatore Windows hello o cloud
È possibile avere l'attività di avvio esegua passaggi diversi durante il funzionamento in toowhen cloud confrontati hello che è nell'emulatore di calcolo hello. Ad esempio, è consigliabile toouse una copia aggiornata dei dati SQL solo quando è in esecuzione nell'emulatore hello. In alternativa è possibile toodo alcune ottimizzazioni delle prestazioni per il cloud hello che non è necessario toodo durante l'esecuzione nell'emulatore hello.

Questa possibilità tooperform diverse azioni sul hello emulatore di calcolo e cloud hello può essere eseguita mediante la creazione di una variabile di ambiente in hello [Servicedefinition] file. e testare la variabile di ambiente su un valore durante l'attività di avvio.

variabile di ambiente hello toocreate aggiungere hello [variabile]/[RoleInstanceValue] elemento e creare un valore XPath di `/RoleEnvironment/Deployment/@emulated`. valore hello Hello **ComputeEmulatorRunning %** variabile di ambiente è `true` durante l'esecuzione nell'emulatore di calcolo, hello e `false` durante l'esecuzione nel cloud hello.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

attività Hello ora è possibile archiviare hello **ComputeEmulatorRunning %** azioni diverse tooperform variabile di ambiente in base che il ruolo di hello sia in esecuzione in hello cloud o hello emulatore. Di seguito è riportato uno script shell con estensione cmd che controlla la variabile di ambiente.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Rilevare se l'attività è già stata eseguita
ruolo Hello può riciclare senza riavvio causando nuovamente il toorun di attività di avvio. Non sussiste alcun tooindicate flag che un'attività è già stato eseguito nel hello ospita macchina virtuale. Per alcune attività non è importante se l'esecuzione avviene più volte. Tuttavia, è possibile eseguire una situazione in cui è necessario tooprevent in un'attività dall'esecuzione di più di una volta.

toodetect modo più semplice Hello che un'attività è già stato eseguito è un file di hello toocreate **% TEMP %** cartella quando l'attività hello ha esito positivo e osservare che hello di inizio dell'attività di hello. Di seguito è riportato uno script shell con estensione cmd di esempio che esegue automaticamente questa operazione.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>Procedure consigliate per l'attività
Di seguito sono riportate alcune procedure consigliate da seguire durante la configurazione dell'attività per il ruolo Web o di lavoro.

### <a name="always-log-startup-activities"></a>Registrare sempre le attività di avvio
Visual Studio non fornisce toostep un debugger tramite file batch, pertanto è buona tooget tutti i dati sull'operazione di hello dei file batch possibile. Output di hello dei file batch, di registrazione sia **stdout** e **stderr**possono fornire informazioni importanti quando si tenta di toodebug e correggere i file batch. entrambi toolog **stdout** e **stderr** file StartupLog.txt toohello in hello di hello directory punta tooby **% TEMP %** variabile di ambiente, aggiungere testo hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello fine specifiche righe si desidera toolog. Ad esempio, tooexecute setup.exe in hello **% PathToApp1Install %** directory:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify nel codice xml, è possibile creare un wrapper *cmd* file che chiama tutti l'avvio attività con la registrazione e assicura hello di condivisioni ogni attività figlio stesse variabili di ambiente.

Potrebbe essere tuttavia indesiderate toouse `>> "%TEMP%\StartupLog.txt" 2>&1` end hello di ogni attività di avvio. È possibile applicare la registrazione dell'attività tramite la creazione di un wrapper che gestisce la registrazione al posto dell'utente. Il wrapper chiama file batch reale hello desiderato toorun. L'output di file batch di destinazione hello sarà reindirizzato toohello *Startuplog.txt* file.

Hello di esempio seguente viene illustrato come tooredirect tutti output da un file batch di avvio. In questo esempio, file Serverdefinition hello crea un'attività di avvio che chiama *logwrap.cmd*. *logwrap.cmd* chiamate *Startup2.cmd*, reindirizzando tutto l'output troppo**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

Esempio di output di hello **StartupLog.txt** file:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Hello **StartupLog.txt** file si trova in hello *C:\Resources\temp\\\RoleTemp {identificatore del ruolo}* cartella.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Impostare l'attributo executionContext in modo appropriato per le attività di avvio
Impostare i privilegi in modo appropriato per l'attività di avvio hello. Talvolta le attività di avvio devono eseguire con privilegi elevati, anche se il ruolo di hello viene eseguito con privilegi normali.

Hello [executionContext][attività] attributo imposta il livello di privilegio hello dell'attività di avvio hello. Utilizzando `executionContext="limited"` indica dispone di attività di avvio hello hello stesso livello di privilegio del ruolo hello. Utilizzando `executionContext="elevated"` significa che l'attività di avvio hello privilegi di amministratore, che consente attività di amministrazione di attività tooperform avvio hello senza assegnazione di ruolo di tooyour privilegi di amministratore.

Un esempio di un'attività di avvio che richiede privilegi elevati è un'attività di avvio che usa **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** richiede `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Utilizzare l'attributo taskType appropriato hello
Hello [taskType][attività] attributo determina l'esecuzione delle attività di avvio di hello modo hello. Sono disponibili tre valori: **simple**, **background** e **foreground**. Hello attività di primo piano e vengono avviate in modo asincrono e quindi hello semplice esecuzione delle attività in modo sincrono una alla volta.

Con **semplice** le attività di avvio, è possibile impostare l'ordine di hello esecuzione delle attività hello base all'ordine in cui hello attività sono elencate nel file servicedefinition. Csdef hello hello. Se un **semplice** attività termina con un diverso da zero, il codice di uscita, quindi fare hello arresta procedure di avvio e ruolo hello non viene avviato.

Hello differenza tra **background** le attività di avvio e **in primo piano** le attività di avvio è che **in primo piano** attività mantenere in esecuzione ruolo hello finché hello  **in primo piano** attività termina. Ciò significa anche che se hello **in primo piano** operazione blocca o arresti anomali del sistema, hello ruolo non verrà riciclato fino hello **in primo piano** viene forzato l'attività chiusa. Per questo motivo, **background** è consigliato per l'attività di avvio asincrono a meno che non necessarie le funzionalità di hello **in primo piano** attività.

### <a name="end-batch-files-with-exit-b-0"></a>Terminare i file batch con EXIT /B 0
Hello ruolo verrà avviato solo se hello **errorlevel** da ciascuna di avvio semplici attività è zero. Non tutti i programmi impostare hello **errorlevel** (codice di uscita) in modo corretto, pertanto, file batch hello deve terminare con un `EXIT /B 0` se tutto ciò che è stato eseguito correttamente.

Manca un `EXIT /B 0` hello fine di un file batch di avvio è una causa comune di ruoli che non vengono avviati.

> [!NOTE]
> Ho notato batch nidificati in alcuni casi i file di blocco quando si utilizza hello `/B` parametro. È possibile assicurarsi che il problema di blocco non si verifica se un altro file batch chiama il file batch corrente, ad esempio se si utilizza hello toomake [wrapper log](#always-log-startup-activities). È possibile omettere hello `/B` parametro in questo caso.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Prevede più di una volta toorun attività di avvio
Non tutti i ricicli dei ruoli includono un riavvio, ma tutti includono l'esecuzione di tutte le attività di avvio. Ciò significa che le attività di avvio devono essere in grado di toorun più volte tra i riavvii senza problemi. Questo argomento viene discusso in hello [precedente sezione](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Utilizzare i file di archiviazione locale toostore che devono essere accessibili nel ruolo hello
Se si desidera toocopy oppure crea un file durante l'attività di avvio che è quindi accessibile tooyour ruolo, quindi tale file deve trovarsi nell'archivio locale. Vedere hello [precedente sezione](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Passaggi successivi
Esaminare i cloud hello [del pacchetto e del modello di servizio](cloud-services-model-and-package.md)

Altre informazioni sul funzionamento delle [attività](cloud-services-startup-tasks.md) .

[Creare e distribuire](cloud-services-how-to-create-deploy-portal.md) il pacchetto del servizio cloud.

[Servicedefinition]: cloud-services-model-and-package.md#csdef
[attività]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variabile]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
