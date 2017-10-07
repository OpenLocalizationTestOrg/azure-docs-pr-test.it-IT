---
title: domande frequenti (FAQ) di Service Bus aaaAzure | Documenti Microsoft
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
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Domande frequenti sul bus di servizio
Questo articolo risponde ad alcune domande frequenti sul bus di servizio di Microsoft Azure. È inoltre possibile visitare hello [domande frequenti su supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083) per informazioni generali su Azure prezzi e supporto.

## <a name="general-questions-about-azure-service-bus"></a>Domande generali sul bus di servizio di Azure
### <a name="what-is-azure-service-bus"></a>Cos'è il bus di servizio di Azure?
[Azure Service Bus](service-bus-messaging-overview.md) è una piattaforma cloud di messaggistica asincrona che consente di toosend dati tra sistemi separati. Microsoft offre questa funzionalità come servizio, il che significa che non è necessario toohost qualsiasi dell'hardware in ordine toouse è.

### <a name="what-is-a-service-bus-namespace"></a>Cos'è uno spazio dei nomi del bus di servizio?
Lo [spazio dei nomi](service-bus-create-namespace-portal.md) è un contenitore per le risorse del bus di servizio all'interno dell'applicazione. Crearne uno nuovo, è necessario toouse Bus di servizio e sarà uno dei hello primi passaggi della Guida introduttiva.

### <a name="what-is-an-azure-service-bus-queue"></a>Cos'è una coda del bus di servizio di Azure?
La [coda del bus di servizio](service-bus-queues-topics-subscriptions.md) è un'entità in cui vengono archiviati i messaggi. Le code sono particolarmente utili quando si dispone di più applicazioni o più parti di un'applicazione distribuita che devono toocommunicate tra loro. coda Hello è simile tooa del centro di distribuzione in più prodotti (messaggi) vengono ricevuti e quindi inviati da tale posizione.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?
Un argomento può essere visualizzato come coda e quando si usano più sottoscrizioni diventa un modello di messaggistica più completo. Si tratta essenzialmente di uno strumento di comunicazione uno-a-molti. Questo modello di pubblicazione/sottoscrizione (o *pub/sub*) consente a un'applicazione che invia un argomento con più sottoscrizioni toohave tooa al messaggio di tale messaggio ricevuto da più applicazioni.

### <a name="what-is-a-partitioned-entity"></a>Cos'è un'entità partizionata?
Una coda o un argomento convenzionale è gestito da un singolo broker messaggi e archiviato in un archivio di messaggistica. Le [code o gli argomenti partizionati](service-bus-partitioning.md) vengono gestiti da più broker dei messaggi e salvati in più archivi di messaggistica. Ciò significa che hello velocità effettiva complessiva di una coda o argomento partizionato non è più limitata dalle prestazioni hello di un singolo broker messaggi o archivio di messaggistica. Inoltre, un'interruzione temporanea dell'alimentazione di un archivio di messaggistica non determina la mancanza di disponibilità di una coda o di un argomento partizionato.

Se si usano entità di partizionamento, l'ordinamento non è garantito. Nell'evento hello che una partizione non è disponibile, è comunque possibile inviare e ricevere messaggi da hello altre partizioni.

## <a name="best-practices"></a>Procedure consigliate
### <a name="what-are-some-azure-service-bus-best-practices"></a>Quali sono alcune procedure consigliate per il bus di servizio di Azure?
* [Procedure consigliate per migliorare le prestazioni tramite il Bus di servizio] [ Best practices for performance improvements using Service Bus] – in questo articolo viene descritto come toooptimize prestazioni durante lo scambio di messaggi.

### <a name="what-should-i-know-before-creating-entities"></a>Cosa è necessario sapere prima di creare entità?
Hello seguenti proprietà di una coda e un argomento non sono modificabile. Tenerne conto quando si effettua il provisioning delle entità perché non è possibile apportare modifiche senza creare una nuova entità sostitutiva.

* Dimensione
* Partizionamento
* Sessioni
* Rilevamento duplicati
* Entità espressa

## <a name="pricing"></a>Prezzi
In questa sezione data risposta ad alcune domande frequenti sulla struttura dei prezzi di hello Bus di servizio.

Hello [Bus di servizio prezzi e fatturazione](service-bus-pricing-billing.md) articolo spiega metri di fatturazione hello nel Bus di servizio e per informazioni sui prezzi di opzioni di Service Bus, vedere [dettagli prezzi di Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).

