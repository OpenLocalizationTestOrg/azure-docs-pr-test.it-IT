---
title: aaaChange le password di StorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toochange servizio di gestione di dispositivi StorSimple le password di amministratore di StorSimple Snapshot Manager e dispositivo.
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
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Utilizzare toochange servizio di gestione di dispositivi StorSimple hello le password di StorSimple

## <a name="overview"></a>Panoramica
portale di Azure Hello **le impostazioni del dispositivo** opzione contiene tutti i parametri di dispositivo hello che è possibile riconfigurare in un dispositivo StorSimple è gestito da un servizio di gestione di dispositivi StorSimple. In questa esercitazione viene illustrato come utilizzare hello **sicurezza** opzione **le impostazioni del dispositivo** toochange all'amministratore del dispositivo o la password di gestione Snapshot StorSimple.

## <a name="change-hello-device-administrator-password"></a>Password amministratore del dispositivo hello modifica
Quando si usa il dispositivo StorSimple hello di Windows PowerShell interfaccia tooaccess, verrà richiesto tooenter una password amministratore del dispositivo. Quando il dispositivo StorSimple prima di hello viene registrato con un servizio, la password di hello predefinito per questa interfaccia è *Password1*. Per sicurezza hello dei dati, si è obbligatorio toochange la password al fine di hello hello del processo di registrazione. È possibile uscire dal processo di registrazione hello senza cambiare la password. Per ulteriori informazioni, vedere [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hello prima impostato tramite l'interfaccia di Windows PowerShell hello durante la registrazione può essere cambiata in un secondo momento tramite hello portale di Azure. Eseguire hello password amministratore del dispositivo hello toochange i passaggi seguenti.

#### <a name="toochange-hello-device-administrator-password"></a>password amministratore del dispositivo hello toochange
1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**.

2. Dall'elenco tabulare di hello delle periferiche, selezionare e fare clic su dispositivo hello cui password intendi toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. In hello **impostazioni** pannello andare troppo**le impostazioni del dispositivo > sicurezza**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. In hello **le impostazioni di sicurezza** pannello, fare clic su **Password** password amministratore del dispositivo toochange hello.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. In hello **Password** pannello, specificare una password amministratore contenente dagli 8 too15 caratteri. password di Hello deve essere una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.

6. Conferma password hello.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

password amministratore del dispositivo Hello dovrebbe ora essere aggiornata. È possibile utilizzare questa interfaccia di Windows PowerShell hello tooaccess password modificata.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Impostare la password di StorSimple Snapshot Manager hello
Software di gestione Snapshot StorSimple risiede nell'host di Windows e consente agli amministratori di backup toomanage del dispositivo StorSimple in forma di hello di locale e gli snapshot cloud.

Quando si configura un dispositivo StorSimple Snapshot Manager, verrà richiesto tooprovide hello tooauthenticate di password e l'indirizzo IP dispositivo del dispositivo di archiviazione.

È possibile impostare o modificare password hello gestione Snapshot StorSimple tramite hello portale di Azure. Eseguire i seguenti passaggi tooset hello o modificare la password di StorSimple Snapshot Manager hello.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>password di StorSimple Snapshot Manager hello tooset
1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**.

2. Dall'elenco tabulare di hello delle periferiche, selezionare e fare clic su dispositivo hello cui si intende tooset o si modifica la password gestione Snapshot StorSimple.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. In hello **impostazioni** pannello andare troppo**le impostazioni del dispositivo > sicurezza**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. In hello **le impostazioni di sicurezza** pannello, fare clic su **Password** tooset o modifica password di StorSimple Snapshot Manager hello.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. In hello **Password** pannello, immettere una password composta da 14 o 15 caratteri. Assicurarsi che la password hello contiene una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.

6. Conferma password hello.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Alla richiesta di conferma fare clic su **Salva** e quindi su **Sì**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

password gestione Snapshot StorSimple Hello dovrebbe ora essere aggiornata.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).
* [Ulteriori informazioni su come modificare la configurazione del dispositivo](storsimple-8000-modify-device-config.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

