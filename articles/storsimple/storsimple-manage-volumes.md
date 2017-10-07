---
title: aaaManage i volumi StorSimple | Documenti Microsoft
description: Viene illustrato come tooadd, modificare, monitorare ed eliminare i volumi StorSimple e come tootake, non in linea se necessario.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Utilizzare i volumi di toomanage servizio StorSimple Manager hello
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come toouse hello toocreate servizio StorSimple Manager e gestire i volumi nel dispositivo StorSimple hello e dispositivo virtuale StorSimple.

servizio StorSimple Manager Hello è un'estensione di hello portale classico di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web. Nei volumi toomanaging aggiunta, è possibile utilizzare toocreate servizio StorSimple Manager di hello e gestire i servizi StorSimple, visualizzare e gestire i dispositivi, visualizzare gli avvisi e visualizzare e gestire criteri di backup e di catalogo di backup hello.

> [!NOTE]
> StorSimple di Azure consente di creare solo volumi di thin provisioning. Non è possibile creare volumi con provisioning completo o parziale in un sistema StorSimple di Azure.
> 
> Thin provisioning è una tecnologia di virtualizzazione in cui archiviazione disponibili risultano tooexceed di risorse fisiche. Anziché riservare in anticipo spazio di archiviazione sufficiente, Azure StorSimple Usa tooallocate di provisioning thin sufficiente spazio toomeet corrente. natura elastica di Hello dell'archiviazione cloud facilita questo approccio perché StorSimple di Azure è possibile aumentare o diminuire cloud archiviazione toomeet cambiare della domanda.
> 
> 

## <a name="hello-volumes-page"></a>pagina volumi Hello
Hello **volumi** pagina permette di volumi di archiviazione hello toomanage sono a provisioning nel dispositivo Microsoft Azure StorSimple hello per gli iniziatori (server). Viene visualizzato l'elenco di hello dei volumi nel dispositivo StorSimple.

 ![Pagina dei volumi](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Un volume è costituito da una serie di attributi:

* **Nome** : un nome descrittivo che deve essere univoco e consente di identificare il volume di hello. Questo nome viene utilizzato anche nei rapporti di monitoraggio quando di applica un filtro su un volume specifico.
* **Stato** : online oppure offline. Se un volume offline, non è visibile tooinitiators (server) che è consentito l'accesso toouse hello volume.
* **Capacità** : specifica le dimensioni volume hello è, base alla percezione dell'iniziatore hello (server). La capacità specifica quantità totale di hello di dati che possono essere archiviati dall'iniziatore hello (server). Viene eseguito il thin provisioning del volumi e i dati vengono deduplicati. Ciò implica che il dispositivo non esegue la preallocazione della capacità di archiviazione fisica internamente o nel cloud hello in tooconfigured capacità del volume di base. capacità del volume Hello viene allocata e usata su richiesta.
* **Tipo** -tipo di volume hello può essere a più livelli o dell'archivio (un sottotipo del tipo a livelli)
* **Accesso** – specifica iniziatori hello (server) che sono consentiti l'accesso toothis volume. Gli iniziatori che non sono membri di record di controllo di accesso (ACR) associato al volume hello non verranno visualizzato il volume di hello.
* **Monitoraggio** : specifica se un volume viene monitorato. Un volume avrà il monitoraggio abilitato per impostazione predefinita quando viene creato. Il monitoraggio sarà però disabilitato per un clone del volume. tooenable monitoraggio per un volume, seguire le istruzioni hello monitoraggio un volume.

attività più comuni di Hello associata a un volume sono:

* Aggiungere un volume
* Modificare un volume
* Eliminare un volume
* Portare un volume offline
* Monitorare a volume

## <a name="add-a-volume"></a>Aggiungere un volume
Il [volume è stato creato](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) durante la distribuzione della soluzione StorSimple. L’aggiunta di un volume è una procedura simile.

### <a name="tooadd-a-volume"></a>tooadd un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare un contenitore del volume e fare clic sulla freccia hello hello corrispondente riga tooaccess hello volumi associati al contenitore hello.
3. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello. viene avviata l'aggiunta guidata volume Hello.
   
     ![Aggiungi procedura guidata del volume Impostazioni di base](./media/storsimple-manage-volumes/AddVolume1.png)
4. In hello Aggiungi un volume, in **le impostazioni di base**, hello seguenti:
   
   1. Digitare un **Nome** per il volume.
   2. Specificare hello **capacità fornita** per il volume in GB o TB. capacità di Hello deve essere compreso tra 1 GB e 64 TB per un dispositivo fisico. capacità massima di Hello che è possibile effettuare il provisioning per un volume su un dispositivo virtuale StorSimple è di 30 TB.
   3. Seleziona hello **tipo di utilizzo** per il volume. Se si utilizza un volume a livelli per i dati di archiviazione, la selezione di hello hello **usare questo volume per i dati dell'archivio si accede di frequente** le dimensioni del blocco hello deduplicazione per il volume di casella di controllo too512 KB. Se non si seleziona questa opzione, il volume a livelli corrispondente hello utilizzerà una dimensione del blocco di 64 KB. Dimensioni del blocco più grande deduplicazione consentono trasferimento di hello dispositivi tooexpedite hello del cloud toohello dati dell'archivio di grandi dimensioni. (I volumi a livelli precedentemente chiamati volumi primari).
   4. Fare clic sull'icona di freccia hello ![icona freccia](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **impostazioni aggiuntive** pagina.
      
        ![Aggiungi procedura guidata del volume Impostazioni aggiuntive](./media/storsimple-manage-volumes/AddVolume2.png)
5. Nella finestra di dialogo **Impostazioni aggiuntive**, aggiungere un nuovo record di controllo di accesso (ACR):
   
   1. Selezionare un record di controllo di accesso (ACR) dall'elenco a discesa hello. In alternativa, è possibile aggiungere un nuovo ACR. ACR determinano quali host possono accedere ai volumi da hello corrispondente ospitare IQN con quello elencato nel record di hello.
   2. Si consiglia di abilitare un backup predefinito selezionando hello **abilitare un backup predefinito per questo volume** casella di controllo.
   3. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-volumes/HCS_CheckIcon.png) volume di hello toocreate con hello specificato le impostazioni.

