---
title: Criteri in Gestione API di Azure | Microsoft Docs
description: Informazioni su come creare, modificare e configurare criteri in Gestione API.
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
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="2ed4b-103">Criteri in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="2ed4b-103">Policies in Azure API Management</span></span>
<span data-ttu-id="2ed4b-104">In Gestione API di Azure i criteri sono una potente funzionalità del sistema che consentono all'entità di pubblicazione di modificare il comportamento dell'API tramite la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="2ed4b-105">I criteri sono una raccolta di istruzioni che vengono eseguite in modo sequenziale in caso di richiesta o risposta di un'API.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="2ed4b-106">Le istruzioni più comuni includono la conversione di formato da XML a JSON e la limitazione della frequenza delle chiamate per limitare la quantità di chiamate in ingresso da uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="2ed4b-107">Sono disponibili molti altri criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="2ed4b-108">Per un elenco completo di istruzioni dei criteri e delle relative impostazioni, vedere [Informazioni di riferimento per i criteri][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="2ed4b-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="2ed4b-109">I criteri vengono applicati nel gateway che si trova tra il consumer di API e l'API gestita.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="2ed4b-110">Il gateway riceve tutte le richieste e in genere le inoltra invariate all'API sottostante.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="2ed4b-111">Tuttavia i criteri possono applicare modifiche sia alla richiesta in ingresso che alla risposta in uscita.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="2ed4b-112">Le espressioni di criteri possono essere usate come valori di attributo o valori di testo in uno qualsiasi dei criteri di Gestione API, salvo diversamente specificato dai criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="2ed4b-113">Alcuni criteri, come [Flusso di controllo][Control flow] e [Imposta variabile][Set variable], sono basati su espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="2ed4b-114">Per altre informazioni, vedere [Criteri avanzati][Advanced policies] e [Espressioni di criteri][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="2ed4b-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="2ed4b-115"><a name="scopes"> </a>Come configurare criteri</span><span class="sxs-lookup"><span data-stu-id="2ed4b-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="2ed4b-116">I criteri possono essere configurati a livello globale o nell'ambito di un [Prodotto][Product], [API][API] o [Operazione][Operation].</span><span class="sxs-lookup"><span data-stu-id="2ed4b-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="2ed4b-117">Per configurare i criteri, passare all'editor dei criteri nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Menu Criteri][policies-menu]

<span data-ttu-id="2ed4b-119">L'editor dei criteri comprende tre sezioni principali: l'ambito criteri (in alto), la definizione criteri in cui i criteri vengono modificati (a sinistra) e l'elenco di istruzioni (a destra).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Editor criteri][policies-editor]

<span data-ttu-id="2ed4b-121">Per iniziare a configurare i criteri, prima è necessario selezionare l'ambito in cui applicare i criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="2ed4b-122">Nella schermata seguente è selezionato il prodotto **Starter** .</span><span class="sxs-lookup"><span data-stu-id="2ed4b-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="2ed4b-123">Il quadratino accanto al nome del criterio indica che un criterio è già applicato a questo livello.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="2ed4b-125">Poiché è già stato applicato un criterio, la configurazione viene mostrata nella visualizzazione definizione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configurare][policies-configure]

<span data-ttu-id="2ed4b-127">Il criterio viene dapprima visualizzato come di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="2ed4b-128">Per modificare la definizione, fare clic sull'azione di **configurazione dei criteri** .</span><span class="sxs-lookup"><span data-stu-id="2ed4b-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Modificare][policies-edit]

<span data-ttu-id="2ed4b-130">La definizione criteri è un semplice documento XML che descrive una sequenza di istruzioni in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="2ed4b-131">Il codice XML può essere modificato direttamente nella finestra della definizione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="2ed4b-132">Un elenco di istruzioni è disponibile a destra e le istruzioni applicabili all'ambito corrente sono abilitate ed evidenziate, come ad esempio l'istruzione **Limita frequenza chiamate** nella schermata precedente.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="2ed4b-133">Facendo clic su un'istruzione abilitata, il codice XML appropriato verrà aggiunto in corrispondenza del cursore nella visualizzazione definizione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ed4b-134">Se il criterio che si desidera aggiungere non è abilitato, verificare di essere nell'ambito corretto per il criterio.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="2ed4b-135">Ogni istruzione di criterio è progettata per essere usata in determinati ambiti e sezioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="2ed4b-136">Per esaminare le sezioni dei criteri e gli ambiti di un criterio, controllare la sezione relativa all'**Utilizzo** del criterio in [Informazioni di riferimento per i criteri][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="2ed4b-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="2ed4b-137">Un elenco completo di istruzioni dei criteri e le relative impostazioni sono disponibili in [Informazioni di riferimento per i criteri][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="2ed4b-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="2ed4b-138">Ad esempio, per aggiungere una nuova istruzione per limitare le richieste in arrivo agli indirizzi IP specificati, posizionare il cursore nel contenuto dell'elemento XML `inbound` e fare clic sull'istruzione **Limita IP chiamanti** .</span><span class="sxs-lookup"><span data-stu-id="2ed4b-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Criteri di restrizione][policies-restrict]

