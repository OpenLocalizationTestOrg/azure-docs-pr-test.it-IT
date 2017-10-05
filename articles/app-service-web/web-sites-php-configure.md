---
title: Configurare PHP nelle app Web del Servizio app di Azure | Microsoft Doc
description: Informazioni su come configurare l'installazione predefinita di PHP o aggiungere un'installazione personalizzata di PHP in Servizio app di Azure."
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="930fa-103">Configurazione di PHP nelle app Web di Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="930fa-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="930fa-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="930fa-104">Introduction</span></span>
<span data-ttu-id="930fa-105">In questa guida verrà descritto come configurare il runtime PHP incorporato in App Web per [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714), fornire un PHP personalizzato runtime e abilitare le estensioni.</span><span class="sxs-lookup"><span data-stu-id="930fa-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="930fa-106">Per usare Servizio app di Azure, effettuare l'iscrizione per ricevere la versione di [valutazione gratuita].</span><span class="sxs-lookup"><span data-stu-id="930fa-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="930fa-107">Per ottenere il massimo da questa guida, è necessario innanzitutto creare un'app Web PHP in Servizio app.</span><span class="sxs-lookup"><span data-stu-id="930fa-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="930fa-108">Procedura: modificare la versione PHP incorporata</span><span class="sxs-lookup"><span data-stu-id="930fa-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="930fa-109">Per impostazione predefinita, PHP 5.5 è installato e immediatamente disponibile per l'uso quando si crea un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="930fa-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="930fa-110">Il modo migliore per visualizzare la revisione della versione disponibile, la sua configurazione predefinita e le estensioni abilitate consiste nel distribuire uno script che chiama la funzione [phpinfo ()] .</span><span class="sxs-lookup"><span data-stu-id="930fa-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="930fa-111">Sono anche disponibili le versioni PHP 5.6 e PHP 7.0, che però non sono abilitate per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="930fa-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="930fa-112">Per aggiornare la versione di PHP, seguire uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="930fa-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="930fa-113">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="930fa-113">Azure Portal</span></span>
1. <span data-ttu-id="930fa-114">Passare all'app Web nel [Portale di Azure](https://portal.azure.com) e fare clic sul pulsante **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="930fa-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
2. <span data-ttu-id="930fa-116">Dal pannello **Impostazioni** selezionare **Impostazioni dell'applicazione** e scegliere la nuova versione di PHP.</span><span class="sxs-lookup"><span data-stu-id="930fa-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Impostazioni dell'applicazione][application-settings]
3. <span data-ttu-id="930fa-118">Fare clic sul pulsante **Salva** all'inizio del pannello **Impostazioni app Web**.</span><span class="sxs-lookup"><span data-stu-id="930fa-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="930fa-120">Azure PowerShell (solo Windows).</span><span class="sxs-lookup"><span data-stu-id="930fa-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="930fa-121">Aprire Azure PowerShell e accedere al proprio account:</span><span class="sxs-lookup"><span data-stu-id="930fa-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="930fa-122">Impostare la versione PHP per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="930fa-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="930fa-123">La versione di PHP è ora impostata.</span><span class="sxs-lookup"><span data-stu-id="930fa-123">The PHP version is now set.</span></span> <span data-ttu-id="930fa-124">È possibile verificare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="930fa-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="930fa-125">Interfaccia della riga di comando di Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="930fa-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="930fa-126">Per usare l'interfaccia della riga di comando di Azure, è necessario che **Node.js** sia installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="930fa-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="930fa-127">Aprire il terminale e accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="930fa-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="930fa-128">Impostare la versione PHP per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="930fa-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="930fa-129">La versione di PHP è ora impostata.</span><span class="sxs-lookup"><span data-stu-id="930fa-129">The PHP version is now set.</span></span> <span data-ttu-id="930fa-130">È possibile verificare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="930fa-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="930fa-131">I comandi dell'[interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) equivalenti a quanto riportato sopra sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="930fa-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="930fa-132">Modificare la configurazione PHP incorporata</span><span class="sxs-lookup"><span data-stu-id="930fa-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="930fa-133">Per qualsiasi runtime PHP incorporato, è possibile modificare le opzioni di configurazione eseguendo la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="930fa-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="930fa-134">(per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).</span><span class="sxs-lookup"><span data-stu-id="930fa-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="930fa-135">Modifica delle impostazioni di configurazione PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="930fa-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="930fa-136">Aggiungere un file [.user.ini] alla directory radice in uso.</span><span class="sxs-lookup"><span data-stu-id="930fa-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="930fa-137">Aggiungere le impostazioni di configurazione al file  `.user.ini` usando la stessa sintassi che si userebbe in un file `php.ini`.</span><span class="sxs-lookup"><span data-stu-id="930fa-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="930fa-138">Ad esempio, se si desidera attivare l'impostazione `display_errors` e configurare l'impostazione `upload_max_filesize` su 10M, il file `.user.ini` conterrà il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="930fa-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="930fa-139">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="930fa-139">Deploy your web app.</span></span>
4. <span data-ttu-id="930fa-140">Riavviare l'app Web .</span><span class="sxs-lookup"><span data-stu-id="930fa-140">Restart the web app.</span></span> <span data-ttu-id="930fa-141">Il riavvio è necessario in quanto la frequenza di lettura dei file `.user.ini` a parte di PHP è governata dall'impostazione `user_ini.cache_ttl` configurata a livello di sistema, che per impostazione predefinita corrisponde a 300 secondi (5 minuti).</span><span class="sxs-lookup"><span data-stu-id="930fa-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="930fa-142">Il riavvio del sito forza PHP a leggere le nuove impostazioni nel file `.user.ini` .</span><span class="sxs-lookup"><span data-stu-id="930fa-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="930fa-143">In alternativa a un file `.user.ini` è possibile usare la funzione [ini_set()] negli script per impostare le opzioni di configurazione che non sono direttive a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="930fa-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="930fa-144">Modifica delle impostazioni di configurazione PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="930fa-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="930fa-145">Aggiungere un'impostazione dell'applicazione all'applicazione Web con la chiave `PHP_INI_SCAN_DIR` e valore `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="930fa-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="930fa-146">Creare un file `settings.ini` usando la console Kudu (http://&lt;site-name&gt;.scm.azurewebsite.net) nella directory `d:\home\site\ini`.</span><span class="sxs-lookup"><span data-stu-id="930fa-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="930fa-147">Aggiungere le impostazioni di configurazione al file `settings.ini` utilizzando la stessa sintassi che si userebbe in un file php.ini.</span><span class="sxs-lookup"><span data-stu-id="930fa-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="930fa-148">Ad esempio, se si desidera fare riferimento il `curl.cainfo` impostazione su un `*.crt` file e impostare su 512K 'wincache.maxfilesize' impostazione del `settings.ini` file conterrebbe il testo:</span><span class="sxs-lookup"><span data-stu-id="930fa-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="930fa-149">Riavviare l'applicazione Web per caricare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="930fa-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="930fa-150">Abilitare le estensioni nel runtime PHP predefinito</span><span class="sxs-lookup"><span data-stu-id="930fa-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="930fa-151">Come indicato nella sezione precedente, il modo migliore per visualizzare la versione PHP disponibile, la sua configurazione predefinita e le estensioni abilitate consiste nel distribuire uno script che chiama la funzione [phpinfo ()].</span><span class="sxs-lookup"><span data-stu-id="930fa-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="930fa-152">Per abilitare le estensioni aggiuntive, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="930fa-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="930fa-153">Configurare tramite le impostazioni del file ini</span><span class="sxs-lookup"><span data-stu-id="930fa-153">Configure via ini settings</span></span>
1. <span data-ttu-id="930fa-154">Aggiungere una `ext` directory alla `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="930fa-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="930fa-155">Inserire i file con estensione `.dll` nella directory `ext` (ad esempio `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="930fa-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="930fa-156">Verificare che le estensioni siano compatibili con la versione predefinita di PHP e con VC9 e non thread-safe (nts).</span><span class="sxs-lookup"><span data-stu-id="930fa-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="930fa-157">Aggiungere un'impostazione dell'applicazione all'applicazione Web con la chiave `PHP_INI_SCAN_DIR` e valore `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="930fa-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="930fa-158">Creare un `ini` del file in `d:\home\site\ini` chiamato `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="930fa-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="930fa-159">Aggiungere le impostazioni di configurazione al file `extensions.ini` utilizzando la stessa sintassi che si userebbe in un file php.ini.</span><span class="sxs-lookup"><span data-stu-id="930fa-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="930fa-160">Ad esempio, se si desidera abilitare le estensioni di MongoDB e XDebug il `extensions.ini` file conterrebbe il testo:</span><span class="sxs-lookup"><span data-stu-id="930fa-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="930fa-161">Riavviare l'applicazione Web per caricare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="930fa-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="930fa-162">Configurare tramite impostazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="930fa-162">Configure via App Setting</span></span>
1. <span data-ttu-id="930fa-163">Aggiungere una `bin` directory alla directory radice.</span><span class="sxs-lookup"><span data-stu-id="930fa-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="930fa-164">Inserire i file con estensione `.dll` nella directory `bin` (ad esempio `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="930fa-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="930fa-165">Verificare che le estensioni siano compatibili con la versione predefinita di PHP e con VC9 e non thread-safe (nts).</span><span class="sxs-lookup"><span data-stu-id="930fa-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="930fa-166">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="930fa-166">Deploy your web app.</span></span>
4. <span data-ttu-id="930fa-167">Passare all'app Web nel Portale di Azure e fare clic sul pulsante **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="930fa-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
5. <span data-ttu-id="930fa-169">Dal pannello **Impostazioni** selezionare **Impostazioni dell'applicazione** e scorrere fino alla sezione **Impostazioni app**.</span><span class="sxs-lookup"><span data-stu-id="930fa-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="930fa-170">Nella sezione **Impostazioni app** creare una chiave **PHP_EXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="930fa-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="930fa-171">Il valore di questa chiave deve corrispondere a un percorso relativo alla radice del sito Web: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="930fa-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![Abilitare le estensioni nelle impostazioni app][php-extensions]
7. <span data-ttu-id="930fa-173">Fare clic sul pulsante **Salva** all'inizio del pannello **Impostazioni app Web**.</span><span class="sxs-lookup"><span data-stu-id="930fa-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

