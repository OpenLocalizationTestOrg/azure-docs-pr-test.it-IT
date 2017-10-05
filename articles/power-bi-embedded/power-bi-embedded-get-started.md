---
title: Introduzione a Microsoft Power BI Embedded
description: Power BI Embedded, aggiungere report di Power BI interattivi nell'applicazione di Business Intelligence
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="2112b-103">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2112b-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="2112b-104">**Power BI Embedded** è un servizio di Azure che consente agli sviluppatori di applicazioni di aggiungere report interattivi di Power BI alle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2112b-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="2112b-105">**Power BI Embedded** interagisce con le applicazioni esistenti senza che sia necessario riprogettarle o modificare la modalità di accesso da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="2112b-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="2112b-106">Il provisioning delle risorse di **Microsoft Power BI Embedded** viene effettuato tramite le [API di Azure Resource Manager](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="2112b-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="2112b-107">In questo caso, la risorsa di cui si effettua il provisioning è una **Raccolta di aree di lavoro di Power BI**.</span><span class="sxs-lookup"><span data-stu-id="2112b-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="2112b-108">Creare una raccolta di aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="2112b-108">Create a workspace collection</span></span>

<span data-ttu-id="2112b-109">Una **Raccolta di aree di lavoro** è la risorsa di primo livello di Azure e un contenitore per il contenuto che verrà incorporato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2112b-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="2112b-110">Una **Raccolta di aree di lavoro** può essere creata in due modi:</span><span class="sxs-lookup"><span data-stu-id="2112b-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="2112b-111">Uso manuale del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2112b-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="2112b-112">Uso delle API di Azure Resource Manager a livello di codice</span><span class="sxs-lookup"><span data-stu-id="2112b-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="2112b-113">Di seguito è descritta la procedura per compilare una **Raccolta di aree di lavoro** tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2112b-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="2112b-114">Aprire il **portale di Azure**ed eseguire l'accesso: [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2112b-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="2112b-115">Fare clic su **+ Nuovo** nel pannello in alto.</span><span class="sxs-lookup"><span data-stu-id="2112b-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="2112b-116">In **Dati e analisi** fare clic su **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="2112b-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="2112b-117">Nel **pannello della Raccolta di aree di lavoro** immettere le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="2112b-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="2112b-118">Per **Prezzi**, vedere [Prezzi di Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="2112b-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="2112b-119">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="2112b-119">Click **Create**.</span></span>

<span data-ttu-id="2112b-120">Il provisioning della **Raccolta di aree di lavoro** richiederà alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="2112b-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="2112b-121">Al termine verrà visualizzato il **pannello della Raccolta di aree di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2112b-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="2112b-122">Questo **pannello di creazione** contiene le informazioni necessarie per chiamare le API che creano le aree di lavoro e vi distribuiscono il contenuto.</span><span class="sxs-lookup"><span data-stu-id="2112b-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="2112b-123">Visualizzare le chiavi di accesso dell'API Power BI</span><span class="sxs-lookup"><span data-stu-id="2112b-123">View Power BI API access keys</span></span>

<span data-ttu-id="2112b-124">Le **chiavi di accesso**sono tra le informazioni più importanti necessarie per chiamare le API REST Power BI.</span><span class="sxs-lookup"><span data-stu-id="2112b-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="2112b-125">Vengono usate per generare i **token delle app** che servono per autenticare le richieste delle API.</span><span class="sxs-lookup"><span data-stu-id="2112b-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="2112b-126">Per visualizzare le **chiavi di accesso** fare clic su **Chiavi di accesso** nel pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="2112b-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="2112b-127">Per altre informazioni sui **token delle app**, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="2112b-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="2112b-128">Come si noterà, sono disponibili due chiavi.</span><span class="sxs-lookup"><span data-stu-id="2112b-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="2112b-129">Copiarle e archiviarle in modo sicuro nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2112b-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="2112b-130">È molto importante gestire queste chiavi come una password, perché forniscono l'accesso a tutto il contenuto della **Raccolta di aree di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2112b-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="2112b-131">Anche se sono disponibili due chiavi, è necessaria una sola chiave alla volta.</span><span class="sxs-lookup"><span data-stu-id="2112b-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="2112b-132">La seconda chiave viene fornita per consentire di rigenerare periodicamente le chiavi senza interrompere l'accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="2112b-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="2112b-133">Dopo aver creato un'istanza di Power BI per l'applicazione e le **chiavi di accesso**, è possibile importare un report nell'app in uso.</span><span class="sxs-lookup"><span data-stu-id="2112b-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="2112b-134">Prima di apprendere come importare un report, la sezione successiva descrive come creare set di dati e report di Power BI da incorporare in un'app.</span><span class="sxs-lookup"><span data-stu-id="2112b-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="2112b-135">Utilizzo di aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="2112b-135">Working with workspaces</span></span>

