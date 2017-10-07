---
title: aaaHow toodebug un'app web Node.js in Azure App Service
description: Informazioni su come toodebug un Node.js web app in Azure App Service.
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="fd62c-103">Come toodebug un Node.js web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fd62c-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="fd62c-104">Azure offre tooassist di diagnostica con il debug di applicazioni Node.js ospitate in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) App Web.</span><span class="sxs-lookup"><span data-stu-id="fd62c-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="fd62c-105">In questo articolo si apprenderà come registrazione tooenable di stdout e stderr, informazioni di errore visualizzato nel browser hello e la modalità di toodownload e visualizzare i file di log.</span><span class="sxs-lookup"><span data-stu-id="fd62c-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="fd62c-106">La diagnostica per le applicazioni Node.js ospitate in Azure viene fornita da [IISNode].</span><span class="sxs-lookup"><span data-stu-id="fd62c-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="fd62c-107">Anche se in questo articolo illustra le impostazioni più comuni di hello per raccogliere le informazioni di diagnostica, non fornisce un riferimento completo per l'utilizzo di IISNode.</span><span class="sxs-lookup"><span data-stu-id="fd62c-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="fd62c-108">Per ulteriori informazioni sull'uso di IISNode, vedere hello [IISNode Readme] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd62c-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="fd62c-109">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="fd62c-109">Enable logging</span></span>
<span data-ttu-id="fd62c-110">Per impostazione predefinita, un'app web servizio App acquisisce solo le informazioni di diagnostica relative distribuzioni, ad esempio quando si distribuisce un'app web utilizzando Git.</span><span class="sxs-lookup"><span data-stu-id="fd62c-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="fd62c-111">Tali informazioni sono utili in caso di problemi durante la distribuzione, ad esempio quando non si riesce a installare un modulo cui viene fatto riferimento in **package.json**oppure se si usa uno script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fd62c-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="fd62c-112">hello tooenable registrazione di flussi di stdout e stderr, è necessario creare un **IISNode.yml** file alla radice dell'applicazione Node.js hello e aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd62c-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="fd62c-113">In questo modo la registrazione di hello di stderr e stdout dall'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="fd62c-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="fd62c-114">Hello **IISNode.yml** file può anche essere toocontrol utilizzati se descrittivi errori o per sviluppatori restituiti toohello browser quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="fd62c-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="fd62c-115">individuare errori degli sviluppatori tooenable, aggiungere hello seguente riga toohello **IISNode.yml** file:</span><span class="sxs-lookup"><span data-stu-id="fd62c-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="fd62c-116">Dopo aver abilitata questa opzione, IISNode restituirà hello ultimo 64 KB di informazioni inviate toostderr anziché un errore descrittivo, ad esempio "si è verificato un errore interno del server".</span><span class="sxs-lookup"><span data-stu-id="fd62c-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="fd62c-117">Anche devErrorsEnabled è utile quando si diagnosticano problemi durante lo sviluppo, abilitarlo in un ambiente di produzione può comportare errori di sviluppo inviati agli utenti di tooend.</span><span class="sxs-lookup"><span data-stu-id="fd62c-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="fd62c-118">Se hello **IISNode.yml** file non esiste già all'interno dell'applicazione, è necessario riavviare l'app web dopo la pubblicazione di un'applicazione hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="fd62c-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="fd62c-119">Se si intende solo modificare le impostazioni in un file **IISNode.yml** già pubblicato, il riavvio non è richiesto.</span><span class="sxs-lookup"><span data-stu-id="fd62c-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="fd62c-120">Se l'app web è stato creato utilizzando gli strumenti da riga di comando di hello Azure o i cmdlet PowerShell di Azure, valore predefinito è **IISNode.yml** file viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd62c-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="fd62c-121">toorestart hello web app, app web selezionare hello in hello [portale Azure](https://portal.azure.com), quindi fare clic su **riavviare** pulsante:</span><span class="sxs-lookup"><span data-stu-id="fd62c-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Pulsante Restart][restart-button]

