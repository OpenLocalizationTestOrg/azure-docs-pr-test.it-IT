---
title: Sicurezza e autenticazione di Griglia di eventi di Azure
description: Vengono descritti il servizio Griglia di eventi di Azure e i concetti correlati.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 09/18/2017
ms.author: babanisa
ms.openlocfilehash: e2f48b6e72072ce6bf019b3adc138ae83c162f25
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="event-grid-security-and-authentication"></a>Sicurezza e autenticazione di Griglia di eventi 

Griglia di eventi di Azure ha tre tipi di autenticazione:

* Sottoscrizioni di eventi
* Pubblicazione di eventi
* Recapito eventi webhook

## <a name="webhook-event-delivery"></a>Recapito eventi webhook

I webhook sono uno dei modi per ricevere gli eventi in tempo reale da Griglia di eventi di Azure. Ogni volta che un nuovo evento è pronto per essere recapitato, il webhook della Griglia di eventi invia una richiesta HTTP all'endpoint HTTP configurato nel cui corpo è contenuto l'evento.

Quando si registra l'endpoint del webhook con Griglia di eventi, viene inviata una richiesta POST con un semplice codice di convalida per dimostrare la proprietà dell'endpoint. È necessario che l'app risponda rimandando il codice di convalida. La Griglia di eventi non recapita gli eventi agli endpoint del webhook che non hanno superato la convalida.

### <a name="validation-details"></a>Dettagli di convalida

* In fase di creazione/aggiornamento della sottoscrizione dell'evento, Griglia di eventi pubblica un evento "SubscriptionValidationEvent" nell'endpoint di destinazione.
* L'evento contiene un valore di intestazione "Aeg-Event-Type: SubscriptionValidation".
* Il corpo dell'evento ha lo stesso schema degli altri eventi di Griglia di eventi.
* I dati dell'evento includono una proprietà "validationCode" con una stringa generata in modo casuale. ad esempio "validationCode: acb13…".

Un esempio di SubscriptionValidationEvent è mostrato di seguito:

```json
[{
  "id": "2d1781af-3a4c-4d7c-bd0c-e34b19da4e66",
  "topic": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subject": "",
  "data": {
    "validationCode": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6"
  },
  "eventType": "Microsoft.EventGrid.SubscriptionValidationEvent",
  "eventTime": "2017-08-06T22:09:30.740323Z"
}]
```

Per dimostrare la proprietà dell'endpoint, rimandare il codice di convalida nella proprietà validationResponse, come mostrato nell'esempio seguente:

```json
{
  "validationResponse": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6"
}
```

È infine importante notare che Griglia di eventi di Azure supporta solo endpoint di webhook HTTPS.

## <a name="event-subscription"></a>Sottoscrizione dell'evento

Per sottoscrivere un evento, è necessaria l'autorizzazione **Microsoft.EventGrid/EventSubscriptions/Write** per la risorsa richiesta. Questa autorizzazione è necessaria perché si sta scrivendo una nuova sottoscrizione nell'ambito della risorsa. La risorsa necessaria è diversa a seconda del fatto che si sottoscriva un argomento di sistema o un argomento personalizzato. Entrambi i tipi sono descritti in questa sezione.

### <a name="system-topics-azure-service-publishers"></a>Argomenti di sistema (entità di pubblicazione dei servizi di Azure)

Per gli argomenti di sistema, è necessaria l'autorizzazione per scrivere una nuova sottoscrizione di evento nell'ambito della risorsa che pubblica l'evento. Il formato della risorsa è: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Per sottoscrivere, ad esempio, un evento in un account di archiviazione denominato **myacct**, è necessaria l'autorizzazione Microsoft.EventGrid/EventSubscriptions/Write per: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Argomenti personalizzati

Per gli argomenti personalizzati, è necessaria l'autorizzazione per scrivere una nuova sottoscrizione di evento nell'ambito dell'argomento di Griglia di eventi. Il formato della risorsa è: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Per sottoscrivere, ad esempio, un argomento personalizzato denominato **mytopic**, è necessaria l'autorizzazione Microsoft.EventGrid/EventSubscriptions/Write per: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Pubblicazione di argomenti

Gli argomenti usano la firma di accesso condiviso o l'autenticazione della chiave. È consigliabile la firma di accesso condiviso, ma l'autenticazione della chiave fornisce una programmazione semplice ed è compatibile con molte entità di pubblicazione di webhook esistenti. 

Il valore dell'autenticazione viene incluso nell'intestazione HTTP. Per la firma di accesso condiviso, usare **aeg-sas-token** per il valore dell'intestazione. Per l'autenticazione della chiave, usare **aeg-sas-key** per il valore dell'intestazione.

### <a name="key-authentication"></a>Autenticazione della chiave

L'autenticazione della chiave è la forma più semplice di autenticazione. Usare il formato: `aeg-sas-key: <your key>`

Ad esempio, passare una chiave con:

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Token di firma di accesso condiviso

I token di firma di accesso condiviso per Griglia di eventi includono la risorsa, un'ora di scadenza e una firma. Il formato del token di firma di accesso condiviso è: `r={resource}&e={expiration}&s={signature}`.

La risorsa è il percorso dell'argomento a cui si inviano gli eventi. Un percorso di risorsa valido, ad esempio, è: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

La firma viene generata da una chiave.

Un valore **aeg-sas-token** valido, ad esempio, è:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
```

L'esempio seguente crea un token di firma di accesso condiviso per l'uso con Griglia di eventi:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    var culture = CultureInfo.CreateSpecificCulture("en-US");
    var encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString(culture));

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

Griglia di eventi di Azure consente di controllare il livello di accesso assegnato ai diversi utenti per eseguire svariate operazioni di gestione, ad esempio elencare sottoscrizioni di eventi, crearne di nuove e generare chiavi. La Griglia di eventi utilizza a questo scopo il controllo degli accessi in base al ruolo di Azure.

### <a name="operation-types"></a>Tipi di operazioni

Griglia di eventi di Azure supporta le azioni seguenti:

* Microsoft.EventGrid/*/read
* Microsoft.EventGrid/*/write
* Microsoft.EventGrid/*/delete
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action
* Microsoft.EventGrid/topics/listKeys/action
* Microsoft.EventGrid/topics/regenerateKey/action

Le ultime tre operazioni restituiscono informazioni potenzialmente riservate che vengono filtrate dalle normali operazioni di lettura. È consigliabile limitare l'accesso a queste operazioni. I ruoli personalizzati possono essere creati usando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [l'interfaccia della riga di comando di Azure (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md) e la [API REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Applicazione del controllo degli accessi in base al ruolo

Usare i passaggi seguenti per applicare il controllo degli accessi in base al ruolo per utenti diversi:

#### <a name="create-a-custom-role-definition-file-json"></a>Creare un file di definizione del ruolo personalizzato (JSON)

Le seguenti sono definizioni del ruolo di Griglia di eventi che consentono agli utenti di eseguire set diversi di azioni.

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
    "/subscriptions/<Subscription id>"
  ]
}
```

#### <a name="create-and-assign-custom-role-with-azure-cli"></a>Creare e assegnare un ruolo personalizzato con l'interfaccia della riga di comando di Azure

Per creare un ruolo personalizzato, usare:

```azurecli
az role definition create --role-definition @<file path>
```

Per assegnare il ruolo a un utente, usare:

```azurecli
az role assignment create --assignee <user name> --role "<name of role>"
```

## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md).
