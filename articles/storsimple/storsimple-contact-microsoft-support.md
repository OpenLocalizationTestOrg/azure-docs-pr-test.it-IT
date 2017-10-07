---
title: ticket di supporto per StorSimple serie 8000 aaaLog | Documenti Microsoft
description: Informazioni su come toocreate un supporto richiesta e avviare una sessione di supporto nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Contattare il supporto tecnico Microsoft per il dispositivo StorSimple in uso
Se si verificano problemi con la soluzione Microsoft Azure StorSimple, è possibile creare una richiesta di servizio per il supporto tecnico. In una sessione in linea con il tecnico del supporto, è necessario anche toostart una sessione di supporto nel dispositivo StorSimple. In questo articolo viene descritto:

* Come richiedere toocreate un supporto.
* Toostart una sessione di supporto nella hello come interfaccia di Windows PowerShell del dispositivo StorSimple.

Hello revisione [StorSimple 8000 Series supporto SLA e le informazioni](https://msdn.microsoft.com/library/mt433077.aspx) prima di creare una richiesta di supporto.

## <a name="create-a-support-request"></a>Creare una richiesta di supporto
Eseguire hello seguendo i passaggi toocreate una richiesta di supporto:

#### <a name="toocreate-a-support-request"></a>toocreate una richiesta di supporto
1. In hello [portale di Azure classico](https://manage.windowsazure.com/), hello angolo superiore destro, scegliere il nome di account e quindi fare clic su **contattare il supporto tecnico Microsoft**.
   
    ![Contattare il supporto tecnico Microsoft tramite il portale di gestione](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Sarà reindirizzato toohello nuovo portale di Azure (portal.azure.com). Fare clic su hello **nuova richiesta di assistenza** riquadro.
   
    ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Sul lato destro di hello della schermata ciao, hello **nuova richiesta di assistenza** verrà visualizzato il riquadro. 
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. In hello **nozioni di base** della finestra di dialogo hello completo seguente:                                
   
   1. Da hello **rilascio tipo** elenco a discesa, seleziona **tecniche**.
   2. Selezionare un **sottoscrizione** dall'elenco a discesa hello.
   3. Da hello **servizio** elenco a discesa, seleziona **StorSimple**. 
   4. Selezionare un **piano di supporto** dall'elenco a discesa hello. È necessario un tooenable piano di supporto a pagamento il supporto tecnico.
4. Fare clic su **Avanti**. Hello **problema** viene visualizzata la finestra di dialogo.
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. In hello **problema** della finestra di dialogo hello completo seguente:
   
   1. Selezionare un **gravità** livello dall'elenco a discesa hello.
   2. Selezionare un **tipo di problema** dall'elenco a discesa hello.
   3. Selezionare un **categoria** dall'elenco a discesa hello. 
   4. In hello **dettagli** casella, una breve descrizione del problema.
   5. In hello **tempo** casella, indicare hello data, ora e fuso orario corrispondente toohello occorrenza più recente del problema.
   6. In **caricamento del File**, fare clic su hello cartella icona toobrowse tooyour pacchetto per il supporto.
   7. Seleziona hello **condividere le informazioni di diagnostica** casella di controllo.
6. Fare clic su **Avanti**. Hello **le informazioni di contatto** viene visualizzata la finestra di dialogo.
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Immettere le informazioni di contatto e selezionare un metodo di contatto (telefono o posta elettronica). 
8. Seleziona hello **Salva le modifiche di contatto per le richieste di supporto futuro** casella di controllo.
9. Fare clic su **Crea**.

Dopo l'invio della richiesta, un tecnico del supporto contatterà l'utente appena possibile tooproceed con la richiesta.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Avviare una sessione di supporto in Windows PowerShell per StorSimple
tootroubleshoot eventuali problemi che potrebbero verificarsi con il dispositivo di StorSimple hello, sarà necessario tooengage con il team di supporto Microsoft hello. Supporto Microsoft potrebbe essere necessario un toolog di sessione di supporto nel dispositivo tooyour toouse. 

Eseguire l'esempio hello passaggi toostart una sessione di supporto:

#### <a name="toostart-a-support-session"></a>toostart una sessione di supporto
1. Hello dispositivo per l'accesso direttamente tramite la console seriale hello o tramite una sessione telnet da un computer remoto. toodo, seguire la procedura seguente hello in [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Nella sessione hello aperta, premere hello **invio** chiave tooget un prompt dei comandi.
3. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.
4. Al prompt dei comandi hello, digitare hello seguenti password: 
   
    `Password1`
5. Al prompt dei comandi hello, digitare hello comando seguente:
   
    `Enable-HcsSupportAccess`
6. Verrà visualizzata una stringa crittografata tooyou. Copiare la stringa in un editor di testo, ad esempio Blocco note.
7. Salvare la stringa e inviarla in un tooMicrosoft messaggio di posta elettronica supporto. 

> [!IMPORTANT]
> È possibile disabilitare l'accesso del supporto eseguendo `Disable-HcsSupportAccess`. dispositivo StorSimple Hello tenterà anche accesso al supporto toodisable 8 ore dopo l'avvio della sessione hello. È una migliore toochange pratica le credenziali del dispositivo StorSimple dopo l'avvio di una sessione di supporto.
> 
> 

