---
title: Scalare un'app Web in Servizio app di Azure
description: Collegamenti a risorse per la gestione di un'applicazione web nel servizio di applicazione Azure.
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="50975-103">Scalare un'app Web in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="50975-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="50975-104">Questo argomento include i collegamenti alle risorse per la gestione di un'app Web nel [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="50975-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="50975-105">Nella gestione sono incluse tutte le attività che consentono al sito Web di funzionare alla perfezione.</span><span class="sxs-lookup"><span data-stu-id="50975-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="50975-106">Nel corso del ciclo di vita di un sito, vengono eseguite diverse attività di gestione, a mano a mano che si passa dalla distribuzione iniziale alle normali attività operative, di manutenzione e di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="50975-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="50975-107">Nel portale di Azure è possibile eseguire diverse attività di gestione dei siti Web.</span><span class="sxs-lookup"><span data-stu-id="50975-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="50975-108">Prima della distribuzione del sito alla produzione</span><span class="sxs-lookup"><span data-stu-id="50975-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="50975-109">Scegliere un livello</span><span class="sxs-lookup"><span data-stu-id="50975-109">Choose a tier</span></span>
<span data-ttu-id="50975-110">Servizio di applicazione Azure è disponibile in cinque livelli: libero, Shared, Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="50975-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="50975-111">Per ulteriori informazioni sulle funzionalità e i prezzi di ciascun livello, vedere [Dettagli prezzi](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="50975-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="50975-112">[Piani di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) consentono di raggruppare più applicazioni web con lo stesso livello.</span><span class="sxs-lookup"><span data-stu-id="50975-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="50975-113">È sempre possibile [cambiare livello](web-sites-scale.md) dopo aver creato il sito Web.</span><span class="sxs-lookup"><span data-stu-id="50975-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="50975-114">Configurazione</span><span class="sxs-lookup"><span data-stu-id="50975-114">Configuration</span></span>
<span data-ttu-id="50975-115">Utilizzare il [portale di Azure](https://portal.azure.com/) per impostare varie opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="50975-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="50975-116">Per informazioni dettagliate, vedere [Configurazione delle app Web in Servizio app di Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="50975-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="50975-117">Di seguito è riportato un rapido elenco di controllo:</span><span class="sxs-lookup"><span data-stu-id="50975-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="50975-118">Selezionare le **versioni runtime** per .NET, PHP, Java o Python, se necessario.</span><span class="sxs-lookup"><span data-stu-id="50975-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="50975-119">Abilitare **WebSocket** se il sito Web utilizza il protocollo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="50975-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="50975-120">Sono incluse le app che usano [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="50975-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="50975-121">Sul sito vengono eseguiti lavori Web continui?</span><span class="sxs-lookup"><span data-stu-id="50975-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="50975-122">In caso affermativo, abilitare l'opzione **Sempre attivo**.</span><span class="sxs-lookup"><span data-stu-id="50975-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="50975-123">Impostare il **documento predefinito**, ad esempio index.html.</span><span class="sxs-lookup"><span data-stu-id="50975-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="50975-124">Oltre a tali impostazioni di configurazione di base, può essere opportuno configurare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="50975-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="50975-125">**Secure Socket Layer (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="50975-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="50975-126">Per utilizzare SSL con un nome di dominio personalizzato, è necessario ottenere un certificato SSL e configurare il sito Web in modo tale che lo utilizzi.</span><span class="sxs-lookup"><span data-stu-id="50975-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="50975-127">Vedere [Abilitazione di HTTPS per un'app Web nel servizio app di Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="50975-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="50975-128">**Nome di dominio personalizzato.**</span><span class="sxs-lookup"><span data-stu-id="50975-128">**Custom domain name.**</span></span> <span data-ttu-id="50975-129">L'applicazione web dispone automaticamente un sottodominio in azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="50975-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="50975-130">È possibile associare un nome di dominio personalizzato, ad esempio contoso.com.</span><span class="sxs-lookup"><span data-stu-id="50975-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="50975-131">Vedere [Configurazione di un nome di dominio personalizzato nel servizio app di Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="50975-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="50975-132">Configurazione specifica per ciascun linguaggio:</span><span class="sxs-lookup"><span data-stu-id="50975-132">Language-specific configuration:</span></span>

* <span data-ttu-id="50975-133">**PHP**: [Configurazione di PHP nelle app Web di Servizio app di Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="50975-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="50975-134">**Python**: [configurazione Python con Azure applicazione servizio Web App](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="50975-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="50975-135">Durante l'esecuzione di un'applicazione web</span><span class="sxs-lookup"><span data-stu-id="50975-135">While your web app is running</span></span>
<span data-ttu-id="50975-136">Quando il sito è in esecuzione, accertarsi che sia disponibile e che assicuri la scalabilità in base al traffico degli utenti.</span><span class="sxs-lookup"><span data-stu-id="50975-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="50975-137">Potrebbe essere necessario risolvere eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="50975-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="50975-138">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="50975-138">Monitoring</span></span>
* <span data-ttu-id="50975-139">Attraverso il portale di Azure, è possibile [aggiungere metriche delle prestazioni](web-sites-monitor.md) quali utilizzo della CPU e numero di richieste dei client.</span><span class="sxs-lookup"><span data-stu-id="50975-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="50975-140">[Applicare la scalabilità al proprio sito Web](web-sites-scale.md) per rispondere al traffico.</span><span class="sxs-lookup"><span data-stu-id="50975-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="50975-141">A seconda del livello, è possibile applicare la scalabilità al numero di VM e/o le dimensioni delle istanze delle VM.</span><span class="sxs-lookup"><span data-stu-id="50975-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="50975-142">Nel piano Standard, è inoltre possibile impostare la scalabilità automatica da applicare automaticamente ai siti secondo una pianificazione fissa o in risposta al carico.</span><span class="sxs-lookup"><span data-stu-id="50975-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="50975-143">Backup</span><span class="sxs-lookup"><span data-stu-id="50975-143">Backups</span></span>
* <span data-ttu-id="50975-144">Impostare i [backups automatici](web-sites-backup.md) del sito Web.</span><span class="sxs-lookup"><span data-stu-id="50975-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="50975-145">Ulteriori informazioni sui backup sono disponibili in [questo video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="50975-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="50975-146">Ulteriori informazioni sulle opzioni per il [ripristino database](../sql-database/sql-database-business-continuity.md) nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="50975-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="50975-147">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="50975-147">Troubleshooting</span></span>
* <span data-ttu-id="50975-148">In caso di problemi, procedere con la [risoluzione dei problemi in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), utilizzando log di diagnostica e debug attivo nel cloud.</span><span class="sxs-lookup"><span data-stu-id="50975-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="50975-149">Oltre a Visual Studio, esistono diversi modi per ottenere i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="50975-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="50975-150">Vedere [Abilitazione della registrazione diagnostica per app Web nel servizio app di Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="50975-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="50975-151">Per le applicazioni Node.js, vedere [Come eseguire il debug di un'applicazione Node.js in Siti Web di Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="50975-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="50975-152">Ripristino dei dati</span><span class="sxs-lookup"><span data-stu-id="50975-152">Restoring Data</span></span>
* <span data-ttu-id="50975-153">[Ripristino](web-sites-restore.md) di un sito Web di cui si era eseguito un backup in precedenza.</span><span class="sxs-lookup"><span data-stu-id="50975-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="50975-154">Durante l'aggiornamento del sito Web</span><span class="sxs-lookup"><span data-stu-id="50975-154">When you update your web app</span></span>
<span data-ttu-id="50975-155">Se non sono stati abilitati i backup automatici, è possibile creare un [backup manuale](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="50975-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="50975-156">Valutare l'opportunità di applicare una [distribuzione a fasi](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="50975-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="50975-157">Questa opzione consente di pubblicare aggiornamenti a una distribuzione a fasi che viene eseguita in parallelo alla distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="50975-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


