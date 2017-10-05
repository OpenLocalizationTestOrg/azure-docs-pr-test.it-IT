---
ms.assetid: 
title: Guida alla limitazione delle richieste per Azure Key Vault | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="1bfda-102">Guida alla limitazione delle richieste per Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1bfda-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="1bfda-103">La limitazione delle richieste è un processo che consente di limitare il numero di chiamate simultanee al servizio di Azure per prevenire l'uso eccessivo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="1bfda-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="1bfda-104">Azure Key Vault è progettato per gestire un volume di richieste elevato.</span><span class="sxs-lookup"><span data-stu-id="1bfda-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="1bfda-105">In caso di un numero eccessivamente elevato di richieste, la limitazione delle richieste del client aiuta a mantenere le prestazioni ottimali e l'affidabilità del servizio di Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1bfda-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="1bfda-106">I limiti delle richieste variano in base allo scenario.</span><span class="sxs-lookup"><span data-stu-id="1bfda-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="1bfda-107">Ad esempio, se si esegue un volume elevato di operazioni di scrittura, la possibilità di limitare le richieste è maggiore rispetto a quando si eseguono solo operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="1bfda-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="1bfda-108">Gestione dei limiti da parte di Key Vault</span><span class="sxs-lookup"><span data-stu-id="1bfda-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="1bfda-109">I limiti del servizio in Key Vault hanno lo scopo di evitare un uso improprio delle risorse e garantire la qualità del servizio per tutti i client di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1bfda-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="1bfda-110">Quando si supera la soglia di un servizio, Key Vault limita le nuove richieste del client per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="1bfda-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="1bfda-111">In questo caso, Key Vault restituisce il codice di stato HTTP 429, ovvero Too many requests (Numero di richieste eccessivo), e le richieste hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1bfda-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="1bfda-112">Inoltre, le richieste non riuscite che restituiscono un codice 429 valgono per le limitazioni tracciate da Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1bfda-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="1bfda-113">Nel caso l'utente abbia delle esigenze aziendali per cui sono necessarie delle limitazioni maggiori, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1bfda-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="1bfda-114">Come limitare le richieste per l'app in risposta ai limiti del servizio</span><span class="sxs-lookup"><span data-stu-id="1bfda-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="1bfda-115">Di seguito sono riportate le **pratiche ottimali** per la limitazione delle richieste per l'app:</span><span class="sxs-lookup"><span data-stu-id="1bfda-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="1bfda-116">Ridurre il numero di operazioni per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="1bfda-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="1bfda-117">Ridurre la frequenza delle richieste.</span><span class="sxs-lookup"><span data-stu-id="1bfda-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="1bfda-118">Evitare tentativi immediati.</span><span class="sxs-lookup"><span data-stu-id="1bfda-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="1bfda-119">Tutte le richieste si accumulano per i limiti di consumo.</span><span class="sxs-lookup"><span data-stu-id="1bfda-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="1bfda-120">Quando si implementa la gestione degli errori dell'app, usare il codice di errore HTTP 429 per rilevare la necessità di limitazione delle richieste lato client.</span><span class="sxs-lookup"><span data-stu-id="1bfda-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="1bfda-121">Se la richiesta ha di nuovo esito negativo con un codice di errore HTTP 429, vuol dire che ci sono ancora limiti nel servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfda-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="1bfda-122">Continuare a usare il metodo di limitazione delle richieste lato client consigliato, provando a inviare nuovamente la richiesta fino a quando non ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="1bfda-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="1bfda-123">Metodo consigliato per la limitazione delle richieste lato client</span><span class="sxs-lookup"><span data-stu-id="1bfda-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="1bfda-124">Quando si genera il codice di errore HTTP 429, iniziare a limitare le richieste del client con un approccio di backoff esponenziale:</span><span class="sxs-lookup"><span data-stu-id="1bfda-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="1bfda-125">Attendere 1 secondo e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="1bfda-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="1bfda-126">Se viene ancora limitata, attendere 2 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="1bfda-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="1bfda-127">Se viene ancora limitata, attendere 4 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="1bfda-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="1bfda-128">Se viene ancora limitata, attendere 8 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="1bfda-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="1bfda-129">Se viene ancora limitata, attendere 16 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="1bfda-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="1bfda-130">A questo punto, il codice di risposta HTTP 429 dovrebbe non essere più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="1bfda-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="1bfda-131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1bfda-131">See also</span></span>

<span data-ttu-id="1bfda-132">Per un approfondimento sulla limitazione delle richieste nel cloud di Microsoft, vedere [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling) (Modello di limitazione delle richieste).</span><span class="sxs-lookup"><span data-stu-id="1bfda-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

