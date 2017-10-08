---
title: dispositivi aaaManage con StorSimple Snapshot Manager | Documenti Microsoft
description: Viene descritto come toouse hello tooconnect snap-in MMC di StorSimple Snapshot Manager e gestire i dispositivi StorSimple.
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Utilizzare Gestione Snapshot StorSimple tooconnect e gestire i dispositivi StorSimple
## <a name="overview"></a>Panoramica
È possibile utilizzare i nodi in Gestione Snapshot StorSimple hello **ambito** riquadro tooverify importati i dati del dispositivo StorSimple e aggiornare i dispositivi di archiviazione connesso. Inoltre, quando si fa clic su hello **dispositivi** nodo, è possibile visualizzare un elenco di dispositivi connessi e le informazioni sullo stato corrispondenti in hello **risultati** riquadro.

![Dispositivi connessi](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Figura 1: Dispositivo di Gestione snapshot StorSimple connesso** 

A seconda del **vista** selezioni, hello **risultati** riquadro vengono visualizzate le seguenti informazioni su ogni dispositivo hello. (Per ulteriori informazioni sulla configurazione di una vista, visitare troppo[dal menu Visualizza](storsimple-use-snapshot-manager.md#view-menu).

| Colonna risultati | Descrizione |
|:--- |:--- |
| Nome |nome Hello del dispositivo hello configurato nel portale di Azure classico hello |
| Modello |numero di dispositivi hello modello Hello |
| Versione |versione di Hello di hello installata nel dispositivo hello |
| Stato |Se il dispositivo hello è disponibile |
| Ultima sincronizzazione |Data e ora dell'ultima sincronizzazione dispositivo hello |
| N. di serie |numero di serie Hello per dispositivo hello |

Se si fa clic su hello **dispositivi** nodo hello **ambito** , è possibile selezionare da hello seguenti azioni:

* Aggiunta o sostituzione di un dispositivo
* Connessione di un dispositivo e verifica delle importazioni
* Aggiornamento dei dispositivi connessi

Se si fa clic hello **dispositivi** nodo e quindi fare un dispositivo il nome in hello **risultati** , è possibile selezionare da hello seguenti azioni:

* Autenticazione di un dispositivo
* Visualizzazione dei dettagli del dispositivo
* Aggiornamento di un dispositivo
* Eliminazione della configurazione di un dispositivo
* Modifica della password di un dispositivo

> [!NOTE]
> Tutte queste azioni sono disponibili anche in hello **azioni** riquadro.


In questa esercitazione viene illustrato come toouse tooconnect gestione Snapshot StorSimple e gestire i dispositivi e di eseguire hello seguenti attività:

* Aggiunta o sostituzione di un dispositivo
* Connessione di un dispositivo e verifica delle importazioni
* Aggiornamento dei dispositivi connessi
* Autenticazione di un dispositivo
* Visualizzazione dei dettagli del dispositivo
* Aggiornamento di un singolo dispositivo
* Eliminazione della configurazione di un dispositivo
* Modifica della password scaduta di un dispositivo
* Sostituzione di un dispositivo guasto

> [!NOTE]
> Per informazioni generali sull'utilizzo di interfaccia di gestione Snapshot StorSimple hello, andare troppo[interfaccia utente di gestione Snapshot StorSimple](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Aggiunta o sostituzione di un dispositivo
Utilizzare hello seguendo procedure tooadd o sostituire un dispositivo StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd o sostituire un dispositivo
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, hello rapida **dispositivi** nodo e quindi fare clic su **configurare un dispositivo**. Hello **configurare un dispositivo** viene visualizzata la finestra di dialogo.
   
    ![Configurazione di un dispositivo StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. In hello **dispositivo** casella di riepilogo a discesa, indirizzo IP selezionare hello di hello o del dispositivo virtuale. 
4. In hello **Password** casella di testo, la password di StorSimple Snapshot Manager hello tipo creati per il dispositivo hello nel portale di Azure classico hello. Fare clic su **OK**. Gestione Snapshot StorSimple Cerca dispositivi hello identificato. 
   
   * Se il dispositivo hello è disponibile, gestione Snapshot StorSimple aggiunge una connessione.
   * Se il dispositivo hello è disponibile per qualsiasi motivo, gestione Snapshot StorSimple restituisce un messaggio di errore. Fare clic su **OK** tooclose hello messaggio di errore e quindi fare clic su **Annulla** tooclose hello **configurare un dispositivo** la finestra di dialogo.

## <a name="connect-a-device-and-verify-imports"></a>Connessione di un dispositivo e verifica delle importazioni
Utilizzare hello seguendo procedure tooconnect un dispositivo StorSimple e verificare che eventuali gruppi di volumi esistenti con backup associati vengano importati.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect un dispositivo e verificare le importazioni
1. tooconnect tooStorSimple un dispositivo Manager di Snapshot, seguire le istruzioni hello aggiungere o sostituire un dispositivo. Quando si connette il dispositivo tooa, gestione Snapshot StorSimple risponde come segue:
   
   * Se il dispositivo hello è disponibile per qualsiasi motivo, gestione Snapshot StorSimple restituisce un messaggio di errore. 
   
   * Se il dispositivo hello è disponibile, gestione Snapshot StorSimple aggiunge una connessione. Quando si seleziona dispositivo hello, viene visualizzata in hello **risultati** riquadro e hello campo di stato indica che il dispositivo hello **disponibile**. Gestione Snapshot StorSimple Importa i gruppi di volumi configurati per il dispositivo di hello, purché hello volume gruppi abbiano backup associati. I criteri di backup non vengono importati. I gruppi di volumi che non dispongono di backup associati non vengono importati.
2. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
3. Nodo principale di hello pulsante destro del mouse in hello **ambito** riquadro e quindi fare clic su **Visualizza/Nascondi importazioni**.
   
    ![Selezione di Visualizza/Nascondi importazioni](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Hello **Visualizza/Nascondi importazioni** viene visualizzata la finestra di dialogo, con stato hello di hello importare gruppi di volumi. Fare clic su **OK**.

Dopo che sono state importate hello gruppi di volumi, è possibile utilizzare Gestione Snapshot StorSimple toomanage loro, proprio come gestione di gruppi di volumi creati e configurati con gestione Snapshot StorSimple. 

## <a name="refresh-connected-devices"></a>Aggiornamento dei dispositivi connessi
Utilizzare hello seguendo procedure toosynchronize hello connesso i dispositivi StorSimple con StorSimple Snapshot Manager.

#### <a name="toorefresh-connected-devices"></a>i dispositivi connessi toorefresh
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro destro **dispositivi**, quindi fare clic su **Aggiorna dispositivi**. Questo consente di sincronizzare i dispositivi connesso hello con StorSimple Snapshot Manager in modo che è possibile visualizzare hello gruppi di volumi, incluse tutte le aggiunte recenti. 
   
    ![Aggiornare i dispositivi StorSimple hello](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Hello **Aggiorna dispositivi** azione recupera eventuali nuovi gruppi di volumi e i backup associati dai dispositivi connessi. A differenza di hello **Ripeti analisi dei volumi** azione disponibile per hello **volumi** nodo **Aggiorna dispositivi** Ripristina backup Registro di sistema hello.

## <a name="authenticate-a-device"></a>Autenticazione di un dispositivo
Utilizzare hello seguendo procedure tooauthenticate un dispositivo StorSimple con StorSimple Snapshot Manager.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate un dispositivo
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su **dispositivi**.
3. In hello **risultati** riquadro, fare doppio clic su nome hello del dispositivo di hello e quindi fare clic su **Authenticate**.
4. Hello **Authenticate** viene visualizzata la finestra di dialogo. Digitare una password del dispositivo hello e quindi fare clic su **OK**.
   
    ![Finestra di dialogo Autentica](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Visualizzazione dei dettagli del dispositivo
Utilizzare hello seguenti procedure tooview hello dettagli di un dispositivo StorSimple e, se necessario, risincronizzare dispositivo hello StorSimple Snapshot Manager.

#### <a name="tooview-and-resynchronize-device-details"></a>tooview e risincronizzare i dettagli dispositivo
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su **dispositivi**.
3. In hello **risultati** riquadro, fare doppio clic su nome hello del dispositivo di hello e quindi fare clic su **dettagli**.

4 hello **dettagli dispositivo** viene visualizzata la finestra di dialogo. Questa casella viene visualizzato il nome di hello, modello, versione, il numero di serie, stato, destinazione iSCSI nome qualificato, ultimo di sincronizzazione data e ora.

* Fare clic su **Resync** dispositivo hello toosynchronize.
* Fare clic su **OK** o **Annulla** tooclose hello finestra di dialogo.
  
  ![Dettagli dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Aggiornamento di un singolo dispositivo
Utilizzare hello seguendo procedure tooresynchronize un singolo dispositivo StorSimple con StorSimple Snapshot Manager.

#### <a name="toorefresh-a-device"></a>toorefresh un dispositivo
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple. 
2. In hello **ambito** riquadro, fare clic su **dispositivi**. 
3. In hello **risultati** riquadro, fare doppio clic su nome hello del dispositivo di hello e quindi fare clic su **Aggiorna dispositivo**. Dispositivo hello viene sincronizzato con StorSimple Snapshot Manager.

## <a name="delete-a-device-configuration"></a>Eliminazione della configurazione di un dispositivo
Utilizzare hello seguendo procedure toodelete una singola configurazione di dispositivo StorSimple da StorSimple Snapshot Manager.

#### <a name="toodelete-a-device-configuration"></a>configurazione di un dispositivo toodelete
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su **dispositivi**. 
3. In hello **risultati** riquadro, fare doppio clic su nome hello del dispositivo di hello e quindi fare clic su **eliminare**. 
4. verrà visualizzata la seguente messaggio Hello. Fare clic su **Sì** toodelete hello configurazione oppure fare clic su **n** eliminazione hello toocancel.
   
    ![Eliminazione della configurazione del dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Modifica della password scaduta di un dispositivo
È necessario immettere un tooauthenticate password, un dispositivo StorSimple con StorSimple Snapshot Manager. Configurare la password quando si utilizza tooset di interfaccia di Windows PowerShell hello dispositivo hello. Tuttavia, può scadere password hello. In questo caso, è possibile utilizzare una password di hello hello Azure toochange portale classico. Quindi, perché il dispositivo hello è stato configurato in Gestione Snapshot StorSimple prima della scadenza password hello, è necessario autenticare nuovamente il dispositivo di hello in Gestione Snapshot StorSimple.

#### <a name="toochange-hello-expired-password"></a>password scaduta di hello toochange
1. Nel portale di Azure classico hello, avviare il servizio StorSimple Manager hello.
2. Fare clic su **dispositivi** > **configura** per dispositivo hello.
3. Scorrere verso il basso toohello sezione Gestione Snapshot StorSimple. Immettere una password composta da 14-15 caratteri. Assicurarsi che la password hello contiene una combinazione di caratteri maiuscoli, minuscoli, numerici e speciali.
4. Immettere nuovamente tooconfirm password hello è.
5. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.

#### <a name="toore-authenticate-hello-device"></a>toore-autenticare hello dispositivo
1. Avviare Gestione snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su **dispositivi**. Viene visualizzato un elenco di dispositivi configurati in hello **risultati** riquadro.
3. Selezionare il dispositivo di hello, pulsante destro del mouse e quindi fare clic su **Authenticate**.
4. In hello **Authenticate** finestra immettere hello nuova password.
5. Selezionare il dispositivo di hello, pulsante destro del mouse e selezionare **Aggiorna dispositivo**. Dispositivo hello viene sincronizzato con StorSimple Snapshot Manager.

## <a name="replace-a-failed-device"></a>Sostituzione di un dispositivo guasto
Se un dispositivo StorSimple non riesce e viene sostituito da un dispositivo di standby (di failover), utilizzare hello seguendo i passaggi tooconnect visualizzazione e toohello nuovo dispositivo hello backup associati.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa nuovo dispositivo dopo il failover
1. Riconfigurare hello iSCSI connessione toohello nuovo dispositivo. Per istruzioni, vedere troppo "passaggio 7: montaggio, inizializzazione e formato di un volume" in [distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Se il dispositivo StorSimple nuovo hello è hello hello nello stesso indirizzo IP precedente, potrebbe essere in grado di tooconnect la configurazione precedente hello.


1. Interrompi servizio di gestione Microsoft StorSimple hello:
   
   1. Avviare Server Manager.
   2. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   3. In hello **servizi** finestra, seleziona hello **servizio di gestione Microsoft StorSimple**.
   4. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **arrestare servizio hello**.
2. Rimuovi dispositivo toohello correlati di informazioni configurazione hello precedente:
   
   1. In Esplora File passare tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Eliminare i file nella cartella BACatalog hello hello.
3. Riavviare il servizio di gestione di Microsoft StorSimple hello:
   
   1. Nel Dashboard di Server Manager, di hello in hello **strumenti** dal menu **servizi**.
   2. In hello **servizi** finestra, seleziona hello **servizio di gestione Microsoft StorSimple**.
   3. In hello destro in riquadro **servizio di gestione Microsoft StorSimple**, fare clic su **riavviare servizio hello**.
4. Avviare Gestione snapshot StorSimple.
5. la periferica tooconfigure hello nuovo StorSimple, hello completato i passaggi nel passaggio 2: connettere un dispositivo StorSimple in [distribuire StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
6. Nodo di primo livello hello pulsante destro del mouse in hello **ambito** riquadro (gestione Snapshot StorSimple nell'esempio hello) e quindi fare clic su **Visualizza/Nascondi importazioni**. 
7. Viene visualizzato un messaggio hello importata gruppi di volumi e i backup sono visibili in Gestione Snapshot StorSimple. Fare clic su **OK**.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[tooview StorSimple Snapshot Manager di utilizzare e gestire volumi](storsimple-snapshot-manager-manage-volumes.md).

