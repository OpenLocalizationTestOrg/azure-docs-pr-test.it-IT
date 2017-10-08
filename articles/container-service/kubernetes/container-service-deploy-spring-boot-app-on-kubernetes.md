---
title: aaaDeploy un'App di avvio molla su Kubernetes nel servizio contenitore di Azure | Documenti Microsoft
description: In questa esercitazione assiste l'utente tuttavia hello passaggi toodeploy un'applicazione di avvio Spring in un cluster Kubernetes in Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure

Hello  **[Spring Framework]**  è un framework open source più diffuso che consente agli sviluppatori Java di creare applicazioni API web e dispositivi mobili. Questa esercitazione viene utilizzato una app di esempio creata con [avvio Spring], un approccio basato su convenzione per l'utilizzo di tooget Spring in tempi brevi.

**[Kubernetes]**  e  **[Docker]**  sono soluzioni open source che consentono agli sviluppatori automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.

In questa esercitazione viene illustrato anche se la combinazione di queste due tecnologie comuni, open source di toodevelop e distribuire un tooMicrosoft di primavera avvio applicazione Azure. In particolare, utilizzare  *[avvio Spring]*  per lo sviluppo di applicazioni,  *[Kubernetes]*  per la distribuzione di contenitore e hello [Servizio contenitore di azure (ACS)] toohost l'applicazione.

### <a name="prerequisites"></a>Prerequisiti

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].
* Hello [Azure interfaccia della riga di comando (CLI)].
* Un [Java Developer Kit (JDK)] aggiornato.
* Lo strumento di compilazione [Maven] di Apache (versione 3).
* Un client [Git].
* Un client [Docker].

> [!NOTE]
>
> A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Creare hello avvio molla nell'applicazione web di Guida introduttiva di Docker

Hello seguendo i passaggi illustrati la creazione di un'applicazione web Spring avvio e il relativo test in locale.

1. Aprire un prompt dei comandi e creare toohold una directory locale dell'applicazione e spostarsi nella directory toothat; Per esempio:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - o-
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Directory toohello completata progetto modificato.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Utilizzare toobuild Maven e app di esempio hello esecuzione.
   ```
   mvn package spring-boot:run
   ```

1. Test hello web app esplorando toohttp://localhost:8080 o con il seguente hello `curl` comando:
   ```
   curl http://localhost:8080
   ```

1. Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World**

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Creare un Azure contenitore del Registro di sistema utilizzando hello CLI di Azure

1. Aprire un prompt dei comandi.

1. Accedi tooyour account di Azure:
   ```azurecli
   az login
   ```

1. Creare un gruppo di risorse per hello risorse di Azure utilizzate in questa esercitazione.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Creare un registro di sistema contenitore privato di Azure nel gruppo di risorse hello. esercitazione Hello inserisce hello app di esempio come un Docker immagine toothis del Registro di sistema nei passaggi successivi. Sostituire `wingtiptoysregistry` con un nome univoco per il registro.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Eseguire il push del Registro di sistema di app toohello contenitore

1. Passare toohello directory di configurazione per l'installazione di Maven (~/.m2/ predefinito o C:\Users\username\.m2) e aprire hello *Settings* file con un editor di testo.

1. Recuperare la password di hello per il Registro di sistema del contenitore da hello CLI di Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Aggiungere il nuovo tooa del Registro di sistema di Azure contenitore di id e password `<server>` insieme in hello *Settings* file.
Hello `id` e `username` sono il nome di hello del Registro di sistema hello. Hello utilizzare `password` valore dal comando precedente di hello (senza virgolette).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Passare una directory del progetto toohello completato per l'applicazione di avvio Spring (ad esempio, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completamento*") e aprire hello *pom.xml* file con un editor di testo.

1. Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema di contenitore di Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hello aggiornamento `<plugins>` insieme in hello *pom.xml* file in modo che hello `<plugin>` contiene hello server indirizzo e del Registro di sistema nome di accesso per il Registro di sistema di contenitore di Azure.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Passare directory del progetto toohello completato per l'applicazione di avvio molla ed eseguire hello comando toobuild hello Docker contenitore e push hello immagine toohello del Registro di sistema seguente:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Si potrebbe ricevere un messaggio di errore è simile tooone seguenti hello quando Maven inserisce hello immagine tooAzure:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Se questo errore si verifica, accedere tooAzure dalla riga di comando di Docker hello.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Effettuare quindi il push del contenitore:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Creare un Kubernetes Cluster in ACS utilizzando hello CLI di Azure

1. Creare un cluster Kubernetes nel servizio contenitore di Azure. Hello comando seguente crea un *kubernetes* cluster in hello *wingtiptoys kubernetes* risorse al gruppo *servizio contenitore di wingtiptoys* come cluster hello nome, e *wingtiptoys kubernetes* come prefisso DNS hello:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Questo comando potrebbe richiedere qualche minuto toocomplete.

1. Installare `kubectl` utilizzando hello CLI di Azure. Gli utenti di Linux potrebbero essere tooprefix questo comando con `sudo` poiché distribuisce hello Kubernetes CLI troppo`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Scaricare le informazioni di configurazione del cluster di hello, pertanto è possibile gestire il cluster dall'interfaccia web di hello Kubernetes e `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Distribuire hello immagine tooyour Kubernetes cluster

