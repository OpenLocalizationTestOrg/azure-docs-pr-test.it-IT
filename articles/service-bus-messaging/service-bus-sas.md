---
title: l'autenticazione del Bus di servizio aaaAzure con firme di accesso condiviso | Documenti Microsoft
description: Panoramica dell'autenticazione del bus di servizio con firme di accesso condiviso, dettagli dell'autenticazione con firme di accesso condiviso con il bus di servizio.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Autenticazione del bus di servizio con firme di accesso condiviso

*Firme di accesso condiviso* (SAS) sono il meccanismo di sicurezza primario hello per Bus di servizio di messaggistica. In questo articolo viene SAS, come funzionino e come toouse loro in modo indipendente dalla piattaforma.

L'autenticazione SAS consente applicazioni tooauthenticate tooService Bus usando una chiave di accesso configurata nello spazio dei nomi hello o in hello messaggistica entità (coda o argomento) con cui sono associati diritti specifici. È quindi possibile utilizzare questa chiave toogenerate un token di firma di accesso condiviso che i client possono utilizzare tooauthenticate tooService Bus.

Supporto per l'autenticazione di firma di accesso condiviso è incluso in hello Azure SDK versione 2.0 e versioni successive.

## <a name="overview-of-sas"></a>Panoramica di SAS

Le firme di accesso condiviso sono un meccanismo di autenticazione basato su hash sicuri SHA-256 o URI. SAS è un meccanismo estremamente efficace utilizzato da tutti i servizi del bus di servizio. Nell'uso effettivo, SAS presenta due componenti: i *criteri di accesso condiviso* e una *firma di accesso condiviso* che viene spesso chiamata *token*.

L'autenticazione di firma di accesso condiviso nel Bus di servizio è inclusa la configurazione di hello di una chiave di crittografia con i relativi diritti in una risorsa del Bus di servizio. I client attestazione accesso tooService Bus risorse presentando un token di firma di accesso condiviso. Questo token è costituito da risorse hello URI a cui si accede e una scadenza firmata con hello chiave configurata.

