---
title: password amministratore del dispositivo StorSimple Virtual Array aaaChange | Documenti Microsoft
description: "Viene descritto come toouse hello è il portale di Azure o Array virtuale StorSimple web UI toochange hello password amministratore del dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Modifica password amministratore del dispositivo StorSimple Virtual Array hello tramite Gestione dispositivi StorSimple

## <a name="overview"></a>Panoramica

Quando si utilizza tooaccess di interfaccia di Windows PowerShell hello hello Array virtuale StorSimple, è necessario tooenter una password amministratore del dispositivo. Quando il dispositivo StorSimple hello viene innanzitutto effettuato il provisioning e avviata, la password predefinita hello è *Password1*. Per la protezione dei dati hello, scadenza password predefinito di hello hello prima volta che si accede e si è necessari toochange questa password.

È anche possibile utilizzare entrambi hello web locale dell'interfaccia utente o hello toochange portale Azure hello password amministratore del dispositivo in qualsiasi momento dopo hello dispositivo viene distribuito nell'ambiente di produzione. Tutte queste procedure vengono descritte in questo articolo.

 ![pannello Dispositivi](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Usare password di hello hello toochange portale di Azure

Eseguire i seguenti passaggi toochange hello password amministratore del dispositivo tramite il portale di Azure hello hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>password amministratore del dispositivo hello toochange tramite hello portale di Azure

1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **Management** fare clic su **dispositivi**. Verrà visualizzata hello **dispositivi** blade che elenca tutti i dispositivi StorSimple Virtual Array.

2. In hello **dispositivi** pannello, fare doppio clic sul dispositivo di hello che richiede una modifica della password.

3. In hello **impostazioni** pannello per il dispositivo, fare clic su **sicurezza**.

4. In hello **le impostazioni di sicurezza** pannello hello seguenti:
   
   1. Scorrere verso il basso toohello **Password amministratore del dispositivo** sezione. Specificare una password amministratore contenente dagli 8 too15 caratteri.
   2. Conferma password hello.
   3. Fare clic su **salvare** nella parte superiore di hello del pannello hello.

password amministratore del dispositivo Hello è ora aggiornata. È possibile utilizzare il dispositivo di hello tooaccess password modificata in locale.

![Pannello impostazioni di sicurezza](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Utilizzare password hello toochange di hello web locale dell'interfaccia utente

Eseguire i seguenti passaggi toochange hello password amministratore del dispositivo tramite l'interfaccia utente web locale hello hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>password amministratore del dispositivo hello toochange tramite l'interfaccia utente web locale hello

1. In hello interfaccia utente web locale, fare clic su **manutenzione** > **modifica della Password** per il dispositivo.
   
    ![cambiare password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Immettere hello **password corrente**.
3. Fornire una **Nuova password**. password di Hello deve essere composta da almeno 8 caratteri. Deve contenere 3 delle 4 seguenti hello: caratteri maiuscoli, minuscoli, numerici e speciali.
   
    Si noti che la password non può essere hello stesso hello ultime 24 password specificate.
4. Immettere nuovamente tooconfirm password hello è.
   
    ![cambiare password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Nella parte inferiore di hello della pagina hello, fare clic su **applica**. nuova password Hello viene ora applicata. Se la modifica della password hello non ha esito positivo, viene visualizzato il seguente errore hello:
   
    ![errore password](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    Dopo aver completato l'aggiornamento password hello, ricevono la notifica. È quindi possibile utilizzare password modificata tooaccess hello dispositivo localmente.


## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[amministrare l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

