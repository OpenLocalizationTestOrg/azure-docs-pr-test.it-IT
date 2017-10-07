---
title: record di controllo di accesso aaaManage per Array virtuale StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toomanage registra toodetermine (ACR) quali host possono connettersi volume tooa hello Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Utilizzare Gestione periferiche di StorSimple toomanage record di controllo di accesso per Array virtuale StorSimple

## <a name="overview"></a>Panoramica

Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi volume tooa hello Array virtuale StorSimple (noto anche come hello StorSimple nel dispositivo virtuale locale). ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello. Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello ACR associata a tale volume per il nome IQN hello e se viene trovata una corrispondenza, viene stabilita la connessione hello. Hello **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione del servizio di gestione dispositivi consente di visualizzare tutti i record di controllo di accesso hello con hello nomi iqn degli host hello corrispondente.

![Gestire record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

In questa esercitazione illustra hello attività comuni correlate ai record di seguito:

* Ottenere hello IQN
* Aggiungere un record di controllo di accesso
* Modificare un record di controllo di accesso
* Eliminare un record di controllo di accesso

> [!IMPORTANT]
> 
> * Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.
> * Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.


## <a name="get-hello-iqn"></a>Ottenere hello IQN

Eseguire hello seguendo i passaggi tooget hello nome qualificato iSCSI di un host Windows che esegue Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Aggiungere un record di controllo di accesso

Utilizzare **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione tooadd di servizio ACR il dispositivo StorSimple Manager. In genere, a un volume viene associato un record di controllo di accesso.

Per informazioni sull'associazione di un record con un volume, andare troppo[aggiungere un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.


Eseguire hello seguendo i passaggi tooadd un record.

#### <a name="tooadd-an-acr"></a>un record tooadd

1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.
2. In hello **record di controllo di accesso** pannello, fare clic su **Aggiungi**.
3. In hello **aggiungere ACR** pannello hello seguenti:
   
    1. Fornire un **Nome** per l'ACR.
    
    2. In **nome iniziatore iSCSI**, fornire il nome IQN hello dell'host Windows. hello tooget hello IQN dell'host, Windows Server seguenti:
   
    3. Avviare l'iniziatore iSCSI Microsoft di hello nell'host di Windows. Nella finestra Proprietà iniziatore iSCSI di hello, su hello **configurazione** , selezionare e copiare la stringa hello hello **nome iniziatore** campo.
    Incollare la stringa hello **IQN** campo hello **aggiungere ACR** blade.
   
    6. Fare clic su **Aggiungi** tooadd hello ACR.  
   
        ![Aggiungere record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Elenco tabulare Hello viene aggiornato tooreflect questa aggiunta.

## <a name="edit-an-acr"></a>Modificare un record di controllo di accesso

Utilizzare hello **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione del servizio di Gestione periferiche in hello ACR tooedit portale Azure.

> [!NOTE]
> Non è opportuno modificare un record di controllo di accesso attualmente in uso. tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.


Eseguire hello seguendo i passaggi tooedit un record.

#### <a name="tooedit-an-acr"></a>un record tooedit

1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** sezione **record di controllo di accesso**.
2. In hello **record di controllo di accesso** pannello, dall'elenco in formato tabulare hello dei record di controllo di accesso hello, fare doppio clic sul record che si desidera toomodify hello.
3. In hello **record di controllo di accesso di modifica** pannello hello seguenti:
   
    1. Alimentatore hello IQN per hello ACR.
   
    2. Fare clic su **salvare** nella parte superiore di hello di hello pannello toosave hello modificato ACR. Vedrai hello messaggio di conferma seguente:
   
        ![Modificare i record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Eliminare un record di controllo di accesso

Utilizzare hello **configurazione** pagina hello ACR toodelete portale Azure.

> [!NOTE]
> 
> * Non è opportuno eliminare un record di controllo di accesso attualmente in uso. toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.
> * Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.


Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un record di controllo di accesso

1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** sezione **record di controllo di accesso**.

2. In hello **record di controllo di accesso** pannello, dall'elenco in formato tabulare hello dei record di controllo di accesso hello, fare doppio clic sul record che si desidera toodelete hello.

3. Nel Pannello di hello Modifica accesso controllo record, fare clic su **eliminare**.
   
    ![Eliminare record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Quando viene richiesta la conferma, fare clic su **eliminare** toocontinue con l'eliminazione di hello. Elenco tabulare Hello è l'eliminazione di hello tooreflect aggiornato.
   
   ![Messaggio di avviso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sull' [aggiunta di volumi e la configurazione di record di controllo di accesso](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