È possibile configurare le regole di autorizzazione della firma di accesso condiviso in [inoltri](service-bus-fundamentals-hybrid-solutions.md#relays), [code](service-bus-fundamentals-hybrid-solutions.md#queues) e [argomenti](service-bus-fundamentals-hybrid-solutions.md#topics) del bus di servizio.

L'autenticazione SAS utilizza hello seguenti elementi:

* [Regola di autorizzazione per l'accesso condiviso](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): una chiave di crittografia primaria a 256 bit in formato Base 64, una chiave secondaria facoltativa e un nome di chiave e i diritti associati (una raccolta di diritti di tipo *Listen*, *Send* o *Manage*).
* [Firma di accesso condiviso](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: generato utilizzando hello HMAC-SHA256 di una stringa di risorsa, costituito da hello URI della risorsa hello che è possibile accedere a e da una scadenza, con chiave di crittografia hello. firma Hello e altri elementi descritti nella hello le sezioni seguenti vengono formattati in un hello tooform stringa token SAS.

## <a name="shared-access-policy"></a>Criteri di accesso condiviso

Toounderstand una cosa importante sulla firma di accesso condiviso è che inizia con un criterio. Per ogni criterio si stabiliscono tre informazioni: **nome**, **ambito** e **autorizzazioni**. Hello **nome** semplicemente che; è un nome univoco all'interno di tale ambito. Hello ambito è abbastanza semplice: è hello URI della risorsa hello in questione. Per uno spazio dei nomi Service Bus, hello ambito è il nome di dominio completo hello (FQDN), ad esempio `https://<yournamespace>.servicebus.windows.net/`.

Hello le autorizzazioni disponibili per i criteri sono in gran parte non necessitano di spiegazione:

* Invio
* Attesa
* Gestisci

Dopo aver creato criteri hello, viene assegnato un *chiave primaria* e *chiave secondaria*. Si tratta di chiavi di crittografia complesse. Non andranno perse o perdita li - sempre siano disponibili in hello [portale di Azure][Azure portal]. È possibile utilizzare una delle chiavi di hello generato e li può essere rigenerato in qualsiasi momento. Tuttavia, se si rigenera o modificare la chiave primaria di hello nei criteri di hello, le firme di accesso condiviso creato da esso verranno invalidate.

Quando si crea uno spazio dei nomi del Bus di servizio, viene creato automaticamente un criterio per hello tutto lo spazio dei nomi denominato **RootManageSharedAccessKey**, e questo criterio ha tutte le autorizzazioni. Non accedere come **radice** e non usare questo criterio a meno che non esista un motivo molto valido. È possibile creare criteri aggiuntivi in hello **configura** scheda per spazio dei nomi hello nel portale di hello. È importante toonote che un livello di struttura con un unico Bus di servizio (spazio dei nomi, coda, e così via) può avere solo backup too12 criteri allegati tooit.

## <a name="configuration-for-shared-access-signature-authentication"></a>Configurazione dell'autenticazione della firma di accesso condiviso
È possibile configurare hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) regola in spazi dei nomi Service Bus, code o argomenti. Configurazione di un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) su un Bus di servizio di sottoscrizione non è supportata, ma è possibile utilizzare le regole configurate in un toosubscriptions accesso toosecure dello spazio dei nomi o un argomento. Per un esempio che illustra questa procedura, vedere hello [l'autenticazione tramite firma di accesso condiviso (SAS) con le sottoscrizioni del Bus di servizio](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) esempio.

In uno spazio dei nomi, una coda o un argomento del bus di servizio è possibile configurare fino 12 regole di questo tipo. Le regole configurate in uno spazio dei nomi del Bus di servizio si applicano tooall entità nello spazio dei nomi.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

In questa figura, hello *manageRuleNS*, *sendRuleNS*, e *listenRuleNS* si applicano le regole di autorizzazione tooboth coda Q1 che all'argomento T1, mentre *listenRuleQ*  e *sendRuleQ* si applicano solo tooqueue Q1 e *sendRuleT* si applica solo a tootopic T1.

Hello parametri principali di un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) sono i seguenti:

| . | Descrizione |
| --- | --- |
| *KeyName* |Stringa che descrive la regola di autorizzazione hello. |
| *PrimaryKey* |Una codifica base64 a 256 bit chiave primaria per la firma e convalida i token di firma di accesso condiviso hello. |
| *SecondaryKey* |Una con codifica base64 a 256 bit chiave secondaria per la firma e convalida i token di firma di accesso condiviso hello. |
| *AccessRights* |Un elenco di diritti di accesso concessi dalla regola di autorizzazione hello. Questi diritti possono essere qualsiasi raccolta di diritti di ascolto, invio e gestione. |

Quando viene eseguito il provisioning di uno spazio dei nomi del Bus di servizio, un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), con [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) impostare troppo**RootManageSharedAccessKey**, viene creato per impostazione predefinita.

## <a name="generate-a-shared-access-signature-token"></a>Generare una firma di accesso condiviso (token)

criterio Hello stesso non è il token di accesso hello per Bus di servizio. Oggetto hello da quale hello viene generato il token di accesso - con una chiave primaria o secondaria di hello è. Qualsiasi client che dispone di accesso toohello specificate nella regola di autorizzazione di accesso condiviso hello chiavi di firma può generare token SAS hello. token Hello è generato da con attenzione la creazione di una stringa in hello seguente formato:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Dove `signature-string` hash SHA-256 hello dell'ambito di hello del token hello (**ambito** come descritto nella sezione precedente hello) con un CRLF aggiunto e un'ora di scadenza (in secondi trascorsi hello: `00:00:00 UTC` del 1 ° gennaio 1970). 

> [!NOTE]
> tooavoid un breve scadenza dei token, è consigliabile codificare valore ora di scadenza hello come almeno un intero senza segno a 32 bit o, preferibilmente, un numero intero lungo (64 bit).  
> 
> 

