---
title: aaaConfigure CHAP per dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come tooconfigure hello Challenge Handshake Authentication Protocol (CHAP) in un dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>Configurare CHAP per il dispositivo StorSimple
In questa esercitazione viene illustrato come tooconfigure CHAP per il dispositivo StorSimple. procedura di Hello descritta in questo articolo si applica 8000 serie tooStorSimple, nonché i dispositivi StorSimple 1200.

CHAP è l'acronimo di Challenge Handshake Authentication Protocol. È uno schema di autenticazione utilizzato dall'identità di hello server toovalidate di client remoti. verifica di Hello si basa su una password condivisa o un segreto. CHAP può essere unidirezionale o bidirezionale (reciproco). CHAP unidirezionale è quando la destinazione hello autentica un iniziatore. CHAP reciproco o inverso, sul hello invece necessario che la destinazione hello autentica l'iniziatore di hello e successivamente hello iniziatore autentica destinazione di hello. È possibile implementare l'autenticazione dell'iniziatore senza autenticazione della destinazione. L’autenticazione della destinazione, tuttavia, può essere implementata solo se viene implementata anche l'autenticazione dell'iniziatore. 

Come procedura consigliata, è consigliabile utilizzare la sicurezza iSCSI tooenhance CHAP.

> [!NOTE]
> Tenere presente che IPSEC non è attualmente supportato in dispositivi StorSimple.
> 
> 

Hello CHAP nel dispositivo StorSimple hello possono essere configurate in hello seguenti modi:

* Autenticazione unidirezionale 
* Autenticazione bidirezionale, reciproca o inversa 

In ognuno di questi casi, il portale di hello per dispositivo hello e il software dell'iniziatore iSCSI di hello server deve toobe configurato. Hello i passaggi dettagliati per questa configurazione sono descritti nella seguente esercitazione hello.

## <a name="unidirectional-or-one-way-authentication"></a>Autenticazione unidirezionale 
Nell'autenticazione unidirezionale la destinazione hello autentica l'iniziatore di hello. Questa autenticazione, è necessario configurare impostazioni dell'iniziatore CHAP di hello nel dispositivo StorSimple hello e hello iSCSI software Initiator in host hello. procedure dettagliate per il dispositivo StorSimple Hello e host di Windows vengono descritte di seguito.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure del dispositivo per l'autenticazione unidirezionale
1. Nel portale di Azure classico, in hello hello **dispositivi** pagina, fare clic su hello **configura** scheda.
   
    ![Iniziatore CHAP](./media/storsimple-configure-chap/IC740943.png)
2. Scorrere verso il basso, in questa pagina in hello **iniziatore CHAP** sezione:
   
   1. Specificare un nome utente per l'iniziatore CHAP.
   2. Specificare una password per l'iniziatore CHAP.
      
    > [!IMPORTANT]
    > nome utente Hello deve contenere meno di 233 caratteri. password CHAP Hello deve essere compreso tra 12 e 16 caratteri. Un nome utente o una password più lungo comporterà un errore di autenticazione sull'host di Windows hello.
   
   3. Conferma password hello.
