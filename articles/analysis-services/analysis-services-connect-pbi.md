---
title: Connettersi ad Azure Analysis Services con Power BI | Microsoft Docs
description: Informazioni su come connettersi a un server di Azure Analysis Services usando Power BI.
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="75d22-103">Connettersi con Power BI</span><span class="sxs-lookup"><span data-stu-id="75d22-103">Connect with Power BI</span></span>

<span data-ttu-id="75d22-104">Dopo aver creato un server in Azure e aver distribuito un modello tabulare nel server, gli utenti dell'organizzazione sono pronti per connettersi e iniziare l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="75d22-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="75d22-105">Assicurarsi di usare la versione più recente di [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="75d22-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="75d22-106">Connettersi in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="75d22-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="75d22-107">In Power BI Desktop fare clic su **Recupera dati** > **Azure** > **Database di Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="75d22-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="75d22-108">In **Server** immettere il nome del server.</span><span class="sxs-lookup"><span data-stu-id="75d22-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="75d22-109">Assicurarsi di includere l'URL completo.</span><span class="sxs-lookup"><span data-stu-id="75d22-109">Be sure to include the full URL.</span></span> <span data-ttu-id="75d22-110">Ad esempio, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="75d22-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="75d22-111">In **Database**, se si conosce il nome della prospettiva o del database del modello tabulare a cui connettersi, incollarlo qui.</span><span class="sxs-lookup"><span data-stu-id="75d22-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="75d22-112">In caso contrario, è possibile lasciare vuoto questo campo e selezionare un database o una prospettiva in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="75d22-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="75d22-113">Lasciare l'impostazione predefinita dell'opzione **Connessione dinamica** e quindi scegliere **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="75d22-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="75d22-114">Immettere le credenziali di accesso, se richieste.</span><span class="sxs-lookup"><span data-stu-id="75d22-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="75d22-115">In **Strumento di navigazione** espandere il server, selezionare il modello o la prospettiva a cui connettersi e quindi fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="75d22-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="75d22-116">Fare clic su un modello o su una prospettiva per visualizzare tutti gli oggetti per la vista selezionata.</span><span class="sxs-lookup"><span data-stu-id="75d22-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="75d22-117">Il modello viene aperto in Power BI Desktop con un report vuoto nella vista Report.</span><span class="sxs-lookup"><span data-stu-id="75d22-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="75d22-118">L'elenco Campi consente di visualizzare tutti gli oggetti modello non nascosti.</span><span class="sxs-lookup"><span data-stu-id="75d22-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="75d22-119">Lo stato della connessione viene visualizzato nell'angolo in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="75d22-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="75d22-120">Connettersi in Power BI (servizio)</span><span class="sxs-lookup"><span data-stu-id="75d22-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="75d22-121">Creare un file di Power BI Desktop che dispone di una connessione dinamica al modello sul server.</span><span class="sxs-lookup"><span data-stu-id="75d22-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="75d22-122">In [Power BI](https://powerbi.microsoft.com) fare clic su **Recupera dati** > **File**.</span><span class="sxs-lookup"><span data-stu-id="75d22-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="75d22-123">Individuare e selezionare il file.</span><span class="sxs-lookup"><span data-stu-id="75d22-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="75d22-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75d22-124">See also</span></span>
<span data-ttu-id="75d22-125">[Connettersi ad Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="75d22-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="75d22-126">Librerie client</span><span class="sxs-lookup"><span data-stu-id="75d22-126">Client libraries</span></span>](analysis-services-data-providers.md)

