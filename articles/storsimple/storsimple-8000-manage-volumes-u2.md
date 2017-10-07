---
title: i volumi StorSimple aaaManage (Update 3) | Documenti Microsoft
description: Viene illustrato come tooadd, modificare, monitorare ed eliminare i volumi StorSimple e come tootake, non in linea se necessario.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Utilizzare i volumi hello dispositivo StorSimple Manager servizio toomanage (Update 3 o versioni successive)

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire volumi su dispositivi della serie StorSimple 8000 hello con Update 3 e successive.

servizio di gestione di dispositivi StorSimple Hello è un'estensione in hello portale di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web. Utilizzare i volumi di Azure toomanage portale hello su tutti i dispositivi. È anche possibile creare e gestire i servizi StorSimple, gestire i dispositivi, i criteri di backup e il catalogo di backup e visualizzare gli avvisi.

## <a name="volume-types"></a>Tipi di volume

I volumi di StorSimple possono essere:

* **Aggiunto in locale volumi**: dati in tali volumi rimangono nel dispositivo StorSimple locale hello in qualsiasi momento.
* **A più livelli volumi**: toohello cloud possono lo spill dei dati in tali volumi.

Un volume di archivio è un tipo di volume a livelli. Hello maggiore deduplicazione dimensioni del blocco utilizzate per i volumi di archiviazione consentono di segmenti maggiore hello dispositivo tootransfer di toohello dati nel cloud.

