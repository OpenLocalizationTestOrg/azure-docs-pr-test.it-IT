---
title: "proprietà toouse aaaHow nei criteri di gestione API di Azure"
description: "Informazioni su come proprietà toouse nei criteri di gestione API di Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="d0c5d-103">Come proprietà toouse nei criteri di gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="d0c5d-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="d0c5d-104">Criteri di gestione API sono una potente funzionalità del sistema hello che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="d0c5d-105">I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="d0c5d-106">Per creare istruzioni dei criteri è possibile usare valori di testo, espressioni di criteri e proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="d0c5d-107">Ogni istanza del servizio Gestione API include una raccolta di proprietà di coppie chiave/valore che sono toohello globale dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="d0c5d-108">Queste proprietà possono essere valori stringa costante toomanage utilizzata in tutti i criteri e configurazione dell'API.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="d0c5d-109">Ogni proprietà dispone hello gli attributi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="d0c5d-110">Attributo</span><span class="sxs-lookup"><span data-stu-id="d0c5d-110">Attribute</span></span> | <span data-ttu-id="d0c5d-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="d0c5d-111">Type</span></span> | <span data-ttu-id="d0c5d-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d0c5d-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d0c5d-113">Name</span><span class="sxs-lookup"><span data-stu-id="d0c5d-113">Name</span></span> |<span data-ttu-id="d0c5d-114">string</span><span class="sxs-lookup"><span data-stu-id="d0c5d-114">string</span></span> |<span data-ttu-id="d0c5d-115">nome di Hello della proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-115">hello name of hello property.</span></span> <span data-ttu-id="d0c5d-116">Può contenere solo lettere, cifre, punti, trattini e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="d0c5d-117">Valore</span><span class="sxs-lookup"><span data-stu-id="d0c5d-117">Value</span></span> |<span data-ttu-id="d0c5d-118">string</span><span class="sxs-lookup"><span data-stu-id="d0c5d-118">string</span></span> |<span data-ttu-id="d0c5d-119">valore di Hello della proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-119">hello value of hello property.</span></span> <span data-ttu-id="d0c5d-120">Non può essere vuoto o contenere solo spazi.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="d0c5d-121">Segreto</span><span class="sxs-lookup"><span data-stu-id="d0c5d-121">Secret</span></span> |<span data-ttu-id="d0c5d-122">boolean</span><span class="sxs-lookup"><span data-stu-id="d0c5d-122">boolean</span></span> |<span data-ttu-id="d0c5d-123">Determina se il valore di hello è una chiave privata e deve essere crittografato o meno.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="d0c5d-124">Tag</span><span class="sxs-lookup"><span data-stu-id="d0c5d-124">Tags</span></span> |<span data-ttu-id="d0c5d-125">matrice di valori string</span><span class="sxs-lookup"><span data-stu-id="d0c5d-125">array of string</span></span> |<span data-ttu-id="d0c5d-126">Tag facoltativo che quando viene fornito può essere utilizzato toofilter hello proprietà elenco.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="d0c5d-127">Le proprietà vengono configurate nel portale di server di pubblicazione hello in hello **proprietà** scheda. Nell'esempio seguente di hello, sono configurate tre proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Proprietà][api-management-properties]