<span data-ttu-id="fd62c-123">Se gli strumenti da riga di comando di hello Azure sono installati nell'ambiente di sviluppo, è possibile utilizzare hello comando toorestart hello web app seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd62c-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="fd62c-124">Mentre loggingEnabled e devErrorsEnabled sono le opzioni di configurazione IISNode.yml hello più comunemente usato per l'acquisizione di informazioni di diagnostica, IISNode.yml può essere utilizzato tooconfigure un'ampia gamma di opzioni per l'ambiente di hosting.</span><span class="sxs-lookup"><span data-stu-id="fd62c-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="fd62c-125">Per un elenco completo delle opzioni di configurazione di hello, vedere hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span><span class="sxs-lookup"><span data-stu-id="fd62c-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="fd62c-126">Accesso ai log</span><span class="sxs-lookup"><span data-stu-id="fd62c-126">Accessing logs</span></span>
<span data-ttu-id="fd62c-127">I log di diagnostica possono avvenire in tre modi; Utilizzando hello protocollo FTP (File Transfer), il download di un archivio Zip, o come attivo aggiornato flusso del log hello (noto anche come finale).</span><span class="sxs-lookup"><span data-stu-id="fd62c-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="fd62c-128">Download di archivio di Zip hello hello dei file di log o la visualizzazione flusso live hello richiedono strumenti da riga di comando di hello Azure.</span><span class="sxs-lookup"><span data-stu-id="fd62c-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="fd62c-129">È possibile installarli utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fd62c-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="fd62c-130">Una volta installato, è possano accedere agli strumenti di hello comando hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="fd62c-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="fd62c-131">Hello strumenti da riga di comando deve essere innanzitutto configurato toouse la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd62c-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="fd62c-132">Per informazioni su come tooaccomplish questa attività, vedere hello **come di toodownload e importare le impostazioni di pubblicazione** sezione di hello [come tooUse hello strumenti da riga di comando di Azure](../xplat-cli-connect.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fd62c-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="fd62c-133">FTP</span><span class="sxs-lookup"><span data-stu-id="fd62c-133">FTP</span></span>
<span data-ttu-id="fd62c-134">informazioni di diagnostica hello tooaccess tramite FTP, visitare hello [portale Azure](https://portal.azure.com), selezionare l'app web, quindi hello **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="fd62c-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="fd62c-135">In hello **collegamenti rapidi** sezione hello **registri di diagnostica FTP** e **registri di diagnostica FTPS** collegamenti forniscono accesso toohello log utilizzando il protocollo FTP hello.</span><span class="sxs-lookup"><span data-stu-id="fd62c-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="fd62c-136">Se non è stato precedentemente configurato nome utente e password per il FTP o distribuzione, è possibile farlo da hello **delle Guide rapide** pagina di gestione selezionando **impostare le credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="fd62c-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="fd62c-137">Hello FTP URL restituito nel dashboard di hello è per hello **LogFiles** directory, che conterrà hello seguente sottodirectory:</span><span class="sxs-lookup"><span data-stu-id="fd62c-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="fd62c-138">[Metodo di distribuzione](web-sites-deploy.md) -se si utilizza un metodo di distribuzione, ad esempio Git, una directory di hello stesso nome, verrà creato e contiene le informazioni correlate toodeployments.</span><span class="sxs-lookup"><span data-stu-id="fd62c-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="fd62c-139">nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="fd62c-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="fd62c-140">Archivio ZIP</span><span class="sxs-lookup"><span data-stu-id="fd62c-140">Zip archive</span></span>
<span data-ttu-id="fd62c-141">un archivio Zip dei log di diagnostica hello, utilizzare hello comando seguente da strumenti da riga di comando di Azure hello toodownload:</span><span class="sxs-lookup"><span data-stu-id="fd62c-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="fd62c-142">Questo verrà scaricato un **diagnostics.zip** nella directory corrente hello.</span><span class="sxs-lookup"><span data-stu-id="fd62c-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="fd62c-143">Questo archivio contiene hello seguente struttura di directory:</span><span class="sxs-lookup"><span data-stu-id="fd62c-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="fd62c-144">deployments: log delle informazioni sulle distribuzioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd62c-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="fd62c-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="fd62c-145">LogFiles</span></span>
  
  * <span data-ttu-id="fd62c-146">[Metodo di distribuzione](web-sites-deploy.md) -se si utilizza un metodo di distribuzione, ad esempio Git, una directory di hello stesso nome, verrà creato e contiene le informazioni correlate toodeployments.</span><span class="sxs-lookup"><span data-stu-id="fd62c-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="fd62c-147">nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="fd62c-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="fd62c-148">Flusso in diretta (tail)</span><span class="sxs-lookup"><span data-stu-id="fd62c-148">Live stream (tail)</span></span>
<span data-ttu-id="fd62c-149">tooview un flusso di informazioni di log di diagnostica, utilizzare hello comando seguente da strumenti da riga di comando di Azure hello in tempo reale:</span><span class="sxs-lookup"><span data-stu-id="fd62c-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="fd62c-150">Verrà restituito un flusso di eventi di log che vengono aggiornate quando si verificano nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="fd62c-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="fd62c-151">Questo flusso restituirà le informazioni relative alla distribuzione, oltre alle informazioni di stdout e stderr, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="fd62c-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="fd62c-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd62c-152">Next Steps</span></span>
<span data-ttu-id="fd62c-153">In questo articolo si è appreso come tooenable e alle informazioni di diagnostica per Azure.</span><span class="sxs-lookup"><span data-stu-id="fd62c-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="fd62c-154">Mentre questo è utile per informazioni sui problemi con l'applicazione, può puntare tooa problema con un modulo in uso o la versione di hello di Node.js utilizzato dal servizio App dell'App Web è diverso da quello hello quello utilizzato nella distribuzione ambiente.</span><span class="sxs-lookup"><span data-stu-id="fd62c-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="fd62c-155">Per informazioni sull'uso di moduli in Azure, vedere [Uso di moduli Node.js con applicazioni Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fd62c-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="fd62c-156">Per informazioni sulla specifica di una versione di Node.js per l'applicazione, vedere [Specifica di una versione di Node.js in un'applicazione Azure].</span><span class="sxs-lookup"><span data-stu-id="fd62c-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="fd62c-157">Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="fd62c-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fd62c-158">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="fd62c-158">What's changed</span></span>
* <span data-ttu-id="fd62c-159">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fd62c-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="fd62c-160">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="fd62c-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fd62c-161">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="fd62c-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Specifica di una versione di Node.js in un'applicazione Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

