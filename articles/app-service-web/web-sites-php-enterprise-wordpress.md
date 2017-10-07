---
title: classe aaaEnterprise WordPress in Azure | Documenti Microsoft
description: Informazioni su come toohost un WordPress di classe enterprise del sito nel servizio App di Azure
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>WordPress di livello aziendale in Azure
Il Servizio app di Azure rende disponibile un ambiente scalabile, sicuro e facile da usare per siti [WordPress][wordpress] di importanza critica e su vasta scala. Microsoft ha eseguito siti aziendali, ad esempio hello [Office] [ officeblog] e [Bing] [ bingblog] blog. Questo articolo illustra come toouse hello funzionalità App Web di Microsoft Azure App Service tooestablish e mantenere un livello aziendale, il sito WordPress basato su cloud in grado di gestire un volume elevato di visitatori.

## <a name="architecture-and-planning"></a>Architettura e pianificazione
Un'installazione di base di WordPress prevede solo due requisiti:

* **MySQL Database**: questo requisito è disponibile tramite [ClearDB in hello Azure Marketplace][cdbnstore]. In alternativa, è possibile gestire l'installazione di MySQL su macchine virtuali di Azure tramite [Windows][mysqlwindows] o [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB prevede diverse configurazioni di MySQL. Ciascuna configurazione presenta diverse caratteristiche di prestazioni. Vedere hello [Azure Store] [ cdbnstore] per informazioni sulle offerte che vengono fornite tramite hello Azure Store o direttamente nei hello [sito Web ClearDB](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 o versioni successive**: il Servizio app di Azure fornisce attualmente le [versioni PHP 5.4, 5.5 e 5.6][phpwebsite].

  > [!NOTE]
  > È consigliabile che è sempre esecuzione hello versione più recente di PHP in modo da disporre di correzioni più recenti hello.
  >
  >

### <a name="basic-deployment"></a>Distribuzione di base
Se si utilizzano solo i requisiti di base hello, è possibile creare una soluzione di base all'interno di un'area di Azure.

![Un'app Web di Azure e il database MySQL ospitati in un'unica area di Azure][basic-diagram]

Anche se ciò consente di creare più istanze di App Web di hello sito tooscale orizzontalmente l'applicazione, tutto ciò che è ospitato all'interno di Data Center hello in un'area geografica specifica. Visitatori di fuori di quest'area possono vedere i tempi di risposta lenti quando usano sito hello. Se i Data Center hello in quest'area si disattivano, pertanto non l'applicazione.

### <a name="multi-region-deployment"></a>Distribuzione in più aree
Tramite Azure [Traffic Manager][trafficmanager], è possibile ridimensionare il sito WordPress in più aree geografiche diverse e fornire hello stesso URL per tutti i visitatori. Tutti i visitatori possono essere tramite Gestione traffico e sono quindi area tooa indirizzato che è basato su hello configurazione di bilanciamento del carico.

