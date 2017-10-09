---
title: domande frequenti di inoltro aaaAzure | Documenti Microsoft
description: Ottenere risposte toosome domande frequenti su Azure inoltro.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Domande frequenti sul servizio di inoltro di Azure

Questo articolo contiene le risposte ad alcune domande frequenti sul [servizio di inoltro di Microsoft Azure](https://azure.microsoft.com/services/service-bus/). Per informazioni generali sui prezzi e sul supporto di Azure, vedere [Domande frequenti sul supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Domande generali
### <a name="what-is-azure-relay"></a>Che cos'è il servizio di inoltro di Azure?
Hello [servizio di inoltro Azure](relay-what-is-it.md) facilita applicazioni ibride, consentono in modo più sicuro di esporre servizi che risiedono all'interno di un cloud pubblico di rete toohello aziendali. È possibile esporre servizi hello senza dover aprire una connessione di firewall e senza infrastruttura della rete aziendale tooa modifiche intrusiva.

### <a name="what-is-a-relay-namespace"></a>Che cos'è uno spazio dei nomi di inoltro?
Oggetto [dello spazio dei nomi](relay-create-namespace-portal.md) è un ambito contenitore che è possibile utilizzare le risorse di inoltro tooaddress all'interno dell'applicazione. È necessario creare un inoltro di toouse dello spazio dei nomi. Questo è uno dei primi passaggi di hello nella Guida introduttiva.

### <a name="what-happened-tooservice-bus-relay-service"></a>Il servizio di inoltro del Bus di tooService verificato anomalo?
Hello in precedenza denominato servizio di inoltro del Bus di servizio è ora denominata inoltro WCF. È possibile continuare toouse questo servizio come di consueto. funzionalità di connessioni ibride Hello è una versione aggiornata di un servizio che è stata essere applicato dai servizi BizTalk di Azure. Inoltro di WCF e le connessioni ibride continuare toobe supportato.

## <a name="pricing"></a>Prezzi
Questo consente di individuare sezione alcune domande frequenti su hello inoltro struttura dei prezzi. Per informazioni generali sui prezzi di Azure, vedere [Domande frequenti sul supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083). Per informazioni complete sui prezzi del servizio di inoltro, vedere la pagina contenente i [dettagli dei prezzi del bus di servizio][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Come vengono addebitati i costi di Connessioni ibride e Inoltro WCF?
Per informazioni complete sui prezzi di inoltro, vedere hello [connessioni ibride e inoltri WCF] [ Pricing overview] tabella nella pagina dettagli sui prezzi di hello Bus di servizio. Inoltre toohello prezzi indicati in questa pagina vengono addebitati i trasferimenti dati associati in uscita datacenter hello in cui viene eseguito il provisioning dell'applicazione.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Come viene fatturato l'uso di Connessioni ibride?
Ecco tre scenari di fatturazione di esempio per Connessioni ibride:

*   Scenario 1:
    *   Si dispone di un listener singolo, ad esempio un'istanza di gestione di connessioni ibride installato e in esecuzione continua per un mese intero hello hello.
    *   3 GB di dati inviati attraverso la connessione hello durante il mese di hello. 
    *   Il costo totale è $ 5.
*   Scenario 2:
    *   Si dispone di un listener singolo, ad esempio un'istanza di gestione di connessioni ibride installato e in esecuzione continua per un mese intero hello hello.
    *   10 GB di dati inviati attraverso la connessione hello durante il mese di hello.
    *   Il costo totale è $ 7,50, Primi 5 GB + $2,50 per hello aggiuntive 5 GB di dati che è $5 per la connessione hello.
*   Scenario 3:
    *   Si dispone di due istanze, A e B, di gestione di connessioni ibride installato e in esecuzione continua per un mese intero hello hello.
    *   3 GB di dati inviati attraverso la connessione A durante il mese di hello.
    *   6 GB di dati inviati attraverso la connessione B mese hello.
    *   Il costo totale è $ 10,50, Che è di $5 per la connessione A + $5 per la connessione B + $0,50 (per gigabyte di sesto hello in connessione B).

Si noti che prezzi hello utilizzati negli esempi di hello sono applicabili solo durante il periodo di anteprima di hello connessioni ibride. I prezzi sono toochange soggetto alla disponibilità generale di connessioni ibride.

### <a name="how-are-hours-calculated-for-relay"></a>Come vengono calcolate le ore per l'inoltro?

L'inoltro WCF è disponibile solo negli spazi dei nomi di livello Standard. Prezzi e [quote di connessione](../service-bus-messaging/service-bus-quotas.md) per i servizi di inoltro restano invariati in caso contrario. Ciò significa che gli inoltri continuare toobe addebitato in base al numero di hello dei messaggi (non di operazioni) e ore di inoltro. Per ulteriori informazioni, vedere hello ["Connessioni ibride e inoltri WCF"](https://azure.microsoft.com/pricing/details/service-bus/) tabella nella pagina dei dettagli dei prezzi hello.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>Cosa accade se si dispone di più di inoltro specifico del listener di tooa connessi?
In alcuni casi, a un singolo inoltro possono essere connessi più listener. Un inoltro viene considerato aperto quando almeno un listener di inoltro è tooit connesso. Aggiungono i risultati di inoltro tooan listener in ore di inoltro aggiuntive. numero di Hello di inoltro mittenti (i client che richiamano o invia messaggi toorelays) che sono connessi tooa inoltro non influisce sul calcolo hello delle ore di inoltro.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Come è hello messaggi calcolati per gli inoltri WCF?
(**Si applica solo a tooWCF inoltri. I messaggi non implicano un costo per Connessioni ibride.**

In generale, i messaggi fatturabili per gli inoltri vengono calcolati utilizzando hello stesso metodo utilizzato per negoziata entità (code, argomenti e sottoscrizioni), descritta in precedenza. Esistono tuttavia alcune differenze significative.

L'invio di un inoltro del Bus di servizio tooa messaggio viene considerato come un "completa tramite" trasmissione toohello i listener di inoltro che riceve il messaggio hello. Non viene considerato come un trasmissione operazione toohello inoltro di Service Bus, seguito da un listener di inoltro toohello di recapito. Una chiamata di servizio di tipo request / reply (di backup too64 KB) contro un risultati listener di inoltro in due messaggi fatturabili: un unico messaggio fatturabile per la richiesta di hello e un unico messaggio fatturabile per la risposta hello (presupponendo che la risposta hello è 64 KB o inferiore). Questa è diversa rispetto all'utilizzo di una coda toomediate tra un client e un servizio. Se si utilizza un toomediate coda tra un client e un servizio, hello stesso modello request / reply è necessaria una richiesta trasmissione toohello coda, seguita da un'operazione di rimozione dalla coda/recapito dal servizio di toohello coda hello. È seguito da una coda di risposta trasmissione tooanother e un'operazione di rimozione dalla coda/recapito provenienti da client toohello coda. Utilizza hello stesse dimensioni presupposti (backup too64 KB), hello mediato risultati modello coda 4 messaggi fatturabili. Per la fatturazione per due volte il numero hello di hello tooimplement messaggi che stesso criterio che vengono completate tramite inoltro. Naturalmente, esistono vantaggi toousing code tooachieve questo modello, ad esempio la durabilità e livellamento del carico. Questi vantaggi potrebbero giustificare i costi aggiuntivi hello.

Gli inoltri aperti tramite hello **netTCPRelay** binding WCF considerano i messaggi non come singoli messaggi, ma come un flusso di dati che passano attraverso il sistema hello. Quando si usa questa associazione, solo hello mittente e il listener hanno visibilità framing hello di hello singoli messaggi inviati e ricevuti. Per gli inoltri che usano hello **netTCPRelay** tutti i dati di associazione, viene considerato come un flusso per il calcolo dei messaggi fatturabili. In questo caso, il Bus di servizio Calcola quantità totale di hello di dati inviati o ricevuti attraverso ciascun inoltro a intervalli di 5 minuti. Quindi, divide tale quantità totale di dati da 64 KB toodetermine hello numerosi messaggi fatturabili per tale inoltro durante tale periodo di tempo.

## <a name="quotas"></a>Quote
| Nome della quota | Scope | Tipo | Comportamento in caso di superamento | Valore |
| --- | --- | --- | --- | --- |
| Listener simultanei per un inoltro |Entità |statico |Le richieste successive per le connessioni aggiuntive verranno rifiutate e chiamata di codice hello viene restituita un'eccezione. |25 |
| Listener di inoltro simultanei |A livello di sistema |statico |Le richieste successive per le connessioni aggiuntive verranno rifiutate e chiamata di codice hello viene restituita un'eccezione. |2.000 |
| Connessioni di inoltro simultanee per tutti gli endpoint di inoltro in uno spazio dei nomi del servizio |A livello di sistema |statico |- |5.000 |
| Endpoint di inoltro per ogni spazio dei nomi del servizio |A livello di sistema |statico |- |10.000 |
| Dimensione dei messaggi per gli inoltri [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) e [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) |A livello di sistema |statico |I messaggi in arrivo che superano queste quote vengono rifiutati e chiamata di codice hello viene restituita un'eccezione. |64 KB |
| Dimensione dei messaggi per gli inoltri [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) e [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) |A livello di sistema |statico |- |Illimitato |

### <a name="does-relay-have-any-usage-quotas"></a>Per il servizio di inoltro sono previste quote di utilizzo?
Per impostazione predefinita per qualsiasi servizio cloud, Microsoft imposta una quota di utilizzo mensile aggregata che viene calcolata su tutte le sottoscrizioni di un cliente. In alcuni casi le esigenze del cliente possono superare questi limiti. È possibile contattare il servizio clienti in qualsiasi momento per comunicare esigenze specifiche e consentire un adeguamento appropriato di tali limiti. Per il Bus di servizio, le quote di utilizzo aggregate hello sono i seguenti:

* 5 miliardi di messaggi
* 2 milioni di ore di inoltro

Anche se Microsoft si riserva hello destra toodisable un account che supera le relative quote di utilizzo mensile, è fornire la notifica di posta elettronica e si rende più clienti di hello toocontact tentativi prima di eseguire alcuna azione. I clienti che superano tali quote saranno comunque responsabili degli addebiti delle eccedenze.

### <a name="naming-restrictions"></a>Limitazioni relative all'assegnazione dei nomi
Lo spazio dei nomi dell'inoltro deve avere una lunghezza compresa tra 6 e 50 caratteri.

## <a name="subscription-and-namespace-management"></a>Gestione di sottoscrizioni e spazi dei nomi
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Migrazione di una sottoscrizione di Azure di tooanother dello spazio dei nomi

toomove uno spazio dei nomi da una sottoscrizione di tooanother sottoscrizione di Azure, è possibile l'uso hello [portale di Azure](https://portal.azure.com) o utilizzare i comandi di PowerShell. toomove una sottoscrizione di tooanother dello spazio dei nomi, hello dello spazio dei nomi deve essere già attivo. utente di Hello hello comandi deve essere un utente amministratore in entrambe le sottoscrizioni di origine e destinazione hello.

#### <a name="azure-portal"></a>Portale di Azure

toouse hello Azure toomigrate portale Azure inoltro gli spazi dei nomi sottoscrizione tooanother una sottoscrizione, vedere [spostare le risorse tooa nuovo gruppo di risorse o sottoscrizione](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove uno spazio dei nomi da sottoscrizione tooanother una sottoscrizione di Azure, utilizzare hello seguente sequenza di comandi. tooexecute questa operazione, hello dello spazio dei nomi deve già essere attivo e hello utente che esegue i comandi di PowerShell hello deve essere un amministratore in entrambe le sottoscrizioni di origine e destinazione hello.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Quali sono alcune eccezioni hello generati dalle API di inoltro di Azure e suggerito azioni da che eseguire?
Per una descrizione di eccezioni comuni e delle azioni consigliate, vedere [Eccezioni di inoltro][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>Che cos'è una firma di accesso condiviso, e quali lingue è possibile usare una firma toogenerate?
Le firme di accesso condiviso sono un meccanismo di autenticazione basato su hash sicuri SHA-256 o URI. Per informazioni su come toogenerate propria firme nel nodo, PHP, Java, C e c#, vedere [l'autenticazione del Bus di servizio con firme di accesso condiviso][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>È possibile toowhitelist gli endpoint di inoltro?
Sì. client di inoltro Hello stabilisce le connessioni del servizio di inoltro Azure toohello con i nomi di dominio completo. I clienti possono quindi aggiungere una voce per `*.servicebus.windows.net` nei firewall che supportano l'aggiunta all'elenco elementi consentiti per DNS.

## <a name="next-steps"></a>Passaggi successivi
* [Creare uno spazio dei nomi](relay-create-namespace-portal.md)
* [Introduzione a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introduzione a Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md