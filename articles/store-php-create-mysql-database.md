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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Creazione e la connessione di database MySQL tooa in Azure
Questa esercitazione viene illustrato come database MySQL toocreate hello [portale di Azure](https://portal.azure.com) (provider [ClearDB](http://www.cleardb.com/)) e come tooit tooconnect da PHP web app in esecuzione in [Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> È anche possibile creare un database MySQL come parte di un [modello di applicazione Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Creare un database MySQL nel portale di Azure
un database MySQL nel portale di Azure hello toocreate hello seguenti:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra hello **New** > **dati e archiviazione** > **MySQL Database**.

    ![Creare un database MySQL in Azure: avvio](./media/store-php-create-mysql-database/create-db-1-start.png)
3. Nel nuovo MySQL Database hello [pannello](azure-portal-overview.md), configurare il nuovo database MySQL nel modo seguente (*pannello*: una pagina del portale che consente di aprire orizzontalmente):

   * **Nome database**: digitare un nome identificabile in modo univoco.
   * **Sottoscrizione**: scegliere hello sottoscrizione toouse
   * **Tipo di database**: selezionare **Shared** per i livelli basso costo o disponibili, o **dedicato** tooget risorse dedicate.
   * **Gruppo di risorse**: Aggiungi tooan di hello database MySQL esistente [gruppo di risorse](azure-resource-manager/resource-group-overview.md) o inserirlo in una nuova. Risorse hello nello stesso gruppo può essere facilmente gestito insieme.
   * **Percorso**: selezionare un tooyou Chiudi percorso. Quando si aggiungono tooan gruppo di risorse esistente, si è il percorso del gruppo di risorse toohello bloccato.
   * **Piano tariffario**: fare clic su **Piano tariffario**, quindi selezionare un'opzione di prezzo (il livello **Mercurio** è gratuito) e fare clic su **Seleziona**.
   * **Note legali**: fare clic su **legali**, esaminare i dettagli di acquisto hello e fare clic su **acquistare**.
   * **PIN toodashboard**: selezionare se si desidera tooaccess direttamente dal dashboard hello. Questa opzione è particolarmente utile se ancora non si ha familiarità con la navigazione nel portale.

     Hello seguente schermata è solo un esempio di come è possibile configurare il database MySQL.  
     ![Creare un database MySQL in Azure: configurazione](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Al termine della configurazione, scegliere **Crea**.

    ![Creare un database MySQL in Azure: creazione](./media/store-php-create-mysql-database/create-db-3-create.png)

    Viene visualizzata una notifica popup che informa che la distribuzione è stata avviata.

    ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Al termine della distribuzione verrà visualizzata un'altra finestra popup. portale Hello verrà aperto automaticamente pannello del database MySQL.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>La connessione di database MySQL tooyour
informazioni di connessione hello toosee per il nuovo database MySQL, fare semplicemente clic **proprietà** nel pannello dell'app web.

![Creare un database MySQL in Azure: pannello Database MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

È ora possibile usare le informazioni di connessione in qualsiasi app Web. Un esempio che illustra come informazioni di connessione hello toouse da una semplice app PHP sono disponibile [qui](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Connettersi a un'app web Laravel (da get PHP hello esercitazione introduttiva)
Si supponga di esercitazione hello appena terminato [creare, configurare e distribuire un tooAzure di app web PHP](app-service-web/app-service-web-php-get-started.md) e avere un [Laravel](https://www.laravel.com/) app web in esecuzione in Azure. È possibile aggiungere facilmente app Laravel tooyour funzionalità di database. Segui i passaggi di hello riportati di seguito:

> [!NOTE]
> Hello passaggi seguenti presuppongono che sono state esercitazione hello [creare, configurare e distribuire un tooAzure di app web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Configurare app Laravel hello del database MySQL di toohello toopoint di ambiente di sviluppo locale. toodo, aprire `.env` dall'app Laravel directory radice e configurare le opzioni di database MySQL hello.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > In hello **proprietà** pannello nome hello del database MySQL può o potrebbe non essere visualizzato hello uno in hello **nome del DATABASE** campo. È preferibile toocheck hello Database parametro in hello **stringa di connessione** campo.    
   >
   > ![Creare un database MySQL in Azure: in corso](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. più rapido tooverify modo di avere accesso MySQL ora Hello è toouse [lo scaffolding di autenticazione predefinito di Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Nel terminale della riga di comando hello, eseguire hello seguendo i comandi dalla directory radice dell'applicazione Laravel:

         php artisan migrate
         php artisan make:auth

    Hello primo comando crea tabelle hello in Azure in base alle migrazioni predefinite in hello `database/migrations` directory e secondo comando hello strutture hello viste di base e le route per l'autenticazione e registrazione dell'utente.
3. Eseguire subito il server di sviluppo hello:

        php artisan serve
4. Nel browser hello, passare toohttp://localhost:8000 e registrare un nuovo utente, come illustrato:

    ![Connessione database tooMySQL in Azure - registrazione utente](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Eseguire la registrazione di hello completa dei messaggi di richiesta dell'interfaccia utente di hello. Dopo aver completato la registrazione, l'utente accede in automatico.

    ![Connessione database tooMySQL in Azure - registrazione utente](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Ora si sviluppa l'app nei database di MySQL hello in Azure.
5. A questo punto, è sufficiente tooreplicate il `.env` impostazioni tooyour Azure web app. Eseguire hello seguendo i comandi CLI di Azure:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Successivamente, eseguire il commit e push tooAzure hello le modifiche locali apportate in precedenza durante l'esecuzione `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Sfoglia toohello Azure web app.

        azure site browse
8. Accedere con le credenziali utente hello creato in precedenza.

    ![Connessione database tooMySQL in Azure - Sfoglia tooAzure web app](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Dopo l'accesso, verrà visualizzata hello descrittivo schermata di post-login.

    ![La connessione a database tooMySQL in Azure - connesso](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Complimenti, l'app Web PHP di Azure dispone ora di accesso ai dati del database MySQL.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).
