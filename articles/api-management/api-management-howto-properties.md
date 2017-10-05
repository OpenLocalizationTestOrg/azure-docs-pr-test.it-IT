---
title: "Come usare le proprietà nei criteri di Gestione API di Azure"
description: "Informazioni su come usare le proprietà nei criteri di Gestione API di Azure"
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
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="33d2c-103">Come usare le proprietà nei criteri di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="33d2c-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="33d2c-104">I criteri di Gestione API sono una potente funzionalità del sistema che consentono all'entità di pubblicazione di modificare il comportamento dell'API tramite la configurazione.</span><span class="sxs-lookup"><span data-stu-id="33d2c-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="33d2c-105">I criteri sono una raccolta di istruzioni che vengono eseguite in modo sequenziale sulla richiesta o la risposta di un'API.</span><span class="sxs-lookup"><span data-stu-id="33d2c-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="33d2c-106">Per creare istruzioni dei criteri è possibile usare valori di testo, espressioni di criteri e proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="33d2c-107">Ogni istanza del servizio Gestione API dispone di una raccolta di proprietà di coppie chiave/valore globali per l'istanza stessa.</span><span class="sxs-lookup"><span data-stu-id="33d2c-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="33d2c-108">Queste proprietà possono essere usate per gestire i valori stringa costanti all'interno dell'intera configurazione e di tutti i criteri delle API.</span><span class="sxs-lookup"><span data-stu-id="33d2c-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="33d2c-109">Ogni proprietà ha gli attributi seguenti.</span><span class="sxs-lookup"><span data-stu-id="33d2c-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="33d2c-110">Attributo</span><span class="sxs-lookup"><span data-stu-id="33d2c-110">Attribute</span></span> | <span data-ttu-id="33d2c-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="33d2c-111">Type</span></span> | <span data-ttu-id="33d2c-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="33d2c-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33d2c-113">Name</span><span class="sxs-lookup"><span data-stu-id="33d2c-113">Name</span></span> |<span data-ttu-id="33d2c-114">stringa</span><span class="sxs-lookup"><span data-stu-id="33d2c-114">string</span></span> |<span data-ttu-id="33d2c-115">Nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-115">The name of the property.</span></span> <span data-ttu-id="33d2c-116">Può contenere solo lettere, cifre, punti, trattini e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="33d2c-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="33d2c-117">Valore</span><span class="sxs-lookup"><span data-stu-id="33d2c-117">Value</span></span> |<span data-ttu-id="33d2c-118">stringa</span><span class="sxs-lookup"><span data-stu-id="33d2c-118">string</span></span> |<span data-ttu-id="33d2c-119">Valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-119">The value of the property.</span></span> <span data-ttu-id="33d2c-120">Non può essere vuoto o contenere solo spazi.</span><span class="sxs-lookup"><span data-stu-id="33d2c-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="33d2c-121">Segreto</span><span class="sxs-lookup"><span data-stu-id="33d2c-121">Secret</span></span> |<span data-ttu-id="33d2c-122">boolean</span><span class="sxs-lookup"><span data-stu-id="33d2c-122">boolean</span></span> |<span data-ttu-id="33d2c-123">Determina se il valore è un segreto e se deve essere crittografato.</span><span class="sxs-lookup"><span data-stu-id="33d2c-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="33d2c-124">Tag</span><span class="sxs-lookup"><span data-stu-id="33d2c-124">Tags</span></span> |<span data-ttu-id="33d2c-125">matrice di valori string</span><span class="sxs-lookup"><span data-stu-id="33d2c-125">array of string</span></span> |<span data-ttu-id="33d2c-126">Facoltativi. Quando specificati possono essere usati per filtrare l'elenco delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="33d2c-127">Le proprietà vengono configurate nel portale di pubblicazione nella scheda **Properties** .</span><span class="sxs-lookup"><span data-stu-id="33d2c-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="33d2c-128">Nell'esempio seguente, sono configurate tre proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-128">In the following example, three properties are configured.</span></span>

![Properties][api-management-properties]

