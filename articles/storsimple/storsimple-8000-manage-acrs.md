---
title: record di controllo di accesso aaaManage in StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toouse registra toodetermine (ACR) quali host possono connettersi tooa volume nel dispositivo StorSimple hello.
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Utilizzare i record di controllo accesso toomanage servizio StorSimple Manager hello

## <a name="overview"></a>Panoramica
Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi tooa volume nel dispositivo StorSimple hello. ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello. Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello che ACR associata a tale volume nome IQN hello e, se viene trovata una corrispondenza, hello connessione. record di controllo di accesso in hello Hello **configurazione** sezione del Pannello di servizio gestione di dispositivi StorSimple visualizzare tutti i record di controllo di accesso hello con hello nomi iqn degli host hello corrispondente.

In questa esercitazione illustra hello attività comuni correlate ai record di seguito:

* Aggiungere un record di controllo di accesso
* Modificare un record di controllo di accesso
* Eliminare un record di controllo di accesso

> [!IMPORTANT]
> * Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.
> * Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.

## <a name="get-hello-iqn"></a>Ottenere hello IQN

Eseguire hello seguendo i passaggi tooget hello nome qualificato iSCSI di un host Windows che esegue Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Aggiungere un record di controllo di accesso
Utilizzare hello **configurazione** sezione nel servizio pannello tooadd ACR di hello dispositivo StorSimple Manager. In genere, un record di controllo di accesso verrà associato a un volume.

Eseguire hello seguendo i passaggi tooadd un record.

#### <a name="tooadd-an-acr"></a>un record tooadd

1. Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.
2. In hello **record di controllo di accesso** pannello, fare clic su **+ Aggiungi ACR**.

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr1.png)

3. In hello **aggiungere ACR** pannello hello i passaggi seguenti:

    1. Fornire un nome per il record di controllo di accesso.
    
    2. Specificare il nome IQN hello dell'host Windows Server in **nome iniziatore (IQN) iSCSI**.

    3. Fare clic su **Aggiungi** toocreate hello ACR.

        ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Hello appena aggiunti che record verrà visualizzato nell'elenco in formato tabulare hello ACR.

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Modificare un record di controllo di accesso
Utilizzare hello **configurazione** sezione nel servizio pannello tooedit ACR di hello dispositivo StorSimple Manager.

> [!NOTE]
> È consigliabile modificare solo i record di controllo di accesso che non sono attualmente in uso. tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.

Eseguire hello seguendo i passaggi tooedit un record.

#### <a name="tooedit-an-access-control-record"></a>tooedit un record di controllo di accesso
1.  Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Nell'elenco tabulare di hello dei record di controllo di accesso di hello, fare clic e selezionare i record che si desidera toomodify hello.

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. In hello **record di controllo di accesso di modifica** pannello, fornire un diverso host tooanother IQN corrispondente.

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Fare clic su **Salva**. Alla richiesta di conferma fare clic su **Sì**. 

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Ricevono una notifica quando viene aggiornata hello ACR. Elenco tabulare Hello aggiorna anche modifica hello tooreflect.

   
## <a name="delete-an-access-control-record"></a>Eliminare un record di controllo di accesso
Utilizzare hello **configurazione** sezione nel servizio pannello toodelete ACR di hello dispositivo StorSimple Manager.

> [!NOTE]
> È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso. toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.

Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un record di controllo di accesso
1.  Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Nell'elenco tabulare di hello dei record di controllo di accesso di hello, fare clic e selezionare i record che si desidera toodelete hello.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Menu di scelta rapida tooinvoke hello e scegliere **eliminare**.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Quando viene richiesta la conferma, esaminare le informazioni di hello e quindi fare clic su **eliminare**.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Ricevono una notifica al termine dell'eliminazione di hello. Elenco tabulare Hello è l'eliminazione di hello tooreflect aggiornato.

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

