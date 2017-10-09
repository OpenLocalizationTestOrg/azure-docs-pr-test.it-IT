---
title: limiti per le richieste di gestione delle risorse aaaAzure | Documenti Microsoft
description: Viene descritto come toouse la limitazione delle richieste con Gestione risorse di Azure richiede quando sono stati raggiunti i limiti della sottoscrizione.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Limitazione delle richieste di Resource Manager
Per ogni sottoscrizione e tenant, i limiti di gestione risorse richieste too15, 000 all'ora di lettura e scrittura richieste too1, 200 all'ora. Questi limiti si applicano tooeach istanza di gestione risorse di Azure. sono presenti più istanze in ogni area di Azure e Gestione risorse di Azure viene distribuito tooall Azure aree.  Pertanto, in pratica, i limiti sono effettivamente molto superiori a quelli elencati in precedenza, poiché le richieste utente sono in genere gestite da molte istanze diverse.

Se l'applicazione o script raggiunge questi limiti, è necessario toothrottle le richieste. Questo argomento viene illustrato come le richieste di hello toodetermine rimanente è prima di raggiungere il limite di hello e come toorespond quando è stato raggiunto il limite di hello.

Quando si raggiunge il limite di hello, viene visualizzato il codice di stato HTTP hello **429 troppe richieste molti**.

numero di richieste di Hello è tooeither con ambito la sottoscrizione o il tenant. Se si dispone di più, applicazioni simultanee effettua richieste nella sottoscrizione, le richieste di hello da tali applicazioni vengono sommate numero hello toodetermine delle richieste rimanenti.

Le richieste di sottoscrizione con ambito sono quelli hello comportano passando l'id sottoscrizione, ad esempio il recupero dei gruppi di risorse hello nella sottoscrizione. Le richieste nell'ambito del tenant non includono l'ID sottoscrizione, ad esempio il recupero delle posizioni di Azure valide.

## <a name="remaining-requests"></a>Richieste rimanenti
È possibile determinare il numero di hello delle richieste rimanenti esaminando le intestazioni di risposta. Ogni richiesta include i valori per il numero di hello delle richieste di scrittura e lettura rimanente. Hello nella tabella seguente vengono descritte le intestazioni di risposta hello che è possibile esaminare per i valori:

| Intestazione risposta | Descrizione |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |Richieste di lettura rimanenti nell'ambito della sottoscrizione |
| x-ms-ratelimit-remaining-subscription-writes |Richieste di scrittura rimanenti nell'ambito della sottoscrizione |
| x-ms-ratelimit-remaining-tenant-reads |Richieste di lettura rimanenti nell'ambito del tenant |
| x-ms-ratelimit-remaining-tenant-writes |Richieste di scrittura rimanenti nell'ambito del tenant |
| x-ms-ratelimit-remaining-subscription-resource-requests |Richieste di tipo di risorsa rimanenti nell'ambito della sottoscrizione.<br /><br />Il valore dell'intestazione viene restituito solo se un servizio ha eseguito l'override di limite predefinito di hello. Gestione risorse aggiunge questo valore anziché hello sottoscrizione letture o scritture. |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |Richieste di raccolta di tipo di risorsa rimanenti nell'ambito della sottoscrizione.<br /><br />Il valore dell'intestazione viene restituito solo se un servizio ha eseguito l'override di limite predefinito di hello. Questo valore fornisce il numero di hello di richieste di raccolta rimanenti (risorse elenco). |
| x-ms-ratelimit-remaining-tenant-resource-requests |Richieste di tipo di risorsa rimanenti nell'ambito del tenant.<br /><br />Questa intestazione viene aggiunto solo per le richieste a livello di tenant, e solo se un servizio ha eseguito l'override limite predefinito di hello. Gestione risorse aggiunge questo valore anziché hello tenant letture o scritture. |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |Richieste di raccolta di tipo di risorsa rimanenti nell'ambito del tenant.<br /><br />Questa intestazione viene aggiunto solo per le richieste a livello di tenant, e solo se un servizio ha eseguito l'override limite predefinito di hello. |

## <a name="retrieving-hello-header-values"></a>Il recupero dei valori di intestazione hello
Il recupero di questi valori di intestazione nel codice o nello script non è diverso rispetto al recupero di qualsiasi valore di intestazione. 

Ad esempio, in **c#**, si recupera il valore di intestazione hello da un **HttpWebResponse** oggetto denominato **risposta** con hello seguente codice:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

In **PowerShell**, recuperare il valore dell'intestazione hello un'operazione Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

In alternativa, se desidera toosee hello rimanenti richieste per il debug, è possibile fornire hello **-Debug** parametro il **PowerShell** cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

Restituisce molti valori, inclusi hello il valore di risposta seguente:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

In **CLI di Azure**, si recupera il valore dell'intestazione hello utilizzando hello opzione più dettagliato.

```azurecli
azure group list -vv --json
```

Restituisce molti valori, inclusi hello seguente oggetto:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Attesa prima dell'invio della richiesta successiva
Quando si raggiunge il limite di richieste di hello, Gestione risorse restituisce hello **429** codice di stato HTTP e un **Retry-After** valore nell'intestazione di hello. Hello **Retry-After** valore specifica il numero di hello di secondi di attesa dell'applicazione (o sospensione) prima di inviare la richiesta successiva hello. Se si invia una richiesta prima che sia trascorso il valore di retry hello, non è possibile elaborare la richiesta e viene restituito un nuovo valore dei tentativi.

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sui limiti e quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).
* toolearn sulla gestione di richieste REST asincrone, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).
