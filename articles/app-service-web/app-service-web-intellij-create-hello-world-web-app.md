---
title: un'applicazione web di Azure di base in IntelliJ aaaCreate | Documenti Microsoft
description: Questa esercitazione viene illustrato come toouse hello Azure Toolkit per IntelliJ toocreate un'App Web di Hello World per Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Creare un'app Web di base di Azure in IntelliJ
Questa esercitazione viene illustrato come toocreate e distribuire una base tooAzure applicazione Hello World come un'App Web utilizzando hello [Azure Toolkit per IntelliJ]. Per semplicità è riportato un esempio JSP di base, ma è possibile adottare una procedura simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.

Dopo aver completato questa esercitazione, l'applicazione avrà un aspetto simile toohello seguente illustrazione, quando viene visualizzata in un web browser:

![Pagina Web di esempio][01]

## <a name="prerequisites"></a>Prerequisiti
* Java Developer Kit (JDK) versione 1.8 o successiva.
* IntelliJ IDEA Ultimate Edition. È possibile scaricarlo da <https://www.jetbrains.com/idea/download/index.html>.
* Distribuzione di un server Web basato su Java o un server applicazioni, ad esempio [Apache Tomcat] o [Jetty].
* Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello [Azure Toolkit per IntelliJ]. Per informazioni sull'installazione hello Azure Toolkit, vedere [installazione hello Azure Toolkit per IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>toocreate un'applicazione Hello World
Creare innanzitutto un progetto Java.

1. Avviare IntelliJ e fare clic su hello **File** menu, quindi fare clic su **New**, quindi fare clic su **progetto**.
   
    ![File > New Project (Nuovo progetto)][02]
2. Nella finestra di dialogo Nuovo progetto di hello, selezionare **Java**, quindi **applicazione Web**, quindi fare clic su **New** tooadd un SDK di progetto.
   
    ![Finestra di dialogo Nuovo progetto][03a]
   
3. In hello selezione della Home Directory per la finestra di dialogo JDK, selezionare hello cartella in cui è installato il pacchetto JDK e quindi fare clic su **OK**. Fare clic su **Avanti** in toocontinue casella finestra di dialogo Nuovo progetto di hello.
   
    ![Specificare la home directory di JDK][03b]
4. Ai fini di questa esercitazione, denominare il progetto di hello **Java-Web-App-in-Azure**, quindi fare clic su **fine**.
   
    ![Finestra di dialogo Nuovo progetto][04]
5. Nella visualizzazione Project Explorer di IntelliJ espandere **Java-Web-App-On-Azure** e **web**, quindi fare doppio clic su **index.jsp**.
   
    ![Pagina di indice aperta][05c]
6. All'apertura del file index.jsp in IntelliJ, aggiungere la visualizzazione del testo toodynamically **Hello World!** all'interno di hello esistente `<body>` elemento. L'aggiornamento `<body>` contenuto dovrebbe essere simile a hello di esempio seguente:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Salvare index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy il tooan applicazione contenitore di App Web di Azure
Esistono diversi modi con cui è possibile distribuire un tooAzure di applicazione web Java. Questa esercitazione viene descritto uno dei più semplice hello: l'applicazione sarà distribuito tooan contenitore di App Web di Azure: nessun tipo di progetto speciale né altri strumenti sono necessari. Hello JDK hello web contenitore software e verrà fornito automaticamente da Azure, pertanto non c'è alcuna necessità tooupload proprio; è sufficiente l'App Web Java. Di conseguenza, processo di pubblicazione per l'applicazione hello richiederà secondi, minuti non.

Prima di pubblicare l'applicazione, è innanzitutto necessario tooconfigure le impostazioni del modulo. toodo in tal caso, utilizzare hello alla procedura seguente:

1. In Esplora progetti del IntelliJ pulsante destro del mouse hello **Java-Web-App-in-Azure** progetto. Quando viene visualizzato il menu di scelta rapida hello, fare clic su **aprire le impostazioni del modulo**.

    ![Open Module Settings (Apri impostazioni modulo)][05a]
