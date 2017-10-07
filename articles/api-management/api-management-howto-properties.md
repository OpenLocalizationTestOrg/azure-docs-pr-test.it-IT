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
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Come proprietà toouse nei criteri di gestione API di Azure
Criteri di gestione API sono una potente funzionalità del sistema hello che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione. I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API. Per creare istruzioni dei criteri è possibile usare valori di testo, espressioni di criteri e proprietà. 

Ogni istanza del servizio Gestione API include una raccolta di proprietà di coppie chiave/valore che sono toohello globale dell'istanza del servizio. Queste proprietà possono essere valori stringa costante toomanage utilizzata in tutti i criteri e configurazione dell'API. Ogni proprietà dispone hello gli attributi seguenti.

| Attributo | Tipo | Descrizione |
| --- | --- | --- |
| Name |string |nome di Hello della proprietà hello. Può contenere solo lettere, cifre, punti, trattini e caratteri di sottolineatura. |
| Valore |string |valore di Hello della proprietà hello. Non può essere vuoto o contenere solo spazi. |
| Segreto |boolean |Determina se il valore di hello è una chiave privata e deve essere crittografato o meno. |
| Tag |matrice di valori string |Tag facoltativo che quando viene fornito può essere utilizzato toofilter hello proprietà elenco. |

Le proprietà vengono configurate nel portale di server di pubblicazione hello in hello **proprietà** scheda. Nell'esempio seguente di hello, sono configurate tre proprietà.

![Proprietà][api-management-properties]

I valori delle proprietà possono contenere stringhe letterali ed [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx). Hello nella tabella seguente mostra hello precedente esempio tre proprietà e i relativi attributi. valore di Hello `ExpressionProperty` è un'espressione di criteri che restituisce una stringa contenente hello data e ora correnti. proprietà Hello `ContosoHeaderValue` è contrassegnata come chiave privata, pertanto il relativo valore non viene visualizzato.

| Nome | Valore | Segreto | Tag |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>una proprietà toouse
come nome della proprietà hello sul posto all'interno di una coppia di parentesi graffe doppia toouse una proprietà in un criterio, `{{ContosoHeader}}`, come illustrato nell'esempio seguente hello.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

In questo esempio, `ContosoHeader` viene utilizzato come nome hello di un'intestazione in un `set-header` , criteri e `ContosoHeaderValue` viene utilizzato come valore hello di tale intestazione. Quando questo criterio viene valutato durante un gateway di gestione API toohello richiesta o risposta, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` vengono sostituiti con i relativi valori di proprietà corrispondenti.

Proprietà possono essere utilizzate come attributi completo o valori di elemento, come illustrato nell'esempio precedente hello, ma anche possono essere inseriti o combinati con parte di un'espressione di testo letterale, come illustrato nell'esempio seguente hello:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Le proprietà possono anche contenere espressioni di criteri. Nell'esempio seguente di hello, hello `ExpressionProperty` viene utilizzato.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Quando questo criterio viene valutato, `{{ExpressionProperty}}` viene sostituito dal valore corrispondente: `@(DateTime.Now.ToString())`. Poiché il valore di hello è un'espressione di criteri, hello espressione viene valutata e criteri hello continua con l'esecuzione.

È possibile testare questo out nel portale per sviluppatori hello chiamando un'operazione che ha un criterio con le proprietà nell'ambito. Nell'esempio seguente di hello, chiamata di un'operazione con l'esempio precedente due hello `set-header` criteri con le proprietà. Si noti che la risposta hello contiene due intestazioni personalizzate che sono state configurate usando i criteri con le proprietà.

![Portale per sviluppatori][api-management-send-results]

Se si osserva hello [traccia API controllo](api-management-howto-api-inspector.md) per una chiamata che include hello due precedenti esempi di criteri con le proprietà, è possibile visualizzare due hello `set-header` criteri con i valori delle proprietà hello inseriti nonché l'espressione di criteri hello valutazione di proprietà hello contenente l'espressione di criteri hello.

![Traccia di Controllo API][api-management-api-inspector-trace]

Si noti che mentre i valori delle proprietà possono contenere espressioni di criteri, i valori delle proprietà non possono contenere altre proprietà. Se il testo che contiene un riferimento di proprietà viene utilizzato per un valore della proprietà, ad esempio `Property value text {{MyProperty}}`, un riferimento a proprietà non verrà sostituito che verrà incluso come parte del valore della proprietà hello.

## <a name="toocreate-a-property"></a>una proprietà toocreate
Fare clic su una proprietà, toocreate **aggiungere proprietà** su hello **proprietà** scheda.

![Aggiungi proprietà][api-management-properties-add-property-menu]

**Nome** e **Valore** sono obbligatori. Se il valore della proprietà è una chiave privata, selezionare hello **si tratta di un segreto** casella di controllo. Immettere uno o più toohelp tag facoltativo all'organizzazione le proprietà e fare clic su **salvare**.

![Aggiungi proprietà][api-management-properties-add-property]

Quando viene salvata una nuova proprietà, hello **proprietà di ricerca** casella di testo viene popolata con il nome di hello della nuova proprietà hello e hello nuova proprietà viene visualizzata. Deselezionare tutte le proprietà, toodisplay hello **proprietà di ricerca** casella di testo, quindi premere INVIO.

![Proprietà][api-management-properties-property-saved]

Per informazioni sulla creazione di una proprietà utilizzando l'API REST di hello, vedere [creare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>una proprietà tooedit
Fare clic su una proprietà, tooedit **modifica** accanto a tooedit proprietà hello.

![Modifica proprietà][api-management-properties-edit]

Apportare le modifiche desiderate e fare clic su **Save**. Se si modifica il nome di proprietà hello, tutti i criteri che fanno riferimento a tale proprietà sono di nuovo nome di hello toouse aggiornate automaticamente.

![Modifica proprietà][api-management-properties-edit-property]

Per informazioni sulla modifica di una proprietà utilizzando l'API REST di hello, vedere [modificare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>una proprietà toodelete
Fare clic su una proprietà, toodelete **eliminare** accanto a toodelete proprietà hello.

![Elimina proprietà][api-management-properties-delete]

Fare clic su **Sì, eliminarlo** tooconfirm.

![Conferma dell'eliminazione][api-management-delete-confirm]

> [!IMPORTANT]
> Se la proprietà hello viene fatto riferimento da alcun criterio, non sarà possibile toosuccessfully eliminarlo finché non si rimuove la proprietà hello da tutti i criteri che la utilizzano.
> 
> 

Per informazioni sull'eliminazione di una proprietà utilizzando l'API REST di hello, vedere [eliminare una proprietà utilizzando l'API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>proprietà toosearch e filtro
Hello **proprietà** scheda include la ricerca e filtro toohelp funzionalità gestire le proprietà. elenco di proprietà hello toofilter dal nome di proprietà, immettere un termine di ricerca in hello **proprietà di ricerca** casella di testo. Deselezionare tutte le proprietà, toodisplay hello **proprietà di ricerca** casella di testo, quindi premere INVIO.

![Ricerca][api-management-properties-search]

elenco di proprietà hello toofilter dai valori di tag, immettere uno o più tag in hello **Filtra in base a tag** casella di testo. Deselezionare tutte le proprietà, toodisplay hello **Filtra in base a tag** casella di testo, quindi premere INVIO.

![Filtro][api-management-properties-filter]

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sull'uso dei criteri
  * [Criteri in Gestione API](api-management-howto-policies.md)
  * [Riferimento ai criteri](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Guardare un video introduttivo
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