3. Fare clic su **Salva**. Verrà visualizzato un messaggio di conferma. Fare clic su **OK** modifiche hello toosave.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>server host tooconfigure autenticazione unidirezionale in Windows hello
1. Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.
2. In hello **iniziatore iSCSI-proprietà** finestra, eseguire hello alla procedura seguente:
   
   1. Fare clic su hello **individuazione** scheda.
      
       ![Proprietà iniziatore iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. Fare clic su **Individua portale**.
3. In hello **individua portale destinazione** la finestra di dialogo:
   
   1. Specificare l'indirizzo IP di hello del dispositivo.
   2. Fare clic su **Advanced**.
      
       ![Individua portale destinazione](./media/storsimple-configure-chap/IC740945.png)
4. In hello **impostazioni avanzate** la finestra di dialogo:
   
   1. Seleziona hello **Abilita accesso CHAP** casella di controllo.
   2. In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.
   3. In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.
   4. Fare clic su **OK**.
      
       ![Impostazioni avanzate - Generale](./media/storsimple-configure-chap/IC740946.png)
5. In hello **destinazioni** scheda di hello **iniziatore iSCSI-proprietà** , lo stato del dispositivo hello finestra come **connesso**. Se si usa un dispositivo StorSimple 1200, ogni volume verrà montato come destinazione iSCSI, come illustrato di seguito. Di conseguenza, i passaggi 3 e 4, saranno necessario toobe ripetuto per ogni volume.
   
    ![Volumi montati come destinazioni separate](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Se si modifica il nome di iSCSI hello, nuovo nome hello verrà utilizzato per le nuove sessioni iSCSI. Le nuove impostazioni non vengono utilizzate per le sessioni esistenti fino a quando non si esegue la disconnessione e il nuovo accesso.
   > 
   > 

Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Autenticazione bidirezionale o reciproca 
Nell'autenticazione bidirezionale destinazione hello l'autenticazione dell'iniziatore hello e iniziatore hello destinazione hello. Questa operazione richiede le impostazioni dell'iniziatore CHAP hello tooconfigure utente hello, nonché hello reverse impostazioni CHAP nel dispositivo hello e iSCSI software Initiator in host hello. Hello procedure seguenti descrivono l'autenticazione reciproca hello passaggi tooconfigure nel dispositivo di hello e nell'host di Windows hello.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure il dispositivo per l'autenticazione reciproca
1. Nel portale di Azure classico, in hello hello **dispositivi** pagina, fare clic su hello **configura** scheda.
   
    ![Destinazione CHAP](./media/storsimple-configure-chap/IC740948.png)
2. Scorrere verso il basso, in questa pagina in hello **destinazione CHAP** sezione:
   
   1. Fornire un **nome utente per l’autenticazione CHAP inversa** per il dispositivo.
   2. Fornire una **password per l’autenticazione CHAP inversa** per il dispositivo.
   3. Conferma password hello.
3. In hello **iniziatore CHAP** sezione:
   
   1. Specificare un **nome utente** per il dispositivo.
   2. Specificare una **password** per il dispositivo.
   3. Conferma password hello.
4. Fare clic su **Salva**. Verrà visualizzato un messaggio di conferma. Fare clic su **OK** modifiche hello toosave.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>autenticazione bidirezionale tooconfigure in Windows hello server host
1. Nel server host di Windows hello, avviare l'iniziatore iSCSI hello.
2. In hello **iniziatore iSCSI-proprietà** finestra, fare clic su hello **configurazione** scheda.
3. Fare clic su **CHAP**.
4. In hello **segreto autenticazione CHAP reciproca iniziatore iSCSI** la finestra di dialogo:
   
   1. Hello tipo **Password di autenticazione CHAP inversa** configurate nel portale di Azure classico hello.
   2. Fare clic su **OK**.
      
       ![Segreto autenticazione CHAP reciproca iniziatore iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. Fare clic su hello **destinazioni** scheda.
6. Fare clic su hello **Connetti** pulsante. 
7. In hello **connettersi tooTarget** la finestra di dialogo, fare clic su **avanzate**.
8. In hello **proprietà avanzate** la finestra di dialogo:
   
   1. Seleziona hello **Abilita accesso CHAP** casella di controllo.
   2. In hello **nome** campo, specificare hello il nome utente specificato per hello iniziatore CHAP nel portale classico hello.
   3. In hello **segreto destinazione** campo, una password di hello alimentatore specificato per hello iniziatore CHAP nel portale classico hello.
   4. Seleziona hello **Esegui autenticazione reciproca** casella di controllo.
      
       ![Impostazioni avanzate - Autenticazione reciproca](./media/storsimple-configure-chap/IC740950.png)
   5. Fare clic su **OK** configurazione di CHAP hello toocomplete

Per ulteriori informazioni sulla configurazione dell'autenticazione CHAP nel server host di Windows hello, andare troppo[considerazioni aggiuntive](#additional-considerations).

## <a name="additional-considerations"></a>Considerazioni aggiuntive
Hello **connessione rapida** funzionalità non supporta le connessioni con CHAP abilitato. Quando è abilitata l'autenticazione CHAP, assicurarsi di utilizzare hello **Connetti** pulsante è disponibile in hello **destinazioni** destinazione tooa tooconnect di scheda.

![Connettersi tootarget](./media/storsimple-configure-chap/IC740947.png)

In hello **connettersi tooTarget** la finestra di dialogo che è disponibile, seleziona hello **aggiungere questo elenco toohello connessione destinazioni preferite** casella di controllo. In questo modo si garantisce che ogni riavvio del computer hello, viene effettuato un tentativo toorestore hello connessione toohello iSCSI alle destinazioni preferite.

## <a name="errors-during-configuration"></a>Errori durante la configurazione
Se la configurazione CHAP non è corretta, quindi si è probabilmente toosee un **errore di autenticazione** messaggio di errore.

## <a name="verification-of-chap-configuration"></a>Verifica della configurazione di CHAP
È possibile verificare che sia in uso dell'autenticazione CHAP completando hello alla procedura seguente.

#### <a name="tooverify-your-chap-configuration"></a>tooverify la configurazione CHAP
1. Fare clic su **Destinazioni preferite**.
2. Selezionare hello di destinazione per cui è abilitata l'autenticazione.
3. Fare clic su **Dettagli**.
   
    ![Proprietà iniziatore iSCSI - Destinazioni preferite](./media/storsimple-configure-chap/IC740951.png)
4. In hello **dettagli destinazione preferita** nella finestra di dialogo immissione hello nota in hello **autenticazione** campo. Se la configurazione hello ha esito positivo, dovrebbe essere visualizzato **CHAP**.
   
    ![Dettagli destinazione preferita](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-security.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

