---
title: librerie aaaClient necessarie per la connessione di Analysis Services di tooAzure | Documenti Microsoft
description: Descrive le librerie client necessarie per client tooconnect di strumenti e applicazioni Azure Analysis Services
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="991e2-103">Librerie client per la connessione tooAzure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="991e2-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="991e2-104">Le librerie client sono necessari per le applicazioni client e server di servizi tooAnalysis tooconnect strumenti.</span><span class="sxs-lookup"><span data-stu-id="991e2-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="991e2-105">Analysis Services usa tre librerie client.</span><span class="sxs-lookup"><span data-stu-id="991e2-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="991e2-106">ADOMD.NET e Analysis Services Management Objects (AMO) sono librerie client gestite.</span><span class="sxs-lookup"><span data-stu-id="991e2-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="991e2-107">provider OLE DB per Analysis Services Hello (MSOLAP DLL) è una libreria client nativa.</span><span class="sxs-lookup"><span data-stu-id="991e2-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="991e2-108">In genere, in cui sono installati tutti e tre in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="991e2-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="991e2-109">Azure Analysis Services richiede versioni più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="991e2-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="991e2-110">Le applicazioni client di Microsoft, come ad esempio Power BI Desktop ed Excel, installano tutte e tre le librerie client.</span><span class="sxs-lookup"><span data-stu-id="991e2-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="991e2-111">Tuttavia, a seconda della versione di hello o frequenza degli aggiornamenti, le librerie client potrebbero non essere versioni più recenti di hello richieste da Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="991e2-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="991e2-112">Hello vale toocustom applicazioni o altre interfacce, ad esempio AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="991e2-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="991e2-113">Queste applicazioni richiedono l'installazione manuale di librerie hello.</span><span class="sxs-lookup"><span data-stu-id="991e2-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="991e2-114">le librerie client Hello per l'installazione manuale sono inclusi nel feature pack di SQL Server come pacchetti distribuibili.</span><span class="sxs-lookup"><span data-stu-id="991e2-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="991e2-115">Tuttavia, le librerie client sono toohello legati versione di SQL Server e hello potrebbero non essere più recente.</span><span class="sxs-lookup"><span data-stu-id="991e2-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="991e2-116">Le librerie client per le connessioni client sono diverse dalle tooconnect necessari i provider di dati da un'origine di dati tooa server Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="991e2-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="991e2-117">toolearn più sulle connessioni di origine dati, vedere [connessioni origine dati](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="991e2-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="991e2-118">Scaricare le librerie client più recente di hello</span><span class="sxs-lookup"><span data-stu-id="991e2-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="991e2-119">Utilizzare hello seguendo le librerie client se si dispone di un ambiente di produzione e richiedono versioni completamente rilasciate e supportate.</span><span class="sxs-lookup"><span data-stu-id="991e2-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="991e2-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="991e2-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="991e2-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="991e2-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="991e2-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="991e2-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="991e2-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="991e2-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="991e2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="991e2-124">Next steps</span></span>
<span data-ttu-id="991e2-125">[Connettersi con Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="991e2-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="991e2-126">Stabilire la connessione con Power BI</span><span class="sxs-lookup"><span data-stu-id="991e2-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