<span data-ttu-id="33d2c-130">I valori delle proprietà possono contenere stringhe letterali ed [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="33d2c-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="33d2c-131">Nella tabella seguente sono mostrate le tre proprietà di esempio precedenti e i relativi attributi.</span><span class="sxs-lookup"><span data-stu-id="33d2c-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="33d2c-132">Il valore di `ExpressionProperty` è un'espressione di criteri che restituisce una stringa contenente la data e l'ora correnti.</span><span class="sxs-lookup"><span data-stu-id="33d2c-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="33d2c-133">La proprietà `ContosoHeaderValue` è contrassegnata come un segreto, quindi il valore corrispondente non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="33d2c-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="33d2c-134">Name</span><span class="sxs-lookup"><span data-stu-id="33d2c-134">Name</span></span> | <span data-ttu-id="33d2c-135">Valore</span><span class="sxs-lookup"><span data-stu-id="33d2c-135">Value</span></span> | <span data-ttu-id="33d2c-136">Segreto</span><span class="sxs-lookup"><span data-stu-id="33d2c-136">Secret</span></span> | <span data-ttu-id="33d2c-137">Tag</span><span class="sxs-lookup"><span data-stu-id="33d2c-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="33d2c-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="33d2c-138">ContosoHeader</span></span> |<span data-ttu-id="33d2c-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="33d2c-139">TrackingId</span></span> |<span data-ttu-id="33d2c-140">False</span><span class="sxs-lookup"><span data-stu-id="33d2c-140">False</span></span> |<span data-ttu-id="33d2c-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="33d2c-141">Contoso</span></span> |
| <span data-ttu-id="33d2c-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="33d2c-142">ContosoHeaderValue</span></span> |<span data-ttu-id="33d2c-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="33d2c-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="33d2c-144">True</span><span class="sxs-lookup"><span data-stu-id="33d2c-144">True</span></span> |<span data-ttu-id="33d2c-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="33d2c-145">Contoso</span></span> |
| <span data-ttu-id="33d2c-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="33d2c-146">ExpressionProperty</span></span> |<span data-ttu-id="33d2c-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="33d2c-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="33d2c-148">False</span><span class="sxs-lookup"><span data-stu-id="33d2c-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="33d2c-149">Per usare una proprietà</span><span class="sxs-lookup"><span data-stu-id="33d2c-149">To use a property</span></span>
<span data-ttu-id="33d2c-150">Per usare una proprietà di un criterio, inserire il nome della proprietà all'interno di parentesi graffe doppie, ad esempio `{{ContosoHeader}}`, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="33d2c-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="33d2c-151">In questo esempio, la proprietà `ContosoHeader` viene usata come nome di un'intestazione in un criterio `set-header` e la proprietà `ContosoHeaderValue` viene usata come valore di tale intestazione.</span><span class="sxs-lookup"><span data-stu-id="33d2c-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="33d2c-152">Quando questo criterio viene valutato durante una richiesta o una risposta al gateway di Gestione API, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` vengono sostituiti dai valori delle rispettive proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="33d2c-153">Le proprietà possono essere usate come valori completi di attributo o di elemento, come illustrato nell'esempio precedente, ma possono anche essere inserite all'interno di un'espressione di testo o combinate con una parte di un'espressione di testo, come illustrato nell'esempio seguente: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="33d2c-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="33d2c-154">Le proprietà possono anche contenere espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="33d2c-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="33d2c-155">Nell'esempio seguente viene usata la proprietà `ExpressionProperty` .</span><span class="sxs-lookup"><span data-stu-id="33d2c-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="33d2c-156">Quando questo criterio viene valutato, `{{ExpressionProperty}}` viene sostituito dal valore corrispondente: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="33d2c-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="33d2c-157">Poiché il valore è un'espressione di criteri, l'espressione viene valutata e il criterio passa alla fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="33d2c-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="33d2c-158">È possibile eseguire un test nel portale per sviluppatori chiamando un'operazione il cui ambito contiene un criterio con proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="33d2c-159">Nell'esempio seguente viene chiamata un'operazione che contiene i due criteri di esempio precedenti `set-header` con proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="33d2c-160">Si noti che la risposta contiene due intestazioni personalizzate configurate tramite criteri con proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Portale per sviluppatori][api-management-send-results]

<span data-ttu-id="33d2c-162">Se si osserva la [traccia di Controllo API](api-management-howto-api-inspector.md) relativa a una chiamata che include i due criteri con proprietà degli esempi precedenti, è possibile vedere i due criteri `set-header` con i valori delle proprietà inseriti, nonché la valutazione delle espressioni dei criteri per la proprietà che contiene l'espressione.</span><span class="sxs-lookup"><span data-stu-id="33d2c-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Traccia di Controllo API][api-management-api-inspector-trace]

<span data-ttu-id="33d2c-164">Si noti che mentre i valori delle proprietà possono contenere espressioni di criteri, i valori delle proprietà non possono contenere altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="33d2c-165">Se il testo che contiene un riferimento a una proprietà viene usato come valore di una proprietà, ad esempio `Property value text {{MyProperty}}`, tale riferimento alla proprietà non viene sostituito e viene incluso come parte del valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="33d2c-166">Per creare una proprietà</span><span class="sxs-lookup"><span data-stu-id="33d2c-166">To create a property</span></span>
<span data-ttu-id="33d2c-167">Per creare una proprietà, fare clic su **Aggiungi proprietà** nella scheda **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="33d2c-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Aggiungi proprietà][api-management-properties-add-property-menu]

<span data-ttu-id="33d2c-169">**Nome** e **Valore** sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="33d2c-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="33d2c-170">Se il valore della proprietà è un segreto, selezionare la casella di controllo **This is a secret** .</span><span class="sxs-lookup"><span data-stu-id="33d2c-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="33d2c-171">Immettere uno o più tag facoltativi per organizzare le proprietà, quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="33d2c-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Aggiungi proprietà][api-management-properties-add-property]

<span data-ttu-id="33d2c-173">Quando si salva una nuova proprietà, la casella di testo di **ricerca di proprietà** viene popolata con il nome della nuova proprietà e la nuova proprietà viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="33d2c-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="33d2c-174">Per visualizzare tutte le proprietà, cancellare il contenuto della casella di testo di **ricerca di proprietà** e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="33d2c-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Properties][api-management-properties-property-saved]

