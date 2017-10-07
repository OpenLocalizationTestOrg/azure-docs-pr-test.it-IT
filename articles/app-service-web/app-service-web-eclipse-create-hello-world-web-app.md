---
title: aaaCreate un'app web basic di Azure usando Eclipse | Documenti Microsoft
description: Questa esercitazione viene illustrato come toouse hello Azure Toolkit per Eclipse toocreate un'App Web di Hello World per Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Creare un'app Web di base di Azure con Eclipse
Questa esercitazione viene illustrato come toocreate e distribuire una base tooAzure applicazione Hello World come un'App Web utilizzando hello [Azure Toolkit per Eclipse]. Per semplicità è riportato un esempio JSP di base, ma è possibile adottare una procedura simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.

Dopo aver completato questa esercitazione, l'applicazione avrà un aspetto simile toohello seguente illustrazione, quando viene visualizzata in un web browser:

![Anteprima dell'app Hello World][01]

## <a name="prerequisites"></a>Prerequisiti
* Java Developer Kit (JDK) versione 1.8 o successiva.
* IDE Eclipse per sviluppatori Java EE, Luna o versione successiva. È possibile scaricare il pacchetto all'indirizzo <http://www.eclipse.org/downloads/>.
* Distribuzione di un server Web basato su Java o un server applicazioni, ad esempio [Apache Tomcat] o [Jetty].
* Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello [Azure Toolkit per Eclipse]. Per informazioni sull'installazione hello Azure Toolkit, vedere [installazione hello Azure Toolkit per Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate un'applicazione Hello World
Creare innanzitutto un progetto Java.

1. Avviare Eclipse e nel menu hello scegliere **File**, fare clic su **New**, quindi fare clic su **progetto Web dinamico**. (Se non viene visualizzato **progetto Web dinamico** elencati tra i progetti disponibili dopo aver fatto clic **File** e **New**, quindi hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto...** , espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su **Avanti**.)
2. Ai fini di questa esercitazione, denominare il progetto di hello **MyWebApp**. Verrà visualizzata una schermata simile toohello seguenti:
   
    ![Creazione di un nuovo progetto Web dinamico][02]
3. Fare clic su **Fine**.
4. Nella visualizzazione Project Explorer (Esplora progetti) di Eclipse espandere **MyWebApp**. Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.
5. In hello **New JSP File** della finestra di dialogo file hello nome **index.jsp**, mantenere come cartella padre di hello **MyWebApp/WebContent**, quindi fare clic su **Avanti**.
6. In hello **Select JSP Template** la finestra di dialogo, ai fini di questa esercitazione, selezionare **New JSP File (html)**, quindi fare clic su **fine**.
7. All'apertura del file index.jsp in Eclipse, aggiungere la visualizzazione del testo toodynamically **Hello World!** all'interno di hello esistente `<body>` elemento. L'aggiornamento `<body>` contenuto dovrebbe essere simile a hello di esempio seguente:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Salvare index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy il tooan applicazione contenitore di App Web di Azure
Esistono diversi modi con cui è possibile distribuire un tooAzure di applicazione web Java. Questa esercitazione viene descritto uno dei più semplice hello: l'applicazione sarà distribuito tooan contenitore di App Web di Azure: nessun tipo di progetto speciale né altri strumenti sono necessari. Hello JDK hello web contenitore software e verrà fornito automaticamente da Azure, pertanto non c'è alcuna necessità tooupload proprio; è sufficiente l'App Web Java. Di conseguenza, processo di pubblicazione per l'applicazione hello richiederà secondi, minuti non.

1. In Project Explorer (Esplora progetti) di Eclipse fare clic con il pulsante destro del mouse su **MyWebApp**.
2. Nel menu di scelta rapida hello, selezionare **Azure**, quindi fare clic su **pubblica come App Web di Azure...**
   
    ![Publish as Azure Web App][03]
   
    In alternativa, mentre il progetto di applicazione web è stato selezionato in Esplora progetti hello, è possibile fare clic su hello **pubblica** pulsante a discesa sulla barra degli strumenti hello e selezionare **pubblica come App Web di Azure** da qui:
   
    ![Publish as Azure Web App][14]
3. Se non hanno già effettuato l'accesso a Azure da Eclipse, sarà possibile toosign richiesta nell'account Azure:
   
    ![Finestra di dialogo di accesso di Azure][04]
   
    Se si dispone di più account di Azure, alcune delle richieste di hello durante hello Accedi processo potrebbe essere visualizzato più volte, anche se appaiono toobe hello stesso. In questo caso, continuare dopo il segno di hello nelle istruzioni.
4. Dopo aver completato l'accesso all'account Azure, hello **Gestisci sottoscrizioni** la finestra di dialogo verrà visualizzato un elenco di sottoscrizioni associate le credenziali. Se sono presenti più sottoscrizioni elencate e si desidera toowork con solo un sottoinsieme specifico di essi, è possibile deselezionare l'opzione hello desiderati toouse. Dopo aver selezionato le sottoscrizioni, fare clic su **Close**(Chiudi).
   
    ![Finestra di dialogo Gestisci sottoscrizioni][05]
5. Quando hello **tooAzure contenitore di App Web di distribuire** viene visualizzata la finestra di dialogo, verrà visualizzato qualsiasi contenitore di App Web creato in precedenza; se non è stato creato tutti i contenitori, elenco hello sarà vuoto.
   
    ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][06]
