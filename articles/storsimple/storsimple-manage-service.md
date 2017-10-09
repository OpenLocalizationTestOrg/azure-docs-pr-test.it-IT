---
title: hello aaaDeploy servizio StorSimple Manager | Documenti Microsoft
description: Viene illustrato come toocreate e delete hello servizio StorSimple Manager nel portale di Azure classico hello e descrive come toomanage hello chiave di registrazione del servizio.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Distribuire il servizio StorSimple Manager hello in hello portale di Azure classico

## <a name="overview"></a>Panoramica
Hello servizio StorSimple Manager in esecuzione in Microsoft Azure e si connette dispositivi StorSimple toomultiple. Dopo aver creato il servizio di hello, è possibile utilizzare i dispositivi di hello toomanage da hello Microsoft Azure classico portale in esecuzione in un browser. In questo modo toomonitor tutti i dispositivi che sono connesso toohello StorSimple Manager hello del servizio da un'unica posizione centrale, riducendo così al minimo carico amministrativo.

pagina di destinazione di StorSimple Manager Hello Elenca tutti i servizi StorSimple Manager hello, che è possibile utilizzare toomanage i dispositivi di archiviazione StorSimple. Per ogni servizio StorSimple Manager, hello le seguenti informazioni verrà visualizzata nella pagina di StorSimple Manager hello:

* **Nome** – nome hello assegnato al servizio StorSimple Manager tooyour quando è stata creata. **Impossibile modificare il nome del servizio Hello dopo aver creato il servizio di hello. Questo vale anche per altre entità, ad esempio i dispositivi, volumi, contenitori di volumi e criteri di backup che non possono essere rinominati in hello portale di Azure classico.**
* **Stato** : hello lo stato del servizio di hello, che può essere **Active**, **creazione**, o **Online**.
* **Percorso** : hello posizione geografica in cui hello StorSimple dispositivo verrà distribuito.
* **Sottoscrizione** : hello sottoscrizione a cui è associato al servizio di fatturazione.

attività comuni di Hello che possono essere eseguite tramite una pagina di hello StorSimple Manager sono:

* Creare un servizio
* Eliminare un servizio
* Ottenere una chiave di registrazione del servizio hello
* Rigenerare la chiave di registrazione del servizio hello

Questa esercitazione viene descritto come tooperform di queste attività.

## <a name="create-a-service"></a>Creare un servizio
Hello utilizzare **creazione rapida** opzione toocreate un servizio StorSimple Manager se si desidera toodeploy dispositivo StorSimple. toocreate un servizio, è necessario toohave:

* Una sottoscrizione con un contratto Enterprise Agreement
* Un account di archiviazione di Microsoft Azure attivo
* le informazioni di fatturazione che viene utilizzate per la gestione accessi Hello

È inoltre possibile toogenerate un account di archiviazione predefinito quando si crea il servizio di hello.

Un singolo servizio può gestire più dispositivi, ma un dispositivo non può estendersi a più servizi. Una grande organizzazione può avere più toowork di istanze di servizio con diverse sottoscrizioni, organizzazioni o anche percorsi di distribuzione. Si noti che è necessario separare le istanze di dispositivi della serie StorSimple 8000 toomanage servizio StorSimple Manager e le matrici virtuale StorSimple.

> [!IMPORTANT] 
> Se si dispone di un servizio inutilizzato creato (dispositivo non sono state eseguite operazioni su questa risorsa) precedenti tooAugust 2016, non può essere gestito tramite il portale di Azure o un portale di Azure classico. È consigliabile creare un nuovo servizio nel portale di Azure hello.

Eseguire hello seguendo i passaggi toocreate un servizio.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminare un servizio
Prima di eliminare un servizio, verificare che non sia usato da dispositivi connessi. Se il servizio di hello è in uso, disattivare i dispositivi connesso hello. operazione di disattivazione Hello dividere hello connessione tra il dispositivo di hello e servizio hello, ma conservare i dati del dispositivo hello nel cloud hello.

> [!IMPORTANT] 
> Dopo l'eliminazione di un servizio, operazione hello non può essere annullata. Qualsiasi dispositivo che utilizza il servizio hello sarà necessario toobe delle impostazioni di fabbrica prima che possa essere usato con un altro servizio. In questo scenario, i dati locali di hello sul dispositivo hello, nonché la configurazione di hello, andranno persi.

Eseguire hello seguendo i passaggi toodelete un servizio.

### <a name="toodelete-a-service"></a>toodelete un servizio
1. In hello **servizio StorSimple Manager** pagina servizio selezionare hello che si desidera toodelete.
2. Fare clic su **eliminare** nella parte inferiore di hello della pagina hello.
3. Fare clic su **Sì** nella notifica di conferma hello. Potrebbe richiedere alcuni minuti per hello servizio toobe eliminato.

## <a name="get-hello-service-registration-key"></a>Ottenere una chiave di registrazione del servizio hello
Dopo avere creato un servizio, è necessario tooregister dispositivo StorSimple con servizio hello. tooregister del primo dispositivo StorSimple, si sarà necessario hello chiave di registrazione del servizio. tooregister ulteriori dispositivi con un servizio StorSimple esistente, è necessario sia la chiave di registrazione hello e hello chiave DEK del servizio (che viene generato nel primo dispositivo hello durante la registrazione). Per ulteriori informazioni sulla chiave di crittografia di hello servizio dati, vedere [sicurezza in StorSimple](storsimple-security.md). È possibile ottenere la chiave di registrazione hello accedendo **chiave di registrazione** su hello **servizi** pagina.

Eseguire hello seguendo i passaggi tooget hello chiave di registrazione.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Mantenere una chiave di registrazione del servizio hello in un luogo sicuro. Sarà necessario questa chiave, nonché hello chiave DEK del servizio, tooregister ulteriori dispositivi con questo servizio. Dopo aver ottenuto una chiave di registrazione del servizio hello, sarà necessario tooconfigure il dispositivo tramite Windows PowerShell hello per l'interfaccia di StorSimple.

Per informazioni dettagliate su come toouse questa chiave, vedere registrazione [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Rigenerare la chiave di registrazione del servizio hello
Se si è obbligatorio tooperform rotazione delle chiavi o se l'elenco di hello degli amministratori del servizio è stato modificato, sarà necessario tooregenerate una chiave di registrazione del servizio. Quando si rigenera la chiave hello, nuova chiave hello viene utilizzato solo per registrare i dispositivi successivi. i dispositivi Hello già registrati sono interessati da questo processo.

Eseguire hello seguendo i passaggi tooregenerate una chiave di registrazione del servizio.

### <a name="tooregenerate-hello-service-registration-key"></a>chiave di registrazione del servizio hello tooregenerate
1. In hello **servizio StorSimple Manager** pagina, fare clic su **chiave di registrazione**.
2. In hello **chiave di registrazione del servizio** la finestra di dialogo, fare clic su **rigenerare**.
3. Verrà visualizzato un messaggio di conferma. Fare clic su **OK** toocontinue con rigenerazione hello.
4. Verrà visualizzata una nuova chiave di registrazione del servizio.
5. Copiare la chiave e salvarla per registrare eventuali nuovi dispositivi con il servizio.
6. Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose questa finestra di dialogo.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [il processo di distribuzione di StorSimple](storsimple-deployment-walkthrough-u2.md).
* Ulteriori informazioni sulla [gestione dell'account di archiviazione di StorSimple](storsimple-manage-storage-accounts.md).
* Per ulteriori informazioni su troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).