![Un'applicazione web di Azure, ospitata in più aree, con disponibilità elevata CDBR router tooroute tooMySQL in aree geografiche][multi-region-diagram]

All'interno di ogni area sito WordPress hello sarebbe comunque essere scalato in più istanze di App Web, ma questa scalabilità è l'area tooa specifico. ossia può essere diversa per le aree a traffico elevato rispetto a quelle a traffico ridotto.

tooreplicate e instradare il traffico toomultiple database MySQL, è possibile utilizzare [router a disponibilità elevata ClearDB (CDBRs)] [ cleardbscale] (visualizzata a sinistra) o [MySQL Cluster vettore livello Edition (esegue questa operazione)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Distribuzione in più aree con memorizzazione nella cache e archiviazione di contenuti multimediali
Se il sito hello accetta caricamenti o ospita i file di supporto, usare archiviazione Blob di Azure. Se è necessario che la memorizzazione nella cache, è consigliabile [cache Redis][rediscache], [Memcache Cloud](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), o una delle altre offerte di memorizzazione nella cache di hello hello [Azure Store](http://azure.microsoft.com/gallery/store/).

![Un'app Web di Azure, ospitata in più aree, con l'uso del router CDBR a disponibilità elevata per MySQL, con cache gestita, archiviazione BLOB e rete per la distribuzione di contenuti][performance-diagram]

Archiviazione BLOB è distribuita geograficamente in aree geografiche per impostazione predefinita, non vi è tooworry sulla replica file in tutti i siti. È inoltre possibile abilitare hello Azure [Content Delivery Network] [ cdn] per l'archiviazione Blob, che distribuisce i file tooend nodi visitatori tooyour più vicino.

### <a name="planning"></a>Pianificazione
#### <a name="additional-requirements"></a>Requisiti aggiuntivi
| toodo questo... | Opzione |
| --- | --- |
| **Caricare o archiviare file di grandi dimensioni** |[Plug-in di WordPress per l'uso dell'archiviazione BLOB][storageplugin] |
| **Inviare posta elettronica** |[SendGrid] [ storesendgrid] e hello [plug-in WordPress per l'uso di SendGrid][sendgridplugin] |
| **Nomi di dominio personalizzati** |[Configurare un nome di dominio personalizzato nel Servizio app di Azure][customdomain] |
| **HTTPS** |[Abilitare HTTPS per un'app Web nel Servizio app di Azure][httpscustomdomain] |
| **Convalida di preproduzione** |[Configurare ambienti di gestione temporanea per le app Web nel Servizio app di Azure][staging] <p>Quando si sposta un'app web da tooproduction di gestione temporanea, è inoltre possibile spostare configurazione WordPress hello. Assicurarsi che tutte le impostazioni siano aggiornate toohello requisiti per l'applicazione di produzione prima di spostare tooproduction app hello gestione temporanea.</p> |
| **Monitoraggio e risoluzione dei problemi** |[Abilitare la registrazione diagnostica per le app Web nel Servizio app di Azure][log] e [Monitorare le app Web nel Servizio app di Azure][monitor] |
| **Distribuire il sito** |[Distribuire un'app Web nel Servizio app di Azure][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Disponibilità e ripristino di emergenza
| toodo questo... | Opzione |
| --- | --- |
| **Bilanciare il carico dei siti** o **distribuire geograficamente i siti** |[Instradare il traffico con Gestione traffico di Azure][trafficmanager] |
| **Backup e ripristino** |[Eseguire il backup di un'app Web nel Servizio app di Azure][backup] e [Ripristinare un'app Web nel Servizio app di Azure][restore] |

#### <a name="performance"></a>Prestazioni
Le prestazioni nel cloud hello avviene principalmente tramite la memorizzazione nella cache e di scalabilità orizzontale. Tuttavia, è necessario considerare hello memoria, larghezza di banda e altri attributi dell'hosting di applicazioni Web.

| toodo questo... | Opzione |
| --- | --- |
| **Identificare le funzionalità delle istanze del servizio app** |[Dettagli dei prezzi, incluse le funzionalità dei livelli del Servizio app][websitepricing] |
| **Memorizzare risorse nella cache** |[Cache redis][rediscache], [Memcache Cloud](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), o una delle altre offerte di memorizzazione nella cache di hello hello [Azure Store](/gallery/store/) |
| **Scalare l'applicazione** |[Ridimensionare un'app Web nel Servizio app di Azure][websitescale] e [Routing ClearDB a disponibilità elevata][cleardbscale]. Se si sceglie toohost e gestire la propria installazione di MySQL, è necessario considerare [esegue questa operazione Cluster MySQL] [ cge] per scalabilità orizzontale. |

#### <a name="migration"></a>Migrazione
Esistono due metodi toomigrate un tooAzure di sito WordPress servizio App esistente:

* **[Esportazione di WordPress][export]**: questo metodo consente di esportare il contenuto di hello del blog. È quindi possibile importare hello tooa contenuto nuovo WordPress sito nel servizio App di Azure tramite hello [plug-in WordPress importatore][import].

  > [!NOTE]
  > Questa procedura consente di eseguire la migrazione del contenuto, ma non di eventuali plug-in, temi o altre personalizzazioni. È necessario reinstallare questi componenti manualmente.
  >
  >
* **La migrazione manuale**: [eseguire il backup del sito] [ wordpressbackup] e [database][wordpressdbbackup]e quindi ripristinare manualmente il tooa web app in Azure Servizio App e il database MySQL associato. Questo metodo è utile toomigrate altamente personalizzati siti quanto evita la necessità hello installare manualmente i plug-in, temi e altre personalizzazioni.

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate
### <a name="create-a-wordpress-site"></a>Creare un sito WordPress
1. Hello utilizzare [Azure Marketplace] [ cdbnstore] toocreate un database MySQL delle dimensioni di hello identificati nel hello [pianificazione e architettura](#planning) sezione nell'area di hello o aree in cui ospitare il sito.
2. Seguire i passaggi di hello in [creare un'app web WordPress in Azure App Service] [ createwordpress] toocreate un'app web WordPress. Quando si crea un'app web hello, selezionare **utilizza un MySQL Database esistente**, quindi selezionare il database hello creato nel passaggio 1.

Se si esegue la migrazione di un sito WordPress esistente, vedere [eseguire la migrazione di un esistente tooAzure sito WordPress](#Migrate-an-existing-WordPress-site-to-Azure) dopo aver creato una nuova app web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Eseguire la migrazione di un esistente tooAzure sito WordPress
Come accennato in hello [pianificazione e architettura](#planning) sezione, sono disponibili due modi toomigrate un sito WordPress:

* **Usare l'esportazione e importazione** per i siti che non dispongono di livello di personalizzazione o in cui si desidera solo contenuto hello toomove.
* **Utilizzare backup e ripristino** per i siti che hanno una grande quantità di personalizzazione in cui si desidera toomove tutti gli elementi.

Utilizzare una delle seguenti sezioni toomigrate hello al sito.

#### <a name="hello-export-and-import-method"></a>Hello esportazione e importazione (metodo)
1. Utilizzare [WordPress esportare] [ export] tooexport esistente del sito.
2. Creare un'app web utilizzando i passaggi di hello hello [creare un sito WordPress](#Create-a-new-WordPress-site) sezione.
3. Accedi al sito WordPress tooyour hello [portale di Azure][mgmtportal], quindi fare clic su **plug-in** > **Aggiungi nuovo**. Cercare e installare hello **WordPress importatore** plug-in.
4. Dopo aver installato hello plug-in WordPress dell'utilità di importazione, fare clic su **strumenti** > **importazione**, quindi fare clic su **WordPress** toouse hello plug-in WordPress dell'utilità di importazione.
5. In hello **importazione WordPress** pagina, fare clic su **Scegli File**. Trovare il file WXR hello esportata dal sito WordPress esistente e quindi fare clic su **file di caricamento e l'importazione**.
6. Fare clic su **Submit**. Viene richiesto che l'importazione di hello ha esito positivo.
7. Dopo aver completato tutti questi passaggi, riavviare il sito da relativo **servizi App** pannello in hello [portale di Azure][mgmtportal].

Dopo aver importato sito hello, potrebbe essere necessario hello tooperform seguendo i passaggi tooenable impostazioni non nel file di importazione hello.

| Se si usano... | Effettuare l'operazione seguente: |
| --- | --- |
| **Collegamenti permanenti** |Dashboard di WordPress hello del nuovo sito hello fare clic su **impostazioni** > **permanenti**, quindi aggiornare struttura permanenti hello. |
| **Collegamenti a immagini/file multimediali** |tooupdate collegamenti toohello nuova posizione, utilizzare hello [plug-in Velluto blu aggiornare URL][velvet], una ricerca e sostituzione strumento oppure aggiornare manualmente i collegamenti di hello nel database. |
| **Temi** |Andare troppo**aspetto** > **tema**, quindi aggiornare il tema di sito hello in base alle esigenze. |
| **Menu** |Se il tema supporta i menu, home page di collegamenti tooyour potrebbe essere sottodirectory di hello precedente incorporati in essi contenuti. Andare troppo**aspetto** > **menu**, quindi eseguire l'aggiornamento. |

#### <a name="hello-backup-and-restore-method"></a>Hello backup e ripristino (metodo)
1. Eseguire il backup del WordPress esistente del sito usando informazioni hello in [WordPress backup][wordpressbackup].
2. Eseguire il backup del database esistente usando informazioni hello in [backup del database][wordpressdbbackup].
3. Creare un database e ripristinare i backup di hello.

   1. Acquistare un nuovo database da hello [Azure Marketplace][cdbnstore], o impostare un database MySQL in un [Windows] [ mysqlwindows] o [Linux ] [ mysqllinux] macchina virtuale.
   2. Utilizzare un client di MySQL come [MySQL Workbench] [ workbench] tooconnect toohello nuovi database e importare il database di WordPress.
   3. Aggiornamento hello database toochange hello voci tooyour nuovo servizio App di Azure dominio, ad esempio, mywordpress.azurewebsites.net. Hello utilizzare [ricerca e sostituzione per lo Script di database di WordPress] [ searchandreplace] toosafely modificare tutte le istanze.
4. Creare un'app web nel portale di Azure hello e pubblicare backup WordPress hello.

   1. un'app web con un database, in hello toocreate [portale di Azure][mgmtportal], fare clic su **New** > **Web e dispositivi mobili**  >  **Azure Marketplace** > **le app Web** > **Web app + SQL** (o **Web app + MySQL**) > **Creare**. Configurare tutte le necessarie hello impostazioni toocreate un'app web vuota.
   2. Nel processo di backup di WordPress, individuare hello **wp config.php** file e aprirlo in un editor. Sostituire hello seguendo le voci con le informazioni di hello per il nuovo database MySQL:

      * **Db_name**: nome utente hello del database hello.
      * **DB_USER**: hello utente nome utilizzato tooaccess hello database.
      * **DB_PASSWORD**: password utente hello.

        Dopo la modifica di queste voci, salvare e chiudere hello **wp config.php** file.
   3. Hello utilizzare [distribuire un'app web in Azure App Service] [ deploy] informazioni tooenable hello metodo di distribuzione che si desidera toouse e quindi distribuirla l'app web di WordPress tooyour backup nel servizio App di Azure.
5. Dopo la distribuzione di sito WordPress hello, è necessario nuovo sito di tooaccess in grado di hello (come un'app web di servizio App) utilizzando hello *. URL azurewebsite.net hello sito.

### <a name="configure-your-site"></a>Configurare il sito
Dopo la creazione o la migrazione sito WordPress hello, utilizzare hello seguente prestazioni tooimprove informazioni o abilitare funzionalità aggiuntive.

| toodo questo... | Opzione |
| --- | --- |
| **Impostare la modalità del piano e le dimensioni del servizio app e abilitare la scalabilità** |[Ridimensionare un'app Web nel Servizio app di Azure][websitescale]. |
| **Abilitare connessioni di database permanenti** |Per impostazione predefinita, WordPress non utilizza connessioni di database persistente, che potrebbero causare il toobecome di database toohello connessione limitata dopo più connessioni. tooenable connessioni permanenti, installare hello [plug-in di connessioni permanenti adapter](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Migliorare le prestazioni** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Disabilitare i cookie ARR hello</a>, che può migliorare le prestazioni durante l'esecuzione di WordPress in più istanze di applicazioni Web.</p></li><li><p>Abilitare il caching. È possibile utilizzare <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">cache Redis</a> (anteprima) con hello <a href="https://wordpress.org/plugins/redis-object-cache/">plug-in WordPress di oggetto della cache Redis</a>, oppure è possibile utilizzare uno di hello altre offerte di memorizzazione nella cache di hello <a href="/gallery/store/">Azure Store</a>.</p></li><li><p>[Come rendere più veloce WordPress con WinCache](https://wordpress.org/plugins/w3-total-cache/). Lo strumento WinCache è abilitato per impostazione predefinita per le app Web. Quando l'utilizzo combinato di WinCache e Cache dinamica, disattivare la cache dei file di WinCache, ma lasciare utente hello e la cache della sessione abilitata. tooturn disattivata la cache dei file, in un file con estensione ini a livello di sistema, impostare il valore seguente hello:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Ridimensionare un'app Web nel Servizio app di Azure][websitescale] e usare il <a href="http://www.cleardb.com/developers/cdbr/introduction">routing a disponibilità elevata di ClearDB</a> o <a href="http://www.mysql.com/products/cluster/">MySQL Cluster CGE</a>.</p></li></ul> |
| **Usare i BLOB per l'archiviazione** |<ol><li><p>[Creare un account di Archiviazione di Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Informazioni su come troppo[hello utilizzo rete per la distribuzione di contenuti](../cdn/cdn-create-new-endpoint.md) toogeo-distribuire i dati archiviati nel BLOB.</p></li><li><p>Installare e configurare hello <a href="https://wordpress.org/plugins/windows-azure-storage/">archiviazione di Azure per i plug-in WordPress</a>.</p><p>Per il programma di installazione dettagliata e informazioni di configurazione per i plug-in di hello, vedere hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">manuale dell'utente</a>.</p> </li></ol> |
| **Abilitare la posta elettronica** |Abilitare <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> utilizzando hello Azure Store. Installare hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">plug-in di SendGrid</a> per WordPress. |
| **Configurare un nome di dominio personalizzato** |[Configurare un nome di dominio personalizzato nel Servizio app di Azure][customdomain]. |
| **Abilitare HTTPS per un nome di dominio personalizzato** |[Abilitare HTTPS per un'app Web nel Servizio app di Azure][httpscustomdomain]. |
| **Bilanciare il carico o distribuire geograficamente il sito** |[Instradare il traffico con Gestione traffico di Azure][trafficmanager]. Se si utilizza un dominio personalizzato, vedere [configurare un nome di dominio personalizzato in Azure App Service] [ customdomain] per informazioni su come toouse gestione traffico con nomi di dominio personalizzati. |
| **Abilitare i backup automatici** |[Eseguire il backup di un'app Web nel Servizio app di Azure][backup]. |
| **Abilitare la registrazione diagnostica** |[Abilitare la registrazione diagnostica per le app Web nel Servizio app di Azure][log]. |

## <a name="next-steps"></a>Passaggi successivi
* [Ottimizzazione di WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Convertire toomultisite WordPress in Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [Aggiornamento guidato di ClearDB per Azure](http://www.cleardb.com/store/azure/upgrade)
* [Hosting di WordPress in una sottocartella dell'app Web nel servizio app di Azure](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Procedura dettagliata: Creare un sito WordPress con Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Ospitare il blog WordPress esistente in Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Abilitare collegamenti permanenti efficaci in WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Come toomigrate ed eseguire il blog di WordPress in Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Come liberare WordPress in Azure App Service per toorun](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress in Azure in un massimo di due minuti](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Lo spostamento di un tooAzure blog di WordPress - parte 1: creazione di un blog di WordPress in Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Lo spostamento di un tooAzure blog di WordPress - parte 2: il trasferimento del contenuto](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Lo spostamento di un tooAzure blog di WordPress - parte 3: impostazione del dominio personalizzato](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Lo spostamento di un tooAzure blog di WordPress - parte 4: piuttosto permanenti e le regole di riscrittura URL](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Lo spostamento di un tooAzure blog di WordPress - parte 5: lo spostamento da una radice toohello sottocartella](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Ricerca tooset backup un WordPress web app nell'account di Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Supporto di WordPress in Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Suggerimenti per WordPress in Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di iscriversi per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
>
>

## <a name="whats-changed"></a>Modifiche apportate
Per una modifica di toohello della Guida da tooApp di siti Web del servizio, vedere [servizio App di Azure e il relativo impatto sui servizi di Azure esistente](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
