---
title: un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per Eclipse

I contenitori Docker sono un metodo molto diffuso per la distribuzione di applicazioni Web. Usando i contenitori di Docker, gli sviluppatori possono consolidare tutti i relativi file di progetto e le dipendenze in un singolo pacchetto tooa come server di distribuzione. Hello Azure Toolkit per Eclipse semplifica questo processo per gli sviluppatori Java aggiungendo *pubblica come contenitore Docker* funzionalità per tooMicrosoft distribuzione Azure. In questo articolo illustra hello passaggi necessari toopublish tooAzure le applicazioni come contenitori Docker.

> [!NOTE]
> Ulteriori informazioni su Docker sono disponibili sul hello [sito Web di Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Pubblicare il tooAzure app web con un contenitore Docker

1. Aprire il progetto dell'applicazione Web in Eclipse.

2. hello toostart **pubblica come contenitore Docker** procedura guidata, effettuare una delle seguenti hello:

   * In hello **Navigator** visualizzare mouse sul progetto, fare clic su **Azure**, quindi fare clic su **pubblica come contenitore Docker**.

      ![Comando Publish as Docker Container (Pubblica come contenitore Docker) nella vista Navigator (Strumento di navigazione)][PUB01]

   * Sulla barra degli strumenti di hello Eclipse, fare clic su hello **pubblica** pulsante e quindi fare clic su **pubblica come contenitore Docker**.

      ![Comando Publish as Docker Container (Pubblica come contenitore Docker) sulla barra degli strumenti di Eclipse][PUB02]
      
    Hello **distribuire contenitore Docker in Azure** apre la procedura guidata.

    ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB03]

3. In hello **digitare un nome di immagine, selezionare il percorso dell'elemento hello e verificare un toobe host Docker utilizzato** finestra hello seguenti:

    a. In hello **nome immagine Docker** , immettere un nome univoco per l'host Docker. (hello verrà creata automaticamente un nome, ma è possibile modificarlo).

    b. Hello **host** area vengono visualizzati tutti gli host Docker che è già stato creato. Effettuare una delle seguenti hello:

    * Se si dispone di un host Docker esistente, è possibile distribuire il tooit app web.
    * Fare clic su un nuovo host Docker, toocreate **Aggiungi**.  
      
    Hello **creare Host Docker** verrà visualizzata la finestra di dialogo.

    ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB04a]

4. In hello **configurare hello nuova macchina virtuale** finestra, specificare le opzioni per l'host Docker seguenti hello. (la maggior parte delle opzioni hello hello generato automaticamente, ma è possibile modificare ciascuno di essi).

   a. **Nome**: immettere un nome univoco per l'host Docker hello. (È hello non uguali a quelli hello Nome immagine con Docker specificato in precedenza).

   b. **Sottoscrizione**: immettere hello sottoscrizione di Azure in uso per l'host.

   c. **Area**: entrare hello un'area geografica in cui si trova nell'host.

   d. In hello **del sistema operativo Host e le dimensioni** scheda:
     * **Host del sistema operativo**: immettere hello del sistema operativo per la macchina virtuale hello che contiene l'host.
     * **Dimensioni**: immettere una dimensione di macchina virtuale hello per l'host.

   e. In hello **gruppo di risorse** scheda:
     * **New resource group** (Nuovo gruppo di risorse): creare un nuovo gruppo di risorse per l'host.
     * **Existing resource group** (Gruppo di risorse esistente): immettere un gruppo di risorse dal proprio account Azure.

   f. In hello **rete** scheda:
     * **New virtual network** (Nuova rete virtuale): creare una nuova rete virtuale per l'host.
     * **Existing virtual network** (Rete virtuale esistente): immettere una rete virtuale esistente dal proprio account Azure.

   g. In hello **archiviazione** scheda:
     * **New storage account** (Nuovo account di archiviazione): creare un nuovo account di archiviazione per l'host.
     * **Existing storage account** (Account di archiviazione esistente): immettere un account di archiviazione esistente dal proprio account Azure.

5. Fare clic su **Avanti**.

