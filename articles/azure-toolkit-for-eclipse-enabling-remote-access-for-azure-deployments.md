---
title: aaaEnabling accesso remoto per le distribuzioni di Azure in Eclipse
description: "Informazioni su modalità di accesso remoto tooenable per distribuzioni di Azure utilizzando hello Azure Toolkit per Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Abilitare l'accesso remoto per le distribuzioni di Azure in Eclipse
toohelp di risolvere i problemi delle distribuzioni, è possibile abilitare e usare accesso remoto tooconnect toohello macchina virtuale che ospita la distribuzione. Hello funzionalità di accesso remoto si basa su hello Remote Desktop Protocol (RDP). È possibile configurare accesso remoto per la distribuzione dopo averlo pubblicato tooAzure o se si usa Eclipse con un sistema operativo Windows, è possibile configurare accesso remoto prima di pubblicare tooAzure. Si noti che è necessario un client desktop remoto compatibile con il sistema operativo nella macchina virtuale della distribuzione di ordine tooconnect tooyour in Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Come tooenable accesso remoto prima di distribuire tooAzure
> [!NOTE]
> Accesso remoto prima di distribuire l'applicazione tooAzure tooenable, è necessario eseguire Eclipse in Windows toobe.
> 
> 

Hello immagine seguente viene illustrato hello **accesso remoto** finestra di dialogo proprietà utilizzato tooenable di accesso remoto.

![][ic719494]

Esistono due hello toodisplay di modi **accesso remoto** finestra di dialogo proprietà:

* Fare clic su hello **avanzate** collegamento hello **accesso remoto** sezione di hello **pubblicare tooAzure** finestra di dialogo.

* Aprire hello **proprietà** finestra di dialogo del progetto Azure.

Quando si crea un nuovo progetto di distribuzione di Azure, progetto hello non è abilitato per impostazione predefinita l'accesso remoto. Tuttavia, è possibile abilitare facilmente l'accesso remoto specificando nome utente hello e una password in hello **pubblicare tooAzure** finestra di dialogo. password di accesso remoto Hello viene crittografata mediante certificati x. 509. Se non si utilizza, fornire il proprio certificato, la crittografia hello si basa su un certificato autofirmato fornito con hello Azure Plugin for Eclipse. Questo certificato autofirmato è hello **cert** cartella del progetto Azure, archiviato sia come un file di certificato pubblico (SampleRemoteAccessPublic.cer) e come un scambio di informazioni personali (PFX) (file di certificato SampleRemoteAccessPrivate.pfx). Hello quest'ultimo contiene la chiave privata per il certificato di hello hello e una password predefinita, ha **Password1**. Tuttavia, poiché questa password è pubblico, il certificato di predefinito hello deve essere usato solo per finalità di apprendimento, non per una distribuzione di produzione. In modo diverso ai fini dell'apprendimento, quando si desidera che le sessioni remote tooenabled per le distribuzioni, è necessario fare clic hello **avanzate** collegamento hello **pubblicare tooAzure** toospecify finestra di dialogo personalizzate certificato. Si noti che è necessario tooupload hello PFX versione servizio di hello certificati tooyour ospitato all'interno di hello portale di gestione di Azure, in modo che Azure possa decrittografare la password utente hello.

resto Hello di esercitazione hello viene illustrata la modalità di accesso remoto di tooenable per un progetto di distribuzione di Azure che è stato inizialmente creato con l'accesso remoto disabilitato. Ai fini di questa esercitazione, verrà creato un nuovo certificato autofirmato e il relativo file con estensione pfx avrà una password di propria scelta. È anche possibile hello utilizzando un certificato emesso da un'autorità di certificazione.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Come tooenable accesso remoto dopo avere distribuito tooAzure
accesso remoto tooenable dopo aver distribuito tooAzure, utilizzare hello alla procedura seguente:

1. Accedere al portale di gestione di Azure di hello utilizzando l'account di Azure

2. Nell'elenco di **servizi Cloud**, selezionare il servizio cloud distribuito

3. Nella pagina web del servizio cloud hello, fare clic su hello **configura** collegamento

4. Nella parte inferiore di hello hello della pagina di configurazione, fare clic su hello **remoto** collegamento

5. Quando viene visualizzata finestra di dialogo popup hello:
   
   * Specificare hello ruolo è per il quale si desidera l'accesso remoto tooenable

   * Fare clic su hello tooselect **Abilita Desktop remoto** casella di controllo
   
   * Specificare un nome utente e password per l'accesso remoto da toouse
   
   * Selezionare hello certificato toouse

6. Fare clic su **OK** 

Si verrà visualizzato un messaggio che informa che la modifica della configurazione è in corso, che potrebbe richiedere alcuni minuti toocomplete. Al termine della modifica della configurazione hello, seguire i passaggi hello hello **toolog in modalità remota** sezione più avanti in questo articolo.

