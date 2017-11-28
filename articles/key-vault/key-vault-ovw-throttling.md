---
ms.assetid: 
title: Guida di limitazione delle richieste di insieme di credenziali chiave aaaAzure | Documenti Microsoft
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="c0ecf-102">Guida alla limitazione delle richieste per Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c0ecf-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="c0ecf-103">La limitazione delle richieste è un processo si avvia che limita il numero di hello di chiamate simultanee toohello servizio Azure tooprevent utilizzo eccessivo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="c0ecf-104">Insieme di credenziali di chiave di Azure (insieme) è progettata toohandle un volume elevato di richieste.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="c0ecf-105">Se si verifica un numero eccessivo di richieste, la limitazione delle richieste del client consente di garantire prestazioni ottimali e l'affidabilità del servizio AKV hello.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="c0ecf-106">I limiti di limitazione delle richieste variano in base uno scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="c0ecf-107">Ad esempio, se si sta eseguendo un volume elevato di operazioni di scrittura, il possibilità hello di limitazione delle richieste è maggiore se si eseguono solo letture.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="c0ecf-108">Gestione dei limiti da parte di Key Vault</span><span class="sxs-lookup"><span data-stu-id="c0ecf-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="c0ecf-109">Limiti dei servizi nell'insieme di credenziali chiave sono presenti un utilizzo improprio tooprevent delle risorse e assicurare la qualità del servizio per tutti i client dell'insieme di credenziali di chiave.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="c0ecf-110">Quando si supera la soglia di un servizio, Key Vault limita le nuove richieste del client per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="c0ecf-111">In questo caso, l'insieme di credenziali chiave restituisce il codice di stato HTTP 429 (eccessivo numero di richieste), e di errore delle richieste hello.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="c0ecf-112">Inoltre, non è stato possibile richieste che restituiscono un conteggio 429 verso i limiti di velocità hello monitorate dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="c0ecf-113">Nel caso l'utente abbia delle esigenze aziendali per cui sono necessarie delle limitazioni maggiori, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="c0ecf-114">Come toothrottle l'applicazione in risposta tooservice limita</span><span class="sxs-lookup"><span data-stu-id="c0ecf-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="c0ecf-115">Hello di seguito sono **consigliate** per la limitazione dell'app:</span><span class="sxs-lookup"><span data-stu-id="c0ecf-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="c0ecf-116">Ridurre il numero di hello delle operazioni per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="c0ecf-117">Ridurre la frequenza hello delle richieste.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="c0ecf-118">Evitare tentativi immediati.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="c0ecf-119">Tutte le richieste si accumulano per i limiti di consumo.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="c0ecf-120">Quando si implementa la gestione degli errori dell'applicazione, utilizzare hello HTTP Errore codice 429 toodetect hello necessario per la limitazione sul lato client.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="c0ecf-121">Se è richiesta hello ha nuovamente esito negativo con un codice di errore HTTP 429, continuano a verificarsi il limite di un servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="c0ecf-122">Continuare toouse hello consigliato metodo limitazione sul lato client, nuovo tentativo di richiesta di hello fino al completamento.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="c0ecf-123">Metodo consigliato per la limitazione delle richieste lato client</span><span class="sxs-lookup"><span data-stu-id="c0ecf-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="c0ecf-124">Quando si genera il codice di errore HTTP 429, iniziare a limitare le richieste del client con un approccio di backoff esponenziale:</span><span class="sxs-lookup"><span data-stu-id="c0ecf-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="c0ecf-125">Attendere 1 secondo e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="c0ecf-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="c0ecf-126">Se viene ancora limitata, attendere 2 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="c0ecf-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="c0ecf-127">Se viene ancora limitata, attendere 4 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="c0ecf-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="c0ecf-128">Se viene ancora limitata, attendere 8 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="c0ecf-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="c0ecf-129">Se viene ancora limitata, attendere 16 secondi e ripetere la richiesta</span><span class="sxs-lookup"><span data-stu-id="c0ecf-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="c0ecf-130">A questo punto, il codice di risposta HTTP 429 dovrebbe non essere più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c0ecf-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0ecf-131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c0ecf-131">See also</span></span>

<span data-ttu-id="c0ecf-132">Per un orientamento più approfondito della limitazione delle richieste in hello Cloud Microsoft, vedere [limitazione modello](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="c0ecf-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