2. Quando viene visualizzata la finestra di dialogo di hello struttura del progetto:

   a. Fare clic su **elementi** nell'elenco di hello di **impostazioni progetto**.
   b. Nome dell'artefatto modifica hello in hello **nome** casella in modo che non contenga spazi o caratteri speciali; questa operazione è necessaria perché verrà usati nome hello in hello identificatore URI (Uniform Resource).
   c. Hello modifica **tipo** troppo**applicazione Web: archivio**.
   d. Fare clic su **OK** la finestra di dialogo di tooclose hello struttura del progetto.

    ![Open Module Settings (Apri impostazioni modulo)][05b]

Dopo aver configurato le impostazioni del modulo, è possibile pubblicare l'applicazione tooAzure utilizzando hello alla procedura seguente:

1. In Esplora progetti del IntelliJ pulsante destro del mouse hello **Java-Web-App-in-Azure** progetto. Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure**, quindi fare clic su **pubblica come App Web di Azure...**
   
    ![Menu di scelta rapida per la pubblicazione in Azure][06]
2. Se non hanno già effettuato l'accesso a Azure da IntelliJ, sarà richiesta toosign all'account Azure. (Se si dispone di più account di Azure, alcune delle richieste di hello durante il processo di accesso hello potrebbero essere visualizzati più volte, anche se appaiono toobe hello stesso. In questo caso, continuare toofollow hello sign in istruzioni).
   
    ![Finestra di accesso di Azure][07]
3. Dopo aver completato l'accesso all'account Azure, hello **Gestisci sottoscrizioni** la finestra di dialogo verrà visualizzato un elenco di sottoscrizioni associate le credenziali. (Se sono presenti più sottoscrizioni elencate e si desidera toowork con solo un sottoinsieme specifico di essi, è possibile facoltativamente deselezionare sottoscrizioni hello non si desidera toouse.) Dopo aver selezionato le sottoscrizioni, fare clic su **Close**(Chiudi).
   
    ![Gestisci sottoscrizioni][08]
4. Quando hello **tooAzure contenitore di App Web di distribuire** viene visualizzata la finestra di dialogo, verrà visualizzato qualsiasi contenitore di App Web creato in precedenza; se non è stato creato tutti i contenitori, elenco hello sarà vuoto.
   
    ![Contenitori di app][09]
