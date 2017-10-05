---
title: Creare un modello tabulare usando la finestra di progettazione Web di Azure Analysis Services | Microsoft Docs
description: Informazioni su come creare un modello tabulare di Azure Analysis Services usando la finestra di progettazione Web nel portale di Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: bd58f1845dabf6afb47ce27236d14479677a8808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="11e2c-103">Creare un modello nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="11e2c-103">Create a model in Azure portal</span></span>

<span data-ttu-id="11e2c-104">La funzione finestra di progettazione Web di Azure Analysis Services (anteprima) nel portale di Azure offre un modo semplice e rapido per creare e modificare modelli tabulari ed eseguire query nei dati dei modelli direttamente dal browser in uso.</span><span class="sxs-lookup"><span data-stu-id="11e2c-104">The Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way to create and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="11e2c-105">Tenere presente che la finestra di progettazione Web è in versione di **anteprima**.</span><span class="sxs-lookup"><span data-stu-id="11e2c-105">Keep in mind, the web designer is **preview**.</span></span> <span data-ttu-id="11e2c-106">Anche se vengono aggiunte continuamente nuove funzionalità, nell'anteprima le funzionalità sono limitate.</span><span class="sxs-lookup"><span data-stu-id="11e2c-106">While new functionality is being added all the time, in preview, functionality is limited.</span></span> <span data-ttu-id="11e2c-107">Per operazioni più avanzate di sviluppo e testing dei modelli, è consigliabile usare Visual Studio (SSDT) e SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="11e2c-107">For more advanced model development and testing, it's best to use Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11e2c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="11e2c-108">Prerequisites</span></span>

- <span data-ttu-id="11e2c-109">Un server di Azure Analysis Services, livello Standard o Developer.</span><span class="sxs-lookup"><span data-stu-id="11e2c-109">An Azure Analysis Services server at the Standard or Developer tier.</span></span> <span data-ttu-id="11e2c-110">I nuovi modelli creati usando la finestra di progettazione Web sono di tipo DirectQuery e sono supportati solo da questi livelli.</span><span class="sxs-lookup"><span data-stu-id="11e2c-110">New models created by using the Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="11e2c-111">Un database SQL di Azure, Azure SQL Data Warehouse o un file di Power BI Desktop (con estensione pbix) come origine dati.</span><span class="sxs-lookup"><span data-stu-id="11e2c-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="11e2c-112">I nuovi modelli creati a partire da file di Power BI Desktop supportano origini dati di database SQL di Azure, Azure SQL Data Warehouse, Oracle e Teradata.</span><span class="sxs-lookup"><span data-stu-id="11e2c-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="11e2c-113">Un account di SQL Server con password per la connessione a origini dati di database SQL di Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="11e2c-113">A SQL Server account and password for connecting to Azure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="to-create-a-new-tabular-model"></a><span data-ttu-id="11e2c-114">Per creare un nuovo modello tabulare</span><span class="sxs-lookup"><span data-stu-id="11e2c-114">To create a new tabular model</span></span>

1. <span data-ttu-id="11e2c-115">Nel pannello **Panoramica**  del server > **Web designer** (Finestra di progettazione Web) fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="11e2c-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="11e2c-117">In **Web designer** (Finestra di progettazione Web)  >  **Modelli** fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="11e2c-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="11e2c-119">In **Nuovo modello** digitare un nome di modello e quindi selezionare un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="11e2c-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Finestra di dialogo Nuovo modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="11e2c-121">In **Connetti** immettere le proprietà di connessione.</span><span class="sxs-lookup"><span data-stu-id="11e2c-121">In **Connect**, enter the connection properties.</span></span> <span data-ttu-id="11e2c-122">Il nome utente e la password devono fare riferimento a un account di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="11e2c-122">Username and password must be a SQL Server account.</span></span>

     ![Finestra di dialogo Connetti nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="11e2c-124">In **Tabelle e viste** selezionare le tabelle da includere nel modello e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="11e2c-124">In **Tables and views**, select the tables to include in your model, and then click **Create**.</span></span> <span data-ttu-id="11e2c-125">Tra le tabelle con una coppia di chiavi vengono automaticamente create relazioni.</span><span class="sxs-lookup"><span data-stu-id="11e2c-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="11e2c-127">Nel browser verrà visualizzato il nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="11e2c-127">Your new model appears in your browser.</span></span> <span data-ttu-id="11e2c-128">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="11e2c-128">From here, you can:</span></span>   

- <span data-ttu-id="11e2c-129">Eseguire query nei dati del modello trascinando i campi nella finestra di progettazione delle query e aggiungendo i filtri desiderati.</span><span class="sxs-lookup"><span data-stu-id="11e2c-129">Query model data by dragging fields to the query designer and adding filters.</span></span>
- <span data-ttu-id="11e2c-130">Creare nuove misure nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="11e2c-130">Create new measures in tables.</span></span>
- <span data-ttu-id="11e2c-131">Modificare i metadati del modello usando l'editor JSON.</span><span class="sxs-lookup"><span data-stu-id="11e2c-131">Edit model metadata by using the json editor.</span></span>
- <span data-ttu-id="11e2c-132">Aprire il modello in Visual Studio (SSDT), Power BI Desktop o Excel.</span><span class="sxs-lookup"><span data-stu-id="11e2c-132">Open the model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="11e2c-134">Quando si modificano i metadati del modello o si creano nuove misure nel browser, le modifiche vengono salvate nel modello in Azure.</span><span class="sxs-lookup"><span data-stu-id="11e2c-134">When you edit model metadata or create new measures in your browser, you're saving those changes to your model in Azure.</span></span> <span data-ttu-id="11e2c-135">Se si stanno eseguendo operazioni sul modello anche in SSDT, Power BI Desktop o Excel, è possibile che il modello non venga sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="11e2c-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="11e2c-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11e2c-136">Next steps</span></span> 
[<span data-ttu-id="11e2c-137">Gestire ruoli e utenti del database</span><span class="sxs-lookup"><span data-stu-id="11e2c-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="11e2c-138">Stabilire la connessione con Excel</span><span class="sxs-lookup"><span data-stu-id="11e2c-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


