---
title: le password aaaChange tramite Gestione dispositivi StorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toochange servizio StorSimple Manager le password di amministratore di StorSimple Snapshot Manager e dispositivo.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Utilizzare toochange servizio StorSimple Manager di hello le password di StorSimple
## <a name="overview"></a>Panoramica
portale di Azure classico Hello **configura** pagina contiene tutti i parametri di dispositivo hello che è possibile riconfigurare in un dispositivo StorSimple è gestito da un servizio StorSimple Manager. In questa esercitazione viene illustrato come utilizzare hello **configura** pagina toochange all'amministratore del dispositivo o la password di gestione Snapshot StorSimple.

## <a name="change-hello-device-administrator-password"></a>Password amministratore del dispositivo hello modifica
Quando si usa il dispositivo StorSimple hello di Windows PowerShell interfaccia tooaccess, verrà richiesto tooenter una password amministratore del dispositivo. Quando il dispositivo StorSimple prima di hello viene registrato con un servizio, la password di hello predefinito per questa interfaccia è *Password1*. Per sicurezza hello dei dati, si è obbligatorio toochange la password al fine di hello hello del processo di registrazione. È possibile uscire dal processo di registrazione hello senza cambiare la password. Per ulteriori informazioni, vedere [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

password Hello prima impostato tramite l'interfaccia di Windows PowerShell hello durante la registrazione può quindi essere modificata tramite hello portale di Azure classico. Eseguire hello password amministratore del dispositivo hello toochange i passaggi seguenti.

#### <a name="toochange-hello-device-administrator-password"></a>password amministratore del dispositivo hello toochange
1. Nel portale classico hello, fare clic su **dispositivi** > **configura** per il dispositivo.
2. Scorrere verso il basso toohello **Password amministratore del dispositivo** sezione. Specificare una password amministratore contenente dagli 8 too15 caratteri. password di Hello deve essere una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.
3. Conferma password hello.
4. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

password amministratore del dispositivo Hello dovrebbe ora essere aggiornata. È possibile utilizzare questa interfaccia di Windows PowerShell hello tooaccess password modificata.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Modificare la password di StorSimple Snapshot Manager hello
Software di gestione Snapshot StorSimple risiede nell'host di Windows e consente agli amministratori di backup toomanage del dispositivo StorSimple in forma di hello di locale e gli snapshot cloud.

Quando si configura un dispositivo StorSimple Snapshot Manager, verrà richiesto tooprovide hello tooauthenticate di password e l'indirizzo IP dispositivo del dispositivo di archiviazione. Questa password viene prima configurata tramite l'interfaccia di Windows PowerShell hello. Per ulteriori informazioni, vedere [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hello prima impostato tramite l'interfaccia di Windows PowerShell hello durante la registrazione può quindi essere cambiata tramite il portale classico di hello. Eseguire hello password gestione Snapshot StorSimple hello toochange di passaggi seguenti.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>password di StorSimple Snapshot Manager hello toochange
1. Nel portale classico hello, fare clic su **dispositivi** > **configura** per il dispositivo.
2. Scorrere verso il basso toohello **gestione Snapshot StorSimple** sezione. Immettere una password composta da 14 o 15 caratteri. Assicurarsi che la password hello contiene una combinazione di 3 o più dei caratteri maiuscoli, minuscoli, numerici e speciali.
3. Conferma password hello.
4. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

password gestione Snapshot StorSimple Hello dovrebbe ora essere aggiornata.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-security.md).
* [Ulteriori informazioni su come modificare la configurazione del dispositivo](storsimple-modify-device-config.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

