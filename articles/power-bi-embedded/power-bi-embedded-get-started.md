---
title: Introduzione a Microsoft Power BI Embedded aaaGet
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
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="7f13a-103">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7f13a-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="7f13a-104">**Power BI Embedded** è un servizio di Azure che tooadd agli sviluppatori di applicazioni consente report interattivi di Power BI nelle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7f13a-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="7f13a-105">**Power BI Embedded** funziona con le applicazioni esistenti, senza la necessità di riprogettazione o modificare utenti modo hello Accedi.</span><span class="sxs-lookup"><span data-stu-id="7f13a-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="7f13a-106">Risorse per **Microsoft Power BI Embedded** viene effettuato il provisioning tramite hello [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f13a-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="7f13a-107">In questo caso, risorse hello viene effettuato il provisioning sono una **raccolta dell'area di lavoro di Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="7f13a-108">Creare una raccolta di aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="7f13a-108">Create a workspace collection</span></span>

<span data-ttu-id="7f13a-109">Oggetto **dell'area di lavoro raccolta** è una risorsa di Azure di livello superiore di hello e un contenitore per il contenuto di hello che verrà incorporato nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f13a-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="7f13a-110">Una **Raccolta di aree di lavoro** può essere creata in due modi:</span><span class="sxs-lookup"><span data-stu-id="7f13a-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="7f13a-111">Manualmente tramite il portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7f13a-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="7f13a-112">Livello di programmazione tramite hello API Manager(ARM) risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7f13a-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="7f13a-113">Si analizzerà hello passaggi toobuild un **dell'area di lavoro raccolta** utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f13a-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="7f13a-114">Aprire il **portale di Azure**ed eseguire l'accesso: [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f13a-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="7f13a-115">Fare clic su **+ nuovo** nel riquadro superiore hello.</span><span class="sxs-lookup"><span data-stu-id="7f13a-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="7f13a-116">In **Dati e analisi** fare clic su **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="7f13a-117">In hello **dell'area di lavoro Raccolta pannello**, immettere le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="7f13a-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="7f13a-118">Per **Prezzi**, vedere [Prezzi di Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="7f13a-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="7f13a-119">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-119">Click **Create**.</span></span>

<span data-ttu-id="7f13a-120">Hello **dell'area di lavoro raccolta** richiederà qualche minuto tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7f13a-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="7f13a-121">Al termine, verrà visualizzato toohello **dell'area di lavoro Raccolta pannello**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="7f13a-122">Hello **pannello creazione** contiene informazioni hello necessarie toocall hello API che creano aree di lavoro e distribuire contenuto toothem.</span><span class="sxs-lookup"><span data-stu-id="7f13a-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="7f13a-123">Visualizzare le chiavi di accesso dell'API Power BI</span><span class="sxs-lookup"><span data-stu-id="7f13a-123">View Power BI API access keys</span></span>

<span data-ttu-id="7f13a-124">Uno dei principali tipi di informazioni necessarie toocall hello API REST di Power BI hello sono hello **chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="7f13a-125">Questi vengono utilizzati toogenerate hello **token app** che vengono utilizzati tooauthenticate le richieste API.</span><span class="sxs-lookup"><span data-stu-id="7f13a-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="7f13a-126">tooview il **chiavi di accesso**, fare clic su **chiavi di accesso** su hello **pannello impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="7f13a-127">Per altre informazioni sui **token delle app**, vedere [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="7f13a-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="7f13a-128">Come si noterà, sono disponibili due chiavi.</span><span class="sxs-lookup"><span data-stu-id="7f13a-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="7f13a-129">Copiarle e archiviarle in modo sicuro nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f13a-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="7f13a-130">È molto importante considerare queste chiavi come si farebbe con una password, perché verrà forniscono accesso tooall hello contenuto il **dell'area di lavoro insieme**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="7f13a-131">Anche se sono disponibili due chiavi, è necessaria una sola chiave alla volta.</span><span class="sxs-lookup"><span data-stu-id="7f13a-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="7f13a-132">seconda chiave Hello viene fornito e quindi è possibile rigenerare periodicamente le chiavi senza interrompere il servizio di accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="7f13a-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="7f13a-133">Dopo aver creato un'istanza di Power BI per l'applicazione e le **chiavi di accesso**, è possibile importare un report nell'app in uso.</span><span class="sxs-lookup"><span data-stu-id="7f13a-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="7f13a-134">Prima viene illustrato come tooimport un report, nella sezione successiva hello descrive la creazione tooembed set di dati e i report di Power BI in un'app.</span><span class="sxs-lookup"><span data-stu-id="7f13a-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="7f13a-135">Utilizzo di aree di lavoro</span><span class="sxs-lookup"><span data-stu-id="7f13a-135">Working with workspaces</span></span>

