---
title: un'app web da Azure Marketplace hello aaaCreate | Documenti Microsoft
description: Informazioni su come una nuova app web WordPress da hello Azure Marketplace tramite toocreate hello portale di Azure.
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Creare un'app web da hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketplace fornisce un'ampia gamma di applicazioni web comuni sviluppati dalla community di software Apri origine, ad esempio WordPress e Umbraco CMS. In questa esercitazione, è illustrato come app WordPress toocreate da Azure marketplace.
che consente di creare un'app Web di Azure e un database MySQL. 

![Dashboard dell'app Web WordPress di esempio](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Prima di iniziare 

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

## <a name="deploy-from-azure-marketplace"></a>Distribuire da Azure Marketplace
Eseguire operazioni di hello seguenti toodeploy WordPress da Azure Marketplace.

### <a name="sign-in-tooazure"></a>Accedi tooAzure
Accedi toohello [portale di Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Distribuire il modello di WordPress
Hello Azure Marketplace fornisce modelli per la configurazione di risorse, hello installazione [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget modello avviata.
   
Immettere il seguente hello informazioni toodeploy hello WordPress app e le relative risorse.

  ![Flusso per la creazione di WordPress](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Campo         | Valore consigliato           | Descrizione  |
| ------------- |-------------------------|-------------|
| Nome app      | mywordpressapp          | Immettere un nome univoco dell'app per il **nome dell'app Web**. Questo nome viene utilizzato come parte del nome DNS di hello predefinito per l'app `<app_name>.azurewebsites.net`, pertanto è necessario toobe univoco tra tutte le App in Azure. È possibile mappare un'app tooyour nome di dominio personalizzato in un secondo momento per esporre gli utenti tooyour |
| Sottoscrizione  | Pagamento in base al consumo             | Selezionare una **Sottoscrizione**. Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata hello. |
| Gruppo di risorse| mywordpressappgroup                 |    Inserire un **gruppo di risorse**. Un gruppo di risorse è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web e database. È possibile creare un gruppo di risorse o usarne uno esistente |
| Piano di servizio app | myappplan          | Piani di servizio App rappresentano raccolta hello di risorse fisiche utilizzate toohost app. Seleziona hello **percorso** hello e **tariffario**. Per altre informazioni sul prezzo, vedere il [piano tariffario del servizio app di Azure](https://azure.microsoft.com/pricing/details/app-service/) |
| Database      | mywordpressapp          | Selezionare il provider di database appropriata hello per MySQL. App Web supporta **ClearDB**, **Database di Azure per MySQL** e **MySQL in-app**. Per ulteriori informazioni, vedere la sezione [Configurazione del database](#database-config) riportata di seguito. |
| Application Insights | ON oppure OFF          | Facoltativo. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) offre i servizi di monitoraggio per l'app web facendo clic su **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Configurazione del database
Procedura hello riportata di seguito in base a propria scelta del provider di database MySQL.  Si consiglia di tale database sia App Web e MySQL in hello nello stesso percorso.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) è una soluzione di terze parti per un servizio completamente integrato di MySQL in Azure. Nei database di ClearDB toouse ordine, sarà necessario tooassociate tooyour una carta di credito [account Azure](http://account.windowsazure.com/subscriptions). Se si seleziona il provider di database ClearDB, è possibile visualizzare un elenco di toochoose database esistenti da o fare clic su **Crea nuovo** pulsante toocreate un database.

![Creazione di ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Database di Azure per MySQL (anteprima)
[Il Database di Azure per MySQL](https://azure.microsoft.com/en-us/services/mysql) fornisce un servizio di database gestito per lo sviluppo di app e la distribuzione che consente di toostand backup di un database MySQL minuti e scalabilità su hello in entrata nel cloud hello più attendibili. Con inclusi piani tariffari, si otterranno tutte le funzionalità di hello desiderato come a disponibilità elevata, protezione e ripristino: incorporata, senza costi aggiuntivi. Fare clic su **tariffario** toochoose un altro [tariffario](https://azure.microsoft.com/pricing/details/mysql). toouse esistente del database o esistente di MySQL server, utilizzare un gruppo di risorse esistente in cui hello risiede server. 

![Configurare le impostazioni di database hello per app web hello](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Il database di Azure per MySQL (anteprima) e App Web su Linux (anteprima) non è disponibile in tutte le aree. toolearn ulteriori informazioni sulla [Database di Azure per MySQL (anteprima)](https://docs.microsoft.com/en-us/azure/mysql) e [App Web in Linux](./app-service-linux-intro.md) limitazioni. 

#### <a name="mysql-in-app"></a>MySQL in-app
[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) è una funzionalità di servizio App che abilita l'esecuzione di MySql in modo nativo su piattaforma hello. funzionalità di base Hello è supportata con versione di hello di hello funzionalità:

- Server MySQL in esecuzione nella stessa istanza del server web che ospita il sito hello in modo affiancato con hello. Questo consente di migliorare le prestazioni dell'applicazione.
- L'archiviazione è condivisa tra i file di MySQL e quelli dell'app Web. Si noti con i piani gratuito e condiviso, che è possibile riscontrare i limiti di quota quando utilizza sito hello in base alle azioni hello è eseguono. Verificare i [limiti di quota](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) per i piani gratuiti e condivisi.
- È possibile attivare la registrazione generale per MySQL e quella per le query lente. Si noti che questo può influire sulle prestazioni del sito hello e dovrebbe non essere sempre accesi. funzionalità di registrazione Hello consente di esaminare eventuali problemi di applicazione. 

Per altri dettagli, vedere questo [articolo](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![Gestione di MySQL in-app](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

È possibile controllare lo stato di avanzamento hello facendo clic sull'icona di campanello hello nella parte superiore di hello della pagina del portale hello durante hello WordPress app viene distribuita.    
![Indicatore di stato](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Gestire la nuova app Web di Azure

Passare toohello tootake portale Azure esamina hello web app che appena creato.

toodo, accedi troppo[https://portal.azure.com](https://portal.azure.com).

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Si accede così al _pannello_, ovvero una pagina del portale visualizzata in orizzontale, dell'app Web.

Per impostazione predefinita, il pannello dell'app web illustra hello **Panoramica** pagina. che offre una visualizzazione dello stato dell'app. In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare. le schede di Hello sul lato sinistro di hello del pannello hello Mostra è possibile aprire le pagine di configurazione diverso hello.

![Pannello del servizio app nel portale di Azure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Queste schede nel pannello hello mostrano hello numerose funzionalità è possibile aggiungere tooyour web app. Hello elenco seguente offre solo alcune delle possibilità hello:

* Eseguire il mapping di un nome DNS personalizzato
* Associare un certificato SSL personalizzato
* Configurare la distribuzione continua
* Aumentare le prestazioni e il numero di istanze
* Aggiungere l'autenticazione utente

Completare hello 5 minuti WordPress installazione guidata toohave WordPress app attivo e in esecuzione. Estrarre [Wordpress documentazione](https://codex.WordPress.org/) toodevelop app web.

![Installazione guidata di WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configurazione dell'app 
Prima che l'app WordPress sia pronta per la produzione, è necessario seguire diversi passaggi. Seguire questi passaggi tooconfigure e gestire app WordPress:

| toodo questo... | Opzione |
| --- | --- |
| **Caricare o archiviare file di grandi dimensioni** |[Plug-in di WordPress per l'uso dell'archiviazione BLOB](https://wordpress.org/plugins/windows-azure-storage/)|
| **Inviare posta elettronica** |Acquisto [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) servizio di posta elettronica e usare hello [plug-in WordPress per l'uso di SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure,|
| **Nomi di dominio personalizzati** |[Configurare un nome di dominio personalizzato nel servizio app di Azure](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Abilitare HTTPS per un'app Web nel Servizio app di Azure](app-service-web-tutorial-custom-ssl.md) |
| **Convalida di preproduzione** |[Configurare ambienti di staging e sviluppo per le app Web nel servizio app di Azure](web-sites-staged-publishing.md)|
| **Monitoraggio e risoluzione dei problemi** |[Abilitare la registrazione diagnostica per le app Web nel Servizio app di Azure](web-sites-enable-diagnostic-log.md) e [monitorare le app Web nel Servizio app di Azure](app-service-web-tutorial-monitoring.md) |
| **Distribuire il sito** |[Distribuire un'app Web nel Servizio app di Azure](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Proteggere la rete virtuale 
Prima che l'app WordPress sia pronta per la produzione, è necessario seguire diversi passaggi. Seguire questi passaggi tooconfigure e gestire app WordPress:

| toodo questo... | Opzione |
| --- | --- |
| **Nome utente e password complessi**|  Modificare la password di frequente. Non usare nomi utente comuni come *admin* o *wordpress* e così via. Forzare tutti i nomi utente univoci di WordPress utenti toouse e le password complesse. |
| **Mantenersi aggiornati** | Mantenere i componenti di base di WordPress, temi e i plug-in di toodate. Utilizzare hello runtime più recente PHP disponibili nel servizio App di Azure |
| **Aggiornare le chiavi di sicurezza di WordPress** | Aggiornamento [chiave di sicurezza di WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tooimprove crittografia archiviata nei cookie|

## <a name="improve-performance"></a>Migliorare le prestazioni
Le prestazioni nel cloud hello avviene principalmente tramite la memorizzazione nella cache e di scalabilità orizzontale. Tuttavia, è necessario considerare hello memoria, larghezza di banda e altri attributi dell'hosting di applicazioni Web.

| toodo questo... | Opzione |
| --- | --- |
| **Identificare le funzionalità delle istanze del servizio app** |[Dettagli sui prezzi, incluse le funzionalità dei livelli del Servizio app](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Memorizzare risorse nella cache** |Utilizzare [cache redis di Azure-](https://azure.microsoft.com/en-us/services/cache/), o una delle altre offerte di memorizzazione nella cache di hello hello [Azure Store](https://azuremarketplace.microsoft.com) |
| **Scalare l'applicazione** |È necessario tooscale [hello web app in Azure App Service](web-sites-scale.md) database MySQL e/o. MySQL in-app non supporta la scalabilità orizzontale, quindi scegliere ClearDB o il database di Azure per MySQL (anteprima). [Ridimensionare il database di Azure per MySQL (anteprima)](https://azure.microsoft.com/en-us/pricing/details/mysql/) o se si utilizza [ClearDB elevata disponibilità e Routing](http://w2.cleardb.net/faqs/) tooscale backup del database |

## <a name="availability-and-disaster-recovery"></a>Disponibilità e ripristino di emergenza
Disponibilità elevata include aspetto hello di continuità aziendale toomaintain ripristino di emergenza. Pianificazione per gli errori e le emergenze nel cloud hello richiede errori hello toorecognize rapidamente. Queste soluzioni consentono di implementare una strategia di disponibilità elevata.

| toodo questo... | Opzione |
| --- | --- |
| **Bilanciare il carico dei siti** o **distribuire geograficamente i siti** |[Instradare il traffico con Gestione traffico di Azure](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Backup e ripristino** |[Eseguire il backup di un'app Web nel Servizio app di Azure](web-sites-backup.md) e [ripristinare un'app Web nel Servizio app di Azure](web-sites-restore.md) |

## <a name="next-steps"></a>Passaggi successivi
Informazioni sulle diverse funzionalità di [toodevelop di servizio App e la scala](/app-service-web/).
