---
title: aaaConfigure PHP nelle App Web di servizio App di Azure | Documenti Microsoft
description: Informazioni su come tooconfigure hello installazione PHP predefinita o un'installazione personalizzata di PHP per le app Web in Azure App Service.
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="f27b5-103">Configurazione di PHP nelle app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="f27b5-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="f27b5-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f27b5-104">Introduction</span></span>
<span data-ttu-id="f27b5-105">Questa guida Mostra come tooconfigure hello runtime PHP predefiniti per le app Web in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fornire un runtime PHP personalizzato e abilitare le estensioni.</span><span class="sxs-lookup"><span data-stu-id="f27b5-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="f27b5-106">Servizio App, toouse iscriversi hello [versione di valutazione gratuita].</span><span class="sxs-lookup"><span data-stu-id="f27b5-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="f27b5-107">hello tooget più da questa Guida, è necessario creare prima un'app web PHP nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="f27b5-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="f27b5-108">Procedura: versione PHP modifica hello incorporata</span><span class="sxs-lookup"><span data-stu-id="f27b5-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="f27b5-109">Per impostazione predefinita, PHP 5.5 è installato e immediatamente disponibile per l'uso quando si crea un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="f27b5-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="f27b5-110">migliore toosee hello versione disponibile revisione, la configurazione predefinita, Hello ed estensioni abilitate hello è uno script che chiama hello toodeploy [phpinfo] (funzione).</span><span class="sxs-lookup"><span data-stu-id="f27b5-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="f27b5-111">Sono anche disponibili le versioni PHP 5.6 e PHP 7.0, che però non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f27b5-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="f27b5-112">hello tooupdate versione PHP, seguire uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f27b5-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="f27b5-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f27b5-113">Azure Portal</span></span>
1. <span data-ttu-id="f27b5-114">Esplorare app web tooyour hello [portale Azure](https://portal.azure.com) e fare clic su hello **impostazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f27b5-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
2. <span data-ttu-id="f27b5-116">Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scegliere nuova versione PHP hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Impostazioni dell'applicazione][application-settings]
3. <span data-ttu-id="f27b5-118">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.</span><span class="sxs-lookup"><span data-stu-id="f27b5-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="f27b5-120">Azure PowerShell (solo Windows).</span><span class="sxs-lookup"><span data-stu-id="f27b5-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="f27b5-121">Aprire Azure PowerShell e account di accesso tooyour:</span><span class="sxs-lookup"><span data-stu-id="f27b5-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="f27b5-122">Impostare la versione di PHP hello per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="f27b5-123">versione PHP Hello è ora impostato.</span><span class="sxs-lookup"><span data-stu-id="f27b5-123">hello PHP version is now set.</span></span> <span data-ttu-id="f27b5-124">È possibile verificare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f27b5-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="f27b5-125">Interfaccia della riga di comando di Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="f27b5-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="f27b5-126">toouse hello Azure interfaccia della riga di comando, è necessario **Node.js** installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="f27b5-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="f27b5-127">Aprire Terminal e account di accesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="f27b5-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="f27b5-128">Impostare la versione di PHP hello per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="f27b5-129">versione PHP Hello è ora impostato.</span><span class="sxs-lookup"><span data-stu-id="f27b5-129">hello PHP version is now set.</span></span> <span data-ttu-id="f27b5-130">È possibile verificare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="f27b5-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="f27b5-131">Hello [CLI di Azure 2.0](https://github.com/Azure/azure-cli) sono comandi che sono equivalente toohello precedente:</span><span class="sxs-lookup"><span data-stu-id="f27b5-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="f27b5-132">Procedura: modificare le configurazioni di PHP predefinite hello</span><span class="sxs-lookup"><span data-stu-id="f27b5-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="f27b5-133">Per qualsiasi runtime PHP predefiniti, è possibile modificare le opzioni di configurazione hello seguendo i passaggi di hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f27b5-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="f27b5-134">(per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).</span><span class="sxs-lookup"><span data-stu-id="f27b5-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="f27b5-135">Modifica delle impostazioni di configurazione PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="f27b5-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="f27b5-136">Aggiungere un [. user.ini] tooyour directory radice del file.</span><span class="sxs-lookup"><span data-stu-id="f27b5-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="f27b5-137">Aggiungi configurazione impostazioni toohello `.user.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un `php.ini` file.</span><span class="sxs-lookup"><span data-stu-id="f27b5-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="f27b5-138">Ad esempio, se si desidera hello tooturn `display_errors` impostazione e imposta `upload_max_filesize` too10M, impostando il `.user.ini` file conterrà questo testo:</span><span class="sxs-lookup"><span data-stu-id="f27b5-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="f27b5-139">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f27b5-139">Deploy your web app.</span></span>
4. <span data-ttu-id="f27b5-140">Riavviare l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-140">Restart hello web app.</span></span> <span data-ttu-id="f27b5-141">(Il riavvio è necessario in quanto la frequenza di hello con cui PHP legge `.user.ini` file non sia disciplinato da hello `user_ini.cache_ttl` impostazione, che è 300 secondi (5 minuti) per impostazione predefinita ed è un'impostazione del livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="f27b5-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="f27b5-142">Il riavvio dell'applicazione web di hello forza PHP tooread hello nuove impostazioni in hello `.user.ini` file.)</span><span class="sxs-lookup"><span data-stu-id="f27b5-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="f27b5-143">Come un'alternativa toousing un `.user.ini` file, è possibile utilizzare hello [ini_set()] funzione nelle opzioni di configurazione tooset script che non sono direttive a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="f27b5-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="f27b5-144">Modifica delle impostazioni di configurazione PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="f27b5-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="f27b5-145">Aggiungere un tooyour di impostazione dell'App Web App con la chiave hello `PHP_INI_SCAN_DIR` e valore`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="f27b5-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="f27b5-146">Creare un `settings.ini` file utilizzando la Console Kudu (http://&lt;nome sito&gt;. scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="f27b5-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="f27b5-147">Aggiungi configurazione impostazioni toohello `settings.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un file php.ini.</span><span class="sxs-lookup"><span data-stu-id="f27b5-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="f27b5-148">Ad esempio, se si desidera hello toopoint `curl.cainfo` impostazione tooa `*.crt` file e impostare 'wincache.maxfilesize' impostazione too512K, il `settings.ini` file conterrà questo testo:</span><span class="sxs-lookup"><span data-stu-id="f27b5-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="f27b5-149">Riavviare le modifiche di hello tooload App Web.</span><span class="sxs-lookup"><span data-stu-id="f27b5-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="f27b5-150">Procedura: abilitare le estensioni nel runtime PHP hello predefinito</span><span class="sxs-lookup"><span data-stu-id="f27b5-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="f27b5-151">Come indicato nella sezione precedente hello, versione PHP hello di toosee di hello migliore modalità predefinita, la configurazione predefinita e hello abilitato estensioni è uno script che chiama toodeploy [phpinfo].</span><span class="sxs-lookup"><span data-stu-id="f27b5-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="f27b5-152">tooenable estensioni aggiuntive, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="f27b5-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="f27b5-153">Configurare tramite le impostazioni del file ini</span><span class="sxs-lookup"><span data-stu-id="f27b5-153">Configure via ini settings</span></span>
1. <span data-ttu-id="f27b5-154">Aggiungere un `ext` toohello directory `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="f27b5-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="f27b5-155">Inserire `.dll` i file di estensione in hello `ext` directory (ad esempio, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="f27b5-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="f27b5-156">Assicurarsi che le estensioni di hello sono compatibili con la versione predefinita di PHP e sono VC9 compatibile non thread-safe (punta).</span><span class="sxs-lookup"><span data-stu-id="f27b5-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="f27b5-157">Aggiungere un tooyour di impostazione dell'App Web App con la chiave hello `PHP_INI_SCAN_DIR` e valore`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="f27b5-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="f27b5-158">Creare un `ini` del file in `d:\home\site\ini` chiamato `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="f27b5-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="f27b5-159">Aggiungi configurazione impostazioni toohello `extensions.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un file php.ini.</span><span class="sxs-lookup"><span data-stu-id="f27b5-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="f27b5-160">Ad esempio, se si desidera tooenable hello MongoDB e XDebug le estensioni, i `extensions.ini` file conterrà questo testo:</span><span class="sxs-lookup"><span data-stu-id="f27b5-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="f27b5-161">Riavviare le modifiche di hello tooload App Web.</span><span class="sxs-lookup"><span data-stu-id="f27b5-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="f27b5-162">Configurare tramite impostazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f27b5-162">Configure via App Setting</span></span>
1. <span data-ttu-id="f27b5-163">Aggiungere un `bin` toohello la directory di directory radice.</span><span class="sxs-lookup"><span data-stu-id="f27b5-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="f27b5-164">Inserire `.dll` i file di estensione in hello `bin` directory (ad esempio, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="f27b5-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="f27b5-165">Assicurarsi che le estensioni di hello sono compatibili con la versione predefinita di PHP e sono VC9 compatibile non thread-safe (punta).</span><span class="sxs-lookup"><span data-stu-id="f27b5-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="f27b5-166">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f27b5-166">Deploy your web app.</span></span>
4. <span data-ttu-id="f27b5-167">Esplorare app web tooyour nel portale di Azure hello e fare clic su hello **impostazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f27b5-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
5. <span data-ttu-id="f27b5-169">Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scorrere toohello **impostazioni App** sezione.</span><span class="sxs-lookup"><span data-stu-id="f27b5-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="f27b5-170">In hello **impostazioni App** sezione, creare un **PHP_EXTENSIONS** chiave.</span><span class="sxs-lookup"><span data-stu-id="f27b5-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="f27b5-171">il valore di Hello per questa chiave deve corrispondere a una radice del percorso relativo toowebsite: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="f27b5-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Abilitare le estensioni nelle impostazioni app][php-extensions]
7. <span data-ttu-id="f27b5-173">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.</span><span class="sxs-lookup"><span data-stu-id="f27b5-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

<span data-ttu-id="f27b5-175">Con l'uso di una chiave **PHP_ZENDEXTENSIONS** sono supportate anche le estensioni Zend.</span><span class="sxs-lookup"><span data-stu-id="f27b5-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="f27b5-176">tooenable più estensioni, includere un elenco delimitato da virgole di `.dll` file per valore dell'impostazione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="f27b5-177">Usare un runtime PHP personalizzato</span><span class="sxs-lookup"><span data-stu-id="f27b5-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="f27b5-178">Invece di runtime PHP predefinito hello, App Web del servizio App può usare un runtime PHP fornire tooexecute gli script PHP.</span><span class="sxs-lookup"><span data-stu-id="f27b5-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="f27b5-179">runtime Hello specificata dall'utente può essere configurate da un `php.ini` file che fornisce anche.</span><span class="sxs-lookup"><span data-stu-id="f27b5-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="f27b5-180">toouse un runtime PHP personalizzato con le app Web, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="f27b5-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="f27b5-181">Ottenere una versione compatibile con VC9 o VC11 e non-thread-safe di PHP per Windows.</span><span class="sxs-lookup"><span data-stu-id="f27b5-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="f27b5-182">Versioni recenti di PHP per Windows sono disponibili qui: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="f27b5-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="f27b5-183">Le versioni precedenti sono disponibili nell'archivio di hello qui: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="f27b5-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="f27b5-184">Modificare hello `php.ini` file per il runtime.</span><span class="sxs-lookup"><span data-stu-id="f27b5-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="f27b5-185">Si noti che qualsiasi impostazione di configurazione che non sia una direttiva solo a livello di sistema verrà ignorata da App Web</span><span class="sxs-lookup"><span data-stu-id="f27b5-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="f27b5-186">(per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).</span><span class="sxs-lookup"><span data-stu-id="f27b5-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="f27b5-187">Facoltativamente, aggiungere le estensioni tooyour PHP runtime e abilitarli nel hello `php.ini` file.</span><span class="sxs-lookup"><span data-stu-id="f27b5-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="f27b5-188">Aggiungere un `bin` directory radice di directory tooyour e put hello directory che contiene il runtime PHP in essa contenuti (ad esempio, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="f27b5-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="f27b5-189">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="f27b5-189">Deploy your web app.</span></span>
6. <span data-ttu-id="f27b5-190">Esplorare app web tooyour nel portale di Azure hello e fare clic su hello **impostazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f27b5-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
7. <span data-ttu-id="f27b5-192">Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scorrere toohello **Mapping gestori** sezione.</span><span class="sxs-lookup"><span data-stu-id="f27b5-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="f27b5-193">Aggiungere `*.php` toohello estensione campo e aggiungere hello percorso toohello `php-cgi.exe` eseguibile.</span><span class="sxs-lookup"><span data-stu-id="f27b5-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="f27b5-194">Se si inserisce il runtime PHP in hello `bin` directory nella directory radice dell'applicazione hello, percorso di hello sarà `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="f27b5-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Specificare il gestore nei mapping gestore][handler-mappings]
8. <span data-ttu-id="f27b5-196">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.</span><span class="sxs-lookup"><span data-stu-id="f27b5-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="f27b5-198">Procedura: Abilitare l’automazione Composer in Azure</span><span class="sxs-lookup"><span data-stu-id="f27b5-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="f27b5-199">Per impostazione predefinita, il servizio app non esegue operazioni relative a composer.json, se questo è presente nel progetto PHP.</span><span class="sxs-lookup"><span data-stu-id="f27b5-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="f27b5-200">Se si utilizza [distribuzione Git](app-service-deploy-local-git.md), è possibile abilitare composer.json durante l'elaborazione di `git push` abilitando l'estensione Composer hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="f27b5-201">È possibile [votare qui per il supporto Composer avanzato nel servizio app](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="f27b5-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="f27b5-202">Nel PHP web pannello dell'app in hello [portale di Azure](https://portal.azure.com), fare clic su **strumenti** > **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="f27b5-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Tooenable pannello Impostazioni portale Azure automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="f27b5-204">Fare clic su **Aggiungi**, quindi su **Compositore**.</span><span class="sxs-lookup"><span data-stu-id="f27b5-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Aggiungere l'automazione di Composer Composer estensione tooenable in Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="f27b5-206">Fare clic su **OK** tooaccept legali.</span><span class="sxs-lookup"><span data-stu-id="f27b5-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="f27b5-207">Fare clic su **OK** nuovamente tooadd estensione di hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="f27b5-208">Hello **estensioni installate** pannello verrà visualizzati estensione Composer hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="f27b5-209">![Accettare i termini legali specifici tooenable Composer automazione Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="f27b5-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="f27b5-210">A questo punto, eseguire `git add`, `git commit`, e `git push` come nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="f27b5-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="f27b5-211">Si noterà che ora Composer installa le dipendenze definite in composer.json.</span><span class="sxs-lookup"><span data-stu-id="f27b5-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Distribuzione Git con l’automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="f27b5-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f27b5-213">Next steps</span></span>
<span data-ttu-id="f27b5-214">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f27b5-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="f27b5-215">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="f27b5-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f27b5-216">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="f27b5-216">No credit cards required; no commitments.</span></span>
> 
> 

[versione di valutazione gratuita]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Lista delle direttive php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

