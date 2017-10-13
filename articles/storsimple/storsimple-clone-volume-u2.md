---
title: Clonare il volume serie 8000 StorSimple | Documentazione Microsoft
description: Vengono descritti i diversi tipi di clone e le relative situazioni di utilizzo. Viene inoltre illustrato come utilizzare un set di backup per clonare un singolo volume.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 2b627250df62bbe3299869ef3812947afbb8f29f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume-update-2"></a>Utilizzare il servizio StorSimple Manager per clonare un volume (aggiornamento 2)
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Panoramica
Nella pagina **Catalogo di backup** del servizio StorSimple Manager vengono visualizzati tutti i set di backup creati quando si eseguono backup manuali o automatizzati. È possibile utilizzare questa pagina per elencare tutti i backup per un criterio di backup o un volume, selezionare o eliminare i backup o utilizzare un backup per ripristinare o clonare un volume.

![Pagina catalogo di backup](./media/storsimple-clone-volume-u2/backupCatalog.png)  

In questa esercitazione viene descritto come utilizzare un set di backup per clonare un singolo volume. Viene inoltre spiegata la differenza tra cloni *temporanei* e *permanenti*.

> [!NOTE]
> Un volume aggiunto in locale verrà duplicato come volume a livelli. Se è necessario che il volume clonato venga aggiunto in locale, è possibile convertire il clone in un volume aggiunto in locale dopo il completamento dell'operazione di clonazione. Per informazioni sulla conversione di un volume a livelli in volume aggiunto in locale, vedere l'articolo relativo alla [Modificare il tipo di volume](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Se si tenta di convertire un volume clonato da volume a livelli a volume aggiunto in locale immediatamente dopo la clonazione (quando è ancora un clone temporaneo), la conversione avrà esito negativo con il messaggio di errore seguente:
> 
> `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.` 
> 
> Questo errore si verifica solo se si esegue la clonazione in un altro dispositivo. È possibile convertire correttamente il volume in volume aggiunto in locale se il clone temporaneo viene prima convertito in un clone permanente. Per convertire il clone temporaneo in un clone permanente, creare uno snapshot cloud di esso.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Creare un clone di un volume
È possibile creare un clone sullo stesso dispositivo, su un altro dispositivo o persino su una macchina virtuale utilizzando uno snapshot locale o del cloud.

#### <a name="to-clone-a-volume"></a>Per clonare un volume
1. Nella pagina del servizio StorSimple Manager, fare clic sulla scheda **Catalogo di Backup** e selezionare un set di backup.
2. Espandere il set di backup per visualizzare i volumi associati. Fare clic e selezionare un volume dal set di backup.
   
     ![Clonare un volume](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Fare clic su **Clona** per iniziare a clonare il volume selezionato.
4. Nella procedura guidata Clona volume, in **Impostazione nome e percorso**:
   
   1. Identificare un dispositivo di destinazione. Si tratta del percorso in cui verrà creato il clone. È possibile scegliere lo stesso dispositivo o specificare un altro dispositivo. Se si sceglie un volume associato ad altri provider di servizi cloud (non Azure), nell'elenco a discesa per il dispositivo di destinazione verranno visualizzati solo i dispositivi fisici. Non è possibile clonare un volume associato con altri provider di servizi cloud in un dispositivo virtuale.
      
      > [!NOTE]
      > Assicurarsi che la capacità richiesta per il clone sia inferiore a quella disponibile nel dispositivo di destinazione.
      > 
      > 
   2. Specificare un nome volume univoco per il clone. Il nome deve contenere tra 3 e 127 caratteri. 
      
      > [!NOTE]
      > Il campo **Clona volume come** viene impostato su **A livelli** anche se si esegue la clonazione di un volume aggiunto in locale. Non è possibile modificare questa impostazione. Tuttavia, se è necessario che il volume clonato venga aggiunto anche in locale, è possibile convertire il clone in un volume aggiunto in locale dopo averlo creato. Per informazioni sulla conversione di un volume a livelli in volume aggiunto in locale, vedere l'articolo relativo alla [Modificare il tipo di volume](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Clonazione guidata 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Fare clic sull'icona freccia  ![icona a forma di freccia](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) per passare alla pagina successiva.
5. In **Specificare gli host che possono utilizzare questo volume**:
   
   1. Specificare un record di controllo di accesso (ACR) per il clone. È possibile aggiungere un nuovo ACR o scegliere dall'elenco esistente.
      
        ![Clonazione guidata 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Fare clic sull’icona del segno di spunta  ![icona del segno di spunta](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)per completare l’operazione.
6. Verrà avviato un processo di clonazione e quando il clone viene creato correttamente si riceverà una notifica. Fare clic su **Visualizza processo** per monitorare il processo di clonazione nella pagina **Processi**. Al termine del processo di clonazione, verrà visualizzato il messaggio seguente:
   
    ![Messaggio clone](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Al termine del processo di clonazione:
   
   1. Nella pagina **Dispositivi** fare clic sulla scheda **Contenitori dei volumi**. 
   2. Selezionare il contenitore del volume associato al volume di origine clonato. Nell'elenco di volumi, verrà visualizzato il clone che è stato appena creato.

> [!NOTE]
> Il monitoraggio e il backup predefinito vengono disabilitati automaticamente in un volume clonato.
> 
> 

Un clone creato in questo modo è un clone temporaneo. Per ulteriori informazioni sui tipi di cloni, vedere [Cloni temporanei e cloni permanenti](#transient-vs-permanent-clones).

Questo clone ora è un volume normale e qualsiasi operazione possibile su un volume sarà disponibile anche per il clone. È necessario configurare questo volume per tutti i backup.

## <a name="transient-vs-permanent-clones"></a>Cloni temporanei e cloni permanenti
I cloni temporanei vengono creati solo quando si esegue la clonazione in un dispositivo differente. È possibile clonare un volume specifico da un set di backup in un dispositivo differente gestito da StorSimple Manager. Il clone temporaneo disporrà di riferimenti ai dati nel volume originale e userà tali dati per la lettura e la scrittura in locale sul dispositivo di destinazione. 

Dopo l'esecuzione di uno snapshot del cloud di un clone temporaneo, il clone risultante sarà un clone *permanente* . Durante questo processo viene creata una copia dei dati nel cloud e il tempo di copia è determinato dalla dimensione dei dati e dalle latenze di Azure (si tratta di una copia da Azure ad Azure). Il processo potrebbe richiedere da giorni a settimane. In questo modo il clone temporaneo diventa permanente e non contiene alcun riferimento ai dati del volume originale dal quale è stato clonato. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenari per cloni temporanei e cloni permanenti
Nelle sezioni seguenti vengono descritte situazioni di esempio in cui è possibile utilizzare cloni temporanei e permanenti.

### <a name="item-level-recovery-with-a-transient-clone"></a>Ripristino a livello di elemento con un clone temporaneo
È necessario ripristinare un file di presentazione di Microsoft PowerPoint dell’anno precedente. L'amministratore IT identifica il backup di tale periodo di tempo specifico e filtra il volume. Quindi, l'amministratore clona il volume, individua il file che si sta cercando e lo fornisce all'utente. In questo scenario viene utilizzato un clone temporaneo. 

![Video disponibile](./media/storsimple-clone-volume-u2/Video_icon.png) **Video disponibile**

Per guardare un video che illustra come è possibile utilizzare le funzionalità di copia e ripristino di StorSimple per ripristinare file eliminati, fare clic [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a>Test nell'ambiente di produzione con un clone permanente
È necessario verificare un bug di test nell'ambiente di produzione. Viene creato un clone del volume nell'ambiente di produzione e quindi creato uno snapshot cloud di questo clone per creare un volume clonato indipendente. In questo scenario viene utilizzato un clone permanente.  

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come [ripristinare un volume StorSimple da un set di backup](storsimple-restore-from-backup-set-u2.md).
* Informazioni su come [utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).

