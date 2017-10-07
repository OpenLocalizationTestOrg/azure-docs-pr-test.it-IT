---
title: aaaConnect tooAzure Analysis Services con Power BI | Documenti Microsoft
description: Informazioni su come tooconnect tooan Azure Analysis Services server tramite Power BI.
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="7a8d8-103">Connettersi con Power BI</span><span class="sxs-lookup"><span data-stu-id="7a8d8-103">Connect with Power BI</span></span>

<span data-ttu-id="7a8d8-104">Dopo avere creato un server in Azure e distribuiti tooit un modello tabulare, gli utenti dell'organizzazione tooconnect pronto e iniziano l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="7a8d8-105">Essere certi toouse hello versione [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="7a8d8-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="7a8d8-106">Connettersi in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7a8d8-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="7a8d8-107">In Power BI Desktop fare clic su **Recupera dati** > **Azure** > **Database di Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="7a8d8-108">In **Server**, immettere il nome di server hello.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="7a8d8-109">Essere l'URL completo che tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="7a8d8-110">Ad esempio, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="7a8d8-111">In **Database**, se si conosce il nome di hello del database modello tabulare hello o una prospettiva si desidera tooconnect per incollarlo qui.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="7a8d8-112">In caso contrario, è possibile lasciare vuoto questo campo e selezionare un database o una prospettiva in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="7a8d8-113">Lasciare l'impostazione predefinita hello **connessione in tempo reale** opzione, quindi premere **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="7a8d8-114">Immettere le credenziali di accesso, se richieste.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="7a8d8-115">In **Navigator**, espandere server hello, quindi selezionare il modello di hello o una prospettiva che si desidera tooconnect su, quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="7a8d8-116">Fare clic su un modello o della prospettiva di tooshow tutti gli oggetti di hello per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="7a8d8-117">modello di Hello viene visualizzato in Power BI Desktop con un report vuoto nella visualizzazione di Report.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="7a8d8-118">elenco di campi Hello Visualizza tutti gli oggetti modello non nascosto.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="7a8d8-119">Stato di connessione viene visualizzato nell'angolo inferiore destro hello.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="7a8d8-120">Connettersi in Power BI (servizio)</span><span class="sxs-lookup"><span data-stu-id="7a8d8-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="7a8d8-121">Creare un file di Power BI Desktop che dispone di un modello di connessione in tempo reale tooyour sul server.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="7a8d8-122">In [Power BI](https://powerbi.microsoft.com) fare clic su **Recupera dati** > **File**.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="7a8d8-123">Individuare e selezionare il file.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="7a8d8-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7a8d8-124">See also</span></span>
<span data-ttu-id="7a8d8-125">[Connettersi tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="7a8d8-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="7a8d8-126">Librerie client</span><span class="sxs-lookup"><span data-stu-id="7a8d8-126">Client libraries</span></span>](analysis-services-data-providers.md)

