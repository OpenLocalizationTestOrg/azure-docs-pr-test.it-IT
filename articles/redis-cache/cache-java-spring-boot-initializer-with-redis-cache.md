---
title: Come configurare un'app Spring Boot Initializer per l'uso della cache Redis
description: Informazioni su come configurare un'applicazione Spring Boot creata con Spring Initializr per l'uso di Cache Redis di Azure.
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
ms.openlocfilehash: fb3fc96a2136b7c326bb0eb291b7204e7acf0190
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="a98e1-104">Come configurare un'app Spring Boot Initializer per l'uso della cache Redis</span><span class="sxs-lookup"><span data-stu-id="a98e1-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="a98e1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a98e1-105">Overview</span></span>

<span data-ttu-id="a98e1-106">**[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello enterprise.</span><span class="sxs-lookup"><span data-stu-id="a98e1-106">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a98e1-107">Uno dei progetti più comuni che si basa su questa piattaforma è [Spring Boot], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="a98e1-107">One of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="a98e1-108">Per semplificare le operazioni iniziali con Spring Boot per gli sviluppatori, alcuni pacchetti Spring Boot di esempio sono disponibili all'indirizzo <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="a98e1-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="a98e1-109">Oltre a consentire di scegliere dall'elenco di progetti Spring Boot di base, **[Spring Initializr]** semplifica le operazioni iniziali degli sviluppatori per la creazione di applicazioni Spring Boot personalizzate.</span><span class="sxs-lookup"><span data-stu-id="a98e1-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="a98e1-110">Questo articolo illustra in modo dettagliato come creare una cache Redis tramite il portale di Azure, come usare **Spring Initializr** per creare un'applicazione personalizzata e quindi come creare un'applicazione Web Java che archivia e recupera dati tramite la cache Redis.</span><span class="sxs-lookup"><span data-stu-id="a98e1-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98e1-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a98e1-111">Prerequisites</span></span>

<span data-ttu-id="a98e1-112">I prerequisiti seguenti sono necessari per seguire le procedure disponibili in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="a98e1-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="a98e1-113">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="a98e1-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="a98e1-114">[Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versione 1.7 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a98e1-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="a98e1-115">[Apache Maven](http://maven.apache.org/), versione 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a98e1-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="a98e1-116">Creare una cache Redis in Azure</span><span class="sxs-lookup"><span data-stu-id="a98e1-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="a98e1-117">Passare al portale di Azure all'indirizzo <https://portal.azure.com/> e fare clic sulla voce **+Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="a98e1-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Portale di Azure][AZ01]

1. <span data-ttu-id="a98e1-119">Fare clic su **Database** e quindi su **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="a98e1-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portale di Azure][AZ02]

1. <span data-ttu-id="a98e1-121">Nella pagina **Nuova cache Redis** immettere il valore di **Nome DNS** per la cache e quindi specificare **Sottoscrizione**, **Gruppo di risorse**, **Località** e **Piano tariffario**.</span><span class="sxs-lookup"><span data-stu-id="a98e1-121">On the **New Redis Cache** page, enter the **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="a98e1-122">Dopo avere specificato queste opzioni, fare clic su **Crea** per creare la cache.</span><span class="sxs-lookup"><span data-stu-id="a98e1-122">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Portale di Azure][AZ03]

1. <span data-ttu-id="a98e1-124">Al termine, la cache verrà elencata nel **dashboard** di Azure, nonché nelle pagine **Tutte le risorse** e **Caches Redis**.</span><span class="sxs-lookup"><span data-stu-id="a98e1-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="a98e1-125">È possibile fare clic sulla cache in una di queste posizioni per aprire la pagina delle proprietà per la cache.</span><span class="sxs-lookup"><span data-stu-id="a98e1-125">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Portale di Azure][AZ04]

1. <span data-ttu-id="a98e1-127">Quando viene visualizzata la pagina contenente l'elenco delle proprietà della cache, fare clic su **Chiavi di accesso** e copiare le chiavi di accesso per la cache.</span><span class="sxs-lookup"><span data-stu-id="a98e1-127">When the page which contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portale di Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="a98e1-129">Creare un'applicazione personalizzata tramite Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="a98e1-129">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="a98e1-130">Passare a <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="a98e1-130">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="a98e1-131">Specificare che si vuole generare un progetto **Maven** con **Java**, immettere i nomi di **Group** (Gruppo) e **Artifact** (Elemento) per l'applicazione e quindi fare clic sul collegamento relativo a **Switch to the full version** (Passa alla versione completa) di Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="a98e1-131">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opzioni di base di Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="a98e1-133">Spring Initializr userà i valori di **Group** (Gruppo) e **Artifact** (Elemento) per creare il nome del pacchetto, ad esempio *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="a98e1-133">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="a98e1-134">Scorrere verso il basso fino alla sezione **Web** e selezionare la casella relativa a **Web**, quindi scorrere verso il basso fino alla sezione **NoSQL** e selezionare la casella **Redis**. Scorrere infine fino alla parte inferiore della pagina e fare clic sul pulsante **Generate Project** (Genera progetto).</span><span class="sxs-lookup"><span data-stu-id="a98e1-134">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opzioni complete di Spring Initializr][SI02]

1. <span data-ttu-id="a98e1-136">Quando richiesto, scaricare il progetto in un percorso nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a98e1-136">When prompted, download the project to a path on your local computer.</span></span>

   ![Scaricare il progetto Spring Boot][SI03]

1. <span data-ttu-id="a98e1-138">Dopo l'estrazione dei file nel sistema locale, l'applicazione Spring Boot personalizzata sarà pronta per la modifica.</span><span class="sxs-lookup"><span data-stu-id="a98e1-138">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![File di progetto Spring Boot personalizzati][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="a98e1-140">Configurare il progetto Spring Boot personalizzato per l'uso della cache Redis</span><span class="sxs-lookup"><span data-stu-id="a98e1-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="a98e1-141">Individuare il file *application.properties* nella directory *resources* dell'app o creare il file se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="a98e1-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Individuare il file application.properties][RE01]

1. <span data-ttu-id="a98e1-143">Aprire il file *application.properties* in un editor di testo, quindi aggiungere le righe seguenti al file e sostituire i valori di esempio con le proprietà appropriate dalla cache:</span><span class="sxs-lookup"><span data-stu-id="a98e1-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6380

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modifica del file application.properties][RE02]

1. <span data-ttu-id="a98e1-145">Salvare e chiudere il file *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a98e1-145">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="a98e1-146">Creare una cartella denominata *controller* nella cartella di origine del pacchetto, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a98e1-146">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="a98e1-147">-oppure-</span><span class="sxs-lookup"><span data-stu-id="a98e1-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="a98e1-148">Creare un nuovo file denominato *HelloController.java* nella cartella *controller*.</span><span class="sxs-lookup"><span data-stu-id="a98e1-148">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="a98e1-149">Aprire il file in un editor di testo e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a98e1-149">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve the DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve the port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve the access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object to connect to your Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object to store/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string to your cache.
         jedis.set("greeting", "Hello World!");

         // Return the string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="a98e1-150">Sarà necessario sostituire `com.contoso.myazuredemo` con il nome del pacchetto per il progetto.</span><span class="sxs-lookup"><span data-stu-id="a98e1-150">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="a98e1-151">Salvare e chiudere il file *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="a98e1-151">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="a98e1-152">Compilare l'applicazione Spring Boot con Maven ed eseguirla, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a98e1-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a98e1-153">Testare l'app Web passando a http://localhost:8080 tramite un Web browser o usare una sintassi simile all'esempio seguente, se si hanno curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="a98e1-153">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="a98e1-154">Dovrebbe essere visualizzato il messaggio "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="a98e1-154">You should see the "Hello World!"</span></span> <span data-ttu-id="a98e1-155">dal controller di esempio, recuperato dinamicamente dalla cache Redis.</span><span class="sxs-lookup"><span data-stu-id="a98e1-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a98e1-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a98e1-156">Next steps</span></span>

<span data-ttu-id="a98e1-157">Per altre informazioni sull'uso delle applicazioni Spring Boot in Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="a98e1-157">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="a98e1-158">Distribuire un'applicazione Spring Boot nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a98e1-158">Deploy a Spring Boot Application to the Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="a98e1-159">Eseguire un'applicazione Spring Boot in un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="a98e1-159">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="a98e1-160">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a98e1-160">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a98e1-161">Per altre informazioni sulle operazioni iniziali nella cache Redis con Java in Azure, vedere [Come usare Cache Redis di Azure con Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="a98e1-161">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

<span data-ttu-id="a98e1-162">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="a98e1-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="a98e1-163">[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="a98e1-163">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="a98e1-164">[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="a98e1-164">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="a98e1-165">[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="a98e1-165">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="a98e1-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="a98e1-166">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="a98e1-167">[Spring Initializr]: https://start.spring.io/</span><span class="sxs-lookup"><span data-stu-id="a98e1-167">[Spring Initializr]: https://start.spring.io/</span></span>
<span data-ttu-id="a98e1-168">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="a98e1-168">[Spring Framework]: https://spring.io/</span></span>
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
