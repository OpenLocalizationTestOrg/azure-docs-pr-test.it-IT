---
title: Guida aaaSupportability e sul ritiro di criteri per il sistema operativo Guest Azure | Documenti Microsoft
description: "Fornisce informazioni su cosa Microsoft supporterà per toohello del sistema operativo Guest Azure utilizzati dai servizi Cloud."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Criteri relativi al supporto e al ritiro del sistema operativo guest di Azure
informazioni di Hello in questa pagina si riferiscono sistema operativo Guest Azure di toohello ([del sistema operativo Guest](cloud-services-guestos-update-matrix.md)) per i servizi Cloud web e lavoro ruoli (PaaS). Non è applicabile macchine tooVirtual (IaaS).

Microsoft dispone di un report pubblicato [criteri di supporto per sistemi operativi Guest hello](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). pagina Hello che si sta leggendo viene ora implementazione dei criteri di hello.

criteri di Hello è

1. Microsoft supporterà **almeno hello ultime due famiglie del sistema operativo Guest hello**. Quando una famiglia viene ritirata, i clienti hanno 12 mesi dalla hello ufficiale di ritiro data tooupdate tooa famiglia supportata più recente del sistema operativo Guest.
2. Microsoft supporterà **almeno hello ultime due versioni delle famiglie del sistema operativo Guest supportato hello**.
3. Microsoft supporterà **almeno hello ultime due versioni di Azure SDK hello**. Quando una versione di hello che SDK viene ritirata, i clienti avranno 12 mesi dalla versione più recente di hello ufficiale di ritiro data tooupdate tooa.

