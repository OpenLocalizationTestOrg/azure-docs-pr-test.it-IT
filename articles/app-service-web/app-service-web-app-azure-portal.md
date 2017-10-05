---
title: Informazioni di riferimento per l'esplorazione del portale di Azure
description: Apprendere le diverse esperienze utente per il servizio per app Web tra il portale di gestione e il portale di Azure
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="a7fa9-103">Informazioni di riferimento per l'esplorazione del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7fa9-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="a7fa9-104">Siti Web di Azure è ora denominato [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a7fa9-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="a7fa9-105">Stiamo aggiornando tutta la documentazione per evidenziare questo cambiamento di nome e per fornire istruzioni per il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="a7fa9-106">Fino al completamento di tale processo, è possibile usare questo documento come guida per lavorare con le app Web nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="a7fa9-107">Il futuro del portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="a7fa9-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="a7fa9-108">Sebbene le modifiche di personalizzazione siano visibili anche nel portale di Azure classico, è in corso la sostituzione di quest'ultimo con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="a7fa9-109">Il portale classico verrà eventualmente eliminato e tutte le nuove attività correlate allo sviluppo verranno spostate e proseguiranno nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="a7fa9-110">Tutte le nuove funzionalità per app Web in arrivo verranno ospitate nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="a7fa9-111">Iniziare subito a usare il portale di Azure per sfruttare i vantaggi offerti dalle ultime e migliori app Web.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="a7fa9-112">Differenze del layout tra il portale di Azure classico e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a7fa9-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="a7fa9-113">Nel portale classico, tutti i servizi di Azure sono elencati nella parte sinistra.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="a7fa9-114">La navigazione nel portale classico segue una struttura ad albero, in cui si inizia dal servizio e si naviga all'interno di ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="a7fa9-115">Questa struttura funziona bene quando si gestiscono componenti indipendenti.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="a7fa9-116">Le applicazioni create in Azure, tuttavia, sono una raccolta di servizi interconnessi e questa struttura ad albero non risulta ideale per lavorare con raccolte di servizi.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="a7fa9-117">Il portale di Azure semplifica la creazione di applicazioni end-to-end con componenti provenienti da più servizi.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="a7fa9-118">Il portale è organizzato in *esplorazioni*.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="a7fa9-119">Un'*esplorazione* è una serie di *pannelli*, ovvero contenitori per i diversi componenti.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="a7fa9-120">La configurazione della scalabilità automatica per un'app Web, ad esempio, è un'*esplorazione* che ospita diversi pannelli, come illustrato nell'esempio seguente: il pannello del **sito Web** (con il titolo non ancora aggiornato alla nuova terminologia), il pannello **Impostazioni** e il pannello **Aumenta istanze**.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="a7fa9-121">In questo esempio la scalabilità automatica viene configurata secondo l'uso della CPU ed è pertanto presente anche un pannello **Percentuale CPU** .</span><span class="sxs-lookup"><span data-stu-id="a7fa9-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="a7fa9-122">I componenti all'interno dei *pannelli* sono denominati *parti* e sono simili ai riquadri.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="a7fa9-123">Esempio di navigazione: creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="a7fa9-123">Navigation example: create a web app</span></span>
<span data-ttu-id="a7fa9-124">La creazione di app Web resta un'operazione semplicissima.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="a7fa9-125">La figura seguente illustra il portale classico e il portale affiancati e dimostra che ben poco è cambiato quanto al numero di passaggi necessari per creare un'app Web e renderla operativa.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="a7fa9-126">Nel portale è possibile scegliere tra i tipi di app Web più comuni, comprese applicazioni note da raccolte come WordPress.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="a7fa9-127">Per un elenco completo delle applicazioni disponibili, visitare [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="a7fa9-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="a7fa9-128">Per creare un'app Web si specificano l'URL, il piano di servizio app e la posizione nel portale esattamente come avviene nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="a7fa9-129">Nel portale è inoltre possibile definire altre impostazioni comuni.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="a7fa9-130">Ad esempio i [gruppi di risorse](../azure-resource-manager/resource-group-overview.md) semplificano la visualizzazione e la gestione delle risorse di Azure correlate.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="a7fa9-131">Esempio di navigazione: impostazioni e funzionalità</span><span class="sxs-lookup"><span data-stu-id="a7fa9-131">Navigation example: settings and features</span></span>
<span data-ttu-id="a7fa9-132">Tutte le impostazioni e funzionalità sono ora raggruppate logicamente in un unico riquadro, da cui è possibile avviare una navigazione.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="a7fa9-133">Ad esempio, è possibile creare domini personalizzati facendo clic su **Domini personalizzati ed SSL** nel pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="a7fa9-134">Per impostare una notifica di monitoraggio, fare clic su **Richieste ed errori** e quindi su **Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="a7fa9-135">Per abilitare la diagnostica, fare clic su **Log di diagnostica** nel pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="a7fa9-136">Per configurare le impostazioni dell'applicazione, fare clic su **Impostazioni dell'applicazione** nel pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="a7fa9-137">Oltre al nome del marchio, alcuni altri elementi nel portale sono stati rinominati o raggruppati in modo diverso per semplificarne l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="a7fa9-138">Ad esempio, quella riportata di seguito è una schermata della pagina corrispondente a quella delle impostazioni dell'app (**Configura**) nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="a7fa9-139">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="a7fa9-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="a7fa9-140">[Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="a7fa9-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="a7fa9-141">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a7fa9-142">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="a7fa9-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a7fa9-143">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="a7fa9-143">What's changed</span></span>
* <span data-ttu-id="a7fa9-144">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a7fa9-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