5. Se non create un contenitore di App Web di Azure prima o se si desidera toopublish nel nuovo contenitore tooa di applicazione, utilizzare hello alla procedura seguente. In caso contrario, selezionare un contenitore di App Web esistente e ignorare toostep 6 seguente.
   
   1. Fare clic su **+**
      
       ![Aggiungere un contenitore di app][10]
   2. Hello **nuovo contenitore di App Web** verrà visualizzata la finestra di dialogo, che sarà utilizzato per hello next diversi passaggi.
      
       ![Nuovo contenitore di app][11a]
   3. Immettere un **etichetta DNS** per il contenitore di App Web; verrà formato etichetta DNS foglia di hello dell'URL host hello per l'applicazione web in Azure. Si noti che nome hello deve essere disponibile e conforme tooAzure requisiti di denominazione App Web.
   4. In hello **contenitore Web** dal menu a discesa, selezionare hello del software di appropriato per l'applicazione.
      
       Attualmente è possibile scegliere fra Tomcat 8, Tomcat 7 o Jetty 9. Una distribuzione recente del software hello selezionata verrà fornita da Azure e verrà eseguito in una distribuzione recente di JDK 8 creata da Oracle e fornita da Azure.
   5. In hello **sottoscrizione** dal menu a discesa, selezionare hello sottoscrizione toouse per questa distribuzione.
   6. In hello **gruppo di risorse** dal menu a discesa, seleziona hello gruppo di risorse a cui si desidera tooassociate App Web. (Gruppi di risorse di azure consente si toogroup correlate alle risorse in modo che, ad esempio, possibile eliminati insieme).
      
       È possibile selezionare un gruppo di risorse esistente (se sono presenti) e Ignora toostep g seguente, o a seguito di hello utilizzare passaggi toocreate un nuovo gruppo di risorse:
      
      * Selezionare  **&lt; &lt; Crea nuovo gruppo di risorse &gt; &gt;**  in hello **gruppo di risorse** dal menu a discesa.
      * Hello **nuovo gruppo di risorse** verrà visualizzata la finestra di dialogo:
        
          ![Nuovo gruppo di risorse][12]
      * In hello hello **nome** casella di testo, specificare un nome per il nuovo gruppo di risorse.
      * In hello hello **area** menu a discesa, selezionare hello appropriato data center di Azure percorso per il gruppo di risorse.
      * Fare clic su **OK**.
   7. Hello **piano di servizio App** dal menu a discesa sono elencati i piani di servizio app hello associati hello gruppo di risorse selezionato. (Un piano di servizio App consente di specificare informazioni quali il percorso di hello dell'App Web, hello piano tariffario e dimensioni di istanze di calcolo hello. È possibile usare un singolo piano di servizio app per più app Web. Per questo motivo viene gestito separatamente da una distribuzione di app Web specifica.
      
       È possibile selezionare un piano di servizio App esistente (se sono presenti) e ignorare toostep h riportato di seguito oppure utilizzare hello seguendo i passaggi toocreate un piano di servizio App nuovo:
      
      * Selezionare  **&lt; &lt; crea piano di servizio App nuovo &gt; &gt;**  in hello **piano di servizio App** dal menu a discesa.
      * Hello **piano di servizio App nuovo** verrà visualizzata la finestra di dialogo:
        
          ![Nuovo piano di servizio app][13]
      * In hello hello **nome** casella di testo, specificare un nome per il piano di servizio App nuovo.
      * In hello hello **percorso** menu a discesa, selezionare hello appropriato data center di Azure percorso per il piano di hello.
      * In hello hello **tariffario** dal menu a discesa, seleziona hello prezzi per il piano di hello appropriato. Ai fini del test è possibile scegliere **Gratuito**.
      * In hello hello **dimensioni istanze** dal menu a discesa, dimensioni di istanza appropriata di hello selezionare per il piano di hello. Ai fini del test è possibile scegliere **Piccolo**.
      * Fare clic su **OK**.
   8. (Facoltativo) Per impostazione predefinita, una distribuzione recente di Java 8 verrà automaticamente distribuita come la JVM dal contenitore di app web di Azure tooyour. Tuttavia, è possibile selezionare una versione diversa e la distribuzione di hello JVM. toodo in tal caso, utilizzare hello alla procedura seguente:
      
      * Fare clic su hello **JDK** scheda hello **nuovo contenitore di App Web** la finestra di dialogo.
      * È possibile scegliere una delle seguenti opzioni hello:
        
        * Distribuire predefinito hello JDK fornito da Azure
        * Distribuire un JDK di terze parti da un elenco a discesa di altri JDK disponibili in Azure
        * Distribuire un JDK personalizzato, che deve essere compresso come file ZIP e disponibile pubblicamente o nell'account di archiviazione di Azure
        
        ![Scheda JDK della finestra di dialogo New Web App Container (Nuovo contenitore app Web)][11b]
   9. Dopo aver completato tutti hello sopra passaggi, la finestra di dialogo Nuovo contenitore di App Web di hello dovrebbe essere simile a hello nella figura riportata di seguito:
      
       ![Nuovo contenitore di app][14]
   10. Fare clic su **OK** creazione hello toocomplete del nuovo contenitore App Web.
       
        Attendere alcuni secondi per elenco hello di hello App Web contenitori toobe aggiornato e il contenitore di app web appena creato dovrebbe ora essere selezionato nell'elenco di hello.
6. Si è ora pronto toocomplete hello la distribuzione iniziale di tooAzure l'App Web; Fare clic su **OK** toodeploy toohello di applicazione del linguaggio selezionato contenitore di App Web. Per impostazione predefinita, l'applicazione verrà distribuita come sottodirectory hello del server delle applicazioni. Se si vuole toobe distribuito come applicazione radice hello, controllare hello **distribuire tooroot** casella di controllo prima di scegliere **OK**.
   
    ![Distribuire tooAzure][15]
7. Successivamente, si dovrebbe essere hello **Log attività Azure** visualizzazione, che indica lo stato di distribuzione hello dell'App Web.
   
    ![Indicatore di stato][16]
   
    il processo di Hello di distribuzione tooAzure l'App Web debba richiedere solo pochi secondi toocomplete. Quando l'inizio di applicazione, verrà visualizzato un collegamento denominato **pubblicato** in hello **stato** colonna. Quando si fa clic sul collegamento hello, si passerà home page dell'App Web tooyour distribuito o è possibile utilizzare i passaggi di hello in hello seguente sezione toobrowse tooyour web app.

## <a name="browsing-tooyour-web-app-on-azure"></a>Esplorazione tooyour App Web in Azure
toobrowse tooyour App Web in Azure, è possibile utilizzare hello **Esplora Azure** visualizzazione.

Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **vista** IntelliJ, quindi scegliere **finestre degli strumenti**, quindi fare clic su  **Service Explorer**. Se non è stato precedentemente eseguito, verrà chiesto toodo così.

Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire tooyour di toobrowse App Web questi passaggi: 

1. Espandere hello **Azure** nodo.
2. Espandere hello **App Web** nodo. 
3. Pulsante destro del mouse hello desiderato App Web.
4. Quando viene visualizzato il menu di scelta rapida hello, fare clic su **Apri nel Browser**.
   
    ![Sfogliare l'app Web][17]

## <a name="updating-your-web-app"></a>Aggiornamento dell'app Web
L'aggiornamento di un'app Web di Azure in esecuzione è un processo semplice e rapido. Sono disponibili due opzioni per l'aggiornamento:

* È possibile aggiornare la distribuzione di hello di un'App Web Java esistente.
* È possibile pubblicare un aggiuntiva toohello applicazione Java nello stesso contenitore di App Web.

In entrambi i casi, il processo di hello è identico e richiede solo pochi secondi:

1. In Esplora progetti di hello IntelliJ, fare doppio clic su un'applicazione Java hello desiderati tooupdate o aggiungere tooan contenitore di App Web esistente.
2. Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure** e quindi **pubblica come App Web di Azure...**
3. Poiché è già stato effettuato l'accesso in precedenza, verrà visualizzato un elenco dei contenitori di app Web esistenti. Selezionare hello uno desiderati toopublish o pubblicare nuovamente il clic tooand di applicazioni Java **OK**.

Pochi secondi dopo, hello **Log attività Azure** visualizzazione saranno inclusi distribuzione aggiornata come **pubblicato** e si sarà in grado di tooverify l'applicazione aggiornata in un web browser.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Avvio, arresto o riavvio di un'app Web esistente
toostart o arrestare un contenitore di App Web di Azure esistente, (incluse tutte le applicazioni Java hello distribuito in essa contenuti), è possibile usare hello **Esplora Azure** visualizzazione.

Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **vista** IntelliJ, quindi scegliere **finestre degli strumenti**, quindi fare clic su  **Service Explorer**. Se non è stato precedentemente eseguito, verrà chiesto toodo così.

Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire questi passaggi toostart o arrestare l'App Web: 

1. Espandere hello **Azure** nodo.
2. Espandere hello **App Web** nodo. 
3. Pulsante destro del mouse hello desiderato App Web.
4. Quando viene visualizzato il menu di scelta rapida hello, fare clic su **avviare**, **arrestare**, o **riavviare**. Si noti che le opzioni di menu hello che riconoscano il contesto, pertanto è possibile arrestare un'app web in esecuzione o avviare un'app web che non è attualmente in esecuzione.
   
    ![Arrestare l'app Web][18]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Toolkit di Azure per Eclipse]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
  * [Novità in Azure Toolkit per Eclipse hello]
* [Azure Toolkit per IntelliJ]
  * [installazione hello Azure Toolkit per IntelliJ]
  * *Creare un’app Web Hello World per Azure in IntelliJ (questo articolo)*
  * [Novità in Azure Toolkit per IntelliJ hello]

<a name="see-also"></a>

## <a name="see-also"></a>Vedere anche
Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

Per ulteriori informazioni sulla creazione di App Web di Azure, vedere hello [Panoramica di App Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[installazione hello Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novità in Azure Toolkit per Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Panoramica di App Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