<span data-ttu-id="7f13a-136">Dopo aver creato la raccolta dell'area di lavoro, sarà necessario toocreate un'area di lavoro che conterrà i report e set di dati.</span><span class="sxs-lookup"><span data-stu-id="7f13a-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="7f13a-137">toocreate un'area di lavoro, sarà necessario hello toouse [API REST di area di lavoro Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f13a-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="7f13a-138">Creare tooembed set di dati e i report di Power BI in un'app con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7f13a-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="7f13a-139">Ora che è stata creata un'istanza di Power BI per l'applicazione e ha **chiavi di accesso**, saranno necessari il set di dati di toocreate hello Power BI e report che si desidera tooembed.</span><span class="sxs-lookup"><span data-stu-id="7f13a-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="7f13a-140">I set di dati e i report possono essere creati con **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="7f13a-141">È possibile scaricare [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="7f13a-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="7f13a-142">In alternativa, iniziare tooquickly, è possibile scaricare hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="7f13a-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="7f13a-143">altre informazioni su come toolearn toouse **Power BI Desktop**, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="7f13a-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="7f13a-144">Con **Power BI Desktop**, tooyour origine dei dati si connette tramite l'importazione di una copia dei dati di hello in **Power BI Desktop** o la connessione diretta toohello dati di origine utilizzando **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="7f13a-145">Di seguito sono differenze nell'utilizzo hello **importazione** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="7f13a-146">Importa</span><span class="sxs-lookup"><span data-stu-id="7f13a-146">Import</span></span> | <span data-ttu-id="7f13a-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="7f13a-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="7f13a-148">Tabelle, colonne, *e dati* vengono importati o copiati in **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7f13a-149">Mentre si lavora con visualizzazioni, **Power BI Desktop** una copia dei dati hello una query.</span><span class="sxs-lookup"><span data-stu-id="7f13a-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="7f13a-150">toosee eventuali modifiche di dati sottostante toohello durante l'esecuzione, è necessario aggiornare o importare, nuovamente un dataset corrente non completato.</span><span class="sxs-lookup"><span data-stu-id="7f13a-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="7f13a-151">Solo *tabelle e colonne* vengono importate o copiate in **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7f13a-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7f13a-152">Mentre si lavora con visualizzazioni, **Power BI Desktop** query hello origine dati sottostante, ovvero sempre si visualizzano i dati correnti.</span><span class="sxs-lookup"><span data-stu-id="7f13a-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="7f13a-153">Per ulteriori informazioni sull'origine dei dati tooa connessione, vedere [origine dati di connessione tooa](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="7f13a-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="7f13a-154">Dopo aver salvato il lavoro in **Power BI Desktop**viene creato un file PBIX.</span><span class="sxs-lookup"><span data-stu-id="7f13a-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="7f13a-155">Questo file contiene il report.</span><span class="sxs-lookup"><span data-stu-id="7f13a-155">This file contains your report.</span></span> <span data-ttu-id="7f13a-156">Inoltre, se si importa hello dati PBIX contiene hello set di dati completo, o se si utilizza **DirectQuery**, hello PBIX contiene uno schema di set di dati.</span><span class="sxs-lookup"><span data-stu-id="7f13a-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="7f13a-157">Distribuire a livello di codice hello PBIX nell'area di lavoro utilizzando hello [API Power BI Importa](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f13a-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7f13a-158">**Power BI Embedded** dispone di altre API toochange hello server e database che il set di dati fa riferimento il set di tooand una credenziale dell'account del servizio che hello set di dati utilizzerà tooconnect tooyour database.</span><span class="sxs-lookup"><span data-stu-id="7f13a-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="7f13a-159">Vedere [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) (POST di SetAllConnections) e [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (PATCH dell'origine dati del gateway).</span><span class="sxs-lookup"><span data-stu-id="7f13a-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="7f13a-160">Creare set di dati e report di Power BI usando le API</span><span class="sxs-lookup"><span data-stu-id="7f13a-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="7f13a-161">Set di dati</span><span class="sxs-lookup"><span data-stu-id="7f13a-161">Datsets</span></span>

<span data-ttu-id="7f13a-162">È possibile creare set di dati in Power BI Embedded utilizzando hello API REST.</span><span class="sxs-lookup"><span data-stu-id="7f13a-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="7f13a-163">ed effettuare poi il push dei dati nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="7f13a-163">You can then push data into your dataset.</span></span> <span data-ttu-id="7f13a-164">In questo modo toowork con i dati senza necessità di hello di Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7f13a-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="7f13a-165">Per altre informazioni, vedere [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Pubblica set di dati).</span><span class="sxs-lookup"><span data-stu-id="7f13a-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="7f13a-166">Report</span><span class="sxs-lookup"><span data-stu-id="7f13a-166">Reports</span></span>

<span data-ttu-id="7f13a-167">È possibile creare un report da un set di dati direttamente in un'applicazione con hello API JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7f13a-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="7f13a-168">Per altre informazioni, vedere [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="7f13a-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7f13a-169">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7f13a-169">See Also</span></span>

[<span data-ttu-id="7f13a-170">Esempio introduttivo</span><span class="sxs-lookup"><span data-stu-id="7f13a-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7f13a-171">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7f13a-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="7f13a-172">[Embed a report](power-bi-embedded-embed-report.md) (Incorporare un report)</span><span class="sxs-lookup"><span data-stu-id="7f13a-172">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
<span data-ttu-id="7f13a-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creare un nuovo report da un set di dati in Power BI Embedded)
[Save reports](power-bi-embedded-save-reports.md) (Salvare report)</span><span class="sxs-lookup"><span data-stu-id="7f13a-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="7f13a-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7f13a-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7f13a-175">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="7f13a-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7f13a-176">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="7f13a-176">More questions?</span></span> [<span data-ttu-id="7f13a-177">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="7f13a-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

