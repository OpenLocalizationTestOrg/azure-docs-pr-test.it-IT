---
title: rete CDN di Azure con CORS aaaUsing | Documenti Microsoft
description: Informazioni su come toouse hello Azure rete CDN (Content Delivery) toowith condivisione delle risorse Multiorigine (CORS).
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="9bb6e-103">Uso della rete CDN di Azure con CORS</span><span class="sxs-lookup"><span data-stu-id="9bb6e-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="9bb6e-104">Informazioni su CORS</span><span class="sxs-lookup"><span data-stu-id="9bb6e-104">What is CORS?</span></span>
<span data-ttu-id="9bb6e-105">CORS (Cross Origin Resource Sharing) è una funzionalità HTTP che consente a un'applicazione web in esecuzione risorse di tooaccess in un dominio in un altro dominio.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="9bb6e-106">In ordine tooreduce hello possibilità di attacchi di script, tutti i browser moderni implementano una restrizione di sicurezza nota come [criteri stessa origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="9bb6e-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="9bb6e-107">Questo impedisce a una pagina Web di chiamare le API in un dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="9bb6e-108">Condivisione CORS offre una sezione relativa al toocall dei (dominio di origine hello) di un'origine di in modo sicuro tooallow in un'altra origine API.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9bb6e-109">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="9bb6e-109">How it works</span></span>
<span data-ttu-id="9bb6e-110">Esistono due tipi di richieste CORS, le *richieste semplici* e le *richieste complesse*.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="9bb6e-111">Per le richieste semplici:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-111">For simple requests:</span></span>

1. <span data-ttu-id="9bb6e-112">browser Hello Invia richiesta CORS hello con un'ulteriore **origine** intestazione della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="9bb6e-113">il valore di Hello di questa intestazione è origine hello resi hello padre pagina nella quale è definito come combinazione di hello di *protocollo,* *dominio* e *porta.*</span><span class="sxs-lookup"><span data-stu-id="9bb6e-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="9bb6e-114">Quando una pagina da https://www.contoso.com tenta tooaccess dati di un utente in origine fabrikam.com hello, hello dopo l'intestazione della richiesta verrà inviata toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="9bb6e-115">server Hello può rispondere con hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="9bb6e-116">Un'intestazione **Access-Control-Allow-Origin** presente nella risposta, per indicare il sito di origine consentito.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="9bb6e-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="9bb6e-118">Codice di errore HTTP, ad esempio 403 se hello server non consente la richiesta multiorigine hello dopo il controllo intestazione Origin hello</span><span class="sxs-lookup"><span data-stu-id="9bb6e-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="9bb6e-119">Un'intestazione **Access-Control-Allow-Origin** con un carattere jolly che consente tutte le origini:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="9bb6e-120">Per le richieste complesse:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-120">For complex requests:</span></span>