<span data-ttu-id="33d2c-176">Per informazioni sulla creazione di una proprietà tramite l'API REST, vedere la [pagina relativa alla creazione di una proprietà tramite l'API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="33d2c-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="33d2c-177">Per modificare una proprietà</span><span class="sxs-lookup"><span data-stu-id="33d2c-177">To edit a property</span></span>
<span data-ttu-id="33d2c-178">Per modificare una proprietà, fare clic su **Edit** accanto alla proprietà da modificare.</span><span class="sxs-lookup"><span data-stu-id="33d2c-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Modifica proprietà][api-management-properties-edit]

<span data-ttu-id="33d2c-180">Apportare le modifiche desiderate e fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="33d2c-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="33d2c-181">Se si modifica il nome della proprietà, tutti i criteri che fanno riferimento a tale proprietà vengono aggiornati automaticamente con il nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="33d2c-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Modifica proprietà][api-management-properties-edit-property]

<span data-ttu-id="33d2c-183">Per informazioni sulla modifica di una proprietà tramite l'API REST, vedere la [pagina relativa alla modifica di una proprietà tramite l'API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="33d2c-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="33d2c-184">Per eliminare una proprietà</span><span class="sxs-lookup"><span data-stu-id="33d2c-184">To delete a property</span></span>
<span data-ttu-id="33d2c-185">Per eliminare una proprietà, fare clic su **Delete** accanto alla proprietà da eliminare.</span><span class="sxs-lookup"><span data-stu-id="33d2c-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Elimina proprietà][api-management-properties-delete]

<span data-ttu-id="33d2c-187">Fare clic su **Sì, elimina** per confermare.</span><span class="sxs-lookup"><span data-stu-id="33d2c-187">Click **Yes, delete it** to confirm.</span></span>

![Conferma dell'eliminazione][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="33d2c-189">Se all'interno di almeno un criterio si fa riferimento alla proprietà, sarà possibile eliminare quest'ultima solo dopo averla rimossa da tutti i criteri che la usano.</span><span class="sxs-lookup"><span data-stu-id="33d2c-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="33d2c-190">Per informazioni sull'eliminazione di una proprietà tramite l'API REST, vedere la [pagina relativa all'eliminazione di una proprietà tramite l'API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="33d2c-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="33d2c-191">Per cercare e filtrare proprietà</span><span class="sxs-lookup"><span data-stu-id="33d2c-191">To search and filter properties</span></span>
<span data-ttu-id="33d2c-192">La scheda **Properties** include funzionalità di ricerca e filtro che consentono di gestire le proprietà.</span><span class="sxs-lookup"><span data-stu-id="33d2c-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="33d2c-193">Per filtrare l'elenco delle proprietà in base al nome di queste, immettere un termine di ricerca nella casella di testo di **ricerca di proprietà** .</span><span class="sxs-lookup"><span data-stu-id="33d2c-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="33d2c-194">Per visualizzare tutte le proprietà, cancellare il contenuto della casella di testo di **ricerca di proprietà** e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="33d2c-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="33d2c-196">Per filtrare l'elenco delle proprietà in base al valore dei tag, immettere uno o più tag nella casella di testo di **filtro in base ai tag** .</span><span class="sxs-lookup"><span data-stu-id="33d2c-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="33d2c-197">Per visualizzare tutte le proprietà, cancellare il contenuto della casella di testo di **filtro in base ai tag** e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="33d2c-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtro][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="33d2c-199">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33d2c-199">Next steps</span></span>
* <span data-ttu-id="33d2c-200">Ulteriori informazioni sull'uso dei criteri</span><span class="sxs-lookup"><span data-stu-id="33d2c-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="33d2c-201">Criteri in Gestione API</span><span class="sxs-lookup"><span data-stu-id="33d2c-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="33d2c-202">Riferimento ai criteri</span><span class="sxs-lookup"><span data-stu-id="33d2c-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="33d2c-203">Espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="33d2c-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="33d2c-204">Guardare un video introduttivo</span><span class="sxs-lookup"><span data-stu-id="33d2c-204">Watch a video overview</span></span>
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

