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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="11bd9-103">Attività di avvio comuni del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="11bd9-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="11bd9-104">In questo articolo vengono forniti alcuni esempi comuni delle attività di avvio è tooperform nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="11bd9-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="11bd9-105">È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="11bd9-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="11bd9-106">Le operazioni che è possibile tooperform includono l'installazione di un componente, la registrazione dei componenti COM, impostano le chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="11bd9-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="11bd9-107">Vedere [questo articolo](cloud-services-startup-tasks.md) toounderstand funzionamento delle attività di avvio, e in particolare come toocreate hello voci che definiscono un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="11bd9-108">Attività di avvio non sono applicabili tooVirtual macchine, solo tooCloud servizio Web e ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11bd9-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="11bd9-109">Definire le variabili di ambiente prima dell'avvio di un ruolo</span><span class="sxs-lookup"><span data-stu-id="11bd9-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="11bd9-110">Se è necessario variabili di ambiente definite per un'attività specifica, utilizzare hello [ambiente] elemento all'interno di hello [attività] elemento.</span><span class="sxs-lookup"><span data-stu-id="11bd9-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="11bd9-111">Le variabili possono anche utilizzare un [valore XPath di Azure valido](cloud-services-role-config-xpath.md) tooreference qualcosa sulla distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="11bd9-112">Anziché utilizzare hello `value` attributo, definire un [RoleInstanceValue] elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="11bd9-113">Configurare l'avvio IIS con AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="11bd9-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="11bd9-114">Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) strumento da riga di comando può essere utilizzato toomanage le impostazioni di IIS all'avvio in Azure.</span><span class="sxs-lookup"><span data-stu-id="11bd9-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="11bd9-115">*AppCmd.exe* fornisce le impostazioni di tooconfiguration ideale della riga di comando di accesso per l'utilizzo nelle attività di avvio in Azure.</span><span class="sxs-lookup"><span data-stu-id="11bd9-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="11bd9-116">Tramite *AppCmd.exe*è possibile aggiungere, modificare o rimuovere impostazioni per applicazioni e siti Web.</span><span class="sxs-lookup"><span data-stu-id="11bd9-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="11bd9-117">Tuttavia, esistono alcuni aspetti toowatch, out per uso hello di *AppCmd.exe* come attività di avvio:</span><span class="sxs-lookup"><span data-stu-id="11bd9-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="11bd9-118">Le attività di avvio possono essere eseguite più di una volta tra un riavvio e l'altro.</span><span class="sxs-lookup"><span data-stu-id="11bd9-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="11bd9-119">Ad esempio, quando un ruolo viene riciclato.</span><span class="sxs-lookup"><span data-stu-id="11bd9-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="11bd9-120">Se eseguita più volte, l'azione *AppCmd.exe* potrebbe generare un errore.</span><span class="sxs-lookup"><span data-stu-id="11bd9-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="11bd9-121">Ad esempio, il tentativo di troppo tooadd una sezione*Web. config* due volte è stato possibile generare un errore.</span><span class="sxs-lookup"><span data-stu-id="11bd9-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="11bd9-122">Le attività di avvio danno esito negativo se restituiscono un codice di uscita o un valore di **errorlevel**diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="11bd9-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="11bd9-123">Ad esempio, quando *AppCmd.exe* genera un errore.</span><span class="sxs-lookup"><span data-stu-id="11bd9-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="11bd9-124">È un hello toocheck buona norma **errorlevel** dopo la chiamata *AppCmd.exe*, che è facile toodo se si esegue il wrapping di chiamate hello troppo*AppCmd.exe* con un *cmd*  file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="11bd9-125">Se si rileva un valore di **errorlevel** noto, è possibile ignorarlo oppure restituirlo.</span><span class="sxs-lookup"><span data-stu-id="11bd9-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="11bd9-126">Hello errorlevel restituito da *AppCmd.exe* sono elencati nel file Winerror hello e possono essere visualizzati anche nel [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="11bd9-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="11bd9-127">Esempio di gestione a livello di errore hello</span><span class="sxs-lookup"><span data-stu-id="11bd9-127">Example of managing hello error level</span></span>
<span data-ttu-id="11bd9-128">In questo esempio aggiunge una sezione di compressione e una voce di compressione per JSON toohello *Web. config* file, con la gestione e registrazione degli errori.</span><span class="sxs-lookup"><span data-stu-id="11bd9-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="11bd9-129">le sezioni pertinenti di hello Hello [Servicedefinition] file riportati di seguito, che includono l'impostazione di hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attributo troppo`elevated` toogive *AppCmd.exe*  sufficiente toochange hello le impostazioni delle autorizzazioni in hello *Web. config* file:</span><span class="sxs-lookup"><span data-stu-id="11bd9-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="11bd9-130">Hello *Startup.cmd* batch utilizza file *AppCmd.exe* tooadd una sezione di compressione e una voce di compressione per JSON toohello *Web. config* file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="11bd9-131">Hello previsto **errorlevel** di 183 viene impostato utilizzando hello verificare toozero. Programma della riga di comando eseguibile.</span><span class="sxs-lookup"><span data-stu-id="11bd9-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="11bd9-132">Valori di ERRORLEVEL imprevisti vengono registrati tooStartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="11bd9-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="11bd9-133">Aggiungere regole di firewall</span><span class="sxs-lookup"><span data-stu-id="11bd9-133">Add firewall rules</span></span>
<span data-ttu-id="11bd9-134">In Azure sono disponibili due firewall.</span><span class="sxs-lookup"><span data-stu-id="11bd9-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="11bd9-135">Hello prima controlla le connessioni tra macchine virtuali hello e hello world di fuori.</span><span class="sxs-lookup"><span data-stu-id="11bd9-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="11bd9-136">Questo firewall è controllato da hello [endpoint] elemento hello [Servicedefinition] file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="11bd9-137">Hello secondo controlla le connessioni tra macchine virtuali hello e processi hello all'interno di tale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11bd9-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="11bd9-138">Questo firewall può essere controllato dal hello `netsh advfirewall firewall` strumento da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="11bd9-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="11bd9-139">Azure crea regole del firewall per hello processi avviati nei ruoli.</span><span class="sxs-lookup"><span data-stu-id="11bd9-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="11bd9-140">Ad esempio, quando si avvia un servizio o un programma, Azure crea automaticamente tooallow di regole firewall necessarie hello toocommunicate tale servizio con hello Internet.</span><span class="sxs-lookup"><span data-stu-id="11bd9-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="11bd9-141">Tuttavia, se si crea un servizio che viene avviato da un processo esterno al ruolo (ad esempio, un servizio COM+ o un'attività pianificata di Windows), è necessario toomanually creare un servizio di toothat firewall regola tooallow accesso.</span><span class="sxs-lookup"><span data-stu-id="11bd9-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="11bd9-142">Queste regole di firewall possono essere create usando un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="11bd9-143">In un'attività di avvio che crea una regola di firewall l'attributo [executionContext][attività] deve essere impostato su **elevato** diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="11bd9-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="11bd9-144">Aggiungere hello dopo l'avvio attività toohello [Servicedefinition] file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="11bd9-145">regola del firewall hello tooadd, è necessario utilizzare hello appropriato `netsh advfirewall firewall` comandi nel file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="11bd9-146">In questo esempio, attività di avvio hello richiede protezione e crittografia per la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="11bd9-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="11bd9-147">Bloccare un indirizzo IP specifico</span><span class="sxs-lookup"><span data-stu-id="11bd9-147">Block a specific IP address</span></span>
<span data-ttu-id="11bd9-148">È possibile limitare un set di tooa accesso ruolo web di Azure di indirizzi IP specificati modificando il server IIS **Web. config** file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="11bd9-149">È inoltre necessario disporre di un file di comando che consente di sbloccare hello toouse **ipSecurity** sezione di hello **applicationHost. config** file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="11bd9-150">toodo sbloccare hello **ipSecurity** sezione di hello **applicationHost. config** file, creare un file di comando che viene eseguita all'avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="11bd9-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="11bd9-151">Creare una cartella a livello di radice hello del ruolo web chiamato **avvio** e, in questa cartella, creare un file batch denominato **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="11bd9-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="11bd9-152">Aggiungere il progetto di Visual Studio tooyour file e impostare le proprietà di hello troppo**Copia sempre** tooensure viene incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="11bd9-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="11bd9-153">Aggiungere hello dopo l'avvio attività toohello [Servicedefinition] file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="11bd9-154">Aggiungere questo toohello comando **startup.cmd** file:</span><span class="sxs-lookup"><span data-stu-id="11bd9-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="11bd9-155">Questa attività, hello **startup.cmd** batch toobe file eseguito ogni volta che viene inizializzato ruolo web hello, assicurando che hello necessario **ipSecurity** sezione è sbloccata.</span><span class="sxs-lookup"><span data-stu-id="11bd9-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="11bd9-156">Infine, modificare hello [sezione System. webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) del ruolo web **Web. config** file tooadd un elenco di indirizzi IP autorizzati ad accedere, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="11bd9-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="11bd9-157">Questa configurazione di esempio **consente** tutti gli indirizzi IP tooaccess hello server ad eccezione del fatto hello due definite</span><span class="sxs-lookup"><span data-stu-id="11bd9-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="11bd9-158">Questa configurazione di esempio **Nega** tutti gli indirizzi IP di accedere ai server hello tranne hello due definito.</span><span class="sxs-lookup"><span data-stu-id="11bd9-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="11bd9-159">Creare un'attività di avvio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="11bd9-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="11bd9-160">Script di Windows PowerShell non possono essere chiamati direttamente dal hello [Servicedefinition] file, ma possono essere richiamati da un file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="11bd9-161">Per impostazione predefinita, in PowerShell non vengono eseguiti script non firmati.</span><span class="sxs-lookup"><span data-stu-id="11bd9-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="11bd9-162">A meno che non si firma lo script, è necessario tooconfigure PowerShell toorun script non firmati.</span><span class="sxs-lookup"><span data-stu-id="11bd9-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="11bd9-163">toorun script non firmati, hello **ExecutionPolicy** deve essere impostato troppo**Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="11bd9-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="11bd9-164">Hello **ExecutionPolicy** impostazione uso si basa sulla versione di hello di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11bd9-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="11bd9-165">Se si utilizza un sistema operativo Guest che viene eseguito PowerShell 2.0 o 1.0 è possibile forzare toorun versione 2 e se non è disponibile, utilizzare la versione 1.</span><span class="sxs-lookup"><span data-stu-id="11bd9-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="11bd9-166">Creare file nell'archiviazione locale da un'attività di avvio</span><span class="sxs-lookup"><span data-stu-id="11bd9-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="11bd9-167">È possibile utilizzare un toostore risorse di archiviazione locale i file creati dall'attività di avvio a cui si accede in un secondo momento dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="11bd9-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="11bd9-168">toocreate hello risorsa di archiviazione locale, aggiungere un [LocalResources] sezione toohello [Servicedefinition] file e quindi aggiungere hello [LocalStorage] elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="11bd9-169">Assegnare un nome univoco e una dimensione appropriata risorsa di archiviazione locale hello per le attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="11bd9-170">toouse una risorsa di archiviazione locale nell'attività di avvio, è necessario un percorso risorse di archiviazione locale di ambiente tooreference variabile hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="11bd9-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="11bd9-171">Quindi hello attività di avvio e un'applicazione hello sono in grado di tooread e scrivere file di risorse di archiviazione locale toohello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="11bd9-172">le sezioni pertinenti di hello Hello **Servicedefinition** file riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="11bd9-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="11bd9-173">Ad esempio, questo **Startup.cmd** file batch utilizza hello **PathToStartupStorage** file hello toocreate variabile di ambiente **MyTest.txt** nell'archiviazione locale hello percorso.</span><span class="sxs-lookup"><span data-stu-id="11bd9-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="11bd9-174">È possibile accedere dalla hello Azure SDK cartella di archiviazione locale tramite hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="11bd9-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="11bd9-175">Esecuzione nell'emulatore Windows hello o cloud</span><span class="sxs-lookup"><span data-stu-id="11bd9-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="11bd9-176">È possibile avere l'attività di avvio esegua passaggi diversi durante il funzionamento in toowhen cloud confrontati hello che è nell'emulatore di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="11bd9-177">Ad esempio, è consigliabile toouse una copia aggiornata dei dati SQL solo quando è in esecuzione nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="11bd9-178">In alternativa è possibile toodo alcune ottimizzazioni delle prestazioni per il cloud hello che non è necessario toodo durante l'esecuzione nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="11bd9-179">Questa possibilità tooperform diverse azioni sul hello emulatore di calcolo e cloud hello può essere eseguita mediante la creazione di una variabile di ambiente in hello [Servicedefinition] file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="11bd9-180">e testare la variabile di ambiente su un valore durante l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="11bd9-181">variabile di ambiente hello toocreate aggiungere hello [variabile]/[RoleInstanceValue] elemento e creare un valore XPath di `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="11bd9-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="11bd9-182">valore hello Hello **ComputeEmulatorRunning %** variabile di ambiente è `true` durante l'esecuzione nell'emulatore di calcolo, hello e `false` durante l'esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="11bd9-183">attività Hello ora è possibile archiviare hello **ComputeEmulatorRunning %** azioni diverse tooperform variabile di ambiente in base che il ruolo di hello sia in esecuzione in hello cloud o hello emulatore.</span><span class="sxs-lookup"><span data-stu-id="11bd9-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="11bd9-184">Di seguito è riportato uno script shell con estensione cmd che controlla la variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="11bd9-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="11bd9-185">Rilevare se l'attività è già stata eseguita</span><span class="sxs-lookup"><span data-stu-id="11bd9-185">Detect that your task has already run</span></span>
<span data-ttu-id="11bd9-186">ruolo Hello può riciclare senza riavvio causando nuovamente il toorun di attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="11bd9-187">Non sussiste alcun tooindicate flag che un'attività è già stato eseguito nel hello ospita macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="11bd9-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="11bd9-188">Per alcune attività non è importante se l'esecuzione avviene più volte.</span><span class="sxs-lookup"><span data-stu-id="11bd9-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="11bd9-189">Tuttavia, è possibile eseguire una situazione in cui è necessario tooprevent in un'attività dall'esecuzione di più di una volta.</span><span class="sxs-lookup"><span data-stu-id="11bd9-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="11bd9-190">toodetect modo più semplice Hello che un'attività è già stato eseguito è un file di hello toocreate **% TEMP %** cartella quando l'attività hello ha esito positivo e osservare che hello di inizio dell'attività di hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="11bd9-191">Di seguito è riportato uno script shell con estensione cmd di esempio che esegue automaticamente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="11bd9-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="11bd9-192">Procedure consigliate per l'attività</span><span class="sxs-lookup"><span data-stu-id="11bd9-192">Task best practices</span></span>
<span data-ttu-id="11bd9-193">Di seguito sono riportate alcune procedure consigliate da seguire durante la configurazione dell'attività per il ruolo Web o di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11bd9-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="11bd9-194">Registrare sempre le attività di avvio</span><span class="sxs-lookup"><span data-stu-id="11bd9-194">Always log startup activities</span></span>
<span data-ttu-id="11bd9-195">Visual Studio non fornisce toostep un debugger tramite file batch, pertanto è buona tooget tutti i dati sull'operazione di hello dei file batch possibile.</span><span class="sxs-lookup"><span data-stu-id="11bd9-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="11bd9-196">Output di hello dei file batch, di registrazione sia **stdout** e **stderr**possono fornire informazioni importanti quando si tenta di toodebug e correggere i file batch.</span><span class="sxs-lookup"><span data-stu-id="11bd9-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="11bd9-197">entrambi toolog **stdout** e **stderr** file StartupLog.txt toohello in hello di hello directory punta tooby **% TEMP %** variabile di ambiente, aggiungere testo hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello fine specifiche righe si desidera toolog.</span><span class="sxs-lookup"><span data-stu-id="11bd9-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="11bd9-198">Ad esempio, tooexecute setup.exe in hello **% PathToApp1Install %** directory:</span><span class="sxs-lookup"><span data-stu-id="11bd9-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="11bd9-199">toosimplify nel codice xml, è possibile creare un wrapper *cmd* file che chiama tutti l'avvio attività con la registrazione e assicura hello di condivisioni ogni attività figlio stesse variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="11bd9-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="11bd9-200">Potrebbe essere tuttavia indesiderate toouse `>> "%TEMP%\StartupLog.txt" 2>&1` end hello di ogni attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="11bd9-201">È possibile applicare la registrazione dell'attività tramite la creazione di un wrapper che gestisce la registrazione al posto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="11bd9-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="11bd9-202">Il wrapper chiama file batch reale hello desiderato toorun.</span><span class="sxs-lookup"><span data-stu-id="11bd9-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="11bd9-203">L'output di file batch di destinazione hello sarà reindirizzato toohello *Startuplog.txt* file.</span><span class="sxs-lookup"><span data-stu-id="11bd9-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="11bd9-204">Hello di esempio seguente viene illustrato come tooredirect tutti output da un file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="11bd9-205">In questo esempio, file Serverdefinition hello crea un'attività di avvio che chiama *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="11bd9-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="11bd9-206">*logwrap.cmd* chiamate *Startup2.cmd*, reindirizzando tutto l'output troppo**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="11bd9-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="11bd9-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="11bd9-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="11bd9-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="11bd9-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="11bd9-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="11bd9-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="11bd9-210">Esempio di output di hello **StartupLog.txt** file:</span><span class="sxs-lookup"><span data-stu-id="11bd9-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="11bd9-211">Hello **StartupLog.txt** file si trova in hello *C:\Resources\temp\\\RoleTemp {identificatore del ruolo}* cartella.</span><span class="sxs-lookup"><span data-stu-id="11bd9-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="11bd9-212">Impostare l'attributo executionContext in modo appropriato per le attività di avvio</span><span class="sxs-lookup"><span data-stu-id="11bd9-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="11bd9-213">Impostare i privilegi in modo appropriato per l'attività di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="11bd9-214">Talvolta le attività di avvio devono eseguire con privilegi elevati, anche se il ruolo di hello viene eseguito con privilegi normali.</span><span class="sxs-lookup"><span data-stu-id="11bd9-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="11bd9-215">Hello [executionContext][attività] attributo imposta il livello di privilegio hello dell'attività di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="11bd9-216">Utilizzando `executionContext="limited"` indica dispone di attività di avvio hello hello stesso livello di privilegio del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="11bd9-217">Utilizzando `executionContext="elevated"` significa che l'attività di avvio hello privilegi di amministratore, che consente attività di amministrazione di attività tooperform avvio hello senza assegnazione di ruolo di tooyour privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="11bd9-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="11bd9-218">Un esempio di un'attività di avvio che richiede privilegi elevati è un'attività di avvio che usa **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="11bd9-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="11bd9-219">**AppCmd.exe** richiede `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="11bd9-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="11bd9-220">Utilizzare l'attributo taskType appropriato hello</span><span class="sxs-lookup"><span data-stu-id="11bd9-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="11bd9-221">Hello [taskType][attività] attributo determina l'esecuzione delle attività di avvio di hello modo hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="11bd9-222">Sono disponibili tre valori: **simple**, **background** e **foreground**.</span><span class="sxs-lookup"><span data-stu-id="11bd9-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="11bd9-223">Hello attività di primo piano e vengono avviate in modo asincrono e quindi hello semplice esecuzione delle attività in modo sincrono una alla volta.</span><span class="sxs-lookup"><span data-stu-id="11bd9-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="11bd9-224">Con **semplice** le attività di avvio, è possibile impostare l'ordine di hello esecuzione delle attività hello base all'ordine in cui hello attività sono elencate nel file servicedefinition. Csdef hello hello.</span><span class="sxs-lookup"><span data-stu-id="11bd9-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="11bd9-225">Se un **semplice** attività termina con un diverso da zero, il codice di uscita, quindi fare hello arresta procedure di avvio e ruolo hello non viene avviato.</span><span class="sxs-lookup"><span data-stu-id="11bd9-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="11bd9-226">Hello differenza tra **background** le attività di avvio e **in primo piano** le attività di avvio è che **in primo piano** attività mantenere in esecuzione ruolo hello finché hello  **in primo piano** attività termina.</span><span class="sxs-lookup"><span data-stu-id="11bd9-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="11bd9-227">Ciò significa anche che se hello **in primo piano** operazione blocca o arresti anomali del sistema, hello ruolo non verrà riciclato fino hello **in primo piano** viene forzato l'attività chiusa.</span><span class="sxs-lookup"><span data-stu-id="11bd9-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="11bd9-228">Per questo motivo, **background** è consigliato per l'attività di avvio asincrono a meno che non necessarie le funzionalità di hello **in primo piano** attività.</span><span class="sxs-lookup"><span data-stu-id="11bd9-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="11bd9-229">Terminare i file batch con EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="11bd9-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="11bd9-230">Hello ruolo verrà avviato solo se hello **errorlevel** da ciascuna di avvio semplici attività è zero.</span><span class="sxs-lookup"><span data-stu-id="11bd9-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="11bd9-231">Non tutti i programmi impostare hello **errorlevel** (codice di uscita) in modo corretto, pertanto, file batch hello deve terminare con un `EXIT /B 0` se tutto ciò che è stato eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="11bd9-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="11bd9-232">Manca un `EXIT /B 0` hello fine di un file batch di avvio è una causa comune di ruoli che non vengono avviati.</span><span class="sxs-lookup"><span data-stu-id="11bd9-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="11bd9-233">Ho notato batch nidificati in alcuni casi i file di blocco quando si utilizza hello `/B` parametro.</span><span class="sxs-lookup"><span data-stu-id="11bd9-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="11bd9-234">È possibile assicurarsi che il problema di blocco non si verifica se un altro file batch chiama il file batch corrente, ad esempio se si utilizza hello toomake [wrapper log](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="11bd9-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="11bd9-235">È possibile omettere hello `/B` parametro in questo caso.</span><span class="sxs-lookup"><span data-stu-id="11bd9-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="11bd9-236">Prevede più di una volta toorun attività di avvio</span><span class="sxs-lookup"><span data-stu-id="11bd9-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="11bd9-237">Non tutti i ricicli dei ruoli includono un riavvio, ma tutti includono l'esecuzione di tutte le attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="11bd9-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="11bd9-238">Ciò significa che le attività di avvio devono essere in grado di toorun più volte tra i riavvii senza problemi.</span><span class="sxs-lookup"><span data-stu-id="11bd9-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="11bd9-239">Questo argomento viene discusso in hello [precedente sezione](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="11bd9-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="11bd9-240">Utilizzare i file di archiviazione locale toostore che devono essere accessibili nel ruolo hello</span><span class="sxs-lookup"><span data-stu-id="11bd9-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="11bd9-241">Se si desidera toocopy oppure crea un file durante l'attività di avvio che è quindi accessibile tooyour ruolo, quindi tale file deve trovarsi nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="11bd9-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="11bd9-242">Vedere hello [precedente sezione](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="11bd9-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11bd9-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11bd9-243">Next steps</span></span>
<span data-ttu-id="11bd9-244">Esaminare i cloud hello [del pacchetto e del modello di servizio](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="11bd9-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="11bd9-245">Altre informazioni sul funzionamento delle [attività](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="11bd9-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="11bd9-246">[Creare e distribuire](cloud-services-how-to-create-deploy-portal.md) il pacchetto del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="11bd9-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