6. In hello **configurare log nelle credenziali e le impostazioni delle porte** finestra, selezionare una delle seguenti opzioni hello:

    * **Import credentials from Azure Key Vault** (Importa credenziali da Azure Key Vault): specifica un set di credenziali salvato in precedenza e archiviato nella sottoscrizione di Azure.

      >[!NOTE]
      >Un insieme di credenziali chiave di Azure che viene creato con un account specifico o un'entità servizio non è accessibile automaticamente da un altro account o entità servizio che condivide sottoscrizione hello. tooallow un altro account o un servizio principale toouse hello insieme di credenziali chiave, è necessario utilizzare hello account hello tooadd portale Azure o un'entità servizio.

    * **New log in credentials** (Nuove credenziali di accesso): crea un nuovo set di credenziali di accesso. Se si seleziona questa opzione, hello seguenti:
    
      * In hello **credenziali VM** scheda, scegliere una delle seguenti hello opzioni per le credenziali di accesso di macchina virtuale hello dell'host Docker:

          * **Nome utente**: immettere un nome utente hello per le credenziali di accesso della macchina virtuale.
          * **Password** e **conferma**: immettere la password di hello per le credenziali di accesso della macchina virtuale.
          * **SSH**: immettere le impostazioni di hello Secure Shell (SSH) per l'host Docker. È possibile scegliere tra hello le opzioni seguenti:
            * **None** (Nessuna): specifica che la macchina virtuale non consentirà connessioni SSH.
            * **Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione via SSH.
            * **Import from directory** (Importa da directory): specifica una directory che contiene un set di impostazioni SSH salvate in precedenza. directory Hello deve contenere i seguenti due file hello:
                * *id_rsa*: contiene l'identificazione di hello RSA per un utente.
                * *id_rsa.pub*: hello chiave pubblica RSA utilizzata per l'autenticazione.
        
        ![Creare un host Docker][PUB05]

      * In hello **Docker Daemon credenziali** specificare hello le opzioni seguenti:

          * **Porta Daemon docker**: immettere la porta TCP hello univoca per l'host Docker.
          * **Protezione TLS**: immettere le impostazioni di hello Transport Layer Security per l'host Docker. È possibile scegliere tra hello le opzioni seguenti:
            * **None** (Nessuna): specifica che la macchina virtuale non consentirà connessioni TLS.
            * **Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione tramite TLS.
            * **Import from directory** (Importa da directory): specifica una directory che contiene un set di impostazioni TLS salvate in precedenza. In particolare, directory hello deve contenere i seguenti sei file hello:
                * *CA.PEM* e *ca key.pem*: contengono certificato hello e una chiave pubblica per hello TLS autorità di certificazione.
                * *CERT.PEM* e *key.pem*: contengono certificato client hello e una chiave pubblica che viene utilizzata per l'autenticazione TLS.
                * *Server.PEM* e *server key.pem*: contengono certificato server hello e una chiave pubblica per host hello.

        ![Creare un host Docker][PUB06]

7. Dopo avere immesso le precedenti informazioni hello, fare clic su **fine**.

8. In hello **distribuire contenitore Docker in Azure** procedura guidata, fare clic su **Avanti**.

   ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB07]

9. In hello **configurare hello Docker contenitore toobe creato** finestra hello seguenti:

   a. In hello **nome del contenitore Docker** , immettere un nome univoco per il contenitore Docker.

   b. Scegliere una delle seguenti immagini Docker hello:
     * **Predefined Docker image** (Immagine Docker predefinita): specifica un'immagine preesistente in Azure.

       >[!NOTE]
       >elenco di Hello delle immagini Docker in questa casella è costituito da diverse immagini che hello Azure Toolkit è stato configurato toopatch in modo che l'elemento viene distribuita automaticamente.

     * **Custom Dockerfile** (Dockerfile personalizzato): specifica un Dockerfile salvato in precedenza nel computer locale.

       >[!NOTE]
       >Questa è una funzionalità più avanzata per gli sviluppatori che desiderano toodeploy i propri Dockerfile. È invece backup toodevelopers che utilizzano questo tooensure opzione i Dockerfile compilato correttamente. Hello Azure Toolkit non convalidare il contenuto di hello in un Dockerfile personalizzato, in modo distribuzione hello potrebbe non riuscire se hello Dockerfile presenta problemi. Inoltre, hello Azure Toolkit prevede hello personalizzato Dockerfile toocontain un artefatto di app web, e verrà eseguito un tentativo tooopen una connessione HTTP. Pubblicando un diverso tipo di elemento, gli sviluppatori potrebbero ricevere errori non gravi dopo la distribuzione.

   c. **Le impostazioni delle porte**: immettere hello univoco TCP binding delle porte per il contenitore Docker.

     ![finestra di Hello Configura hello Docker contenitore toobe creato][PUB08]

10. Dopo aver completato tutti i passaggi precedenti, hello, fare clic su **fine**.

Hello Azure Toolkit inizia il tooAzure app web in un contenitore Docker. 

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

Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].

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
[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/

[sito Web di Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png