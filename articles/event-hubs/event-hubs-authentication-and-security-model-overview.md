---
title: aaaOverview del modello di autenticazione e sicurezza degli hub di eventi di Azure | Documenti Microsoft
description: Panoramica sul modello di autenticazione e sicurezza di Hub eventi.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Panoramica sull’autenticazione di Hub eventi e sul modello di protezione
modello di sicurezza degli hub di eventi di Azure Hello soddisfa hello seguenti requisiti:

* Solo i client che presentano credenziali valide possono inviare hub eventi tooan di dati.
* Un client non può rappresentare un altro client.
* Un client non autorizzato può essere bloccato per l'invio di hub di eventi tooan di dati.

## <a name="client-authentication"></a>Autenticazione client
modello di sicurezza degli hub eventi Hello è basato su una combinazione di [firma di accesso condiviso (SAS)](../service-bus-messaging/service-bus-sas.md) token e *i Publisher di eventi*. Un autore di eventi definisce un endpoint virtuale per un hub eventi. server di pubblicazione Hello può essere solo hub di eventi tooan messaggi toosend utilizzato. Non è possibile tooreceive messaggi da un server di pubblicazione.

In genere, un Hub eventi usa un autore per ogni client. Tutti i messaggi vengono inviati tooany degli editori di hello di un hub eventi vengono accodati all'interno di tale hub eventi. Gli autori consentono la limitazione e il controllo di accesso con granularità fine.

Ogni client di hub eventi viene assegnato un token univoco, che viene caricato toohello client. Hello token vengono prodotti in modo che ognuno concede l'accesso tooa univoco server di pubblicazione diverso. Un client che dispone di un token può inviare solo tooone server di pubblicazione, ma nessun altro server di pubblicazione. Se più client Condivisione hello stesso token, quindi ognuno di essi condivide un server di pubblicazione.

Sebbene non sia consigliabile, è possibile tooequip dispositivi con i token che concedono l'hub di eventi di accesso diretto tooan. Qualsiasi dispositivo che contiene un token di questo tipo può inviare messaggi direttamente a tale hub eventi. Il dispositivo non sarà soggetto toothrottling. Inoltre, il dispositivo di hello non è possibile impedire l'invio di hub di eventi toothat.

Tutti i token sono firmati con una chiave SAS. In genere, tutti i token sono firmati con hello stessa chiave. I client non sono a conoscenza della chiave di hello; Ciò impedisce ad altri client di produrre token.

### <a name="create-hello-sas-key"></a>Creare la chiave di firma di accesso condiviso hello

Quando si crea uno spazio dei nomi dell'hub eventi, il servizio di hello genera una chiave di firma di accesso condiviso a 256 bit denominata **RootManageSharedAccessKey**. Questa chiave concede inviano, ascolto e gestire lo spazio dei nomi toohello di diritti. È anche possibile creare chiavi aggiuntive. È consigliabile creare una chiave che concede l'hub di eventi specifici toohello di autorizzazioni di invio. In seguito hello in questo argomento, si presuppone che questa chiave è denominato **EventHubSendKey**.

Hello di esempio seguente crea una chiave di solo invio durante la creazione di hub eventi hello:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Generare token

È possibile generare token usando una chiave SAS hello. È necessario ottenere solo un token per client. I token possono essere creati utilizzando hello al metodo. Tutti i token vengono generati utilizzando hello **EventHubSendKey** chiave. A ogni token viene assegnato un URI univoco.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Quando si chiama questo metodo, hello URI deve essere specificato come `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Per tutti i token, è identico, con l'eccezione hello di hello URI `PUBLISHER_NAME`, che deve essere diverso per ogni token. Idealmente, `PUBLISHER_NAME` rappresenta hello ID del client hello che riceve il token.

Questo metodo genera un token con hello seguente struttura:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

ora di scadenza del token Hello è espresso in secondi dal 1 ° gennaio 1970. Hello Ecco un esempio di un token:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

In genere, i token hello hanno una durata uguale o maggiore durata hello del client hello. Se client hello dispone di un nuovo token hello funzionalità tooobtain, è possono utilizzare i token con una durata più breve.

### <a name="sending-data"></a>Invio di dati
Dopo avere creato il token hello, viene eseguito il provisioning di ogni client con il proprio token univoco.

Quando il client di hello invia dati a un hub eventi, è la richiesta di trasmissione con token hello di tag. un attacco intercetti e rubi il token di hello, la comunicazione tra client hello e hub eventi hello hello tooprevent devono essere eseguite tramite un canale crittografato.

### <a name="blacklisting-clients"></a>Disattivazione dei client
Se il furto di un token da un utente malintenzionato, hello può rappresentare client hello è stato rubato il token. La disattivazione di un client rende il rendering di tale client inutilizzabile fino a che non riceve un nuovo token che usa un autore diverso.

## <a name="authentication-of-back-end-applications"></a>Autenticazione delle applicazioni back-end

applicazioni back-end tooauthenticate che utilizzano i dati di hello generati dai client di hub eventi, gli hub eventi Usa un modello di sicurezza che è simile modello toohello utilizzato per gli argomenti del Bus di servizio. Un gruppo di consumer dell'hub eventi è l'argomento del Bus di servizio tooa sottoscrizione tooa equivalente. Un client può creare un gruppo di consumer se il gruppo di consumer hello toocreate hello richiesta è accompagnato da un token che concede privilegi per l'hub di eventi hello di gestione o per hello dello spazio dei nomi toowhich hub eventi hello appartiene. Un client è consentito tooconsume dati da un gruppo di consumer se hello ricevere la richiesta sono accompagnati da un token che concede diritti per questo gruppo di consumer di ricezione, hello hub eventi o hub eventi di hello dello spazio dei nomi toowhich hello appartiene.

versione corrente di Hello del Bus di servizio non supporta le regole di firma di accesso condiviso per singole sottoscrizioni. Hello che stesso vale per i gruppi di consumer di hub eventi. Verrà aggiunto il supporto di firma di accesso condiviso per entrambe le funzionalità in hello future.

In assenza di hello di autenticazione SAS per gruppi di consumer singoli, è possibile utilizzare toosecure chiavi SAS tutti i gruppi di consumer con una chiave comune. Questo approccio consente un tooconsume dati dell'applicazione da uno qualsiasi dei gruppi di consumer hello di un hub eventi.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sugli hub di eventi, visitare hello seguenti argomenti:

* [Panoramica di Hub eventi]
* [Panoramica delle firme di accesso condiviso]
* [Applicazioni di esempio che usano Hub eventi]

[Panoramica di Hub eventi]: event-hubs-what-is-event-hubs.md
[Applicazioni di esempio che usano Hub eventi]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Panoramica delle firme di accesso condiviso]: ../service-bus-messaging/service-bus-sas.md