<span data-ttu-id="2ed4b-140">Verrà aggiunto un frammento XML all'elemento `inbound` che fornisce informazioni aggiuntive sulla configurazione dell'istruzione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="2ed4b-141">Per limitare le richieste in ingresso e accettare solo quelle da un indirizzo IP 1.2.3.4, modificare il codice XML nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="2ed4b-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salva][policies-save]

<span data-ttu-id="2ed4b-143">Dopo aver configurato le istruzioni per il criterio, fare clic su **Salva** per propagare immediatamente le modifiche al gateway di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="2ed4b-144"><a name="sections"> </a>Informazioni sulla configurazione dei criteri</span><span class="sxs-lookup"><span data-stu-id="2ed4b-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="2ed4b-145">Un criterio è una serie di istruzioni eseguite in un determinato ordine in relazione a una richiesta e una risposta.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="2ed4b-146">La configurazione è correttamente suddivisa nelle sezioni `inbound`, `backend`, `outbound`, e `on-error` come mostrato nella seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="2ed4b-147">Se si verifica un errore durante l'elaborazione di una richiesta, tutti i rimanenti passaggi nelle sezioni `inbound`, `backend`, o `outbound` vengono ignorate e l'esecuzione prosegue con le istruzioni nella sezione`on-error`.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="2ed4b-148">Inserendo istruzioni di criteri nella sezione `on-error` è possibile rivedere l'errore utilizzando la proprietà `context.LastError`, esaminare e personalizzare la risposta di errore tramite il criterio `set-body` e configurare che cosa accade se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="2ed4b-149">Sono disponibili codici di errore per i passaggi incorporati e per gli errori che possono verificarsi durante l'elaborazione delle istruzioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="2ed4b-150">Per altre informazioni, vedere [Gestione degli errori nei criteri di Gestione API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ed4b-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="2ed4b-151">Poiché i criteri possono essere specificati a livelli diversi (globale, di prodotto, di API e di operazione), la configurazione fornisce un modo per specificare l'ordine in cui le istruzioni della definizione del criterio vengono eseguite rispetto al criterio padre.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="2ed4b-152">Gli ambiti dei criteri vengono valutati nell'ordine seguente.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="2ed4b-153">Ambito globale</span><span class="sxs-lookup"><span data-stu-id="2ed4b-153">Global scope</span></span>
2. <span data-ttu-id="2ed4b-154">Ambito del prodotto</span><span class="sxs-lookup"><span data-stu-id="2ed4b-154">Product scope</span></span>
3. <span data-ttu-id="2ed4b-155">Ambito dell’API</span><span class="sxs-lookup"><span data-stu-id="2ed4b-155">API scope</span></span>
4. <span data-ttu-id="2ed4b-156">Ambito dell'operazione</span><span class="sxs-lookup"><span data-stu-id="2ed4b-156">Operation scope</span></span>

<span data-ttu-id="2ed4b-157">Le istruzioni all'interno di essi vengono valutate in base alla posizione dell’elemento `base` , se presente.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="2ed4b-158">Con i criteri globali non sono disponibili criteri padre e l'uso dell'elemento `<base>` in tali criteri non produce alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="2ed4b-159">Ad esempio, se ci sono un criterio a livello globale e un criterio configurato per un'API, quando questa particolare API viene usata, vengono applicati entrambi i criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="2ed4b-160">Gestione API consente l'ordinamento deterministico delle istruzioni combinate per i criteri attraverso l'elemento di base.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="2ed4b-161">Nella definizione del criterio dell'esempio precedente, l'istruzione `cross-domain` verrà eseguita prima di un criterio di livello superiore che verrà a sua volta seguito dal criterio `find-and-replace`.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="2ed4b-162">Per visualizzare i criteri nell'ambito corrente nell'editor dei criteri, fare clic su **Ricalcolare il criterio effettivo per l'ambito selezionato**.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ed4b-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ed4b-163">Next steps</span></span>
<span data-ttu-id="2ed4b-164">Vedere il video seguente sulle espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="2ed4b-164">Check out following video on policy expressions.</span></span>

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