hash Hello toohello simile pseudo-codice seguente esegue la ricerca e restituisce 32 byte.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

i valori hash non Hello sono hello **SharedAccessSignature** stringa in modo che hello destinatario può calcolare hello hash con hello stessi parametri, che viene restituito toobe hello stesso risultato. nome della chiave hello identifica hello criteri toobe utilizzato toocompute hello hash Hello URI specifica ambito hello. Questo è importante dal punto di vista della sicurezza. Se la firma hello diversa che calcola il destinatario hello (Service Bus), l'accesso è negato. A questo punto è possibile che il mittente hello era toohello tasto di scelta e deve disporre dei diritti di hello specificati nei criteri di hello.

Si noti che è necessario utilizzare hello con codifica URI di risorsa per l'operazione. URI della risorsa Hello è hello che è richiesto l'URI completo di hello toowhich accesso alle risorse di Service Bus. Ad esempio `http://<namespace>.servicebus.windows.net/<entityPath>` o `sb://<namespace>.servicebus.windows.net/<entityPath>`, ovvero `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

regola di autorizzazione di accesso condiviso Hello utilizzata per la firma deve essere configurato sull'entità hello specificata da questo URI, o da un elemento padre nella gerarchia. Ad esempio, `http://contoso.servicebus.windows.net/contosoTopics/T1` o `http://contoso.servicebus.windows.net` nell'esempio precedente hello.

Un token di firma di accesso condiviso è valido per tutte le risorse in hello `<resourceURI>` utilizzato in hello `signature-string`.

Hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) in hello SAS token fa riferimento toohello **keyName** Usa il token di hello toogenerate di hello di regola di autorizzazione di accesso condiviso.

Hello *URL-encoded-resourceURI* deve essere hello stesso hello URI utilizzato in hello stringa da firmare durante il calcolo hello della firma hello. Il valore deve essere [codificato in percentuale](https://msdn.microsoft.com/library/4fkewx0t.aspx).

È consigliabile rigenerare periodicamente le chiavi hello utilizzati hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) oggetto. Le applicazioni in genere consigliabile utilizzare hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate un token di firma di accesso condiviso. Quando si rigenerano le chiavi di hello, è necessario sostituire hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) con primario precedente hello chiave e generare una nuova chiave come nuova chiave primaria hello. In questo modo toocontinue utilizzando token per l'autorizzazione rilasciati con una chiave primaria precedente hello e non ancora scaduti.

Se si dispongono di chiavi hello toorevoke una chiave viene compromessa, è possibile rigenerare sia hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) hello e [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) di un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), sostituirli con le nuove chiavi. Questa procedura invalida tutti i token firmati con le chiavi precedenti hello.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Modalità autenticazione di firma di accesso condiviso toouse con il Bus di servizio

Hello seguenti scenari include la configurazione delle regole di autorizzazione, la generazione di token di firma di accesso condiviso e l'autorizzazione di client.

Per una procedura completa di esempio reale di un'applicazione del Bus di servizio che illustra hello configurazione e Usa SAS autorizzazione, vedere [l'autenticazione di firma di accesso condiviso con il Bus di servizio](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Un esempio correlato che illustra l'uso di hello SAS delle regole di autorizzazione configurati in spazi dei nomi o gli argomenti le sottoscrizioni del Bus di servizio toosecure è disponibile qui: [l'autenticazione tramite firma di accesso condiviso (SAS) con le sottoscrizioni del Bus di servizio ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Accesso alle regole di autorizzazione per l'accesso condiviso in uno spazio dei nomi

Operazioni in radice dello spazio dei nomi del Bus di servizio hello richiedono l'autenticazione del certificato. È necessario caricare un certificato di gestione per la sottoscrizione di Azure. tooupload un certificato di gestione, seguire i passaggi di hello [qui](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), utilizzando hello [portale di Azure][Azure portal]. Per ulteriori informazioni sui certificati di gestione di Azure, vedere hello [panoramica dei certificati di Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

endpoint di Hello per accedere alle regole di autorizzazione di accesso condiviso in uno spazio dei nomi del Bus di servizio è il seguente:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) oggetto in uno spazio dei nomi del Bus di servizio, eseguire un'operazione POST su questo endpoint con le informazioni sulle regole di hello serializzati come JSON o XML. ad esempio:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Analogamente, utilizzare un'operazione GET su hello endpoint tooread hello regole di autorizzazione configurate nello spazio dei nomi hello.