Il nuovo volume è ora pronto toouse.

## <a name="modify-a-volume"></a>Modificare un volume
Modificare un volume quando è necessario tooexpand o modifica gli host che accedono a volume hello hello.

> [!IMPORTANT]
> * Se si modifica la dimensione del volume hello sul dispositivo hello, dimensioni del volume hello devono toobe modificato anche l'host hello.
> * procedure sul lato host Hello descritte di seguito sono per Windows Server 2012 (versione 2012 R2). Procedure per Linux o altri sistemi operativi host saranno diverse. Vedere le istruzioni di sistema operativo host tooyour quando si modifica il volume di hello in un host in esecuzione un altro sistema operativo.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitore del Volume** scheda. Questa pagina elenca in formato tabulare tutti i contenitori di volumi di hello associati al dispositivo hello.
2. Selezionare un contenitore di volumi e farvi clic sopra elenco hello toodisplay di tutti i volumi di hello all'interno del contenitore di hello.
3. In hello **volumi** pagina, selezionare un volume e fare clic su **modifica**.
4. In hello Modifica guidata volume in **le impostazioni di base**, è possibile eseguire il seguente hello:
   
   * Modifica hello **nome** e **tipo** se si desidera toomodify un volume di archiviazione tooan volume a livelli selezionando hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo toochange hello deduplicazione dimensioni del blocco per il volume too512 KB.
   * Aumentare hello **capacità fornita**. Hello **capacità fornita** può solo essere aumentato. Non è possibile ridurre un volume dopo averlo creato.
     
     > [!NOTE]
     > È possibile modificare il contenitore di volumi hello dopo l'assegnazione tooa volume.
     > 
     > 
