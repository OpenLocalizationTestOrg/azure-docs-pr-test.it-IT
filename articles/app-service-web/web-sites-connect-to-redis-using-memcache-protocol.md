---
title: aaaConnect tooRedis di app web un servizio App tramite hello protocollo Memcache - Azure | Documenti Microsoft
description: Connettersi a un'app web in Azure App service tooRedis Cache mediante protocollo Memcache hello
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Connettersi a un'app web nel servizio App di Azure tooRedis Cache tramite hello protocollo Memcache
In questo articolo si apprenderà come tooconnect un WordPress web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) troppo[Cache Redis di Azure] [ 12] utilizzando hello [Memcache] [ 13] protocollo. Se si dispone di un'app web esistente che utilizza un server Memcache per memorizzare nella cache in memoria, è possibile migrare tooAzure servizio App e usare hello prima parte memorizzazione nella cache soluzione in Microsoft Azure con codice dell'applicazione tooyour modifiche minime o nessuna. Inoltre, è possibile utilizzare le app esistenti di Memcache esperienza toocreate altamente scalabili e distribuite in Azure App Service con Cache Redis di Azure per la memorizzazione nella cache in memoria, quando si utilizza il framework di applicazioni più diffusi, ad esempio .NET, PHP, Node.js, Java e Python.  

Servizio App Web App consente questo scenario di applicazione con shim Memcache di App Web di hello, che è un server Memcache locale che funge da proxy Memcache per la memorizzazione nella cache le chiamate tooAzure Cache Redis. In questo modo tutte le app che comunica con dati di toocache protocollo Memcache hello Cache Redis. Questo shim Memcache opera a livello di protocollo hello, pertanto può essere utilizzato da qualsiasi applicazione o di framework applicazione, purché comunica mediante protocollo Memcache hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Prerequisiti
shim Memcache di App Web Hello è utilizzabile con qualsiasi applicazione fornito comunica mediante protocollo Memcache hello. Per questo particolare esempio, un'applicazione hello riferimento è un sito WordPress scalabile che può essere eseguito il provisioning da hello Azure Marketplace.

Seguire i passaggi di hello descritti negli articoli seguenti:

* [Eseguire il provisioning di un'istanza di hello servizio Cache Redis di Azure][0]
* [Distribuzione di un sito WordPress scalabile in Azure][1]

Dopo aver distribuito del sito WordPress scalabile di hello e un'istanza di Cache Redis provisioning sarà pronto tooproceed con abilitazione shim Memcache hello in App Web di servizio App di Azure.

## Abilitare shim Memcache di App Web hello
In shim Memcache tooconfigure di ordine, è necessario creare tre impostazioni di app. Questa operazione può essere eseguita tramite una vasta gamma di metodi inclusi hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715), hello [portale classico][3], hello [cmdlet di Azure PowerShell] [ 5] o hello [interfaccia della riga di comando di Azure][5]. Per motivi di hello del post, eseguo hello toouse [portale Azure] [ 4] tooset le impostazioni dell'app hello. Hello seguenti possono essere recuperati da **impostazioni** pannello dell'istanza della Cache Redis.