## <a name="how-tooenable-remote-access-in-your-package"></a>La modalità di accesso remoto tooenable nel pacchetto
1. Nel riquadro Project Explorer di Eclipse fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Properties**.

2. In hello **proprietà** finestra di dialogo espandere **Azure** nel riquadro sinistro di hello e fare clic su **accesso remoto**.

3. In hello **accesso remoto** finestra di dialogo, verificare **abilitare tutti i ruoli tooaccept connessioni Desktop remoto con le credenziali di account di accesso** è selezionata.

4. Specificare un nome utente per hello connessione Desktop remoto.

5. Specificare e confermare una password hello hello utente. Hello valori nome utente e password impostati in questa finestra di dialogo verranno utilizzati quando si effettua una connessione Desktop remoto. (Si tratta di una password diversa dalla password PFX).

6. Specificare la data di scadenza hello per account utente di hello.

7. Fare clic su **New** toocreate un nuovo certificato autofirmato. (In alternativa, è possibile selezionare un certificato dal sistema dell'area di lavoro o un file tramite hello **dell'area di lavoro** o **FileSystem** pulsanti, rispettivamente, ma ai fini di questa esercitazione si creerà un nuovo certificato).

   * In hello **nuovo certificato** finestra di dialogo, specificare e confermare una password hello da utilizzare per il file PFX.

   * Accettare il valore specificato per hello **nome (CN)**, oppure utilizzare un nome personalizzato.

   * Specificare hello percorso e nome file in cui verrà salvato hello nuovo certificato, in formato con estensione cer. Per questo passaggio e hello successivo, è possibile utilizzare hello **cert** cartella del progetto Azure, ma si toochoose disponibile un'altra posizione. Ai fini di questa esercitazione, si userà **c:\mycert\mycert.cer**. (Creare hello **c:\mycert** tooproceeding precedente cartella o una cartella esistente, se lo si desidera utilizzare.)

   * Specificare hello percorso e nome file in cui verrà salvati hello nuovo certificato e relativa chiave privata, in formato pfx. Ai fini di questa esercitazione, si userà **c:\mycert\mycert.pfx**. Il **nuovo certificato** finestra di dialogo dovrebbe essere simile toohello seguente (aggiornare i percorsi delle cartelle hello se non si utilizza **c:\mycert**):
     
      ![][ic712275]

   * Fare clic su **OK** tooclose hello **nuovo certificato** finestra di dialogo.

8. Il **accesso remoto** finestra di dialogo dovrebbe essere simile toohello seguenti:</p>
   
   ![][ic719495]

9. Fare clic su **OK** tooclose hello **accesso remoto** finestra di dialogo.

Ricompilare l'applicazione, con hello set per la distribuzione toocloud di compilazione.

## <a name="toolog-in-remotely"></a>toolog in modalità remota
Quando l'istanza del ruolo è pronta, è possibile accedere in remoto nella macchina virtuale toohello che ospita l'applicazione.

* Se Usa Eclipse in Windows e hello selezionato **inizio desktop remoto in distribuire** opzione durante la distribuzione tooAzure, verrà visualizzata una schermata di accesso della connessione Desktop remoto all'avvio della distribuzione. Quando viene chiesto di immettere nome utente hello e una password, immettere i valori hello specificato per l'utente remoto hello e sarà in grado di toolog in.

* Un altro modo toolog in è in modalità remota tramite hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">il portale di gestione di Azure</a>:
  
  * All'interno di hello **servizi Cloud** visualizzazione di hello portale di gestione di Azure, il servizio cloud fare clic su **istanze**, fare clic su un'istanza specifica e quindi fare clic su hello **Connetti**pulsante. Hello **Connetti** pulsante viene visualizzato come riportato di seguito hello nella barra dei comandi di hello:
    
      ![][ic659273]

  * Dopo aver fatto clic hello **Connetti** pulsante, sarà richiesta tooopen un file RDP. Aprire il file hello e seguire le istruzioni di hello. (Si può salvare anche il computer locale tooyour di file e quindi eseguire file hello facendovi doppio clic tooremote log in tooyour macchina virtuale senza la necessità di toofirst visitare il portale di gestione di hello.)

  * Quando viene chiesto di immettere nome utente hello e una password, immettere i valori hello specificato per l'utente remoto hello e sarà in grado di toolog in.

> [!NOTE]
> Se si utilizza un sistema operativo non Windows, è necessario toouse client Desktop remoto compatibile con il sistema operativo e seguire tooconfigure passaggi hello client con le impostazioni di hello in file con estensione RDP hello che è stato scaricato.
> 
> 

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