<span data-ttu-id="930fa-175">Con l'uso di una chiave **PHP_ZENDEXTENSIONS** sono supportate anche le estensioni Zend.</span><span class="sxs-lookup"><span data-stu-id="930fa-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="930fa-176">Per abilitare più estensioni, includere un elenco separato da virgole di `.dll` file per il valore dell'impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="930fa-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="930fa-177">Usare un runtime PHP personalizzato</span><span class="sxs-lookup"><span data-stu-id="930fa-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="930fa-178">Invece del runtime PHP predefinito, App Web di Servizio Web può utilizzare un runtime PHP fornito dall'utente per l'esecuzione degli script PHP.</span><span class="sxs-lookup"><span data-stu-id="930fa-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="930fa-179">Quest'ultimo può essere configurato da un file `php.ini` analogamente fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="930fa-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="930fa-180">Per usare un runtime PHP personalizzato con App Web, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="930fa-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="930fa-181">Ottenere una versione compatibile con VC9 o VC11 e non-thread-safe di PHP per Windows.</span><span class="sxs-lookup"><span data-stu-id="930fa-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="930fa-182">Versioni recenti di PHP per Windows sono disponibili qui: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="930fa-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="930fa-183">Versioni precedenti sono disponibili nell'archivio qui: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="930fa-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="930fa-184">Modificare il file `php.ini` per il proprio runtime.</span><span class="sxs-lookup"><span data-stu-id="930fa-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="930fa-185">Si noti che qualsiasi impostazione di configurazione che non sia una direttiva solo a livello di sistema verrà ignorata da App Web</span><span class="sxs-lookup"><span data-stu-id="930fa-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="930fa-186">(per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).</span><span class="sxs-lookup"><span data-stu-id="930fa-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="930fa-187">Facoltativamente, aggiungere le estensioni al proprio runtime PHP e abilitarle nel file `php.ini` .</span><span class="sxs-lookup"><span data-stu-id="930fa-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="930fa-188">Aggiungere una directory `bin` alla propria directory radice e inserirvi la directory contenente il proprio runtime PHP (ad esempio, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="930fa-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="930fa-189">Distribuire l'app Web.</span><span class="sxs-lookup"><span data-stu-id="930fa-189">Deploy your web app.</span></span>
6. <span data-ttu-id="930fa-190">Passare all'app Web nel Portale di Azure e fare clic sul pulsante **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="930fa-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Impostazioni app Web][settings-button]
7. <span data-ttu-id="930fa-192">Dal pannello **Impostazioni** selezionare **Impostazioni applicazione** e scorrere fino alla sezione **Mapping del gestore**.</span><span class="sxs-lookup"><span data-stu-id="930fa-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="930fa-193">Aggiungere `*.php` al campo Estensione e aggiungere il percorso dell'eseguibile `php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="930fa-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="930fa-194">Se si inserisce il proprio runtime PHP nella directory `bin` nella radice dell'applicazione, il percorso sarà `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="930fa-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Specificare il gestore nei mapping gestore][handler-mappings]
8. <span data-ttu-id="930fa-196">Fare clic sul pulsante **Salva** all'inizio del pannello **Impostazioni app Web**.</span><span class="sxs-lookup"><span data-stu-id="930fa-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvare le impostazioni di configurazione][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="930fa-198">Procedura: Abilitare l’automazione Composer in Azure</span><span class="sxs-lookup"><span data-stu-id="930fa-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="930fa-199">Per impostazione predefinita, il servizio app non esegue operazioni relative a composer.json, se questo è presente nel progetto PHP.</span><span class="sxs-lookup"><span data-stu-id="930fa-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="930fa-200">Se si usa la [distribuzione Git](app-service-deploy-local-git.md), è possibile abilitare l'elaborazione di composer.json durante l'operazione di `git push` abilitando l'estensione Composer.</span><span class="sxs-lookup"><span data-stu-id="930fa-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="930fa-201">È possibile [votare qui per il supporto Composer avanzato nel servizio app](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="930fa-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="930fa-202">Nel pannello dell'app Web PHP nel [portale di Azure](https://portal.azure.com) fare clic su **Strumenti** > **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="930fa-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Pannello delle impostazioni del portale di Azure per abilitare l'automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="930fa-204">Fare clic su **Aggiungi**, quindi su **Compositore**.</span><span class="sxs-lookup"><span data-stu-id="930fa-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Aggiungere l’estensione Composer per abilitare l’automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="930fa-206">Fare clic su **OK** per accettare le note legali.</span><span class="sxs-lookup"><span data-stu-id="930fa-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="930fa-207">Fare di nuovo clic su **OK** per aggiungere l'estensione.</span><span class="sxs-lookup"><span data-stu-id="930fa-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="930fa-208">Nel pannello **Estensioni installate** è ora visualizzata l'estensione Compositore.</span><span class="sxs-lookup"><span data-stu-id="930fa-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="930fa-209">![Accettare le note legali per abilitare l'automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="930fa-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="930fa-210">Eseguire ora `git add`, `git commit` e `git push` come nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="930fa-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="930fa-211">Si noterà che ora Composer installa le dipendenze definite in composer.json.</span><span class="sxs-lookup"><span data-stu-id="930fa-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Distribuzione Git con l’automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="930fa-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="930fa-213">Next steps</span></span>
<span data-ttu-id="930fa-214">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="930fa-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="930fa-215">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="930fa-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="930fa-216">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="930fa-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="930fa-217">[valutazione gratuita]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="930fa-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="930fa-218">[phpinfo ()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="930fa-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="930fa-219">[Lista delle direttive php.ini]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="930fa-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="930fa-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="930fa-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="930fa-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="930fa-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="930fa-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="930fa-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="930fa-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="930fa-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

