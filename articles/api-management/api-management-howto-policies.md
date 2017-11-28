---
title: aaaPolicies in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocreate, modificare e configurare i criteri in Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="a3cf9-103">Criteri in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a3cf9-103">Policies in Azure API Management</span></span>
<span data-ttu-id="a3cf9-104">In Gestione API di Azure, i criteri sono una potente funzionalità del sistema hello che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="a3cf9-105">I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="a3cf9-106">Le istruzioni più comuni includono la conversione di formato da XML tooJSON e limitare toorestrict hello quantità di chiamate in ingresso da uno sviluppatore di frequenza delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="a3cf9-107">Viene fornita hello disponibili molti altri criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="a3cf9-108">Vedere hello [Policy Reference] [ Policy Reference] per un elenco completo delle istruzioni dei criteri e le relative impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="a3cf9-109">I criteri vengono applicati all'interno di gateway hello che si trova tra i consumer di API hello e API hello gestito.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="a3cf9-110">riceve tutte le richieste Hello gateway, in genere inoltrandoli inalterato toohello API sottostante.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="a3cf9-111">Tuttavia, possibile applicare un criterio di modifiche tooboth hello in ingresso richiesta e risposta in uscita.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="a3cf9-112">Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="a3cf9-113">Alcuni criteri, ad esempio hello [flusso di controllo] [ Control flow] e [Imposta variabile] [ Set variable] criteri sono basati su espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="a3cf9-114">Per altre informazioni, vedere [Criteri avanzati][Advanced policies] e [Espressioni di criteri][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="a3cf9-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="a3cf9-115"><a name="scopes"></a>Come tooconfigure criteri</span><span class="sxs-lookup"><span data-stu-id="a3cf9-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="a3cf9-116">È possibile configurare i criteri a livello globale o nell'ambito di hello di un [prodotto][Product], [API] [ API] o [operazione] [Operation].</span><span class="sxs-lookup"><span data-stu-id="a3cf9-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="a3cf9-117">tooconfigure un criterio, passare a editor Criteri di toohello nel portale di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Menu Criteri][policies-menu]

<span data-ttu-id="a3cf9-119">editor Criteri di Hello è costituito da tre sezioni principali: hello criteri (superiore), hello criteri definizione dell'ambito in cui i criteri vengono modificati (a sinistra) e le istruzioni di hello elenco (a destra):</span><span class="sxs-lookup"><span data-stu-id="a3cf9-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Editor criteri][policies-editor]

<span data-ttu-id="a3cf9-121">toobegin un criterio, che è innanzitutto necessario selezionare l'ambito di hello in cui hello è consigliabile applicare criteri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="a3cf9-122">Nella schermata di hello seguito hello **Starter** prodotto selezionato.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="a3cf9-123">Si noti che nome hello quadrato simbolo successivo toohello criteri indica che un criterio è già stato applicato a questo livello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="a3cf9-125">Poiché è già stato applicato un criterio, configurazione hello è mostrati nella visualizzazione di definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Configurare][policies-configure]

<span data-ttu-id="a3cf9-127">Hello criterio viene visualizzato in sola lettura prima.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="a3cf9-128">In ordine tooedit definizione hello, fare clic su hello **configura i criteri di** azione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Modificare][policies-edit]

