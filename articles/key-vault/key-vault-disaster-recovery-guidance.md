---
title: toodo aaaWhat nell'evento hello di un'interruzione del servizio Azure che interessa l'insieme di credenziali chiave di Azure | Documenti Microsoft
description: Informazioni su quali toodo nell'evento hello di un'interruzione del servizio Azure che interessa l'insieme di credenziali chiave di Azure.
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Disponibilità e ridondanza dell'insieme di credenziali delle chiavi di Azure
Insieme di credenziali chiave di Azure offre più livelli di ridondanza toomake assicurarsi che le chiavi e segreti rimangono disponibili tooyour applicazione anche se i singoli componenti di hello del servizio hanno esito negativo.

Hello contenuto di credenziali delle chiavi viene replicati all'interno di area hello e area secondaria tooa almeno 150 miglia immediatamente, ma all'interno di hello geography stesso. Questo garantisce un'elevata durabilità delle chiavi e dei segreti. Vedere hello [Azure abbinato aree](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) per informazioni dettagliate su una coppia di area specifico.

Se i singoli componenti all'interno del servizio dell'insieme di credenziali chiave hello hanno esito negativo, componenti alternativi all'interno di area hello passaggio tooserve toomake la richiesta che vi sia alcuna riduzione delle funzionalità. Non è necessario tootake tootrigger qualsiasi azione questo. Viene eseguita automaticamente e sarà tooyou trasparente.

In evento raro hello che non è disponibile un'intera regione di Azure, le richieste di hello apportate dell'insieme di credenziali chiave di Azure in tale area vengono indirizzate automaticamente (*failover*) area secondaria tooa. Quando l'area primaria hello è nuovamente disponibile, le richieste vengono indirizzate nuovamente (*non è stato possibile eseguire il*) area primaria toohello. Nuovamente, non è necessario tootake alcuna azione perché ciò avviene automaticamente.

Esistono alcuni aspetti toobe conoscere:

* Nell'evento hello di un failover di area, potrebbe richiedere alcuni minuti per hello servizio toofail. Le richieste effettuate durante questo periodo potrebbero non riuscire finché non viene completato il failover hello.
* Dopo il completamento del failover, l'insieme di credenziali delle chiavi è in modalità di sola lettura. Le richieste supportate in questa modalità sono le seguenti:
  * List key vaults
  * Get properties of key vaults
  * List secrets
  * Get secrets
  * List keys
  * Get (properties of) keys
  * Crittografare il contenuto
  * Decrypt
  * Wrap
  * Unwrap
  * Verificare
  * Sign
  * Backup
* Dopo il failback di un failover, tutti i tipi di richiesta, ad esempio le richieste di lettura *e* scrittura, risultano disponibili.