<span data-ttu-id="9bb6e-121">Una richiesta complessa è una richiesta CORS in browser hello toosend richiesto un *richiesta preliminare* (vale a dire una verifica preliminare) prima di inviare una richiesta CORS effettiva hello.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="9bb6e-122">Hello richiesta preliminare richiede autorizzazione server hello se richiesta CORS originale hello può proseguire e un `OPTIONS` richiesta toohello stesso URL.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="9bb6e-123">Per ulteriori informazioni su CORS flussi e i problemi comuni, visualizzare hello [tooCORS della Guida per le API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="9bb6e-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="9bb6e-124">Scenari con caratteri jolly o singola origine</span><span class="sxs-lookup"><span data-stu-id="9bb6e-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="9bb6e-125">CORS nella rete CDN di Azure funzioneranno automaticamente senza alcuna configurazione aggiuntiva quando hello **Access-Control-Allow-Origin** intestazione è impostata toowildcard (*) o una singola origine.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="9bb6e-126">Hello CDN verrà memorizzati nella cache prima risposta hello e le richieste successive utilizzeranno hello stessa intestazione.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="9bb6e-127">Se le richieste sono state apportate toohello CDN tooCORS precedente viene impostata su hello all'origine, sarà necessario toopurge contenuto nel hello tooreload contenuto endpoint contenuto con hello **Access-Control-Allow-Origin** intestazione.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="9bb6e-128">Scenari con più origini</span><span class="sxs-lookup"><span data-stu-id="9bb6e-128">Multiple origin scenarios</span></span>
<span data-ttu-id="9bb6e-129">Se è necessario un elenco specifico di toobe le origini consentite per CORS tooallow, operazioni get leggermente più complesse.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="9bb6e-130">Hello problema si verifica quando hello rete CDN memorizza nella cache di hello **Access-Control-Allow-Origin** intestazione per l'origine CORS prima hello.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="9bb6e-131">Quando una diversa origine CORS effettua una richiesta successiva, hello CDN servirà memorizzati nella cache di hello **Access-Control-Allow-Origin** intestazione, che non corrisponda.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="9bb6e-132">Esistono diversi modi toocorrect questo.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="9bb6e-133">Rete CDN Premium di Azure fornita da Verizon</span><span class="sxs-lookup"><span data-stu-id="9bb6e-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="9bb6e-134">Hello tooenable modo migliore tratta toouse **Premium rete CDN di Azure da Verizon**, che espongono alcune funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="9bb6e-135">È necessario troppo[creare una regola](cdn-rules-engine.md) toocheck hello **origine** intestazione nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="9bb6e-136">Se si tratta di un'origine valida, la regola verrà impostata hello **Access-Control-Allow-Origin** intestazione con origine hello fornito nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="9bb6e-137">Se l'origine hello specificato in hello **origine** intestazione non è consentita, la regola non deve eseguire hello **Access-Control-Allow-Origin** intestazione che può causare errori hello tooreject hello nei browser.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="9bb6e-138">Esistono due modi toodo questo con hello motore regole di business.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="9bb6e-139">In entrambi i casi, hello **Access-Control-Allow-Origin** intestazione dal server di origine del file hello viene ignorato completamente, motore regole di business del hello CDN gestisce completamente hello consentito origini CORS.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="9bb6e-140">Un'espressione regolare con tutte le origini valide</span><span class="sxs-lookup"><span data-stu-id="9bb6e-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="9bb6e-141">In questo caso, si creerà un'espressione regolare che include tutte le origini di hello desiderato tooallow:</span><span class="sxs-lookup"><span data-stu-id="9bb6e-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="9bb6e-142">La **rete CDN di Azure fornita da Verizon** usa la libreria [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) come motore per le espressioni regolari.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="9bb6e-143">È possibile utilizzare uno strumento come [101 di espressioni regolari](https://regex101.com/) toovalidate l'espressione regolare.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="9bb6e-144">Si noti che hello "/" caratteri nelle espressioni regolari valido e non deve necessariamente toobe caratteri di escape, tuttavia, tale carattere di escape è considerata buona norma e prevede un validator di espressione regolare.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="9bb6e-145">Se l'espressione regolare hello corrisponde, la regola sostituirà hello **Access-Control-Allow-Origin** intestazione (se presente) dall'origine hello con origine hello che ha inviato la richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="9bb6e-146">È inoltre possibile aggiungere altre intestazioni CORS, ad esempio **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Esempio di regole con espressione regolare](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="9bb6e-148">Regola intestazione richiesta per ciascuna origine.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-148">Request header rule for each origin.</span></span>
<span data-ttu-id="9bb6e-149">Invece di espressioni regolari, è possibile creare un apposito regola per ogni origine desiderato utilizzando hello tooallow **richiesta jolly intestazione** [corrispondono alla condizione](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="9bb6e-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="9bb6e-150">Come con il metodo di espressione regolare hello, hello motore regole intestazioni da solo con set hello CORS.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Esempio di regole senza espressione regolare](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="9bb6e-152">Nell'esempio hello sopra, hello l'utilizzo del carattere jolly hello * indica toomatch del motore regole di hello HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="9bb6e-153">Rete CDN Standard di Azure</span><span class="sxs-lookup"><span data-stu-id="9bb6e-153">Azure CDN Standard</span></span>
<span data-ttu-id="9bb6e-154">Nei profili di rete CDN di Azure Standard, hello solo tooallow meccanismo per più origini senza utilizzare hello di origine con caratteri jolly hello è toouse [la memorizzazione nella cache di stringa di query](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="9bb6e-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="9bb6e-155">È necessario tooenable impostazione della stringa di query per l'endpoint rete CDN hello e quindi utilizzare una stringa di query univoci per le richieste da ogni dominio consentito.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="9bb6e-156">Questa operazione comporterà hello CDN la memorizzazione nella cache un oggetto separato per ogni stringa di query univoco.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="9bb6e-157">Questo approccio non è ideale, tuttavia, in quanto comporta in più copie di hello lo stesso file hello memorizzati nella cache nella rete CDN.</span><span class="sxs-lookup"><span data-stu-id="9bb6e-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

