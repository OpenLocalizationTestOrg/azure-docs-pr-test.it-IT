---
title: aaaManage i volumi StorSimple (U2) | Documenti Microsoft
description: Viene illustrato come tooadd, modificare, monitorare ed eliminare i volumi StorSimple e come tootake, non in linea se necessario.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Utilizzare volumi toomanage di servizio StorSimple Manager hello (Update 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come toouse hello toocreate servizio StorSimple Manager e gestire i volumi nel dispositivo StorSimple hello e dispositivo virtuale StorSimple con Update 2.

servizio StorSimple Manager Hello è un'estensione in hello portale classico di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web. Nei volumi toomanaging aggiunta, è possibile utilizzare toocreate servizio StorSimple Manager di hello e gestire i servizi StorSimple, visualizzare e gestire i dispositivi, visualizzare gli avvisi e visualizzare e gestire criteri di backup e di catalogo di backup hello.

## <a name="volume-types"></a>Tipi di volume
I volumi di StorSimple possono essere:

* **Aggiunto in locale volumi**: dati in tali volumi rimangono nel dispositivo StorSimple locale hello in qualsiasi momento.
* **A più livelli volumi**: toohello cloud possono lo spill dei dati in tali volumi.

Un volume di archivio è un tipo di volume a livelli. Hello maggiore deduplicazione dimensioni del blocco utilizzate per i volumi di archiviazione consentono di segmenti maggiore hello dispositivo tootransfer di toohello dati nel cloud. 

Se necessario, è possibile modificare il tipo di volume hello da tootiered locale o da toolocal a più livelli. Per ulteriori informazioni, visitare troppo[modificare il tipo di volume hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volumi aggiunti in locale
I volumi aggiunti in locale sono completamente provisioning volumi non di livello dati nel cloud toohello, assicurando locale garantisce per dati primari, in modo indipendente di connettività cloud. I dati nei volumi aggiunti in locale non vengono deduplicati e compressi, mentre gli snapshot dei volumi aggiunti in locale vengono deduplicati. 

Poiché viene effettuato il provisioning completo dei volumi aggiunti in locale, è necessario avere spazio sufficiente nel dispositivo quando li si crea. È possibile eseguire il provisioning di volumi aggiunti in locale fino tooa la dimensione massima di 8 TB nel dispositivo StorSimple 8100 hello e 20 TB in dispositivo 8600 hello. StorSimple riserva hello locale spazio nel dispositivo hello per gli snapshot, metadati e l'elaborazione dei dati. È possibile aumentare la dimensione hello di un volume aggiunto in locale toohello spazio massimo disponibile, ma non è possibile ridurre le dimensioni di hello di un volume dopo la creazione.

Quando si crea un volume aggiunto in locale, spazio disponibile di hello per la creazione di volumi a livelli viene ridotto. Hello inversa è anche vero: se si dispone di volumi a livelli esistenti, hello spazio per la creazione di localmente pinned volumi sarà inferiore a un massimo di hello indicato in precedenza. Per ulteriori informazioni sui volumi locali, vedere toohello [domande frequenti sui volumi aggiunti in locale](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Volumi a livelli
I volumi a livelli sono volumi con thin provisioning in cui hello spesso dati di accesso rimangono locale nel dispositivo hello e meno dati utilizzate di frequente sono automaticamente a livelli toohello cloud. Thin provisioning è una tecnologia di virtualizzazione in cui archiviazione disponibili risultano tooexceed di risorse fisiche. Anziché riservare in anticipo sufficiente spazio di archiviazione, StorSimple Usa tooallocate di provisioning thin sufficiente spazio toomeet corrente. natura elastica di Hello dell'archiviazione cloud facilita questo approccio perché StorSimple può aumentare o diminuire cloud archiviazione toomeet cambiare della domanda.

Se si utilizza un volume a livelli per i dati di archiviazione, la selezione di hello hello **usare questo volume per i dati dell'archivio si accede di frequente** le dimensioni del blocco hello deduplicazione per il volume di casella di controllo too512 KB. Se non si seleziona questa opzione, il volume a livelli corrispondente hello utilizzerà una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni.

> [!NOTE]
> Volumi di archiviazione creati con una versione 2 di pre-aggiornamento di StorSimple verranno importati come livelli hello archiviazione casella di controllo.
> 
> 

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

## <a name="hello-volumes-page"></a>pagina volumi Hello
Hello **volumi** pagina permette di volumi di archiviazione hello toomanage sono a provisioning nel dispositivo Microsoft Azure StorSimple hello per gli iniziatori (server). Viene visualizzato l'elenco di hello dei volumi nel dispositivo StorSimple.

 ![Pagina dei volumi](./media/storsimple-manage-volumes-u2/VolumePage.png)

Un volume è costituito da una serie di attributi:

* **Nome del volume** : un nome descrittivo che deve essere univoco e consente di identificare il volume di hello. Questo nome viene utilizzato anche nei rapporti di monitoraggio quando di applica un filtro su un volume specifico.
* **Stato** : online oppure offline. Se un volume è offline, non è visibile tooinitiators (server) che è consentito l'accesso toouse hello volume.
* **Capacità** – specifica hello quantità totale di dati che possono essere archiviati dall'iniziatore hello (server). Volumi aggiunti in locale vengono effettuato il provisioning completo mentre si trovano nel dispositivo StorSimple hello. I volumi a livelli con thin provisioning e hello dati sono deduplicati. Con i volumi con thin provisioning, il dispositivo non esegue la preallocazione della capacità di archiviazione fisica internamente o nel cloud hello in tooconfigured capacità del volume di base. capacità del volume Hello viene allocata e usata su richiesta.
* **Tipo** – indica se il volume di hello è **a livelli** (hello predefinito) o **aggiunto in locale**.
* **Backup** – indica se è presente un criterio di backup predefinito per il volume di hello.
* **Accesso** – specifica iniziatori hello (server) che sono consentiti l'accesso toothis volume. Gli iniziatori che non sono membri di record di controllo di accesso (ACR) associato al volume hello non verranno visualizzato il volume di hello.
* **Monitoraggio** : specifica se un volume viene monitorato. Un volume avrà il monitoraggio abilitato per impostazione predefinita quando viene creato. Il monitoraggio sarà però disabilitato per un clone del volume. tooenable monitoraggio per un volume, seguire le istruzioni hello [monitoraggio di un volume](#monitor-a-volume). 

Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:

* Aggiungere un volume 
* Modificare un volume 
* Modificare il tipo di volume hello
* Eliminare un volume 
* Portare un volume offline 
* Monitorare a volume 

## <a name="add-a-volume"></a>Aggiungere un volume
Il [volume è stato creato](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) durante la distribuzione della soluzione StorSimple. L’aggiunta di un volume è una procedura simile.

#### <a name="tooadd-a-volume"></a>tooadd un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare un contenitore di volumi hello elenco e fare doppio clic tooaccess hello volumi associati al contenitore hello.
3. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello. viene avviata l'aggiunta guidata volume Hello.
   
     ![Aggiungi procedura guidata del volume Impostazioni di base](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. In hello Aggiungi un volume, in **le impostazioni di base**, hello seguenti:
   
   1. Digitare un **Nome** per il volume.
   2. Selezionare un **tipo di utilizzo** dall'elenco a discesa hello. Per i carichi di lavoro che richiedono dati toobe disponibili in locale nel dispositivo hello in qualsiasi momento, selezionare **aggiunto in locale**. Per tutti gli altri tipi di dati, selezionare **A livelli**. (**a livelli** hello predefinito.)
   3. Se si seleziona **a livelli** nel passaggio 2, è possibile selezionare hello **usare questo volume per i dati dell'archivio si accede di frequente** tooconfigure casella di controllo un volume di archiviazione.
   4. Immettere hello **capacità fornita** per il volume in GB o TB. Vedere [Capacità con provisioning](#provisioned-capacity) per conoscere le dimensioni massime per ogni tipo di dispositivo e di volume. Esaminare hello **capacità disponibile** toodetermine lo spazio di archiviazione è effettivamente disponibile nel dispositivo.
5. Fare clic sull'icona di freccia hello![Icona freccia](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Se si sta configurando un volume aggiunto in locale, si noterà segue messaggio hello.
   
    ![Messaggio relativo alla modifica del tipo di volume](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Fare clic sull'icona di freccia hello ![icona freccia](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)nuovamente toogo toohello **impostazioni aggiuntive** pagina.
   
    ![Aggiungi procedura guidata del volume Impostazioni aggiuntive](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. Nella finestra di dialogo **Impostazioni aggiuntive**, aggiungere un nuovo record di controllo di accesso (ACR):
   
   1. Selezionare un record di controllo di accesso (ACR) dall'elenco a discesa hello. In alternativa, è possibile aggiungere un nuovo ACR. ACR determinano quali host possono accedere ai volumi da hello corrispondente ospitare IQN con quello elencato nel record di hello. Se non si specifica un record, verrà visualizzato hello seguente messaggio.
      
        ![Specificare un ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. È consigliabile selezionare hello **abilitare un backup predefinito per questo volume** casella di controllo.
   3. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) volume di hello toocreate con hello specificato le impostazioni.

Il nuovo volume è ora pronto toouse.

> [!NOTE]
> Se si crea un volume aggiunto in locale e quindi creare un altro localmente bloccata volume immediatamente in seguito, i processi di creazione volume hello eseguiti in sequenza. processo di creazione di Hello primo volume deve essere completata prima di iniziarne il processo di creazione volume Avanti hello.
> 
> 

## <a name="modify-a-volume"></a>Modificare un volume
Modificare un volume quando è necessario tooexpand o modifica gli host che accedono a volume hello hello.

> [!IMPORTANT]
> * Se si modifica la dimensione del volume hello sul dispositivo hello, dimensioni del volume hello devono toobe modificato anche l'host hello. 
> * procedure sul lato host Hello descritte di seguito sono per Windows Server 2012 (versione 2012 R2). Procedure per Linux o altri sistemi operativi host saranno diverse. Vedere le istruzioni di sistema operativo host tooyour quando si modifica il volume di hello in un host in esecuzione un altro sistema operativo. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare un contenitore di volumi hello elenco e fare doppio clic volumi hello tooview associati hello contenitore.
3. Scegliere un volume, quindi nella parte inferiore di hello della pagina hello, **modifica**. Avvia Hello Modifica guidata volume.
4. In hello Modifica guidata volume in **le impostazioni di base**, è possibile eseguire il seguente hello:
   
   * Modifica hello **nome**.
   * Convertire hello **tipo di utilizzo** tootiered aggiunti in locale o a più livelli toolocally bloccato (vedere [modificare il tipo di volume hello](#change-the-volume-type) per altre informazioni).
   * Aumentare hello **capacità fornita**. Hello **capacità fornita** può solo essere aumentato. Non è possibile ridurre un volume dopo averlo creato.
5. In **impostazioni aggiuntive**, è possibile modificare hello ACR, purché hello volume è offline. Se il volume di hello è online, sarà necessario tootake il primo non in linea. Fare riferimento passaggi toohello [portare offline un volume](#take-a-volume-offline) hello toomodifying precedente record.
   
   > [!NOTE]
   > Non è possibile modificare hello **abilitare un backup predefinito** opzione per il volume di hello.
   > 
   > 
6. Salvare le modifiche facendo clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). portale di Azure classico Hello visualizzerà un messaggio di volume ad aggiornamento. Quando è stata aggiornata volume hello visualizzerà un messaggio di conferma.
7. Se si vuole espandere un volume, completare hello nel computer host Windows come segue:
   
   1. Andare troppo**Gestione Computer** ->**Gestione disco**.
   2. Fare clic con il pulsante destro del mouse su **Gestione disco** e selezionare **Rescan Disks** (Ripeti analisi dischi).
   3. Nell'elenco di hello dei dischi, selezionare il volume hello che è stato aggiornato, pulsante destro del mouse e quindi selezionare **Estendi Volume**. Avvia procedura guidata Estendi Volume Hello. Fare clic su **Avanti**.
   4. Completare l'installazione guidata di hello, accettando i valori predefiniti di hello. Al termine, la procedura guidata hello volume hello presenteranno dimensioni hello aumentato.
      
      > [!NOTE]
      > Se si espande un volume aggiunto in locale e quindi espandere aggiunti localmente un altro volume immediatamente in seguito, i processi di espansione di hello volume vengono eseguiti in sequenza. processo di espansione Hello primo volume deve essere completata prima di iniziarne il processo di espansione volume successivo hello.
      > 
      > 

![Video disponibile](./media/storsimple-manage-volumes-u2/Video_icon.png)**Video disponibile**

toowatch un video che illustra come tooexpand un volume, fare clic su [qui](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Modificare il tipo di volume hello
È possibile modificare il tipo di volume hello da toolocally a più livelli bloccato o da tootiered aggiunti in locale. Questa conversione non deve tuttavia essere eseguita con frequenza. Per la conversione di un volume da toolocally a più livelli aggiunti alcuni motivi sono:

* Garanzie locali relative alla disponibilità e alle prestazioni dei dati
* Eliminazione di latenze cloud e di problemi di connettività cloud

In genere, questi sono piccoli volumi esistenti che si desidera tooaccess frequentemente. Quando un volume aggiunto in locale viene creato, ne viene effettuato il provisioning completo. Se si converte un volume aggiunto in locale tooa volume a livelli, StorSimple verifica di disporre di spazio sufficiente nel dispositivo prima di avviare la conversione di hello. Se si dispone di spazio sufficiente, verrà visualizzato un errore e hello operazione verrà annullata. 

> [!NOTE]
> Prima di iniziare una conversione da a più livelli toolocally bloccato, assicurarsi di considerare di hello requisiti di spazio di altri carichi di lavoro. 
> 
> 

È possibile toochange tooa un volume aggiunto in locale a livelli volume se è necessario spazio aggiuntivo tooprovision altri volumi. Quando si converte tootiered volume hello aggiunto in locale, la capacità disponibile hello sul dispositivo hello Aumenta dimensioni hello della capacità di hello rilasciato. Se i problemi di connettività impediscono la conversione di hello di un volume da hello tipo locale toohello a livelli tipo, hello volume locale verrà garantite le proprietà di un volume a livelli fino a quando non viene completata la conversione di hello. Questo avviene perché alcuni dati potrebbero avere distribuito toohello cloud. Questi dati spill continuerà toooccupy spazio locale nel dispositivo hello che non può essere liberato finché l'operazione di hello viene riavviata e completata.

> [!NOTE]
> La conversione di un volume può richiedere tempo e non è possibile annullarla una volta avviata. volume Hello rimane online durante la conversione, hello ed eseguire il backup, ma non è possibile espandere o ripristinare il volume di hello durante la conversione di hello.  
> 
> 

Conversione da un volume a livelli tooa aggiunto in locale può influire negativamente sulle prestazioni del dispositivo. Inoltre, hello seguenti fattori potrà aumentare hello tempo conversione hello toocomplete:

* Larghezza di banda insufficiente.
* Nessun backup corrente disponibile.

effetti di hello toominimize che questi fattori possono avere:

* Rivedere i criteri di limitazione della larghezza di banda e verificare che sia disponibile una larghezza di banda dedicata di 40 Mbps.
* Pianificare la conversione di hello per le ore.
* Creare uno snapshot cloud prima di iniziare la conversione di hello.

Se si desidera convertire più volumi (sono supportati diversi carichi di lavoro), quindi si deve assegnare priorità conversione del volume hello in modo che i volumi di priorità superiore vengono convertiti prima. Ad esempio, è necessario convertire i volumi che ospitano macchine virtuali o con carichi di lavoro SQL prima dei volumi con carichi di lavoro di condivisione file.

#### <a name="toochange-hello-volume-type"></a>tipo di volume hello toochange
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare un contenitore di volumi hello elenco e fare doppio clic volumi hello tooview associati hello contenitore.
3. Scegliere un volume, quindi nella parte inferiore di hello della pagina hello, **modifica**. Avvia Hello Modifica guidata volume.
4. In hello **le impostazioni di base** pagina, modificare il tipo di utilizzo di hello selezionando il nuovo tipo di hello hello **tipo di utilizzo** elenco a discesa.
   
   * Se si modifica il tipo di hello troppo**aggiunto in locale**, StorSimple controllerà toosee se hanno sufficiente capacità.
   * Se si modifica il tipo di hello troppo**a livelli** e il volume verrà utilizzato per i dati di archiviazione, seleziona hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo.
     
       ![Casella di controllo per l'archivio](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Fare clic sull'icona di freccia hello ![icona freccia](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **impostazioni aggiuntive** pagina. Se si sta configurando un volume aggiunto in locale, hello messaggio seguente.
   
    ![Messaggio relativo alla modifica del tipo di volume](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Fare clic sull'icona di freccia hello ![Icona freccia](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toocontinue nuovamente.
7. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) processo di conversione toostart hello. Hello portale di Azure verrà visualizzato un messaggio di volume ad aggiornamento. Quando è stata aggiornata volume hello visualizzerà un messaggio di conferma.

## <a name="take-a-volume-offline"></a>Portare un volume offline
Potrebbe essere necessario tootake un volume offline quando si pianifica toomodify o eliminarlo. Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura. Sarà necessario tootake hello volume offline nell'host di hello e sul dispositivo hello. 

#### <a name="tootake-a-volume-offline"></a>tootake un volume offline
1. Assicurarsi che il volume di hello in questione non è in uso prima di portarlo offline.
2. Portare hello volume offline nell'host di hello prima. In questo modo si evita i potenziali rischi di danneggiamento dei dati nel volume hello. Per passaggi specifici, vedere toohello istruzioni per il sistema operativo host.
3. Dopo aver hello host è offline, portare il volume di hello sul dispositivo hello offline eseguendo hello alla procedura seguente:
   
   1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** hello scheda **contenitori di volumi** scheda elenchi in formato tabulare tutti Hello contenitori dei volumi associati al dispositivo hello.
   2. Selezionare un contenitore di volumi e farvi clic sopra elenco hello toodisplay di tutti i volumi di hello all'interno del contenitore di hello.
   3. Selezionare un volume e fare clic su **Offline**.
   4. Alla richiesta di conferma fare clic su **Sì**. Hello volume dovrebbe essere offline.
      
      Dopo che un volume è offline, hello **in linea** opzione diventa disponibile.

> [!NOTE]
> Hello **non in linea** comando invia un volume hello tootake dispositivo toohello offline. Se l'host siano ancora utilizzando il volume di hello, ciò comporta l'interruzione delle connessioni, ma disconnettere volume hello non avrà esito negativo. 
> 
> 

## <a name="delete-a-volume"></a>Eliminare un volume
> [!IMPORTANT]
> È possibile eliminare un volume solo se è offline.
> 
> 

Completare hello seguendo i passaggi toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare contenitore del volume hello con volume hello da toodelete. Fare clic su hello tooaccess contenitore volume di hello **volumi** pagina.
3. Tutti i volumi di hello associati al contenitore vengono visualizzati in formato tabulare. Controllare lo stato di hello del volume hello desiderato toodelete. Se volume hello da toodelete non è offline, le operazioni non in linea hello in primo luogo, seguenti [portare offline un volume](#take-a-volume-offline).
4. Dopo che il volume di hello è offline, fare clic su **eliminare** nella parte inferiore di hello della pagina hello.
5. Alla richiesta di conferma fare clic su **Sì**. volume Hello verrà eliminata e hello **volumi** pagina verrà visualizzato l'elenco di hello aggiornato di volumi all'interno del contenitore di hello.
   
   > [!NOTE]
   > Se si elimina un volume aggiunto in locale, spazio hello disponibile per nuovi volumi non può essere aggiornato immediatamente. Servizio StorSimple Manager Hello Aggiorna periodicamente hello locale spazio. È consigliabile che attendere qualche minuto prima di tentare di nuovo volume di toocreate hello.<br> Inoltre, se si elimina un volume aggiunto in locale e quindi eliminarla un altro localmente bloccata volume immediatamente in seguito, i processi di eliminazione volume hello vengono eseguiti in sequenza. processo di eliminazione Hello primo volume deve essere completata prima di iniziarne il processo di eliminazione volume Avanti hello.
   > 
   > 

## <a name="monitor-a-volume"></a>Monitorare un volume
Il monitoraggio dei volumi consente toocollect relativi ai / O le statistiche per un volume. Il monitoraggio è attivato per impostazione predefinita per hello primi 32 volumi creati. Il monitoraggio di ulteriori volumi è disabilitato per impostazione predefinita. Il monitoraggio di volumi clonati è disabilitato per impostazione predefinita.

Eseguire i seguenti passaggi tooenable hello o disabilitare il monitoraggio per un volume.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o disabilitare il monitoraggio dei volumi
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare il contenitore di volumi hello in cui hello risiede volume e quindi fare clic su hello tooaccess contenitore volume di hello **volumi** pagina.
3. Nella visualizzazione tabulare hello sono elencati tutti i volumi di hello associati a questo contenitore. Selezionare il volume di hello o un clone di volume.
4. Nella parte inferiore di hello della pagina hello, fare clic su **modifica**.
5. Nella procedura guidata Modifica Volume hello in **le impostazioni di base**selezionare **abilitare** o **disabilitare** da hello **monitoraggio** elenco a discesa.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[clonare un volume StorSimple](storsimple-clone-volume.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

