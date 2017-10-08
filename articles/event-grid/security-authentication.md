---
title: autenticazione e sicurezza griglia eventi aaaAzure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Sicurezza e autenticazione di Griglia di eventi 

Griglia di eventi di Azure ha tre tipi di autenticazione:

* Sottoscrizioni di eventi
* Pubblicazione di eventi
* Recapito eventi webhook

## <a name="webhook-event-delivery"></a>Recapito eventi webhook

Webhook sono uno dei molti eventi di tooreceive modi in tempo reale dalla griglia di eventi di Azure.

Ogni volta che è presente un nuovo toobe pronto evento recapitato, griglia eventi invia una richiesta HTTP con tooyour WebHook con evento hello nel corpo di hello.

Quando si registra il proprio endpoint WebHook con griglia di eventi, invia una richiesta POST con un codice di convalida semplice della proprietà di endpoint tooprove ordine. L'app deve toorespond visualizzando il codice di convalida hello indietro. Griglia di eventi non fornirà eventi tooWebHook endpoint che non hanno superato la convalida di hello.
 
### <a name="validation-details"></a>Informazioni di convalida:

* In fase di hello di creazione/aggiornamento della sottoscrizione evento, evento griglia registra un endpoint di destinazione "SubscriptionValidationEvent" toohello evento.
* evento Hello contiene un valore di intestazione "Convalida di tipo di evento:".
* corpo dell'evento Hello è hello stesso schema di altri eventi di griglia di eventi.
* dati dell'evento Hello includono una proprietà di "ValidationCode" con una stringa generata in modo casuale, ad esempio "ValidationCode: acb13…".

In proprietà di endpoint tooprove ordine, echo ad esempio di codice convalida hello Indietro "ValidationResponse: acb13...".

Infine, è importante toonote che griglia di eventi di Azure supporta solo l'endpoint webhook HTTPS.
## <a name="event-subscription"></a>Sottoscrizione dell'evento

evento tooan toosubscribe, è necessario disporre hello **Microsoft.EventGrid/EventSubscriptions/Write** risorsa necessaria l'autorizzazione in hello. Questa autorizzazione è necessaria poiché si sta creando una nuova sottoscrizione nell'ambito di hello della risorsa hello. Hello necessarie risorse varia in base al se si effettua la sottoscrizione dell'argomento di sistema di tooa o argomento personalizzato. Entrambi i tipi sono descritti in questa sezione.

### <a name="system-topics-azure-service-publishers"></a>Argomenti di sistema (entità di pubblicazione dei servizi di Azure)

Gli argomenti di sistema, è necessario autorizzazione toowrite una nuova sottoscrizione di eventi nell'ambito di hello dell'evento di hello hello risorse pubblicazione. formato Hello della risorsa hello è:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Ad esempio, toosubscribe tooan evento su un account di archiviazione denominato **myacct**, è richiesta l'autorizzazione di Microsoft.EventGrid/EventSubscriptions/Write hello in:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Argomenti personalizzati

Per argomenti personalizzati, è necessario autorizzazione toowrite una nuova sottoscrizione di eventi nell'ambito di hello di argomento evento griglia hello. formato Hello della risorsa hello è:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Ad esempio, toosubscribe tooa argomento personalizzato denominato **mytopic**, è richiesta l'autorizzazione di Microsoft.EventGrid/EventSubscriptions/Write hello in:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Pubblicazione di argomenti

Gli argomenti usano la firma di accesso condiviso o l'autenticazione della chiave. È consigliabile la firma di accesso condiviso, ma l'autenticazione della chiave fornisce una programmazione semplice ed è compatibile con molte entità di pubblicazione di webhook esistenti. 

Includere il valore di autenticazione hello nell'intestazione HTTP hello. Per la firma di accesso condiviso, utilizzare **token di firma di accesso condiviso aeg** per il valore dell'intestazione hello. Per l'autenticazione con chiave, utilizzare **chiave di firma di accesso condiviso aeg** per il valore dell'intestazione hello.

### <a name="key-authentication"></a>Autenticazione della chiave

L'autenticazione con chiave è più semplice di autenticazione hello. Utilizzare il formato: hello`aeg-sas-key: <your key>`

Ad esempio, passare una chiave con: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Token di firma di accesso condiviso

I token di firma di accesso condiviso per griglia di eventi includono risorse hello, un'ora di scadenza e una firma. Hello formato del token di firma di accesso condiviso hello è: `r={resource}&e={expiration}&s={signature}`.

risorsa Hello è il percorso di hello per hello argomento toowhich si invia eventi. Un percorso di risorsa valido, ad esempio, è: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Firma hello generate da una chiave.

Un valore **aeg-sas-token** valido, ad esempio, è:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Hello di esempio seguente crea un token di firma di accesso condiviso per l'utilizzo con griglia eventi:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Controllo di accesso per la gestione

Azure griglia di eventi consente si toocontrol hello livello di accesso assegnato toodifferent utenti toodo varie operazioni di gestione, ad esempio le sottoscrizioni di eventi di elenco, crearne di nuovi e generare le chiavi. Griglia di eventi utilizza a questo scopo il controllo degli accessi in base al ruolo di Azure.

### <a name="operation-types"></a>Tipi di operazioni

Griglia di eventi di Azure supporta hello seguenti azioni:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Hello ultime tre operazioni restituito potenzialmente informazioni segrete Ottiene filtrato da normale operazioni di lettura. È consigliabile per consentire operazioni di toothese toorestrict accesso. È possibile creare ruoli personalizzati utilizzando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure interfaccia della riga di comando (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), hello e [API REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Applicazione del controllo degli accessi in base al ruolo

Utilizzare hello seguendo i passaggi tooenforce RBAC per utenti diversi:

#### <a name="create-a-custom-role-definition-file-json"></a>Creare un file di definizione del ruolo personalizzato (JSON)

di seguito Hello sono definizioni di ruolo della griglia di eventi di esempio che consentono agli utenti tooperform diversi set di azioni.

**EventGridReadOnlyRole.json**: consente solo operazioni di sola lettura.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: consente le azioni di pubblicazione con restrizioni, ma non consente le azioni di eliminazione.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: consente tutte le azioni di Griglia di eventi.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Installazione e account di accesso tooAzure CLI

* Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure. versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager nell'interfaccia della riga di comando di Azure. Andare troppo[Using hello CLI di Azure con Gestione risorse di hello](../xplat-cli-azure-resource-manager.md) per altri dettagli.

#### <a name="create-a-custom-role"></a>Creare un ruolo personalizzato

toocreate un ruolo personalizzato, utilizzare:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Assegnare hello ruolo tooa utente


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione tooEvent griglia, vedere [sulla griglia di eventi](overview.md)
