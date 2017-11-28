---
title: aaaCreate e la connessione di database MySQL tooa in Azure
description: Informazioni su come toouse hello toocreate portale Azure un database MySQL e quindi connettersi tooit da un'app web PHP in Azure.
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
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="ccfd9-103">Creazione e la connessione di database MySQL tooa in Azure</span><span class="sxs-lookup"><span data-stu-id="ccfd9-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="ccfd9-104">Questa esercitazione viene illustrato come database MySQL toocreate hello [portale di Azure](https://portal.azure.com) (provider [ClearDB](http://www.cleardb.com/)) e come tooit tooconnect da PHP web app in esecuzione in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ccfd9-105">È anche possibile creare un database MySQL come parte di un [modello di applicazione Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="ccfd9-106">Creare un database MySQL nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ccfd9-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="ccfd9-107">un database MySQL nel portale di Azure hello toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="ccfd9-108">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ccfd9-109">Scegliere dal menu a sinistra hello **New** > **dati e archiviazione** > **MySQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Creare un database MySQL in Azure: avvio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="ccfd9-111">Nel nuovo MySQL Database hello [pannello](azure-portal-overview.md), configurare il nuovo database MySQL nel modo seguente (*pannello*: una pagina del portale che consente di aprire orizzontalmente):</span><span class="sxs-lookup"><span data-stu-id="ccfd9-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="ccfd9-112">**Nome database**: digitare un nome identificabile in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="ccfd9-113">**Sottoscrizione**: scegliere hello sottoscrizione toouse</span><span class="sxs-lookup"><span data-stu-id="ccfd9-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="ccfd9-114">**Tipo di database**: selezionare **Shared** per i livelli basso costo o disponibili, o **dedicato** tooget risorse dedicate.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="ccfd9-115">**Gruppo di risorse**: Aggiungi tooan di hello database MySQL esistente [gruppo di risorse](azure-resource-manager/resource-group-overview.md) o inserirlo in una nuova.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="ccfd9-116">Risorse hello nello stesso gruppo può essere facilmente gestito insieme.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="ccfd9-117">**Percorso**: selezionare un tooyou Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="ccfd9-118">Quando si aggiungono tooan gruppo di risorse esistente, si è il percorso del gruppo di risorse toohello bloccato.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="ccfd9-119">**Piano tariffario**: fare clic su **Piano tariffario**, quindi selezionare un'opzione di prezzo (il livello **Mercurio** è gratuito) e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="ccfd9-120">**Note legali**: fare clic su **legali**, esaminare i dettagli di acquisto hello e fare clic su **acquistare**.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="ccfd9-121">**PIN toodashboard**: selezionare se si desidera tooaccess direttamente dal dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="ccfd9-122">Questa opzione è particolarmente utile se ancora non si ha familiarità con la navigazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="ccfd9-123">Hello seguente schermata è solo un esempio di come è possibile configurare il database MySQL.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Creare un database MySQL in Azure: configurazione](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="ccfd9-125">Al termine della configurazione, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-125">When you're done configuring, click **Create**.</span></span>

    ![Creare un database MySQL in Azure: creazione](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="ccfd9-127">Viene visualizzata una notifica popup che informa che la distribuzione è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="ccfd9-129">Al termine della distribuzione verrà visualizzata un'altra finestra popup.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="ccfd9-130">portale Hello verrà aperto automaticamente pannello del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="ccfd9-131">La connessione di database MySQL tooyour</span><span class="sxs-lookup"><span data-stu-id="ccfd9-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="ccfd9-132">informazioni di connessione hello toosee per il nuovo database MySQL, fare semplicemente clic **proprietà** nel pannello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Creare un database MySQL in Azure: pannello Database MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="ccfd9-134">È ora possibile usare le informazioni di connessione in qualsiasi app Web.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="ccfd9-135">Un esempio che illustra come informazioni di connessione hello toouse da una semplice app PHP sono disponibile [qui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="ccfd9-136">Connettersi a un'app web Laravel (da get PHP hello esercitazione introduttiva)</span><span class="sxs-lookup"><span data-stu-id="ccfd9-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="ccfd9-137">Si supponga di esercitazione hello appena terminato [creare, configurare e distribuire un tooAzure di app web PHP](app-service-web/app-service-web-php-get-started.md) e avere un [Laravel](https://www.laravel.com/) app web in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="ccfd9-138">È possibile aggiungere facilmente app Laravel tooyour funzionalità di database.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="ccfd9-139">Segui i passaggi di hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="ccfd9-140">Hello passaggi seguenti presuppongono che sono state esercitazione hello [creare, configurare e distribuire un tooAzure di app web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="ccfd9-141">Configurare app Laravel hello del database MySQL di toohello toopoint di ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="ccfd9-142">toodo, aprire `.env` dall'app Laravel directory radice e configurare le opzioni di database MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="ccfd9-143">In hello **proprietà** pannello nome hello del database MySQL può o potrebbe non essere visualizzato hello uno in hello **nome del DATABASE** campo.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="ccfd9-144">È preferibile toocheck hello Database parametro in hello **stringa di connessione** campo.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="ccfd9-146">più rapido tooverify modo di avere accesso MySQL ora Hello è toouse [lo scaffolding di autenticazione predefinito di Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="ccfd9-147">Nel terminale della riga di comando hello, eseguire hello seguendo i comandi dalla directory radice dell'applicazione Laravel:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="ccfd9-148">Hello primo comando crea tabelle hello in Azure in base alle migrazioni predefinite in hello `database/migrations` directory e secondo comando hello strutture hello viste di base e le route per l'autenticazione e registrazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="ccfd9-149">Eseguire subito il server di sviluppo hello:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="ccfd9-150">Nel browser hello, passare toohttp://localhost:8000 e registrare un nuovo utente, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Connessione database tooMySQL in Azure - registrazione utente](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="ccfd9-152">Eseguire la registrazione di hello completa dei messaggi di richiesta dell'interfaccia utente di hello.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="ccfd9-153">Dopo aver completato la registrazione, l'utente accede in automatico.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-153">Once registration completes, you will be logged in.</span></span>

    ![Connessione database tooMySQL in Azure - registrazione utente](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="ccfd9-155">Ora si sviluppa l'app nei database di MySQL hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="ccfd9-156">A questo punto, è sufficiente tooreplicate il `.env` impostazioni tooyour Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="ccfd9-157">Eseguire hello seguendo i comandi CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="ccfd9-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="ccfd9-158">Successivamente, eseguire il commit e push tooAzure hello le modifiche locali apportate in precedenza durante l'esecuzione `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="ccfd9-159">Sfoglia toohello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="ccfd9-160">Accedere con le credenziali utente hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-160">Log in using hello user credentials you created earlier.</span></span>

    ![Connessione database tooMySQL in Azure - Sfoglia tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="ccfd9-162">Dopo l'accesso, verrà visualizzata hello descrittivo schermata di post-login.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![La connessione a database tooMySQL in Azure - connesso](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="ccfd9-164">Complimenti, l'app Web PHP di Azure dispone ora di accesso ai dati del database MySQL.</span><span class="sxs-lookup"><span data-stu-id="ccfd9-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccfd9-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccfd9-165">Next steps</span></span>
<span data-ttu-id="ccfd9-166">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ccfd9-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
