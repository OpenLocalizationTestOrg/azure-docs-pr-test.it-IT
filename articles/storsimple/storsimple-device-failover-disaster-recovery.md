---
title: ripristino di emergenza e failover aaaStorSimple | Documenti Microsoft
description: Informazioni su come toofail il tooitself dispositivo StorSimple, un altro dispositivo fisico o un dispositivo virtuale.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Failover e ripristino di emergenza per il dispositivo StorSimple
## <a name="overview"></a>Panoramica
Questa esercitazione descrive hello passaggi necessari toofail su un dispositivo StorSimple nell'evento hello un'emergenza. Un failover consentirà toomigrate i dati da un dispositivo di origine in hello datacenter tooanother fisico o in un dispositivo virtuale si trovano in hello stesso o in una posizione geografica diversa. 

Ripristino di emergenza (ripristino di emergenza) viene gestito tramite funzionalità di failover di hello dispositivo e può essere avviato da hello **dispositivi** pagina. Questa pagina raccoglie servizio tutti hello StorSimple dispositivi connessi tooyour StorSimple Manager. Per ogni dispositivo, nome descrittivo hello, stato, capacità disponibile e massima, tipo e il modello vengono visualizzati.

![Pagina Dispositivi](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

linee guida di Hello in questa esercitazione si applicano dispositivi fisici e virtuali tooStorSimple tra tutte le versioni di software.

## <a name="disaster-recovery-dr-and-device-failover"></a>Ripristino di emergenza (DR) e failover del dispositivo
In uno scenario di ripristino di emergenza di emergenza nel dispositivo primario hello smette di funzionare. In questo caso, è possibile spostare i dati di cloud hello associati hello tooanother dispositivo utilizzando il dispositivo primario hello come hello *origine* e specificando un altro dispositivo come hello *destinazione*. È possibile selezionare uno o più volumi contenitori toomigrate toohello dispositivo di destinazione. Questo processo è noto tooas hello *failover*. 

Durante il failover hello, i contenitori di volumi hello hello dispositivo di origine modificare la proprietà e sono trasferiti toohello dispositivo di destinazione. Una volta contenitori dei volumi hello modificare la proprietà, questi vengono eliminati dal dispositivo di origine hello. Una volta completata l'eliminazione di hello, il dispositivo di destinazione hello quindi può essere eseguito nuovamente.

In genere dopo un ripristino di emergenza, il backup più recente di hello è dispositivo di destinazione toohello dati hello toorestore utilizzato. Tuttavia, se sono presenti più criteri di backup per hello stesso volume, quindi verrà prelevato criteri di backup hello con numero più grande di hello di volumi e backup più recente di hello da quei criteri toorestore utilizzati hello dati nel dispositivo di destinazione hello.

Ad esempio, se sono presenti due criteri di backup (un valore predefinito e uno personalizzato) *defaultPol*, *customPol* con hello seguenti dettagli:

* *defaultPol*: un solo volume, *vol1*, con esecuzione giornaliera a partire dalle 22:30.
* *customPol*: quattro volumi, *vol1*, *vol2*, *vol3* e *vol4*, con esecuzione giornaliera a partire dalle 22:00.

In questo caso verrà usato *criterioPersonalizzato* perché include più volumi e viene data priorità alla coerenza per arresto anomalo del sistema. backup più recente di Hello da questi criteri viene utilizzato toorestore dati.

## <a name="considerations-for-device-failover"></a>Considerazioni per il failover del dispositivo
In caso di hello un'emergenza, è possibile scegliere toofail failover del dispositivo StorSimple:

* dispositivo fisico tooa 
* tooitself
* dispositivo virtuale tooa

Per un failover del dispositivo, tenere in seguito hello presente:

* Hello prerequisiti per ripristino di emergenza prevedono che tutti i volumi di hello all'interno di contenitori di volumi hello siano offline e contenitori di volumi hello sono associato un snapshot nel cloud. 
* dispositivi di destinazione disponibili Hello per il ripristino di emergenza sono dispositivi che dispongono di sufficiente spazio tooaccommodate hello contenitori del volume selezionati. 
* servizio Hello i dispositivi che sono connessi tooyour ma non soddisfano i criteri hello di sufficiente spazio non saranno disponibile come dispositivi di destinazione.
* Dopo un ripristino di emergenza, per una durata limitata, può influire sulle prestazioni di accesso ai dati hello in modo significativo, come dispositivo hello sarà anche necessario tooaccess hello dati dal cloud hello e archiviate in locale.

#### <a name="device-failover-across-software-versions"></a>Failover del dispositivo in tutte le versioni del software
Un servizio StorSimple Manager in una distribuzione potrebbe avere più dispositivi, fisici e virtuali, che eseguono diverse versioni del software. Seconda versione del software hello, tipi di volumi hello nei dispositivi hello anche siano diversi. Ad esempio, un dispositivo che esegue l’Aggiornamento 2 o versione successiva avrebbe volumi aggiunti in locale e a livelli (con archiviazione in un sottoinsieme a livelli). Un dispositivo pre-aggiornamento 2 in hello invece può avere a più livelli e dei volumi di archiviazione. 

Utilizzare hello seguente toodetermine tabella se è possibile eseguire il failover tooanother dispositivo in esecuzione un comportamento di versione e hello software diversi tipi di volume durante il ripristino di emergenza.

| Failover da | Consentito per il dispositivo fisico | Consentito per il dispositivo virtuale |
| --- | --- | --- |
| Update 2. toopre-Update 1 (versione 0,1, 0,2, 0,3) |No |No |
| Aggiornamento 2 tooUpdate 1 (1, 1.1, 1.2) |Sì <br></br>Se utilizza localmente bloccato o a livelli di volumi o una combinazione di due, hello volumi vengono sempre eseguiti il failover come tipo a livelli. |Sì<br></br>se utilizza volumi aggiunti in locale, il failover viene eseguito come volume a livelli. |
| Aggiornamento 2 tooUpdate 2 (o versione successiva) |Sì<br></br>In volumi localmente bloccati o a più livelli o una combinazione di due volumi hello vengono sempre eseguiti il failover come hello; tipo di volume di avvio a livelli a più livelli e aggiunti in locale nel sistema locale è bloccato. |Sì<br></br>se utilizza volumi aggiunti in locale, il failover viene eseguito come volume a livelli. |

#### <a name="partial-failover-across-software-versions"></a>Failover parziale in tutte le versioni del software
Seguire queste linee guida se si intende tooperform un failover parziale usando un dispositivo di origine di StorSimple che esegue destinazione 1 tooa pre-aggiornamento esecuzione di Update 1 o versione successiva. 

| Origine del failover parziale | Consentito per il dispositivo fisico | Consentito per il dispositivo virtuale |
| --- | --- | --- |
| Pre-aggiornamento 1 (versione 0,1, 0,2, 0,3) tooUpdate 1 o versione successiva |Per il suggerimento prassi migliori di hello Sì, vedere di seguito. |Per il suggerimento prassi migliori di hello Sì, vedere di seguito. |

> [!TIP]
> In Aggiornamento 1 e versioni successive è stata eseguita una modifica ai metadati del cloud e al formato dati. Di conseguenza, non è consigliabile un failover parziale da pre-aggiornamento 1 tooUpdate 1 o versioni successive. Se è necessario un failover parziale tooperform, è consigliabile che è applicare prima l'Update 1 o versioni successive in entrambi i dispositivi hello (origine e destinazione) e quindi procedere con il failover hello. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Eseguire il failover al dispositivo fisico tooanother
Eseguire hello seguendo i passaggi toorestore il dispositivo di destinazione di tooa dispositivo fisico.

1. Verificare il contenitore del volume hello desiderato toofail siano associati snapshot nel cloud.
2. In hello **dispositivi** pagina, fare clic su hello **contenitori di volumi** scheda.
3. Selezionare un contenitore di volumi di cui si desidera toofail su tooanother dispositivo. Fare clic su elenco hello toodisplay hello volumi contenitore di volumi all'interno del contenitore. Selezionare un volume e fare clic su **non in linea** tootake offline volume hello. Ripetere questo processo per tutti i volumi di hello hello contenitore del volume.
4. Passaggio di ripetizione hello precedente per tutti i contenitori dei volumi di hello desideri toofail su tooanother dispositivo.
5. In hello **dispositivi** pagina, fare clic su **Failover**.
6. Nella procedura guidata hello visualizzata nell'area **scegliere toofail contenitore volume su**:
   
   1. Nell'elenco di hello dei contenitori di volumi, selezionare i contenitori di volumi hello desiderato toofail su.
      **Hello solo contenitori di volumi con snapshot cloud associati e i volumi offline sono visualizzati.**
   2. In **scegliere un dispositivo di destinazione** per volumi di hello nei contenitori hello selezionato, selezionare un dispositivo di destinazione dall'elenco a discesa hello dei dispositivi disponibili. Nell'elenco a discesa hello vengono visualizzati solo i dispositivi di hello con capacità disponibile hello.
   3. Esaminare infine tutte le impostazioni di failover hello in **confermare il failover**. Fare clic sull'icona di controllo hello ![icona controllo](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Viene creato un processo di failover che possono essere monitorati tramite hello **processi** pagina. Se il contenitore del volume hello che è stato eseguito il failover con volumi locali, si noterà i processi di ripristino di singole per ogni volume locale (non per i volumi a livelli) nel contenitore hello. I processi di ripristino potrebbe richiedere toocomplete un certo tempo. È probabile che il processo di failover hello può essere completata in precedenza. Si noti che questi volumi avrà garanzie locale solo dopo il completamento dei processi di ripristino hello. Dopo aver completato il failover hello, visitare toohello **dispositivi** pagina.                                            
   
   1. Selezionare il dispositivo hello che è stato usato come dispositivo di destinazione hello per il processo di failover di hello.
   2. Passare toohello **contenitori di volumi** pagina. Tutti i contenitori di volumi di hello, insieme ai volumi hello dispositivo precedente hello, dovrebbero essere elencati.

## <a name="failover-using-a-single-device"></a>Failover con un solo dispositivo
Eseguire hello procedura seguente se si dispone di un singolo tooperform dispositivo ed è necessario un failover.

1. Creare snapshot cloud di tutti i volumi di hello nel dispositivo.
2. Reimpostare le impostazioni predefinite del dispositivo toofactory. Seguire hello dettagliate in [come impostazioni predefinite tooreset un toofactory dispositivo StorSimple](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Configurare il dispositivo e registrarlo nuovamente con il servizio StorSimple Manager.
4. In hello **dispositivi** pagina, dovrebbe risultare dispositivo precedente hello **Offline**. Hello dispositivo appena registrato dovrebbe risultare **Online**.
5. Prima di nuovo dispositivo hello, completa la configurazione minima di hello del dispositivo di hello. 
   
   > [!IMPORTANT]
   > **Se la configurazione minima di hello non viene completata prima di tutto, il ripristino di emergenza avrà esito negativo a causa di un bug nell'implementazione corrente di hello. Questo problema verrà risolto in una versione successiva.**
   > 
   > 
6. Selezionare il dispositivo precedente hello (stato non in linea) e fare clic su **Failover**. Nella procedura guidata hello presentato, il failover il dispositivo e specificare il dispositivo di destinazione hello come dispositivo appena registrato hello. Per istruzioni dettagliate, vedere troppo[failover dispositivo fisico tooanother](#fail-over-to-another-physical-device).
7. Verrà creato un processo di ripristino del dispositivo che è possibile monitorare da hello **processi** pagina.
8. Al termine il processo di hello, accedere di nuovo dispositivo hello e passare toohello **contenitori di volumi** pagina. Tutti i contenitori di volumi di hello dispositivo precedente hello dovrebbero ora essere migrati toohello nuovo dispositivo.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Dispositivo virtuale StorSimple tooa il failover
È necessario disporre di un StorSimple dispositivo virtuale creato e configurato toorunning precedenti in questa procedura. Se in esecuzione Update 2, considerare l'utilizzo di un dispositivo virtuale 8020 per hello ripristino di emergenza che dispone di 64 TB e utilizza l'archiviazione Premium. 

Eseguire hello seguendo i passaggi toorestore hello dispositivo tooa destinazione dispositivo virtuale StorSimple.

1. Verificare il contenitore del volume hello desiderato toofail siano associati snapshot nel cloud.
2. In hello **dispositivi** pagina, fare clic su hello **contenitori di volumi** scheda.
3. Selezionare un contenitore di volumi di cui si desidera toofail su tooanother dispositivo. Fare clic su elenco hello toodisplay hello volumi contenitore di volumi all'interno del contenitore. Selezionare un volume e fare clic su **non in linea** tootake offline volume hello. Ripetere questo processo per tutti i volumi di hello hello contenitore del volume.
4. Passaggio di ripetizione hello precedente per tutti i contenitori dei volumi di hello desideri toofail su tooanother dispositivo.
5. In hello **dispositivi** pagina, fare clic su **Failover**.
6. Nella procedura guidata hello visualizzata nell'area **scegliere toofailover contenitore volume**, completare hello seguente:
   
    a. Nell'elenco di hello dei contenitori di volumi, selezionare i contenitori di volumi hello desiderato toofail su.
   
    **Hello solo contenitori di volumi con snapshot cloud associati e i volumi offline sono visualizzati.**
   
    b. In **scegliere un dispositivo di destinazione per hello volumi nei contenitori selezionato hello**, selezionare hello dispositivo virtuale StorSimple dall'elenco a discesa hello dei dispositivi disponibili. **Nell'elenco a discesa hello vengono visualizzati solo i dispositivi di hello che dispongano di capacità sufficiente.**  
7. Esaminare infine tutte le impostazioni di failover hello in **confermare il failover**. Fare clic sull'icona di controllo hello ![icona controllo](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Dopo aver completato il failover hello, visitare toohello **dispositivi** pagina.
   
    a. Selezionare hello dispositivo virtuale StorSimple che è stato usato come dispositivo di destinazione hello per il processo di failover di hello.
   
    b. Passare toohello **contenitori di volumi** pagina. Tutti i contenitori di volumi di hello, insieme ai volumi hello dispositivo precedente hello dovrebbero ora essere elencati.

![Video disponibile](./media/storsimple-device-failover-disaster-recovery/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra come ripristinare una periferica virtuale tooa di dispositivo fisico nel cloud hello, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Failback
Nell'aggiornamento 3 e versioni successive, StorSimple supporta anche il failback. Al termine del failover hello, hello seguenti azioni:

* contenitori di volumi Hello che è stati eseguiti il failover vengono rimossi dal dispositivo di origine hello.
* Un processo in background per ogni contenitore del volume (failover) viene avviato sul dispositivo di origine hello. Se si tenta di toofailback mentre è in corso il processo di hello, si riceverà un effetto toothat di notifica. Sarà necessario toowait fino al processo hello failback hello toostart completo. 
  
    Hello ora toocomplete hello l'eliminazione di contenitori del volume dipende da vari fattori, ad esempio quantità di dati, l'età di dati hello, numero di backup e hello larghezza di banda disponibile per l'operazione di hello. Se si prevede di effettuare failover/failback di test, si consiglia di testare i contenitori dei volumi con meno dati (GB). Nella maggior parte dei casi, è possibile avviare il failback hello 24 ore dopo il failover hello è stato completato. 

## <a name="frequently-asked-questions"></a>Domande frequenti
D: **Cosa accade se hello ripristino di emergenza non riesce o ha esito positivo parziale?**

R. Se ha esito negativo hello ripristino di emergenza, è consigliabile provare nuovamente. Hello seconda volta, ripristino di emergenza sappia quali tutti sono state eseguite e quando il processo di hello bloccato hello prima volta. il processo di ripristino di emergenza Hello avvia da quel punto in poi. 

D: **È possibile eliminare un dispositivo durante l'esecuzione di failover del dispositivo hello?**

R. Non è possibile eliminare un dispositivo durante un ripristino di emergenza. Al termine hello ripristino di emergenza, è possibile eliminare solo il dispositivo.

D:    **Quando di garbage collection hello viene avviata nel dispositivo di origine hello in modo che i dati locali di hello sul dispositivo di origine verranno eliminati?**

R. Garbage collection verrà abilitata nel dispositivo di origine hello solo dopo che è completamente eliminata dispositivo hello. pulizia Hello include pulitura degli oggetti che hanno eseguito il failover hello dispositivo di origine, ad esempio volumi, oggetti backup (non di dati), i contenitori dei volumi e criteri.

D: **Cosa accade se hello Elimina processo associato a contenitori del volume nel dispositivo di origine hello hello ha esito negativo?**

R.  Se hello Elimina ha esito negativo processo, è necessario l'eliminazione di hello trigger toomanually hello dei contenitori di volumi. In hello **dispositivi** pagina, selezionare il dispositivo di origine e fare clic su **contenitori di volumi**. Contenitori di volumi selezionare hello che è stato eseguito il failover e in basso hello hello pagina, fare clic su **eliminare**. Dopo avere eliminato hello tutti i contenitori di volumi nel dispositivo di origine hello il failover, è possibile avviare il failback hello.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Ripristino di emergenza di continuità aziendale (BCDR)
Uno scenario di ripristino di emergenza la continuità aziendale si verifica quando hello intero Data Center di Azure smette di funzionare. Ciò può influire sul servizio StorSimple Manager e hello associati dispositivi StorSimple.

Se sono presenti dispositivi StorSimple registrati prima che si è verificato un problema grave, questi dispositivi StorSimple potrebbe essere necessario reimposta una factory tooundergo. Dopo l'emergenza hello, il dispositivo di StorSimple hello verrà visualizzato come offline. dispositivo StorSimple Hello deve essere eliminato dal portale hello e, è necessario eseguire un ripristino delle impostazioni predefinite, seguito da una nuova registrazione.

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).
* Per informazioni su come toouse hello StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

