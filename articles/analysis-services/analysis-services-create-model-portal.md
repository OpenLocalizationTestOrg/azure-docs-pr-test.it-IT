---
title: un modello tabulare utilizzando Progettazione Web di Azure Analysis Services hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un modello tabulare di Analysis Services di Azure tramite hello designer Web nel portale di Azure.
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
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="33153-103">Creare un modello nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="33153-103">Create a model in Azure portal</span></span>

<span data-ttu-id="33153-104">funzionalità di progettazione (anteprima) Hello Azure Analysis Services web nel portale di Azure fornisce un modo semplice e rapido di toocreate e modificare i modelli tabulari e query modello dati direttamente nel browser.</span><span class="sxs-lookup"><span data-stu-id="33153-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="33153-105">Tenere presente, finestra di progettazione web hello è **anteprima**.</span><span class="sxs-lookup"><span data-stu-id="33153-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="33153-106">Mentre la nuova funzionalità viene aggiunto ogni volta hello, in anteprima, la funzionalità è limitata.</span><span class="sxs-lookup"><span data-stu-id="33153-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="33153-107">Per più avanzate modello lo sviluppo e test, è migliore toouse Visual Studio (SSDT) e SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="33153-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33153-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33153-108">Prerequisites</span></span>

- <span data-ttu-id="33153-109">Un server di Azure Analysis Services a livello di hello Standard o Developer.</span><span class="sxs-lookup"><span data-stu-id="33153-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="33153-110">I nuovi modelli creati utilizzando la finestra di progettazione Web hello sono DirectQuery, supportato solo da questi livelli.</span><span class="sxs-lookup"><span data-stu-id="33153-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="33153-111">Un database SQL di Azure, Azure SQL Data Warehouse o un file di Power BI Desktop (con estensione pbix) come origine dati.</span><span class="sxs-lookup"><span data-stu-id="33153-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="33153-112">I nuovi modelli creati a partire da file di Power BI Desktop supportano origini dati di database SQL di Azure, Azure SQL Data Warehouse, Oracle e Teradata.</span><span class="sxs-lookup"><span data-stu-id="33153-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="33153-113">Un account di SQL Server e una password per la connessione a origini di dati di Database SQL o Azure SQL Data Warehouse tooAzure.</span><span class="sxs-lookup"><span data-stu-id="33153-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="33153-114">toocreate un nuovo modello tabulare</span><span class="sxs-lookup"><span data-stu-id="33153-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="33153-115">Nel pannello **Panoramica**  del server > **Web designer** (Finestra di progettazione Web) fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="33153-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="33153-117">In **Web designer** (Finestra di progettazione Web)  >  **Modelli** fare clic su **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="33153-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="33153-119">In **Nuovo modello** digitare un nome di modello e quindi selezionare un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="33153-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Finestra di dialogo Nuovo modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="33153-121">In **Connetti**, immettere le proprietà di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="33153-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="33153-122">Il nome utente e la password devono fare riferimento a un account di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33153-122">Username and password must be a SQL Server account.</span></span>

     ![Finestra di dialogo Connetti nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="33153-124">In **tabelle e viste**selezionare hello tooinclude di tabelle nel modello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="33153-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="33153-125">Tra le tabelle con una coppia di chiavi vengono automaticamente create relazioni.</span><span class="sxs-lookup"><span data-stu-id="33153-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="33153-127">Nel browser verrà visualizzato il nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="33153-127">Your new model appears in your browser.</span></span> <span data-ttu-id="33153-128">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="33153-128">From here, you can:</span></span>   

- <span data-ttu-id="33153-129">Dati del modello di query trascinando campi toohello query della finestra di progettazione e l'aggiunta di filtri.</span><span class="sxs-lookup"><span data-stu-id="33153-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="33153-130">Creare nuove misure nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="33153-130">Create new measures in tables.</span></span>
- <span data-ttu-id="33153-131">Modificare i metadati del modello utilizzando l'editor json hello.</span><span class="sxs-lookup"><span data-stu-id="33153-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="33153-132">Aprire il modello di hello in Visual Studio (SSDT), Power BI Desktop o Excel.</span><span class="sxs-lookup"><span data-stu-id="33153-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="33153-134">Quando si modificano i metadati del modello o creare nuove misure nel browser, salvato del modello tooyour tali modifiche in Azure.</span><span class="sxs-lookup"><span data-stu-id="33153-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="33153-135">Se si stanno eseguendo operazioni sul modello anche in SSDT, Power BI Desktop o Excel, è possibile che il modello non venga sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="33153-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="33153-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33153-136">Next steps</span></span> 
[<span data-ttu-id="33153-137">Gestire ruoli e utenti del database</span><span class="sxs-lookup"><span data-stu-id="33153-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="33153-138">Stabilire la connessione con Excel</span><span class="sxs-lookup"><span data-stu-id="33153-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


