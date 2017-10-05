---
title: 'Esercitazione su Azure Analysis Services - Lezione 13: Distribuire | Microsoft Docs'
description: Descrive come distribuire il progetto per l'esercitazione in Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="68eb1-103">Lezione 13: Distribuire</span><span class="sxs-lookup"><span data-stu-id="68eb1-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="68eb1-104">In questa lezione vengono configurate le proprietà della distribuzione, specificando un server di Azure Analysis Services come destinazione per la distribuzione e un nome per il modello.</span><span class="sxs-lookup"><span data-stu-id="68eb1-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="68eb1-105">Verrà quindi descritta la procedura per distribuire il modello in tale istanza.</span><span class="sxs-lookup"><span data-stu-id="68eb1-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="68eb1-106">Dopo aver distribuito il modello, gli utenti possono connettersi a esso tramite un'applicazione client per la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="68eb1-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="68eb1-107">Per altre informazioni, vedere [Distribuire in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="68eb1-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="68eb1-108">Tempo previsto per il completamento della lezione: **5 minuti**</span><span class="sxs-lookup"><span data-stu-id="68eb1-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="68eb1-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68eb1-109">Prerequisites</span></span>  
<span data-ttu-id="68eb1-110">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="68eb1-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="68eb1-111">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 12: Analizzare in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="68eb1-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="68eb1-112">È necessario avere [autorizzazioni di amministratore](../analysis-services-server-admins.md) per l'istanza remota del server Analysis Services per eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="68eb1-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="68eb1-113">Se il database di esempio AdventureWorksDW2014 è stato installato in un'istanza di SQL Server locale e si distribuisce il modello in un server Azure Analysis Services, è richiesto un [gateway dati locale](../analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="68eb1-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="68eb1-114">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="68eb1-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="68eb1-115">Per configurare le proprietà di distribuzione</span><span class="sxs-lookup"><span data-stu-id="68eb1-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="68eb1-116">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **AW Internet Sales** e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="68eb1-117">Nella finestra di dialogo **Pagine delle proprietà di AW Internet Sales** in **Server di distribuzione** nella proprietà **Server** immettere il server completo.</span><span class="sxs-lookup"><span data-stu-id="68eb1-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="68eb1-119">Nella proprietà **Database** digitare **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="68eb1-120">Nella proprietà **Nome modello** digitare **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="68eb1-121">Verificare le selezioni e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="68eb1-122">Per distribuire il modello Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="68eb1-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="68eb1-123">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **AW Internet Sales** e quindi scegliere **Compila**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="68eb1-124">Fare clic con il pulsante destro del mouse sul progetto **AW Internet Sales** e quindi scegliere **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="68eb1-125">Durante la distribuzione in Azure Analysis Services potrebbe essere richiesto di immettere le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="68eb1-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="68eb1-126">Immettere nome e password dell'account dell'organizzazione, ad esempio nancy@adventureworks.com. Questo account deve essere incluso nel gruppo Admins del server.</span><span class="sxs-lookup"><span data-stu-id="68eb1-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="68eb1-127">Verrà visualizzata la finestra di dialogo Distribuisci con indicazione dello stato della distribuzione dei metadati e di ogni tabella inclusa nel modello.</span><span class="sxs-lookup"><span data-stu-id="68eb1-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="68eb1-129">Dopo aver completato correttamente la distribuzione, procedere e fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="68eb1-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="68eb1-130">Conclusione</span><span class="sxs-lookup"><span data-stu-id="68eb1-130">Conclusion</span></span>  
<span data-ttu-id="68eb1-131">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="68eb1-131">Congratulations!</span></span> <span data-ttu-id="68eb1-132">Sono state completate le attività di creazione e distribuzione del primo modello tabulare di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="68eb1-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="68eb1-133">In questa esercitazione sono state descritte le procedure per eseguire in modo guidato la maggior parte delle attività più comuni per la creazione di un modello tabulare.</span><span class="sxs-lookup"><span data-stu-id="68eb1-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="68eb1-134">Dopo aver distribuito il modello Adventure Works Internet Sales, è possibile usare SQL Server Management Studio per gestire il modello, creare script di elaborazione e un piano di backup.</span><span class="sxs-lookup"><span data-stu-id="68eb1-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="68eb1-135">Ora gli utenti possono anche connettersi al modello usando un'applicazione client per la creazione di report, come Microsoft Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="68eb1-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="68eb1-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68eb1-137">What's next?</span></span>
<span data-ttu-id="68eb1-138">[Connettersi con Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="68eb1-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="68eb1-139">[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="68eb1-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="68eb1-140">[Lezione supplementare: Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="68eb1-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="68eb1-141">Lezione supplementare: Gerarchie incomplete</span><span class="sxs-lookup"><span data-stu-id="68eb1-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
