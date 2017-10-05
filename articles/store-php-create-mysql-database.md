---
title: Creare e connettersi a un database MySQL in Azure
description: Informazioni su come usare il portale di Azure per creare un database MySQL e connettersi al database da un'app Web PHP in Azure.
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="1c75f-103">Creare e connettersi a un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="1c75f-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="1c75f-104">Questa esercitazione spiega come creare un database MySQL nel [portale di Azure](https://portal.azure.com) (provider [ClearDB](http://www.cleardb.com/)) e come connettersi al database da un'app Web PHP in esecuzione sul [Servizio app di Azure](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1c75f-105">È anche possibile creare un database MySQL come parte di un [modello di applicazione Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="1c75f-106">Creare un database MySQL nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c75f-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="1c75f-107">Per creare un database MySQL nel portale di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1c75f-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="1c75f-108">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c75f-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c75f-109">Nel menu a sinistra fare clic su **Nuovo** > **Dati e archiviazione** > **Database MySQL**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Creare un database MySQL in Azure: avvio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="1c75f-111">Nel [pannello](azure-portal-overview.md)Nuovo database MySQL, configurare il nuovo database MySQL come indicato di seguito (*pannello*: una pagina del portale che si apre orizzontalmente):</span><span class="sxs-lookup"><span data-stu-id="1c75f-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="1c75f-112">**Nome database**: digitare un nome identificabile in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="1c75f-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="1c75f-113">**Sottoscrizione**: scegliere la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="1c75f-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="1c75f-114">**Tipo database**: selezionare **Condiviso** per i livelli gratuiti o a basso costo oppure **Dedicato** per ottenere risorse dedicate.</span><span class="sxs-lookup"><span data-stu-id="1c75f-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="1c75f-115">**Gruppo di risorse**: aggiungere il database MySQL a un [gruppo di risorse](azure-resource-manager/resource-group-overview.md) esistente o inserirlo in un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="1c75f-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="1c75f-116">Le risorse all'interno dello stesso gruppo possono essere facilmente gestite insieme.</span><span class="sxs-lookup"><span data-stu-id="1c75f-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="1c75f-117">**Località**: scegliere una località vicina.</span><span class="sxs-lookup"><span data-stu-id="1c75f-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="1c75f-118">Quando si aggiunge il database a un gruppo di risorse esistente, l'utente è vincolato alla località del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1c75f-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="1c75f-119">**Piano tariffario**: fare clic su **Piano tariffario**, quindi selezionare un'opzione di prezzo (il livello **Mercurio** è gratuito) e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="1c75f-120">**Note legali**: fare clic su **Note legali**, esaminare i dettagli dell'acquisto e fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="1c75f-121">**Aggiungi al dashboard**: selezionare se si desidera accedere al database direttamente dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="1c75f-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="1c75f-122">Questa opzione è particolarmente utile se ancora non si ha familiarità con la navigazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="1c75f-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="1c75f-123">La schermata seguente rappresenta solo un esempio delle modalità in cui è possibile configurare il database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1c75f-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Creare un database MySQL in Azure: configurazione](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="1c75f-125">Al termine della configurazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-125">When you're done configuring, click **Create**.</span></span>

    ![Creare un database MySQL in Azure: creazione](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="1c75f-127">Viene visualizzata una notifica popup che informa che la distribuzione è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="1c75f-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="1c75f-129">Al termine della distribuzione verrà visualizzata un'altra finestra popup.</span><span class="sxs-lookup"><span data-stu-id="1c75f-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="1c75f-130">Il portale apre il pannello del database MySQL in automatico.</span><span class="sxs-lookup"><span data-stu-id="1c75f-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="1c75f-131">Connettersi al database MySQL</span><span class="sxs-lookup"><span data-stu-id="1c75f-131">Connect to your MySQL database</span></span>
<span data-ttu-id="1c75f-132">Per visualizzare le informazioni di connessione del nuovo database MySQL, fare clic su **Proprietà** nel pannello dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1c75f-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Creare un database MySQL in Azure: pannello Database MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="1c75f-134">È ora possibile usare le informazioni di connessione in qualsiasi app Web.</span><span class="sxs-lookup"><span data-stu-id="1c75f-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="1c75f-135">[Qui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)è disponibile un esempio che illustra come usare le informazioni di connessione da una semplice app PHP.</span><span class="sxs-lookup"><span data-stu-id="1c75f-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="1c75f-136">Connettere un'app web Laravel (dall'esercitazione introduttiva di PHP)</span><span class="sxs-lookup"><span data-stu-id="1c75f-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="1c75f-137">Si supponga che sia stata completata l'esercitazione [Creare, configurare e distribuire un'app Web PHP in Azure](app-service-web/app-service-web-php-get-started.md) e che un'app Web [Laravel](https://www.laravel.com/) sia in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="1c75f-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="1c75f-138">È possibile aggiungere funzionalità di database all'app Laravel in modo semplice.</span><span class="sxs-lookup"><span data-stu-id="1c75f-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="1c75f-139">Seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1c75f-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="1c75f-140">Per questa procedura si presuppone che sia stata completata l'esercitazione [Creare, configurare e distribuire un'app Web PHP in Azure](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1c75f-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="1c75f-141">Configurare l'app Laravel nell'ambiente di sviluppo locale in modo che punti al database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1c75f-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="1c75f-142">A tale scopo, aprire `.env` dalla directory radice dell'app Laravel e configurare le opzioni del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1c75f-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="1c75f-143">Nel pannello **Proprietà** il nome del database MySQL potrebbe non essere l'unico visualizzato nel campo **Nome database**.</span><span class="sxs-lookup"><span data-stu-id="1c75f-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="1c75f-144">È consigliabile controllare il parametro Database nel campo **Stringa di connessione** .</span><span class="sxs-lookup"><span data-stu-id="1c75f-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="1c75f-146">A questo punto, il modo più rapido per verificare di avere accesso a MySQL è usare lo [scaffolding di autenticazione predefinito di Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="1c75f-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="1c75f-147">Nel terminale della riga di comando eseguire i comandi seguenti dalla directory radice dell'app Laravel:</span><span class="sxs-lookup"><span data-stu-id="1c75f-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="1c75f-148">Il primo comando crea le tabelle in Azure in base alle migrazioni predefinite nella directory `database/migrations`, mentre il secondo comando esegue lo scaffolding delle viste e delle route di base per la registrazione e l'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1c75f-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="1c75f-149">A questo punto, eseguire il server di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="1c75f-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="1c75f-150">Nel browser accedere ad http://localhost:8000 e registrare un nuovo utente come illustrato:</span><span class="sxs-lookup"><span data-stu-id="1c75f-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Connettersi al database MySQL in Azure: registrazione utente](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="1c75f-152">Seguire i prompt dell'interfaccia utente per completare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="1c75f-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="1c75f-153">Dopo aver completato la registrazione, l'utente accede in automatico.</span><span class="sxs-lookup"><span data-stu-id="1c75f-153">Once registration completes, you will be logged in.</span></span>

    ![Connettersi al database MySQL in Azure: registrazione utente](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="1c75f-155">Si sta sviluppando l'app con il database MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="1c75f-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="1c75f-156">A questo punto, è sufficiente replicare le impostazioni `.env` nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c75f-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="1c75f-157">Eseguire i comandi seguenti dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="1c75f-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="1c75f-158">Successivamente, eseguire il commit e il push in Azure delle modifiche locali apportate in precedenza durante l'esecuzione di `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="1c75f-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="1c75f-159">Passare all'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c75f-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="1c75f-160">Accedere usando le credenziali utente create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1c75f-160">Log in using the user credentials you created earlier.</span></span>

    ![Connettersi al database MySQL in Azure: passare all'app Web di Azure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="1c75f-162">Dopo l'accesso, verrà visualizzata una schermata descrittiva.</span><span class="sxs-lookup"><span data-stu-id="1c75f-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Connettersi al database MySQL in Azure: accesso eseguito](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="1c75f-164">Complimenti, l'app Web PHP di Azure dispone ora di accesso ai dati del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="1c75f-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c75f-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c75f-165">Next steps</span></span>
<span data-ttu-id="1c75f-166">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="1c75f-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
