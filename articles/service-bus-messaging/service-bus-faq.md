---
title: Domande frequenti sul bus di servizio di Azure | Microsoft Docs
description: Risposte ad alcune delle domande frequenti sul bus di servizio di Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2017
ms.author: sethm
ms.openlocfilehash: ba34938883ee342936b5c7a4568dae5e02684bb2
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="service-bus-faq"></a>Domande frequenti sul bus di servizio
Questo articolo risponde ad alcune domande frequenti sul bus di servizio di Microsoft Azure. Per informazioni generali sui prezzi e sul supporto di Azure, vedere [Domande frequenti sul supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions-about-azure-service-bus"></a>Domande generali sul bus di servizio di Azure
### <a name="what-is-azure-service-bus"></a>Cos'è il bus di servizio di Azure?
Il [bus di servizio di Azure](service-bus-messaging-overview.md) è una piattaforma cloud di messaggistica asincrona che consente di scambiare dati tra sistemi disaccoppiati. Microsoft offre questa funzionalità come servizio. Non è pertanto necessario un hardware per poterla usare.

### <a name="what-is-a-service-bus-namespace"></a>Cos'è uno spazio dei nomi del bus di servizio?
Lo [spazio dei nomi](service-bus-create-namespace-portal.md) è un contenitore per le risorse del bus di servizio all'interno dell'applicazione. La creazione di uno spazio dei nomi è necessaria per usare il bus di servizio ed è uno dei primi passaggi delle attività iniziali.

### <a name="what-is-an-azure-service-bus-queue"></a>Cos'è una coda del bus di servizio di Azure?
La [coda del bus di servizio](service-bus-queues-topics-subscriptions.md) è un'entità in cui vengono archiviati i messaggi. Le code sono utili in presenza di più applicazioni o più parti di un'applicazione distribuita che devono comunicare tra loro. La coda è simile a un centro di distribuzione perché più prodotti (messaggi) vengono ricevuti e quindi inviati da tale posizione.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?
Un argomento può essere visualizzato come coda e quando si usano più sottoscrizioni diventa un modello di messaggistica più completo. Si tratta essenzialmente di uno strumento di comunicazione uno-a-molti. Questo modello di pubblicazione/sottoscrizione, detto anche *Pub/Sub*, consente a un'applicazione che invia un messaggio a un argomento con più sottoscrizioni di garantire la ricezione di tale messaggio da parte di più applicazioni.

### <a name="what-is-a-partitioned-entity"></a>Cos'è un'entità partizionata?
Una coda o un argomento convenzionale è gestito da un singolo broker messaggi e archiviato in un archivio di messaggistica. Le [code o gli argomenti partizionati](service-bus-partitioning.md) vengono gestiti da più broker dei messaggi e salvati in più archivi di messaggistica. Questo significa che la velocità effettiva complessiva di una coda o di un argomento partizionato non è più limitata dalle prestazioni di un singolo broker messaggi o archivio di messaggistica. Inoltre, un'interruzione temporanea dell'alimentazione di un archivio di messaggistica non determina la mancanza di disponibilità di una coda o di un argomento partizionato.

Si noti che se si usano entità partizionate, l'ordinamento non è garantito. Se una partizione non è disponibile è comunque possibile inviare e ricevere messaggi da altre partizioni.

## <a name="best-practices"></a>Procedure consigliate
### <a name="what-are-some-azure-service-bus-best-practices"></a>Quali sono alcune procedure consigliate per il bus di servizio di Azure?
Consultare [Procedure consigliate per il miglioramento delle prestazioni tramite il bus di servizio][Best practices for performance improvements using Service Bus]: questo articolo descrive come ottimizzare le prestazioni durante lo scambio di messaggi.

### <a name="what-should-i-know-before-creating-entities"></a>Cosa è necessario sapere prima di creare entità?
Le proprietà seguenti di code e argomenti non sono modificabili. Tenere conto di questo limite quando si effettua il provisioning delle entità perché non è possibile apportare modifiche a queste proprietà senza creare una nuova entità sostitutiva.

* Partizionamento
* Sessioni
* Rilevamento duplicati
* Entità espressa

## <a name="pricing"></a>Prezzi
In questa sezione vengono fornite le risposte ad alcune delle domande più frequenti sul modello di prezzo del bus di servizio.

L'articolo [Informazioni sul prezzo e la fatturazione del Bus di servizio](service-bus-pricing-billing.md) spiega i metodi di fatturazione nel bus di servizio. Per informazioni specifiche sulle opzioni relative ai prezzi del bus di servizio, vedere la pagina relativa ai [prezzi del Bus di servizio](https://azure.microsoft.com/pricing/details/service-bus/).

Per informazioni generali sui prezzi di Azure, vedere le [Domande frequenti sul supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083). 

### <a name="how-do-you-charge-for-service-bus"></a>Quali sono le modalità di addebito per il bus di servizio?
Per informazioni complete sui prezzi del bus di servizio, vedere la pagina relativa ai [prezzi del Bus di servizio][Pricing overview]. Oltre ai prezzi indicati, vengono addebitati i trasferimenti di dati associati in uscita dal data center in cui è stato effettuato il provisioning dell'applicazione.

### <a name="what-usage-of-service-bus-is-subject-to-data-transfer-what-is-not"></a>Quale tipo di utilizzo del bus di servizio è soggetto all'addebito per trasferimento di dati e quale non lo è?
Qualsiasi trasferimento di dati nell'ambito di una specifica area di Azure non è soggetto ad alcun addebito, come qualsiasi trasferimento di dati verso l'interno. Il trasferimento di dati all'esterno di un'area è soggetto alle spese di uscita indicate [qui](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Per il bus di servizio viene addebitato lo spazio di archiviazione?
No, per il bus di servizio non viene addebitato lo spazio di archiviazione. È tuttavia prevista una quota che limita la quantità massima di dati che è possibile salvare in modo permanente per ogni coda e argomento. Vedere la risposta alla domanda successiva.

## <a name="quotas"></a>Quote

Per un elenco di limiti e quote del bus di servizio, vedere la [panoramica sulle quote del bus di servizio][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Sono previste quote di utilizzo per il bus di servizio?
Per impostazione predefinita, per qualsiasi servizio cloud, Microsoft imposta una quota di utilizzo mensile aggregata che viene calcolata su tutte le sottoscrizioni di un cliente. Dal momento che i limiti previsti potrebbero non essere sufficienti, è possibile rivolgersi in qualsiasi momento al servizio clienti, che identificherà le esigenze specifiche e modificherà di conseguenza i limiti. Per il bus di servizio, la quota di utilizzo aggregata è pari a 5 miliardi di messaggi al mese.

Anche se Microsoft si riserva il diritto di disabilitare l'account di un cliente che abbia superato le quote di uso previste in un determinato mese, invierà una notifica tramite posta elettronica ed effettuerà diversi tentativi per contattare il cliente prima di intraprendere qualsiasi azione. I clienti che superano tali quote saranno comunque responsabili degli addebiti delle eccedenze.

Come gli altri servizi in Azure, il bus di servizio applica un set specifico di quote per garantire un utilizzo corretto delle risorse. Per altre informazioni su queste quote, vedere la [panoramica sulle quote del bus di servizio][Quotas overview].

## <a name="troubleshooting"></a>risoluzione dei problemi
### <a name="what-are-some-of-the-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Quali sono alcune delle eccezioni generate dalle API del bus di servizio di Azure e le azioni consigliate?
Per un elenco delle possibili eccezioni del bus di servizio, vedere [Eccezioni di messaggistica del bus di servizio][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Cos'è una firma di accesso condiviso e quali linguaggi supportano la generazione di una firma?
Le firme di accesso condiviso sono un meccanismo di autenticazione basato su hash sicuri SHA-256 o URI. Per informazioni su come generare le firme in Node, PHP, Java e C\#, vedere l'articolo relativo alle [firme di accesso condiviso][Shared Access Signatures].

## <a name="subscription-and-namespace-management"></a>Gestione di sottoscrizioni e spazi dei nomi
### <a name="how-do-i-migrate-a-namespace-to-another-azure-subscription"></a>Come si esegue la migrazione di uno spazio dei nomi a un'altra sottoscrizione di Azure?

È possibile spostare uno spazio dei nomi da una sottoscrizione di Azure a un'altra usando il [portale di Azure](https://portal.azure.com) o i comandi di PowerShell. Per eseguire l'operazione, lo spazio dei nomi deve essere già attivo. L'utente che esegue i comandi deve essere un amministratore delle sottoscrizioni di origine e di destinazione.

#### <a name="portal"></a>Portale

Per usare il portale di Azure per eseguire la migrazione degli spazi dei nomi del bus di servizio a un'altra sottoscrizione, seguire le istruzioni riportate [qui](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

La sequenza di comandi PowerShell seguente sposta uno spazio dei nomi da una sottoscrizione di Azure a un'altra. Per eseguire questa operazione, lo spazio dei nomi deve essere già attivo e l'utente che esegue i comandi di PowerShell deve essere un amministratore nella sottoscrizione di origine e in quella di destinazione.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription to target subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sul bus di servizio, vedere gli articoli seguenti:

* [Introduzione ad Azure Service Bus Premium (post di blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introduzione ad Azure Service Bus Premium (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Panoramica del bus di servizio](service-bus-messaging-overview.md)
* [Bus di servizio di Azure](service-bus-fundamentals-hybrid-solutions.md)
* [Introduzione alle code del bus di servizio](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
