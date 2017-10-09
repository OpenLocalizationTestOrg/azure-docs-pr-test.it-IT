---
title: servizio di gestione di dispositivi StorSimple aaaDeploy | Documenti Microsoft
description: Viene illustrato come toocreate e delete hello del servizio di gestione di dispositivi StorSimple nel portale di Azure hello e descrive come toomanage hello chiave di registrazione del servizio.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Distribuire il servizio di gestione di dispositivi StorSimple hello per Array virtuale StorSimple
## <a name="overview"></a>Panoramica

servizio di gestione di dispositivi StorSimple Hello in esecuzione in Microsoft Azure e si connette dispositivi StorSimple toomultiple. Dopo aver creato il servizio di hello, è possibile utilizzare i dispositivi di hello toomanage da hello Microsoft Azure portale in esecuzione in un browser. In questo modo toomonitor tutti i dispositivi che sono connesso toohello dispositivo StorSimple Manager hello del servizio da un'unica posizione centrale, riducendo così al minimo carico amministrativo.

Hello comuni attività correlati tooa servizio di gestione di dispositivi StorSimple sono:

* Creare un servizio
* Eliminare un servizio
* Ottenere una chiave di registrazione del servizio hello
* Rigenerare la chiave di registrazione del servizio hello

In questa esercitazione viene descritto come tooperform di hello attività precedenti. informazioni di Hello contenute in questo articolo sono applicabile solo matrici virtuale tooStorSimple. Per ulteriori informazioni su StorSimple serie 8000, visitare troppo[distribuire un servizio StorSimple Manager](storsimple-manage-service.md).

## <a name="create-a-service"></a>Creare un servizio

toocreate un servizio, è necessario toohave:

* Una sottoscrizione con un contratto Enterprise Agreement
* Un account di archiviazione di Microsoft Azure attivo
* le informazioni di fatturazione che viene utilizzate per la gestione accessi Hello

È inoltre possibile toogenerate un account di archiviazione quando si crea il servizio di hello.

Un singolo servizio può gestire più dispositivi, ma un dispositivo non può estendersi a più servizi. Una grande organizzazione può avere più toowork di istanze di servizio con diverse sottoscrizioni, organizzazioni o anche percorsi di distribuzione.

> [!NOTE]
> È necessario istanze separate di dispositivi della serie StorSimple 8000 toomanage servizio StorSimple Manager di dispositivi e le matrici virtuale StorSimple.


Eseguire hello seguendo i passaggi toocreate un servizio.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminare un servizio

Prima di eliminare un servizio, verificare che non sia usato da dispositivi connessi. Se il servizio di hello è in uso, disattivare i dispositivi connesso hello. operazione di disattivazione Hello dividere hello connessione tra il dispositivo di hello e servizio hello, ma conservare i dati del dispositivo hello nel cloud hello.

> [!IMPORTANT]
> Dopo l'eliminazione di un servizio, operazione hello non può essere annullata. Qualsiasi dispositivo che utilizza il servizio hello sarà necessario toobe delle impostazioni di fabbrica prima che possa essere usato con un altro servizio. In questo scenario, i dati locali di hello sul dispositivo hello, nonché la configurazione di hello, andranno persi.
 

Eseguire hello seguendo i passaggi toodelete un servizio.

#### <a name="toodelete-a-service"></a>toodelete un servizio

1. Andare troppo**tutte le risorse**. Ricercare il servizio Gestione dispositivi StorSimple. Selezionare servizio hello che si desidera toodelete.
   
    ![Selezionare servizio toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Passare tooyour servizio dashboard tooensure esistono dispositivi non connesso toohello servizio. Se non sono presenti dispositivi registrati con questo servizio, verrà visualizzato anche un effetto di toohello messaggio banner. Fare clic su **Elimina**.
   
    ![Delete service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Quando viene richiesta la conferma, fare clic su **Sì** nella notifica di conferma hello. 
   
    ![Confermare l'eliminazione del servizio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Potrebbe richiedere alcuni minuti per hello servizio toobe eliminato. Dopo aver hello servizio viene eliminato correttamente, si riceverà una notifica.
   
    ![Eliminazione del servizio riuscita](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

elenco di Hello dei servizi verrà aggiornato.

 ![Elenco aggiornato dei servizi](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Ottenere una chiave di registrazione del servizio hello
Dopo avere creato un servizio, è necessario tooregister dispositivo StorSimple con servizio hello. tooregister del primo dispositivo StorSimple, si sarà necessario hello chiave di registrazione del servizio. tooregister ulteriori dispositivi con un servizio StorSimple esistente, è necessario sia la chiave di registrazione hello e hello chiave DEK del servizio (che viene generato nel primo dispositivo hello durante la registrazione). Per ulteriori informazioni sulla chiave di crittografia di hello servizio dati, vedere [sicurezza in StorSimple](storsimple-security.md). È possibile ottenere la chiave di registrazione hello accedendo hello **chiavi** pannello per il servizio.

Eseguire hello seguendo i passaggi tooget hello chiave di registrazione.

#### <a name="tooget-hello-service-registration-key"></a>chiave di registrazione del servizio hello tooget
1. In hello **Gestione dispositivi StorSimple** pannello andare troppo**Management &gt;**  **chiavi**.
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. In hello **chiavi** viene visualizzata una chiave di registrazione del servizio di pannello. Chiave di registrazione hello copia utilizzando l'icona di copia hello. 

Mantenere una chiave di registrazione del servizio hello in un luogo sicuro. Sarà necessario questa chiave, nonché hello chiave DEK del servizio, tooregister ulteriori dispositivi con questo servizio. Dopo aver ottenuto una chiave di registrazione del servizio hello, sarà necessario tooconfigure il dispositivo tramite Windows PowerShell hello per l'interfaccia di StorSimple.

## <a name="regenerate-hello-service-registration-key"></a>Rigenerare la chiave di registrazione del servizio hello
Se si è obbligatorio tooperform rotazione delle chiavi o se l'elenco di hello degli amministratori del servizio è stato modificato, sarà necessario tooregenerate una chiave di registrazione del servizio. Quando si rigenera la chiave hello, nuova chiave hello viene utilizzato solo per registrare i dispositivi successivi. i dispositivi Hello già registrati sono interessati da questo processo.

Eseguire hello seguendo i passaggi tooregenerate una chiave di registrazione del servizio.

#### <a name="tooregenerate-hello-service-registration-key"></a>chiave di registrazione del servizio hello tooregenerate
1. In hello **Gestione dispositivi StorSimple** pannello andare troppo**Management &gt;**  **chiavi**.
   
   ![Pannello Chiavi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. In hello **chiavi** pannello, fare clic su **rigenerare**.
   
   ![Fare clic su Rigenera](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. In hello **Rigenera chiave di registrazione** pannello revisione hello azione necessaria per la hello chiavi vengono rigenerate. Tutti i dispositivi successivi hello che sono registrati con questo servizio utilizzerà una nuova chiave di registrazione hello. Fare clic su **rigenerare** tooconfirm. Una volta completata la registrazione di hello si riceverà la notifica.
   
   ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Verrà visualizzata una nuova chiave di registrazione del servizio.
   
    ![Confermare la chiave di rigenerazione](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Copiare la chiave e salvarla per registrare eventuali nuovi dispositivi con il servizio.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[iniziare](storsimple-virtual-array-deploy1-portal-prep.md) con un Array virtuale StorSimple.
* Informazioni su come troppo[amministrare il dispositivo StorSimple](storsimple-ova-web-ui-admin.md).

