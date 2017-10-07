---
ms.assetid: 
title: l'eliminazione temporanea insieme di credenziali chiave aaaAzure | Documenti Microsoft
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Panoramica di eliminazione temporanea di Azure Key Vault

Funzionalità di eliminazione temporanea dell'insieme di credenziali di chiave consente il recupero di archivi hello eliminato e gli oggetti di insieme di credenziali, noti come temporaneamente eliminato. In particolare, è l'indirizzo hello seguenti scenari:

- Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi
- Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi (ad esempio, chiavi, segreti e certificati)

## <a name="supporting-interfaces"></a>Interfacce di supporto

Hello funzionalità soft delete è inizialmente disponibile tramite hello REST, .NET / c# e PowerShell di interfacce. Per questi per ulteriori informazioni, vedere Riferimenti toohello [riferimento insieme di credenziali chiave](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Scenari

Gli insiemi di credenziali delle chiavi di Azure sono risorse tracciate, gestite da Azure Resource Manager. Azure Resource Manager specifica anche un comportamento ben definito per l'eliminazione, in base al quale al termine dell'operazione di eliminazione la risorsa non deve essere più accessibile. gli indirizzi di funzionalità di soft-eliminazione Hello hello ripristino dell'oggetto eliminato hello, se è stata l'eliminazione di hello accidentali o intenzionali.

1. In uno scenario tipico di hello, un utente potrebbe avere inavvertitamente eliminato un insieme di credenziali chiave o un oggetto chiave dell'insieme di credenziali. Se tale chiave o un insieme di credenziali chiave dell'insieme di credenziali oggetto sono state toobe ripristinabili per un periodo predeterminato, utente hello può annullare l'eliminazione di hello e ripristinare i dati.

2. In uno scenario diverso, un utente non autorizzato potrebbe tentare toodelete un insieme di credenziali chiave o un oggetto di insieme di credenziali chiave, ad esempio una chiave all'interno di un insieme di credenziali, toocause un'interruzione di business. Separazione eliminazione hello dell'insieme di credenziali chiave hello o insieme di credenziali delle chiavi dell'oggetto dall'eliminazione effettiva di hello di hello sottostante dei dati può essere utilizzata come misura di sicurezza, ad esempio, limitando le autorizzazioni per tooa l'eliminazione di dati diverso, attendibili ruolo. Con questo approccio, infatti, è necessario un quorum per un'operazione che, altrimenti, determinerebbe una perdita immediata di dati.

### <a name="soft-delete-behavior"></a>Comportamento della funzione di eliminazione temporanea

Con questa funzionalità, operazione DELETE su un insieme di credenziali chiave di hello o oggetto insieme di credenziali delle chiavi è una soft-eliminazione, in modo efficace tenendo risorse hello per un periodo di memorizzazione specificato, fornendo aspetto hello oggetto hello viene eliminato. servizio Hello ulteriormente fornisce un meccanismo per il ripristino oggetto hello eliminato, essenzialmente annullamento eliminazione hello. 

L'eliminazione temporanea è un comportamento facoltativo di Key Vault e in questa versione **non è abilitato per impostazione predefinita**. Per ulteriori informazioni sull'abilitazione di soft-eliminazione per l'insieme di credenziali chiave, vedere una Guida specifica nella Guida di riferimento per l'interfaccia hello di propria scelta, hello hello [riferimento insieme di credenziali chiave](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Recupero di un insieme di credenziali delle chiavi

In seguito all'eliminazione di un insieme di credenziali chiave, il servizio di hello crea una risorsa di proxy in sottoscrizione hello, aggiunta di metadati sufficienti per il ripristino. risorse di Hello proxy sono un oggetto archiviato, disponibile in hello stessa posizione dell'insieme di credenziali chiave hello eliminato. 

### <a name="key-vault-object-recovery"></a>Recupero di un oggetto di un insieme di credenziali delle chiavi

In seguito all'eliminazione di un oggetto chiave dell'insieme di credenziali, ad esempio una chiave, servizio hello inseriranno oggetto hello in uno stato eliminato, rendendo così le operazioni di recupero tooany inaccessibile. In questo stato, oggetto insieme di credenziali chiave hello può solo essere elencato, ripristinato o eliminato in modo forzato/in modo permanente. 

In hello stesso insieme di credenziali delle chiavi, tempo pianificherà l'eliminazione di hello di hello sottostante toohello corrispondente di dati eliminato insieme di credenziali chiave o un oggetto chiave dell'insieme di credenziali per l'esecuzione dopo un intervallo di conservazione predeterminato. Hello DNS record toohello insieme di credenziali corrispondente viene mantenuto anche per la durata di hello dell'intervallo di conservazione hello.

### <a name="soft-delete-retention-period"></a>Periodo di memorizzazione dell'eliminazione temporanea

Le risorse eliminate in modo temporaneo vengono conservate per un periodo di tempo prestabilito di 90 giorni. Durante l'intervallo di conservazione di soft-eliminazione hello, si applicano i seguenti hello:

- È possibile elencare tutti gli insiemi di credenziali chiave hello e gli oggetti chiave dell'insieme di credenziali in stato di soft-eliminazione hello per le sottoscrizioni, nonché informazioni di ripristino e l'eliminazione di accesso su di essi.
    - Gli insiemi di credenziali delle chiavi eliminati possono essere elencati solo da utenti con autorizzazioni speciali. Per la gestione degli insiemi di credenziali delle chiavi eliminati è consigliabile creare un ruolo personalizzato a cui assegnare queste autorizzazioni speciali.
- Un insieme di credenziali chiave con nome stesso può essere creata in hello hello stessa posizione; di conseguenza, un insieme di credenziali chiave Impossibile creare l'oggetto in un determinato insieme di credenziali se tale insieme di credenziali chiave contiene un oggetto con hello stesso nome e che è in uno stato eliminato 
- Solo un utente con privilegi in particolare è possibile ripristinare una chiave dell'insieme di credenziali o un oggetto di insieme di credenziali chiave eseguendo il comando Ripristina sulla risorsa proxy corrispondente hello.
    - utente Hello, membro del ruolo personalizzata hello, che dispone dei privilegi di hello toocreate un insieme di credenziali chiave nel gruppo di risorse hello possibile ripristinare l'insieme di credenziali hello.
- Solo un utente con privilegi in modo specifico forzatamente può eliminare un insieme di credenziali chiave o un oggetto di insieme di credenziali chiave eseguendo il comando delete sulla risorsa proxy corrispondente hello.

A meno che non viene recuperato un insieme di credenziali delle chiavi o chiave dell'insieme di credenziali, hello end del servizio di hello memorizzazione intervallo hello esegue una pulizia dell'insieme di credenziali chiave hello eliminato o oggetto insieme di credenziali chiave e il relativo contenuto. È possibile che l'eliminazione della risorsa non venga ripianificata.

### <a name="permitted-purge"></a>Ripulitura consentita

In modo permanente l'eliminazione, l'eliminazione, un insieme di credenziali chiave è possibile tramite un'operazione POST sulla risorsa proxy hello e richiede privilegi speciali. In genere, solo il proprietario di sottoscrizione hello sarà in grado di toopurge un insieme di credenziali chiave. i trigger di operazione POST Hello hello immediato e irreversibile l'eliminazione dell'insieme di credenziali. 

Toothis un'eccezione è il caso hello hello sottoscrizione di Azure è stato contrassegnato come *cancellabile*. In questo caso, solo il servizio hello può quindi eseguire l'eliminazione effettiva hello e a tale scopo come un processo pianificato. 