Talvolta è possibile che siano supportati più di due rilasci o famiglie. Informazioni ufficiali di supporto del sistema operativo Guest verranno visualizzato nella hello [rilasci del sistema operativo Guest Azure e matrice di compatibilità SDK](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Ritiro di una famiglia o una versione del sistema operativo guest
Un nuovo sistema operativo Guest **famiglia** viene introdotta un po' dopo il rilascio di hello di una nuova versione ufficiale del sistema operativo di Windows Server hello. Ogni volta che viene introdotta una nuova famiglia di sistemi operativi Guest, Microsoft ritirerà famiglia di sistemi operativi meno recente hello.

Nuovo sistema operativo Guest **versioni** vengono rilasciate pressoché ogni mese tooincorporate hello ultimi aggiornamenti di MSRC. A causa di hello aggiornamenti regolari mensili, una versione del sistema operativo Guest è in genere disabilitate 60 giorni dopo il relativo rilascio. In questo modo sono disponibili per l'uso almeno due versioni del sistema operativo guest per ogni famiglia.

### <a name="process-during-a-guest-os-family-retirement"></a>Procedura di ritiro della famiglia di sistemi operativi guest
Una volta che viene annunciato il ritiro di hello, i clienti hanno un periodo di transizione"12 mesi" prima di famiglia di hello precedente venga ufficialmente rimossa dal servizio. Questo periodo di transizione può essere esteso a discrezione di hello di Microsoft. Gli aggiornamenti vengono pubblicati in hello [rilasci del sistema operativo Guest Azure e matrice di compatibilità SDK](cloud-services-guestos-update-matrix.md).

Un processo di ritiro graduale inizierà sei (6) mesi nel periodo di transizione hello. In questo periodo di tempo:

1. Microsoft informerà i clienti del ritiro hello.
2. versione più recente di Hello di hello Azure SDK non supporterà la famiglia di sistemi operativi ritirata hello.
3. Le nuove distribuzioni e ridistribuzioni di servizi Cloud non saranno consentite per la famiglia ritirata hello

Microsoft continuerà toointroduce nuova versione del sistema operativo Guest che includa ultimi aggiornamenti di MSRC hello fino a quando l'ultimo giorno del periodo di transizione hello, noto come "Data di scadenza" hello hello. Data di scadenza hello, non saranno supportati i servizi Cloud ancora in esecuzione in hello SLA di Azure. Microsoft ha hello discrezione tooforce aggiornare, eliminare o arrestare tali servizi dopo tale data.

### <a name="process-during-a-guest-os-version-retirement"></a>Processo durante il ritiro della versione del sistema operativo guest
Se i clienti hanno impostato l'aggiornamento di tooautomatically del sistema operativo Guest, hanno mai tooworry sulla gestione di versioni del sistema operativo Guest. Sempre che useranno hello del sistema operativo Guest più recente.

Le versioni del sistema operativo guest vengono rilasciate ogni mese. A causa di frequenza hello dei rilasci regolari, ogni versione ha una durata fissa.

Dopo 60 giorni nel ciclo di vita di hello, è una versione "*disabilitato*". "Disabilitato" significa che la versione hello viene rimosso dal portale hello. versione di Hello non può più essere impostate dal file di configurazione CSCFG hello. Le distribuzioni esistenti rimangono in esecuzione, Ma nuove distribuzioni e le distribuzioni tooexisting di aggiornamenti di codice e la configurazione non saranno consentite.

Versione del sistema operativo Guest di hello qualche tempo dopo diventi "disabled", "*scadenza*" e le installazioni che ancora eseguono quella versione vengono forzate all'aggiornamento e impostate tooautomatically hello di aggiornamento del sistema operativo Guest in hello future. Scadenza viene eseguita in batch in modo hello periodo di tempo dalla disabilitazione tooexpiration può variare.

Questi periodi possono essere resi più lunghi alle transizioni del cliente tooease discrezione di Microsoft. Tutte le modifiche verranno comunicate in hello [rilasci del sistema operativo Guest Azure e matrice di compatibilità SDK](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Notifiche durante il ritiro
* **Ritiro della famiglia** <br>Microsoft userà i post di blog e la notifica tramite il portale. I clienti che utilizzano ancora una famiglia di sistemi operativi Guest ritirata verranno informati tramite gli amministratori del servizio tooassigned comunicazione diretta (e-mail, messaggi sul portale, telefonata). Tutte le modifiche verranno registrate toothis pagina e hello feed RSS verrà elencato all'inizio di hello di questa pagina.
* **Ritiro della versione** <br>Tutte le modifiche e si verificano le date di hello verranno registrate toothis pagina e hello feed RSS verrà elencato all'inizio di hello di questa pagina, inclusa una scadenza, disabilitato e la versione. Se sono presenti distribuzioni in esecuzione su una versione o famiglia di sistemi operativi guest disabilitata, verranno inviati appositi messaggi e-mail agli amministratori dei servizi. intervallo di Hello di tali messaggi può variare. In genere vengono inviati almeno un mese prima della disabilitazione, anche se questo non rappresenta un impegno contrattuale di servizio.

## <a name="frequently-asked-questions"></a>Domande frequenti
**Come è possibile ridurre l'impatto hello di migrazione?**

Per progettare i Servizi cloud è consigliabile usare la famiglia di sistemi operativi guest più recente.

1. Iniziare la pianificazione della famiglia più recente di tooa migrazione anticipata.
2. Consente di impostare tootest le distribuzioni di test temporanea del servizio Cloud in esecuzione in una nuova famiglia hello.
3. Impostare la versione del sistema operativo Guest troppo**automatica** (osVersion = * in hello [cscfg](cloud-services-model-and-package.md#cscfg) file) in modo le versioni del sistema operativo Guest di hello migrazione toonew viene eseguita automaticamente.

**Cosa accade se l'applicazione web richiede una maggiore integrazione con hello del sistema operativo?**

Se l'architettura dell'applicazione web dipende da funzionalità sottostanti del sistema operativo hello, usare funzionalità supportate della piattaforma, ad esempio [le attività di avvio](cloud-services-startup-tasks.md) o altri meccanismi di estendibilità. In alternativa, è inoltre possibile utilizzare [macchine virtuali di Azure](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS, infrastruttura come servizio), in cui si è responsabile della gestione hello sottostante del sistema operativo.

## <a name="next-steps"></a>Passaggi successivi
Hello revisione più recente [versioni del sistema operativo Guest](cloud-services-guestos-update-matrix.md).
