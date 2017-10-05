---
title: Limitazione avanzata delle richieste con Gestione API di Azure
description: Informazioni su come creare e applicare criteri flessibili di limitazione della frequenza e della quota con Gestione API di Azure.
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="f5f19-103">Limitazione avanzata delle richieste con Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f5f19-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="f5f19-104">La possibilità di limitare le richieste in ingresso è uno dei ruoli fondamentali di Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f19-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="f5f19-105">Tramite il controllo della frequenza delle richieste o del totale delle richieste o dei dati trasferiti, Gestione API consente ai provider di API di proteggere le API da abusi e di aggiungere valore a diversi livelli di prodotto API.</span><span class="sxs-lookup"><span data-stu-id="f5f19-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="f5f19-106">Limitazione basata sul prodotto</span><span class="sxs-lookup"><span data-stu-id="f5f19-106">Product based throttling</span></span>
<span data-ttu-id="f5f19-107">Finora le funzionalità di limitazione della frequenza avevano come ambito una sottoscrizione specifica a un prodotto (essenzialmente una chiave), definita nel portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f5f19-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="f5f19-108">Tali funzionalità sono utili per consentire al provider di API di applicare limiti agli sviluppatori che si sono registrati per l'uso dell'API, ma non consente di limitare ad esempio i singoli utenti finali dell'API.</span><span class="sxs-lookup"><span data-stu-id="f5f19-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="f5f19-109">Il singolo utente dell'applicazione dello sviluppatore può usare l'intera quota e quindi impedire ad altri clienti dello sviluppatore di usare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5f19-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="f5f19-110">Inoltre, alcuni clienti possono generare un numero elevato di richieste, limitando l'accesso agli utenti occasionali.</span><span class="sxs-lookup"><span data-stu-id="f5f19-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="f5f19-111">Limitazione basata su chiave personalizzata</span><span class="sxs-lookup"><span data-stu-id="f5f19-111">Custom key based throttling</span></span>
<span data-ttu-id="f5f19-112">I nuovi criteri [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) offrono una soluzione molto più flessibile per il controllo del traffico.</span><span class="sxs-lookup"><span data-stu-id="f5f19-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="f5f19-113">Questi nuovi criteri consentono di definire le espressioni per l'identificazione delle chiavi che verranno usate per tenere traccia dell'utilizzo del traffico.</span><span class="sxs-lookup"><span data-stu-id="f5f19-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="f5f19-114">Il modo più semplice per spiegarne il funzionamento è illustrare un esempio.</span><span class="sxs-lookup"><span data-stu-id="f5f19-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="f5f19-115">Limitazione dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="f5f19-115">IP Address throttling</span></span>
<span data-ttu-id="f5f19-116">I seguenti criteri limitano l'indirizzo IP di un singolo client a 10 chiamate al minuto, con un totale di 1.000.000 chiamate e 10.000 KB di larghezza di banda al mese.</span><span class="sxs-lookup"><span data-stu-id="f5f19-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="f5f19-117">Se tutti i client su Internet usassero un indirizzo IP univoco, sarebbe un metodo efficace per limitare l'utilizzo per utente.</span><span class="sxs-lookup"><span data-stu-id="f5f19-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="f5f19-118">È tuttavia molto probabile che più utenti condividano un singolo indirizzo IP pubblico, in quanto accedono a Internet tramite un dispositivo NAT.</span><span class="sxs-lookup"><span data-stu-id="f5f19-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="f5f19-119">Nonostante ciò, per le API che consentono l'accesso non autenticato, `IpAddress` può essere la soluzione migliore.</span><span class="sxs-lookup"><span data-stu-id="f5f19-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="f5f19-120">Limitazione dell'identità utente</span><span class="sxs-lookup"><span data-stu-id="f5f19-120">User identity throttling</span></span>
<span data-ttu-id="f5f19-121">Se un utente finale viene autenticato, può essere generata una chiave per la limitazione delle richieste in base alle informazioni che identificano in modo univoco l'utente.</span><span class="sxs-lookup"><span data-stu-id="f5f19-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="f5f19-122">In questo esempio si estrae l'intestazione dell'autorizzazione, la si converte in un oggetto `JWT` e si usa l'oggetto del token per identificare l'utente e usarlo come chiave per la limitazione della frequenza.</span><span class="sxs-lookup"><span data-stu-id="f5f19-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="f5f19-123">Se l'identità dell'utente è archiviata nell'oggetto `JWT` come una delle altre attestazioni, è possibile sostituirla con quel valore.</span><span class="sxs-lookup"><span data-stu-id="f5f19-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="f5f19-124">Criteri combinati</span><span class="sxs-lookup"><span data-stu-id="f5f19-124">Combined policies</span></span>
<span data-ttu-id="f5f19-125">Sebbene i nuovi criteri di limitazione garantiscano maggiore controllo rispetto ai criteri di limitazione esistenti, la combinazione delle due funzionalità presenta comunque dei vantaggi.</span><span class="sxs-lookup"><span data-stu-id="f5f19-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="f5f19-126">La limitazione per chiave di sottoscrizione del prodotto ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) (Limitare la frequenza delle chiamate per sottoscrizione) e [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) (Impostare la quota di utilizzo per sottoscrizione)) è un ottimo metodo per monetizzare un'API effettuando gli addebiti in base ai livelli di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="f5f19-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="f5f19-127">Il controllo con granularità maggiore per impostare la limitazione per utente è complementare e impedisce che il comportamento di un utente comprometta l'esperienza di un altro utente.</span><span class="sxs-lookup"><span data-stu-id="f5f19-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="f5f19-128">Limitazione basata su client</span><span class="sxs-lookup"><span data-stu-id="f5f19-128">Client driven throttling</span></span>
<span data-ttu-id="f5f19-129">Quando la chiave per la limitazione viene definita mediante un' [espressione di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx), è il provider di API a scegliere l'ambito della limitazione.</span><span class="sxs-lookup"><span data-stu-id="f5f19-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="f5f19-130">Uno sviluppatore può tuttavia voler controllare la modalità di limitazione della frequenza per i propri clienti.</span><span class="sxs-lookup"><span data-stu-id="f5f19-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="f5f19-131">Il provider di API può abilitare questa opzione introducendo un'intestazione personalizzata per consentire all'applicazione client dello sviluppatore di comunicare la chiave all'API.</span><span class="sxs-lookup"><span data-stu-id="f5f19-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="f5f19-132">In questo modo l'applicazione client dello sviluppatore è in grado di scegliere la modalità di creazione della chiave di limitazione della frequenza.</span><span class="sxs-lookup"><span data-stu-id="f5f19-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="f5f19-133">Con un po' di astuzia, uno sviluppatore di client può creare i propri livelli di frequenza allocando set di chiavi agli utenti e ruotando l'utilizzo delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="f5f19-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="f5f19-134">Summary</span><span class="sxs-lookup"><span data-stu-id="f5f19-134">Summary</span></span>
<span data-ttu-id="f5f19-135">Gestione API di Azure offre funzionalità di limitazione della frequenza e della quota per proteggere e aggiungere valore al proprio servizio API.</span><span class="sxs-lookup"><span data-stu-id="f5f19-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="f5f19-136">I nuovi criteri di limitazione con regole personalizzate di definizione dell'ambito consentono di controllare con granularità maggiore tali criteri per consentire ai clienti di creare applicazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="f5f19-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="f5f19-137">Gli esempi in questo articolo illustrano l'uso di questi nuovi criteri tramite la produzione di chiavi per la limitazione della frequenza con gli indirizzi IP del client, l'identità dell'utente e valori generati dal client.</span><span class="sxs-lookup"><span data-stu-id="f5f19-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="f5f19-138">È tuttavia possibile usare molte altre parti del messaggio, ad esempio l'agente utente, frammenti del percorso dell'URL e la dimensione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="f5f19-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f19-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5f19-139">Next steps</span></span>
<span data-ttu-id="f5f19-140">È possibile inserire commenti e suggerimenti per questo argomento nel thread Disqus.</span><span class="sxs-lookup"><span data-stu-id="f5f19-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="f5f19-141">Può essere utile individuare altri potenziali valori di chiave che sono utili negli scenari in uso.</span><span class="sxs-lookup"><span data-stu-id="f5f19-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="f5f19-142">Video contenente una panoramica di questi criteri</span><span class="sxs-lookup"><span data-stu-id="f5f19-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="f5f19-143">Per altre informazioni sui criteri [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) descritti in questo articolo, guardare il video seguente.</span><span class="sxs-lookup"><span data-stu-id="f5f19-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

