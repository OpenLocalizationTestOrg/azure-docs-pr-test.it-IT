---
title: aaaStorSimple localmente bloccato volumi domande frequenti | Documenti Microsoft
description: Fornisce le risposte toofrequently frequenti domande su StorSimple locale aggiunto volumi.
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/26/2017
ms.author: manuaery
ms.openlocfilehash: a3a6557ca15e7e1947b45dcfd005640103c09591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>Volumi aggiunti in locale di StorSimple: domande frequenti
## <a name="overview"></a>Panoramica
di seguito Hello sono domande e risposte che possono verificarsi quando si crea un volume aggiunto in locale StorSimple, conversione di un volume a livelli tooa aggiunto in locale (e viceversa), o eseguire il backup e ripristino di un volume aggiunto in locale.

Domande e risposte sono disposti in hello seguenti categorie

* Creazione di un volume aggiunto in locale
* Backup di un volume aggiunto in locale
* Conversione di un volume aggiunto in locale tooa volume a livelli
* Ripristino di un volume aggiunto in locale
* Failover di un volume aggiunto in locale

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Domande sulla creazione di un volume aggiunto in locale
**D.** Che cos'è una dimensione massima di hello di un volume aggiunto in locale che è possibile creare su dispositivi serie 8000 hello?

**Oggetto** nei dispositivi che eseguono StorSimple 8000 Series Update 3.0, è possibile effettuare il provisioning di volumi aggiunti in locale fino too8.5 TB o i volumi a livelli di too200 TB sul dispositivo 8100 hello. Nel dispositivo 8600 hello più grande, è possibile eseguire il provisioning di volumi aggiunti in locale fino too22.5 TB o i volumi a livelli di too500 TB.

**D.** Aggiornato di recente my tooUpdate dispositivo 8100 3.0 e quando si tenta di toocreate un volume aggiunto in locale, dimensione massima disponibile di hello è solo 6 TB e non 8,5 TB. Perché non è possibile creare un volume di 8.5 TB?

**Oggetto** se il dispositivo sta eseguendo l'aggiornamento 3.0, è possibile eseguire il provisioning di volumi aggiunti in locale fino too8.5 TB o i volumi a livelli di too200 TB in hello dispositivo 8100. Se il dispositivo ha già a livelli volumi, spazio hello disponibile per la creazione di un volume aggiunto in locale sarà proporzionalmente inferiore a questo limite massimo. Ad esempio, se circa 106 TB dei volumi a livelli è già stato eseguito il provisioning sul dispositivo 8100 (che rappresenta la metà di hello a più livelli capacità), quindi hello la dimensione massima di un volume locale che è possibile creare il dispositivo 8100 hello sarà ridotto too4 TB ( circa la metà del numero massimo di hello localmente bloccata capacità del volume).

Poiché alcuni spazio locale nel dispositivo hello è hello toohost usato l'utilizzo di set di volumi a livelli, lo spazio disponibile di hello per la creazione di un volume aggiunto in locale viene ridotto se il dispositivo hello è a più livelli di volumi. Al contrario, la creazione di un volume aggiunto in locale in modo proporzionale riduce lo spazio disponibile di hello per i volumi a livelli. Hello le tabelle seguenti vengono riepilogate capacità a più livelli hello disponibile nei dispositivi hello 8100 e 8600 quando vengono creati i volumi aggiunti in locale.

#### <a name="update-30"></a>Aggiornamento 3.0 
| Capacità volumi aggiunti in locale di cui è stato effettuato il provisioning | Capacità disponibile toobe effettuato il provisioning per i volumi a livelli - 8100 | Capacità disponibile toobe effettuato il provisioning per i volumi a livelli - 8600 |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176.5 TB |477.8 TB |
| 4 TB |105.9 TB |411.1 TB |
| 8.5 TB |0 TB |311.1 TB |
| 10 TB |ND |277.8 TB |
| 15 TB |ND |166.7 TB |
| 22.5 TB |ND |0 TB |

**D.** Perché la creazione di un volume aggiunto in locale è un'operazione di lunga durata?

