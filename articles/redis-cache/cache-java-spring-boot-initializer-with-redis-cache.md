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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="02f97-104">Come tooconfigure toouse di app un inizializzatore di avvio Spring Cache Redis</span><span class="sxs-lookup"><span data-stu-id="02f97-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="02f97-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="02f97-105">Overview</span></span>

<span data-ttu-id="02f97-106">Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="02f97-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="02f97-107">Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="02f97-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="02f97-108">gli sviluppatori toohelp iniziare con l'avvio della primavera, sono disponibili in diversi pacchetti di esempio Spring avvio <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="02f97-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="02f97-109">Inoltre toochoosing dall'elenco di hello di avvio di base Spring progetti, hello  **[Spring Initializr]**  consente agli sviluppatori di iniziare a utilizzare la creazione di applicazioni Spring avvio personalizzate.</span><span class="sxs-lookup"><span data-stu-id="02f97-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="02f97-110">Questo articolo vengono illustrati la creazione di una cache Redis tramite hello portale Azure, quindi usando hello **Spring Initializr** toocreate un'applicazione personalizzata e quindi la creazione di un linguaggio ' applicazione web che archivia e recupera i dati tramite il Cache redis.</span><span class="sxs-lookup"><span data-stu-id="02f97-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02f97-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02f97-111">Prerequisites</span></span>

<span data-ttu-id="02f97-112">Hello seguenti prerequisiti è necessari nei passaggi di hello ordine toofollow in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="02f97-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="02f97-113">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="02f97-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="02f97-114">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="02f97-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="02f97-115">[Apache Maven](http://maven.apache.org/), versione 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="02f97-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="02f97-116">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="02f97-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="02f97-117">Sfoglia toohello Azure portale in <https://portal.azure.com/> e fare clic su elemento hello per **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="02f97-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Portale di Azure][AZ01]

1. <span data-ttu-id="02f97-119">Fare clic su **Database** e quindi su **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="02f97-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portale di Azure][AZ02]

1. <span data-ttu-id="02f97-121">In hello **nuova Cache Redis** pagina, immettere hello **nome DNS** per la cache, quindi specificare il **sottoscrizione**, **gruppo di risorse**,  **Percorso**, e **tariffario**.</span><span class="sxs-lookup"><span data-stu-id="02f97-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="02f97-122">Dopo aver specificato queste opzioni, fare clic su **crea** toocreate la cache.</span><span class="sxs-lookup"><span data-stu-id="02f97-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Portale di Azure][AZ03]

1. <span data-ttu-id="02f97-124">Una volta completata la cache, si verrà visualizzato solo nella finestra di Azure **Dashboard**, nonché nel hello **tutte le risorse**, e **cache Redis** pagine.</span><span class="sxs-lookup"><span data-stu-id="02f97-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="02f97-125">È possibile fare clic nella cache in qualsiasi tali percorsi tooopen hello pagina delle proprietà per la cache.</span><span class="sxs-lookup"><span data-stu-id="02f97-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portale di Azure][AZ04]

1. <span data-ttu-id="02f97-127">Quando viene visualizzata la pagina hello contenente hello elenco di proprietà per la cache, fare clic su **le chiavi di accesso** e copiare le chiavi di accesso per la cache.</span><span class="sxs-lookup"><span data-stu-id="02f97-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portale di Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="02f97-129">Creare un'applicazione personalizzata utilizzando hello Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="02f97-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="02f97-130">Sfoglia troppo<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="02f97-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="02f97-131">Specifica che si desidera toogenerate un **Maven** il progetto con **Java**, immettere hello **gruppo** e **Aritifact** nomi per l'applicazione, e quindi fare clic su collegamento hello troppo**versione completa di commutatore toohello** di hello Initializr molla.</span><span class="sxs-lookup"><span data-stu-id="02f97-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Opzioni di base di Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="02f97-133">Hello Spring Initializr utilizzerà hello **gruppo** e **Aritifact** nome del pacchetto hello toocreate nomi, ad esempio: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="02f97-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="02f97-134">Scorrere verso il basso toohello **Web** sezione e selezionare la casella di hello per **Web**, quindi scorrere verso il basso toohello **NoSQL** sezione e selezionare la casella di hello per **Redis**, quindi scorrere toohello parte inferiore della pagina hello e fare clic su pulsante hello troppo**generare progetto**.</span><span class="sxs-lookup"><span data-stu-id="02f97-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Opzioni complete di Spring Initializr][SI02]