In questa esercitazione consente di distribuire app hello usando `kubectl`, quindi consentono di distribuzione hello tooexplore tramite l'interfaccia web di Kubernetes hello.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Distribuire con l'interfaccia web di hello Kubernetes

1. Aprire un prompt dei comandi.

1. Aprire hello sito Web di configurazione per il cluster Kubernetes nel browser predefinito:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Al sito Web di configurazione Kubernetes hello apre nel browser, fare clic su collegamento hello troppo**distribuire un'app nei contenitori**:

   ![Sito Web di configurazione di Kubernetes][KB01]

1. Quando hello **distribuire un'app nei contenitori** viene visualizzata la pagina, specificare hello le opzioni seguenti:

   a. Selezionare **Specify app details below** (Specificare più avanti i dettagli dell'app).

   b. Immettere il nome dell'applicazione di avvio molla per hello **nome App**, ad esempio: "*docker gs-spring-avvio*".

   c. Immettere l'immagine di contenitore e server di accesso da versioni precedenti per hello **immagine contenitore**, ad esempio: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Scegliere **esterno** per hello **servizio**.

   e. Specificare le porte interne ed esterne in hello **porta** e **porta di destinazione** caselle di testo.

   ![Sito Web di configurazione di Kubernetes][KB02]


1. Fare clic su **Distribuisci** contenitore hello toodeploy.

   ![Distribuire un contenitore][KB05]

1. Al termine della distribuzione dell'applicazione, l'applicazione Spring Boot verrà elencata in **Services** (Servizi).

   ![Servizi Kubernetes][KB06]

1. Se si fa clic sul collegamento hello per **endpoint esterni**, è possibile visualizzare l'applicazione di avvio Spring in esecuzione in Azure.

   ![Servizi Kubernetes][KB07]

   ![Esplorare l'app di esempio in Azure][SB02]


### <a name="deploy-with-kubectl"></a>Eseguire la distribuzione con kubectl

1. Aprire un prompt dei comandi.

1. Eseguire il contenitore in cluster Kubernetes hello utilizzando hello `kubectl run` comando. Assegnare un nome di servizio per l'app in Kubernetes e un nome di immagine completa hello. ad esempio:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   In questo comando:

   * nome del contenitore Hello `gs-spring-boot-docker` specificato immediatamente dopo hello `run` comando

   * Hello `--image` parametro specifica hello combinati di server di accesso e il nome immagine`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Esporre il cluster Kubernetes esternamente tramite hello `kubectl expose` comando. Specificare il nome del servizio, hello pubblico TCP porta utilizzata tooaccess hello app e la porta di destinazione interno hello su che l'app è in ascolto. ad esempio:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   In questo comando:

   * nome del contenitore Hello `gs-spring-boot-docker` specificato immediatamente dopo hello `expose deployment` comando

   * Hello `--type` parametro specifica di tale cluster hello Usa bilanciamento del carico

   * Hello `--port` parametro specifica hello pubblico la porta TCP 80. Accedere all'app hello su questa porta.

   * Hello `--target-port` parametro specifica hello interno la porta TCP 8080. servizio di bilanciamento del carico Hello inoltra le richieste tooyour app su questa porta.

1. Una volta distribuita l'applicazione hello toohello cluster, eseguire una query l'indirizzo IP esterno hello e aprirlo nel web browser:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Esplorare l'app di esempio in Azure][SB02]


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di avvio Spring in Azure, vedere hello seguenti articoli:

* [Distribuire un servizio App di Azure di toohello Spring avvio applicazione](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Distribuire un'applicazione di avvio molla su Linux in hello servizio contenitore di Azure](container-service-deploy-spring-boot-app-on-linux.md)

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

Per ulteriori informazioni sull'avvio Spring hello nel progetto di esempio Docker, vedere [avvio molla su Docker Introduzione].

Hello seguenti collegamenti fornisce informazioni aggiuntive sulla creazione di applicazioni Spring avvio:

* Per ulteriori informazioni sulla creazione di una semplice applicazione Spring avvio, vedere hello Spring Initializr in https://start.spring.io/.

Hello seguenti collegamenti forniscono informazioni aggiuntive sull'utilizzo di Kubernetes con Azure:

* [Introduzione a un cluster Kubernetes nel servizio contenitore](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Utilizzo di hello Kubernetes web dell'interfaccia utente con il servizio contenitore di Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Ulteriori informazioni sull'utilizzo dell'interfaccia della riga di comando Kubernetes sono disponibile in hello **kubectl** Guida dell'utente al <https://kubernetes.io/docs/user-guide/kubectl/>.

sito Web Kubernetes Hello sono diversi articoli che illustrano l'utilizzo di immagini in registri privati:

* [Configuring Service Accounts for Pods] (Configurazione degli account del servizio per i pod)
* [Namespaces] (Spazi dei nomi)
* [Pulling an Image from a Private Registry] (Effettuare il pull di un'immagine da un registro privato)

Per altri esempi per la modalità toouse immagini Docker personalizzato con Azure, vedere [utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux].

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[Servizio contenitore di azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/ (Framework di Spring)
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurazione degli account del servizio per i pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Spazi dei nomi)
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Effettuare il pull di un'immagine da un registro privato)

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