**R.** Viene effettuato il thick provisioning dei volumi aggiunti in locale. spazio toocreate su hello livelli locali del dispositivo hello, alcuni dati dai volumi a livelli esistenti potrebbero essere inseriti toohello cloud durante il processo di provisioning hello. E poiché questo dipende dalla dimensione di hello del volume hello in corso il provisioning dei dati esistenti di hello sul dispositivo e hello larghezza di banda disponibile toohello cloud, il tempo di hello impiegato toocreate che un volume locale può essere diverse ore.

**D.** Quanto tempo occorre toocreate un volume aggiunto in locale?

**R.** Poiché i volumi aggiunti in locale sono stati sottoposti a thick provisioning, alcuni dati dai volumi a livelli esistenti potrebbero inseriti toohello cloud durante il processo di provisioning hello. Pertanto, hello scattato toocreate un volume aggiunto in locale dipende da vari fattori, tra cui hello dimensione del volume di hello, hello dati nel dispositivo e hello larghezza di banda disponibile. In un dispositivo appena installato che non dispone di alcun volume, hello tempo toocreate un volume aggiunto in locale è di circa 10 minuti per terabyte di dati. Tuttavia, la creazione di volumi locali può richiedere diverse ore in base a fattori hello illustrati in precedenza in un dispositivo in uso.

**D.** Si desidera toocreate un volume aggiunto in locale. Sono presenti eventuali procedure consigliate, che è necessario conoscere toobe?

**R.** I volumi aggiunti in locale sono adatti per carichi di lavoro che richiedono garanzie locale dei dati in qualsiasi momento e sono riservate toocloud latenze. Prendendo in considerazione l'utilizzo di volumi locali per tutti i carichi di lavoro, tenere presente i seguenti hello:

* Volumi aggiunti in locale sono stati sottoposti a thick provisioning e la creazione di volumi locali influisce sullo spazio disponibile di hello per i volumi a livelli. È quindi consigliabile iniziare con volumi più piccoli e aumentarli parallelamente ai requisiti di archiviazione.
* Il provisioning dei volumi locali è un'operazione a esecuzione prolungata che può comportare il push dei dati esistenti dal cloud toohello volumi a livelli. Di conseguenza, questi volumi possono subire un calo delle prestazioni.
* Il provisioning di volumi locali è un'operazione dispendiosa in termini di tempo. Hello effettivo tempi dipendono da numerosi fattori: hello dimensione del volume hello in corso il provisioning, i dati sul dispositivo e larghezza di banda disponibile. Se non è stato effettuato il backup del cloud di toohello volumi esistenti, la creazione del volume è più lenta. Prima del provisioning di un volume locale, è consigliabile acquisire snapshot nel cloud dei volumi esistenti.
* È possibile convertire i volumi toolocally bloccato volumi a livelli esistenti e questa conversione comporta il provisioning di spazio sul dispositivo hello per hello risultante volume aggiunto in locale (in aggiunta toobringing verso il basso di dati a più livelli, se presente, dal cloud hello). Questa è poi un'operazione di lunga durata che dipende dai fattori illustrati sopra. Si consiglia di eseguire il backup del tooconversion precedente di volumi esistenti come processo hello risulterà anche più lenta se i volumi esistenti non vengono sottoposti a backup. Il dispositivo può anche subire un calo delle prestazioni durante questo processo.

