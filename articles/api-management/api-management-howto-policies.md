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
# <a name="policies-in-azure-api-management"></a>Criteri in Gestione API di Azure
In Gestione API di Azure, i criteri sono una potente funzionalità del sistema hello che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione. I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API. Le istruzioni più comuni includono la conversione di formato da XML tooJSON e limitare toorestrict hello quantità di chiamate in ingresso da uno sviluppatore di frequenza delle chiamate. Viene fornita hello disponibili molti altri criteri.

Vedere hello [Policy Reference] [ Policy Reference] per un elenco completo delle istruzioni dei criteri e le relative impostazioni.

I criteri vengono applicati all'interno di gateway hello che si trova tra i consumer di API hello e API hello gestito. riceve tutte le richieste Hello gateway, in genere inoltrandoli inalterato toohello API sottostante. Tuttavia, possibile applicare un criterio di modifiche tooboth hello in ingresso richiesta e risposta in uscita.

Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello. Alcuni criteri, ad esempio hello [flusso di controllo] [ Control flow] e [Imposta variabile] [ Set variable] criteri sono basati su espressioni di criteri. Per altre informazioni, vedere [Criteri avanzati][Advanced policies] e [Espressioni di criteri][Policy expressions].

## <a name="scopes"></a>Come tooconfigure criteri
È possibile configurare i criteri a livello globale o nell'ambito di hello di un [prodotto][Product], [API] [ API] o [operazione] [Operation]. tooconfigure un criterio, passare a editor Criteri di toohello nel portale di pubblicazione hello.

![Menu Criteri][policies-menu]

editor Criteri di Hello è costituito da tre sezioni principali: hello criteri (superiore), hello criteri definizione dell'ambito in cui i criteri vengono modificati (a sinistra) e le istruzioni di hello elenco (a destra):

![Editor criteri][policies-editor]

toobegin un criterio, che è innanzitutto necessario selezionare l'ambito di hello in cui hello è consigliabile applicare criteri di configurazione. Nella schermata di hello seguito hello **Starter** prodotto selezionato. Si noti che nome hello quadrato simbolo successivo toohello criteri indica che un criterio è già stato applicato a questo livello.

![Scope][policies-scope]

Poiché è già stato applicato un criterio, configurazione hello è mostrati nella visualizzazione di definizione di hello.

![Configurare][policies-configure]

Hello criterio viene visualizzato in sola lettura prima. In ordine tooedit definizione hello, fare clic su hello **configura i criteri di** azione.

![Modificare][policies-edit]

definizione dei criteri Hello è un semplice documento XML che descrive una sequenza di istruzioni in ingresso e in uscita. Hello XML può essere modificata direttamente nella finestra di definizione hello. Un elenco di istruzioni viene fornito toohello destra e ambito di istruzioni toohello applicabile corrente sono abilitati, evidenziati; come illustrato da hello **limite di velocità di chiamare** istruzione hello schermata precedente.

Fare clic su un'istruzione abilitata aggiungerà hello XML appropriato nella posizione di hello del cursore hello nella visualizzazione definizione hello. 

> [!NOTE]
> Se i criteri di hello che si desidera tooadd non sono abilitato, verificare di essere nell'ambito corretto di hello per tale criterio. Ogni istruzione di criterio è progettata per essere usata in determinati ambiti e sezioni dei criteri. sezioni del criterio tooreview hello e gli ambiti per i criteri, controllare hello **utilizzo** sezione relativo hello [Policy Reference][Policy Reference].
> 
> 

Un elenco completo delle istruzioni dei criteri e le relative impostazioni sono disponibili in hello [Policy Reference][Policy Reference].

Ad esempio, tooadd un toorestrict istruzione nuova in ingresso richiede indirizzi IP toospecified, posizionare il cursore hello solo all'interno del contenuto di hello di hello `inbound` hello di elemento e fare clic su XML **chiamante limitare gli indirizzi IP** istruzione.

![Criteri di restrizione][policies-restrict]

Verrà aggiunta una toohello frammento XML `inbound` elemento che fornisce indicazioni su come tooconfigure hello istruzione.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit le richieste in ingresso e accettare solo quelli da un indirizzo IP di 1.2.3.4 modificare hello XML come segue:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salva][policies-save]

Una volta completata la configurazione di istruzioni hello per criteri di hello, fare clic su **salvare** e modifiche hello saranno gateway di gestione API toohello propagate immediatamente.

## <a name="sections"> </a>Informazioni sulla configurazione dei criteri
Un criterio è una serie di istruzioni eseguite in un determinato ordine in relazione a una richiesta e una risposta. configurazione di Hello è suddivisa in modo appropriato `inbound`, `backend`, `outbound`, e `on-error` sezioni come illustrato nella seguente configurazione hello.

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

Se si verifica un errore durante l'elaborazione di hello di una richiesta, tutti i rimanenti passaggi hello `inbound`, `backend`, o `outbound` sezioni vengono ignorate e l'esecuzione passa istruzioni toohello hello `on-error` sezione. Inserendo istruzioni dei criteri in hello `on-error` sezione è possibile esaminare l'errore hello utilizzando hello `context.LastError` proprietà, esaminare e personalizzare risposta di errore di hello utilizzando hello `set-body` , criteri e configurare che cosa accade se si verifica un errore. Sono disponibili codici di errore per i passaggi predefiniti e gli errori che possono verificarsi durante l'elaborazione di hello delle istruzioni dei criteri. Per altre informazioni, vedere [Gestione degli errori nei criteri di Gestione API](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Poiché è possibile specificare i criteri a livelli diversi (globale, prodotto, api e operation) configurazione hello offre un modo per si ordine hello toospecify in cui vengono eseguite le istruzioni di definizione dei criteri hello con i criteri di riguardo toohello padre. 

Ambiti del criterio vengono valutati nell'ordine hello.

1. Ambito globale
2. Ambito del prodotto
3. Ambito dell’API
4. Ambito dell'operazione

salve le istruzioni all'interno di essi vengono valutate in base a posizione toohello di hello `base` elemento, se presente. Criteri globali dispone di alcun criterio padre e l'utilizzo di hello `<base>` elemento in esso non ha alcun effetto.

Ad esempio, se si dispone di un criterio a livello globale di hello e configurato un criterio per un'API, quindi ogni volta che viene utilizzato tale API specifica entrambi i criteri diventeranno. Consente di gestione API per l'ordinamento deterministica delle istruzioni dei criteri combinati tramite l'elemento di base hello. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Nella definizione di criteri esempio hello sopra, hello `cross-domain` istruzione verrebbe eseguito prima che tutti i criteri superiore che a sua volta, potrebbe essere seguito da hello `find-and-replace` criteri. 

Fare clic su criteri hello toosee nell'ambito corrente di hello in editor Criteri di hello **ricalcolare il criterio effettivo per l'ambito selezionato**.

## <a name="next-steps"></a>Passaggi successivi
Vedere il video seguente sulle espressioni di criteri.

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