6. Se non create un contenitore di App Web di Azure prima o se si desidera toopublish nel nuovo contenitore tooa di applicazione, utilizzare hello alla procedura seguente. In caso contrario, selezionare un contenitore di App Web esistente e ignorare toostep 7 seguente.
   
   1. Fare clic su **Nuovo**
      
       ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][15]
   2. Hello **nuovo contenitore di App Web** verrà visualizzata la finestra di dialogo:
      
       ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][07a]
   3. Immettere un **etichetta DNS** per il contenitore di App Web; verrà formato etichetta DNS foglia di hello dell'URL host hello per l'applicazione web in Azure. Si noti che nome hello deve essere disponibile e conforme tooAzure requisiti di denominazione App Web.
   4. In hello **contenitore Web** dal menu a discesa, selezionare hello del software di appropriato per l'applicazione.
      
       Attualmente è possibile scegliere fra Tomcat 8, Tomcat 7 o Jetty 9. Una distribuzione recente del software hello selezionata verrà fornita da Azure e verrà eseguito in una distribuzione recente di JDK 8 creata da Oracle e fornita da Azure.
   5. In hello **sottoscrizione** dal menu a discesa, selezionare hello sottoscrizione toouse per questa distribuzione.
   6. In hello **gruppo di risorse** dal menu a discesa, seleziona hello gruppo di risorse a cui si desidera tooassociate App Web. (Gruppi di risorse di azure consente si toogroup correlate alle risorse in modo che, ad esempio, possibile eliminati insieme).
      
       È possibile selezionare un gruppo di risorse esistente (se sono presenti) e Ignora toostep g seguente o utilizzare hello seguendo questi passaggi toocreate un nuovo gruppo di risorse:
      
      * Fare clic su **Nuovo**
      * Hello **nuovo gruppo di risorse** verrà visualizzata la finestra di dialogo:
        
          ![Finestra di dialogo Nuovo gruppo di risorse][08]
      * In hello hello **nome** casella di testo, specificare un nome per il nuovo gruppo di risorse.
      * In hello hello **area** menu a discesa, selezionare hello appropriato data center di Azure percorso per il gruppo di risorse.
      * Facoltativo: Per impostazione predefinita, una distribuzione recente di Java 8 verrà distribuita da Azure automaticamente il contenitore di app web di tooyour come la JVM. Tuttavia, è possibile specificare una versione diversa e la distribuzione di hello JVM se richiesto per l'App Web. hello toospecify JDK per l'App Web, fare clic su hello **JDK** scheda e selezionare una delle seguenti opzioni hello:
        
        * **Distribuire predefinito hello JDK offerta dal servizio App Web di Azure**: questa opzione verrà distribuito a una distribuzione recente di Java 8.
        * **Distribuire una 3rd party JDK disponibile in Azure**: questa opzione consente di toochoose dall'elenco di hello di JDK forniti da Microsoft Azure.
        * **Distribuzione di JDK da questo percorso di download**: questa opzione consente di toospecify la propria distribuzione di JDK, che deve essere compresso come un file ZIP e caricati tooeither un percorso di download disponibile pubblicamente o una risorsa di archiviazione di Azure con un account per il quale si ha accesso.
          
          ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][07b]
   7. Fare clic su **OK**.
   8. Hello **piano di servizio App** dal menu a discesa sono elencati i piani di servizio app hello associati hello gruppo di risorse selezionato. (I piani di servizio app consente di specificare informazioni quali il percorso di hello dell'App Web, hello piano tariffario e dimensioni di istanze di calcolo hello. È possibile usare un singolo piano di servizio app per più app Web. Per questo motivo viene gestito separatamente da una distribuzione di app Web specifica.
      
       È possibile selezionare un piano di servizio App esistente (se sono presenti) e ignorare toostep h riportato di seguito oppure utilizzare hello seguendo questi passaggi toocreate un piano di servizio App nuovo:
      
      * Fare clic su **Nuovo**
      * Hello **piano di servizio App nuovo** verrà visualizzata la finestra di dialogo:
        
          ![Finestra di dialogo New App Service Plan (Nuovo piano di servizio app)][09]
      * In hello hello **nome** casella di testo, specificare un nome per il piano di servizio App nuovo.
      * In hello hello **percorso** menu a discesa, selezionare hello appropriato data center di Azure percorso per il piano di hello.
      * In hello hello **tariffario** dal menu a discesa, seleziona hello prezzi per il piano di hello appropriato. Ai fini del test è possibile scegliere **Gratuito**.
      * In hello hello **dimensioni istanze** dal menu a discesa, dimensioni di istanza appropriata di hello selezionare per il piano di hello. Ai fini del test è possibile scegliere **Piccolo**.
   9. Dopo aver completato tutti hello sopra passaggi, la finestra di dialogo Nuovo contenitore di App Web di hello dovrebbe essere simile a hello nella figura riportata di seguito:
      
       ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][10]
   10. Fare clic su **OK** creazione hello toocomplete del nuovo contenitore App Web.
       
        Attendere alcuni secondi per elenco hello di hello App Web contenitori toobe aggiornato e il contenitore di app web appena creato dovrebbe ora essere selezionato nell'elenco di hello.
