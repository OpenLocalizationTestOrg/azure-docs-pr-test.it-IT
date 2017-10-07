---
<span data-ttu-id="7ae79-101">titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 13: distribuire | Descrizione di "Microsoft Docs: viene descritto come esercitazione hello toodeploy progetto tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7ae79-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="7ae79-102">servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '</span><span class="sxs-lookup"><span data-stu-id="7ae79-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="7ae79-103">ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: na ms. date: 07/17/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="7ae79-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="7ae79-104">Lezione 13: Distribuire</span><span class="sxs-lookup"><span data-stu-id="7ae79-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7ae79-105">In questa lezione, configurare le proprietà di distribuzione; Specifica un tooand di toodeploy server un nome per il modello di hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7ae79-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="7ae79-106">È quindi possibile distribuire istanza toothat di hello del modello.</span><span class="sxs-lookup"><span data-stu-id="7ae79-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="7ae79-107">Dopo aver distribuito il modello, gli utenti possono connettersi tooit tramite un'applicazione client di creazione di report.</span><span class="sxs-lookup"><span data-stu-id="7ae79-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="7ae79-108">vedere, più toolearn [distribuire tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="7ae79-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="7ae79-109">Stimato toocomplete ora questa lezione: **5 minuti**</span><span class="sxs-lookup"><span data-stu-id="7ae79-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7ae79-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7ae79-110">Prerequisites</span></span>  
<span data-ttu-id="7ae79-111">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="7ae79-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7ae79-112">Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 12: analizza in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="7ae79-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="7ae79-113">È necessario disporre di [le autorizzazioni di amministratore](../analysis-services-server-admins.md) on hello remoto Analysis Services server nell'ordine toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="7ae79-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="7ae79-114">Se è installato il database di esempio hello AdventureWorksDW2014 su un Server SQL locale e si distribuisce il server di Azure Analysis Services tooan modello, un [gateway dati locale](../analysis-services-gateway.md) è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="7ae79-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="7ae79-115">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="7ae79-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="7ae79-116">proprietà di distribuzione tooconfigure</span><span class="sxs-lookup"><span data-stu-id="7ae79-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="7ae79-117">In **Esplora**, hello rapida **AW Internet Sales** del progetto e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="7ae79-118">In hello **pagine delle proprietà di AW Internet Sales** nella finestra di dialogo **Server di distribuzione**, in hello **Server** proprietà, digitare hello del server completo.</span><span class="sxs-lookup"><span data-stu-id="7ae79-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="7ae79-120">In hello **Database** proprietà, digitare **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="7ae79-121">In hello **nome modello** proprietà, digitare **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="7ae79-122">Verificare le selezioni e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="7ae79-123">hello toodeploy Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="7ae79-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="7ae79-124">In **Esplora**, hello rapida **AW Internet Sales** progetto > **compilare**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="7ae79-125">Pulsante destro del mouse hello **AW Internet Sales** progetto > **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="7ae79-126">Quando si distribuisce tooAzure Analysis Services, potrebbe essere richiesta tooenter l'account.</span><span class="sxs-lookup"><span data-stu-id="7ae79-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="7ae79-127">Immettere nome e password dell'account dell'organizzazione, ad esempio nancy@adventureworks.com. Questo account deve essere Admins nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="7ae79-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="7ae79-128">finestra di dialogo Distribuisci Hello viene visualizzato e Mostra lo stato di distribuzione hello dei metadati hello e ogni tabella inclusa nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7ae79-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="7ae79-130">Dopo aver completato correttamente la distribuzione, procedere e fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="7ae79-131">Conclusione</span><span class="sxs-lookup"><span data-stu-id="7ae79-131">Conclusion</span></span>  
<span data-ttu-id="7ae79-132">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="7ae79-132">Congratulations!</span></span> <span data-ttu-id="7ae79-133">Sono state completate le attività di creazione e distribuzione del primo modello tabulare di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7ae79-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="7ae79-134">Questa esercitazione sono state consentono di eseguire il completamento delle attività più comuni di hello nella creazione di un modello tabulare.</span><span class="sxs-lookup"><span data-stu-id="7ae79-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="7ae79-135">Ora che viene distribuito il modello Adventure Works Internet Sales, è possibile utilizzare un modello di hello toomanage di SQL Server Management Studio. creare script di processo e un piano di backup.</span><span class="sxs-lookup"><span data-stu-id="7ae79-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="7ae79-136">Gli utenti possono ora connettersi toohello modello utilizzando un'applicazione client di creazione di report, ad esempio Microsoft Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="7ae79-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="7ae79-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ae79-138">What's next?</span></span>
<span data-ttu-id="7ae79-139">[Connettersi con Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="7ae79-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="7ae79-140">[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="7ae79-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="7ae79-141">[Lezione supplementare: Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="7ae79-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="7ae79-142">Lezione supplementare: Gerarchie incomplete</span><span class="sxs-lookup"><span data-stu-id="7ae79-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
