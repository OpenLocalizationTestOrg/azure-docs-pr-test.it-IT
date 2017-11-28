---
title: le app web tecnologie aaaOpen origine domande frequenti su Azure | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti sulle tecnologie open source in funzionalità App Web hello di servizio App di Azure."
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
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="e88e1-103">Domande frequenti sulle tecnologie open source per App Web in Azure</span><span class="sxs-lookup"><span data-stu-id="e88e1-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="e88e1-104">In questo articolo ha toofrequently risposte domande frequenti (FAQ) sui problemi relativi a tecnologie open source per hello [funzionalità App Web di Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="e88e1-105">Il database ClearDB è inattivo.</span><span class="sxs-lookup"><span data-stu-id="e88e1-105">My ClearDB database is down.</span></span> <span data-ttu-id="e88e1-106">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="e88e1-106">How do I resolve this?</span></span>

<span data-ttu-id="e88e1-107">Per i problemi relativi ai database, contattare il [supporto tecnico di ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="e88e1-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="e88e1-108">Per le risposte toocommon domande ClearDB, vedere [domande frequenti su ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="e88e1-109">Perché il database ClearDB non è elencato nel portale di hello?</span><span class="sxs-lookup"><span data-stu-id="e88e1-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="e88e1-110">Se si crea un database ClearDB in hello [portale di Azure](http://portal.azure.com/), database hello non viene visualizzato in hello [portale di Azure classico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="e88e1-111">toowork il problema, è possibile collegare manualmente l'app web toohello di database.</span><span class="sxs-lookup"><span data-stu-id="e88e1-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="e88e1-112">Analogamente, se si crea un database ClearDB in hello [portale di Azure classico](http://manage.windowsazure.com/), non verrà visualizzato il database in hello [portale di Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="e88e1-113">In questo caso non sono disponibili soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="e88e1-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="e88e1-114">Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="e88e1-115">Per quale ragione non è stata eseguita la migrazione del database ClearDB durante la migrazione della sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="e88e1-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="e88e1-116">Quando si esegue la migrazione delle risorse tra le sottoscrizioni, esistono alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="e88e1-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="e88e1-117">Il database MySQL ClearDB è un servizio di terze parti e non viene sottoposto a migrazione durante la migrazione di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e88e1-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="e88e1-118">Se non si gestisce la migrazione di hello del database MySQL prima della migrazione delle risorse di Azure, il database ClearDB MySQL potrebbe non essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="e88e1-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="e88e1-119">tooavoid questo, in primo luogo, eseguire manualmente la migrazione del database ClearDB e quindi eseguire la migrazione hello sottoscrizione di Azure per l'app web.</span><span class="sxs-lookup"><span data-stu-id="e88e1-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="e88e1-120">Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="e88e1-121">Come attivare la registrazione di problemi PHP tootroubleshoot PHP?</span><span class="sxs-lookup"><span data-stu-id="e88e1-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="e88e1-122">tooturn registrazione PHP:</span><span class="sxs-lookup"><span data-stu-id="e88e1-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="e88e1-123">Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="e88e1-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="e88e1-124">Nel menu in alto hello selezionare **Debug Console** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="e88e1-125">Seleziona hello **sito** cartella.</span><span class="sxs-lookup"><span data-stu-id="e88e1-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="e88e1-126">Seleziona hello **wwwroot** cartella.</span><span class="sxs-lookup"><span data-stu-id="e88e1-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="e88e1-127">Seleziona hello  **+**  icona e quindi selezionare **nuovo File**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="e88e1-128">Impostare il nome di file hello troppo**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="e88e1-129">Selezionare l'icona matita hello Avanti troppo**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="e88e1-130">Nel file hello, aggiungere questo codice:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="e88e1-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="e88e1-131">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-131">Select **Save**.</span></span>
10. <span data-ttu-id="e88e1-132">Selezionare l'icona matita hello Avanti troppo**wp config.php**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="e88e1-133">Modificare toohello testo hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="e88e1-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="e88e1-134">Nel portale di Azure, nel menu di app web hello, hello riavviare l'app web.</span><span class="sxs-lookup"><span data-stu-id="e88e1-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="e88e1-135">Per altre informazioni, vedere [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Abilitare i log degli errori di WordPress).</span><span class="sxs-lookup"><span data-stu-id="e88e1-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="e88e1-136">Come si registrano gli errori delle applicazioni Python in app ospitate nel servizio app?</span><span class="sxs-lookup"><span data-stu-id="e88e1-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="e88e1-137">errori di applicazione Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="e88e1-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="e88e1-138">Nel portale di Azure nell'app web hello selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="e88e1-139">In hello **impostazioni** , selezionare **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="e88e1-140">In **impostazioni App**, immettere hello seguenti coppia chiave/valore:</span><span class="sxs-lookup"><span data-stu-id="e88e1-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="e88e1-141">Chiave : WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="e88e1-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="e88e1-142">Valore : D:\home\site\wwwroot\logs.txt (immettere il nome file scelto)</span><span class="sxs-lookup"><span data-stu-id="e88e1-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="e88e1-143">Errori nel file logs.txt hello nella cartella wwwroot hello dovrebbe.</span><span class="sxs-lookup"><span data-stu-id="e88e1-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="e88e1-144">Come è possibile modificare la versione hello di hello applicazione Node.js è ospitato nel servizio App?</span><span class="sxs-lookup"><span data-stu-id="e88e1-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="e88e1-145">versione di hello toochange di hello applicazione Node.js, è possibile utilizzare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="e88e1-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="e88e1-146">Nel portale di Azure hello, utilizzare **impostazioni App**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="e88e1-147">Nel portale di Azure hello, andare tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="e88e1-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="e88e1-148">In hello **impostazioni** pannello seleziona **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="e88e1-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="e88e1-149">In **impostazioni App**, è possibile includere WEBSITE_NODE_DEFAULT_VERSION come chiave hello e hello versione di Node. js si vuole usare come valore di hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="e88e1-150">Passare tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="e88e1-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="e88e1-151">toocheck hello versione di Node. js, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e88e1-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="e88e1-152">Modificare il file di iisnode.yml hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="e88e1-153">Versione di Node. js hello modifica nel file iisnode.yml hello imposta solo ambiente di runtime hello che iisnode utilizza.</span><span class="sxs-lookup"><span data-stu-id="e88e1-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="e88e1-154">Il cmd Kudu e altri ancora utilizzare versione di Node. js hello impostato in **impostazioni App** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e88e1-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="e88e1-155">tooset hello iisnode.yml manualmente, creare un file di iisnode.yml nella cartella radice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e88e1-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="e88e1-156">Nel file hello, includere hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e88e1-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="e88e1-157">Impostare file iisnode.yml hello utilizzando package. JSON durante la distribuzione di origine del controllo.</span><span class="sxs-lookup"><span data-stu-id="e88e1-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="e88e1-158">processo di distribuzione di origine Azure controllo Hello prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e88e1-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="e88e1-159">Sposta l'app web di Azure toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="e88e1-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="e88e1-160">Crea uno script di distribuzione predefinito, se questo non è disponibile (deploy, .deployment file) nella cartella radice di hello web app.</span><span class="sxs-lookup"><span data-stu-id="e88e1-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="e88e1-161">Esegue uno script di distribuzione in cui viene creato un file iisnode.yml se hai accennato versione di Node. js hello nel file package. JSON hello > motore di`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="e88e1-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="e88e1-162">file iisnode.yml Hello è hello successiva riga di codice:</span><span class="sxs-lookup"><span data-stu-id="e88e1-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="e88e1-163">Viene visualizzato il messaggio di hello "Errore di connessione al database" nell'applicazione WordPress ospitato nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="e88e1-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="e88e1-164">Come si risolve il problema?</span><span class="sxs-lookup"><span data-stu-id="e88e1-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="e88e1-165">Se viene visualizzato questo errore in app di Azure WordPress, tooenable php_errors.log e debug. log, descritti in dettaglio i passaggi di completamento hello in [log degli errori di WordPress abilitare](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="e88e1-166">Quando sono abilitati i registri di hello, riprodurre l'errore hello e quindi controllare hello registri toosee se si esaurisce le connessioni:</span><span class="sxs-lookup"><span data-stu-id="e88e1-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="e88e1-167">Se viene visualizzato questo errore nei file di debug. log o php_errors.log, l'app ha superato il numero di hello di connessioni.</span><span class="sxs-lookup"><span data-stu-id="e88e1-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="e88e1-168">Se si ospita sul ClearDB, verificare il numero di hello di connessioni disponibili nel [piano di servizio](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="e88e1-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="e88e1-169">Come si esegue il debug di un'app Node.js ospitata nel servizio app?</span><span class="sxs-lookup"><span data-stu-id="e88e1-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="e88e1-170">Passare tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="e88e1-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="e88e1-171">Cartella logs tooyour passare applicazione (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="e88e1-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="e88e1-172">Nel file logging_errors.txt hello, la presenza di contenuto.</span><span class="sxs-lookup"><span data-stu-id="e88e1-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="e88e1-173">Come si installano i moduli Python nativi in un'app Web o in un'app per le API del servizio app?</span><span class="sxs-lookup"><span data-stu-id="e88e1-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="e88e1-174">È possibile che alcuni pacchetti non vengano installati tramite PIP in Azure.</span><span class="sxs-lookup"><span data-stu-id="e88e1-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="e88e1-175">pacchetto di Hello potrebbe non essere disponibile in hello indice del pacchetto Python o un compilatore potrebbe essere necessario (un compilatore non è disponibile nel computer di hello che esegue l'app web hello nel servizio App).</span><span class="sxs-lookup"><span data-stu-id="e88e1-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="e88e1-176">Per informazioni sull'installazione dei moduli nativi nelle app Web e nelle app per le API del servizio app, vedere [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Installare moduli Python nel servizio app).</span><span class="sxs-lookup"><span data-stu-id="e88e1-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="e88e1-177">Come distribuire un tooApp app Django servizio tramite Git e nuova versione di Python hello?</span><span class="sxs-lookup"><span data-stu-id="e88e1-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="e88e1-178">Per informazioni sull'installazione Django, vedere [la distribuzione di un tooApp app Django servizio](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="e88e1-179">Dove si trovano i file di log Tomcat hello?</span><span class="sxs-lookup"><span data-stu-id="e88e1-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="e88e1-180">Per Azure Marketplace e per le distribuzioni personalizzate:</span><span class="sxs-lookup"><span data-stu-id="e88e1-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="e88e1-181">Percorso della cartella: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="e88e1-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="e88e1-182">File rilevanti:</span><span class="sxs-lookup"><span data-stu-id="e88e1-182">Files of interest:</span></span>
    * <span data-ttu-id="e88e1-183">catalina.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-184">host-manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-185">localhost.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-186">manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-187">site_access_log.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="e88e1-188">Per distribuzioni di tipo **Impostazioni dell'app** nel portale:</span><span class="sxs-lookup"><span data-stu-id="e88e1-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="e88e1-189">Percorso della cartella: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="e88e1-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="e88e1-190">File rilevanti:</span><span class="sxs-lookup"><span data-stu-id="e88e1-190">Files of interest:</span></span>
    * <span data-ttu-id="e88e1-191">catalina.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-192">host-manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-193">localhost.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-194">manager.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e88e1-195">site_access_log.*aaaa-mm-gg*.log</span><span class="sxs-lookup"><span data-stu-id="e88e1-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="e88e1-196">Come si risolvono gli errori di connessione del driver JDBC?</span><span class="sxs-lookup"><span data-stu-id="e88e1-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="e88e1-197">Verrà visualizzato hello segue messaggio log Tomcat:</span><span class="sxs-lookup"><span data-stu-id="e88e1-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="e88e1-198">Errore di hello tooresolve:</span><span class="sxs-lookup"><span data-stu-id="e88e1-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="e88e1-199">Rimuovere file sqljdbc*.jar hello dalla cartella app/lib.</span><span class="sxs-lookup"><span data-stu-id="e88e1-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="e88e1-200">Se si utilizza server web Tomcat o Azure Marketplace Tomcat personalizzata hello, copiare questa cartella di lib JAR file toohello Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e88e1-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="e88e1-201">Se si sta abilitando Java da hello portale di Azure (selezionare **Java 1.8** > **server Tomcat**), file jar di copia hello sqljdbc.* in cartella hello app tooyour parallelo.</span><span class="sxs-lookup"><span data-stu-id="e88e1-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="e88e1-202">Aggiungere quindi hello seguenti il file Web. config di classpath impostazione toohello:</span><span class="sxs-lookup"><span data-stu-id="e88e1-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="e88e1-203">Motivo per cui è non vengono visualizzati errori quando si tentano di file di log in tempo reale toocopy?</span><span class="sxs-lookup"><span data-stu-id="e88e1-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="e88e1-204">Se si tenta di file di log in tempo reale toocopy per un'applicazione Java (ad esempio, Tomcat), verrà visualizzato l'errore FTP:</span><span class="sxs-lookup"><span data-stu-id="e88e1-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="e88e1-205">messaggio di errore Hello potrebbe variare, in base al client FTP hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="e88e1-206">Tutte le app Java presentano questo errore di blocco.</span><span class="sxs-lookup"><span data-stu-id="e88e1-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="e88e1-207">Solo Kudu supporta il download del file durante l'esecuzione di app hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="e88e1-208">Arresto applicazione hello consente l'accesso FTP toothese dei file.</span><span class="sxs-lookup"><span data-stu-id="e88e1-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="e88e1-209">Un'altra soluzione alternativa è toowrite un processo Web in esecuzione su una pianificazione e copia le directory dei file tooa diversi.</span><span class="sxs-lookup"><span data-stu-id="e88e1-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="e88e1-210">Per un progetto di esempio, vedere hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) progetto.</span><span class="sxs-lookup"><span data-stu-id="e88e1-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="e88e1-211">Dove trovare i file di log hello per Jetty?</span><span class="sxs-lookup"><span data-stu-id="e88e1-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="e88e1-212">Marketplace e le distribuzioni personalizzate, i file di log hello è nella cartella D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="e88e1-213">Si noti che il percorso di cartella hello dipende dalla versione di hello di Jetty in uso.</span><span class="sxs-lookup"><span data-stu-id="e88e1-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="e88e1-214">Ad esempio, fornire il percorso di hello è qui per Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="e88e1-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="e88e1-215">Cercare jetty_*AAAA_MM_GG*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="e88e1-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="e88e1-216">Per le distribuzioni di impostazione dell'App del portale, i file di log hello è D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="e88e1-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="e88e1-217">Cercare jetty_*AAAA_MM_GG*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="e88e1-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="e88e1-218">È possibile inviare messaggi di posta elettronica dall'app Web di Azure?</span><span class="sxs-lookup"><span data-stu-id="e88e1-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="e88e1-219">Il servizio app non include alcuna funzionalità di posta elettronica predefinita.</span><span class="sxs-lookup"><span data-stu-id="e88e1-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="e88e1-220">Per alternative valide per l'invio di messaggi di posta elettronica dall'app, vedere questa [discussione su Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="e88e1-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="e88e1-221">Perché sito personale WordPress URL di reindirizzamento tooanother?</span><span class="sxs-lookup"><span data-stu-id="e88e1-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="e88e1-222">Se la migrazione di recente tooAzure, WordPress potrebbe reindirizzare toohello URL di dominio precedente.</span><span class="sxs-lookup"><span data-stu-id="e88e1-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="e88e1-223">Ciò è causato da un'impostazione nel database di MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="e88e1-224">WordPress Buddy + non è un'estensione del sito di Azure che è possibile utilizzare l'URL di reindirizzamento hello tooupdate direttamente nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="e88e1-225">Per altre informazioni sull'uso di WordPress Buddy+, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="e88e1-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="e88e1-226">In alternativa, se si preferisce l'URL di reindirizzamento toomanually aggiornamento hello tramite query SQL o PHPMyAdmin, vedere [WordPress: reindirizzamento URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="e88e1-227">Come si modifica la password di accesso di WordPress?</span><span class="sxs-lookup"><span data-stu-id="e88e1-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="e88e1-228">Se si dimentica la propria password di accesso di WordPress, è possibile utilizzare WordPress Buddy + tooupdate è.</span><span class="sxs-lookup"><span data-stu-id="e88e1-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="e88e1-229">tooreset la password, hello installazione sito WordPress Buddy + Azure estensione e le procedure hello completa quindi descritto in [WordPress strumenti e la migrazione di MySQL con WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="e88e1-230">Impossibile accedere tooWordPress.</span><span class="sxs-lookup"><span data-stu-id="e88e1-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="e88e1-231">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="e88e1-231">How do I resolve this?</span></span>

<span data-ttu-id="e88e1-232">Se non è possibile accedere a WordPress dopo l'installazione recente di un plug-in, è possibile che il plug-in sia danneggiato.</span><span class="sxs-lookup"><span data-stu-id="e88e1-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="e88e1-233">WordPress Buddy+ è un'estensione del sito di Azure che consente di disabilitare i plug-in in WordPress.</span><span class="sxs-lookup"><span data-stu-id="e88e1-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="e88e1-234">Per altre informazioni, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="e88e1-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="e88e1-235">Come si esegue la migrazione del database di WordPress?</span><span class="sxs-lookup"><span data-stu-id="e88e1-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="e88e1-236">Sono disponibili più opzioni per la migrazione dei database MySQL hello di sito Web WordPress tooyour connessa:</span><span class="sxs-lookup"><span data-stu-id="e88e1-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="e88e1-237">Sviluppatori: Hello utilizzare [prompt dei comandi o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="e88e1-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="e88e1-238">Non sviluppatori: usare [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="e88e1-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="e88e1-239">Come si migliora la protezione di WordPress?</span><span class="sxs-lookup"><span data-stu-id="e88e1-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="e88e1-240">toolearn sulle procedure consigliate di sicurezza per WordPress, vedere [procedure consigliate per la sicurezza di WordPress in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="e88e1-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="e88e1-241">Si sta tentando di toouse PHPMyAdmin e viene visualizzato il messaggio hello "Accesso negato".</span><span class="sxs-lookup"><span data-stu-id="e88e1-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="e88e1-242">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="e88e1-242">How do I resolve this?</span></span>

<span data-ttu-id="e88e1-243">Questo problema potrebbe verificarsi se funzionalità nell'applicazione di hello MySQL non è ancora in esecuzione in questa istanza di servizio App.</span><span class="sxs-lookup"><span data-stu-id="e88e1-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="e88e1-244">tooresolve hello problema, provare a tooaccess il sito Web.</span><span class="sxs-lookup"><span data-stu-id="e88e1-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="e88e1-245">Verrà avviata processi hello necessario, tra cui il processo di hello MySQL in app.</span><span class="sxs-lookup"><span data-stu-id="e88e1-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="e88e1-246">tooverify che MySQL nell'applicazione è in esecuzione, Process Explorer, assicurarsi che mysqld.exe è elencato in processi hello.</span><span class="sxs-lookup"><span data-stu-id="e88e1-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="e88e1-247">Dopo avere verificato che MySQL in-app è in esecuzione, provare a toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="e88e1-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="e88e1-248">Quando si tenta tooimport o Esporta il database di MySQL in-app con PHPMyadmin, viene visualizzato un errore HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="e88e1-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="e88e1-249">Come posso risolvere il problema?</span><span class="sxs-lookup"><span data-stu-id="e88e1-249">How do I resolve this?</span></span>

<span data-ttu-id="e88e1-250">Se si usa una versione precedente di Chrome, è possibile che si riscontri un bug noto.</span><span class="sxs-lookup"><span data-stu-id="e88e1-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="e88e1-251">problema di hello tooresolve, tooa aggiornamento versione più recente di Chrome.</span><span class="sxs-lookup"><span data-stu-id="e88e1-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="e88e1-252">Provare anche utilizzando un browser diverso, ad esempio Internet Explorer o Edge, in cui hello non si verifica.</span><span class="sxs-lookup"><span data-stu-id="e88e1-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