tooupdate o eliminare una regola di autorizzazione specifico, utilizzare hello seguenti endpoint:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Accedere alle regole di autorizzazione per l'accesso condiviso in un'entità

È possibile accedere a un [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) oggetto configurato in una coda del Bus di servizio o un argomento tramite hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) insieme in hello corrispondente [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) o [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Hello seguente codice mostra come delle regole di autorizzazione tooadd per una coda.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Usare l'autorizzazione con firma di accesso condiviso

Applicazioni che usano hello Azure .NET SDK con le librerie .NET di Service Bus hello possono utilizzare l'autorizzazione di firma di accesso condiviso tramite hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) classe. Hello codice riportato di seguito viene illustrato hello utilizzo della coda del Bus di servizio tooa toosend messaggi hello provider di token.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Le applicazioni possono anche usare la firma di accesso condiviso per l'autenticazione usando una stringa di connessione della firma di accesso condiviso nei metodi che accettano stringhe di connessione.

Si noti che autorizzazione SAS toouse con inoltri del Bus di servizio, è possibile usare le chiavi di firma di accesso condiviso configurate nello spazio dei nomi Service Bus hello. Se si crea in modo esplicito un inoltro nello spazio dei nomi hello ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) con un [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) dell'oggetto, è possibile impostare regole di firma di accesso condiviso hello solo per tale inoltro. autorizzazione di firma di accesso condiviso toouse con le sottoscrizioni del Bus di servizio, è possibile utilizzare le chiavi di firma di accesso condiviso configurate in uno spazio dei nomi del Bus di servizio o in un argomento.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Utilizzare la firma di accesso condiviso hello (a livello HTTP)

Ora che è stato appreso come toocreate firme di accesso condiviso per qualsiasi entità nel Bus di servizio, si è pronti a tooperform un POST HTTP:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Questa procedura funziona per ogni elemento. È possibile creare una firma di accesso condiviso per una coda, un argomento o una sottoscrizione. 

Se fornire un token di firma di accesso condiviso a un mittente o client, che non dispongono di chiave hello direttamente e non è possibile invertire tooobtain hash hello è. Di conseguenza, è necessario controllare a cosa possono accedere e per quanto tempo. Tooremember una cosa importante è che se si modifica una chiave primaria di hello nei criteri di hello, le firme di accesso condiviso creato da esso verranno invalidate.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Utilizzare la firma di accesso condiviso hello (a livello AMQP)

Nella sezione precedente hello, si è visto come toouse hello token di firma di accesso condiviso con una richiesta HTTP POST per l'invio di dati toohello Bus di servizio. Come è noto, è possibile accedere a Bus di servizio utilizzando hello Advanced Message Queuing Protocol (AMQP) che è toouse protocollo hello preferito per motivi di prestazioni, in molti scenari. utilizzo dei token di firma di accesso condiviso con AMQP Hello è descritto nel documento hello [AMQP Claim-Based sicurezza versione 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) ovvero in bozza di lavoro poiché 2013 ma ben supportata da Azure oggi.