Se necessario, è possibile modificare il tipo di volume hello da tootiered locale o da toolocal a più livelli. Per ulteriori informazioni, visitare troppo[modificare il tipo di volume hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumi aggiunti in locale

I volumi aggiunti in locale sono completamente provisioning volumi non di livello dati nel cloud toohello, assicurando locale garantisce per dati primari, in modo indipendente di connettività cloud. I dati nei volumi aggiunti in locale non vengono deduplicati e compressi, mentre gli snapshot dei volumi aggiunti in locale vengono deduplicati. 

Poiché viene effettuato il provisioning completo dei volumi aggiunti in locale, è necessario avere spazio sufficiente nel dispositivo quando li si crea. È possibile eseguire il provisioning di volumi aggiunti in locale fino tooa la dimensione massima di 8 TB nel dispositivo StorSimple 8100 hello e 20 TB in dispositivo 8600 hello. StorSimple riserva hello locale spazio nel dispositivo hello per gli snapshot, metadati e l'elaborazione dei dati. È possibile aumentare la dimensione hello di un volume aggiunto in locale toohello spazio massimo disponibile, ma non è possibile ridurre le dimensioni di hello di un volume dopo la creazione.

Quando si crea un volume aggiunto in locale, spazio disponibile di hello per la creazione di volumi a livelli viene ridotto. Hello inversa è anche vero: se si dispone di volumi a livelli esistenti, hello spazio per la creazione di localmente pinned volumi sarà inferiore a un massimo di hello indicato in precedenza. Per ulteriori informazioni sui volumi locali, vedere toohello [domande frequenti sui volumi aggiunti in locale](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Volumi a livelli

I volumi a livelli sono volumi con thin provisioning in cui hello spesso dati di accesso rimangono locale nel dispositivo hello e meno dati utilizzate di frequente sono automaticamente a livelli toohello cloud. Thin provisioning è una tecnologia di virtualizzazione in cui archiviazione disponibili risultano tooexceed di risorse fisiche. Anziché riservare in anticipo sufficiente spazio di archiviazione, StorSimple Usa tooallocate di provisioning thin sufficiente spazio toomeet corrente. natura elastica di Hello dell'archiviazione cloud facilita questo approccio perché StorSimple può aumentare o diminuire cloud archiviazione toomeet cambiare della domanda.

Se si utilizza un volume a livelli dati di archiviazione, seleziona hello hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo toochange hello deduplicazione dimensioni del blocco per il volume too512 KB. Se non si seleziona questa opzione, il volume a livelli corrispondente hello utilizzerà una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni.


### <a name="provisioned-capacity"></a>Capacità con provisioning

Fare riferimento toohello seguente tabella per la capacità massima di provisioning per ogni tipo di dispositivo e il volume. Si noti che i volumi aggiunti in locale non sono disponibili in un dispositivo virtuale.

|  | Dimensione massima volume a livelli | Dimensione massima volume aggiunto in locale |
| --- | --- | --- |
| **Dispositivi fisici** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Dispositivi virtuali** | | |
| 8010 |30 TB |N/D |
| 8020 |64 TB |N/D |

## <a name="hello-volumes-blade"></a>Pannello volumi Hello

Hello **volumi** pannello consente volumi di archiviazione hello toomanage sono a provisioning nel dispositivo Microsoft Azure StorSimple hello per gli iniziatori (server). Visualizza elenco hello volumi hello StorSimple dispositivi connessi tooyour servizio.

 ![Pagina dei volumi](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Un volume è costituito da una serie di attributi:

* **Nome del volume** : un nome descrittivo che deve essere univoco e consente di identificare il volume di hello. Questo nome viene utilizzato anche nei rapporti di monitoraggio quando di applica un filtro su un volume specifico. Non è possibile rinominare una volta creato, hello volume.
* **Stato** : online oppure offline. Se un volume è offline, non è visibile tooinitiators (server) che è consentito l'accesso toouse hello volume.
* **Capacità** – specifica hello quantità totale di dati che possono essere archiviati dall'iniziatore hello (server). Volumi aggiunti in locale vengono effettuato il provisioning completo mentre si trovano nel dispositivo StorSimple hello. I volumi a livelli con thin provisioning e hello dati sono deduplicati. Con i volumi con thin provisioning, il dispositivo non esegue la preallocazione della capacità di archiviazione fisica internamente o nel cloud hello in tooconfigured capacità del volume di base. capacità del volume Hello viene allocata e usata su richiesta.
* **Tipo** – indica se il volume di hello è **a livelli** (hello predefinito) o **aggiunto in locale**.

Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:

* Aggiungere un volume 
* Modificare un volume 
* Modificare il tipo di volume hello
* Eliminare un volume 
* Portare un volume offline 
* Monitorare a volume 

## <a name="add-a-volume"></a>Aggiungere un volume

Il [volume è stato creato](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) durante la distribuzione del dispositivo StorSimple serie 8000. L’aggiunta di un volume è una procedura simile.

#### <a name="tooadd-a-volume"></a>tooadd un volume

1. Dall'elenco in formato tabulare hello dispositivi hello in hello **dispositivi** pannello, selezionare il dispositivo. Fare clic su **+ Aggiungi volume**.

    ![Aggiungere un nuovo volume](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. In hello **aggiungere un volume** pannello:
   
    1. Hello **seleziona dispositivo** campo viene popolato automaticamente con il dispositivo corrente.

    2. Dall'elenco a discesa hello, selezionare il contenitore di volumi hello in cui è necessario tooadd un volume.

    3.  Digitare un **Nome** per il volume. Una volta creato il volume di hello, è possibile rinominare il volume di hello.

    4. Nell'elenco a discesa hello selezionare hello **tipo** per il volume. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni più elevate, selezionare un volume **aggiunto in locale** . Per tutti gli altri dati, selezionare un volume **a livelli** . Se si usa questo volume per dati di archivio, selezionare la casella di controllo **Usare questo volume per i dati di archivio a cui si accede non di frequente**.
      
       Per un volume a livelli viene effettuato il thin provisioning e la creazione può essere rapida. Selezione **usare questo volume per i dati dell'archivio si accede di frequente** per il volume a livelli per i dati di archiviazione modifiche hello deduplicazione dimensioni del blocco per il volume di destinazione too512 KB. Se questo campo non è selezionato, volume a livelli corrispondente hello utilizza una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni.
       
       Un volume aggiunto in locale stati sottoposti a thick provisioning e garantisce che i dati primario hello sul volume hello rimangono dispositivo toohello locale e non spill toohello cloud.  Se si crea un volume aggiunto in locale, lo spazio disponibile nei livelli locale hello dei controlli dispositivo di hello volume hello tooprovision di hello dimensione richiesta. operazione Hello di creazione di un volume aggiunto in locale potrebbe comportare la distribuzione di dati esistenti dal cloud di toohello dispositivo hello e hello impiegato volume hello toocreate potrebbe richiedere tempo. tempo totale di Hello dipende dalle dimensioni hello del volume hello il provisioning, della larghezza di banda di rete disponibile e dati hello nel dispositivo.

    5. Specificare hello **capacità fornita** per il volume. Prendere nota della capacità di hello che è disponibile in base al tipo di volume hello selezionato. Hello specificato di dimensioni del volume non devono superare lo spazio disponibile hello.
      
       È possibile eseguire il provisioning di volumi aggiunti in locale fino too8.5 TB o i volumi a livelli di too200 TB sul dispositivo 8100 hello. Nel dispositivo 8600 hello più grande, è possibile eseguire il provisioning di volumi aggiunti in locale fino too22.5 TB o i volumi a livelli di too500 TB. Lo spazio locale nel dispositivo hello è hello toohost richiesto l'utilizzo di set di volumi a livelli, la creazione di volumi aggiunti in locale influisce sulle spazio hello disponibile per il provisioning dei volumi a livelli. Creando un volume aggiunto in locale, viene quindi ridotto lo spazio disponibile per la creazione di volumi a livelli. Analogamente, se viene creato un volume a livelli, lo spazio disponibile di hello per la creazione di volumi aggiunti in locale viene ridotto.
      
       Se si esegue il provisioning di un volume aggiunto in locale di 8,5 TB (dimensione massima consentita) sul dispositivo 8100, aver esaurito tutti hello lo spazio locale disponibile nel dispositivo hello. Non è possibile creare qualsiasi volume a livelli da tale punto in poi, non è disponibile spazio locale nel working set di hello dispositivo toohost hello di hello a livelli a volume. I volumi a livelli esistenti influiscono spazio hello disponibile. Ad esempio, se nel dispositivo 8100 sono già presenti volumi a livelli di circa 106 TB, saranno disponibili solo 4 TB di spazio per i volumi aggiunti in locale.

    6. In hello **connesso host** campo, fare clic sulla freccia di hello. 

        ![Host connessi](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. In hello **connesso host** pannello, scegliere un record esistente o aggiungere un nuovo record. Se si sceglie un nuovo record, quindi fornire un **nome** del record, fornire hello **iSCSI Qualified Name** (IQN) dell'host Windows. Se non si dispone di hello IQN, andare troppo[Get hello nome qualificato iSCSI di un host Windows Server](#get-the-iqn-of-a-windows-server-host). Fare clic su **Crea**. Viene creato un volume con hello specificato le impostazioni.

        ![Fare clic su Crea](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

Il nuovo volume è ora pronto toouse.

> [!NOTE]
> Se si crea un volume aggiunto in locale e quindi creare un altro localmente bloccata volume immediatamente in seguito, i processi di creazione volume hello eseguiti in sequenza. processo di creazione di Hello primo volume deve essere completata prima di iniziarne il processo di creazione volume Avanti hello.

## <a name="modify-a-volume"></a>Modificare un volume

Modificare un volume quando è necessario tooexpand o modifica gli host che accedono a volume hello hello.

> [!IMPORTANT]
> * Se si modifica la dimensione del volume hello sul dispositivo hello, dimensioni del volume hello devono toobe modificato anche l'host hello.
> * procedure sul lato host Hello descritte di seguito sono per Windows Server 2012 (versione 2012 R2). Procedure per Linux o altri sistemi operativi host saranno diverse. Vedere le istruzioni di sistema operativo host tooyour quando si modifica il volume di hello in un host in esecuzione un altro sistema operativo.

#### <a name="toomodify-a-volume"></a>toomodify un volume

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **dispositivi**. Elenco tabulare di hello di dispositivi hello, selezionare dispositivo hello con volume hello che si desidera toomodify. Fare clic su **Impostazioni > Volumi**.

    ![Andare a pannello tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. Hello tabulare elenco di volumi, selezionare il volume di hello dal menu di scelta rapida di contesto tooinvoke hello. Selezionare **portare offline** volume hello tootake si modificherà offline.

    ![Selezionare e portare offline i volumi](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. In hello **portare offline** pannello, esaminare l'impatto di hello di portare offline il volume di hello e selezionare la casella di controllo corrispondente hello. Assicurarsi che il volume corrispondente di hello nell'host di hello sia offline prima di tutto. Per informazioni su come tootake un volume offline nel server host connesso tooStorSimple, consultare toooperating istruzioni specifiche del sistema. Fare clic su **Porta offline**.

    ![Esaminare l'impatto del portare un volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Dopo che il volume di hello è offline (come indicato dallo stato del volume hello), selezionare il volume di hello e menu di scelta rapida di contesto tooinvoke hello. Selezionare **Modifica volume**.

    ![Selezionare Modifica volume](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. In hello **modifica del volume** pannello, è possibile apportare hello seguenti modifiche:
   
   1. Hello volume **nome** non può essere modificato.
   2. Convertire hello **tipo** tootiered aggiunti in locale o a più livelli toolocally bloccato (vedere [modificare il tipo di volume hello](#change-the-volume-type) per altre informazioni).
   3. Aumentare hello **capacità fornita**. Hello **capacità fornita** può solo essere aumentato. Non è possibile ridurre un volume dopo averlo creato.
   4. In **connesso host**, è possibile modificare hello ACR. toomodify un record, il volume di hello deve essere offline.

       ![Esaminare l'impatto del portare un volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Fare clic su **salvare** toosave le modifiche. Alla richiesta di conferma fare clic su **Sì**. Hello portale di Azure verrà visualizzato un messaggio di volume ad aggiornamento. Quando è stata aggiornata volume hello visualizzerà un messaggio di conferma.

    ![Esaminare l'impatto del portare un volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Se si vuole espandere un volume, completare hello nel computer host Windows come segue:
   
   1. Andare troppo**Gestione Computer** ->**Gestione disco**.
   2. Fare clic con il pulsante destro del mouse su **Gestione disco** e selezionare **Rescan Disks** (Ripeti analisi dischi).
   3. Nell'elenco di hello dei dischi, selezionare il volume hello che è stato aggiornato, pulsante destro del mouse e quindi selezionare **Estendi Volume**. Avvia procedura guidata Estendi Volume Hello. Fare clic su **Avanti**.
   4. Completare l'installazione guidata di hello, accettando i valori predefiniti di hello. Al termine, la procedura guidata hello volume hello presenteranno dimensioni hello aumentato.
      
      > [!NOTE]
      > Se si espande un volume aggiunto in locale e quindi espandere aggiunti localmente un altro volume immediatamente in seguito, i processi di espansione di hello volume vengono eseguiti in sequenza. processo di espansione Hello primo volume deve essere completata prima di iniziarne il processo di espansione volume successivo hello.
      

## <a name="change-hello-volume-type"></a>Modificare il tipo di volume hello

È possibile modificare il tipo di volume hello da toolocally a più livelli bloccato o da tootiered aggiunti in locale. Questa conversione non deve tuttavia essere eseguita con frequenza.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Considerazioni sulla conversione di volume toolocal a più livelli

Per la conversione di un volume da toolocally a più livelli aggiunti alcuni motivi sono:

* Garanzie locali relative alla disponibilità e alle prestazioni dei dati
* Eliminazione di latenze cloud e di problemi di connettività cloud

In genere, questi sono piccoli volumi esistenti che si desidera tooaccess frequentemente. Quando un volume aggiunto in locale viene creato, ne viene effettuato il provisioning completo. 

Se si converte un volume aggiunto in locale tooa volume a livelli, StorSimple verifica di disporre di spazio sufficiente nel dispositivo prima di avviare la conversione di hello. Se si dispone di spazio sufficiente, verrà visualizzato un errore e hello operazione verrà annullata. 

> [!NOTE]
> Prima di iniziare una conversione da a più livelli toolocally bloccato, assicurarsi di considerare di hello requisiti di spazio di altri carichi di lavoro. 

Conversione da un volume a livelli tooa aggiunto in locale può influire negativamente sulle prestazioni del dispositivo. Inoltre, hello seguenti fattori potrà aumentare hello tempo conversione hello toocomplete:

* Larghezza di banda insufficiente.
* Nessun backup corrente disponibile.

effetti di hello toominimize che questi fattori possono avere:

* Rivedere i criteri di limitazione della larghezza di banda e verificare che sia disponibile una larghezza di banda dedicata di 40 Mbps.
* Pianificare la conversione di hello per le ore.
* Creare uno snapshot cloud prima di iniziare la conversione di hello.

Se si desidera convertire più volumi (sono supportati diversi carichi di lavoro), quindi si deve assegnare priorità conversione del volume hello in modo che i volumi di priorità superiore vengono convertiti prima. Ad esempio, è necessario convertire i volumi che ospitano macchine virtuali o con carichi di lavoro SQL prima dei volumi con carichi di lavoro di condivisione file.

### <a name="local-tootiered-volume-conversion-considerations"></a>Considerazioni sulla conversione di volume tootiered locale

È opportuno toochange tooa un volume aggiunto in locale a livelli volume se è necessario spazio aggiuntivo tooprovision altri volumi. Quando si converte tootiered volume hello aggiunto in locale, la capacità disponibile hello sul dispositivo hello Aumenta dimensioni hello della capacità di hello rilasciato. Se i problemi di connettività impediscono la conversione di hello di un volume da hello tipo locale toohello a livelli tipo, hello volume locale verrà garantite le proprietà di un volume a livelli fino a quando non è stata completata la conversione di hello. Questo avviene perché alcuni dati potrebbero avere distribuito toohello cloud. Questi dati spill continuano toooccupy spazio locale nel dispositivo hello che non può essere liberato finché l'operazione di hello viene riavviata e completata.

> [!NOTE]
> La conversione di un volume può richiedere tempo e non è possibile annullarla una volta avviata. volume Hello rimane online durante la conversione, hello ed eseguire il backup, ma non è possibile espandere o ripristinare il volume di hello durante la conversione di hello.


#### <a name="toochange-hello-volume-type"></a>tipo di volume hello toochange

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **dispositivi**. Elenco tabulare di hello di dispositivi hello, selezionare dispositivo hello con volume hello che si desidera toomodify. Fare clic su **Impostazioni > Volumi**.

    ![Andare a pannello tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Hello tabulare elenco di volumi, selezionare il volume di hello dal menu di scelta rapida di contesto tooinvoke hello. Selezionare **Modifica**.

    ![Seleziona Elimina dal menu di scelta rapida](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. In hello **modifica del volume** pannello, modificare il tipo di volume hello selezionando il nuovo tipo di hello hello **tipo** elenco a discesa.
   
   * Se si modifica il tipo di hello troppo**aggiunto in locale**, StorSimple controllerà toosee se hanno sufficiente capacità.
   * Se si modifica il tipo di hello troppo**a livelli** e il volume verrà utilizzato per i dati di archiviazione, seleziona hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo.
   * Se si sta configurando un volume aggiunto in locale come a più livelli o _viceversa_, hello seguente messaggio viene visualizzato.
   
    ![Messaggio relativo alla modifica del tipo di volume](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Fare clic su **salvare** modifiche hello toosave. Quando viene richiesta la conferma, fare clic su **Sì** toostart processo di conversione hello. 

    ![Salvare e confermare](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. portale di Azure viene visualizzato una notifica per la creazione di processi hello che aggiorna volume hello. Fare clic su stato di hello notifica toomonitor hello del processo di conversione volume hello.

    ![Processo di conversione del volume](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Portare un volume offline

Potrebbe essere necessario tootake un volume offline quando si intende toomodify o eliminare il volume di hello. Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura. È necessario portare offline di volume hello sull'host di hello e dispositivo hello.

#### <a name="tootake-a-volume-offline"></a>tootake un volume offline

1. Assicurarsi che il volume di hello in questione non è in uso prima di portarlo offline.
2. Portare hello volume offline nell'host di hello prima. In questo modo si evita i potenziali rischi di danneggiamento dei dati nel volume hello. Per passaggi specifici, vedere toohello istruzioni per il sistema operativo host.
3. Dopo aver hello host è offline, portare il volume di hello sul dispositivo hello offline eseguendo hello alla procedura seguente:
   
    1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **dispositivi**. Elenco tabulare di hello di dispositivi hello, selezionare dispositivo hello con volume hello che si desidera toomodify. Fare clic su **Impostazioni > Volumi**.

        ![Andare a pannello tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. Hello tabulare elenco di volumi, selezionare il volume di hello dal menu di scelta rapida di contesto tooinvoke hello. Selezionare **portare offline** volume hello tootake si modificherà offline.

        ![Selezionare e portare offline i volumi](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. In hello **portare offline** pannello, esaminare l'impatto di hello di portare offline il volume di hello e selezionare la casella di controllo corrispondente hello. Fare clic su **Porta offline**. 

    ![Esaminare l'impatto del portare un volume offline](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Ricevere notifiche quando il volume di hello è offline. lo stato dei volumi Hello aggiorna anche tooOffline.
      
4. Dopo che un volume è offline, se si seleziona volume hello e pulsante destro del mouse, **in linea** opzione diventa disponibile nel menu di scelta rapida hello.

> [!NOTE]
> Hello **non in linea** comando invia un volume hello tootake dispositivo toohello offline. Se l'host siano ancora utilizzando il volume di hello, ciò comporta l'interruzione delle connessioni, ma disconnettere volume hello non avrà esito negativo.

## <a name="delete-a-volume"></a>Eliminare un volume

> [!IMPORTANT]
> È possibile eliminare un volume solo se è offline.

Completare hello seguendo i passaggi toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **dispositivi**. Elenco tabulare di hello di dispositivi hello, selezionare dispositivo hello con volume hello che si desidera toomodify. Fare clic su **Impostazioni > Volumi**.

    ![Andare a pannello tooVolumes](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Controllare lo stato di hello del volume hello desiderato toodelete. Se il volume di hello da toodelete non è offline, portarlo prima offline. Seguire i passaggi di hello in [portare offline un volume](#take-a-volume-offline).
4. Dopo che il volume di hello è offline, selezionare il volume di hello, menu di scelta rapida hello tooinvoke destro e quindi selezionare **eliminare**.

    ![Seleziona Elimina dal menu di scelta rapida](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. In hello **eliminare** pannello, esaminare e hello selezionare la casella di controllo in relazione impatto hello di eliminazione di un volume. Quando si elimina un volume, tutti i dati che si trovano in hello hello viene perso. 

    ![Salvare e confermare le modifiche](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Una volta eliminato il volume di hello, hello Elenco tabulare dei volumi verrà aggiornato l'eliminazione di hello tooindicate.

    ![Elenco aggiornato dei volumi](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Se si elimina un volume aggiunto in locale, spazio hello disponibile per nuovi volumi non può essere aggiornato immediatamente. Servizio di gestione di dispositivi StorSimple Hello Aggiorna periodicamente hello locale spazio. È consigliabile che attendere qualche minuto prima di tentare di nuovo volume di toocreate hello.
   >
   > Inoltre, se si elimina un volume aggiunto in locale e quindi eliminarla un altro localmente bloccata volume immediatamente in seguito, i processi di eliminazione volume hello vengono eseguiti in sequenza. processo di eliminazione Hello primo volume deve essere completata prima di iniziarne il processo di eliminazione volume Avanti hello.

## <a name="monitor-a-volume"></a>Monitorare un volume

Il monitoraggio dei volumi consente toocollect relativi ai / O le statistiche per un volume. Il monitoraggio è attivato per impostazione predefinita per hello primi 32 volumi creati. Il monitoraggio di ulteriori volumi è disabilitato per impostazione predefinita. 

> [!NOTE]
> Il monitoraggio di volumi clonati è disabilitato per impostazione predefinita.


Eseguire i seguenti passaggi tooenable hello o disabilitare il monitoraggio per un volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o disabilitare il monitoraggio dei volumi

1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **dispositivi**. Elenco tabulare di hello di dispositivi hello, selezionare dispositivo hello con volume hello che si desidera toomodify. Fare clic su **Impostazioni > Volumi**.
2. Hello tabulare elenco di volumi, selezionare il volume di hello dal menu di scelta rapida di contesto tooinvoke hello. Selezionare **Modifica**.
3. In hello **modifica del volume** pannello per **monitoraggio** selezionare **abilitare** o **disabilitare** tooenable o disabilitare il monitoraggio.

    ![Disabilitare il monitoraggio](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**. portale di Azure viene visualizzato una notifica per l'aggiornamento di volume hello e quindi un messaggio di conferma, dopo aver completato l'aggiornamento di volume hello.

## <a name="next-steps"></a>Passaggi successivi

* Informazioni su come troppo[clonare un volume StorSimple](storsimple-8000-clone-volume-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

