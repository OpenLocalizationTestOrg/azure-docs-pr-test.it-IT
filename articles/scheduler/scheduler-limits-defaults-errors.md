---
title: aaaScheduler limiti e i valori predefiniti
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
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="45e05-103">Limiti e impostazioni predefinite dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="45e05-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="45e05-104">Quote, limiti, impostazioni predefinite e limiti dell'utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="45e05-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="45e05-105">Hello x-ms-request-id intestazione</span><span class="sxs-lookup"><span data-stu-id="45e05-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="45e05-106">Ogni richiesta effettuata hello servizio Utilità di pianificazione restituisce un'intestazione di risposta denominata**x-ms-request-id**. Questa intestazione contiene un valore opaco che identifica in modo univoco la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="45e05-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="45e05-107">Se una richiesta è costantemente esito negativo e si sono verificate che hello corretta formulazione è, è possibile utilizzare questo errore tooMicrosoft di valore tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="45e05-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="45e05-108">Nel report, includere il valore di hello di x-ms-request-id, hello ora approssimativa in cui è stata effettuata la richiesta di hello, hello identificatore di sottoscrizione hello, raccolta di processi e/o processo e tipo di operazione hello richiesta ha tentato di hello.</span><span class="sxs-lookup"><span data-stu-id="45e05-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="45e05-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="45e05-109">See Also</span></span>
 [<span data-ttu-id="45e05-110">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="45e05-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="45e05-111">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="45e05-112">Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="45e05-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="45e05-113">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="45e05-114">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="45e05-115">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="45e05-116">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="45e05-117">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45e05-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

