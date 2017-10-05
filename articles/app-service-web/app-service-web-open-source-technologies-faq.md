---
title: Domande frequenti sulle tecnologie open source per App Web di Azure | Microsoft Docs
description: "È possibile ottenere risposte alle domande frequenti sulle tecnologie open source nella funzionalità App Web del servizio app di Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="56522-103">Domande frequenti sulle tecnologie open source per App Web in Azure</span><span class="sxs-lookup"><span data-stu-id="56522-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="56522-104">Questo articolo fornisce risposte alle domande frequenti sui problemi relativi alle tecnologie per la [funzionalità App Web del servizio app di Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="56522-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="56522-105">Il database ClearDB è inattivo.</span><span class="sxs-lookup"><span data-stu-id="56522-105">My ClearDB database is down.</span></span> <span data-ttu-id="56522-106">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="56522-106">How do I resolve this?</span></span>

<span data-ttu-id="56522-107">Per i problemi relativi ai database, contattare il [supporto tecnico di ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="56522-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="56522-108">Per risposte alle domande frequenti su ClearDB, vedere [Domande frequenti su ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="56522-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="56522-109">Perché il database ClearDB non è elencato nel portale?</span><span class="sxs-lookup"><span data-stu-id="56522-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="56522-110">Se si crea un database ClearDB nel [portale di Azure](http://portal.azure.com/), il database non viene visualizzato nel [portale di Azure classico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="56522-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="56522-111">Per risolvere il problema, è possibile collegare manualmente il database all'app Web.</span><span class="sxs-lookup"><span data-stu-id="56522-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="56522-112">Analogamente, se si crea un database ClearDB nel [portale di Azure classico](http://manage.windowsazure.com/), il database non verrà visualizzato nel [portale di Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="56522-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="56522-113">In questo caso non sono disponibili soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="56522-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="56522-114">Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="56522-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="56522-115">Per quale ragione non è stata eseguita la migrazione del database ClearDB durante la migrazione della sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="56522-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="56522-116">Quando si esegue la migrazione delle risorse tra le sottoscrizioni, esistono alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="56522-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="56522-117">Il database MySQL ClearDB è un servizio di terze parti e non viene sottoposto a migrazione durante la migrazione di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="56522-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="56522-118">Se non si gestisce la migrazione del database MySQL prima della migrazione delle risorse di Azure, è possibile che il database MySQL ClearDB non sia disponibile.</span><span class="sxs-lookup"><span data-stu-id="56522-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="56522-119">Per evitare questo problema, eseguire manualmente la migrazione del database ClearDB e quindi eseguire la migrazione della sottoscrizione di Azure per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="56522-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="56522-120">Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="56522-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="56522-121">Come si attiva la registrazione PHP per risolvere i problemi relativi a PHP?</span><span class="sxs-lookup"><span data-stu-id="56522-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="56522-122">Per attivare la registrazione PHP:</span><span class="sxs-lookup"><span data-stu-id="56522-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="56522-123">Accedere al [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="56522-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="56522-124">Nel menu in alto selezionare **Debug Console** (Console di debug)  > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="56522-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="56522-125">Selezionare la cartella **Site** (Sito).</span><span class="sxs-lookup"><span data-stu-id="56522-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="56522-126">Selezionare la cartella **wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="56522-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="56522-127">Selezionare l'icona **+** e quindi selezionare **New File** (Nuovo file).</span><span class="sxs-lookup"><span data-stu-id="56522-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="56522-128">Impostare **.user.ini** come nome del file.</span><span class="sxs-lookup"><span data-stu-id="56522-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="56522-129">Selezionare l'icona della matita accanto a **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="56522-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="56522-130">Nel file aggiungere questo codice: `log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="56522-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="56522-131">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="56522-131">Select **Save**.</span></span>
10. <span data-ttu-id="56522-132">Selezionare l'icona della matita accanto a **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="56522-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="56522-133">Modificare il testo specificando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="56522-134">Nel portale di Azure riavviare l'app Web dal menu corrispondente.</span><span class="sxs-lookup"><span data-stu-id="56522-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="56522-135">Per altre informazioni, vedere [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Abilitare i log degli errori di WordPress).</span><span class="sxs-lookup"><span data-stu-id="56522-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="56522-136">Come si registrano gli errori delle applicazioni Python in app ospitate nel servizio app?</span><span class="sxs-lookup"><span data-stu-id="56522-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="56522-137">Per acquisire gli errori delle applicazioni Python:</span><span class="sxs-lookup"><span data-stu-id="56522-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="56522-138">Nel portale di Azure selezionare **Impostazioni** nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="56522-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="56522-139">Nella scheda **Impostazioni** selezionare **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="56522-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="56522-140">In **Impostazioni dell'applicazione** immettere la coppia chiave/valore seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="56522-141">Chiave : WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="56522-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="56522-142">Valore : D:\home\site\wwwroot\logs.txt (immettere il nome file scelto)</span><span class="sxs-lookup"><span data-stu-id="56522-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="56522-143">Gli errori dovrebbero essere ora visualizzati nel file logs.txt nella cartella wwwroot.</span><span class="sxs-lookup"><span data-stu-id="56522-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="56522-144">Come si cambia la versione dell'applicazione Node.js ospitata nel servizio app?</span><span class="sxs-lookup"><span data-stu-id="56522-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="56522-145">Per cambiare la versione dell'applicazione Node.js, è possibile usare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56522-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="56522-146">Nel portale di Azure usare **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="56522-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="56522-147">Nel portale di Azure passare all'app Web.</span><span class="sxs-lookup"><span data-stu-id="56522-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="56522-148">Nel pannello **Impostazioni** selezionare **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="56522-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="56522-149">In **Impostazioni dell'applicazione** è possibile includere WEBSITE_NODE_DEFAULT_VERSION come chiave e la versione di Node.js da usare come valore.</span><span class="sxs-lookup"><span data-stu-id="56522-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="56522-150">Passare alla [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="56522-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="56522-151">Per verificare la versione di Node.js, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="56522-152">Modificare il file iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="56522-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="56522-153">La modifica della versione di Node.js nel file iisnode.yml consente solo di configurare l'ambiente di runtime usato da iisnode.</span><span class="sxs-lookup"><span data-stu-id="56522-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="56522-154">Kudu CMD e altre applicazioni usano ancora la versione Node.js specificata in **Impostazioni dell'applicazione** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="56522-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="56522-155">Per configurare manualmente iisnode.yml, creare un file iisnode.yml nella cartella radice dell'app.</span><span class="sxs-lookup"><span data-stu-id="56522-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="56522-156">Nel file includere la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="56522-157">Configurare il file iisnode.yml usando package.json durante la distribuzione del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="56522-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="56522-158">Il processo di distribuzione del controllo del codice sorgente di Azure prevede la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="56522-159">Spostamento del contenuto nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="56522-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="56522-160">Creazione di uno script di distribuzione predefinito, se non è già presente (file deploy.cmd, file con estensione deployment), nella cartella radice dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="56522-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="56522-161">Esecuzione di uno script di distribuzione in cui viene creato un file iisnode.yml file se si indica la versione di Node.js nel file package.json > motore `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="56522-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="56522-162">Il file iisnode.yml include la riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="56522-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="56522-163">Viene visualizzato il messaggio "Errore di connessione al database" nell'app WordPress ospitata nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="56522-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="56522-164">Come si risolve il problema?</span><span class="sxs-lookup"><span data-stu-id="56522-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="56522-165">Se viene visualizzato questo errore nell'app Azure WordPress, per abilitare php_errors.log e debug.log completare la procedura illustrata in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Abilitare i log degli errori di WordPress).</span><span class="sxs-lookup"><span data-stu-id="56522-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="56522-166">Quando i log sono abilitati, riprodurre l'errore e quindi controllare i log per verificare se le connessioni sono quasi esaurite:</span><span class="sxs-lookup"><span data-stu-id="56522-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="56522-167">Se viene visualizzato questo errore nei file debug.log o php_errors.log, l'app ha superato il numero di connessioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="56522-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="56522-168">Se l'hosting viene eseguito su ClearDB, verificare il numero di connessioni disponibili nel [piano di servizio](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="56522-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="56522-169">Come si esegue il debug di un'app Node.js ospitata nel servizio app?</span><span class="sxs-lookup"><span data-stu-id="56522-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="56522-170">Passare alla [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="56522-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="56522-171">Passare alla cartella dei log dell'applicazione (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="56522-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="56522-172">Nel file logging_errors.txt controllare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="56522-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="56522-173">Come si installano i moduli Python nativi in un'app Web o in un'app per le API del servizio app?</span><span class="sxs-lookup"><span data-stu-id="56522-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="56522-174">È possibile che alcuni pacchetti non vengano installati tramite PIP in Azure.</span><span class="sxs-lookup"><span data-stu-id="56522-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="56522-175">È possibile che il pacchetto non sia disponibile in PIP (Python Package Index) o che sia necessario un compilatore. I compilatori non sono disponibili nei computer che eseguono app Web nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="56522-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="56522-176">Per informazioni sull'installazione dei moduli nativi nelle app Web e nelle app per le API del servizio app, vedere [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Installare moduli Python nel servizio app).</span><span class="sxs-lookup"><span data-stu-id="56522-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="56522-177">Come si distribuisce un'app Django nel servizio app usando Git e la nuova versione di Python?</span><span class="sxs-lookup"><span data-stu-id="56522-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="56522-178">Per informazioni sull'installazione di Django, vedere [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/) (Distribuzione di un'app Django nel servizio app).</span><span class="sxs-lookup"><span data-stu-id="56522-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="56522-179">Dove si trovano i file di log di Tomcat?</span><span class="sxs-lookup"><span data-stu-id="56522-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="56522-180">Per Azure Marketplace e per le distribuzioni personalizzate:</span><span class="sxs-lookup"><span data-stu-id="56522-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="56522-181">Percorso della cartella: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="56522-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="56522-182">File rilevanti:</span><span class="sxs-lookup"><span data-stu-id="56522-182">Files of interest:</span></span>
    * <span data-ttu-id="56522-183">catalina.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-184">host-manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-185">localhost.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-186">manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-187">site_access_log.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="56522-188">Per distribuzioni di tipo **Impostazioni dell'app** nel portale:</span><span class="sxs-lookup"><span data-stu-id="56522-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="56522-189">Percorso della cartella: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="56522-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="56522-190">File rilevanti:</span><span class="sxs-lookup"><span data-stu-id="56522-190">Files of interest:</span></span>
    * <span data-ttu-id="56522-191">catalina.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-192">host-manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-193">localhost.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-194">manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="56522-195">site_access_log.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="56522-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="56522-196">Come si risolvono gli errori di connessione del driver JDBC?</span><span class="sxs-lookup"><span data-stu-id="56522-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="56522-197">È possibile che venga visualizzato il messaggio seguente nei log di Tomcat:</span><span class="sxs-lookup"><span data-stu-id="56522-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="56522-198">Per risolvere l'errore:</span><span class="sxs-lookup"><span data-stu-id="56522-198">To resolve the error:</span></span>

1. <span data-ttu-id="56522-199">Rimuovere il file sqljdbc*.jar dalla cartella app/lib.</span><span class="sxs-lookup"><span data-stu-id="56522-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="56522-200">Se si usa il server Web Tomcat o Azure Marketplace Tomcat personalizzato, copiare questo file con estensione jar nella cartella lib di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="56522-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="56522-201">Se si abilita Java dal portale di Azure, selezionando **Java 1.8** > **Tomcat server** (Server Tomcat), copiare il file sqljdbc.* jar nella cartella parallela all'app specifica.</span><span class="sxs-lookup"><span data-stu-id="56522-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="56522-202">Aggiungere quindi l'impostazione classpath seguente al file web.config:</span><span class="sxs-lookup"><span data-stu-id="56522-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="56522-203">Perché vengono visualizzati errori quando si prova a copiare i file di log attivi?</span><span class="sxs-lookup"><span data-stu-id="56522-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="56522-204">Se si prova a copiare i file di log attivi per un'app Java (ad esempio, Tomcat), è possibile che venga visualizzato questo errore FTP:</span><span class="sxs-lookup"><span data-stu-id="56522-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="56522-205">Il messaggio di errore può variare in base al client FTP.</span><span class="sxs-lookup"><span data-stu-id="56522-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="56522-206">Tutte le app Java presentano questo errore di blocco.</span><span class="sxs-lookup"><span data-stu-id="56522-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="56522-207">Solo Kudu supporta il download di questo file durante l'esecuzione dell'app.</span><span class="sxs-lookup"><span data-stu-id="56522-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="56522-208">L'arresto dell'app consente a FTP di accedere a questi file.</span><span class="sxs-lookup"><span data-stu-id="56522-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="56522-209">Un'altra soluzione consiste nello scrivere un processo Web eseguito in base a una pianificazione che copia questi file in una directory diversa.</span><span class="sxs-lookup"><span data-stu-id="56522-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="56522-210">Per un progetto di esempio, vedere il progetto [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob).</span><span class="sxs-lookup"><span data-stu-id="56522-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="56522-211">Dove si trovano i file di log per Jetty?</span><span class="sxs-lookup"><span data-stu-id="56522-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="56522-212">Per il Marketplace e le distribuzioni personalizzate il file di log si trova nella cartella D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="56522-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="56522-213">Si noti che il percorso della cartella dipende dalla versione di Jetty in uso.</span><span class="sxs-lookup"><span data-stu-id="56522-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="56522-214">Ad esempio, il percorso specificato qui è per Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="56522-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="56522-215">Cercare jetty_*AAAA_MM_GG*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="56522-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="56522-216">Per le distribuzioni di tipo Impostazioni dell'app nel portale il file si trova in D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="56522-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="56522-217">Cercare jetty_*AAAA_MM_GG*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="56522-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="56522-218">È possibile inviare messaggi di posta elettronica dall'app Web di Azure?</span><span class="sxs-lookup"><span data-stu-id="56522-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="56522-219">Il servizio app non include alcuna funzionalità di posta elettronica predefinita.</span><span class="sxs-lookup"><span data-stu-id="56522-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="56522-220">Per alternative valide per l'invio di messaggi di posta elettronica dall'app, vedere questa [discussione su Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="56522-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="56522-221">Perché il sito WordPress reindirizza a un altro URL?</span><span class="sxs-lookup"><span data-stu-id="56522-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="56522-222">Se è stata eseguita di recente la migrazione ad Azure, è possibile che WordPress reindirizzi all'URL di dominio precedente.</span><span class="sxs-lookup"><span data-stu-id="56522-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="56522-223">Questo problema è causato da un'impostazione nel database MySQL.</span><span class="sxs-lookup"><span data-stu-id="56522-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="56522-224">WordPress Buddy+ è un'estensione del sito di Azure che consente di aggiornare l'URL di reindirizzamento direttamente nel database.</span><span class="sxs-lookup"><span data-stu-id="56522-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="56522-225">Per altre informazioni sull'uso di WordPress Buddy+, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="56522-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="56522-226">In alternativa, se si preferisce aggiornare manualmente l'URL di reindirizzamento usando query SQL o PHPMyAdmin, vedere [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/) (WordPress: Reindirizzamento all'URL errato).</span><span class="sxs-lookup"><span data-stu-id="56522-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="56522-227">Come si modifica la password di accesso di WordPress?</span><span class="sxs-lookup"><span data-stu-id="56522-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="56522-228">Se si dimentica la password di accesso di WordPress, è possibile usare WordPress Buddy+ per aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="56522-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="56522-229">Per reimpostare la password, installare l'estensione WordPress Buddy+ del sito di Azure e quindi completare la procedura descritta in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="56522-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="56522-230">Non è possibile accedere a WordPress.</span><span class="sxs-lookup"><span data-stu-id="56522-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="56522-231">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="56522-231">How do I resolve this?</span></span>

<span data-ttu-id="56522-232">Se non è possibile accedere a WordPress dopo l'installazione recente di un plug-in, è possibile che il plug-in sia danneggiato.</span><span class="sxs-lookup"><span data-stu-id="56522-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="56522-233">WordPress Buddy+ è un'estensione del sito di Azure che consente di disabilitare i plug-in in WordPress.</span><span class="sxs-lookup"><span data-stu-id="56522-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="56522-234">Per altre informazioni, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="56522-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="56522-235">Come si esegue la migrazione del database di WordPress?</span><span class="sxs-lookup"><span data-stu-id="56522-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="56522-236">Sono disponibili diverse opzioni per la migrazione del database MySQL connesso al sito Web WordPress:</span><span class="sxs-lookup"><span data-stu-id="56522-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="56522-237">Sviluppatori: usare il [prompt dei comandi o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="56522-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="56522-238">Non sviluppatori: usare [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="56522-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="56522-239">Come si migliora la protezione di WordPress?</span><span class="sxs-lookup"><span data-stu-id="56522-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="56522-240">Per informazioni sulle procedure consigliate per la sicurezza di WordPress, vedere [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/) (Procedure consigliate per la sicurezza di WordPress in Azure).</span><span class="sxs-lookup"><span data-stu-id="56522-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="56522-241">Si sta provando a usare PHPMyAdmin e viene visualizzato il messaggio "Accesso negato".</span><span class="sxs-lookup"><span data-stu-id="56522-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="56522-242">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="56522-242">How do I resolve this?</span></span>

<span data-ttu-id="56522-243">È possibile che si verifichi questo problema se la funzionalità MySQL in-app non è ancora in esecuzione in questa istanza del servizio app.</span><span class="sxs-lookup"><span data-stu-id="56522-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="56522-244">Per risolvere il problema, provare ad accedere al sito Web.</span><span class="sxs-lookup"><span data-stu-id="56522-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="56522-245">Verranno avviati i processi necessari, incluso il processo MySQL in-app.</span><span class="sxs-lookup"><span data-stu-id="56522-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="56522-246">Per verificare che il processo MySQL in-app sia in esecuzione, in Esplora processi assicurarsi che mysqld.exe sia elencato nei processi.</span><span class="sxs-lookup"><span data-stu-id="56522-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="56522-247">Dopo avere verificato che MySQL in-app è in esecuzione, provare a usare PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="56522-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="56522-248">Viene visualizzato un errore HTTP 403 quando si prova a importare o esportare il database di MySQL in-app usando PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="56522-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="56522-249">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="56522-249">How do I resolve this?</span></span>

<span data-ttu-id="56522-250">Se si usa una versione precedente di Chrome, è possibile che si riscontri un bug noto.</span><span class="sxs-lookup"><span data-stu-id="56522-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="56522-251">Per risolvere il problema, eseguire l'aggiornamento a una versione più recente di Chrome.</span><span class="sxs-lookup"><span data-stu-id="56522-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="56522-252">Provare anche a usare un browser diverso, ad esempio Internet Explorer o Microsoft Edge, in cui non si verifica il problema.</span><span class="sxs-lookup"><span data-stu-id="56522-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