<span data-ttu-id="a3cf9-130">definizione dei criteri Hello è un semplice documento XML che descrive una sequenza di istruzioni in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="a3cf9-131">Hello XML può essere modificata direttamente nella finestra di definizione hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="a3cf9-132">Un elenco di istruzioni viene fornito toohello destra e ambito di istruzioni toohello applicabile corrente sono abilitati, evidenziati; come illustrato da hello **limite di velocità di chiamare** istruzione hello schermata precedente.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="a3cf9-133">Fare clic su un'istruzione abilitata aggiungerà hello XML appropriato nella posizione di hello del cursore hello nella visualizzazione definizione hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="a3cf9-134">Se i criteri di hello che si desidera tooadd non sono abilitato, verificare di essere nell'ambito corretto di hello per tale criterio.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="a3cf9-135">Ogni istruzione di criterio è progettata per essere usata in determinati ambiti e sezioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="a3cf9-136">sezioni del criterio tooreview hello e gli ambiti per i criteri, controllare hello **utilizzo** sezione relativo hello [Policy Reference][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a3cf9-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="a3cf9-137">Un elenco completo delle istruzioni dei criteri e le relative impostazioni sono disponibili in hello [Policy Reference][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a3cf9-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="a3cf9-138">Ad esempio, tooadd un toorestrict istruzione nuova in ingresso richiede indirizzi IP toospecified, posizionare il cursore hello solo all'interno del contenuto di hello di hello `inbound` hello di elemento e fare clic su XML **chiamante limitare gli indirizzi IP** istruzione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Criteri di restrizione][policies-restrict]

<span data-ttu-id="a3cf9-140">Verrà aggiunta una toohello frammento XML `inbound` elemento che fornisce indicazioni su come tooconfigure hello istruzione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="a3cf9-141">toolimit le richieste in ingresso e accettare solo quelli da un indirizzo IP di 1.2.3.4 modificare hello XML come segue:</span><span class="sxs-lookup"><span data-stu-id="a3cf9-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salva][policies-save]

<span data-ttu-id="a3cf9-143">Una volta completata la configurazione di istruzioni hello per criteri di hello, fare clic su **salvare** e modifiche hello saranno gateway di gestione API toohello propagate immediatamente.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="a3cf9-144"><a name="sections"> </a>Informazioni sulla configurazione dei criteri</span><span class="sxs-lookup"><span data-stu-id="a3cf9-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="a3cf9-145">Un criterio è una serie di istruzioni eseguite in un determinato ordine in relazione a una richiesta e una risposta.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="a3cf9-146">configurazione di Hello è suddivisa in modo appropriato `inbound`, `backend`, `outbound`, e `on-error` sezioni come illustrato nella seguente configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="a3cf9-147">Se si verifica un errore durante l'elaborazione di hello di una richiesta, tutti i rimanenti passaggi hello `inbound`, `backend`, o `outbound` sezioni vengono ignorate e l'esecuzione passa istruzioni toohello hello `on-error` sezione.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="a3cf9-148">Inserendo istruzioni dei criteri in hello `on-error` sezione è possibile esaminare l'errore hello utilizzando hello `context.LastError` proprietà, esaminare e personalizzare risposta di errore di hello utilizzando hello `set-body` , criteri e configurare che cosa accade se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="a3cf9-149">Sono disponibili codici di errore per i passaggi predefiniti e gli errori che possono verificarsi durante l'elaborazione di hello delle istruzioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="a3cf9-150">Per altre informazioni, vedere [Gestione degli errori nei criteri di Gestione API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3cf9-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="a3cf9-151">Poiché è possibile specificare i criteri a livelli diversi (globale, prodotto, api e operation) configurazione hello offre un modo per si ordine hello toospecify in cui vengono eseguite le istruzioni di definizione dei criteri hello con i criteri di riguardo toohello padre.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="a3cf9-152">Ambiti del criterio vengono valutati nell'ordine hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="a3cf9-153">Ambito globale</span><span class="sxs-lookup"><span data-stu-id="a3cf9-153">Global scope</span></span>
2. <span data-ttu-id="a3cf9-154">Ambito del prodotto</span><span class="sxs-lookup"><span data-stu-id="a3cf9-154">Product scope</span></span>
3. <span data-ttu-id="a3cf9-155">Ambito dell’API</span><span class="sxs-lookup"><span data-stu-id="a3cf9-155">API scope</span></span>
4. <span data-ttu-id="a3cf9-156">Ambito dell'operazione</span><span class="sxs-lookup"><span data-stu-id="a3cf9-156">Operation scope</span></span>

<span data-ttu-id="a3cf9-157">salve le istruzioni all'interno di essi vengono valutate in base a posizione toohello di hello `base` elemento, se presente.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="a3cf9-158">Criteri globali dispone di alcun criterio padre e l'utilizzo di hello `<base>` elemento in esso non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="a3cf9-159">Ad esempio, se si dispone di un criterio a livello globale di hello e configurato un criterio per un'API, quindi ogni volta che viene utilizzato tale API specifica entrambi i criteri diventeranno.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="a3cf9-160">Consente di gestione API per l'ordinamento deterministica delle istruzioni dei criteri combinati tramite l'elemento di base hello.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="a3cf9-161">Nella definizione di criteri esempio hello sopra, hello `cross-domain` istruzione verrebbe eseguito prima che tutti i criteri superiore che a sua volta, potrebbe essere seguito da hello `find-and-replace` criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="a3cf9-162">Fare clic su criteri hello toosee nell'ambito corrente di hello in editor Criteri di hello **ricalcolare il criterio effettivo per l'ambito selezionato**.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3cf9-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3cf9-163">Next steps</span></span>
<span data-ttu-id="a3cf9-164">Vedere il video seguente sulle espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
