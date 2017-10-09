---
title: aaaHow toocreate e pubblicazione di un prodotto in Gestione API di Azure
description: Informazioni su come toocreate e pubblicare prodotti in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Come toocreate e pubblicazione di un prodotto in Gestione API di Azure
In Gestione API di Azure, un prodotto contiene una o più API, nonché di utilizzo della quota e hello le condizioni di utilizzo. Dopo aver pubblicato un prodotto, gli sviluppatori possono sottoscrivere toohello prodotto e iniziare l'API del prodotto di toouse hello. argomento Hello fornisce una Guida toocreating un prodotto, aggiunta di un'API e pubblicarlo per gli sviluppatori.

## <a name="create-product"> </a>Creare un prodotto
Le operazioni vengono aggiunte e configurate tooan API nel portale di server di pubblicazione hello. Fare clic su portale, server di pubblicazione di hello tooaccess **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **prodotti** menu hello in hello toodisplay sinistro hello **prodotti** pagina e fare clic su **Aggiungi prodotto**.

![Prodotti][api-management-products]

![Nuovo prodotto][api-management-add-new-product]

Immettere un nome descrittivo per il prodotto hello in hello **nome** campo e una descrizione del prodotto hello hello **descrizione** campo.

Lo stato dei prodotti in Gestione API può essere **Aperto** o **Protetto**. Prodotti protetti devono essere toobefore sottoscritti possono essere utilizzati, aperti prodotti possono essere utilizzati senza alcuna sottoscrizione. Controllare **richiedono sottoscrizione** toocreate protetto prodotto che richiede una sottoscrizione. Questo è l'impostazione predefinita hello.

Controllare **richiedono l'approvazione della sottoscrizione** se si desidera che un amministratore tooreview e accettare o rifiutare la sottoscrizione tenterà toothis prodotto. Se hello casella è deselezionata, i tentativi di sottoscrizione sarà approvata automaticamente. Per ulteriori informazioni sulle sottoscrizioni, vedere [Visualizza prodotti di sottoscrittori tooa][View subscribers tooa product].

tooallow developer account toosubscribe prodotto toohello più volte, controllare hello **può supportare più sottoscrizioni** casella di controllo. Se questa casella è deselezionata, ogni account sviluppatore possono sottoscrivere solo un prodotto toohello sola volta.

![Più sottoscrizioni senza limitazioni][api-management-unlimited-multiple-subscriptions]

numero di hello toolimit di più sottoscrizioni simultanee, controllare hello **Limita numero di sottoscrizioni simultanee** casella di controllo e immettere il limite di sottoscrizione hello. Nell'esempio seguente di hello, le sottoscrizioni simultanee sono toofour limitato per l'account sviluppatore.

![Quattro sottoscrizioni][api-management-four-multiple-subscriptions]

Dopo aver configurate tutte le nuove opzioni di prodotto, fare clic su **salvare** nuovo prodotto di toocreate hello.

![Prodotti][api-management-products-page]

> Per impostazione predefinita sono non pubblicati nuovi prodotti e sono visibile toohello solo **amministratori** gruppo.
> 
> 

tooconfigure un prodotto, fare clic sul nome del prodotto hello in hello **prodotti** scheda.

## <a name="add-apis"></a>Prodotto tooa aggiungere API
Hello **prodotti** pagina contiene quattro collegamenti per la configurazione: **riepilogo**, **impostazioni**, **visibilità**, e  **I sottoscrittori**. Hello **riepilogo** scheda è dove è possibile aggiungere le API e pubblicare o annullare la pubblicazione di un prodotto.

![Riepilogo][api-management-new-product-summary]

Prima di pubblicare il prodotto è necessario tooadd una o più API. toodo, fare clic su **tooproduct aggiungere API**.

![Aggiunta di API][api-management-add-apis-to-product]

Lo si desidera seleziona hello API e fare clic su **salvare**.

## <a name="add-description"></a>Prodotto tooa di aggiungere informazioni descrittive
Hello **impostazioni** scheda permette tooprovide informazioni dettagliate sul prodotto hello, ad esempio il suo scopo hello fornisce accesso all'API e altre informazioni utili. contenuto Hello è destinato agli sviluppatori di hello che chiameremo hello API e possono essere scritti in testo normale o markup HTML.

![Impostazioni prodotto][api-management-product-settings]

Controllare **richiedono sottoscrizione** toocreate un prodotto protetto che richiede un toobe di sottoscrizione utilizzato o non crittografato hello toocreate casella di controllo un prodotto open che può essere chiamato senza una sottoscrizione.

Selezionare **richiedono l'approvazione della sottoscrizione** se si desidera toomanually approvare tutte le richieste di sottoscrizione al prodotto. Per impostazione predefinita, tutte le sottoscrizioni al prodotto vengono concesse automaticamente.

tooallow developer account toosubscribe prodotto toohello più volte, controllare hello **può supportare più sottoscrizioni** casella di controllo e, facoltativamente, specificare un limite. Se questa casella è deselezionata, ogni account sviluppatore possono sottoscrivere solo un prodotto toohello sola volta.

Se lo si desidera compilare hello **condizioni di utilizzo** campo che descrive le condizioni di hello di utilizzo per il prodotto hello che i sottoscrittori devono accettare nel prodotto di hello toouse dell'ordine.

## <a name="publish-product"></a>Pubblicare un prodotto
Prima di poter chiamare le API di hello in un prodotto, deve essere pubblicata prodotto hello. In hello **riepilogo** per prodotto hello scheda, fare clic su **pubblica**, quindi fare clic su **Sì, pubblicarlo** tooconfirm. toomake private prodotto pubblicati in precedenza, fare clic su **Annulla pubblicazione**.

![Pubblicazione prodotto][api-management-publish-product]

## <a name="make-visible"></a>Rendere un toodevelopers visibile prodotto
Hello **visibilità** scheda permette toochoose i ruoli che sono in grado di toosee hello prodotto nel portale per sviluppatori hello e sottoscrivono toohello prodotto.

![Visibilità prodotto][api-management-product-visiblity]

tooenable o disattivare la visibilità di un prodotto per gli sviluppatori di hello in un gruppo di selezionare o deselezionare la casella di controllo hello accanto gruppo hello e quindi fare clic su **salvare**.

> Per ulteriori informazioni, vedere [come account di sviluppatore di toomanage gruppi toocreate e l'utilizzo in Gestione API di Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Prodotto tooa i sottoscrittori di visualizzazione
Hello **sottoscrittori** scheda vengono elencati gli sviluppatori di hello che hanno sottoscritto il prodotto toohello. Hello dettagli e le impostazioni per ogni sviluppatore possono essere visualizzate facendo clic sul nome dello sviluppatore hello. In questo esempio non gli sviluppatori hanno ancora sottoscritto toohello prodotto.

![Sviluppatori][api-management-developer-list]

## <a name="next-steps"></a>Passaggi successivi
Una volta hello desiderato vengono aggiunte le API e prodotto hello pubblicata, gli sviluppatori possono sottoscrivere toohello prodotto e iniziare hello toocall API. Per una dimostrazione di questi elementi e della configurazione avanzata del prodotto, vedere l'esercitazione [Come creare e configurare le impostazioni avanzate del prodotto in Gestione API di Azure][How create and configure advanced product settings in Azure API Management].

Per ulteriori informazioni sull'utilizzo dei prodotti, vedere hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
