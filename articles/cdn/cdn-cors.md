---
title: Uso della rete CDN di Azure con CORS | Documentazione Microsoft
description: Informazioni su come usare la rete per la distribuzione di contenuti (rete CDN) di Azure con CORS (Cross-Origin Resource Sharing).
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="a4387-103">Uso della rete CDN di Azure con CORS</span><span class="sxs-lookup"><span data-stu-id="a4387-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="a4387-104">Informazioni su CORS</span><span class="sxs-lookup"><span data-stu-id="a4387-104">What is CORS?</span></span>
<span data-ttu-id="a4387-105">CORS (Cross Origin Resource Sharing) è una funzionalità HTTP che consente a un'applicazione Web in esecuzione in un dominio di accedere alle risorse in un altro dominio.</span><span class="sxs-lookup"><span data-stu-id="a4387-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="a4387-106">Per ridurre il rischio di attacchi tramite script da altri siti, tutti i Web browser moderni implementano una restrizione di sicurezza nota come [regola della stessa origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="a4387-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="a4387-107">Questo impedisce a una pagina Web di chiamare le API in un dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="a4387-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="a4387-108">CORS offre un modo sicuro per consentire a una origine, ovvero il dominio di origine, di chiamare le API in un'altra origine.</span><span class="sxs-lookup"><span data-stu-id="a4387-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a4387-109">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="a4387-109">How it works</span></span>
<span data-ttu-id="a4387-110">Esistono due tipi di richieste CORS, le *richieste semplici* e le *richieste complesse*.</span><span class="sxs-lookup"><span data-stu-id="a4387-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="a4387-111">Per le richieste semplici:</span><span class="sxs-lookup"><span data-stu-id="a4387-111">For simple requests:</span></span>

1. <span data-ttu-id="a4387-112">Il browser invia la richiesta CORS con un'ulteriore intestazione della richiesta HTTP **Origin**.</span><span class="sxs-lookup"><span data-stu-id="a4387-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="a4387-113">Il valore di questa intestazione è l'origine che ha gestito la pagina padre, definita come la combinazione di *protocollo*, *dominio* e *porta*.</span><span class="sxs-lookup"><span data-stu-id="a4387-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="a4387-114">Quando una pagina prova ad accedere da https://www.contoso.com ai dati di un utente nell'origine fabrikam.com, a tale sito viene inviata l'intestazione di richiesta seguente:</span><span class="sxs-lookup"><span data-stu-id="a4387-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="a4387-115">Il server può rispondere con uno degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4387-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="a4387-116">Un'intestazione **Access-Control-Allow-Origin** presente nella risposta, per indicare il sito di origine consentito.</span><span class="sxs-lookup"><span data-stu-id="a4387-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="a4387-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a4387-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="a4387-118">Un codice di errore HTTP, ad esempio 403, se il server non consente la richiesta multiorigine dopo il controllo dell'intestazione Origin.</span><span class="sxs-lookup"><span data-stu-id="a4387-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="a4387-119">Un'intestazione **Access-Control-Allow-Origin** con un carattere jolly che consente tutte le origini:</span><span class="sxs-lookup"><span data-stu-id="a4387-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="a4387-120">Per le richieste complesse:</span><span class="sxs-lookup"><span data-stu-id="a4387-120">For complex requests:</span></span>