5. In **impostazioni aggiuntive**, è possibile eseguire il seguente hello:
   
   * Modificare ACR hello, purché hello volume è offline. Se il volume di hello è online, sarà necessario tootake il primo non in linea. Fare riferimento passaggi toohello [portare offline un volume](#take-a-volume-offline) hello toomodifying precedente record.
   * Modificare l'elenco di hello di ACR dopo che il volume di hello è offline.
     
     > [!NOTE]
     > Non è possibile modificare hello **abilitare un backup predefinito per questo volume** opzione per il volume di hello.
     > 
     > 
6. Salvare le modifiche facendo clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-manage-volumes/HCS_CheckIcon.png). portale di Azure classico Hello visualizzerà un messaggio di volume ad aggiornamento. Quando è stata aggiornata volume hello visualizzerà un messaggio di conferma.
7. Se si vuole espandere un volume, completare hello nel computer host Windows come segue:
   
   1. Andare troppo**Gestione Computer** ->**Gestione disco**.
   2. Fare clic con il pulsante destro del mouse su **Gestione disco** e selezionare **Rescan Disks** (Ripeti analisi dischi).
   3. Nell'elenco di hello dei dischi, selezionare il volume hello che è stato aggiornato, pulsante destro del mouse e quindi selezionare **Estendi Volume**. Avvia procedura guidata Estendi Volume Hello. Fare clic su **Avanti**.
   4. Completare l'installazione guidata di hello, accettando i valori predefiniti di hello. Al termine, la procedura guidata hello volume hello presenteranno dimensioni hello aumentato.

![Video disponibile](./media/storsimple-manage-volumes/Video_icon.png)**Video disponibile**

toowatch un video che illustra come tooexpand un volume, fare clic su [qui](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Portare un volume offline
Potrebbe essere necessario tootake un volume offline quando si pianifica toomodify o eliminarlo. Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura. Sarà necessario tootake hello volume offline nell'host di hello e sul dispositivo hello. Eseguire hello seguendo i passaggi tootake un volume offline.

### <a name="tootake-a-volume-offline"></a>tootake un volume offline
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

### <a name="toodelete-a-volume"></a>toodelete un volume
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare contenitore del volume hello con volume hello da toodelete. Fare clic su hello tooaccess contenitore volume di hello **volumi** pagina.
3. Tutti i volumi di hello associati al contenitore vengono visualizzati in formato tabulare. Controllare lo stato di hello del volume hello desiderato toodelete. Se volume hello da toodelete non è offline, le operazioni non in linea hello in primo luogo, seguenti [portare offline un volume](#take-a-volume-offline).
4. Dopo che il volume di hello è offline, fare clic su **eliminare** nella parte inferiore di hello della pagina hello.
5. Alla richiesta di conferma fare clic su **Sì**. volume Hello verrà eliminata e hello **volumi** pagina verrà visualizzato l'elenco di hello aggiornato di volumi all'interno del contenitore di hello.

## <a name="monitor-a-volume"></a>Monitorare un volume
Il monitoraggio dei volumi consente toocollect relativi ai / O le statistiche per un volume. Il monitoraggio è attivato per impostazione predefinita per hello primi 32 volumi creati. Il monitoraggio di ulteriori volumi è disabilitato per impostazione predefinita. Il monitoraggio di volumi clonati è disabilitato per impostazione predefinita.

Eseguire i seguenti passaggi tooenable hello o disabilitare il monitoraggio per un volume.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o disabilitare il monitoraggio dei volumi
1. In hello **dispositivi** pagina, selezionare il dispositivo di hello, fare doppio clic e quindi fare clic su hello **contenitori di volumi** scheda.
2. Selezionare il contenitore di volumi hello in cui hello risiede volume e quindi fare clic su hello tooaccess contenitore volume di hello **volumi** pagina.
3. Nella visualizzazione tabulare hello sono elencati tutti i volumi di hello associati a questo contenitore. Selezionare il volume di hello o un clone di volume.
4. Nella parte inferiore di hello della pagina hello, fare clic su **modifica**.
5. Nella procedura guidata Modifica Volume hello in **le impostazioni di base**selezionare **abilitare** o **disabilitare** da hello **monitoraggio** elenco a discesa.
   
    ![Modificare le impostazioni di base di un volume](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[clonare un volume StorSimple](storsimple-clone-volume.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

