---
title: portale per sviluppatori di aaaCustomize hello gestione API mediante modelli-Azure | Documenti Microsoft
description: Informazioni su come toocustomize hello portale per sviluppatori di gestione API di Azure utilizzando i modelli.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Come toocustomize hello portale per sviluppatori di gestione API di Azure utilizzando i modelli

In Gestione API di Azure sono disponibili tre modi principali toocustomize hello portale:

* [Modificare il contenuto di hello di pagine statiche e gli elementi di layout di pagina][modify-content-layout]
* [Aggiornare gli stili di hello in portale per sviluppatori hello vengono utilizzati per gli elementi di pagina][customize-styles]
* [Modificare modelli di hello utilizzati per le pagine generate dal portale hello] [ portal-templates] (descritto in questa Guida)

I modelli sono utilizzati toocustomize hello contenuto di pagine del portale per sviluppatori generato dal sistema (ad esempio documenti di API, prodotti, l'autenticazione utente e così via). Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e un set specificato di risorse stringa localizzata, icone e i controlli di pagina, è necessario il contenuto di una grande flessibilità tooconfigure hello delle pagine di hello come desiderato.

## <a name="developer-portal-templates-overview"></a>Panoramica sui modelli del portale per sviluppatori
Modifica dei modelli viene eseguita tramite hello **portale per sviluppatori** mentre viene effettuato l'accesso come amministratore. tooget esiste prima di tutto aprire hello portale di Azure e fare clic su **portale di pubblicazione** dalla barra degli strumenti del servizio hello dell'istanza di gestione API.

![Portale di pubblicazione][api-management-management-console]

Fare clic su **portale per sviluppatori** in alto a destra di hello. 

![Menu del portale per sviluppatori][api-management-developer-portal-menu]

tooaccess hello modelli portale per sviluppatori, fare clic su hello personalizzare l'icona nel menu di personalizzazione di hello toodisplay sinistro hello e fare clic su **modelli**.

![Modelli del portale per sviluppatori][api-management-customize-menu]

elenco di modelli Hello consente di visualizzare diverse categorie di modelli che coprono diverse pagine di hello nel portale per sviluppatori hello. Ogni modello è diverso, ma hello passaggi tooedit li e pubblicare le modifiche di hello sono hello stesso. tooedit un modello, fare clic su nome hello del modello di hello.

![Modelli del portale per sviluppatori][api-management-templates-menu]

Fare clic su un modello accetta toohello developer pagina del portale è personalizzabile da tale modello. In questo hello esempio **Product list** modello viene visualizzato. Hello **Product list** controlli modello hello area dello schermo hello indicato dal rettangolo rosso hello. 

![Modello Product list][api-management-developer-portal-templates-overview]

Alcuni modelli, ad esempio hello **profilo utente** modelli, personalizzare diverse parti di hello stessa pagina. 

![Modelli User Profile][api-management-user-profile-templates]

editor Hello per ogni modello di portale per sviluppatori ha due sezioni visualizzate nella parte inferiore di hello della pagina hello. lato sinistro Hello Visualizza hello modifica riquadro per il modello di hello e sul lato destro di hello hello data model per il modello di hello. 

riquadro di modifica del modello Hello contiene markup hello che controlla l'aspetto di hello e il comportamento di hello pagina corrispondente nel portale per sviluppatori hello. markup Hello nel modello hello utilizza hello [DotLiquid](http://dotliquidmarkup.org/) sintassi. Uno degli editor più diffusi per DotLiquid è [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Qualsiasi modello toohello le modifiche apportate durante la modifica vengono visualizzati in tempo reale nel browser hello, ma sono i clienti tooyour non visibile finché non si [salvare](#to-save-a-template) e [pubblicare](#to-publish-a-template) modello hello.

![Markup del modello][api-management-template]

Hello **dati modello** riquadro viene fornita una Guida toohello dati del modello per le entità hello sono disponibili per l'utilizzo in un modello specifico. Questa guida fornisce visualizzando i dati in tempo reale hello attualmente visualizzati nel portale per sviluppatori hello. È possibile espandere i riquadri di modello hello facendo clic sul rettangolo hello nell'angolo superiore destro di hello di hello **dati modello** riquadro.

![Modello Template data][api-management-template-data]

Nell'esempio precedente hello esistono due prodotti visualizzati nel portale per sviluppatori hello che sono stati recuperati dati hello visualizzati in hello **dati modello** riquadro, come illustrato nell'esempio seguente hello.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

markup Hello in hello **Product list** processi modello hello output hello desiderato dei dati tooprovide scorrendo hello insieme di informazioni toodisplay prodotti e un singolo prodotto tooeach di collegamento. Hello nota `<search-control>` e `<page-control>` elementi nel markup hello. Queste modalità controllano la visualizzazione hello di hello ricerca e i controlli nella pagina hello di paging. `ProductsStrings|PageTitleProducts`è un riferimento a una stringa localizzata contenente hello `h2` testo dell'intestazione di pagina hello. Per un elenco delle risorse stringa, i controlli di pagina e le icone disponibili per l'uso nei modelli del portale per sviluppatori, vedere il [riferimento ai modelli del portale per sviluppatori di Gestione API](api-management-developer-portal-templates-reference.md).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave un modello
toosave un modello, fare clic su Salva nell'editor dei modelli di hello.

![Salvare il modello][api-management-save-template]

Le modifiche salvate non sono in tempo reale nel portale per sviluppatori hello finché non vengono pubblicati.

## <a name="toopublish-a-template"></a>toopublish un modello
I modelli salvati possono essere pubblicati singolarmente o tutti insieme. toopublish un singolo modello, fare clic su pubblica nell'editor dei modelli di hello.

![Pubblicare il modello][api-management-publish-template]

Fare clic su **Sì** tooconfirm e modello hello in tempo reale nel portale per sviluppatori hello.

![Confermare la pubblicazione][api-management-publish-template-confirm]

toopublish annullata attualmente tutte le versioni dei modelli, fare clic su **pubblica** nell'elenco di modelli di hello. Modelli non pubblicati sono contraddistinte da un asterisco dopo il nome di modello hello. In questo esempio hello **Product list** e **prodotto** modelli vengono pubblicati.

![Pubblicare i modelli][api-management-publish-templates]

Fare clic su **pubblicare le personalizzazioni** tooconfirm.

![Confermare la pubblicazione][api-management-publish-customizations]

I modelli appena pubblicati diventano effettive immediatamente nel portale per sviluppatori di hello.

## <a name="toorevert-a-template-toohello-previous-version"></a>una versione precedente del modello toohello toorevert
una versione pubblicata precedente modello toohello toorevert, fare clic su Ripristina nell'editor dei modelli di hello.

![Annullare le modifiche al modello][api-management-revert-template]

Fare clic su **Sì** tooconfirm.

![Confirm][api-management-revert-template-confirm]

Hello in precedenza la versione pubblicata di un modello è live nel portale per sviluppatori hello dopo hello annullare l'operazione è stata completata.

## <a name="toorestore-a-template-toohello-default-version"></a>una versione predefinita di toohello modello toorestore
Versione predefinita di ripristino modelli tootheir è un processo in due passaggi. Primo modelli hello devono essere ripristinati e quindi versioni hello ripristinato devono essere pubblicate.

toorestore una versione predefinita di toohello singolo modello di fare clic su Ripristina nell'editor dei modelli di hello.

![Annullare le modifiche al modello][api-management-reset-template]

Fare clic su **Sì** tooconfirm.

![Confirm][api-management-reset-template-confirm]

Fare clic su tutte le versioni predefinite tootheir modelli, toorestore **ripristino configurazione di modelli predefiniti** nell'elenco modello hello.

![Ripristinare i modelli][api-management-restore-templates]

Hello ripristinati modelli devono quindi essere pubblicati singolarmente o in un'unica seguendo procedure hello [toopublish un modello](#to-publish-a-template).

## <a name="next-steps"></a>Passaggi successivi
Per informazioni di riferimento sui modelli del portale per sviluppatori, le risorse stringa, le icone e i controlli di pagina, vedere il [riferimento ai modelli del portale per sviluppatori di Gestione API](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







