---
title: server applicazioni Java di aaaRun in una VM di Azure classico | Documenti Microsoft
description: In questa esercitazione Usa le risorse create con il modello di distribuzione classica hello e Mostra come toocreate virtuale di Windows del computer e configurarlo come server applicazioni di toorun Apache Tomcat.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Come toorun un server applicazioni Java in una macchina virtuale creata con il modello di distribuzione classica hello
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per un modello di gestione delle risorse toodeploy un'App Web con Java 8 e Tomcat, vedere [qui](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Con Azure, è possibile utilizzare una funzionalità server tooprovide delle macchine virtuali. Ad esempio, una macchina virtuale in esecuzione in Azure può essere toohost configurato un server applicazioni Java, ad esempio Apache Tomcat.

Dopo aver completato questa Guida, si avrà una migliore comprensione di come toocreate una macchina virtuale in esecuzione in Azure e configurarlo toorun un server applicazioni Java. Informazioni che eseguire hello seguenti attività:

* Modalità virtuale toocreate computer che dispone di un Kit di sviluppo Java (JDK) già installato.
* Tooremotely Accedi come macchina virtuale tooyour.
* Come tooinstall un tipo server applicazioni Java - Apache Tomcat - sulla macchina virtuale.
* Come toocreate un endpoint per la macchina virtuale.
* Una porta di hello tooopen come il firewall per il server applicazioni.

Hello completata i risultati dell'installazione di Tomcat in esecuzione in una macchina virtuale.