È inoltre possibile visitare hello [domande frequenti su supporto di Azure](http://go.microsoft.com/fwlink/?LinkID=185083) per Azure generale informazioni sui prezzi. 

### <a name="how-do-you-charge-for-service-bus"></a>Quali sono le modalità di addebito per il bus di servizio?
Per informazioni complete sui prezzi del bus di servizio, vedere la pagina relativa ai [prezzi del bus di servizio][Pricing overview]. Inoltre i prezzi toohello notare, vengono addebitati i trasferimenti dati associati in uscita hello data center in cui viene eseguito il provisioning dell'applicazione.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Quale tipo di utilizzo del Bus di servizio è trasferimento toodata soggetto? e quale non lo è?
Qualsiasi trasferimento di dati nell'ambito di una specifica area di Azure non è soggetto ad alcun addebito, come qualsiasi trasferimento di dati verso l'interno. Trasferimento dei dati all'esterno di un'area è addebiti tooegress di oggetto che possono essere trovati [qui](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Per il bus di servizio viene addebitato lo spazio di archiviazione?
No, per il bus di servizio non viene addebitato lo spazio di archiviazione. Tuttavia, è una quota limitazione hello quantità massima di dati che possono essere resa persistente per ogni coda o un argomento. Vedere hello domande frequenti.

## <a name="quotas"></a>Quote

Per un elenco di Service Bus limiti e quote, vedere hello [Cenni preliminari sulle quote di Service Bus][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Sono previste quote di utilizzo per il bus di servizio?
Per impostazione predefinita, per qualsiasi servizio cloud, Microsoft imposta una quota di utilizzo mensile aggregata che viene calcolata su tutte le sottoscrizioni di un cliente. Dal momento che i limiti previsti potrebbero non essere sufficienti, è possibile rivolgersi in qualsiasi momento al servizio clienti, che identificherà le esigenze specifiche e modificherà di conseguenza i limiti. Per il Bus di servizio, la quota di utilizzo aggregate hello è 5 miliardi di messaggi al mese.

Mentre si riserva hello destra toodisable un account cliente che ha superato le relative quote di utilizzo in un determinato mese, verrà notifiche tramite posta elettronica e rendere più tentativi toocontact un cliente prima di eseguire alcuna azione. I clienti che superano tali quote saranno comunque responsabili per gli addebiti che superano le quote di hello.

Come con altri servizi in Azure, Bus di servizio applica un set specifico di quote tooensure un utilizzo equo delle risorse. È possibile trovare ulteriori informazioni su queste quote in hello [Cenni preliminari sulle quote di Service Bus][Quotas overview].

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Quali sono le eccezioni di hello generate dall'API di Azure Service Bus e le relative azioni suggerite?
Per un elenco delle possibili eccezioni del bus di servizio, vedere [Eccezioni di messaggistica del bus di servizio][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Cos'è una firma di accesso condiviso e quali linguaggi supportano la generazione di una firma?
Le firme di accesso condiviso sono un meccanismo di autenticazione basato su hash sicuri SHA-256 o URI. Per informazioni su come toogenerate propria firme nel nodo, PHP, Java e C\#, vedere hello [firme di accesso condiviso] [ Shared Access Signatures] articolo.

## <a name="subscription-and-namespace-management"></a>Gestione di sottoscrizioni e spazi dei nomi
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Migrazione di una sottoscrizione di Azure di tooanother dello spazio dei nomi

È possibile spostare uno spazio dei nomi da una sottoscrizione di Azure tooanother, utilizzando entrambi hello [portale di Azure](https://portal.azure.com) o i comandi di PowerShell. In un'operazione tooexecute hello ordine, hello dello spazio dei nomi deve essere già attivo. utente di Hello l'esecuzione di comandi hello deve essere un amministratore sia origine hello e le sottoscrizioni di destinazione.

#### <a name="portal"></a>di Microsoft Azure

hello toouse sottoscrizione di tooanother gli spazi dei nomi Service Bus toomigrate portale Azure, seguire le direzioni di hello [qui](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Hello sequenza di comandi di PowerShell seguente sposta uno spazio dei nomi da una sottoscrizione di Azure tooanother. tooexecute questa operazione, hello dello spazio dei nomi deve già essere attivo e utente hello esecuzione comandi PowerShell hello deve essere un amministratore in entrambe le sottoscrizioni di origine e destinazione hello.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su Service Bus, vedere hello seguenti argomenti.

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