7. Si è ora pronto toocomplete hello la distribuzione iniziale di tooAzure l'App Web:
   
    ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][11]
   
    Fare clic su **OK** toodeploy toohello di applicazione del linguaggio selezionato contenitore di App Web.
   
    Per impostazione predefinita, l'applicazione verrà distribuita come sottodirectory hello del server delle applicazioni. Se si vuole toobe distribuito come applicazione radice hello, controllare hello **distribuire tooroot** casella di controllo prima di scegliere **OK**.
8. Successivamente, si dovrebbe essere hello **Log attività Azure** visualizzazione, che indica lo stato di distribuzione hello dell'App Web.
   
    ![Azure Activity Log][12]
   
    il processo di Hello di distribuzione tooAzure l'App Web debba richiedere solo pochi secondi toocomplete. Quando l'inizio di applicazione, verrà visualizzato un collegamento denominato **pubblicato** in hello **stato** colonna. Quando si fa clic sul collegamento hello, si passerà home page dell'App Web tooyour distribuito.

## <a name="updating-your-web-app"></a>Aggiornamento dell'app Web
L'aggiornamento di un'app Web di Azure in esecuzione è un processo semplice e rapido. Sono disponibili due opzioni per l'aggiornamento:

* È possibile aggiornare la distribuzione di hello di un'App Web Java esistente.
* È possibile pubblicare un aggiuntiva toohello applicazione Java nello stesso contenitore di App Web.

In entrambi i casi, il processo di hello è identico e richiede solo pochi secondi:

1. In Esplora progetti di Eclipse hello, fare doppio clic su un'applicazione Java hello desiderati tooupdate o aggiungere tooan contenitore di App Web esistente.
2. Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure** e quindi **pubblica come App Web di Azure...**
3. Poiché è già stato effettuato l'accesso in precedenza, verrà visualizzato un elenco dei contenitori di app Web esistenti. Selezionare hello uno desiderati toopublish o pubblicare nuovamente il clic tooand di applicazioni Java **OK**.

Pochi secondi dopo, hello **Log attività Azure** visualizzazione saranno inclusi distribuzione aggiornata come **pubblicato** e si sarà in grado di tooverify l'applicazione aggiornata in un web browser.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Avvio, arresto o riavvio di un'app Web esistente
toostart o arrestare un contenitore di App Web di Azure esistente, (incluse tutte le applicazioni Java hello distribuito in essa contenuti), è possibile usare hello **Esplora Azure** visualizzazione.

Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **finestra** menu in Eclipse, quindi fare clic su **Mostra visualizzazione**, quindi **altri...** , quindi **Azure**, quindi fare clic su **Esplora Azure**. Se non è stato precedentemente eseguito, verrà chiesto toodo così.

Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire questi passaggi toostart o arrestare l'App Web: 

1. Espandere hello **Azure** nodo.
2. Espandere hello **App Web** nodo. 
3. Pulsante destro del mouse hello desiderato App Web.
4. Quando viene visualizzato il menu di scelta rapida hello, fare clic su **avviare**, **arrestare**, o **riavviare**. Si noti che le opzioni di menu hello che riconoscano il contesto, pertanto è possibile arrestare un'app web in esecuzione o avviare un'app web che non è attualmente in esecuzione.
   
    ![Arresto di un'app Web esistente][13]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Azure Toolkit per Eclipse]
  * [installazione hello Azure Toolkit per Eclipse]
  * *Creare un’app Web Hello World per Azure in Eclipse (questo articolo)*
  * [Novità in Azure Toolkit per Eclipse hello]
* [Toolkit di Azure per IntelliJ]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]
  * [Novità in Azure Toolkit per IntelliJ hello]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

Per ulteriori informazioni sulla creazione di App Web di Azure, vedere hello [Panoramica di App Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installazione hello Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novità in Azure Toolkit per Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Panoramica di App Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