Prima di iniziare toosend dati tooService Bus, server di pubblicazione hello deve inviare il token SAS hello all'interno di un AMQP messaggio tooa ben definito AMQP nodo denominato **$cbs** (è possibile visualizzarlo come "speciale" coda utilizzata da tooacquire servizio hello e convalidare tutte token di firma di accesso condiviso Hello). server di pubblicazione Hello deve specificare hello **ReplyTo** campo all'interno del messaggio AMQP hello; questo è il nodo hello in cui hello servizio risponde publisher toohello con risultato hello hello di convalida di token (un semplice modello richiesta/risposta tra server di pubblicazione e servizio). Viene creato questo nodo di risposta "on hello immediatamente," generale "creazione dinamica del nodo remoto", come descritto dalla specifica hello AMQP 1.0. Dopo aver controllato che il token di firma di accesso condiviso hello è valido, publisher hello può andare avanti e avviare il servizio di toohello toosend dati.

Hello passaggi seguenti viene illustrato come toosend hello token di firma di accesso condiviso con il protocollo AMQP utilizzando hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) libreria. Ciò è utile se non è possibile utilizzare ufficiale hello Service Bus SDK (ad esempio su WinRT, .net Compact Framework, .net Framework Micro e Mono) lo sviluppo in C\#. Questa libreria è certamente utile toohelp la comprensione della sicurezza basata sulle attestazioni come opera a livello AMQP hello, come visto come funziona a livello di hello HTTP (con un HTTP POST di richiesta e hello SAS token hello inviati all'interno di intestazione "Authorization"). Se non sono necessarie tali informazioni complete sui AMQP, è possibile utilizzare ufficiale hello Service Bus SDK con .net per applicazioni di Framework, che eseguiranno automaticamente.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hello `PutCbsToken()` metodo riceve hello *connessione* (istanza della classe connessione AMQP fornito da hello [AMQP .NET Lite libreria](https://github.com/Azure/amqpnetlite)) che rappresenta il servizio toohello di connessioni TCP hello e hello *sasToken* parametro hello toosend di token SAS. 

> [!NOTE]
> È importante che la connessione hello viene creata con **tooEXTERNAL di impostare il meccanismo di autenticazione SASL** (e non hello normale predefinito con nome utente e password utilizzata quando non è necessario alcun token di firma di accesso condiviso hello toosend).
> 
> 

Successivamente, server di pubblicazione hello crea due collegamenti AMQP per inviare il token di firma di accesso condiviso hello e ricevere risposta hello (risultato di convalida del token hello) dal servizio hello.

messaggio AMQP contiene un set di proprietà e altre informazioni oltre un semplice messaggio. token SAS Hello è il corpo di hello del messaggio (tramite il relativo costruttore). Hello **"ReplyTo"** toohello nome del nodo per la ricezione dei risultati di convalida hello sul collegamento di ricevitore hello (è possibile modificarne il nome se si desidera, e verrà creato in modo dinamico dal servizio hello) è impostata. Hello ultime tre applicazioni/personalizzato vengono utilizzate da hello servizio tooindicate il tipo di operazione ha tooexecute. Come descritto dalla bozza di specifica CBS hello, devono essere hello **nome operazione** ("put-token"), hello **tipo di token** (in questo caso, un "servicebus.windows.net:sastoken"), hello e **" nome"gruppo di destinatari hello** token hello toowhich Applica (entità intera hello).

Dopo l'invio dei token SAS hello sul collegamento mittente hello, server di pubblicazione hello deve leggere risposta hello sul collegamento ricevitore hello. risposta di Hello è un semplice messaggio AMQP con una proprietà dell'applicazione denominata **"codice di stato"** che può contenere hello uguali i valori come un codice di stato HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Diritti necessari per le operazioni del bus di servizio

Hello nella tabella seguente mostra i diritti di accesso hello necessari per diverse operazioni sulle risorse Bus di servizio.

