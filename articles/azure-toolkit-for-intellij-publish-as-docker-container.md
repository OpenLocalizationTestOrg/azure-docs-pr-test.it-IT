---
title: un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ

I contenitori Docker sono un metodo molto diffuso per la distribuzione di applicazioni Web. Usando i contenitori di Docker, gli sviluppatori possono consolidare tutti i relativi file di progetto e le dipendenze in un singolo pacchetto tooa come server di distribuzione. Hello Azure Toolkit per IntelliJ semplifica questo processo per gli sviluppatori Java aggiungendo *pubblica come contenitore Docker* funzionalità per tooMicrosoft distribuzione Azure. In questo articolo illustra hello passaggi necessari toopublish tooAzure le applicazioni come contenitori Docker.

> [!NOTE]
>
> Ulteriori informazioni su Docker sono disponibili sul hello [sito Web di Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Pubblicare il tooAzure app web con un contenitore Docker

> [!NOTE]
> * toopublish l'app web, è necessario creare un elemento pronto per la distribuzione. toolearn informazioni, vedere hello [ulteriori informazioni sulla creazione di elementi](#artifacts) sezione.
>
> * Dopo aver completato la creazione guidata distribuzione hello almeno una volta, la maggior parte delle impostazioni vengono utilizzata come impostazioni predefinite quando si esegue nuovamente la procedura guidata hello.
>

1. Aprire il progetto dell'app Web in IntelliJ.

2. hello toostart **pubblica come contenitore Docker** procedura guidata, effettuare una delle seguenti hello:

   * In hello **progetto** finestra degli strumenti, mouse sul progetto, fare clic su **Azure**, quindi fare clic su **pubblica come contenitore Docker**:

      ![Hello pubblica come comando contenitore Docker][PUB01]

   * Sulla barra degli strumenti IntelliJ hello, fare clic su hello **gruppo pubblica** pulsante e quindi fare clic su **pubblica come contenitore Docker**:

      ![Hello pubblica come comando contenitore Docker][PUB02]  
    Hello **distribuire contenitore Docker in Azure** apre la procedura guidata.

   ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB03]

3. In hello **digitare un nome di immagine, selezionare il percorso dell'elemento hello e verificare un toobe host Docker utilizzato** finestra hello seguenti: 

   a. In hello **nome immagine Docker** , immettere un nome univoco per l'host Docker. (hello verrà creata automaticamente un nome, ma è possibile modificarlo). 

   b. Hello **host** area vengono visualizzati tutti gli host Docker che è già stato creato. Effettuare una delle seguenti hello: 
      * Se si dispone di un host Docker esistente, è possibile distribuire il tooit app web.
      * toocreate un host Docker, fare clic su verde hello sul segno più (**+**).  
       Hello **creare Host Docker** verrà visualizzata la finestra di dialogo. 

      ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB04a]

4. In hello **configurare hello nuova macchina virtuale** finestra, fornire le seguenti informazioni sull'host Docker hello. (la maggior parte delle informazioni hello hello generato automaticamente, ma è possibile modificare ciascuno di essi). 

   a. In hello **nome** , immettere un nome univoco per l'host Docker hello. (È hello non uguali a quelli hello Nome immagine con Docker specificato in precedenza). 
    
   b. In hello **sottoscrizione** immettere hello sottoscrizione di Azure in uso per l'host. 
      
   c. In hello **area** , immettere l'area geografica di hello in cui si trova nell'host.
      
   d. In hello **del sistema operativo e le dimensioni** scheda, hello seguenti:      
      * **Host del sistema operativo**: immettere hello del sistema operativo per la macchina virtuale hello che contiene l'host. 
      * **Dimensioni**: immettere una dimensione di macchina virtuale hello per l'host.   
       
   e. In hello **gruppo di risorse** selezionare hello seguenti:      
      * **New resource group** (Nuovo gruppo di risorse): consente di creare un nuovo gruppo di risorse per l'host.
      * **Existing resource group** (Gruppo di risorse esistente): consente di specificare un gruppo di risorse dal proprio account Azure. 
       
   f. In hello **rete** selezionare hello seguenti:      
      * **New virtual network** (Nuova rete virtuale): consente di creare una nuova rete virtuale per l'host.
      * **Existing virtual network** (Rete virtuale esistente): consente di specificare una rete virtuale esistente dal proprio account Azure. 
       
   g. In hello **archiviazione** selezionare hello seguenti:      
      * **New storage account** (Nuovo account di archiviazione): consente di creare un nuovo account di archiviazione per l'host.
      * **Existing storage account** (Account di archiviazione esistente): consente di specificare un account di archiviazione esistente dal proprio account Azure.
       
5. Fare clic su **Avanti**.  
     Hello **configurare log nelle credenziali e le impostazioni delle porte** verrà visualizzata la finestra.

      ![log Configura Hello nella finestra di impostazioni di porta e credenziali][PUB05]