<span data-ttu-id="a4387-121">Una richiesta complessa è una richiesta CORS in cui il browser deve inviare una *richiesta preliminare*, ovvero un probe preliminare, prima di inviare la richiesta CORS effettiva.</span><span class="sxs-lookup"><span data-stu-id="a4387-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="a4387-122">La richiesta preliminare chiede l'autorizzazione del server perché la richiesta CORS originale possa procedere e si tratta di una richiesta `OPTIONS` allo stesso URL.</span><span class="sxs-lookup"><span data-stu-id="a4387-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="a4387-123">Per altre informazioni sui flussi CORS e i problemi comuni, vedere [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/) (Guida di CORS per le API REST).</span><span class="sxs-lookup"><span data-stu-id="a4387-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="a4387-124">Scenari con caratteri jolly o singola origine</span><span class="sxs-lookup"><span data-stu-id="a4387-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="a4387-125">La condivisione CORS sulla rete CDN di Azure funzionerà automaticamente senza operazioni di configurazione aggiuntive quando l'intestazione **Access-Control-Allow-Origin** è impostata sul carattere jolly asterisco (*) o su una singola origine.</span><span class="sxs-lookup"><span data-stu-id="a4387-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="a4387-126">La rete CDN memorizzerà nella cache la prima risposta e le richieste successive useranno la stessa intestazione.</span><span class="sxs-lookup"><span data-stu-id="a4387-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="a4387-127">Se sono state inviate richieste alla rete CDN prima che la condivisione CORS venisse impostata nell'origine, sarà necessario eliminare il contenuto sull'endpoint e ricaricarlo con l'intestazione **Access-Control-Allow-Origin** .</span><span class="sxs-lookup"><span data-stu-id="a4387-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="a4387-128">Scenari con più origini</span><span class="sxs-lookup"><span data-stu-id="a4387-128">Multiple origin scenarios</span></span>
<span data-ttu-id="a4387-129">Se si desidera autorizzare per CORS uno specifico elenco di origini, le operazioni da eseguire sono più complesse.</span><span class="sxs-lookup"><span data-stu-id="a4387-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="a4387-130">Il problema si verifica quando la rete CDN memorizza nella cache l'intestazione **Access-Control-Allow-Origin** per la prima origine CORS.</span><span class="sxs-lookup"><span data-stu-id="a4387-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="a4387-131">Quando un'origine CORS differente effettua una richiesta successiva, la rete CDN gestisce l'intestazione **Access-Control-Allow-Origin** memorizzata nella cache, che però non corrisponde.</span><span class="sxs-lookup"><span data-stu-id="a4387-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="a4387-132">Esistono diversi modi per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a4387-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="a4387-133">Rete CDN Premium di Azure fornita da Verizon</span><span class="sxs-lookup"><span data-stu-id="a4387-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="a4387-134">Il modo migliore per abilitare questa rete consiste nell'usare la **rete CDN Premium di Azure fornita da Verizon**, in cui sono disponibili alcune funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="a4387-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="a4387-135">È necessario [creare una regola](cdn-rules-engine.md) per verificare l'intestazione **Origin** nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="a4387-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="a4387-136">Se l'origine è valida, la regola imposterà l'intestazione **Access-Control-Allow-Origin** sull'origine indicata nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="a4387-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="a4387-137">Se l'origine specificata nell'intestazione **Origin** non è consentita, la regola dovrà omettere l'intestazione **Access-Control-Allow-Origin**, che causerà il rifiuto della richiesta da parte del browser.</span><span class="sxs-lookup"><span data-stu-id="a4387-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="a4387-138">Per eseguire questa operazione è possibile procedere in due modi usando il motore regole:</span><span class="sxs-lookup"><span data-stu-id="a4387-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="a4387-139">In entrambi i casi, l'intestazione **Access-Control-Allow-Origin** proveniente dal server di origine del file viene completamente ignorata e il motore regole della rete CDN gestisce interamente le origini CORS consentite.</span><span class="sxs-lookup"><span data-stu-id="a4387-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="a4387-140">Un'espressione regolare con tutte le origini valide</span><span class="sxs-lookup"><span data-stu-id="a4387-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="a4387-141">In questo caso verrà creata un'espressione regolare che include tutte le origini che si desidera consentire:</span><span class="sxs-lookup"><span data-stu-id="a4387-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="a4387-142">La **rete CDN di Azure fornita da Verizon** usa la libreria [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) come motore per le espressioni regolari.</span><span class="sxs-lookup"><span data-stu-id="a4387-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="a4387-143">Per convalidare le espressioni regolari, è possibile usare uno strumento come [Regular Expressions 101](https://regex101.com/).</span><span class="sxs-lookup"><span data-stu-id="a4387-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="a4387-144">Si noti che il carattere "/" è valido nelle espressioni regolari e non deve essere preceduto da un carattere di escape. Tuttavia, l'inserimento di un carattere di escape prima di "/" è considerato una procedura consigliata ed è previsto da alcuni strumenti di convalida delle espressioni regolari.</span><span class="sxs-lookup"><span data-stu-id="a4387-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="a4387-145">Se l'espressione regolare corrisponde, la regola specificata sostituirà l'intestazione **Access-Control-Allow-Origin** (se presente) proveniente dall'origine con l'origine che ha inviato la richiesta.</span><span class="sxs-lookup"><span data-stu-id="a4387-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="a4387-146">È inoltre possibile aggiungere altre intestazioni CORS, ad esempio **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="a4387-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Esempio di regole con espressione regolare](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="a4387-148">Regola intestazione richiesta per ciascuna origine.</span><span class="sxs-lookup"><span data-stu-id="a4387-148">Request header rule for each origin.</span></span>
<span data-ttu-id="a4387-149">Anziché usare espressioni regolari, è possibile creare una regola separata per ogni origine che si vuole consentire usando la [condizione di corrispondenza](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1) **Request Header Wildcard** (Carattere jolly intestazione richiesta).</span><span class="sxs-lookup"><span data-stu-id="a4387-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="a4387-150">Come per il metodo delle espressioni regolari, il motore regole imposta le intestazioni CORS.</span><span class="sxs-lookup"><span data-stu-id="a4387-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Esempio di regole senza espressione regolare](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="a4387-152">Nell'esempio precedente l'uso del carattere jolly asterisco (*) indica al motore regole di mettere in corrispondenza sia HTTP che HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4387-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="a4387-153">Rete CDN Standard di Azure</span><span class="sxs-lookup"><span data-stu-id="a4387-153">Azure CDN Standard</span></span>
<span data-ttu-id="a4387-154">Nei profili della rete CDN Standard di Azure, l'unico meccanismo per consentire più origini senza l'uso dell'origine con caratteri jolly consiste nella [memorizzazione della stringa di query nella cache](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="a4387-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="a4387-155">È necessario abilitare l'impostazione della stringa di query per l'endpoint della rete CDN e usare quindi una stringa di query univoca per le richieste provenienti da ciascun dominio consentito.</span><span class="sxs-lookup"><span data-stu-id="a4387-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="a4387-156">Con questa operazione la rete CDN memorizzerà nella cache un oggetto separato per ciascuna stringa di query univoca.</span><span class="sxs-lookup"><span data-stu-id="a4387-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="a4387-157">Questo approccio tuttavia non rappresenta la soluzione ideale, poiché avrà come risultato la memorizzazione nella cache di più copie dello stesso file nella rete CDN.</span><span class="sxs-lookup"><span data-stu-id="a4387-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

