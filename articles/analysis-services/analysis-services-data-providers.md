---
title: Librerie client necessarie per la connessione ad Azure Analysis Services | Microsoft Docs
description: Vengono illustrate le librerie client necessarie per la connessione di applicazioni e strumenti client ad Azure Analysis Services
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
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="babf9-103">Librerie client per la connessione ad Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="babf9-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="babf9-104">Le librerie client sono necessarie per la connessione di applicazioni e strumenti client ai server di Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="babf9-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="babf9-105">Analysis Services usa tre librerie client.</span><span class="sxs-lookup"><span data-stu-id="babf9-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="babf9-106">ADOMD.NET e Analysis Services Management Objects (AMO) sono librerie client gestite.</span><span class="sxs-lookup"><span data-stu-id="babf9-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="babf9-107">Il provider Analysis Services OLE DB (MSOLAP DLL) è una libreria client nativa.</span><span class="sxs-lookup"><span data-stu-id="babf9-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="babf9-108">In genere, vengono installate tutte e tre nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="babf9-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="babf9-109">Azure Analysis Services richiede le versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="babf9-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="babf9-110">Le applicazioni client di Microsoft, come ad esempio Power BI Desktop ed Excel, installano tutte e tre le librerie client.</span><span class="sxs-lookup"><span data-stu-id="babf9-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="babf9-111">A seconda della versione o della frequenza degli aggiornamenti, le librerie client potrebbero tuttavia non essere le versioni più recenti richieste da Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="babf9-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="babf9-112">Lo stesso vale per le applicazioni personalizzate o per le altre interfacce come AsCmd, TOM e ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="babf9-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="babf9-113">Queste applicazioni richiedono l'installazione manuale delle librerie.</span><span class="sxs-lookup"><span data-stu-id="babf9-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="babf9-114">Le librerie client per l'installazione manuale sono incluse nei Feature Pack di SQL Server come pacchetti distribuibili.</span><span class="sxs-lookup"><span data-stu-id="babf9-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="babf9-115">Queste librerie client sono tuttavia collegate alla versione di SQL Server e potrebbero non essere le più recenti.</span><span class="sxs-lookup"><span data-stu-id="babf9-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="babf9-116">Le librerie client per le connessioni client sono diverse dai provider di dati necessari per connettersi da un server di Azure Analysis Services a un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="babf9-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="babf9-117">Per ulteriori informazioni sulle connessioni alle origini dati, vedere [Connessioni alle origini dati](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="babf9-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="babf9-118">Scaricare le librerie client più recenti</span><span class="sxs-lookup"><span data-stu-id="babf9-118">Download the latest client libraries</span></span>  
<span data-ttu-id="babf9-119">Usare le librerie client seguenti se ci si trova in un ambiente di produzione e sono richieste versioni completamente rilasciate e supportate.</span><span class="sxs-lookup"><span data-stu-id="babf9-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="babf9-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="babf9-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="babf9-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="babf9-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="babf9-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="babf9-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="babf9-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="babf9-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="babf9-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="babf9-124">Next steps</span></span>
<span data-ttu-id="babf9-125">[Connettersi con Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="babf9-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="babf9-126">Stabilire la connessione con Power BI</span><span class="sxs-lookup"><span data-stu-id="babf9-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
