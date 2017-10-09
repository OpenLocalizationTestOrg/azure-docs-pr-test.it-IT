---
title: aaaDeploy toohello un'applicazione di avvio Spring servizio App di Azure | Documenti Microsoft
description: In questa esercitazione fornisce le istruzioni sviluppatori tramite hello passaggi toodeploy hello Spring avvio introduzione web app tooAzure servizio App.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Distribuire un servizio App di Azure di toohello Spring avvio applicazione

Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale e uno dei progetti comuni a più di hello che si basa sulla piattaforma [Avvio spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.

In questa esercitazione assiste l'utente tramite la creazione di app web di molla avvio introduzione esempio hello e la distribuzione troppo[Azure App Service].

### <a name="prerequisites"></a>Prerequisiti

In ordine toocomplete hello passaggi di questa esercitazione, è necessario seguente hello toohave:

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].
* Un [Java Developer Kit (JDK)] aggiornato.
* Lo strumento di compilazione [Maven] di Apache (versione 3).
* Un client [Git].

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Creare app web Spring avvio introduzione hello

Hello passaggi seguenti verranno illustrati i passaggi di hello che sono necessari toocreate una semplice applicazione web di avvio molla ed eseguirne il test in locale.

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

1. Hello clone [Spring avvio Introduzione] progetto di esempio nella directory hello appena creato; ad esempio:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Cambiare il progetto completato toohello directory; Per esempio:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Compilare i file JAR hello utilizzando Maven; Per esempio:
   ```
   mvn package
   ```

1. Una volta hello web app è stata creata, modificare il file JAR di directory toohello e avviare l'app web hello; Per esempio:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Testare l'app web hello esplorando toohttp://localhost:8080 mediante un web browser o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:
   ```
   curl http://localhost:8080
   ```

1. Dovrebbe essere hello segue messaggio visualizzato: **Greetings da avvio Spring!**

   ![Esplora la app di esempio][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Creare un'app web di Azure con Java

Hello alla procedura seguente verrà illustrata hello passaggi toocreate un'App Web di Azure, configurare le impostazioni di hello necessario per Java e configurare le credenziali FTP.

1. Sfoglia toohello [portale di Azure] ed effettuare l'accesso.

1. Dopo aver eseguito l'accesso al tuo account nel portale di Azure hello, fare clic sull'icona di menu hello per **servizi App**:
   
   ![Portale di Azure][AZ01]

1. Quando hello **servizi App** viene visualizzata la pagina, fare clic su **+ Aggiungi** toocreate un nuovo servizio App.

   ![Creare un servizio app][AZ02]

1. Quando viene visualizzato l'elenco di hello di modelli di app web, fare clic sul collegamento hello per hello base App Web di Microsoft.

   ![Modelli di app Web][AZ03]

1. Quando viene visualizzata la pagina informazioni hello per il modello di App Web hello, fare clic su **crea**.

   ![Crea app Web][AZ04]

1. Specificare un nome univoco per l'app Web, quindi specificare eventuali impostazioni aggiuntive e scegliere **Crea**.

   ![Creare delle impostazioni app Web][AZ05]

1. Dopo aver creato l'app web, fare clic sull'icona di menu hello per **servizi App**, quindi fare clic su app web appena creato:

   ![Elenco delle app Web][AZ06]

1. Quando viene visualizzata l'app web, è possibile specificare la versione di Java hello utilizzando hello alla procedura seguente:

   a. Fare clic su hello **le impostazioni dell'applicazione** voce di menu.

   b. Scegliere **Java 8** per la versione di Java hello.

   c. Scegliere **più recente** per versione di hello secondaria Java.

   d. Scegliere **più recenti Tomcat 8.5** per contenitore web hello. (Questo contenitore non verrà effettivamente utilizzato; Azure userà il contenitore di hello dall'applicazione di avvio molla.)

   e. Fare clic su **Salva**.

   ![Impostazioni dell'applicazione][AZ07]

1. Specificare le credenziali di distribuzione FTP utilizzando hello alla procedura seguente:

   a. Fare clic su hello **le credenziali di distribuzione** voce di menu.

   b. Specificare il proprio nome utente e la password.

   c. Fare clic su **Salva**.

   ![Specificare le credenziali di distribuzione][AZ08]

1. Recuperare le informazioni di connessione FTP tramite hello alla procedura seguente:

   a. Fare clic su hello **le credenziali di distribuzione** voce di menu.

   b. Copiare il nome utente FTP completo e l'URL e salvate per la sezione successiva di hello di questa esercitazione.

   ![URL FTP e credenziali][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Distribuire il tooAzure app web di avvio della primavera

Hello passaggi verrà illustrati hello passaggi toodeploy tooAzure di app web la molla avvio.

1. Aprire un editor di testo come blocco note di Windows e incollare hello dopo il testo in un nuovo documento, quindi salvare il file hello come *Web. config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Dopo aver salvato hello *Web. config* del file system tooyour, connettere tooyour app web tramite FTP utilizzando URL hello, username e password da hello precedente sezione di questa esercitazione. ad esempio:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Cartella radice dell'app web modifica hello directory remota toohello (ovvero */sito/wwwroot*), quindi copiare il file JAR hello dall'applicazione di avvio molla e hello *Web. config* precedenti. ad esempio:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Dopo aver distribuito il file JAR e *Web. config* file tooyour web app, è necessario toorestart app web utilizzando hello portale di Azure:

   ![][AZ10]

1. Testare app web hello passando l'URL dell'app web tooyour mediante un web browser, o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Dovrebbe essere hello segue messaggio visualizzato: **Greetings da avvio Spring!**

   ![Esplora la app di esempio][SB02]

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:

* [Distribuire un'applicazione di avvio Spring in Linux in hello servizio contenitore di Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

Per ulteriori informazioni su depoying web App tooAzure tramite FTP, vedere [distribuire il servizio App utilizzando FTP/S di tooAzure app].

Per ulteriori informazioni sul progetto di esempio hello Spring avvio, vedere [Spring avvio Introduzione].

Per informazioni sulla Guida introduttiva a applicazioni Spring avvio, vedere hello **Initializr Spring** in https://start.spring.io/.

Per altre informazioni sulla configurazione delle impostazioni aggiuntive per l'app Web, vedere [Configurare app Web in Servizio app di Azure].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[Configurare app Web in Servizio app di Azure]: /azure/app-service-web/web-sites-configure
[distribuire il servizio App utilizzando FTP/S di tooAzure app]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Avvio spring]: http://projects.spring.io/spring-boot/
[Spring avvio Introduzione]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