| Operazione | Attestazione necessaria | Ambito attestazione |
| --- | --- | --- |
| **Spazio dei nomi** | | |
| Configurare le regole di autorizzazione relative a uno spazio dei nomi |Manage |Qualsiasi indirizzo dello spazio dei nomi |
| **Registro di sistema del servizio** | | |
| Enumerare i criteri privati |Manage |Qualsiasi indirizzo dello spazio dei nomi |
| Iniziare l'attesa su uno spazio dei nomi del servizio |Attesa |Qualsiasi indirizzo dello spazio dei nomi |
| Inviare listener tooa messaggi a uno spazio dei nomi |Invio |Qualsiasi indirizzo dello spazio dei nomi |
| **Coda** | | |
| Creare una coda |Manage |Qualsiasi indirizzo dello spazio dei nomi |
| Eliminare una coda |Manage |Qualsiasi indirizzo valido della coda |
| Enumerare le code |Manage |/$Resources/Queues |
| Ottenere una descrizione della coda hello |Gestisci |Qualsiasi indirizzo valido della coda |
| Configurare le regole di autorizzazione per una coda |Manage |Qualsiasi indirizzo valido della coda |
| Inviare in coda toohello |Invio |Qualsiasi indirizzo valido della coda |
| Ricevere messaggi da una coda |Attesa |Qualsiasi indirizzo valido della coda |
| Abbandonare o completare messaggi dopo la ricezione di messaggi hello in modalità di blocco di visualizzazione |Attesa |Qualsiasi indirizzo valido della coda |
| Rinviare un messaggio per il successivo recupero |Attesa |Qualsiasi indirizzo valido della coda |
| Spostare un messaggio nella coda dei messaggi non recapitabili |Attesa |Qualsiasi indirizzo valido della coda |
| Ottenere lo stato di hello associato a una sessione di coda di messaggi |Attesa |Qualsiasi indirizzo valido della coda |
| Imposta stato di hello associato a una sessione di coda di messaggi |Attesa |Qualsiasi indirizzo valido della coda |
| **Argomento** | | |
| Creare un argomento |Manage |Qualsiasi indirizzo dello spazio dei nomi |
| Eliminare un argomento |Manage |Qualsiasi indirizzo valido dell'argomento |
| Enumerare gli argomenti |Manage |/$Resources/Topics |
| Ottenere una descrizione dell'argomento hello |Gestisci |Qualsiasi indirizzo valido dell'argomento |
| Configurare le regole di autorizzazione per un argomento |Manage |Qualsiasi indirizzo valido dell'argomento |
| Inviare l'argomento toohello |Invio |Qualsiasi indirizzo valido dell'argomento |
| **Sottoscrizione** | | |
| Creare una sottoscrizione |Manage |Qualsiasi indirizzo dello spazio dei nomi |
| Eliminare una sottoscrizione |Manage |../myTopic/Subscriptions/mySubscription |
| Enumerare le sottoscrizioni |Manage |../myTopic/Subscriptions |
| Ottenere la descrizione di una sottoscrizione |Gestire |../myTopic/Subscriptions/mySubscription |
| Abbandonare o completare messaggi dopo la ricezione di messaggi hello in modalità di blocco di visualizzazione |Attesa |../myTopic/Subscriptions/mySubscription |
| Rinviare un messaggio per il successivo recupero |Attesa |../myTopic/Subscriptions/mySubscription |
| Spostare un messaggio nella coda dei messaggi non recapitabili |Attesa |../myTopic/Subscriptions/mySubscription |
| Ottenere lo stato di hello associato a una sessione dell'argomento |Attesa |../myTopic/Subscriptions/mySubscription |
| Stato di hello set associato a una sessione dell'argomento |Attesa |../myTopic/Subscriptions/mySubscription |
| **Regole** | | |
| Creare una regola |Manage |../myTopic/Subscriptions/mySubscription |
| Eliminare una regola |Manage |../myTopic/Subscriptions/mySubscription |
| Enumerare le regole |Manage o Listen |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Passaggi successivi

toolearn più sulla messaggistica del Bus di servizio, vedere hello seguenti argomenti.

* [Dati fondamentali del bus di servizio](service-bus-fundamentals-hybrid-solutions.md)
* [Code, argomenti e sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md)
* [Come le code del Bus di servizio toouse](service-bus-dotnet-get-started-with-queues.md)
* [Il Bus di servizio toouse argomenti e sottoscrizioni](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com