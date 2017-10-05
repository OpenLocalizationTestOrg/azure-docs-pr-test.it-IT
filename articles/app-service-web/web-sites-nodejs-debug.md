---
title: Come eseguire il debug di un'app Web Node.js nel servizio app di Azure
description: Informazioni su come eseguire il debug di un'app Web Node.js nel servizio app di Azure.
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="45abe-103">Come eseguire il debug di un'app Web Node.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="45abe-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="45abe-104">Azure offre diagnostica integrata per agevolare il debug di applicazioni Node.js ospitate in App Web del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) .</span><span class="sxs-lookup"><span data-stu-id="45abe-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="45abe-105">In questo articolo verrà illustrato come abilitare la registrazione di stdout e stderr, visualizzare informazioni sugli errori nel browser, nonché come scaricare e visualizzare i file di log.</span><span class="sxs-lookup"><span data-stu-id="45abe-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="45abe-106">La diagnostica per le applicazioni Node.js ospitate in Azure viene fornita da [IISNode].</span><span class="sxs-lookup"><span data-stu-id="45abe-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="45abe-107">In questo articolo vengono illustrate le impostazioni più comuni per la raccolta delle informazioni di diagnostica; non sono invece incluse informazioni dettagliate sull'utilizzo di IISNode.</span><span class="sxs-lookup"><span data-stu-id="45abe-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="45abe-108">Per ulteriori informazioni sull'utilizzo di IISNode, vedere il [file Readme di IISNode] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="45abe-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="45abe-109">Abilitazione della registrazione</span><span class="sxs-lookup"><span data-stu-id="45abe-109">Enable logging</span></span>
<span data-ttu-id="45abe-110">Per impostazione predefinita, un'app web servizio App acquisisce solo le informazioni di diagnostica relative distribuzioni, ad esempio quando si distribuisce un'app web utilizzando Git.</span><span class="sxs-lookup"><span data-stu-id="45abe-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="45abe-111">Tali informazioni sono utili in caso di problemi durante la distribuzione, ad esempio quando non si riesce a installare un modulo cui viene fatto riferimento in **package.json**oppure se si usa uno script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="45abe-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="45abe-112">Per abilitare la registrazione di flussi stdout e stderr, è necessario creare un file **IISNode.yml** nella radice dell'applicazione Node.js e aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="45abe-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="45abe-113">In tal modo la registrazione di stderr e stdout dall'applicazione Node.js verrà abilitata.</span><span class="sxs-lookup"><span data-stu-id="45abe-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="45abe-114">È inoltre possibile utilizzare il file **IISNode.yml** per controllare se in caso di errore al browser vengono restituiti errori descrittivi o dello sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="45abe-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="45abe-115">Per abilitare gli errori dello sviluppatore, aggiungere la riga seguente al file **IISNode.yml** :</span><span class="sxs-lookup"><span data-stu-id="45abe-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="45abe-116">Dopo aver abilitato questa opzione, IISNode restituirà gli ultimi 64 KB di informazioni inviate a stderr anziché un errore descrittivo, quale "si è verificato un errore interno del server".</span><span class="sxs-lookup"><span data-stu-id="45abe-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="45abe-117">devErrorsEnabled è utile per diagnosticare problemi che si verificano durante lo sviluppo, tuttavia se viene abilitato in un ambiente di produzione è possibile che gli eventuali errori di sviluppo vengano inviati agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="45abe-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="45abe-118">Se il **IISNode.yml** non esisteva già nell'applicazione, sarà necessario riavviare il sito Web dopo aver pubblicato l'applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="45abe-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="45abe-119">Se si intende solo modificare le impostazioni in un file **IISNode.yml** già pubblicato, il riavvio non è richiesto.</span><span class="sxs-lookup"><span data-stu-id="45abe-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="45abe-120">Se il sito Web è stato creato con gli strumenti da riga di comando di Azure o i cmdlet di Azure PowerShell, verrà creato automaticamente un file **IISNode.yml** predefinito.</span><span class="sxs-lookup"><span data-stu-id="45abe-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="45abe-121">Per riavviare l'app Web, selezionarla nel [portale di Azure](https://portal.azure.com)e quindi fare clic sul pulsante **RIAVVIA** :</span><span class="sxs-lookup"><span data-stu-id="45abe-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Pulsante Restart][restart-button]

