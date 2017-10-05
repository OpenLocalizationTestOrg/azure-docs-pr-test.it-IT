---
title: Creare ruoli Web e di lavoro di Azure per PHP | Documentazione Microsoft
description: Guida alla creazione di ruoli Web e di lavoro PHP in un servizio cloud di Azure e configurazione del runtime PHP.
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="01e3f-103">Come creare ruoli Web e di lavoro PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="01e3f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="01e3f-104">Overview</span></span>
<span data-ttu-id="01e3f-105">Questa guida illustrerà come creare ruoli Web o di lavoro PHP in un ambiente di sviluppo Windows, scegliere una versione specifica di PHP tra le versioni incorporate disponibili, modificare la configurazione di PHP, abilitare le estensioni e, infine, eseguire la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="01e3f-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="01e3f-106">Verrà inoltre descritto come configurare un ruolo Web o di lavoro per l'uso del runtime PHP (con configurazione ed estensioni personalizzate) fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="01e3f-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="01e3f-107">Cosa sono i ruoli Web e di lavoro PHP?</span><span class="sxs-lookup"><span data-stu-id="01e3f-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="01e3f-108">Azure offre tre modelli di calcolo per le applicazioni in esecuzione: Servizio App di Azure, Macchine virtuali di Azure e Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="01e3f-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="01e3f-109">Tutti e tre i modelli supportano PHP.</span><span class="sxs-lookup"><span data-stu-id="01e3f-109">All three models support PHP.</span></span> <span data-ttu-id="01e3f-110">Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia *PaaS (Platform as a Service)*.</span><span class="sxs-lookup"><span data-stu-id="01e3f-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="01e3f-111">In un servizio cloud un ruolo Web fornisce un server Web IIS (Internet Information Services) dedicato per ospitare applicazioni Web front-end.</span><span class="sxs-lookup"><span data-stu-id="01e3f-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="01e3f-112">Un ruolo di lavoro può eseguire attività asincrone, con esecuzione prolungata o perpetue indipendenti dall'interazione o dall'input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="01e3f-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="01e3f-113">Per altre informazioni su queste opzioni, vedere [Opzioni di hosting di calcolo fornite da Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="01e3f-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="01e3f-114">Download di Azure SDK per PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="01e3f-115">[Azure SDK per PHP] è composto da diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="01e3f-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="01e3f-116">Questo articolo ne userà due: Azure PowerShell e gli emulatori di Azure.</span><span class="sxs-lookup"><span data-stu-id="01e3f-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="01e3f-117">È possibile installare questi due componenti tramite Installazione piattaforma Web Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01e3f-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="01e3f-118">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01e3f-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="01e3f-119">Creare un progetto di servizi cloud</span><span class="sxs-lookup"><span data-stu-id="01e3f-119">Create a Cloud Services project</span></span>
<span data-ttu-id="01e3f-120">Il primo passaggio nella creazione di un ruolo Web o di lavoro PHP consiste nel creare un progetto di servizio di Azure,</span><span class="sxs-lookup"><span data-stu-id="01e3f-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="01e3f-121">che funge da contenitore logico per i ruoli Web e di lavoro e contiene la [definizione del servizio (.csdef)] e i file di [configurazione del servizio (.cscfg)] del progetto.</span><span class="sxs-lookup"><span data-stu-id="01e3f-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="01e3f-122">Per creare un nuovo progetto di servizio di Azure, eseguire Azure PowerShell come amministratore e avviare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="01e3f-123">Questo comando permette di creare una nuova directory (`myProject`) a cui è possibile aggiungere ruoli Web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="01e3f-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="01e3f-124">Aggiungere ruoli Web o di lavoro PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="01e3f-125">Per aggiungere un ruolo Web PHP a un progetto, avviare il comando seguente dalla directory radice del progetto:</span><span class="sxs-lookup"><span data-stu-id="01e3f-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="01e3f-126">Per un ruolo di lavoro, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="01e3f-127">`roleName` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="01e3f-128">se omesso, il nome del ruolo verrà generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="01e3f-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="01e3f-129">Il primo ruolo Web creato sarà `WebRole1`, il secondo sarà `WebRole2` e così via.</span><span class="sxs-lookup"><span data-stu-id="01e3f-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="01e3f-130">Il primo ruolo di lavoro creato sarà `WorkerRole1`, il secondo sarà `WorkerRole2` e così via.</span><span class="sxs-lookup"><span data-stu-id="01e3f-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="01e3f-131">Specificare la versione PHP incorporata</span><span class="sxs-lookup"><span data-stu-id="01e3f-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="01e3f-132">Quando si aggiunge un ruolo Web o di lavoro PHO a un progetto, i file di configurazione del progetto verranno modificati in modo che PHP venga installato su ciascuna istanza Web o di lavoro dell'applicazione alla sua distribuzione.</span><span class="sxs-lookup"><span data-stu-id="01e3f-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="01e3f-133">Per visualizzare la versione di PHP che verrà installata per impostazione predefinita, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="01e3f-134">Il risultato del comando sopra riportato sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="01e3f-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="01e3f-135">In questo esempio, il flag `IsDefault` è impostato su `true` per PHP 5.3.17, a indicare che questa sarà la versione di PHP installata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="01e3f-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="01e3f-136">È possibile impostare la versione del runtime PHP su una qualsiasi delle versioni PHP elencate.</span><span class="sxs-lookup"><span data-stu-id="01e3f-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="01e3f-137">Per impostare ad esempio la versione PHP (per un ruolo denominato `roleName`) su 5.4.0, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="01e3f-138">Le versioni PHP disponibili possono cambiare in futuro.</span><span class="sxs-lookup"><span data-stu-id="01e3f-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="01e3f-139">Personalizzare il runtime PHP incorporato</span><span class="sxs-lookup"><span data-stu-id="01e3f-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="01e3f-140">L'utente dispone del controllo completo sulla configurazione del runtime PHP che viene installato eseguendo la procedura sopra illustrata, incluse le modifiche delle impostazioni `php.ini` e l'abilitazione delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="01e3f-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="01e3f-141">Per personalizzare il runtime PHP incorporato, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="01e3f-142">Aggiungere una nuova cartella denominata `php` alla directory `bin` del ruolo Web in uso.</span><span class="sxs-lookup"><span data-stu-id="01e3f-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="01e3f-143">Per un ruolo di lavoro, aggiungerlo alla directory radice del ruolo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="01e3f-144">Nella cartella `php` creare un'altra cartella denominata `ext`.</span><span class="sxs-lookup"><span data-stu-id="01e3f-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="01e3f-145">Inserire tutti i file con estensione `.dll` (ad esempio `php_mongo.dll`) da abilitare in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="01e3f-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="01e3f-146">Aggiungere un file `php.ini` alla cartella `php`.</span><span class="sxs-lookup"><span data-stu-id="01e3f-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="01e3f-147">Abilitare eventuali estensioni personalizzate e impostare qualsiasi direttiva PHP in questo file.</span><span class="sxs-lookup"><span data-stu-id="01e3f-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="01e3f-148">Ad esempio, se si desidera attivare `display_errors` e abilitare l'estensione `php_mongo.dll` il contenuto del file `php.ini` sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="01e3f-149">Qualsiasi impostazione non esplicitamente impostata nel file `php.ini` fornito verrà automaticamente impostata sui valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="01e3f-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="01e3f-150">Si tenga tuttavia presente che è possibile aggiungere un file `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="01e3f-151">Utilizzare il proprio runtime PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-151">Use your own PHP runtime</span></span>
<span data-ttu-id="01e3f-152">In alcuni casi, invece di selezionare un runtime PHP incorporato e configurarlo come sopra descritto, può essere consigliabile fornire un proprio runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="01e3f-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="01e3f-153">È ad esempio possibile usare lo stesso runtime PHP in un ruolo Web o di lavoro usato nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="01e3f-154">In questo modo sarà più semplice garantire che il comportamento dell'applicazione non cambi nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="01e3f-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="01e3f-155">Configurare un ruolo Web per l'uso del proprio runtime PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="01e3f-156">Per configurare un ruolo Web per l'uso di un runtime PHP fornito dall'utente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="01e3f-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="01e3f-157">Creare un progetto di servizio Azure e aggiungere un ruolo Web PHP come descritto precedentemente in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="01e3f-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="01e3f-158">Creare una cartella `php` nella cartella `bin` che si trova nella directory radice del proprio ruolo Web e quindi aggiungere nella cartella `php` il proprio runtime PHP (tutti i file binari, i file di configurazione, le sottocartelle e così via).</span><span class="sxs-lookup"><span data-stu-id="01e3f-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="01e3f-159">(FACOLTATIVO) Se il runtime PHP usa i [driver Microsoft per PHP per SQL Server][sqlsrv drivers], sarà necessario configurare il ruolo Web per installare [SQL Server Native Client 2012][sql native client] quando viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="01e3f-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="01e3f-160">A tale scopo, aggiungere il [programma di installazione sqlncli.msi x64] nella cartella `bin` nella directory radice del ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="01e3f-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="01e3f-161">Lo script di avvio descritto nel passaggio successivo eseguirà il programma di installazione senza avvisi quando viene eseguito il provisioning del ruolo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="01e3f-162">Se il proprio runtime PHP non usa i Driver Microsoft per PHP per SQL Server è possibile rimuovere la seguente riga dallo script illustrato nel passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="01e3f-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="01e3f-163">Definire un'attività di avvio per configurare [Internet Information Services (IIS)][iis.net] per l'uso del runtime PHP nella gestione delle richieste di pagine `.php`.</span><span class="sxs-lookup"><span data-stu-id="01e3f-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="01e3f-164">A tale scopo, aprire il file `setup_web.cmd` (nel file `bin` della directory radice del proprio ruolo Web) in un editor di testo e sostituirne il contenuto con lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="01e3f-165">Aggiungere i file applicazione alla directory radice del proprio ruolo Web,</span><span class="sxs-lookup"><span data-stu-id="01e3f-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="01e3f-166">che sarà la directory radice del server Web.</span><span class="sxs-lookup"><span data-stu-id="01e3f-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="01e3f-167">Pubblicare l'applicazione come descritto nella sezione [Pubblicare l'applicazione](#publish-your-application) più avanti.</span><span class="sxs-lookup"><span data-stu-id="01e3f-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="01e3f-168">Lo script `download.ps1` (nella cartella `bin` della directory radice del proprio ruolo Web) può essere eliminato dopo aver eseguito i passaggi sopra descritti per l'uso del proprio runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="01e3f-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="01e3f-169">Configurare un ruolo di lavoro per l'uso del proprio runtime PHP</span><span class="sxs-lookup"><span data-stu-id="01e3f-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="01e3f-170">Per configurare un ruolo di lavoro per l'uso di un runtime PHP fornito dall'utente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="01e3f-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="01e3f-171">Creare un progetto di servizio Azure e aggiungere un ruolo di lavoro PHP come descritto precedentemente in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="01e3f-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="01e3f-172">Creare una cartella `php` nella directory radice del proprio ruolo di lavoro e quindi aggiungere il proprio runtime PHP nella cartella `php` (tutti i file binari, i file di configurazione, le sottocartelle e così via).</span><span class="sxs-lookup"><span data-stu-id="01e3f-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="01e3f-173">(FACOLTATIVO) Se il runtime PHP usa i [driver Microsoft per PHP per SQL Server][sqlsrv drivers], sarà necessario configurare il ruolo di lavoro per installare [SQL Server Native Client 2012][sql native client] quando viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="01e3f-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="01e3f-174">A tale scopo, aggiungere il [programma di installazione sqlncli.msi x64] nella directory radice del proprio ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="01e3f-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="01e3f-175">Lo script di avvio descritto nel passaggio successivo eseguirà il programma di installazione senza avvisi quando viene eseguito il provisioning del ruolo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="01e3f-176">Se il proprio runtime PHP non usa i Driver Microsoft per PHP per SQL Server è possibile rimuovere la seguente riga dallo script illustrato nel passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="01e3f-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="01e3f-177">Definire un'attività di avvio per l'aggiunta dell'eseguibile `php.exe` alla variabile di ambiente PATH del ruolo di lavoro durante il provisioning del ruolo.</span><span class="sxs-lookup"><span data-stu-id="01e3f-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="01e3f-178">A tale scopo, aprire il file `setup_worker.cmd` (nella directory radice del proprio ruolo di lavoro) in un editor di testo e sostituirne il contenuto con lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="01e3f-179">Aggiungere i file applicazione alla directory radice del proprio ruolo di lavoro,</span><span class="sxs-lookup"><span data-stu-id="01e3f-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="01e3f-180">Pubblicare l'applicazione come descritto nella sezione [Pubblicare l'applicazione](#publish-your-application) più avanti.</span><span class="sxs-lookup"><span data-stu-id="01e3f-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="01e3f-181">Eseguire l'applicazione negli emulatori di calcolo e archiviazione</span><span class="sxs-lookup"><span data-stu-id="01e3f-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="01e3f-182">Gli emulatori di Azure forniscono un ambiente locale in cui è possibile testare l'applicazione Azure prima di distribuirla nel cloud.</span><span class="sxs-lookup"><span data-stu-id="01e3f-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="01e3f-183">Vi sono alcune differenze tra gli emulatori e l'ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="01e3f-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="01e3f-184">Per una migliore comprensione, vedere [Usare l'emulatore di archiviazione di Azure per sviluppo e test](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="01e3f-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="01e3f-185">Si noti che per usare l'emulatore di calcolo è necessario aver installato PHP in locale.</span><span class="sxs-lookup"><span data-stu-id="01e3f-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="01e3f-186">L'emulatore di calcolo userà l'installazione locale di PHP per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="01e3f-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="01e3f-187">Per eseguire il progetto negli emulatori, avviare il comando seguente dalla directory radice del progetto:</span><span class="sxs-lookup"><span data-stu-id="01e3f-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="01e3f-188">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="01e3f-189">Per visualizzare l'applicazione in esecuzione nell'emulatore, aprire un Web browser e immettere l'indirizzo locale indicato nell'output (`http://127.0.0.1:81` nell'output di esempio sopra riportato).</span><span class="sxs-lookup"><span data-stu-id="01e3f-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="01e3f-190">Per arrestare gli emulatori, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01e3f-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="01e3f-191">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="01e3f-191">Publish your application</span></span>
<span data-ttu-id="01e3f-192">Per pubblicare l'applicazione, è necessario prima importare le impostazioni di pubblicazione usando il cmdlet [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) .</span><span class="sxs-lookup"><span data-stu-id="01e3f-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="01e3f-193">Pubblicare quindi l'applicazione usando il cmdlet [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) .</span><span class="sxs-lookup"><span data-stu-id="01e3f-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="01e3f-194">Per informazioni sull'accesso, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01e3f-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01e3f-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01e3f-195">Next steps</span></span>
<span data-ttu-id="01e3f-196">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="01e3f-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK per PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definizione del servizio (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configurazione del servizio (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[programma di installazione sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
