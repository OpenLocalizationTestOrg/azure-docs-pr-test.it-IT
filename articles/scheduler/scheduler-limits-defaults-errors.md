---
title: "Limiti e impostazioni predefinite dell'Utilità di pianificazione"
description: "Limiti e impostazioni predefinite dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="d9658-103">Limiti e impostazioni predefinite dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="d9658-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="d9658-104">Quote, limiti, impostazioni predefinite e limiti dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="d9658-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="d9658-105">L'intestazione x-ms-request-id</span><span class="sxs-lookup"><span data-stu-id="d9658-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="d9658-106">Ogni richiesta effettuata per il servizio dell’Utilità di pianificazione restituisce un'intestazione di risposta denominata**x-ms-request-id**.</span><span class="sxs-lookup"><span data-stu-id="d9658-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="d9658-107">Questa intestazione contiene un valore opaco che identifica in modo univoco la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d9658-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="d9658-108">Se una richiesta fallisce sistematicamente e si è verificato che la richiesta è formulata in modo appropriato, si può usare questo valore per riportare l'errore a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d9658-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="d9658-109">Nel report includere il valore di x-ms-request-id, l'ora approssimativa in cui è stata eseguita la richiesta, l'identificativo della sottoscrizione, la raccolta processi e/o il processo e il tipo di operazione tentata con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d9658-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="d9658-110">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d9658-110">See Also</span></span>
 [<span data-ttu-id="d9658-111">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="d9658-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="d9658-112">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d9658-113">Introduzione all'uso dell'Utilità di pianificazione di Azure nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d9658-114">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d9658-115">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d9658-116">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d9658-117">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d9658-118">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9658-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

