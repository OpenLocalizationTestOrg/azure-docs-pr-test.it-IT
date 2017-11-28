---
title: aaaManage un'app web nel servizio App di Azure
description: Tooresources collegamenti per la gestione di un'app web nel servizio App di Azure.
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="59778-103">Scalare un'app Web in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="59778-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="59778-104">In questo argomento contiene collegamenti tooresources per la gestione di un'app web nel [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="59778-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="59778-105">La gestione include tutte le attività hello che consentono di mantenere l'app web in esecuzione senza problemi.</span><span class="sxs-lookup"><span data-stu-id="59778-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="59778-106">Nel corso della durata hello di un'app web, verranno eseguite diverse operazioni di gestione, si sposta da operazione toonormal distribuzione iniziale degli aggiornamenti e manutenzione.</span><span class="sxs-lookup"><span data-stu-id="59778-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="59778-107">Molte attività di gestione di app web possono essere eseguite in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59778-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="59778-108">Prima di distribuire il tooproduction app web</span><span class="sxs-lookup"><span data-stu-id="59778-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="59778-109">Scegliere un livello</span><span class="sxs-lookup"><span data-stu-id="59778-109">Choose a tier</span></span>
<span data-ttu-id="59778-110">Servizio di applicazione Azure è disponibile in cinque livelli: libero, Shared, Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="59778-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="59778-111">Per informazioni sulle funzionalità di hello e sui prezzi per ogni livello, vedere [prezzi](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="59778-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="59778-112">[Piani di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) consentono di raggruppare più App web in hello stesso livello.</span><span class="sxs-lookup"><span data-stu-id="59778-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="59778-113">È sempre possibile [cambiare livello](web-sites-scale.md) dopo aver creato il sito Web.</span><span class="sxs-lookup"><span data-stu-id="59778-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="59778-114">Configurazione</span><span class="sxs-lookup"><span data-stu-id="59778-114">Configuration</span></span>
<span data-ttu-id="59778-115">Hello utilizzare [portale Azure](https://portal.azure.com/) tooset varie opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="59778-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="59778-116">Per informazioni dettagliate, vedere [Configurazione delle app Web in Servizio app di Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="59778-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="59778-117">Di seguito è riportato un rapido elenco di controllo:</span><span class="sxs-lookup"><span data-stu-id="59778-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="59778-118">Selezionare le **versioni runtime** per .NET, PHP, Java o Python, se necessario.</span><span class="sxs-lookup"><span data-stu-id="59778-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="59778-119">Abilitare **WebSocket** se l'app web Usa protocollo WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="59778-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="59778-120">Sono incluse le app che usano [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="59778-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="59778-121">Sul sito vengono eseguiti lavori Web continui?</span><span class="sxs-lookup"><span data-stu-id="59778-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="59778-122">In caso affermativo, abilitare l'opzione **Sempre attivo**.</span><span class="sxs-lookup"><span data-stu-id="59778-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="59778-123">Set hello **documento predefinito**, ad esempio index.html.</span><span class="sxs-lookup"><span data-stu-id="59778-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="59778-124">Nelle impostazioni di configurazione di base toothese aggiunta, è necessario seguente hello tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="59778-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="59778-125">**Secure Socket Layer (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="59778-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="59778-126">toouse SSL con un nome di dominio personalizzato, è necessario ottenere un SSL dei certificati e configurare il toouse app web è.</span><span class="sxs-lookup"><span data-stu-id="59778-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="59778-127">Vedere [Abilitazione di HTTPS per un'app Web nel servizio app di Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="59778-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="59778-128">**Nome di dominio personalizzato.**</span><span class="sxs-lookup"><span data-stu-id="59778-128">**Custom domain name.**</span></span> <span data-ttu-id="59778-129">L'applicazione web dispone automaticamente un sottodominio in azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="59778-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="59778-130">È possibile associare un nome di dominio personalizzato, ad esempio contoso.com. Vedere [Configurazione di un nome di dominio personalizzato nel servizio app di Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="59778-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="59778-131">Configurazione specifica per ciascun linguaggio:</span><span class="sxs-lookup"><span data-stu-id="59778-131">Language-specific configuration:</span></span>

* <span data-ttu-id="59778-132">**PHP**: [Configurazione di PHP nelle app Web di Servizio app di Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="59778-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="59778-133">**Python**: [configurazione Python con Azure applicazione servizio Web App](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="59778-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="59778-134">Durante l'esecuzione di un'applicazione web</span><span class="sxs-lookup"><span data-stu-id="59778-134">While your web app is running</span></span>
<span data-ttu-id="59778-135">Mentre l'app web è in esecuzione, si desidera che sia disponibile e che si adatta il traffico utente toomeet toomake.</span><span class="sxs-lookup"><span data-stu-id="59778-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="59778-136">È necessario anche tootroubleshoot errori.</span><span class="sxs-lookup"><span data-stu-id="59778-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="59778-137">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="59778-137">Monitoring</span></span>
* <span data-ttu-id="59778-138">Tramite il portale di Azure hello, è possibile [aggiungere metriche delle prestazioni](web-sites-monitor.md) , ad esempio l'utilizzo della CPU e numero di richieste client.</span><span class="sxs-lookup"><span data-stu-id="59778-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="59778-139">[Ridimensionare l'app web](web-sites-scale.md) in tootraffic di risposta.</span><span class="sxs-lookup"><span data-stu-id="59778-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="59778-140">A seconda del livello, è possibile scalare il numero di hello di macchine virtuali e/o di dimensioni hello di istanze VM hello.</span><span class="sxs-lookup"><span data-stu-id="59778-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="59778-141">In hello Standard e i livelli Premium, è possibile anche impostare il ridimensionamento automatico in modo da app web si adatta automaticamente, in base a una pianificazione fissa o in tooload di risposta.</span><span class="sxs-lookup"><span data-stu-id="59778-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="59778-142">Backup</span><span class="sxs-lookup"><span data-stu-id="59778-142">Backups</span></span>
* <span data-ttu-id="59778-143">Impostare i [backups automatici](web-sites-backup.md) del sito Web.</span><span class="sxs-lookup"><span data-stu-id="59778-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="59778-144">Ulteriori informazioni sui backup sono disponibili in [questo video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="59778-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="59778-145">Informazioni sulle opzioni di hello per [il ripristino del database](../sql-database/sql-database-business-continuity.md) nel Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="59778-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="59778-146">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="59778-146">Troubleshooting</span></span>
* <span data-ttu-id="59778-147">Se si verificano problemi, è possibile [risoluzione dei problemi in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), utilizzando i log di diagnostica e il debug nel cloud hello attivo.</span><span class="sxs-lookup"><span data-stu-id="59778-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="59778-148">All'esterno di Visual Studio, esistono diversi modi toocollect i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="59778-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="59778-149">Vedere [Abilitazione della registrazione diagnostica per app Web nel servizio app di Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="59778-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="59778-150">Per le applicazioni Node.js, vedere [come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="59778-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="59778-151">Ripristino dei dati</span><span class="sxs-lookup"><span data-stu-id="59778-151">Restoring Data</span></span>
* <span data-ttu-id="59778-152">[Ripristino](web-sites-restore.md) di un sito Web di cui si era eseguito un backup in precedenza.</span><span class="sxs-lookup"><span data-stu-id="59778-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="59778-153">Durante l'aggiornamento del sito Web</span><span class="sxs-lookup"><span data-stu-id="59778-153">When you update your web app</span></span>
<span data-ttu-id="59778-154">Se non sono stati abilitati i backup automatici, è possibile creare un [backup manuale](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="59778-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="59778-155">Valutare l'opportunità di applicare una [distribuzione a fasi](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="59778-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="59778-156">Questa opzione consente di pubblicare aggiornamenti tooa distribuzione che viene eseguito side-by-side di gestione temporanea con la distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="59778-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


