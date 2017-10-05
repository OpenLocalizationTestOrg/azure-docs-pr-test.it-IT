---
title: "Attività di avvio comuni per Servizi cloud | Documentazione Microsoft"
description: "Questo articolo fornisce alcuni esempi delle attività di avvio comuni che è possibile eseguire nel ruolo Web o di lavoro dei servizi cloud."
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="9066e-103">Attività di avvio comuni del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="9066e-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="9066e-104">Questo articolo fornisce alcuni esempi relativi alle attività di avvio comuni che è possibile eseguire nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9066e-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="9066e-105">È possibile usare le attività di avvio per eseguire operazioni prima dell'avvio di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="9066e-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="9066e-106">Le operazioni che si possono eseguire sono l'installazione di un componente, la registrazione dei componenti COM, l'impostazione delle chiavi del Registro di sistema o l'avvio di un processo a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="9066e-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="9066e-107">Per comprendere il funzionamento delle attività di avvio e in particolare la modalità di creazione delle voci che definiscono un'attività di avvio, vedere [questo articolo](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="9066e-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="9066e-108">Le attività di avvio non sono applicabili ai ruoli VM, ma solo ai ruoli Web e di lavoro del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9066e-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="9066e-109">Definire le variabili di ambiente prima dell'avvio di un ruolo</span><span class="sxs-lookup"><span data-stu-id="9066e-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="9066e-110">Se si devono definire le variabili di ambiente per un'attività specifica, usare l'elemento [Environment] all'interno dell'elemento [Task].</span><span class="sxs-lookup"><span data-stu-id="9066e-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="9066e-111">Le variabili possono inoltre usare un [valore XPath di Azure valido](cloud-services-role-config-xpath.md) per fare riferimento a un elemento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9066e-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="9066e-112">Anziché usare l'attributo `value` , definire un elemento figlio [RoleInstanceValue] .</span><span class="sxs-lookup"><span data-stu-id="9066e-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="9066e-113">Configurare l'avvio IIS con AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="9066e-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="9066e-114">Lo strumento da riga di comando [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) può essere usato per gestire le impostazioni IIS all'avvio in Azure.</span><span class="sxs-lookup"><span data-stu-id="9066e-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="9066e-115">*AppCmd.exe* offre un comodo accesso da riga di comando alle impostazioni di configurazione da usare nelle attività di avvio in Azure.</span><span class="sxs-lookup"><span data-stu-id="9066e-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="9066e-116">Tramite *AppCmd.exe*è possibile aggiungere, modificare o rimuovere impostazioni per applicazioni e siti Web.</span><span class="sxs-lookup"><span data-stu-id="9066e-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="9066e-117">È necessario tuttavia tenere conto di alcuni aspetti se si usa *AppCmd.exe* come attività di avvio:</span><span class="sxs-lookup"><span data-stu-id="9066e-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="9066e-118">Le attività di avvio possono essere eseguite più di una volta tra un riavvio e l'altro.</span><span class="sxs-lookup"><span data-stu-id="9066e-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="9066e-119">Ad esempio, quando un ruolo viene riciclato.</span><span class="sxs-lookup"><span data-stu-id="9066e-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="9066e-120">Se eseguita più volte, l'azione *AppCmd.exe* potrebbe generare un errore.</span><span class="sxs-lookup"><span data-stu-id="9066e-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="9066e-121">Ad esempio, il tentativo di aggiungere due volte una sezione a *Web.config* potrebbe generare un errore.</span><span class="sxs-lookup"><span data-stu-id="9066e-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="9066e-122">Le attività di avvio danno esito negativo se restituiscono un codice di uscita o un valore di **errorlevel**diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="9066e-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="9066e-123">Ad esempio, quando *AppCmd.exe* genera un errore.</span><span class="sxs-lookup"><span data-stu-id="9066e-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="9066e-124">È consigliabile controllare il valore di **errorlevel** dopo la chiamata di *AppCmd.exe*, operazione semplice se si esegue il wrapping della chiamata a *AppCmd.exe* con un file con estensione *.cmd*.</span><span class="sxs-lookup"><span data-stu-id="9066e-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="9066e-125">Se si rileva un valore di **errorlevel** noto, è possibile ignorarlo oppure restituirlo.</span><span class="sxs-lookup"><span data-stu-id="9066e-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="9066e-126">Il valore di errorlevel restituito da *AppCmd.exe* è elencato nel file winerror.h e può essere visualizzato anche in [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="9066e-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="9066e-127">Esempio di gestione del livello di errore</span><span class="sxs-lookup"><span data-stu-id="9066e-127">Example of managing the error level</span></span>
<span data-ttu-id="9066e-128">In questo esempio vengono aggiunte una sezione di compressione e una voce di compressione per JSON al file *Web.config* , con gestione e registrazione degli errori.</span><span class="sxs-lookup"><span data-stu-id="9066e-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="9066e-129">Le sezioni pertinenti del file [ServiceDefinition.csdef] sono riportate di seguito, evidenziando l'impostazione dell'attributo [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) su `elevated` per fornire ad *AppCmd.exe* le autorizzazioni sufficienti per modificare le impostazioni nel file *Web.config*:</span><span class="sxs-lookup"><span data-stu-id="9066e-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="9066e-130">Nel file batch *Startup.cmd* viene usato *AppCmd.exe* per aggiungere una sezione di compressione e una voce di compressione per JSON al file *Web.config*.</span><span class="sxs-lookup"><span data-stu-id="9066e-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="9066e-131">Il valore di **errorlevel** previsto di 183 viene impostato su zero tramite il programma da riga di comando VERIFY.EXE.</span><span class="sxs-lookup"><span data-stu-id="9066e-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="9066e-132">I valori di errorlevel imprevisti vengono registrati in StartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="9066e-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="9066e-133">Aggiungere regole di firewall</span><span class="sxs-lookup"><span data-stu-id="9066e-133">Add firewall rules</span></span>
<span data-ttu-id="9066e-134">In Azure sono disponibili due firewall.</span><span class="sxs-lookup"><span data-stu-id="9066e-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="9066e-135">Il primo controlla le connessioni tra la macchina virtuale e il mondo esterno.</span><span class="sxs-lookup"><span data-stu-id="9066e-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="9066e-136">Questa funzionalità è controllata dall'elemento [EndPoints] nel file [ServiceDefinition.csdef].</span><span class="sxs-lookup"><span data-stu-id="9066e-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="9066e-137">Il secondo controlla le connessioni tra la macchina virtuale e i processi al suo interno.</span><span class="sxs-lookup"><span data-stu-id="9066e-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="9066e-138">Questo firewall può essere controllato tramite lo strumento della riga di comando `netsh advfirewall firewall`.</span><span class="sxs-lookup"><span data-stu-id="9066e-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="9066e-139">In Azure vengono create regole di firewall per i processi avviati nei ruoli.</span><span class="sxs-lookup"><span data-stu-id="9066e-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="9066e-140">Quando si avvia un servizio o un programma, ad esempio, in Azure vengono create automaticamente le regole di firewall necessarie per consentire la comunicazione del servizio con Internet.</span><span class="sxs-lookup"><span data-stu-id="9066e-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="9066e-141">Tuttavia, se si crea un servizio che viene avviato da un processo esterno al ruolo, come un servizio COM+ o un'attività pianificata di Windows, è necessario creare manualmente una regola di firewall per consentire l'accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="9066e-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="9066e-142">Queste regole di firewall possono essere create usando un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="9066e-143">In un'attività di avvio che crea una regola di firewall l'attributo [executionContext][Task] deve essere impostato su **elevato** diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="9066e-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="9066e-144">Aggiungere l'attività di avvio seguente per il file [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="9066e-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="9066e-145">Per aggiungere la regola di firewall, è necessario usare i comandi `netsh advfirewall firewall` appropriati nel file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="9066e-146">In questo esempio l'attività di avvio richiede la sicurezza e la crittografia per la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="9066e-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="9066e-147">Bloccare un indirizzo IP specifico</span><span class="sxs-lookup"><span data-stu-id="9066e-147">Block a specific IP address</span></span>
<span data-ttu-id="9066e-148">È possibile limitare l'accesso di un ruolo Web di Azure a un set di indirizzi IP specifici modificando il file **web.config** IIS.</span><span class="sxs-lookup"><span data-stu-id="9066e-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="9066e-149">È anche necessario usare un file di comando per lo sblocco della sezione **ipSecurity** del file **ApplicationHost.config**.</span><span class="sxs-lookup"><span data-stu-id="9066e-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="9066e-150">Per sbloccare la sezione **ipSecurity** del file **ApplicationHost.config**, creare un file di comando da eseguire all'avvio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="9066e-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="9066e-151">Creare una cartella al livello radice del ruolo Web denominata **startup** e crearvi un file batch denominato **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="9066e-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="9066e-152">Aggiungere il file al progetto di Visual Studio e impostare le proprietà su **Copia sempre** per assicurarsi che sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9066e-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="9066e-153">Aggiungere l'attività di avvio seguente per il file [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="9066e-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="9066e-154">Aggiungere questo comando al file **startup.cmd** :</span><span class="sxs-lookup"><span data-stu-id="9066e-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="9066e-155">In questo modo il file batch **startup.cmd** viene eseguito ogni volta che il ruolo Web viene inizializzato, assicurando lo sblocco della sezione **ipSecurity**.</span><span class="sxs-lookup"><span data-stu-id="9066e-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="9066e-156">Modificare infine la sezione [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) del file **web.config** del ruolo Web in modo da aggiungere un elenco di indirizzi IP a cui viene concesso l'accesso, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9066e-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="9066e-157">Questa configurazione di esempio **consente** l'accesso al server a tutti gli indirizzi IP, a eccezione dei due IP definiti</span><span class="sxs-lookup"><span data-stu-id="9066e-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="9066e-158">Questa configurazione di esempio **nega** l'accesso al server a tutti gli indirizzi IP, a eccezione dei due IP definiti.</span><span class="sxs-lookup"><span data-stu-id="9066e-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="9066e-159">Creare un'attività di avvio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="9066e-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="9066e-160">Gli script di Windows PowerShell non possono essere chiamati direttamente dal file [ServiceDefinition.csdef] , ma possono essere richiamati da un file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="9066e-161">Per impostazione predefinita, in PowerShell non vengono eseguiti script non firmati.</span><span class="sxs-lookup"><span data-stu-id="9066e-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="9066e-162">Se non si firmano gli script, PowerShell deve essere configurato per eseguire script non firmati.</span><span class="sxs-lookup"><span data-stu-id="9066e-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="9066e-163">Per eseguire script non firmati, **ExecutionPolicy** deve essere impostato su **Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="9066e-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="9066e-164">L'impostazione di **ExecutionPolicy** da usare dipende dalla versione di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9066e-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="9066e-165">Se si usa un sistema operativo Guest che esegue PowerShell 2.0 o 1.0, è possibile forzare l'esecuzione della versione 2 e, se non è disponibile, usare la versione 1.</span><span class="sxs-lookup"><span data-stu-id="9066e-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="9066e-166">Creare file nell'archiviazione locale da un'attività di avvio</span><span class="sxs-lookup"><span data-stu-id="9066e-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="9066e-167">È possibile usare una risorsa di archiviazione locale per archiviare i file creati dall'attività di avvio a cui l'applicazione accederà in seguito.</span><span class="sxs-lookup"><span data-stu-id="9066e-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="9066e-168">Per creare la risorsa di archiviazione locale, aggiungere una sezione [LocalResources] al file [ServiceDefinition.csdef] e quindi aggiungere l'elemento figlio [LocalStorage].</span><span class="sxs-lookup"><span data-stu-id="9066e-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="9066e-169">Assegnare alla risorsa di archiviazione locale un nome univoco e una dimensione appropriata per l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="9066e-170">Per usare una risorsa di archiviazione locale nell'attività di avvio, è necessario creare una variabile di ambiente che faccia riferimento al percorso della risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="9066e-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="9066e-171">In questo modo l'attività di avvio e l'applicazione sono in grado di leggere e scrivere i file nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="9066e-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="9066e-172">Le sezioni pertinenti del file **ServiceDefinition.csdef** sono riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="9066e-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="9066e-173">Nel file batch **Startup.cmd** viene usata la variabile di ambiente **PathToStartupStorage** per creare il file **MyTest.txt** nel percorso di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="9066e-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="9066e-174">È possibile accedere alla cartella di archiviazione locale da Azure SDK usando il metodo [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx).</span><span class="sxs-lookup"><span data-stu-id="9066e-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="9066e-175">Esecuzione nell'emulatore o nel cloud</span><span class="sxs-lookup"><span data-stu-id="9066e-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="9066e-176">È possibile impostare l'attività di avvio in modo che esegua passaggi diversi a seconda che venga usata nel cloud o nell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="9066e-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="9066e-177">È ad esempio possibile decidere di usare una copia aggiornata dei dati SQL solo quando l'esecuzione avviene nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="9066e-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="9066e-178">In alternativa, è possibile eseguire dei passaggi di ottimizzazione delle prestazioni nel cloud che non sono necessari quando l'esecuzione avviene nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="9066e-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="9066e-179">Per eseguire nell'emulatore di calcolo azioni diverse da quelle eseguite nel cloud, è necessario creare una variabile di ambiente nel file [ServiceDefinition.csdef]</span><span class="sxs-lookup"><span data-stu-id="9066e-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="9066e-180">e testare la variabile di ambiente su un valore durante l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="9066e-181">Per creare la variabile di ambiente, aggiungere l'elemento [Variable]/[RoleInstanceValue] e creare un valore XPath di `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="9066e-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="9066e-182">Il valore della variabile di ambiente **%ComputeEmulatorRunning%** è `true` durante l'esecuzione nell'emulatore di calcolo e `false` durante l'esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9066e-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="9066e-183">È ora possibile usare la variabile di ambiente **%ComputeEmulatorRunning%** in qualsiasi esecuzione di attività per eseguire azioni diverse a seconda che il ruolo sia in esecuzione nel cloud o nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="9066e-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="9066e-184">Di seguito è riportato uno script shell con estensione cmd che controlla la variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="9066e-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="9066e-185">Rilevare se l'attività è già stata eseguita</span><span class="sxs-lookup"><span data-stu-id="9066e-185">Detect that your task has already run</span></span>
<span data-ttu-id="9066e-186">Il ruolo può essere riciclato senza riavvio, causando una nuova esecuzione dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="9066e-187">Non esistono flag che indichino che un'attività è già stata eseguita nella macchina virtuale di hosting.</span><span class="sxs-lookup"><span data-stu-id="9066e-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="9066e-188">Per alcune attività non è importante se l'esecuzione avviene più volte.</span><span class="sxs-lookup"><span data-stu-id="9066e-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="9066e-189">Potrebbe tuttavia verificarsi una situazione in cui è necessario impedire l'esecuzione ripetuta di un'attività.</span><span class="sxs-lookup"><span data-stu-id="9066e-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="9066e-190">Il modo più semplice per rilevare se un'attività è già stata eseguita consiste nel creare un file nella cartella **%TEMP%** quando l'attività ha esito positivo e cercarlo all'inizio dell'attività.</span><span class="sxs-lookup"><span data-stu-id="9066e-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="9066e-191">Di seguito è riportato uno script shell con estensione cmd di esempio che esegue automaticamente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="9066e-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="9066e-192">Procedure consigliate per l'attività</span><span class="sxs-lookup"><span data-stu-id="9066e-192">Task best practices</span></span>
<span data-ttu-id="9066e-193">Di seguito sono riportate alcune procedure consigliate da seguire durante la configurazione dell'attività per il ruolo Web o di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9066e-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="9066e-194">Registrare sempre le attività di avvio</span><span class="sxs-lookup"><span data-stu-id="9066e-194">Always log startup activities</span></span>
<span data-ttu-id="9066e-195">In Visual Studio non è previsto un debugger per analizzare i file batch, pertanto è buona pratica ottenere quanti più dati possibile sul funzionamento di tali file.</span><span class="sxs-lookup"><span data-stu-id="9066e-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="9066e-196">La registrazione dell'output dei file batch, sia **stdout** che **stderr**, può fornire informazioni importanti quando si tenta di eseguire il debug e correggere i file batch.</span><span class="sxs-lookup"><span data-stu-id="9066e-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="9066e-197">Per registrare sia **stdout** che **stderr** nel file StartupLog.txt nella directory a cui fa riferimento la variabile di ambiente **%TEMP%**, aggiungere il testo `>>  "%TEMP%\\StartupLog.txt" 2>&1` alla fine delle righe specifiche che si desidera registrare.</span><span class="sxs-lookup"><span data-stu-id="9066e-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="9066e-198">Ad esempio, per eseguire setup.exe nella directory **%PathToApp1Install%** :</span><span class="sxs-lookup"><span data-stu-id="9066e-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="9066e-199">Per semplificare il xml, è possibile creare un file wrapper *cmd* che chiama tutte le attività di avvio insieme alla registrazione e assicura che ogni attività figlio condivida le stesse variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="9066e-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="9066e-200">Può risultare fastidioso usare `>> "%TEMP%\StartupLog.txt" 2>&1` al termine di ogni attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="9066e-201">È possibile applicare la registrazione dell'attività tramite la creazione di un wrapper che gestisce la registrazione al posto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9066e-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="9066e-202">Il wrapper chiama il file batch reale che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="9066e-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="9066e-203">L'output del file batch di destinazione verrà reindirizzato sul file *Startuplog.txt*.</span><span class="sxs-lookup"><span data-stu-id="9066e-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="9066e-204">Di seguito viene fornito un esempio che illustra come reindirizzare tutto l'output di un file batch di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="9066e-205">In questo esempio il file ServerDefinition.csdef crea un'attività di avvio che chiama *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="9066e-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="9066e-206">*logwrap.cmd* chiama *Startup2.cmd*, reindirizzando tutto l'output a **%TEMP%\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="9066e-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="9066e-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="9066e-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="9066e-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="9066e-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="9066e-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="9066e-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="9066e-210">Esempio di output nel file **StartupLog.txt**:</span><span class="sxs-lookup"><span data-stu-id="9066e-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="9066e-211">Il file **StartupLog.txt** si trova nella cartella *C:\Resources\temp\\{identificatore ruolo}\RoleTemp*.</span><span class="sxs-lookup"><span data-stu-id="9066e-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="9066e-212">Impostare l'attributo executionContext in modo appropriato per le attività di avvio</span><span class="sxs-lookup"><span data-stu-id="9066e-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="9066e-213">Impostare i privilegi in modo appropriato per l'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="9066e-214">In alcuni casi le attività di avvio devono essere eseguite con privilegi elevati anche se il ruolo viene eseguito con privilegi normali.</span><span class="sxs-lookup"><span data-stu-id="9066e-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="9066e-215">Lo strumento da riga di comando [executionContext][Task] imposta il livello di privilegio dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="9066e-216">L'uso di `executionContext="limited"` indica che l'attività di avvio dispone dello stesso livello di privilegio del ruolo.</span><span class="sxs-lookup"><span data-stu-id="9066e-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="9066e-217">L'uso di `executionContext="elevated"` indica che l'attività di avvio dispone di privilegi di amministratore, cioè potrà eseguire attività amministrative, senza fornire privilegi di amministratore al ruolo.</span><span class="sxs-lookup"><span data-stu-id="9066e-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="9066e-218">Un esempio di attività di avvio che richiede privilegi elevati è un'attività di avvio che usa **AppCmd.exe** per configurare IIS.</span><span class="sxs-lookup"><span data-stu-id="9066e-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="9066e-219">**AppCmd.exe** richiede `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="9066e-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="9066e-220">Usare l'attributo taskType appropriato</span><span class="sxs-lookup"><span data-stu-id="9066e-220">Use the appropriate taskType</span></span>
<span data-ttu-id="9066e-221">Lo strumento da riga di comando [taskType][Task] determina la modalità di esecuzione dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="9066e-222">Sono disponibili tre valori: **simple**, **background** e **foreground**.</span><span class="sxs-lookup"><span data-stu-id="9066e-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="9066e-223">Le attività in background e in primo piano (foreground) vengono avviate in modo asincrono e le attività semplici (simple) vengono eseguite in modo sincrono una alla volta.</span><span class="sxs-lookup"><span data-stu-id="9066e-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="9066e-224">Con le attività di avvio **simple** è possibile impostare l'ordine in cui le attività si verificano in base all'ordine in cui le attività sono elencate nel file ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="9066e-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="9066e-225">Se un'attività **simple** termina con un codice di uscita diverso da zero, la procedura di avvio viene arrestata e il ruolo non viene avviato.</span><span class="sxs-lookup"><span data-stu-id="9066e-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="9066e-226">La differenza tra le attività di avvio **background** e **foreground** è che le attività **foreground** mantengono il ruolo in esecuzione fino alla fine dell'attività **foreground**.</span><span class="sxs-lookup"><span data-stu-id="9066e-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="9066e-227">Questo significa anche che se l'attività **foreground** si blocca o viene arrestata in modo anomalo, il ruolo non verrà riciclato fino alla chiusura forzata dell'attività **foreground**.</span><span class="sxs-lookup"><span data-stu-id="9066e-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="9066e-228">Per questo motivo, il tipo **background** è consigliato per le attività di avvio asincrono, a meno che non siano necessarie le funzionalità dell'attività di tipo **foreground**.</span><span class="sxs-lookup"><span data-stu-id="9066e-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="9066e-229">Terminare i file batch con EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="9066e-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="9066e-230">Il ruolo verrà avviato solo se il valore di **errorlevel** di ognuna delle attività di avvio semplici è uguale a zero.</span><span class="sxs-lookup"><span data-stu-id="9066e-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="9066e-231">Non in tutti i programmi il valore di **errorlevel** (codice di uscita) viene impostato correttamente, per cui se l'esecuzione è avvenuta correttamente il file batch deve terminare con un comando `EXIT /B 0`.</span><span class="sxs-lookup"><span data-stu-id="9066e-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="9066e-232">L'assenza di `EXIT /B 0` alla fine di un file batch di avvio è una causa comune del mancato avvio dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="9066e-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="9066e-233">Ho notato che a volte i file batch nidificati si bloccano se si usa il parametro `/B`.</span><span class="sxs-lookup"><span data-stu-id="9066e-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="9066e-234">È possibile garantire che non si verifichi il blocco se un altro file batch chiama il file batch corrente, ad esempio se si usa il [wrapper log](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="9066e-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="9066e-235">In questo caso non è possibile omettere il parametro `/B`.</span><span class="sxs-lookup"><span data-stu-id="9066e-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="9066e-236">Prevedere la ripetuta esecuzione delle attività di avvio</span><span class="sxs-lookup"><span data-stu-id="9066e-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="9066e-237">Non tutti i ricicli dei ruoli includono un riavvio, ma tutti includono l'esecuzione di tutte le attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="9066e-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="9066e-238">Ciò significa che deve essere possibile eseguire le attività di avvio più volte tra un riavvio e l'altro senza problemi.</span><span class="sxs-lookup"><span data-stu-id="9066e-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="9066e-239">Questo argomento viene discusso nella [sezione precedente](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="9066e-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="9066e-240">Usare le risorse di archiviazione locale per archiviare i file che dovranno essere accessibili nel ruolo</span><span class="sxs-lookup"><span data-stu-id="9066e-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="9066e-241">Se si desidera copiare o creare un file durante l'attività di avvio che sia quindi accessibile al ruolo, tale file deve essere posizionato nella risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="9066e-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="9066e-242">Vedere la [sezione precedente](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="9066e-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9066e-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9066e-243">Next steps</span></span>
<span data-ttu-id="9066e-244">Verificare il [pacchetto e il modello del servizio](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="9066e-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="9066e-245">Altre informazioni sul funzionamento delle [attività](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="9066e-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="9066e-246">[Creare e distribuire](cloud-services-how-to-create-deploy-portal.md) il pacchetto del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9066e-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="9066e-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="9066e-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="9066e-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="9066e-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="9066e-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="9066e-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="9066e-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="9066e-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="9066e-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="9066e-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="9066e-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="9066e-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="9066e-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="9066e-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="9066e-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="9066e-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="9066e-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="9066e-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
