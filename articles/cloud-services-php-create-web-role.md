---
title: aaaCreate Azure i ruoli web e di lavoro per PHP | Documenti Microsoft
description: Una Guida toocreating PHP ruoli web e di lavoro in un servizio cloud di Azure e configurazione hello PHP runtime.
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="8ef73-103">Come i ruoli di lavoro e web PHP toocreate</span><span class="sxs-lookup"><span data-stu-id="8ef73-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="8ef73-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8ef73-104">Overview</span></span>
<span data-ttu-id="8ef73-105">Questa guida Mostra come toocreate PHP web ruoli di lavoro o in un ambiente di sviluppo di Windows, scegliere una specifica versione di PHP hello "incorporate" versioni disponibili, modificare la configurazione di PHP hello, abilitare le estensioni e infine distribuire tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8ef73-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="8ef73-106">Viene inoltre descritto come tooconfigure un toouse ruolo web o di lavoro un runtime PHP (con configurazione personalizzata e le estensioni) specificata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8ef73-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="8ef73-107">Cosa sono i ruoli Web e di lavoro PHP?</span><span class="sxs-lookup"><span data-stu-id="8ef73-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="8ef73-108">Azure offre tre modelli di calcolo per le applicazioni in esecuzione: Servizio App di Azure, Macchine virtuali di Azure e Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef73-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="8ef73-109">Tutti e tre i modelli supportano PHP.</span><span class="sxs-lookup"><span data-stu-id="8ef73-109">All three models support PHP.</span></span> <span data-ttu-id="8ef73-110">Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia *PaaS (Platform as a Service)*.</span><span class="sxs-lookup"><span data-stu-id="8ef73-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="8ef73-111">All'interno di un servizio cloud, un ruolo web fornisce un web Internet Information Services (IIS) dedicato applicazioni front-end web toohost di server.</span><span class="sxs-lookup"><span data-stu-id="8ef73-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="8ef73-112">Un ruolo di lavoro può eseguire attività asincrone, con esecuzione prolungata o perpetue indipendenti dall'interazione o dall'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ef73-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="8ef73-113">Per altre informazioni su queste opzioni, vedere [Opzioni di hosting di calcolo fornite da Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="8ef73-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="8ef73-114">Scaricare hello Azure SDK per PHP</span><span class="sxs-lookup"><span data-stu-id="8ef73-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="8ef73-115">Hello [Azure SDK per PHP] è costituito da diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="8ef73-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="8ef73-116">Questo articolo verranno utilizzati due di essi: Azure PowerShell e hello emulatori di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef73-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="8ef73-117">Questi due componenti possono essere installati tramite installazione guidata piattaforma Web di Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="8ef73-118">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ef73-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="8ef73-119">Creare un progetto di servizi cloud</span><span class="sxs-lookup"><span data-stu-id="8ef73-119">Create a Cloud Services project</span></span>
<span data-ttu-id="8ef73-120">Hello primo passaggio per la creazione di un ruolo web o di lavoro PHP è toocreate un progetto di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef73-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="8ef73-121">un progetto di servizio di Azure funge da contenitore logico per i ruoli web e di lavoro e del progetto hello contiene [definizione (con estensione csdef) servizio] e [configurazione del servizio (. cscfg)] file.</span><span class="sxs-lookup"><span data-stu-id="8ef73-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="8ef73-122">toocreate un nuovo progetto di servizio di Azure, eseguire Azure PowerShell come amministratore ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="8ef73-123">Questo comando crea una nuova directory (`myProject`) toowhich è possibile aggiungere ruoli web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ef73-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="8ef73-124">Aggiungere ruoli Web o di lavoro PHP</span><span class="sxs-lookup"><span data-stu-id="8ef73-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="8ef73-125">tooadd progetto tooa ruolo web PHP, eseguire hello seguente comando dalla directory radice del progetto hello:</span><span class="sxs-lookup"><span data-stu-id="8ef73-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="8ef73-126">Per un ruolo di lavoro, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="8ef73-127">Hello `roleName` parametro è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="8ef73-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="8ef73-128">Se viene omesso, verrà generato automaticamente il nome di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="8ef73-129">ruolo web prima di Hello creato sarà `WebRole1`, sarà secondo hello `WebRole2`e così via.</span><span class="sxs-lookup"><span data-stu-id="8ef73-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="8ef73-130">Hello primo ruolo di lavoro creato sarà `WorkerRole1`, sarà secondo hello `WorkerRole2`e così via.</span><span class="sxs-lookup"><span data-stu-id="8ef73-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="8ef73-131">Specificare la versione PHP predefiniti hello</span><span class="sxs-lookup"><span data-stu-id="8ef73-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="8ef73-132">Quando si aggiunge un PHP web o lavoro tooa progetto di ruolo, i file di configurazione del progetto hello vengono modificati in modo che PHP venga installato in ogni istanza di web o di lavoro dell'applicazione quando viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="8ef73-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="8ef73-133">versione di hello toosee di PHP che verranno installati per impostazione predefinita, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="8ef73-134">Hello output di hello comando precedente avrà un aspetto simile toowhat è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8ef73-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="8ef73-135">In questo esempio hello `IsDefault` flag è impostato troppo`true` per PHP 5.3.17, che indica che saranno hello predefinito PHP versione installata.</span><span class="sxs-lookup"><span data-stu-id="8ef73-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="8ef73-136">È possibile impostare hello PHP runtime versione tooany delle versioni PHP hello elencati.</span><span class="sxs-lookup"><span data-stu-id="8ef73-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="8ef73-137">Ad esempio la versione PHP hello tooset (per un ruolo con nome hello `roleName`) too5.4.0, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="8ef73-138">Le versioni PHP disponibili potrebbero cambiare in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="8ef73-139">Personalizzare il runtime PHP predefinito di hello</span><span class="sxs-lookup"><span data-stu-id="8ef73-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="8ef73-140">Si dispone di controllo completo sulla configurazione di hello di hello PHP runtime che viene installato quando si esegue la procedura hello sopra, compresa la modifica di `php.ini` impostazioni e l'abilitazione delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="8ef73-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="8ef73-141">toocustomize hello incorporato runtime PHP, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8ef73-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="8ef73-142">Aggiungere una nuova cartella, denominata `php`, toohello `bin` directory di un ruolo web.</span><span class="sxs-lookup"><span data-stu-id="8ef73-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="8ef73-143">Per un ruolo di lavoro, aggiungere la directory radice del ruolo toohello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="8ef73-144">In hello `php` cartella, creare un'altra cartella denominata `ext`.</span><span class="sxs-lookup"><span data-stu-id="8ef73-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="8ef73-145">Inserire alcun `.dll` i file di estensione (ad esempio, `php_mongo.dll`) che si desidera tooenable in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="8ef73-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="8ef73-146">Aggiungere un `php.ini` file toohello `php` cartella.</span><span class="sxs-lookup"><span data-stu-id="8ef73-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="8ef73-147">Abilitare eventuali estensioni personalizzate e impostare qualsiasi direttiva PHP in questo file.</span><span class="sxs-lookup"><span data-stu-id="8ef73-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="8ef73-148">Ad esempio, se si desidera tooturn `display_errors` in e abilitare hello `php_mongo.dll` estensione, il contenuto di hello del `php.ini` sarà come segue:</span><span class="sxs-lookup"><span data-stu-id="8ef73-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="8ef73-149">Eventuali impostazioni non vengono impostate in modo esplicito in hello `php.ini` file fornisce verrà automaticamente essere impostare valori predefiniti tootheir.</span><span class="sxs-lookup"><span data-stu-id="8ef73-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="8ef73-150">Si tenga tuttavia presente che è possibile aggiungere un file `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="8ef73-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="8ef73-151">Utilizzare il proprio runtime PHP</span><span class="sxs-lookup"><span data-stu-id="8ef73-151">Use your own PHP runtime</span></span>
<span data-ttu-id="8ef73-152">In alcuni casi, anziché la selezione di un runtime PHP predefinito e configurarlo come descritto in precedenza, è consigliabile tooprovide la propria esecuzione PHP.</span><span class="sxs-lookup"><span data-stu-id="8ef73-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="8ef73-153">Ad esempio, è possibile utilizzare hello stesso runtime PHP in un ruolo web o di lavoro in uso nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="8ef73-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="8ef73-154">Questo rende più semplice tooensure applicazione hello non modificherà il comportamento nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8ef73-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="8ef73-155">Configurare un toouse ruolo web la propria esecuzione PHP</span><span class="sxs-lookup"><span data-stu-id="8ef73-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="8ef73-156">tooconfigure un toouse ruolo web un runtime PHP che si fornisce, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8ef73-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="8ef73-157">Creare un progetto di servizio Azure e aggiungere un ruolo Web PHP come descritto precedentemente in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8ef73-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="8ef73-158">Creare un `php` cartella hello `bin` cartella che si trova nella directory radice del ruolo web, quindi aggiunta il toohello di runtime (tutti i file binari, i file di configurazione, le sottocartelle, e così via) PHP `php` cartella.</span><span class="sxs-lookup"><span data-stu-id="8ef73-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="8ef73-159">(FACOLTATIVO) Se il runtime PHP utilizza hello [Microsoft Drivers for PHP per SQL Server][sqlsrv drivers], sarà necessario tooconfigure il tooinstall ruolo web [SQL Server Native Client 2012] [ sql native client] quando è disponibile.</span><span class="sxs-lookup"><span data-stu-id="8ef73-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="8ef73-160">toodo, aggiungere hello [sqlncli.msi x64 installer] toohello `bin` cartella nella directory radice del ruolo web.</span><span class="sxs-lookup"><span data-stu-id="8ef73-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="8ef73-161">script di avvio Hello descritto nel passaggio successivo hello eseguirà automaticamente installer hello quando viene eseguito il provisioning ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="8ef73-162">Se il runtime PHP non utilizza hello Microsoft Drivers for PHP per SQL Server, è possibile rimuovere hello successiva riga da script hello illustrato nel passaggio successivo hello:</span><span class="sxs-lookup"><span data-stu-id="8ef73-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="8ef73-163">Definire un'attività di avvio che configura [Internet Information Services (IIS)] [ iis.net] toouse il toohandle runtime PHP richieste per `.php` pagine.</span><span class="sxs-lookup"><span data-stu-id="8ef73-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="8ef73-164">toodo, aprire hello `setup_web.cmd` file (in hello `bin` file della directory radice del ruolo web) in un editor di testo e sostituire il contenuto con hello seguenti script:</span><span class="sxs-lookup"><span data-stu-id="8ef73-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="8ef73-165">Aggiungere una directory radice dell'applicazione file tooyour del ruolo web.</span><span class="sxs-lookup"><span data-stu-id="8ef73-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="8ef73-166">Questo valore sarà una directory radice del server web hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="8ef73-167">Pubblicare l'applicazione, come descritto in hello [pubblicare l'applicazione](#publish-your-application) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="8ef73-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="8ef73-168">Hello `download.ps1` script (in hello `bin` cartella della directory radice del ruolo web hello) può essere eliminato al termine dei passaggi hello descritto in precedenza per l'utilizzo proprio PHP runtime.</span><span class="sxs-lookup"><span data-stu-id="8ef73-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="8ef73-169">Configurare un toouse ruolo di lavoro proprio runtime PHP</span><span class="sxs-lookup"><span data-stu-id="8ef73-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="8ef73-170">tooconfigure un toouse ruolo di lavoro un runtime PHP che si fornisce, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8ef73-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="8ef73-171">Creare un progetto di servizio Azure e aggiungere un ruolo di lavoro PHP come descritto precedentemente in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8ef73-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="8ef73-172">Creare un `php` cartella nella directory radice del ruolo di lavoro hello, quindi aggiungere il toohello di runtime (tutti i file binari, i file di configurazione, le sottocartelle, e così via) PHP `php` cartella.</span><span class="sxs-lookup"><span data-stu-id="8ef73-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="8ef73-173">(FACOLTATIVO) Se il runtime PHP utilizza [Microsoft Drivers for PHP per SQL Server][sqlsrv drivers], sarà necessario tooconfigure il tooinstall ruolo di lavoro [SQL Server Native Client 2012] [ sql native client] quando è disponibile.</span><span class="sxs-lookup"><span data-stu-id="8ef73-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="8ef73-174">toodo, aggiungere hello [sqlncli.msi x64 installer] directory radice del ruolo di lavoro toohello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="8ef73-175">script di avvio Hello descritto nel passaggio successivo hello eseguirà automaticamente installer hello quando viene eseguito il provisioning ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="8ef73-176">Se il runtime PHP non utilizza hello Microsoft Drivers for PHP per SQL Server, è possibile rimuovere hello successiva riga da script hello illustrato nel passaggio successivo hello:</span><span class="sxs-lookup"><span data-stu-id="8ef73-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="8ef73-177">Definire un'attività di avvio che aggiunge il `php.exe` variabile di ambiente PATH del ruolo di lavoro eseguibile toohello quando viene eseguito il provisioning ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="8ef73-178">toodo, aprire hello `setup_worker.cmd` file (nella directory radice del ruolo di lavoro hello) in un editor di testo e sostituirne il contenuto con hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="8ef73-179">Aggiungere una directory radice del ruolo di applicazione file tooyour lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ef73-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="8ef73-180">Pubblicare l'applicazione, come descritto in hello [pubblicare l'applicazione](#publish-your-application) sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="8ef73-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="8ef73-181">Eseguire l'applicazione in hello emulatori di calcolo e archiviazione</span><span class="sxs-lookup"><span data-stu-id="8ef73-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="8ef73-182">Hello gli emulatori di Azure forniscono un ambiente locale in cui è possibile testare l'applicazione Azure prima di distribuirla toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="8ef73-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="8ef73-183">Esistono alcune differenze tra gli emulatori hello e hello ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef73-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="8ef73-184">toounderstand meglio, vedere [Usa hello emulatore di archiviazione Azure per sviluppo e test](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="8ef73-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="8ef73-185">Si noti che è necessario che PHP installato localmente emulatore di calcolo toouse hello.</span><span class="sxs-lookup"><span data-stu-id="8ef73-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="8ef73-186">emulatore di calcolo Hello utilizzerà il toorun di installazione di PHP locale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ef73-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="8ef73-187">eseguire il progetto in emulatori hello toorun hello il seguente comando dalla directory radice del progetto:</span><span class="sxs-lookup"><span data-stu-id="8ef73-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="8ef73-188">Si noterà toothis simili di output:</span><span class="sxs-lookup"><span data-stu-id="8ef73-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="8ef73-189">È possibile visualizzare l'applicazione in esecuzione nell'emulatore hello aprendo un browser web e di esplorazione toohello indirizzo locale illustrato nell'output di hello (`http://127.0.0.1:81` nell'output di esempio hello sopra).</span><span class="sxs-lookup"><span data-stu-id="8ef73-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="8ef73-190">emulatori di hello toostop, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8ef73-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="8ef73-191">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8ef73-191">Publish your application</span></span>
<span data-ttu-id="8ef73-192">toopublish l'applicazione, è necessario importare toofirst le impostazioni di pubblicazione utilizzando hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ef73-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="8ef73-193">Quindi è possibile pubblicare l'applicazione utilizzando hello [pubblica AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ef73-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="8ef73-194">Per informazioni sull'accesso, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ef73-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ef73-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ef73-195">Next steps</span></span>
<span data-ttu-id="8ef73-196">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="8ef73-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK per PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definizione (con estensione csdef) servizio]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configurazione del servizio (. cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
