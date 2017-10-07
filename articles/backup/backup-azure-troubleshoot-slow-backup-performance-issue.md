---
title: backup di lenta aaaTroubleshoot di file e cartelle in Backup di Azure | Documenti Microsoft
description: Fornisce la risoluzione dei problemi toohelp indicazioni per la diagnosi causa hello dei problemi di prestazioni di Backup di Azure
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Risolvere i problemi di rallentamento delle prestazioni di backup di file e cartelle in Backup di Azure
In questo articolo vengono fornite indicazioni sulla risoluzione dei problemi toohelp si diagnosticare hello causa del rallentamento delle prestazioni di backup di file e cartelle, quando si utilizza il Backup di Azure. Quando si usa hello Azure Backup agent tooback dei file, processo di backup hello potrebbe richiedere più tempo del previsto. Questo ritardo può essere causato da uno o più dei seguenti hello:

* [Sono presenti eventuali colli di bottiglia nel computer di hello che viene eseguito il backup.](#cause1)
* [Un altro processo o del software antivirus interferisce con hello il processo di Backup di Azure.](#cause2)
* [l'agente di Backup Hello è in esecuzione in una macchina virtuale di Azure (VM).](#cause3)  
* [Viene eseguito il backup di un numero elevato di file (milioni).](#cause4)

Prima di iniziare la risoluzione dei problemi, si consiglia di scaricare e installare hello [più recenti dell'agente Azure Backup](http://aka.ms/azurebackup_agent). È apportare aggiornamenti frequenti toohello Backup agente toofix vari problemi, aggiungere le funzionalità e migliorare le prestazioni.

È inoltre consigliabile esaminare hello [domande frequenti su servizio di Backup di Azure](backup-azure-backup-faq.md) toomake che non si verificano uno hello comuni di problemi di configurazione.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Causa: Colli di bottiglia delle prestazioni nel computer di hello
Colli di bottiglia sui computer hello che viene eseguito il backup possono causare ritardi. Ad esempio, hello toodisk tooread o di scrittura di capacità del computer, o dati toosend larghezza di banda disponibile in rete hello, può causare colli di bottiglia.

Windows fornisce uno strumento incorporato che viene chiamato [Performance Monitor](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) toodetect (Perfmon) i colli di bottiglia.

Ecco alcuni contatori delle prestazioni e intervalli che possono essere utili per diagnosticare i colli di bottiglia e ottenere backup ottimali.

| Contatore | Stato |
| --- | --- |
| Disco logico (disco fisico) - % inattività |• too50 inattivo 100% % inattivo = integro</br>• too20 inattivo 49% % inattivo = avviso o un monitoraggio</br>• too0 inattivo % 19% inattivo = critico o specifiche |
| Disco logico (disco fisico) - % Media letture o scritture disco/sec |• 0,001 ms too0.015 ms = integro</br>• 0.015 ms too0.025 ms = avviso o un monitoraggio</br>• Da ms 0,026 e oltre = critico o fuori specifica |
| Disco logico (disco fisico) - Lunghezza corrente coda del disco (per tutte le istanze) |80 richieste per più di 6 minuti |
| Memoria - Byte del pool non di paging |• Meno del 60% del pool utilizzato = integro<br>• il 61% too80% del pool utilizzate = avviso o un monitoraggio</br>• Più dell'80% del pool utilizzato = critico o fuori specifica |
| Memoria - Byte del pool di paging |• Meno del 60% del pool utilizzato = integro</br>• il 61% too80% del pool utilizzate = avviso o un monitoraggio</br>• Più dell'80% del pool utilizzato = critico o fuori specifica |
| Memoria - MByte disponibili |• 50% o più di memoria libera disponibile = integro</br>• 25% di memoria libera disponibile = monitoraggio</br>• 10% di memoria libera disponibile = avviso</br>• Meno di 100 MB o 5% della memoria disponibile = critico o fuori specifica |
| Processore - \%Tempo processore (tutte le istanze) |• Meno del 60% utilizzato = integro</br>• il 61% too90% utilizzati = monitoraggio o attenzione</br>• too100 91% % utilizzati = avviso critico |

> [!NOTE]
> Se si determina che l'infrastruttura di hello è provocato da hello, è consigliabile che la deframmentazione dischi hello regolarmente per ottenere prestazioni migliori.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Causa: Un altro processo o un software antivirus interferisce con Backup di Azure
Abbiamo visto più istanze in cui altri processi nel sistema di Windows hello sono influenzate negativamente sulle prestazioni di hello processo dell'agente di Backup di Azure. Ad esempio, se utilizzare l'agente di Backup di Azure hello e un altro programma tooback dei dati o se è in esecuzione un software antivirus e un blocco su file toobe ha eseguito il backup, hello più blocchi sui file potrebbero causare conflitti. In questo caso, potrebbe non riuscire backup hello o processo hello potrebbe richiedere più tempo del previsto.

Hello indicazione migliore in questo scenario è tooturn off hello toosee altro programma di backup se viene modificato l'ora del backup hello di hello Azure Backup agent. In genere, assicurandosi che non eseguono più processi di backup contemporaneamente hello è sufficiente tooprevent di influire su altro.

Per i programmi antivirus, è consigliabile escludere i seguenti hello percorsi di file e:

* C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\bin\cbengine.exe come processo
* Cartelle in C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\
* Percorso dei file temporanei (se non si utilizza la posizione standard hello)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Causa: L'agente di Backup è in esecuzione in una macchina virtuale di Azure
Se si esegue l'agente di Backup hello in una macchina virtuale, è possibile che le prestazioni risulterà più lenta rispetto a quando viene eseguito in un computer fisico. È previsto a causa di limitazioni tooIOPS.  Tuttavia, è possibile ottimizzare le prestazioni di hello passando le unità dati hello sottoposti a backup tooAzure archiviazione Premium. Si sta lavorando correggere il problema e correzione hello sarà disponibile nelle versioni future.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Causa: Viene eseguito il backup di un numero elevato di file (milioni)
Lo spostamento di un grande volume di dati richiederà più tempo rispetto allo spostamento di un volume di dati inferiore. In alcuni casi, l'ora del backup è correlato toonot hello solo dimensioni di dati hello, ma anche il numero di hello di file o cartelle. Ciò vale soprattutto quando milioni di file di piccole dimensioni (pochi byte tooa alcuni kilobyte) viene eseguito il.

Questo comportamento è dovuto al fatto che mentre si esegue il backup dei dati hello e spostandola tooAzure, Azure contemporaneamente la catalogazione dei file. In alcuni casi rari, l'operazione di catalogo hello potrebbe richiedere più tempo del previsto.

Hello seguendo gli indicatori consentono di comprendere collo di bottiglia hello e di conseguenza lavorare sui passaggi successivi hello:

* **Interfaccia utente viene visualizzato lo stato di avanzamento per il trasferimento di dati hello**. dati Hello ancora trasferiti. larghezza di banda Hello o dimensioni hello dei dati possono causare ritardi.
* **Interfaccia utente non viene visualizzato lo stato di avanzamento per il trasferimento di dati hello**. Hello Open log si trova in C:\Microsoft Azure Recovery Services Agent\Temp e quindi verificare la hello FileProvider::EndData voce nel log di hello. Questa voce indica che il trasferimento dei dati hello completato e avviene l'operazione di catalogo hello. Non annullare i processi di backup hello. Al contrario, attendere un po' più hello catalogo operazione toofinish. Se hello problema persiste, contattare [supporto tecnico di Azure](https://portal.azure.com/#create/Microsoft.Support).