<span data-ttu-id="2112b-136">Dopo aver creato la raccolta di aree di lavoro, è necessario creare un'area di lavoro che dovrà contenere i report e i set di dati.</span><span class="sxs-lookup"><span data-stu-id="2112b-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="2112b-137">Per creare un'area di lavoro, usare l'[API REST di pubblicazione area di lavoro](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="2112b-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="2112b-138">Creare set di dati e report di Power BI da incorporare in un'app usando Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2112b-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="2112b-139">Dopo avere creato un'istanza di Power BI per l'applicazione e le **chiavi di accesso**, è necessario creare i set di dati e i report di Power BI da incorporare.</span><span class="sxs-lookup"><span data-stu-id="2112b-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="2112b-140">I set di dati e i report possono essere creati con **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="2112b-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="2112b-141">È possibile scaricare [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="2112b-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="2112b-142">In alternativa, per iniziare rapidamente, è possibile scaricare l' [esempio Retail Analysis PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="2112b-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="2112b-143">Per altre informazioni sull'uso di **Power BI Desktop**, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="2112b-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="2112b-144">**Power BI Desktop** consente di connettersi all'origine dati importando una copia dei dati in **Power BI Desktop** o tramite la connessione diretta all'origine dati con **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="2112b-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="2112b-145">Di seguito sono spiegate le differenze tra l'**importazione** e la modalità **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="2112b-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="2112b-146">Importa</span><span class="sxs-lookup"><span data-stu-id="2112b-146">Import</span></span> | <span data-ttu-id="2112b-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="2112b-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="2112b-148">Tabelle, colonne, *e dati* vengono importati o copiati in **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="2112b-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="2112b-149">Mentre si usano le visualizzazioni, **Power BI Desktop** esegue query su una copia dei dati.</span><span class="sxs-lookup"><span data-stu-id="2112b-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="2112b-150">Per visualizzare le eventuali modifiche apportate ai dati sottostanti, è necessario aggiornare o importare di nuovo un set di dati completo e aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2112b-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="2112b-151">Solo *tabelle e colonne* vengono importate o copiate in **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="2112b-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="2112b-152">Mentre si usano le visualizzazioni, **Power BI Desktop** esegue query sull'origine dati sottostante, quindi vengono sempre visualizzati dati aggiornati.</span><span class="sxs-lookup"><span data-stu-id="2112b-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="2112b-153">Per altre informazioni sulla connessione a un'origine dati, vedere [Connettersi a un'origine dati](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="2112b-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="2112b-154">Dopo aver salvato il lavoro in **Power BI Desktop**viene creato un file PBIX.</span><span class="sxs-lookup"><span data-stu-id="2112b-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="2112b-155">Questo file contiene il report.</span><span class="sxs-lookup"><span data-stu-id="2112b-155">This file contains your report.</span></span> <span data-ttu-id="2112b-156">Se si importano dati, il PBIX include il set di dati completo, mentre se si usa **DirectQuery**, il PBIX contiene solo uno schema del set di dati.</span><span class="sxs-lookup"><span data-stu-id="2112b-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="2112b-157">Distribuire a livello di codice il PBIX nell'area di lavoro con l' [API di importazione di Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="2112b-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2112b-158">**Power BI Embedded** include altre API per modificare il server e il database a cui punta il set di dati e impostare le credenziali dell'account del servizio che saranno usate dal set di dati per la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="2112b-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="2112b-159">Vedere [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (POST di SetAllConnections) e [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (PATCH dell'origine dati del gateway).</span><span class="sxs-lookup"><span data-stu-id="2112b-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="2112b-160">Creare set di dati e report di Power BI usando le API</span><span class="sxs-lookup"><span data-stu-id="2112b-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="2112b-161">Set di dati</span><span class="sxs-lookup"><span data-stu-id="2112b-161">Datsets</span></span>

<span data-ttu-id="2112b-162">È possibile creare set di dati all'interno di Power BI Embedded usando l'API REST</span><span class="sxs-lookup"><span data-stu-id="2112b-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="2112b-163">ed effettuare poi il push dei dati nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="2112b-163">You can then push data into your dataset.</span></span> <span data-ttu-id="2112b-164">In questo modo è possibile usare i dati senza Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="2112b-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="2112b-165">Per altre informazioni, vedere [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Pubblica set di dati).</span><span class="sxs-lookup"><span data-stu-id="2112b-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="2112b-166">Report</span><span class="sxs-lookup"><span data-stu-id="2112b-166">Reports</span></span>

<span data-ttu-id="2112b-167">È possibile creare un report da un set di dati direttamente nell'applicazione usando l'API JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2112b-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="2112b-168">Per altre informazioni, vedere [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="2112b-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2112b-169">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2112b-169">See Also</span></span>

[<span data-ttu-id="2112b-170">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="2112b-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="2112b-171">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2112b-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="2112b-172">[Embed a report](power-bi-embedded-embed-report.md) (Incorporare un report)</span><span class="sxs-lookup"><span data-stu-id="2112b-172">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
<span data-ttu-id="2112b-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded)
[Save reports](power-bi-embedded-save-reports.md) (Salvare report)</span><span class="sxs-lookup"><span data-stu-id="2112b-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="2112b-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2112b-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="2112b-175">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="2112b-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="2112b-176">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="2112b-176">More questions?</span></span> [<span data-ttu-id="2112b-177">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="2112b-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)