6. Selezionare una delle seguenti opzioni hello:

      * **Import credentials from Azure Key Vault** (Importa credenziali da Azure Key Vault): consente di specificare un set di credenziali salvato in precedenza e archiviato nella sottoscrizione di Azure.

          > [!NOTE]
          > Un insieme di credenziali chiave Azure creato con un account specifico o un'entità servizio non è accessibile automaticamente da un altro account o entità servizio che condivide sottoscrizione hello. insieme di credenziali di un altro account o un servizio principale toouse hello chiave tooallow, è necessario utilizzare hello account hello tooadd portale Azure o un'entità servizio.

      * **New log in credentials** (Nuove credenziali di accesso): consente di creare un nuovo set di credenziali di accesso. Se si seleziona questa opzione, hello seguenti:

        a. In hello **credenziali VM** scheda, fornire le seguenti informazioni per le credenziali di accesso di macchina virtuale hello dell'host Docker hello: * **Username**: immettere un nome utente hello per l'account di accesso di macchina virtuale credenziali.
             * **Password** e **conferma**: immettere la password di hello per le credenziali di accesso di macchina virtuale.
             * **SSH**: immettere le impostazioni di hello Secure Shell (SSH) per l'host Docker. È possibile selezionare una delle seguenti opzioni hello: * **Nessuna**: Specifica che la macchina virtuale non consente le connessioni SSH.
                * **Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione via SSH.
                * **Importa da directory**: consente di toospecify una directory che contiene un set di impostazioni SSH salvate in precedenza. directory Hello deve contenere i seguenti due file hello:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. In hello **Docker Daemon accesso** scheda, fornire hello le seguenti informazioni:

          ![Creare un host Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Dopo avere immesso le informazioni necessarie hello, fare clic su **fine**.  
    Hello **distribuire contenitore Docker in Azure** procedura guidata viene visualizzata di nuovo.

   ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB07]

8. Fare clic su **Avanti**.  
    Hello **configurare hello Docker contenitore toobe creato** verrà visualizzata la finestra.

   ![finestra di Hello Configura hello Docker contenitore toobe creato][PUB08]

9. In hello **configurare hello Docker contenitore toobe creato** finestra forniscono hello le seguenti informazioni: 

   a. In hello **nome del contenitore Docker** , immettere un nome univoco per il contenitore Docker.

   b. Scegliere una delle seguenti immagini Docker hello: 

      * **Predefined Docker image** (Immagine Docker predefinita): consente di specificare un'immagine preesistente in Azure. 

        > [!NOTE]
        > elenco di Hello delle immagini Docker in questa casella è costituito da diverse immagini che hello Azure Toolkit è stato configurato toopatch in modo che l'elemento viene distribuita automaticamente. 

      * **Custom Dockerfile** (Dockerfile personalizzato): consente di specificare un Dockerfile salvato in precedenza nel computer locale.

        > [!NOTE]
        > Questa è una funzionalità più avanzata per gli sviluppatori che desiderano toodeploy i propri Dockerfile. È invece backup toodevelopers che utilizzano questo tooensure opzione i Dockerfile compilato correttamente. Hello Azure Toolkit non in grado di convalidare il contenuto di hello in un Dockerfile personalizzato, la distribuzione di hello potrebbe non riuscire se hello Dockerfile presenta problemi. Inoltre, poiché hello Azure Toolkit si aspetta hello personalizzato Dockerfile toocontain un artefatto di app web, viene effettuato un tentativo tooopen una connessione HTTP. Pubblicando un diverso tipo di elemento, gli sviluppatori potrebbero ricevere errori non gravi dopo la distribuzione.

   c. In hello **le impostazioni delle porte** immettere hello univoco TCP binding delle porte per il contenitore Docker. 

10. Dopo aver completato i passaggi precedenti, hello, fare clic su **fine**. 

Hello Azure Toolkit inizia il tooAzure app web in un contenitore Docker. A meno che non è stato configurato toobe IntelliJ distribuito in background hello, un **distribuzione tooAzure** viene visualizzato l'indicatore di stato. 

![indicatore di stato di distribuzione Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Altre informazioni sulla creazione di elementi

hello toocreate un elemento, pronto per la distribuzione seguenti:

1. Aprire il progetto dell'app Web in IntelliJ.

2. Fare clic su **File** e quindi fare clic su **Project Structure** (Struttura del progetto).

   ![Hello comando struttura del progetto][ART01]

3. tooadd un elemento, fare clic su verde hello sul segno più (**+**), quindi fare clic su **applicazione Web: archivio**.

   ![il comando "Archivio Web applicazione:" Hello][ART02]

4. In hello **nome** , immettere un nome per l'elemento (non includono hello *.war* estensione), quindi fare clic su **OK**.

   ![casella nome di elemento Hello][ART03]

Per ulteriori informazioni sulla creazione di elementi in IntelliJ, vedere [configurando elementi] nel sito Web JetBrains hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti risorse:

* [Toolkit di Azure per Eclipse]
  * [Novità di hello Azure Toolkit per Eclipse]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * [Istruzioni di accesso per hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
* [Toolkit di Azure per IntelliJ]
  * [Novità di hello Azure Toolkit per IntelliJ]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Accesso le istruzioni per hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

Per altre risorse per Docker, vedere ufficiale hello [sito Web di Docker].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Istruzioni di accesso per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

[sito Web di Docker]: https://www.docker.com/
[configurando elementi]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configurazione di elementi)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