![Macchina virtuale che esegue Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate una macchina virtuale
1. Accedi toohello [portale di Azure](https://portal.azure.com).  
2. Fare clic su **New**, fare clic su **calcolo**, quindi fare clic su **tutti** in hello **App in evidenza**.
3. Fare clic su **JDK**, fare clic su **JDK 8** in hello **JDK** riquadro.  
   Le immagini di macchina virtuale che supportano **JDK 6** e **JDK 7** sono disponibili se si dispone di applicazioni legacy che non sono pronti toorun JDK 8.
4. Nel riquadro hello JDK 8 selezionare **classico**, quindi fare clic su **crea**.
5. In hello **nozioni di base** pannello:
   1. Specificare un nome per la macchina virtuale hello.
   2. Immettere un nome per l'amministratore di hello in hello **nome utente** campo. Ricordare il nome e la password associata che segue nel campo successivo hello hello. È necessario quando si accede in remoto nella macchina virtuale toohello.
   3. Immettere una password in hello **nuova password** campo e immetterlo di nuovo in hello **Conferma password** campo. Questa password è per hello account amministratore.
   4. Seleziona hello appropriato **sottoscrizione**.
   5. Per hello **gruppo di risorse**, fare clic su **Crea nuovo** e immettere il nome di hello del nuovo gruppo di risorse. Fare clic su **utilizzare esistente** e selezionare uno dei gruppi di risorse disponibili hello.
   6. Selezionare un percorso in cui hello risiede macchina virtuale, ad esempio **centro-meridionali**.
6. Fare clic su **Avanti**.
7. In hello **dimensione dell'immagine di macchina virtuale** pannello seleziona **A1 Standard** o un'altra immagine appropriata.
8. Fare clic su **Seleziona**.

9. In hello **impostazioni** pannello, fare clic su **OK**. È possibile utilizzare i valori predefiniti di hello forniti da Azure.  
10. In hello **riepilogo** pannello, fare clic su **OK**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>segno tooremotely nella macchina virtuale tooyour
1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Macchine virtuali (classico)**. Se necessario, fare clic su **più servizi** angolo hello inferiore sinistro in categorie servizio hello. Hello **macchine virtuali (classico)** voce in hello **calcolo** gruppo.
3. Fare clic su nome hello della macchina virtuale hello che si desidera toosign in.
4. Dopo l'avvio hello virtual machine, un menu nella parte superiore di hello del riquadro hello consente le connessioni.
5. Fare clic su **Connetti**.
6. Risposta toohello chiede come macchina virtuale di toohello tooconnect necessari. In genere, salvare o aprire file con estensione rdp hello che contiene i dettagli della connessione hello. È possibile avere toocopy hello url: porta come ultima parte di hello della prima riga di hello del file con estensione rdp hello e incollarlo in un'applicazione di accesso remota.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall un server applicazioni Java sulla macchina virtuale
È possibile copiare una macchina virtuale di tooyour Java applicazione server oppure è possibile installare un server applicazioni Java tramite un programma di installazione.

Questa esercitazione Usa Tomcat come tooinstall server applicazioni Java di hello.

1. Quando si accede alla macchina virtuale tooyour, aprire una sessione del browser troppo[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Fare doppio clic sul collegamento hello per **programma di installazione del servizio Windows 32-bit/64 bit**. Questa tecnica consente di installare Tomcat come servizio di Windows.
3. Quando richiesto, scegliere il programma di installazione di toorun hello.
4. All'interno di hello **il programma di installazione di Apache Tomcat** , seguire hello richiesto tooinstall Tomcat. Ai fini di hello di questa esercitazione, accettare le impostazioni predefinite hello è corretta. Quando si raggiunge hello **hello completamento installazione guidata di Apache Tomcat** nella finestra di dialogo è possibile controllare **eseguire Apache Tomcat** toohave ora inizio Tomcat. Fare clic su **fine** hello toocomplete il processo di installazione di Tomcat.

## <a name="toostart-tomcat"></a>toostart Tomcat

È possibile avviare manualmente Tomcat aprendo un prompt dei comandi per la macchina virtuale e il comando hello in esecuzione **net&nbsp;avviare&nbsp;Tomcat8**.

Una volta Tomcat è in esecuzione, è possibile accedere Tomcat immettendo l'URL di hello <http://localhost:8080> nel browser della macchina virtuale hello.

toosee Tomcat in esecuzione dal computer esterni, è necessario toocreate un endpoint e aprire una porta.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate un endpoint per la macchina virtuale
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Macchine virtuali (classico)**.
3. Fare clic su nome hello della macchina virtuale hello in cui è in esecuzione il server applicazioni Java.
4. Fare clic su **Endpoint**.
5. Fare clic su **Aggiungi**.
6. In hello **aggiungere endpoint** la finestra di dialogo:
   1. Specificare un nome per l'endpoint di hello; ad esempio, **HttpIn**.
   2. Selezionare **TCP** per protocollo hello.
   3. Specificare **80** per la porta pubblica hello.
   4. Specificare **8080** per la porta privata hello.
   5. Selezionare **disabilitato** per indirizzo IP mobile hello.
   6. Lasciare l'elenco di controllo di accesso di hello è.
   7. Fare clic su hello **OK** tooclose hello finestra di dialogo e creare endpoint hello.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen una porta nel firewall hello per la macchina virtuale
1. Accedi a macchina virtuale tooyour.
2. Fare clic sul pulsante **Start**di Windows.
3. Fare clic su **Pannello di controllo**.
4. Fare clic su **Sistema e sicurezza**, quindi su **Windows Firewall** e infine su **Impostazioni avanzate**.
5. Fare clic su **Regole connessioni in entrata** quindi su **Nuova regola**.  
   ![Nuova regola connessioni in entrata][NewIBRule]
6. Per hello **tipo di regola**selezionare **porta**, quindi fare clic su **Avanti**.  
   ![Porta della nuova regola connessioni in entrata][NewRulePort]
7. In hello **protocollo e porte** selezionare **TCP**, specificare **8080** come hello **porte locali specifiche**, quindi fare clic su **Avanti**.  
  ![Nuova regola connessioni in entrata][NewRuleProtocol]
8. In hello **azione** selezionare **Consenti connessione hello**, quindi fare clic su **Avanti**.
   ![Operazione per nuova regola connessioni in entrata][NewRuleAction]
9. In hello **profilo** schermata, assicurarsi che **dominio**, **privata**, e **pubblica** siano selezionate e quindi fare clic su **successivo** .
   ![Profilo per nuova regola connessioni in entrata][NewRuleProfile]
10. In hello **nome** schermata, specificare un nome per la regola hello, ad esempio **HttpIn** (nome della regola hello non è necessario toomatch nome dell'endpoint hello, tuttavia), quindi fare clic su **fine**.  
    ![Nome della nuova regola connessioni in entrata][NewRuleName]

A questo punto, il sito Web Tomcat dovrebbe essere visibile da un browser esterno. Nella finestra del browser hello indirizzo digitare l'URL di form hello  **http://*il\_DNS\_nome*. cloudapp.net**, in cui ***il\_DNS\_nome*** nome DNS hello specificato al momento della creazione macchina virtuale hello.

## <a name="application-lifecycle-considerations"></a>Considerazioni sul ciclo di vita delle applicazioni
* È possibile creare il proprio archivio di applicazione web (WAR) e aggiungerlo toohello **webapps** cartella. Ad esempio, creare un progetto Web dinamico di una pagina JSP (Java Service Page) di base ed esportarlo come file con estensione WAR. Successivamente, copiare hello WAR toohello Apache Tomcat **webapps** cartella nella macchina virtuale hello, quindi eseguirlo in un browser.
* Per impostazione predefinita quando si è installato il servizio di Tomcat hello, questo viene impostato toostart manualmente. È possibile tornare toostart automaticamente tramite lo snap-in servizi di hello. Avviare lo snap-in servizi di hello facendo **Start di Windows**, **strumenti di amministrazione**e quindi **servizi**. Fare doppio clic su hello **Apache Tomcat** del servizio e impostare **tipo di avvio** troppo**automatica**.

    ![L'impostazione di un servizio toostart automaticamente][service_automatic_startup]

    Hello vantaggi dell'avvio automatico Tomcat sono che viene avviata l'esecuzione quando viene riavviato macchina virtuale hello (ad esempio, dopo aver installati gli aggiornamenti software che richiedono il riavvio).

## <a name="next-steps"></a>Passaggi successivi
Sarà possibile apprendere altri servizi (ad esempio l'archiviazione di Azure, bus di servizio e Database SQL) che è possibile tooinclude con le applicazioni Java. Visualizzare informazioni hello disponibili hello [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
