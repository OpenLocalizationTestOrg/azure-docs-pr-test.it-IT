---
title: Eseguire la distribuzione in Azure Analysis Services con SSDT | Microsoft Docs
description: Informazioni su come distribuire un modello tabulare in un server Azure Analysis Services usando SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="eedbf-103">Distribuire un modello da SSDT</span><span class="sxs-lookup"><span data-stu-id="eedbf-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="eedbf-104">Dopo aver creato un server nella sottoscrizione di Azure, si è pronti per distribuire un database modello tabulare a tale server.</span><span class="sxs-lookup"><span data-stu-id="eedbf-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="eedbf-105">È possibile usare SQL Server Data Tools (SSDT) per compilare e distribuire un progetto modello tabulare in uso.</span><span class="sxs-lookup"><span data-stu-id="eedbf-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eedbf-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eedbf-106">Prerequisites</span></span>
<span data-ttu-id="eedbf-107">Per iniziare, è necessario:</span><span class="sxs-lookup"><span data-stu-id="eedbf-107">To get started, you need:</span></span>

* <span data-ttu-id="eedbf-108">Un **server Analysis Services** in Azure.</span><span class="sxs-lookup"><span data-stu-id="eedbf-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="eedbf-109">Per altre informazioni, vedere [Creare un server Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="eedbf-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="eedbf-110">Un **progetto di modello tabulare** in SSDT o un modello tabulare esistente con livello di compatibilità 1200 o superiore.</span><span class="sxs-lookup"><span data-stu-id="eedbf-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="eedbf-111">Se non è mai stato creato un progetto simile,</span><span class="sxs-lookup"><span data-stu-id="eedbf-111">Never created one?</span></span> <span data-ttu-id="eedbf-112">Vedere [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx) (Esercitazione sul modello tabulare di vendite Internet per Adventure Works).</span><span class="sxs-lookup"><span data-stu-id="eedbf-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="eedbf-113">Un **gateway locale**: se una o più origini dati si trovano nella rete locale dell'organizzazione, è necessario installare un [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="eedbf-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="eedbf-114">Il gateway è necessario affinché il server nel cloud possa connettersi alle origini dati locali per elaborare e aggiornare i dati nel modello.</span><span class="sxs-lookup"><span data-stu-id="eedbf-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="eedbf-115">Prima di distribuire, assicurarsi che sia possibile elaborare i dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="eedbf-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="eedbf-116">In SSDT fare clic su **Modello** > **Elabora** > **Elabora tutto**.</span><span class="sxs-lookup"><span data-stu-id="eedbf-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="eedbf-117">Se l'elaborazione ha esito negativo, la distribuzione non potrà essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="eedbf-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="eedbf-118">Per distribuire un modello tabulare da SSDT</span><span class="sxs-lookup"><span data-stu-id="eedbf-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="eedbf-119">Prima di distribuire, è necessario ottenere il nome del server.</span><span class="sxs-lookup"><span data-stu-id="eedbf-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="eedbf-120">In **portale di Azure** > server > **Panoramica** > **Nome server** copiare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="eedbf-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="eedbf-122">In SSDT > **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto > **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="eedbf-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="eedbf-123">Quindi in **Distribuzione** > **Server** incollare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="eedbf-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Incollare il nome del server nelle proprietà del server di distribuzione](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="eedbf-125">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Proprietà** e quindi scegliere **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="eedbf-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="eedbf-126">Verrà visualizzata la richiesta di accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="eedbf-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Distribuire al server](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="eedbf-128">Lo stato di distribuzione viene visualizzato sia nella finestra di output che nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="eedbf-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Stato della distribuzione](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="eedbf-130">Questo è tutto ciò che occorre fare.</span><span class="sxs-lookup"><span data-stu-id="eedbf-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="eedbf-131">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="eedbf-131">Troubleshooting</span></span>
<span data-ttu-id="eedbf-132">Se la distribuzione non riesce durante la distribuzione dei metadati, probabilmente è dovuto al fatto che SSDT non può connettersi al server.</span><span class="sxs-lookup"><span data-stu-id="eedbf-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="eedbf-133">Assicurarsi di potersi connettere al server usando SSMS.</span><span class="sxs-lookup"><span data-stu-id="eedbf-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="eedbf-134">Verificare quindi che la proprietà del server di distribuzione per il progetto sia corretta.</span><span class="sxs-lookup"><span data-stu-id="eedbf-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="eedbf-135">Se la distribuzione non riesce in una tabella, probabilmente è dovuto al fatto che il server non ha potuto connettersi a un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="eedbf-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="eedbf-136">Se l'origine dati è locale nella rete dell'organizzazione, assicurarsi di installare un [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="eedbf-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eedbf-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eedbf-137">Next steps</span></span>
<span data-ttu-id="eedbf-138">Ora che il modello tabulare è stato distribuito nel server, si è pronti per la connessione.</span><span class="sxs-lookup"><span data-stu-id="eedbf-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="eedbf-139">È possibile [connettersi al modello con SSMS](analysis-services-manage.md) per gestirlo.</span><span class="sxs-lookup"><span data-stu-id="eedbf-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="eedbf-140">Ed è anche possibile [connettersi al modello usando uno strumento client](analysis-services-connect.md) come Power BI, Power BI Desktop o Excel e avviare la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="eedbf-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

