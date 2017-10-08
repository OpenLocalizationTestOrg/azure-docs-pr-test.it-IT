---
title: aaaHow tooconfigure toouse di app un inizializzatore di avvio Spring Cache Redis
description: Informazioni su come tooconfigure un'applicazione di avvio molla creata con hello Spring Initializr toouse Cache Redis di Azure.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cache Redis
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Come tooconfigure toouse di app un inizializzatore di avvio Spring Cache Redis

## <a name="overview"></a>Panoramica

Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale. Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome. gli sviluppatori toohelp iniziare con l'avvio della primavera, sono disponibili in diversi pacchetti di esempio Spring avvio <https://github.com/spring-guides/>. Inoltre toochoosing dall'elenco di hello di avvio di base Spring progetti, hello  **[Spring Initializr]**  consente agli sviluppatori di iniziare a utilizzare la creazione di applicazioni Spring avvio personalizzate.

Questo articolo vengono illustrati la creazione di una cache Redis tramite hello portale Azure, quindi usando hello **Spring Initializr** toocreate un'applicazione personalizzata e quindi la creazione di un linguaggio ' applicazione web che archivia e recupera i dati tramite il Cache redis.

## <a name="prerequisites"></a>Prerequisiti

Hello seguenti prerequisiti è necessari nei passaggi di hello ordine toofollow in questo articolo:

* Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].

* [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versione 1.7 o successiva.

* [Apache Maven](http://maven.apache.org/), versione 3.0 o versione successiva.

## <a name="create-a-redis-cache-on-azure"></a>Creare una cache Redis in Azure

1. Sfoglia toohello Azure portale in <https://portal.azure.com/> e fare clic su elemento hello per **+ nuovo**.

   ![Portale di Azure][AZ01]

1. Fare clic su **Database** e quindi su **Cache Redis**.

   ![Portale di Azure][AZ02]

1. In hello **nuova Cache Redis** pagina, immettere hello **nome DNS** per la cache, quindi specificare il **sottoscrizione**, **gruppo di risorse**,  **Percorso**, e **tariffario**. Dopo aver specificato queste opzioni, fare clic su **crea** toocreate la cache.

   ![Portale di Azure][AZ03]

1. Una volta completata la cache, si verrà visualizzato solo nella finestra di Azure **Dashboard**, nonché nel hello **tutte le risorse**, e **cache Redis** pagine. È possibile fare clic nella cache in qualsiasi tali percorsi tooopen hello pagina delle proprietà per la cache.

   ![Portale di Azure][AZ04]

1. Quando viene visualizzata la pagina hello contenente hello elenco di proprietà per la cache, fare clic su **le chiavi di accesso** e copiare le chiavi di accesso per la cache.

   ![Portale di Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Creare un'applicazione personalizzata utilizzando hello Spring Initializr

1. Sfoglia troppo<https://start.spring.io/>.

1. Specifica che si desidera toogenerate un **Maven** il progetto con **Java**, immettere hello **gruppo** e **Aritifact** nomi per l'applicazione, e quindi fare clic su collegamento hello troppo**versione completa di commutatore toohello** di hello Initializr molla.

   ![Opzioni di base di Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello Spring Initializr utilizzerà hello **gruppo** e **Aritifact** nome del pacchetto hello toocreate nomi, ad esempio: *com.contoso.myazuredemo*.
   >

1. Scorrere verso il basso toohello **Web** sezione e selezionare la casella di hello per **Web**, quindi scorrere verso il basso toohello **NoSQL** sezione e selezionare la casella di hello per **Redis**, quindi scorrere toohello parte inferiore della pagina hello e fare clic su pulsante hello troppo**generare progetto**.

   ![Opzioni complete di Spring Initializr][SI02]

1. Quando richiesto, scaricare percorso tooa del progetto hello nel computer locale.

   ![Scaricare il progetto Spring Boot personalizzato][SI03]

1. Dopo che sono stati estratti i file hello nel sistema locale, l'applicazione di avvio Spring personalizzata sarà pronto per la modifica.

   ![File del progetto Spring Boot personalizzato][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Configurare il toouse Spring avvio personalizzato la Cache Redis

1. Individuare hello *application.properties* file hello *risorse* directory dell'app, o se non esiste già, creare file hello.

   ![Individuare il file application.properties hello][RE01]

1. Aprire hello *application.properties* file in un editor di testo e aggiungere i seguenti file toohello righe hello e sostituire i valori di esempio hello con le proprietà appropriate hello dalla cache:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modifica file application.properties hello][RE02]

1. Salvare e chiudere hello *application.properties* file.

1. Creare una cartella denominata *controller* nella cartella di origine hello per il pacchetto; ad esempio:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -oppure-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Creare un nuovo file denominato *HelloController.java* in hello *controller* cartella. Aprire il file hello in un editor di testo e aggiungere hello tooit di codice seguente:

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   In cui è necessario tooreplace `com.contoso.myazuredemo` con nome hello del pacchetto per il progetto.

1. Salvare e chiudere hello *HelloController.java* file.

1. Compilare l'applicazione Spring Boot con Maven ed eseguirla, ad esempio:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testare l'app web hello esplorando toohttp://localhost:8080 mediante un web browser o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:

   ```shell
   curl http://localhost:8080
   ```

   Dovrebbe essere hello "Hello World!" dal controller di esempio, recuperato dinamicamente dalla cache Redis.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:

* [Distribuire un servizio App di Azure di toohello Spring avvio applicazione](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Esegue un'applicazione di avvio molla su un Kubernetes Cluster in hello servizio contenitore di Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

Per ulteriori informazioni sull'utilizzo di Cache Redis con Java in Azure, vedere [come toouse Cache Redis di Azure con Java][Redis Cache with Java].

<!-- URL List -->

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
