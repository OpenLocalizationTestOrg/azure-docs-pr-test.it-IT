---
ms.assetid: 
title: Guida di limitazione delle richieste di insieme di credenziali chiave aaaAzure | Documenti Microsoft
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Guida alla limitazione delle richieste per Azure Key Vault

La limitazione delle richieste è un processo si avvia che limita il numero di hello di chiamate simultanee toohello servizio Azure tooprevent utilizzo eccessivo di risorse. Insieme di credenziali di chiave di Azure (insieme) è progettata toohandle un volume elevato di richieste. Se si verifica un numero eccessivo di richieste, la limitazione delle richieste del client consente di garantire prestazioni ottimali e l'affidabilità del servizio AKV hello.

I limiti di limitazione delle richieste variano in base uno scenario di hello. Ad esempio, se si sta eseguendo un volume elevato di operazioni di scrittura, il possibilità hello di limitazione delle richieste è maggiore se si eseguono solo letture.

## <a name="how-does-key-vault-handle-its-limits"></a>Gestione dei limiti da parte di Key Vault

Limiti dei servizi nell'insieme di credenziali chiave sono presenti un utilizzo improprio tooprevent delle risorse e assicurare la qualità del servizio per tutti i client dell'insieme di credenziali di chiave. Quando si supera la soglia di un servizio, Key Vault limita le nuove richieste del client per un periodo di tempo. In questo caso, l'insieme di credenziali chiave restituisce il codice di stato HTTP 429 (eccessivo numero di richieste), e di errore delle richieste hello. Inoltre, non è stato possibile richieste che restituiscono un conteggio 429 verso i limiti di velocità hello monitorate dall'insieme di credenziali chiave. 

Nel caso l'utente abbia delle esigenze aziendali per cui sono necessarie delle limitazioni maggiori, contattare Microsoft.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Come toothrottle l'applicazione in risposta tooservice limita

Hello di seguito sono **consigliate** per la limitazione dell'app:
- Ridurre il numero di hello delle operazioni per ogni richiesta.
- Ridurre la frequenza hello delle richieste.
- Evitare tentativi immediati. 
    - Tutte le richieste si accumulano per i limiti di consumo.

Quando si implementa la gestione degli errori dell'applicazione, utilizzare hello HTTP Errore codice 429 toodetect hello necessario per la limitazione sul lato client. Se è richiesta hello ha nuovamente esito negativo con un codice di errore HTTP 429, continuano a verificarsi il limite di un servizio di Azure. Continuare toouse hello consigliato metodo limitazione sul lato client, nuovo tentativo di richiesta di hello fino al completamento.

### <a name="recommended-client-side-throttling-method"></a>Metodo consigliato per la limitazione delle richieste lato client

Quando si genera il codice di errore HTTP 429, iniziare a limitare le richieste del client con un approccio di backoff esponenziale:

1. Attendere 1 secondo e ripetere la richiesta
2. Se viene ancora limitata, attendere 2 secondi e ripetere la richiesta
3. Se viene ancora limitata, attendere 4 secondi e ripetere la richiesta
4. Se viene ancora limitata, attendere 8 secondi e ripetere la richiesta
5. Se viene ancora limitata, attendere 16 secondi e ripetere la richiesta

A questo punto, il codice di risposta HTTP 429 dovrebbe non essere più visualizzato.

## <a name="see-also"></a>Vedere anche

Per un orientamento più approfondito della limitazione delle richieste in hello Cloud Microsoft, vedere [limitazione modello](https://docs.microsoft.com/azure/architecture/patterns/throttling).

