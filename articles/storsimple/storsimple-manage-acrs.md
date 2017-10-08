---
title: record di controllo di accesso aaaManage in StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toouse registra toodetermine (ACR) quali host possono connettersi tooa volume nel dispositivo StorSimple hello.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Utilizzare i record di controllo accesso toomanage servizio StorSimple Manager hello
## <a name="overview"></a>Panoramica
Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi tooa volume nel dispositivo StorSimple hello. ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello. Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello che ACR associata a tale volume nome IQN hello e, se viene trovata una corrispondenza, hello connessione. sezione in hello dei record di controllo di accesso Hello **configura** pagina siano presenti tutti i record di controllo di accesso hello hello nomi iqn degli host hello corrispondente.

In questa esercitazione illustra hello attività comuni correlate ai record di seguito:

* Aggiungere un record di controllo di accesso 
* Modificare un record di controllo di accesso 
* Eliminare un record di controllo di accesso 

> [!IMPORTANT]
> * Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello. 
> * Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.
> 
> 

## <a name="add-an-access-control-record"></a>Aggiungere un record di controllo di accesso
Utilizzare un servizio StorSimple Manager hello **configura** pagina ACR tooadd. In genere, un record di controllo di accesso verrà associato a un volume.

Eseguire hello seguendo i passaggi tooadd un record.

#### <a name="tooadd-an-access-control-record"></a>tooadd un record di controllo di accesso
1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.
2. In hello tabulare visualizzata in **record di controllo di accesso**, fornire un **nome** del record.
3. Specificare il nome IQN hello dell'host di Windows in **nome iniziatore iSCSI**. hello tooget hello IQN dell'host, Windows Server seguenti:
   
   * Avviare l'iniziatore iSCSI Microsoft di hello nell'host di Windows.
   * In hello **iniziatore iSCSI-proprietà** finestra hello **configurazione** , selezionare e copiare la stringa hello hello **nome iniziatore** campo.
   * Incollare la stringa hello **nome iniziatore iSCSI** campo nella tabella ACR hello hello portale di Azure classico.
4. Fare clic su **salvare** hello toosave nuovi record. Hello tabulare elenco verrà aggiornato tooreflect di essere aggiunta.

## <a name="edit-an-access-control-record"></a>Modificare un record di controllo di accesso
Utilizzare hello **configura** pagina hello ACR Azure tooedit portale classico. 

> [!NOTE]
> È possibile modificare solo i record di controllo di acceso che non sono attualmente in uso. tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.
> 
> 

Eseguire hello seguendo i passaggi tooedit un record.

#### <a name="tooedit-an-access-control-record"></a>tooedit un record di controllo di accesso
1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.
2. Nell'elenco tabulare di hello dei record di controllo di accesso di hello, passare il mouse sul record che si desidera toomodify hello.
3. Specificare un nuovo nome e/o il nome IQN hello ACR.
4. Fare clic su **salvare** toosave hello modificato ACR. Hello tabulare elenco verrà aggiornato tooreflect di essere questa modifica.

## <a name="delete-an-access-control-record"></a>Eliminare un record di controllo di accesso
Utilizzare hello **configura** pagina hello ACR Azure toodelete portale classico. 

> [!NOTE]
> È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso. toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.
> 
> 

Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un record di controllo di accesso
1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.
2. Nell'elenco tabulare di hello dei record di controllo di accesso hello (ACR), passare il mouse sul record che si desidera toodelete hello.
3. Un'icona di eliminazione (**x**) verrà visualizzato nella colonna destra estrema hello per hello record selezionato. Fare clic su hello **x** hello toodelete icona record.
4. Quando viene richiesta la conferma, fare clic su **Sì** toocontinue con l'eliminazione di hello. Elenco tabulare Hello sarà aggiornata tooreflect hello eliminazione.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

