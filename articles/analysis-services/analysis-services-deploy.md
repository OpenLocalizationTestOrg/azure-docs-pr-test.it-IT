---
title: aaaDeploy tooAzure Analysis Services tramite SSDT | Documenti Microsoft
description: Informazioni su come toodeploy tooan un modello tabulare Azure Analysis Services server mediante SSDT.
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="867b4-103">Distribuire un modello da SSDT</span><span class="sxs-lookup"><span data-stu-id="867b4-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="867b4-104">Dopo aver creato un server nella sottoscrizione di Azure, si è pronti toodeploy un tooit database modello tabulare.</span><span class="sxs-lookup"><span data-stu-id="867b4-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="867b4-105">È possibile utilizzare SQL Server Data Tools (SSDT) toobuild e distribuire un progetto di modello tabulare, che si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="867b4-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="867b4-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="867b4-106">Prerequisites</span></span>
<span data-ttu-id="867b4-107">tooget avviato, è necessario:</span><span class="sxs-lookup"><span data-stu-id="867b4-107">tooget started, you need:</span></span>

* <span data-ttu-id="867b4-108">Un **server Analysis Services** in Azure.</span><span class="sxs-lookup"><span data-stu-id="867b4-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="867b4-109">vedere, più toolearn [creare un server Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="867b4-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="867b4-110">**Progetto di modello tabulare** in SSDT o un modello tabulare esistente in hello 1200 o livello di compatibilità superiore.</span><span class="sxs-lookup"><span data-stu-id="867b4-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="867b4-111">Se non è mai stato creato un progetto simile,</span><span class="sxs-lookup"><span data-stu-id="867b4-111">Never created one?</span></span> <span data-ttu-id="867b4-112">Provare a hello [esercitazione relativa alla modellazione tabulare delle vendite Internet di Adventure Works](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="867b4-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="867b4-113">**Gateway locale** -se uno o più origini dati locali nella rete dell'organizzazione, è necessario tooinstall un [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="867b4-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="867b4-114">gateway di Hello è necessario per il server nel cloud hello connettersi tooyour locale origini tooprocess e l'aggiornamento dati nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="867b4-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="867b4-115">Prima di distribuire, assicurarsi che è possibile elaborare dati hello nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="867b4-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="867b4-116">In SSDT fare clic su **Modello** > **Elabora** > **Elabora tutto**.</span><span class="sxs-lookup"><span data-stu-id="867b4-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="867b4-117">Se l'elaborazione ha esito negativo, la distribuzione non potrà essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="867b4-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="867b4-118">toodeploy un modello tabulare in SSDT</span><span class="sxs-lookup"><span data-stu-id="867b4-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="867b4-119">Prima di distribuire, è necessario il nome di server hello tooget.</span><span class="sxs-lookup"><span data-stu-id="867b4-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="867b4-120">In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server hello copia.</span><span class="sxs-lookup"><span data-stu-id="867b4-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="867b4-122">In SSDT > **Esplora**, progetto hello rapida > **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="867b4-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="867b4-123">Quindi nel **distribuzione** > **Server** incollare il nome di server hello.</span><span class="sxs-lookup"><span data-stu-id="867b4-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Incollare il nome del server nelle proprietà del server di distribuzione](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="867b4-125">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Proprietà** e quindi scegliere **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="867b4-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="867b4-126">Potrebbe essere richiesta toosign in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="867b4-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Distribuire tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="867b4-128">Nella finestra di Output sia hello e distribuzione, verrà visualizzato lo stato di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="867b4-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Stato della distribuzione](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="867b4-130">Questo è tutto è tooit!</span><span class="sxs-lookup"><span data-stu-id="867b4-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="867b4-131">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="867b4-131">Troubleshooting</span></span>
<span data-ttu-id="867b4-132">Se la distribuzione non riesce durante la distribuzione dei metadati, è probabile perché SSDT non riesce a connettersi tooyour server.</span><span class="sxs-lookup"><span data-stu-id="867b4-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="867b4-133">Verificare che è possibile connettere il server tooyour tramite SSMS.</span><span class="sxs-lookup"><span data-stu-id="867b4-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="867b4-134">Verificare quindi la proprietà Server di distribuzione per il progetto hello hello sia corretto.</span><span class="sxs-lookup"><span data-stu-id="867b4-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="867b4-135">Se la distribuzione non riesce in una tabella, è probabile perché il server non è stato possibile connettersi tooa origine dei dati.</span><span class="sxs-lookup"><span data-stu-id="867b4-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="867b4-136">Se l'origine dati locale nella rete dell'organizzazione, tooinstall assicurarsi di essere un [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="867b4-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="867b4-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="867b4-137">Next steps</span></span>
<span data-ttu-id="867b4-138">Dopo aver creato il server di modello tabulare distribuito tooyour, si è pronti tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="867b4-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="867b4-139">È possibile [connettersi tooit con SSMS](analysis-services-manage.md) toomanage è.</span><span class="sxs-lookup"><span data-stu-id="867b4-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="867b4-140">E, è possibile [tooit utilizzando uno strumento client di connettersi](analysis-services-connect.md) come Power BI, Power BI Desktop o Excel e avviare la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="867b4-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