<span data-ttu-id="45abe-123">Se nell'ambiente di sviluppo sono installati gli strumenti da riga di comando di Azure, è possibile utilizzare il comando seguente per riavviare il sito Web:</span><span class="sxs-lookup"><span data-stu-id="45abe-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="45abe-124">Anche se loggingEnabled e devErrorsEnabled sono le opzioni di configurazione più utilizzate di IISNode.yml per acquisire informazioni diagnostiche, è possibile utilizzare IISNode.yml per configurare numerose opzioni per l'ambiente host.</span><span class="sxs-lookup"><span data-stu-id="45abe-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="45abe-125">Per un elenco completo delle opzioni di configurazione, vedere il file [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).</span><span class="sxs-lookup"><span data-stu-id="45abe-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="45abe-126">Accesso ai log</span><span class="sxs-lookup"><span data-stu-id="45abe-126">Accessing logs</span></span>
<span data-ttu-id="45abe-127">È possibile accedere ai log di diagnostica in tre modi, ovvero utilizzando il protocollo FTP (File Transfer Protocol), scaricando un archivio ZIP oppure sotto forma di flusso aggiornato in diretta del log (noto anche come tail).</span><span class="sxs-lookup"><span data-stu-id="45abe-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="45abe-128">Per il download dell'archivio ZIP dei file di log o per la visualizzazione del flusso in diretta sono necessari gli strumenti da riga di comando di Azure,</span><span class="sxs-lookup"><span data-stu-id="45abe-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="45abe-129">che è possibile installare tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="45abe-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="45abe-130">Dopo l'installazione, è possibile accedere agli strumenti tramite il comando 'azure'.</span><span class="sxs-lookup"><span data-stu-id="45abe-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="45abe-131">È prima necessario configurare gli strumenti da riga di comando per l'uso della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45abe-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="45abe-132">Per informazioni su come eseguire questa attività, vedere la sezione **Come scaricare e importare impostazioni di pubblicazione** dell'articolo [Come utilizzare gli strumenti da riga di comando](../xplat-cli-connect.md) .</span><span class="sxs-lookup"><span data-stu-id="45abe-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="45abe-133">FTP</span><span class="sxs-lookup"><span data-stu-id="45abe-133">FTP</span></span>
<span data-ttu-id="45abe-134">Per accedere alle informazioni diagnostiche tramite FTP, visitare il [portale di Azure](https://portal.azure.com), selezionare l’app Web e scegliere **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="45abe-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="45abe-135">Nella sezione relativa ai **collegamenti rapidi** fare clic sui collegamenti **REGISTRI DI DIAGNOSTICA FTP** e **REGISTRI DI DIAGNOSTICA FTPS** per accedere ai log tramite il protocollo FTP.</span><span class="sxs-lookup"><span data-stu-id="45abe-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="45abe-136">Se in precedenza non sono stati configurati nome utente e password per FTP o per la distribuzione, è possibile eseguire questa operazione nella pagina di gestione **Avvio rapido** selezionando **Imposta credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="45abe-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="45abe-137">L'URL FTP restituito nel dashboard si riferisce alla directory **LogFiles** , che conterrà le seguenti sottodirectory:</span><span class="sxs-lookup"><span data-stu-id="45abe-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="45abe-138">[Metodo di distribuzione](web-sites-deploy.md) : se si utilizza un metodo di distribuzione, ad esempio Git, verrà creata una directory con lo stesso nome, che conterrà le informazioni correlate alle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="45abe-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="45abe-139">nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="45abe-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="45abe-140">Archivio ZIP</span><span class="sxs-lookup"><span data-stu-id="45abe-140">Zip archive</span></span>
<span data-ttu-id="45abe-141">Per scaricare un archivio ZIP dei log di diagnostica, utilizzare il seguente comando degli strumenti da riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="45abe-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="45abe-142">Nella directory corrente verrà scaricato un file **diagnostics.zip** .</span><span class="sxs-lookup"><span data-stu-id="45abe-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="45abe-143">Questo archivio contiene la seguente struttura di directory:</span><span class="sxs-lookup"><span data-stu-id="45abe-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="45abe-144">deployments: log delle informazioni sulle distribuzioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="45abe-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="45abe-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="45abe-145">LogFiles</span></span>
  
  * <span data-ttu-id="45abe-146">[Metodo di distribuzione](web-sites-deploy.md) : se si utilizza un metodo di distribuzione, ad esempio Git, verrà creata una directory con lo stesso nome, che conterrà le informazioni correlate alle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="45abe-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="45abe-147">nodejs: contiene le informazioni di stdout e stderr acquisite da tutte le istanze dell'applicazione, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="45abe-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="45abe-148">Flusso in diretta (tail)</span><span class="sxs-lookup"><span data-stu-id="45abe-148">Live stream (tail)</span></span>
<span data-ttu-id="45abe-149">Per visualizzare un flusso in diretta delle informazioni dei log di diagnostica, usare il seguente comando degli strumenti da riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="45abe-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="45abe-150">Verrà restituito un flusso di eventi log che vengono aggiornati non appena si verificano nel server.</span><span class="sxs-lookup"><span data-stu-id="45abe-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="45abe-151">Questo flusso restituirà le informazioni relative alla distribuzione, oltre alle informazioni di stdout e stderr, quando loggingEnabled è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="45abe-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="45abe-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45abe-152">Next Steps</span></span>
<span data-ttu-id="45abe-153">In questo articolo è stato illustrato come abilitare e accedere alle informazioni di diagnostica in Azure.</span><span class="sxs-lookup"><span data-stu-id="45abe-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="45abe-154">Queste informazioni sono utili per comprendere problemi che si verificano nell'applicazione, tuttavia è possibile che indichino un problema relativo a un modulo in uso oppure che segnalino che la versione di Node.js utilizzata in Siti Web di Azure è diversa da quella dell'ambiente di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="45abe-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="45abe-155">Per informazioni sull'uso di moduli in Azure, vedere [Uso di moduli Node.js con applicazioni Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="45abe-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="45abe-156">Per informazioni sulla specifica di una versione di Node.js per l'applicazione, vedere [Specifica di una versione di Node.js in un'applicazione Azure].</span><span class="sxs-lookup"><span data-stu-id="45abe-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="45abe-157">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="45abe-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="45abe-158">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="45abe-158">What's changed</span></span>
* <span data-ttu-id="45abe-159">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="45abe-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="45abe-160">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="45abe-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="45abe-161">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="45abe-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="45abe-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="45abe-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="45abe-163">[file Readme di IISNode]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="45abe-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="45abe-164">[Specifica di una versione di Node.js in un'applicazione Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="45abe-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