Ulteriori informazioni su come troppo[creare un volume aggiunto in locale](storsimple-8000-manage-volumes-u2.md#add-a-volume)

**D.** È possibile creare più volumi aggiunti in locale in hello contemporaneamente?

**R.** Sì, ma tutti i processi di creazione ed espansione dei volumi aggiunti in locale vengono elaborati in sequenza.

Volumi aggiunti in locale sono stati sottoposti a thick provisioning e ciò richiede la creazione dello spazio locale nel dispositivo hello (che potrebbe comportare dati esistenti di volumi a livelli toobe inserito toohello cloud durante il processo di provisioning hello). Se quindi è in corso un processo di provisioning, gli altri processi di creazione di volumi locali verranno accodati fino al termine di tale processo.

Analogamente, se un volume locale esistente viene espansa o viene convertito un volume a livelli localmente tooa aggiunta volume, quindi hello creazione di un nuovo volume aggiunto in locale è in coda fino al completamento di processo precedente hello. Espansione hello spazio hello esistente locale per il volume è necessario espandere hello dimensioni di un volume aggiunto in locale. Conversione da un volume a livelli toolocally bloccato implica anche la creazione di hello dello spazio locale per hello risultante volume aggiunto in locale. In entrambe le operazioni la creazione o l'espansione dello spazio locale è un processo di lunga durata.

È possibile visualizzare tali processi in hello **processi** blade di hello del servizio di gestione di dispositivi StorSimple. Hello processo attivamente elaborati viene continuamente aggiornato lo stato di avanzamento di tooreflect hello del provisioning di spazio. Hello rimanenti processi volume aggiunto in locale viene contrassegnato come in esecuzione, ma lo stato di avanzamento è bloccato e vengono prelevati in ordine di hello che vengono messe in coda.

**D.** È stato eliminato un volume aggiunto in locale. Perché non è presente spazio hello recuperato riflessi nello spazio disponibile hello quando si tenta di toocreate un nuovo volume?

**R.** Se si elimina un volume aggiunto in locale, spazio hello disponibile per nuovi volumi non può essere aggiornato immediatamente. Servizio di gestione di dispositivi StorSimple Hello Aggiorna hello locale spazio circa ogni ora. Si consiglia di attendere un'ora prima di tentare di nuovo volume di toocreate hello.

**D.** I volumi aggiunti in locale sono supportati nel dispositivo cloud hello?

**R.** I volumi aggiunti in locale non sono supportati nel dispositivo cloud hello (8010 e 8020 dispositivi indicati in precedenza tooas hello dispositivo virtuale StorSimple).

**D.** È possibile utilizzare toocreate i cmdlet di Azure PowerShell hello e gestire i volumi aggiunti in locale?

**R.** No, non è possibile creare volumi aggiunti in locale con i cmdlet di Azure PowerShell. Eventuali volumi creati con Azure PowerShell sono a livelli. È inoltre consigliabile non utilizzare hello Azure PowerShell cmdlet toomodify tutte le proprietà di un volume aggiunto in locale, come che verranno hanno hello indesiderato effetto della modifica hello volume tipo tootiered.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Domande sul backup di un volume aggiunto in locale
**D.** Gli snapshot locali dei volumi aggiunti in locale sono supportati?

**R.** Sì, è possibile acquisire gli snapshot locali dei volumi aggiunti in locale. Tuttavia, è consigliabile che hello è regolarmente eseguire il backup dei volumi aggiunti in locale con tooensure gli snapshot cloud che la protezione dei dati nell'eventualità di una situazione di emergenza.

Si noti che gli snapshot locali di volumi aggiunti in locale possono anche livello out toohello cloud e non sono garantiti toostay al livello locale del dispositivo hello hello.

**D.** Esistono linee guida per la gestione degli snapshot locali per i volumi aggiunti in locale?

**R.** Snapshot locali frequenti insieme a una frequenza elevata di dati varianza hello localmente volume aggiunto potrebbe causare hello dispositivo toobe rapido esaurimento dello spazio locale e dati dai volumi a livelli vengano applicati toohello cloud. Si consiglia pertanto che ridurre al minimo il numero di hello di snapshot locali.

**D.** È stato ricevuto un avviso che informa che gli snapshot locali dei volumi aggiunti in locale potrebbero essere invalidati. Quando può accadere?

**R.** Snapshot locali frequenti insieme a una frequenza elevata di dati varianza hello localmente volume aggiunto potrebbe portare lo spazio locale nel toobe dispositivo hello consumati velocemente. Se vengono utilizzati i livelli locale hello del dispositivo hello, potrebbe comportare un'interruzione del servizio cloud estesa dispositivo hello esaurisca e volume toohello di scritture in arrivo potrebbe comportare l'invalidamento di snapshot hello (come tooupdate hello snapshot toorefer è presente alcuno spazio toohello precedenti blocchi di dati che sono stati sovrascritti). In tali hello una situazione scritture toohello volume continuerà toobe servite, ma gli snapshot locali hello potrebbero non essere validi. Non vi è alcun impatto tooyour cloud gli snapshot esistenti.

avviso di Hello è toonotify è che tale situazione può verificarsi e verificare che indirizzo hello stesso in modo tempestivo entrambi esaminando gli snapshot locali pianifica tootake meno snapshot locali frequenti o l'eliminazione snapshot locali meno recenti che non sono più Obbligatorio.

Se gli snapshot locali hello vengono invalidati, si riceverà un avviso informativo del tipo di notifica che sono stati invalidati gli snapshot locali hello per il criterio di backup specifico di hello insieme elenco hello del timestamp degli snapshot locali hello che sono stati invalidati. Questi snapshot verrà eliminato automaticamente e non sarà in grado di tooview nel hello **cataloghi di Backup** pannello in hello portale di Azure.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Domande sulla conversione di un volume aggiunto in locale tooa volume a livelli
**D.** È osservare alcuni lentezza nel dispositivo hello durante la conversione di un volume aggiunto in locale tooa volume a livelli. Perché accade?

**R.** il processo di conversione Hello prevede due passaggi:

1. Provisioning di spazio sul dispositivo hello per hello, volume appena-a--convertire aggiunto in locale.
2. Download di tutti i dati a più livelli da hello cloud tooensure locale garantisce.

Entrambi questi passaggi sono lunghi in esecuzione di operazioni che dipendono dalla dimensione hello del volume hello convertito, dati sul dispositivo hello e larghezza di banda disponibile. Poiché alcuni dati dai volumi a livelli esistenti potrebbero spill toohello cloud come parte del processo di provisioning hello, il dispositivo potrebbe riscontrare una riduzione delle prestazioni durante l'operazione. Inoltre, il processo di conversione hello può risultare più lento se:

* I volumi esistenti non sottoposti a backup toohello cloud. pertanto è consigliabile che il tooinitiating precedenti una conversione di volumi di backup.
* Sono stati applicati i criteri di limitazione della larghezza di banda, che potrebbero vincolare cloud toohello di hello larghezza di banda disponibile. è pertanto consigliabile che acquisire una 40 Mbps dedicato o più cloud toohello di connessione.
* il processo di conversione Hello può richiedere diverse ore a causa di fattori più toohello illustrati in precedenza; Pertanto, è consigliabile eseguire questa operazione durante i periodi di non picchi o tooavoid un fine settimana hello impatto su utenti finali.

Ulteriori informazioni su come troppo[convertire un volume aggiunto in locale tooa volume a livelli](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)

**D.** È possibile annullare l'operazione di conversione volume hello?

**R.** No, è possibile hello operazione di annullamento conversione hello una volta avviata. Come descritto nella domanda precedente hello, prestare attenzione hello potenziali problemi di prestazioni che si verificano durante il processo di hello e seguire le procedure consigliate hello elencate sopra, quando si pianifica la conversione.

**D.** Volume toomy cosa accade se si verifica un errore di operazione di conversione hello?

**R.** Conversione del volume può non riuscire a causa di problemi di connettività toocloud. dispositivo Hello può infine arrestare il processo di conversione hello dopo una serie di tentativi non riusciti toobring dati a più livelli di cloud hello. In questo caso, il tipo di volume hello continuerà toobe hello origine volume tipo precedente tooconversion, e:

* Un avviso critico sarà generato toonotify di errore di conversione del volume hello. Ulteriori informazioni su [gli avvisi di volumi correlati toolocally bloccato](storsimple-8000-manage-alerts.md#locally-pinned-volume-alerts)
* Se si esegue la conversione di un volume a livelli tooa aggiunto in locale, volume hello continuerà tooexhibit proprietà di un volume a livelli come dati potrebbero comunque a risiedere nel cloud hello. Si consiglia risolvere i problemi di connettività hello e quindi ripetere l'operazione di conversione hello.
* Analogamente, quando la conversione da un tooa aggiunto in locale a livelli ha esito negativo di volume, anche se il volume di hello verrà contrassegnato come volume aggiunto in locale, funzionerà come un volume a livelli (poiché dati potrebbero avere distribuito toohello cloud). Tuttavia, continueranno spazio toooccupy nei livelli di hello locale del dispositivo hello. Questo spazio non sarà disponibile per gli altri volumi aggiunti in locale. È consigliabile che si riprova tooensure questa operazione hello locale nel dispositivo hello è espressamente che la conversione del volume hello sia completezza.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Domande sul ripristino di un volume aggiunto in locale
**D.** I volumi aggiunti in locale vengono ripristinati immediatamente?

**R.** Sì, i volumi aggiunti in locale vengono ripristinati immediatamente. Non appena le informazioni dei metadati hello hello volume viene effettuato il pull dal cloud hello come parte dell'operazione di ripristino hello, volume hello viene portato in linea e accessibile dall'host hello. Tuttavia, le garanzie locale per il volume di hello dati non sarà presenti fino a quando tutti i dati di hello è stato scaricato dal cloud hello e che si verifichi una riduzione delle prestazioni su tali volumi per durata hello del ripristino di hello.

**D.** Quanto tempo occorre toorestore un volume aggiunto in locale?

**R.** I volumi aggiunti in locale vengono ripristinati immediatamente e portati online come metadati informazioni sul volume di hello viene recuperati dal cloud hello, mentre i dati di volume hello continuano toobe scaricato in background di hello. Questa seconda parte dell'operazione di ripristino hello - ottenere per i dati di volume hello - garanzie locale hello è un'operazione a esecuzione prolungata e potrebbe richiedere alcune ore per tutti i toobe dati hello reso locale. Hello scattato toocomplete hello stesso dipende da vari fattori, ad esempio dimensioni hello del volume di hello in fase di ripristino e hello larghezza di banda disponibile. Se è stato eliminato volume originale hello da ripristinare, ulteriore tempo accederà toocreate hello locale spazio sul hello dispositivo come parte dell'operazione di ripristino hello.

**D.** È necessario toorestore locale del proprio account bloccato snapshot meno recente tooan del volume (eseguito quando è stata a livelli a volume hello). Volume hello verrà ripristinato come livelli in questo caso?

**R.** No, verrà ripristinato il volume di hello come volume aggiunto in locale. Sebbene hello snapshot ora toohello date quando volume hello stato a più livelli, durante il ripristino di volumi esistenti, StorSimple utilizza sempre il tipo di hello del volume su disco hello attualmente esistente.

**D.** Esteso il volume aggiunto in locale di recente, ma è ora necessario toorestore hello dati tooa ora volume hello dimensioni minori. Verrà ripristino ridimensionare il volume corrente hello e sarà necessario dimensioni hello tooextend del volume hello una volta completato il ripristino di hello?

**R.** Sì, ripristino hello verrà ridimensionare il volume di hello e sarà necessario dimensioni hello tooextend del volume hello dopo il completamento del ripristino hello.

**D.** È possibile modificare il tipo di hello di un volume durante il ripristino?

**R.**No, non è possibile modificare il tipo di volume hello durante il ripristino.

* Volumi che sono stati eliminati vengono ripristinati come tipo hello archiviato nello snapshot hello.
* I volumi esistenti vengono ripristinati in base al tipo corrente, indipendentemente dal tipo di hello archiviato nello snapshot hello (vedere domande toohello due precedenti).

**D.** È necessario toorestore il volume aggiunto in locale, ma si è scelto un punto corretto nello snapshot di tempo. È possibile annullare l'operazione di ripristino corrente hello?

**R.** Sì, è possibile annullare un'operazione di ripristino in corso. lo stato di Hello del volume hello verrà rollback toohello stato all'avvio di hello del ripristino hello. Tuttavia, le scritture eseguite toohello volume durante il ripristino di hello andranno persi.

**D.** È stata avviata un'azione di ripristino su uno dei volumi aggiunti in locale e ora viene visualizzato uno snapshot nel catalogo backlog che non si ricorda di avere creato. A che cosa serve?

**R.** Si tratta di snapshot temporanei hello viene creato l'operazione di ripristino toohello precedente e viene usato per eseguire il rollback in caso di ripristino hello è stato annullato o ha esito negativo. Non eliminare questo snapshot. verrà automaticamente eliminato una volta completato il ripristino di hello. Questo comportamento può verificarsi se il processo di ripristino dispone solo di volumi associati in locale o di una combinazione di volumi associati in locale e a livelli. Se il processo di ripristino hello include solo i volumi a livelli, questo comportamento non verrà eseguita.

**D.** È possibile clonare un volume aggiunto in locale?

**R.** Sì, Tuttavia, verrà clonate come un volume a livelli volume hello aggiunto in locale per impostazione predefinita. Ulteriori informazioni su come troppo[clonare un volume aggiunto in locale](storsimple-8000-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Domande sul failover di un volume aggiunto in locale
**D.** È necessario toofail sul dispositivo fisico tooanother dispositivo. Dei volumi aggiunti in locale verrà effettuato il failover come volumi aggiunti in locale o a livelli?

**R.** volumi Hello aggiunto in locale vengono eseguiti il failover nel sistema locale è bloccato se il dispositivo di destinazione hello è in esecuzione aggiornamento serie StorSimple 8000 3 o versione successiva.

Sono disponibili altre informazioni sugli [failover e ripristino di emergenza dei volumi aggiunti in locale nelle diverse versioni](storsimple-8000-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**D.** I volumi aggiunti in locale vengono ripristinati immediatamente durante il ripristino di emergenza?

**R.** Sì, i volumi aggiunti in locale vengono ripristinati immediatamente durante il failover. Non appena le informazioni dei metadati hello hello volume viene effettuato il pull dal cloud hello come parte dell'operazione di failover di hello, volume hello viene portata online nel dispositivo di destinazione hello e sono accessibili dall'host hello. Nel frattempo, dati di volume hello continuerà in background hello toodownload e si verifichi una riduzione delle prestazioni su tali volumi per la durata di hello di hello failover.

**D.** Viene visualizzato il processo di failover hello completato, come è possibile tenere traccia del corso hello del volume aggiunto in locale che viene ripristinato nel dispositivo di destinazione hello?

**R.** Durante un'operazione di failover, il processo di failover di hello viene contrassegnato come completato dopo che tutti i volumi di hello in set di failover hello sono stati ripristinati e portati online nel dispositivo di destinazione hello immediatamente. Sono inclusi i volumi aggiunti in locale che è stati eseguiti. Tuttavia, le garanzie locale dei dati hello sarà disponibile solo quando tutti i dati per il volume di hello hello è stato scaricato. È possibile monitorare lo stato di avanzamento per ciascun volume aggiunto in locale che è stato eseguito da monitoraggio dei processi di ripristino corrispondente hello che vengono creati come parte del failover hello. Questi singoli processi di ripristino verranno creati solo per i volumi aggiunti in locale.

**D.** È possibile modificare il tipo di hello di un volume durante il failover?

**R.** No, non è possibile modificare il tipo di volume hello durante un failover. Se hanno esito negativo su tooanother un dispositivo fisico che esegue StorSimple serie 8000 aggiornamento 3, volumi hello vengono eseguiti il failover in base al tipo di volume hello archiviato nello snapshot hello.

**D.** È possibile failover un contenitore di volumi con appliance di cloud toohello volumi aggiunti in locale?

**R.** Sì, volumi Hello aggiunto in locale verranno eseguiti il failover come volumi a livelli. Sono disponibili altre informazioni sugli [failover e ripristino di emergenza dei volumi aggiunti in locale nelle diverse versioni](storsimple-8000-device-failover-disaster-recovery.md#common-considerations-for-device-failover)