1. <span data-ttu-id="02f97-136">Quando richiesto, scaricare percorso tooa del progetto hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="02f97-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Scaricare il progetto Spring Boot personalizzato][SI03]

1. <span data-ttu-id="02f97-138">Dopo che sono stati estratti i file hello nel sistema locale, l'applicazione di avvio Spring personalizzata sarà pronto per la modifica.</span><span class="sxs-lookup"><span data-stu-id="02f97-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![File del progetto Spring Boot personalizzato][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="02f97-140">Configurare il toouse Spring avvio personalizzato la Cache Redis</span><span class="sxs-lookup"><span data-stu-id="02f97-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="02f97-141">Individuare hello *application.properties* file hello *risorse* directory dell'app, o se non esiste già, creare file hello.</span><span class="sxs-lookup"><span data-stu-id="02f97-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Individuare il file application.properties hello][RE01]

1. <span data-ttu-id="02f97-143">Aprire hello *application.properties* file in un editor di testo e aggiungere i seguenti file toohello righe hello e sostituire i valori di esempio hello con le proprietà appropriate hello dalla cache:</span><span class="sxs-lookup"><span data-stu-id="02f97-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modifica file application.properties hello][RE02]

1. <span data-ttu-id="02f97-145">Salvare e chiudere hello *application.properties* file.</span><span class="sxs-lookup"><span data-stu-id="02f97-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="02f97-146">Creare una cartella denominata *controller* nella cartella di origine hello per il pacchetto; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02f97-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="02f97-147">-oppure-</span><span class="sxs-lookup"><span data-stu-id="02f97-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="02f97-148">Creare un nuovo file denominato *HelloController.java* in hello *controller* cartella.</span><span class="sxs-lookup"><span data-stu-id="02f97-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="02f97-149">Aprire il file hello in un editor di testo e aggiungere hello tooit di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="02f97-149">Open hello file in a text editor and add hello following code tooit:</span></span>

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
   
   <span data-ttu-id="02f97-150">In cui è necessario tooreplace `com.contoso.myazuredemo` con nome hello del pacchetto per il progetto.</span><span class="sxs-lookup"><span data-stu-id="02f97-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="02f97-151">Salvare e chiudere hello *HelloController.java* file.</span><span class="sxs-lookup"><span data-stu-id="02f97-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="02f97-152">Compilare l'applicazione Spring Boot con Maven ed eseguirla, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02f97-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="02f97-153">Testare l'app web hello esplorando toohttp://localhost:8080 mediante un web browser o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="02f97-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="02f97-154">Dovrebbe essere hello "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="02f97-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="02f97-155">dal controller di esempio, recuperato dinamicamente dalla cache Redis.</span><span class="sxs-lookup"><span data-stu-id="02f97-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02f97-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02f97-156">Next steps</span></span>

<span data-ttu-id="02f97-157">Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="02f97-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="02f97-158">Distribuire un servizio App di Azure di toohello Spring avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="02f97-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="02f97-159">Esegue un'applicazione di avvio molla su un Kubernetes Cluster in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="02f97-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="02f97-160">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="02f97-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="02f97-161">Per ulteriori informazioni sull'utilizzo di Cache Redis con Java in Azure, vedere [come toouse Cache Redis di Azure con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="02f97-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

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