![Pannello Impostazioni di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Aggiungere l'impostazione di app REDIS_HOST
Hello prima impostazione dell'app è necessario toocreate è hello **REDIS\_HOST** impostazione dell'app. Questa impostazione consente di hello toowhich hello shim inoltra hello cache informazioni sulla destinazione. valore richiesto per l'impostazione dell'app REDIS_HOST hello può essere recuperati da hello Hello **proprietà** pannello dell'istanza della Cache Redis.

![Nome host di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Chiave di hello set di hello app impostazione troppo**REDIS\_HOST** e il valore di hello di hello app impostazione toohello **hostname** dell'istanza di Cache Redis hello.

![Impostazione REDIS_HOST per app Web](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Aggiungere l'impostazione di app REDIS_KEY
Hello secondo impostazione app necessaria toocreate è hello **REDIS\_chiave** impostazione dell'app. Questa impostazione offre una istanza di hello authentication token toosecurely richiesto accesso hello Cache Redis. È possibile recuperare il valore di hello necessari per l'impostazione dell'app da hello hello REDIS_KEY **le chiavi di accesso** pannello dell'istanza di Cache Redis hello.

![Chiave primaria di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Chiave di hello set di hello app impostazione troppo**REDIS\_chiave** e il valore di hello di hello app impostazione toohello **chiave primaria** dell'istanza di Cache Redis hello.

![Impostazione REDIS_KEY per siti Web di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Aggiungere l'impostazione di app MEMCACHESHIM_REDIS_ENABLE
impostazione dell'app ultimo Hello è hello tooenable usati Memcache Shim in applicazioni Web, che usa hello REDIS_HOST e REDIS_KEY toohello tooconnect Cache Redis di Azure e chiamate di cache di hello in avanti. Chiave di hello set di hello app impostazione troppo**MEMCACHESHIM\_REDIS\_abilitare** e hello troppo valore**true**.

![Impostazione MEMCACHESHIM_REDIS_ENABLE per app Web](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Dopo aver eseguito le impostazioni dell'app aggiungendo hello tre (3), fare clic su **salvare**.

## Abilitare l'estensione Memcache per PHP
Affinché hello toospeak di applicazione hello protocollo Memcache, è necessario tooinstall hello Memcache estensione tooPHP - framework di hello del linguaggio per il sito WordPress.

### Scaricare hello php_memcache estensione
Sfoglia troppo[PECL][6]. In hello la memorizzazione nella cache di categoria, fare clic su [memcache][7]. Nella colonna download hello fare clic sul collegamento DLL hello.

![Sito Web di PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Collegamento di hello Non Thread-Safe (punta) x86 per la versione di hello di PHP nelle App Web abilitato per il download. (il valore predefinito è PHP 5.4).

![Pacchetto Memcache sul sito Web di PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Abilitare l'estensione php_memcache hello
Dopo aver scaricato il file hello, decomprimere e caricare hello **php\_memcache.dll** in hello **unità d:\\home\\sito\\wwwroot\\bin\\ext\\**  directory. Dopo aver caricato php_memcache.dll hello in hello web app, è necessario tooenable hello estensione toohello Runtime PHP. hello tooenable estensione Memcache nel portale di Azure, aprire hello hello **le impostazioni dell'applicazione** pannello per l'app web hello, quindi aggiungere una nuova impostazione di app con la chiave di hello di **PHP\_estensioni** hello e valore **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Se l'app web hello deve tooload più estensioni PHP, il valore di hello di PHP_EXTENSIONS deve essere un elenco delimitato da virgole dei file tooDLL i percorsi relativi.
> 
> 

![Impostazione PHP_EXTENSIONS per app Web](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Al termine, fare clic su **Salva**.

## Installare il plug-in Memcache WordPress
> [!NOTE]
> È inoltre possibile scaricare hello [plug-in Cache di Memcache oggetto](https://wordpress.org/plugins/memcached/) da WordPress.org.
> 
> 

Nella pagina di plug-in WordPress di hello, fare clic su **Aggiungi nuovo**.

![Pagina del plug-in WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Nella casella di ricerca hello, digitare **memcache** e premere **invio**.

![Aggiungere il nuovo plug-in WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Trovare **Cache oggetti Memcache** nell'elenco di hello, quindi fare clic su **installa**.

![Installare il plug-in Memcache WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Abilitare hello plug-in WordPress di Memcache
> [!NOTE]
> Seguire le istruzioni di hello in questo blog [come un'estensione del sito nelle App Web tooenable] [ 8] tooinstall Visual Studio Team Services.
> 
> 

In hello `wp-config.php` file, aggiungere hello seguente codice di sopra di commento di modifica stop hello verso la fine hello del file hello.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Una volta che questo codice è stato incollato, monaco salvano automaticamente documento hello.

passaggio successivo Hello è tooenable plug-in della cache di hello. Questa operazione viene eseguita mediante trascinamento della selezione **oggetto cache.php** da **wp-contenuto, i plug-in/memcache** cartella toohello **wp contenuto** tooenable cartella hello oggetto Memcache Funzionalità di cache.

![Individuare i plug-in di hello memcache cache.php-oggetto](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Ora che hello **oggetto cache.php** file si trova in hello **wp contenuto** cartella hello Cache oggetti Memcache è ora abilitata.

![Abilitare i plug-in di hello memcache cache.php-oggetto](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Verificare hello Cache oggetti Memcache funzioni plug-in
Hello passaggi tooenable hello Web App Memcache shim sono ora complete. resta Hello è tooverify che l'istanza di Cache Redis sono popolamento di dati hello.

### Abilitare il supporto di porta non SSL hello in Cache Redis di Azure
> [!NOTE]
> In fase di hello stesura di questo articolo, hello Redis CLI non supporta la connettività SSL, pertanto hello passaggi seguenti sono necessari.
> 
> 

In hello portale di Azure, passare l'istanza di Cache Redis toohello creata per questa app web. Una volta aperto il pannello della cache di hello, fare clic su hello **impostazioni** icona.

![Pulsante Impostazioni di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Selezionare **porte di accesso** dall'elenco di hello.

![Porta di accesso di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Fare clic su **No** per **Consenti l'accesso solo tramite SSL**.

![Porta di accesso solo SSL di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Si noterà che la porta NON SSL hello è ora impostata. Fare clic su **Salva**.

![Portale di accesso non SSL di Cache Redis di Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Connettersi tooAzure Cache Redis da redis-cli
> [!NOTE]
> In questo passaggio si presuppone che Redis sia installato in locale nel computer di sviluppo. [Installare Redis in locale seguendo queste istruzioni][9].
> 
> 

Aprire la console della riga di comando di hello scelta e tipo di comando seguente:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Sostituire hello  **&lt;nome host per redis cache&gt;**  con nome host effettivo xxxxx.redis.cache.windows.net hello e hello  **&lt;primaria-chiave-per--cache redis&gt;**  con chiave di accesso hello per cache di hello, quindi premere **invio**. Una volta hello CLI è connesso toohello istanza di Cache Redis, eseguire qualsiasi comando redis. Nella schermata di hello riportata di seguito, ho scelto toolist chiavi hello.

![Connettersi tooAzure Cache Redis da Redis CLI terminal](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

le chiavi di hello Hello chiamata toolist devono restituire un valore. In caso contrario, provare a passare toohello web app e riprovare.

## Conclusioni
Congratulazioni. app WordPress Hello ha ora un tooaid centralizzata della cache in memoria in aumentando la velocità effettiva. Tenere presente che hello Memcache Shim di App Web può essere utilizzato con qualsiasi client Memcache indipendentemente dal linguaggio o applicazione framework di programmazione. domande di commenti e suggerimenti o tooask tooprovide su shim Memcache di App Web hello, registrare troppo[forum MSDN] [ 10] o [Stackoverflow][11].

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [servizio App di Azure e il relativo impatto sui servizi di Azure esistente](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
