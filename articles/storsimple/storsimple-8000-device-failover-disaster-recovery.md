---
title: failover aaaStorSimple, il ripristino di emergenza per i dispositivi 8000 serie | Documenti Microsoft
description: Informazioni su come toofail il tooitself dispositivo StorSimple, un altro dispositivo fisico o un'applicazione cloud.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Failover e ripristino di emergenza per dispositivi StorSimple serie 8000

## <a name="overview"></a>Panoramica

Questo articolo descrive hello dispositivo funzionalità di failover per i dispositivi della serie StorSimple 8000 hello e come questa funzionalità può essere dispositivi StorSimple toorecover utilizzata se si verifica un'emergenza. StorSimple Usa dati toomigrate hello failover del dispositivo da un dispositivo di origine nel dispositivo di destinazione tooanother hello Data Center. linee guida di Hello in questo articolo si applicano dispositivi fisici serie di tooStorSimple 8000 e Appliance di cloud con le versioni di software Update 3 e successive.

StorSimple Usa hello **dispositivi** pannello toostart hello dispositivo funzionalità di failover in caso di hello un'emergenza. Questo pannello sono elencati tutti hello StorSimple dispositivi connessi tooyour dispositivo StorSimple Manager servizio.

![Pannello Dispositivi](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Ripristino di emergenza (DR) e failover del dispositivo

In uno scenario di ripristino di emergenza di emergenza nel dispositivo primario hello smette di funzionare. StorSimple Usa nel dispositivo primario hello come _origine_ e sposta hello associata cloud dati tooanother _destinazione_ dispositivo. Questo processo è noto tooas hello *failover*. Hello seguente immagine illustra il processo di hello di failover.

![Che cosa avviene nel failover del dispositivo?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

dispositivo di destinazione Hello per un failover potrebbe essere un dispositivo fisico o anche un'applicazione cloud. Hello dispositivo di destinazione può essere situato in hello stesso o in una posizione geografica diversa rispetto al dispositivo di origine hello.

Durante il failover hello, è possibile selezionare i contenitori dei volumi per la migrazione. StorSimple passa quindi la proprietà hello di questi contenitori di volumi da hello origine dispositivo toohello dispositivo di destinazione. Una volta contenitori dei volumi hello modificare la proprietà, questi contenitori StorSimple Elimina hello dispositivo di origine. Una volta completata l'eliminazione di hello, è possibile eseguire il dispositivo di destinazione hello indietro. _Il failback_ trasferimenti hello dispositivo di origine originale toohello indietro di proprietà.

### <a name="cloud-snapshot-used-during-device-failover"></a>Snapshot cloud usato durante il failover del dispositivo

Dopo un ripristino di emergenza, backup più recente nel cloud hello è dispositivo di destinazione toohello dati hello toorestore utilizzato. Per ulteriori informazioni su snapshot nel cloud, vedere [utilizzare tootake servizio di gestione di dispositivi StorSimple hello un backup manuale](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

In una serie StorSimple 8000, i criteri di backup sono associati ai backup. Se sono presenti più criteri di backup per hello stesso volume, quindi seleziona StorSimple hello criteri di backup con numero più grande di hello di volumi. StorSimple Usa quindi i backup più recente di hello dai dati hello toorestore di hello selezionata dei criteri di backup nel dispositivo di destinazione hello.

Si supponga che siano disponibili due criteri di backup, *defaultPol* e *customPol*:

* *defaultPol*: un solo volume, *vol1*, con esecuzione giornaliera a partire dalle 22:30.
* *customPol*: quattro volumi, *vol1*, *vol2*, *vol3* e *vol4*, con esecuzione giornaliera a partire dalle 22:00.

In questo caso StorSimple darà priorità alla coerenza per arresto anomalo del sistema e userà *customPol* perché include più volumi. backup più recente di Hello da questi criteri viene utilizzato toorestore dati. Per ulteriori informazioni su come toocreate e gestire criteri di backup, andare troppo[utilizzare criteri toomanage del servizio gestione di dispositivi StorSimple hello backup](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Considerazioni comuni per il failover del dispositivo

Prima di failover su un dispositivo, è possibile esaminare hello le seguenti informazioni:

* Prima di avviare un failover del dispositivo, tutti i volumi di hello all'interno di contenitori di volumi hello devono essere offline. In un failover non pianificato, i volumi StotSimple passeranno automaticamente alla modalità offline. Tuttavia, se si esegue un failover pianificato (ripristino di emergenza tootest), è necessario eseguire tutti i volumi di hello offline.
* Hello solo contenitori di volumi che sono associato un snapshot cloud sono elencati per ripristino di emergenza. Deve essere presente almeno un contenitore di volumi con una data di toorecover snapshot cloud associato.
* Se sono presenti snapshot cloud che si estendono su più contenitori di volumi, StorSimple esegue il failover di questi contenitori di volumi come set. In un'istanza rara, se sono presenti gli snapshot locali che si estendono su più contenitori del volume, ma non snapshot cloud associati, StorSimple failover gli snapshot locali hello e dati locali hello vanno persi dopo il ripristino di emergenza.
* dispositivi di destinazione disponibili Hello per il ripristino di emergenza sono dispositivi che dispongono di sufficiente spazio tooaccommodate hello contenitori del volume selezionati. I dispositivi che non dispongono di spazio sufficiente non sono elencati come dispositivi di destinazione.
* Dopo un ripristino di emergenza (per un periodo limitato), può influire sulle prestazioni di accesso ai dati hello in modo significativo, come dispositivo hello deve tooaccess hello dati dal cloud hello e archiviate in locale.

#### <a name="device-failover-across-software-versions"></a>Failover del dispositivo in tutte le versioni del software

Un servizio Gestione dispositivi di StorSimple in una distribuzione potrebbe avere più dispositivi, fisici e cloud, che eseguono diverse versioni del software.

Utilizzare hello seguente toodetermine tabella se è possibile eseguire il failover o non riuscire tooanother indietro dispositivi che eseguono una versione diversa del software e il comportano di tipi di volumi hello durante il ripristino di emergenza.

#### <a name="failover-and-failback-across-software-versions"></a>Failover e failback del dispositivo in tutte le versioni del software

| Effettuare il failover/failback da | Dispositivo fisico | Appliance cloud |
| --- | --- | --- |
| TooUpdate Update 3 4 |I volumi a livelli eseguono il failover su più livelli. <br></br>I volumi aggiunti in locale eseguono il failover aggiunto in locale. <br></br> Dopo un failover, quando si crea uno snapshot nel dispositivo hello aggiornamento 4, [rilevamento basato su heatmap](storsimple-update4-release-notes.md#whats-new-in-update-4) interviene. |I volumi aggiunti in locale eseguono il failover su più livelli. |
| Update 4 tooUpdate 3 |I volumi a livelli eseguono il failover su più livelli. <br></br>I volumi aggiunti in locale eseguono il failover aggiunto in locale. <br></br> Backup utilizzato toorestore mantenere i metadati di heatmap. <br></br>Rilevamento basato su Heatmap non è disponibile in Aggiornamento 3 a seguito di un failback. |I volumi aggiunti in locale eseguono il failover su più livelli. |


## <a name="device-failover-scenarios"></a>Scenari di failover del dispositivo

Se si verifica un'emergenza, è possibile scegliere toofail failover del dispositivo StorSimple:

* [dispositivo fisico tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [dispositivo cloud tooa](storsimple-8000-device-failover-cloud-appliance.md).

Hello precedenti articoli forniscono i passaggi dettagliati per ogni hello di sopra di casi di failover.


## <a name="failback"></a>Failback

Nell'aggiornamento 3 e versioni successive, StorSimple supporta anche il failback. Il failback è semplicemente hello inversa di failover, destinazione hello diventa origine hello e hello dispositivo di origine originale durante il failover hello ora diventa il dispositivo di destinazione hello. 

Durante il failback, StorSimple Risincronizza posizione primaria di hello dati back-toohello, interrompe hello i/o e attività dell'applicazione e passa indietro toohello nel percorso originale.

Dopo un failover è stato completato, StorSimple esegue hello seguenti azioni:

* StorSimple pulisce i contenitori di volumi hello che è stati eseguiti il failover dal dispositivo di origine hello.
* StorSimple avvia un processo in background per ogni contenitore del volume (è stato eseguito) nel dispositivo di origine hello. Se si tenta di toofail mentre è in corso il processo di hello, si riceve un effetto toothat notifica. Attendere il processo di hello failback hello toostart completo.
* tempo Hello eliminazione hello toocomplete di contenitori del volume dipende da vari fattori, ad esempio quantità di dati, l'età di dati hello, numero di backup e hello larghezza di banda disponibile per l'operazione di hello.

Se si prevede di effettuare failover/failback di test, si consiglia di testare i contenitori dei volumi con meno dati (GB). In genere, è possibile avviare il failback hello 24 ore dopo il failover hello è stato completato.

## <a name="frequently-asked-questions"></a>Domande frequenti

D: **Cosa accade se hello ripristino di emergenza non riesce o ha esito positivo parziale?**

R. Se ha esito negativo hello ripristino di emergenza, è consigliabile provare nuovamente. il processo di failover Hello secondo dispositivo è a conoscenza dello stato di avanzamento hello del primo processo hello e avvia da quel punto in poi.

D: **È possibile eliminare un dispositivo durante l'esecuzione di failover del dispositivo hello?**

R. Non è possibile eliminare un dispositivo durante un ripristino di emergenza. Al termine hello ripristino di emergenza, è possibile eliminare solo il dispositivo. È possibile monitorare l'avanzamento del processo failover dispositivo hello in hello **processi** blade.

D: **Quando di garbage collection hello viene avviata nel dispositivo di origine hello in modo che i dati locali di hello sul dispositivo di origine verranno eliminati?**

R. Garbage collection è abilitata sul dispositivo di origine hello solo dopo che viene eliminata completamente dispositivo hello. pulizia Hello include pulitura degli oggetti che hanno eseguito il failover hello dispositivo di origine, ad esempio volumi, oggetti backup (non di dati), i contenitori dei volumi e criteri.

D: **Cosa accade se hello Elimina processo associato a contenitori del volume nel dispositivo di origine hello hello ha esito negativo?**

R.  Se hello Elimina ha esito negativo processo, è possibile eliminare manualmente i contenitori di volumi hello. In hello **dispositivi** pannello, selezionare il dispositivo di origine e fare clic su **contenitori di volumi**. Fare clic su contenitori di volumi selezionare hello che è stato eseguito il failover e nella parte inferiore di hello del pannello hello **eliminare**. Dopo aver eliminato hello tutti i contenitori di volumi nel dispositivo di origine hello il failover, è possibile avviare il failback hello. Per ulteriori informazioni, visitare troppo[eliminare un contenitore del volume](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>Ripristino di emergenza di continuità aziendale (BCDR)

Uno scenario di ripristino di emergenza la continuità aziendale si verifica quando hello intero Data Center di Azure smette di funzionare. Questo scenario può influenzare il servizio di gestione di dispositivi StorSimple e hello associati dispositivi StorSimple.

Se un dispositivo StorSimple registrato prima che si è verificato un problema grave, il dispositivo potrebbe essere necessario reimposta una factory tooundergo. Dopo l'emergenza hello, il dispositivo di StorSimple hello viene visualizzato nella hello portale di Azure come offline. Il dispositivo deve essere eliminato dal portale hello. Reimpostare le impostazioni predefinite toofactory hello dispositivo e ripetere la registrazione con il servizio di hello.

## <a name="next-steps"></a>Passaggi successivi

Se si è pronti tooperform un failover del dispositivo, scegliere uno dei seguenti scenari per istruzioni dettagliate hello:

- [Eseguire il failover al dispositivo fisico tooanother](storsimple-8000-device-failover-physical-device.md)
- [Eseguire il failover toohello stesso dispositivo](storsimple-8000-device-failover-same-device.md)
- [Eseguire il failover tooStorSimple Appliance di Cloud](storsimple-8000-device-failover-cloud-appliance.md)

Se non è riuscita sul dispositivo, scegliere una di hello le opzioni seguenti:

* [Disattivare o eliminare un dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* [Utilizzare il dispositivo StorSimple di tooadminister servizio di gestione di dispositivi StorSimple hello](storsimple-8000-manager-service-administration.md).