<span data-ttu-id="d0c5d-129">I valori delle proprietà possono contenere stringhe letterali ed [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0c5d-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="d0c5d-130">Hello nella tabella seguente mostra hello precedente esempio tre proprietà e i relativi attributi.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="d0c5d-131">valore di Hello `ExpressionProperty` è un'espressione di criteri che restituisce una stringa contenente hello data e ora correnti.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="d0c5d-132">proprietà Hello `ContosoHeaderValue` è contrassegnata come chiave privata, pertanto il relativo valore non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="d0c5d-133">Nome</span><span class="sxs-lookup"><span data-stu-id="d0c5d-133">Name</span></span> | <span data-ttu-id="d0c5d-134">Valore</span><span class="sxs-lookup"><span data-stu-id="d0c5d-134">Value</span></span> | <span data-ttu-id="d0c5d-135">Segreto</span><span class="sxs-lookup"><span data-stu-id="d0c5d-135">Secret</span></span> | <span data-ttu-id="d0c5d-136">Tag</span><span class="sxs-lookup"><span data-stu-id="d0c5d-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d0c5d-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="d0c5d-137">ContosoHeader</span></span> |<span data-ttu-id="d0c5d-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="d0c5d-138">TrackingId</span></span> |<span data-ttu-id="d0c5d-139">False</span><span class="sxs-lookup"><span data-stu-id="d0c5d-139">False</span></span> |<span data-ttu-id="d0c5d-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="d0c5d-140">Contoso</span></span> |
| <span data-ttu-id="d0c5d-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="d0c5d-141">ContosoHeaderValue</span></span> |<span data-ttu-id="d0c5d-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="d0c5d-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="d0c5d-143">True</span><span class="sxs-lookup"><span data-stu-id="d0c5d-143">True</span></span> |<span data-ttu-id="d0c5d-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="d0c5d-144">Contoso</span></span> |
| <span data-ttu-id="d0c5d-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="d0c5d-145">ExpressionProperty</span></span> |<span data-ttu-id="d0c5d-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="d0c5d-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="d0c5d-147">False</span><span class="sxs-lookup"><span data-stu-id="d0c5d-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="d0c5d-148">una proprietà toouse</span><span class="sxs-lookup"><span data-stu-id="d0c5d-148">toouse a property</span></span>
<span data-ttu-id="d0c5d-149">come nome della proprietà hello sul posto all'interno di una coppia di parentesi graffe doppia toouse una proprietà in un criterio, `{{ContosoHeader}}`, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="d0c5d-150">In questo esempio, `ContosoHeader` viene utilizzato come nome hello di un'intestazione in un `set-header` , criteri e `ContosoHeaderValue` viene utilizzato come valore hello di tale intestazione.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="d0c5d-151">Quando questo criterio viene valutato durante un gateway di gestione API toohello richiesta o risposta, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` vengono sostituiti con i relativi valori di proprietà corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="d0c5d-152">Proprietà possono essere utilizzate come attributi completo o valori di elemento, come illustrato nell'esempio precedente hello, ma anche possono essere inseriti o combinati con parte di un'espressione di testo letterale, come illustrato nell'esempio seguente hello:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="d0c5d-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="d0c5d-153">Le proprietà possono anche contenere espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="d0c5d-154">Nell'esempio seguente di hello, hello `ExpressionProperty` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="d0c5d-155">Quando questo criterio viene valutato, `{{ExpressionProperty}}` viene sostituito dal valore corrispondente: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="d0c5d-156">Poiché il valore di hello è un'espressione di criteri, hello espressione viene valutata e criteri hello continua con l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="d0c5d-157">È possibile testare questo out nel portale per sviluppatori hello chiamando un'operazione che ha un criterio con le proprietà nell'ambito.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="d0c5d-158">Nell'esempio seguente di hello, chiamata di un'operazione con l'esempio precedente due hello `set-header` criteri con le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="d0c5d-159">Si noti che la risposta hello contiene due intestazioni personalizzate che sono state configurate usando i criteri con le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Portale per sviluppatori][api-management-send-results]

<span data-ttu-id="d0c5d-161">Se si osserva hello [traccia API controllo](api-management-howto-api-inspector.md) per una chiamata che include hello due precedenti esempi di criteri con le proprietà, è possibile visualizzare due hello `set-header` criteri con i valori delle proprietà hello inseriti nonché l'espressione di criteri hello valutazione di proprietà hello contenente l'espressione di criteri hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Traccia di Controllo API][api-management-api-inspector-trace]

<span data-ttu-id="d0c5d-163">Si noti che mentre i valori delle proprietà possono contenere espressioni di criteri, i valori delle proprietà non possono contenere altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="d0c5d-164">Se il testo che contiene un riferimento di proprietà viene utilizzato per un valore della proprietà, ad esempio `Property value text {{MyProperty}}`, un riferimento a proprietà non verrà sostituito che verrà incluso come parte del valore della proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="d0c5d-165">una proprietà toocreate</span><span class="sxs-lookup"><span data-stu-id="d0c5d-165">toocreate a property</span></span>
<span data-ttu-id="d0c5d-166">Fare clic su una proprietà, toocreate **aggiungere proprietà** su hello **proprietà** scheda.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Aggiungi proprietà][api-management-properties-add-property-menu]

<span data-ttu-id="d0c5d-168">**Nome** e **Valore** sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="d0c5d-169">Se il valore della proprietà è una chiave privata, selezionare hello **si tratta di un segreto** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="d0c5d-170">Immettere uno o più toohelp tag facoltativo all'organizzazione le proprietà e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Aggiungi proprietà][api-management-properties-add-property]

<span data-ttu-id="d0c5d-172">Quando viene salvata una nuova proprietà, hello **proprietà di ricerca** casella di testo viene popolata con il nome di hello della nuova proprietà hello e hello nuova proprietà viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="d0c5d-173">Deselezionare tutte le proprietà, toodisplay hello **proprietà di ricerca** casella di testo, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Proprietà][api-management-properties-property-saved]

<span data-ttu-id="d0c5d-175">Per informazioni sulla creazione di una proprietà utilizzando l'API REST di hello, vedere [creare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="d0c5d-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="d0c5d-176">una proprietà tooedit</span><span class="sxs-lookup"><span data-stu-id="d0c5d-176">tooedit a property</span></span>
<span data-ttu-id="d0c5d-177">Fare clic su una proprietà, tooedit **modifica** accanto a tooedit proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Modifica proprietà][api-management-properties-edit]

<span data-ttu-id="d0c5d-179">Apportare le modifiche desiderate e fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="d0c5d-180">Se si modifica il nome di proprietà hello, tutti i criteri che fanno riferimento a tale proprietà sono di nuovo nome di hello toouse aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Modifica proprietà][api-management-properties-edit-property]

<span data-ttu-id="d0c5d-182">Per informazioni sulla modifica di una proprietà utilizzando l'API REST di hello, vedere [modificare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="d0c5d-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="d0c5d-183">una proprietà toodelete</span><span class="sxs-lookup"><span data-stu-id="d0c5d-183">toodelete a property</span></span>
<span data-ttu-id="d0c5d-184">Fare clic su una proprietà, toodelete **eliminare** accanto a toodelete proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Elimina proprietà][api-management-properties-delete]

<span data-ttu-id="d0c5d-186">Fare clic su **Sì, eliminarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-186">Click **Yes, delete it** tooconfirm.</span></span>

![Conferma dell'eliminazione][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="d0c5d-188">Se la proprietà hello viene fatto riferimento da alcun criterio, non sarà possibile toosuccessfully eliminarlo finché non si rimuove la proprietà hello da tutti i criteri che la utilizzano.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="d0c5d-189">Per informazioni sull'eliminazione di una proprietà utilizzando l'API REST di hello, vedere [eliminare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="d0c5d-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="d0c5d-190">proprietà toosearch e filtro</span><span class="sxs-lookup"><span data-stu-id="d0c5d-190">toosearch and filter properties</span></span>
<span data-ttu-id="d0c5d-191">Hello **proprietà** scheda include la ricerca e filtro toohelp funzionalità gestire le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="d0c5d-192">elenco di proprietà hello toofilter dal nome di proprietà, immettere un termine di ricerca in hello **proprietà di ricerca** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="d0c5d-193">Deselezionare tutte le proprietà, toodisplay hello **proprietà di ricerca** casella di testo, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Ricerca][api-management-properties-search]

<span data-ttu-id="d0c5d-195">elenco di proprietà hello toofilter dai valori di tag, immettere uno o più tag in hello **Filtra in base a tag** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="d0c5d-196">Deselezionare tutte le proprietà, toodisplay hello **Filtra in base a tag** casella di testo, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="d0c5d-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filtro][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="d0c5d-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0c5d-198">Next steps</span></span>
* <span data-ttu-id="d0c5d-199">Ulteriori informazioni sull'uso dei criteri</span><span class="sxs-lookup"><span data-stu-id="d0c5d-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="d0c5d-200">Criteri in Gestione API</span><span class="sxs-lookup"><span data-stu-id="d0c5d-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="d0c5d-201">Riferimento ai criteri</span><span class="sxs-lookup"><span data-stu-id="d0c5d-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="d0c5d-202">Espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="d0c5d-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="d0c5d-203">Guardare un video introduttivo</span><span class="sxs-lookup"><span data-stu-id="d0c5d-203">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

