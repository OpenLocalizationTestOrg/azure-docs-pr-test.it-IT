---
title: aaaProtect dell'API di gestione API di Azure | Documenti Microsoft
description: "Informazioni su come tooprotect dell'API di quote e limitazioni (limitazione di velocità) di criteri."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Proteggere le API con limiti di frequenza usando Gestione API di Azure
Questa guida viene illustrato come è facile tooadd protezione per l'API di back-end mediante criteri di limite e quota velocità con gestione API di Azure.

In questa esercitazione si creerà un prodotto di "Versione di valutazione gratuita" API che consente agli sviluppatori toomake backup too10 chiamate al minuto e backup tooa massimo di 200 chiamate alla settimana tooyour API utilizzando hello [frequenza delle chiamate limite per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [ Quota di utilizzo di set per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) criteri. Verrà quindi pubblicare API hello e testare i criteri di limite di frequenza hello.

Più avanzati la limitazione delle richieste di scenari con hello [frequenza limite dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) criteri, vedere [richiesta avanzata di limitazione delle richieste a gestione API di Azure](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate un prodotto
In questo passaggio si creerà un prodotto con una versione di valutazione gratuita che non richiede l'approvazione della sottoscrizione.

> [!NOTE]
> Se si già dispone di un prodotto configurato e si desidera toouse che per questa esercitazione, è possibile passare troppo[Configura frequenza delle chiamate per i criteri di limite e quota] [ Configure call rate limit and quota policies] e seguire l'esercitazione hello da lì, con il prodotto al posto del prodotto di valutazione gratuita di hello.
> 
> 

tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [gestione API in Gestione API di Azure prima] [ Manage your first API in Azure API Management] esercitazione.
> 
> 

Fare clic su **prodotti** in hello **gestione API** menu hello toodisplay sinistro hello **prodotti** pagina.

![Add product][api-management-add-product]

Fare clic su **Aggiungi prodotto** toodisplay hello **Aggiungi nuovo prodotto** la finestra di dialogo.

![Aggiungi nuovo prodotto][api-management-new-product-window]

In hello **titolo** digitare **versione di valutazione gratuita**.

In hello **descrizione** casella, hello di tipo testo seguente: **i sottoscrittori non saranno in grado di toorun 10 chiamate al minuto backup tooa massimo di 200 chiamate/settimana dopo il quale viene negato l'accesso.**

Lo stato dei prodotti in Gestione API può essere Aperto o Protetto. Prodotti protetti devono essere toobefore sottoscritti possono essere utilizzati. mentre i prodotti aperti possono essere usati senza sottoscrizione. Verificare che **richiedono sottoscrizione** è toocreate selezionato un prodotto protetto che richiede una sottoscrizione. Questo è l'impostazione predefinita hello.

Se si desidera che un amministratore tooreview e accettare o rifiutare la sottoscrizione tenta toothis prodotto, selezionare **richiedono l'approvazione della sottoscrizione**. Se la casella di controllo hello non è selezionata, i tentativi di sottoscrizione sarà approvata automaticamente. In questo esempio, le sottoscrizioni vengono approvate automaticamente, in modo non si seleziona la casella hello.

sviluppatore tooallow account toosubscribe nuovo prodotto toohello più volte, seleziona hello **può supportare più sottoscrizioni simultanee** casella di controllo. Questa esercitazione non prevede l'uso di più sottoscrizioni simultanee, quindi lasciare la casella deselezionata.

Dopo avere immesso tutti i valori, fare clic su **salvare** prodotto hello toocreate.

![Product added][api-management-product-added]

Per impostazione predefinita, i nuovi prodotti sono toousers visibile in hello **amministratori** gruppo. Verrà hello tooadd **sviluppatori** gruppo. Fare clic su **versione di valutazione gratuita**, quindi fare clic su hello **visibilità** scheda.

> In Gestione API, i gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers. Prodotti concedono toogroups visibilità e gli sviluppatori possono visualizzare e sottoscrivere i prodotti toohello toohello visibili i gruppi in cui appartengono. Per ulteriori informazioni, vedere [come toocreate e utilizzare i gruppi in Gestione API di Azure][How toocreate and use groups in Azure API Management].
> 
> 

![Add developers group][api-management-add-developers-group]

Seleziona hello **sviluppatori** casella di controllo e quindi fare clic su **salvare**.

## <a name="add-api"></a>tooadd un'API toohello prodotto
In questo passaggio dell'esercitazione hello, si aggiungeranno hello API Echo toohello nuova versione di valutazione gratuita del prodotto.

> Ogni istanza del servizio Gestione API preconfigurata con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API. Per altre informazioni, vedere [Gestire la prima API in Gestione API di Azure][Manage your first API in Azure API Management].
> 
> 

Fare clic su **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **versione di valutazione gratuita** prodotto hello tooconfigure.

![Configure product][api-management-configure-product]

Fare clic su **tooproduct aggiungere API**.

![Aggiungere tooproduct API][api-management-add-api]

Selezionare **Echo API** (API Echo) e quindi fare clic su **Salva**.

![Add Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure criteri di limite e quota di frequenza delle chiamate
I limiti di velocità e le quote sono configurate nell'editor Criteri di hello. i criteri di Hello due verrà aggiunta in questa esercitazione sono hello [frequenza delle chiamate limite per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [Set quota di utilizzo per ogni sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) criteri. Nell'ambito del prodotto hello, è necessario applicare questi criteri.

Fare clic su **criteri** in hello **gestione API** menu di sinistra hello. In hello **prodotto** elenco, fare clic su **versione di valutazione gratuita**.

![Product policy][api-management-product-policy]

Fare clic su **Aggiungi criterio** tooimport hello modello di criteri e avviare la creazione di criteri di limite e una quota di frequenza hello.

![Aggiungi criteri][api-management-add-policy]

Frequenza limite e quota criteri vengono in ingresso, in tal caso posizione hello cursore nell'elemento di hello in ingresso.

![Policy editor][api-management-policy-editor-inbound]

Scorrere l'elenco di hello dei criteri e individuare hello **frequenza delle chiamate limite per ogni sottoscrizione** voce di criterio.

![Policy statements][api-management-limit-policies]

Dopo aver hello cursore viene posizionato nel hello **in ingresso** elemento dei criteri, fare clic sulla freccia di hello accanto a **frequenza delle chiamate limite per ogni sottoscrizione** tooinsert il relativo modello di criteri.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Come si può vedere dal frammento di codice hello, criteri hello consentono l'impostazione dei limiti per le API del prodotto hello e le operazioni. In questa esercitazione è non utilizzare tale funzionalità, quindi eliminare hello **api** e **operazione** gli elementi da hello **limite di velocità** elemento, tale che solo hello outer **limite di velocità** rimarrà elemento, come illustrato nell'esempio seguente hello.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Nel prodotto di valutazione gratuita di hello, frequenza massima consentita di chiamata hello è 10 chiamate al minuto, quindi digitare **10** come valore hello hello **chiamate** attributo, e **60** per hello **periodo di rinnovo** attributo.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

hello tooconfigure **Set quota di utilizzo per ogni sottoscrizione** criteri, posizione del cursore immediatamente di sotto di hello appena aggiunti **limite di velocità** elemento all'interno di hello **in ingresso** elemento, quindi individuare e fare clic su hello freccia toohello sinistro **Set quota di utilizzo per ogni sottoscrizione**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Allo stesso modo toohello **Set quota di utilizzo per ogni sottoscrizione** criteri, **Set quota di utilizzo per ogni sottoscrizione** criteri consentono l'impostazione di delimitatori per le API del prodotto hello e operazioni. In questa esercitazione è non utilizzare tale funzionalità, quindi eliminare hello **api** e **operazione** gli elementi da hello **quota** elemento, come illustrato nell'esempio seguente hello.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Le quote possono essere basate sul numero di hello chiamate per intervallo, la larghezza di banda o entrambi. In questa esercitazione è non stiamo la limitazione della larghezza di banda in base, quindi eliminare hello **della larghezza di banda** attributo.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Nel prodotto di valutazione gratuita di hello, quota hello è 200 chiamate alla settimana. Specificare **200** come valore hello hello **chiamate** attributo e quindi specificare **604800** come valore hello hello **periodo di rinnovo** attributo.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Gli intervalli dei criteri sono specificati in secondi. intervallo di hello toocalculate per una settimana, è possibile moltiplicare hello numero di giorni (7 tramite un numero di ore del giorno (24) tramite un numero di minuti in un'ora (60) tramite un numero di secondi in un minuto (60) hello hello hello): 7 * 24 * 60 * 60 = 604800.
> 
> 

Al termine della configurazione dei criteri di hello, deve corrispondere a hello di esempio seguente.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Dopo hello desiderato sono configurati i criteri, fare clic su **salvare**.

![Save policy][api-management-policy-save]

## <a name="publish-product"></a> prodotto hello toopublish
Ora che hello hello API vengono aggiunti e configurati i criteri di hello, prodotto hello deve essere pubblicata in modo che possono essere usata dagli sviluppatori. Fare clic su **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **versione di valutazione gratuita** prodotto hello tooconfigure.

![Configure product][api-management-configure-product]

Fare clic su **pubblica**, quindi fare clic su **Sì, pubblicarlo** tooconfirm.

![Pubblicazione prodotto][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe un prodotto di toohello account sviluppatore
Ora prodotto hello viene pubblicato, è disponibile toobe sottoscritto tooand utilizzato dagli sviluppatori.

> Gli amministratori di un'istanza di gestione API sono prodotto tooevery automaticamente sottoscritto. In questo passaggio dell'esercitazione, verrà sottoscrivere uno dei prodotti di hello developer non amministratore account toohello versione di valutazione gratuita. Se l'account sviluppatore fa parte del ruolo amministratori di hello, è possibile proseguire con questo passaggio, anche se già iscritto.
> 
> 

Fare clic su **utenti** su hello **gestione API** menu hello a sinistra e quindi fare clic su nome hello del tuo account sviluppatore. In questo esempio, utilizziamo hello **Clayton Gragg** account sviluppatore.

![Configure developer][api-management-configure-developer]

Fare clic su **Aggiungi sottoscrizione**.

![Aggiungi sottoscrizione][api-management-add-subscription-menu]

Selezionare **Free Trial** e quindi fare clic su **Sottoscrivi**.

![Aggiungi sottoscrizione][api-management-add-subscription]

> [!NOTE]
> In questa esercitazione, più sottoscrizioni simultanee non sono abilitate per il prodotto di valutazione gratuita di hello. In questo caso, sarebbe sottoscrizione hello tooname richiesta, come illustrato nell'esempio seguente hello.
> 
> 

![Aggiungi sottoscrizione][api-management-add-subscription-multiple]

Dopo aver fatto clic **Sottoscrivi**, hello prodotto viene visualizzato in hello **sottoscrizione** elenco per l'utente hello.

![Sottoscrizione aggiunta][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall un limite di frequenza hello operazione e di test
Ora che hello prodotto di valutazione gratuita è configurato e pubblicato, è possibile chiamare alcune operazioni e testare i criteri di limite di frequenza hello.
Portale per sviluppatori di toohello commutatore facendo **portale per sviluppatori** nel menu superiore destro di hello.

![Portale per sviluppatori][api-management-developer-portal-menu]

Fare clic su **API** in hello menu superiore e quindi fare clic su **API Echo**.

![Portale per sviluppatori][api-management-developer-portal-api-menu]

Fare clic su **GET Resource** (GET su risorsa) e quindi su **Prova**.

![Open console][api-management-open-console]

Mantenere i valori dei parametri di valore predefinito di hello e quindi selezionare la chiave di sottoscrizione per il prodotto di valutazione gratuita di hello.

![Chiave della sottoscrizione][api-management-select-key]

> [!NOTE]
> Se si dispone di più sottoscrizioni, essere certi tooselect hello chiave **versione di valutazione gratuita**, o altri criteri hello che sono stati configurati nei passaggi precedenti hello sarà attiva.
> 
> 

Fare clic su **inviare**e quindi visualizzare la risposta hello. Hello nota **stato della risposta** di **200 OK**.

![Operation results][api-management-http-get-results]

Fare clic su **inviare** con una frequenza maggiore di criteri di limite di frequenza hello di 10 chiamate al minuto. Criteri di limite di frequenza hello vengano superato, lo stato della risposta **429 troppo numerose richieste** viene restituito.

![Operation results][api-management-http-get-429]

Hello **contenuto della risposta** indica hello rimanenti intervallo prima di tentativi sarà ha esito positivo.

Quando il criterio di limite di velocità di hello di 10 chiamate al minuto è attivo, le chiamate successive avrà esito negativo fino a 60 secondi trascorsi da hello prima del prodotto prima è stato superato il limite di velocità hello di hello 10 chiamate con esito positivo toohello. In questo esempio hello rimanenti intervallo è 54 secondi.

## <a name="next-steps"></a>Passaggi successivi
* Osservare una dimostrazione dell'impostazione di limiti di velocità e le quote in hello seguente video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
