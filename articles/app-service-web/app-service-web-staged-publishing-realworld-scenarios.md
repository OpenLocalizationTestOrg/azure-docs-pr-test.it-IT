---
title: aaaUse DevOps ambienti in modo efficace per l'app web | Documenti Microsoft
description: "Informazioni su come toouse gli slot di distribuzione tooset backup e gestire più ambienti di sviluppo dell'applicazione"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Usare efficacemente gli ambienti DevOps per le app Web
In questo articolo illustra come tooset configurare e gestire le distribuzioni di applicazioni web quando sono più versioni dell'applicazione in ambienti diversi, ad esempio sviluppo, gestione temporanea, qualità (QA) e produzione. Ogni versione dell'applicazione può essere considerato come un ambiente di sviluppo per scopo specifico di hello del processo di distribuzione. Ad esempio, gli sviluppatori possono utilizzare hello QA ambiente tootest hello di qualità del applicazione hello prima che essi push tooproduction modifiche hello.
Più ambienti di sviluppo possono essere difficile perché è necessario utilizzare codice tootrack, gestire le risorse (calcolo, app web, database, cache, e così via) e distribuire codice tutti gli ambienti.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Configurare un ambiente non di produzione (gestione temporanea, sviluppo, controllo qualità)
Dopo un'app web di produzione sia in esecuzione, hello è toocreate un ambiente non di produzione. toouse gli slot di distribuzione, assicurarsi che siano in esecuzione in modalità di piano Standard o Premium di Azure App Service hello. Gli slot di distribuzione sono App Web live con i propri nomi host. Elementi di contenuto e la configurazione di app Web possono essere scambiati tra i due slot di distribuzione, compreso hello slot di produzione. Quando si distribuisce lo slot di distribuzione tooa l'applicazione, si ottiene hello seguenti vantaggi:

- È possibile convalidare le modifiche tooa web app in uno slot di distribuzione di gestione temporanea prima che lo scambio di hello app con lo slot di produzione hello.
- Quando si distribuisce uno slot di tooa app web prima e si scambia nell'ambiente di produzione, tutte le istanze di slot hello sono riscaldate prima viene scambiato nell'ambiente di produzione. Questo processo consente di evitare i tempi di inattività al momento della distribuzione dell'App Web. Hello reindirizzamento del traffico è seamless e nessuna richiesta viene eliminata a causa di operazioni tooswap. tooautomate l'intero flusso di lavoro, configurare [scambio automatico](web-sites-staged-publishing.md#configure-auto-swap) quando non è necessario lo pre-scambio di convalida.
- Dopo uno scambio, slot hello con app web hello inserita in precedenza ora ha hello precedente dell'applicazione web di produzione. Se le modifiche di hello scambiate nello slot di produzione hello non corrisponda a quello desiderato, è possibile eseguire hello stesso scambio immediatamente tooget il "ultima" back app web.

tooset di uno slot di distribuzione di gestione temporanea, vedere [configurare ambienti per le app web in Azure App Service di gestione temporanea](web-sites-staged-publishing.md). Ogni ambiente deve includere un proprio set di risorse. Ad esempio, se l'App Web usa un database, allora sia l'App Web di gestione temporanea che quella di produzione devono usare database diversi. Aggiungere risorse gestione temporanea dell'ambiente di sviluppo, ad esempio database, l'archiviazione o cache tooset l'ambiente di sviluppo di gestione temporanea.

## <a name="examples-of-using-multiple-development-environments"></a>Esempi di utilizzo di più ambienti di sviluppo
Qualsiasi progetto deve seguire la gestione del codice sorgente con almeno due ambienti: sviluppo e produzione. Se si utilizzano sistemi di gestione dei contenuti (CMSs), il framework applicazione e così via, un'applicazione hello potrebbe non supportare questo scenario senza personalizzazione. Questa eventualità è true per alcuni popolari Framework hello che vengono discussi in hello le sezioni seguenti. Un numero elevato di domande toomind sono disponibili quando si lavora con CMS/Framework, ad esempio:

- Come si suddividerà il contenuto di hello out in ambienti diversi?
- Quali file è possibile modificare senza influire sugli aggiornamenti di versione del framework?
- Come si gestiscono le configurazioni per ambiente?
- Come si gestiscono gli aggiornamenti di versione per i moduli plug-in e il framework di base hello?

Esistono molti modi tooset più ambienti per il progetto. Hello esempi seguenti viene illustrato un metodo per ogni applicazione.

### <a name="wordpress"></a>WordPress
In questa sezione si apprenderà come tooset un flusso di lavoro di distribuzione tramite gli slot per WordPress. Come la maggior parte delle soluzioni CMS, WordPress non supporta l'uso di più ambienti di sviluppo senza personalizzazione. funzionalità di App Web Hello di servizio App di Azure presenta alcune funzionalità che rendono facilmente toostore le impostazioni di configurazione all'esterno del codice.

1. Prima di creare uno slot di gestione temporanea, impostare il toosupport codice dell'applicazione più ambienti. toosupport più ambienti in WordPress, è necessario tooedit `wp-config.php` in sviluppo locale app web e aggiungere hello seguente codice all'inizio di hello del file hello. Questo processo consentirà di configurazione dell'applicazione toopick hello corretto in base a ambiente selezionato hello.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Creare una cartella nella radice di app web chiamato `config`e aggiungere hello `wp-config.azure.php` e `wp-config.local.php` file, che rappresentano rispettivamente l'ambiente locale e l'ambiente Azure.

3. Copiare l'esempio hello in `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Impostazione delle chiavi di sicurezza hello, come illustrato nel codice precedente hello, è possibile rendere la tua app web tooprevent da viene violata, pertanto utilizzare valori univoci. Se è necessario stringa hello toogenerate per le chiavi di sicurezza indicate nel codice hello, è possibile [generatore automatico passare toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate nuove coppie chiave/valore.

4. Copia hello seguente codice nel `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Usare percorsi relativi
Uno tooconfigure cosa ultima nell'app WordPress hello è percorsi relativi. WordPress archivia le informazioni sull'URL nel database di hello. Questa risorsa di archiviazione rende più difficile spostando il contenuto di un ambiente tooanother. È necessario il database di hello tooupdate ogni volta che si spostano da toostage locale o in ambienti tooproduction fase. rischio hello tooreduce dei problemi che possono essere causati con la distribuzione di un database ogni volta che si effettua distribuzione da un ambiente tooanother, utilizzare hello [relativo radice collega plug-in](https://wordpress.org/plugins/root-relative-urls/), che è possibile installare tramite hello WordPress amministratore dashboard.

Aggiungere hello seguenti voci tooyour `wp-config.php` file prima di hello `That's all, stop editing!` commento:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Attivare i plug-in di hello tramite hello `Plugins` menu nel dashboard di amministrazione di WordPress. Salvare le impostazioni relative al collegamento permanente per l'app WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Hello finale `wp-config.php` file
Gli eventuali aggiornamenti principali di WordPress non avranno effetto sui file `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`. Di seguito è una versione finale di hello `wp-config.php` file:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Configurare un ambiente di staging
1. Se si dispone già di un'app web WordPress in esecuzione nella sottoscrizione di Azure, effettuare l'accesso toohello [portale di Azure](http://portal.azure.com), quindi andare tooyour WordPress web app. Se non si dispone di un'app web WordPress, è possibile crearne uno da hello Azure Marketplace. vedere, più toolearn [creare un'app web WordPress in Azure App Service](web-sites-php-web-site-gallery.md).
Fare clic su **impostazioni** > **gli slot di distribuzione** > **Aggiungi** toocreate uno slot di distribuzione con nome hello *fase*. Uno slot di distribuzione è un'altra applicazione web che condivisioni hello stesse risorse di app web primario hello creato in precedenza.

    ![Creare lo slot di distribuzione "stage"](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Aggiungere un altro database MySQL, ad esempio `wordpress-stage-db`, gruppo di risorse tooyour `wordpressapp-group`.

    ![Aggiungi gruppo tooresource di database MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Aggiornare le stringhe di connessione hello per fase distribuzione slot toopoint toohello nuovo database, `wordpress-stage-db`. L'app web di produzione, `wordpressprodapp`e app web di gestione temporanea `wordpressprodapp-stage`, deve punto toodifferent database.

#### <a name="configure-environment-specific-app-settings"></a>Configurare impostazioni app specifiche dell'ambiente
Gli sviluppatori possono memorizzare coppie chiave/valore della stringa in Azure come parte delle informazioni di configurazione hello, chiamate **impostazioni App**, che è associata a un'app web. In fase di esecuzione, le applicazioni web automaticamente recuperano questi valori e rendono disponibili toocode che è in esecuzione in un'applicazione web. Dal punto di vista della sicurezza, si tratta di un vantaggio significativo, perché le informazioni sensibili, ad esempio le stringhe di connessione di database e le relative password, non vengono mai visualizzate come testo normale in un file come `wp-config.php`.

Questo processo è illustrato in hello dopo i paragrafi, è utile perché include sia le modifiche di file e database per app di WordPress hello:

* Aggiornamento della versione di WordPress
* Aggiungere, modificare o aggiornare i plug-in
* Aggiungere, modificare o aggiornare i temi

Configurare le impostazioni app per:

* Informazioni sul database
* Attivazione/disattivazione della registrazione a WordPress
* impostazioni di sicurezza di WordPress

![Impostazioni app per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Assicurarsi di aggiungere hello seguendo le impostazioni dell'app per slot di produzione web app e fase. Si noti che dell'applicazione web di produzione hello e app web di gestione temporanea database diversi.

1. Crittografato hello **impostazione Slot** casella di controllo per tutti i parametri di impostazioni di hello tranne WP_ENV. Questo processo verrà scambiato configurazione hello per le app web, contenuto del file e database. Se **impostazione Slot** è selezionata, le impostazioni dell'app dell'app web hello e configurazione della stringa di connessione verrà *non* spostare tutti gli ambienti, quando si esegue un **scambiare** operazione. Eventuali modifiche al database non interrompono l'App Web di produzione.

2. Distribuire hello sviluppo locale ambiente web app toohello fase web app e il database con gli strumenti di propria scelta, ad esempio FTP, Git o PhpMyAdmin o WebMatrix.

    ![Finestra di dialogo di pubblicazione di WebMatrix per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Esplorare e testare l'app Web di staging. Prendendo in considerazione uno scenario in cui il tema hello dell'app web hello toobe aggiornato, ecco hello app web di gestione temporanea.

    ![Esplorare l'app Web di staging prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Se si verificano problemi, fare clic su hello **scambiare** pulsante la gestione temporanea toomove app web nell'ambiente di produzione toohello contenuto. In questo caso, scambiare hello web app e database hello in ambienti durante ogni **scambio** operazione.

    ![Anteprima modifiche dello scambio per WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Se lo scenario richiede file di push tooonly (non gli aggiornamenti del database), quindi controllare **impostazione Slot** per hello tutti correlati al database *impostazioni app* e *impostazionistringhediconnessione*in hello **impostazioni App Web** pannello all'interno di hello portale di Azure prima di eseguire hello **scambiare**. In questo caso le impostazioni DB_NAME, DB_HOST, DB_PASSWORD, DB_USER e la stringa di connessione predefinita non verranno visualizzate nell'anteprima modifiche quando si esegue un'operazione di **scambio**. In questo momento, quando si completa hello **scambiare** operazione, verrà hanno hello app web WordPress hello Aggiorna solo i file.
    >
    >

    Prima di eseguire un **scambiare**, ecco hello produzione WordPress web app.
    ![App Web di produzione prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Dopo aver hello **scambiare** tema hello operazione è stata aggiornata in un'applicazione web di produzione.

    ![App Web di produzione dopo lo scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Quando è necessario tooroll nuovamente, è possibile passare web di produzione toohello **impostazioni App**, fare clic su hello **scambiare** pulsante tooswap hello web app e il database dallo slot di produzione toostaging. Tenere presente che se le modifiche del database sono incluse in un **scambiare** l'operazione, quindi hello successivo si distribuisce l'app web di gestione temporanea tooyour toodeploy hello modifiche toohello corrente il database è necessario per l'app web di gestione temporanea. database corrente Hello potrebbe essere database di produzione precedente hello o hello fase.

#### <a name="summary"></a>Riepilogo
Di seguito è illustrato un processo generalizzato per qualsiasi applicazione con un database:

1. Installare un'applicazione hello in ambiente locale.
2. Includere le configurazioni specifiche dell'ambiente (locale e App Web di Azure).
3. Configurare l'ambiente di produzione e di gestione temporanea per le App Web.
4. Se si dispone di un'applicazione di produzione già in esecuzione in Azure, la sincronizzazione del contenuto (file/codice e database) di gestione temporanea e toolocal gli ambienti di produzione.
5. Sviluppare l'applicazione nell'ambiente locale.
6. Inserire l'app web di produzione in modalità blocco o di manutenzione e la sincronizzazione del contenuto del database da ambienti di produzione toostaging e sviluppo.
7. Distribuire toohello ambiente e test di gestione temporanea.
8. Distribuire l'ambiente tooproduction.
9. Ripetere i passaggi da 4 a 6.

### <a name="umbraco"></a>Umbraco
In questa sezione si apprenderà come hello Umbraco CMS Usa toodeploy un modulo personalizzato in diversi ambienti DevOps. In questo esempio fornisce un approccio diverso di toomanaging più ambienti di sviluppo.

[Umbraco CMS](http://umbraco.com/) è una soluzione .NET CMS diffusa che viene usata da molti sviluppatori. Fornisce hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy modulo da ambienti di sviluppo toostaging tooproduction. Per creare facilmente un ambiente di sviluppo locale per un'App Web Umbraco CMS è possibile usare Visual Studio o WebMatrix.

- [Creare un'App Web Umbraco con Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Creare un'App Web Umbraco con WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

È sempre necessario hello tooremove `install` cartella dell'applicazione e non caricarlo mai le app web toostage o di produzione. In questa esercitazione viene usato WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Configurare un ambiente di staging
1. Creare uno slot di distribuzione, come indicato in precedenza per hello Umbraco CMS web app, presupponendo che si dispone già di un'app web Umbraco CMS e in esecuzione. In caso contrario, è possibile crearne uno da hello Marketplace.
2. Aggiornare la stringa di connessione hello per le nuove toohello fase distribuzione slot toopoint **umbraco-fase-db** database. L'app web di produzione (umbraositecms-1) e l'app web di gestione temporanea (umbracositecms-1-fase) *deve* punto toodifferent database.

    ![Aggiornare la stringa di connessione per l'app Web di staging con il nuovo database di staging](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Fare clic su **impostazioni di pubblicazione ottenere** per lo slot di distribuzione hello **fase**. Questo processo verrà scaricato un file di impostazioni di pubblicazione che archivia tutte le informazioni di hello che Visual Studio o WebMatrix richiede toopublish l'applicazione da un'app web di Azure toohello di hello sviluppo locale web app.

    ![Ottenere l'impostazione di hello app web di gestione temporanea di pubblicazione](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Aprire l'App Web di sviluppo locale in WebMatrix o Visual Studio. In questa esercitazione viene usato WebMatrix. È innanzitutto necessario tooimport hello pubblicare file di impostazioni per l'app web di gestione temporanea.

    ![Importare le impostazioni di pubblicazione per Umbraco tramite WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Rivedere le modifiche apportate nella finestra di dialogo hello e distribuire l'app web di Azure tooyour app web locale, *umbracositecms-1-fase*. Quando si distribuiscono file direttamente l'app web di gestione temporanea tooyour, si verranno omettere i file in hello `~/app_data/TEMP/` cartella poiché questi file verranno rigenerati quando app web di hello fase viene avviato. È necessario omettere anche hello `~/app_data/umbraco.config` file, verrà rigenerato.

    ![Rivedere le modifiche da pubblicare in WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Dopo aver pubblicato correttamente hello Umbraco web locale app toohello staging app web, selezionare l'app web di gestione temporanea tooyour ed eseguire alcuni test toorule gli eventuali problemi.

#### <a name="set-up-hello-courier2-deployment-module"></a>Impostare il modulo di distribuzione Courier2 hello
Con hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modulo, è possibile semplicemente fare doppio clic toopush contenuto, fogli di stile e lo sviluppo moduli da un'app di web di gestione temporanea di web app tooa produzione. Questo processo riduce il rischio di hello di danneggiare l'app web di produzione quando si distribuisce un aggiornamento.
Acquistare una licenza per Courier2 per hello `*.azurewebsites.net` dominio e il dominio personalizzato (ad esempio http://abc.com). Dopo aver acquistato una licenza di hello, sul posto hello scaricato licenza (. File GCI) in hello `bin` cartella.

![Salvare il file di licenza nella cartella bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Scaricare il pacchetto di hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Accedi tooyour fase web app, ad esempio http://umbracocms-site-stage.azurewebsites.net/umbraco, fare clic su hello **Developer** menu e quindi fare clic su **pacchetti** > **installare pacchetto locale**.

    ![Programma di installazione del pacchetto Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Caricare il pacchetto di hello Courier2 tramite installazione guidata di hello.

    ![Caricare il pacchetto per il modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. pacchetto di hello tooconfigure, è necessario tooupdate hello courier.config file hello **Config** cartella dell'app web.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. In `<repositories>`, immettere hello produzione sito URL e le informazioni utente.
    Se si utilizza provider di appartenenze Umbraco hello predefinito, quindi aggiungere hello ID utente di amministrazione di hello in hello &lt;utente&gt; sezione.
    Se si utilizza un provider di appartenenze personalizzato Umbraco, utilizzare `<login>`,`<password>` nel sito di produzione toohello tooconnect hello Courier2 modulo.
    Per ulteriori dettagli, [, vedere la documentazione di hello per il modulo hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Analogamente, installare il modulo di Courier2 hello nel sito di produzione e configurarlo toopoint toohello fase web app nel relativo file courier.config corrispondente, come illustrato di seguito.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Fare clic su hello **Courier2** scheda hello del dashboard di Umbraco CMS web app e quindi fare clic su **percorsi**. Verrà visualizzato il nome di repository hello come indicato in `courier.config`. Eseguire questo processo nell'App Web di produzione e di gestione temporanea.

    ![Visualizzare il repository dell'app Web di destinazione](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. toodeploy contenuto dal sito di produzione toohello del sito di gestione temporanea hello andare troppo**contenuto**e selezionare una pagina esistente oppure crearne una nuova pagina. Selezionerà una pagina esistente dall'app web in cui titolo hello della pagina di hello è **Guida introduttiva: nuovo**, quindi fare clic su **salvare e pubblicare**.

    ![Modificare il titolo della pagina e pubblicare](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Pulsante destro del mouse hello modificato tooview pagina tutte le opzioni di hello. Fare clic su **Courier** tooopen hello **distribuzione** la finestra di dialogo. Fare clic su **Distribuisci** tooinitiate distribuzione.

    ![Finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Rivedere le modifiche di hello e quindi fare clic su **continua**.

    ![Verifica delle modifiche nella finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    log di distribuzione Hello Mostra se la distribuzione di hello è riuscita.

     ![Visualizzare i log di distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Se vengono riflesse hello, esplorare il toosee app web di produzione.

     ![Esplorare l'app Web di produzione](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

ulteriori informazioni sulla modalità toouse Courier, revisione hello documentazione toolearn.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Come tooupgrade hello versione Umbraco CMS
Verrà Courier non si esegue l'aggiornamento da una versione di Umbraco CMS tooanother come guida. Quando si aggiorna una versione di Umbraco CMS, è necessario verificare la presenza di incompatibilità con i moduli personalizzati o da partner e le librerie di base di Umbraco hello. Alcune procedure consigliate:

* Eseguire sempre un backup dell'App Web e del database prima di un aggiornamento. Nelle App web in Azure, è possibile configurare backup automatici per i siti Web utilizzando le funzionalità di backup hello e ripristino del sito, se necessario utilizzando la funzionalità Ripristino hello. Per ulteriori informazioni, vedere [come tooback backup dell'app web](web-sites-backup.md) e [come toorestore app web](web-sites-restore.md).
* Verificare se sono compatibili con la versione di hello di che si esegue l'aggiornamento pacchetti da partner. Pagina di download del pacchetto di hello, verificare di compatibilità del progetto con versione Umbraco CMS hello.

Per ulteriori informazioni su come tooupgrade in locale, l'app web [vedere indicazioni sull'aggiornamento generale di hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Dopo l'aggiornamento del sito di sviluppo locale, pubblicare hello modifiche toohello app web di gestione temporanea. Testare l'applicazione. Se si verificano problemi, utilizzare hello **scambiare** pulsante tooswap gestione temporanea del sito toohello produzione app web. Quando si utilizza hello **scambiare** operazione, è possibile visualizzare le modifiche di hello che saranno interessate nella configurazione dell'applicazione web. Questo **scambiare** operazione Scambia hello web App e i database. Dopo aver hello **scambiare**, database di produzione web app verrà toohello punto umbraco-fase-db hello e hello database di gestione temporanea web app verrà tooumbraco punto-op-db.

![Anteprima dello scambio per la distribuzione di Umbraco CMS.](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Ecco i vantaggi di swapping sia hello web app e database hello:

* È possibile eseguire il rollback toohello versione precedente dell'app web con un altro **scambiare** se sono presenti eventuali problemi di applicazione.
* Per un aggiornamento, è necessario toodeploy file e database di gestione temporanea dell'applicazione web di produzione di web app toohello hello e il database. Quando si distribuiscono file e database, molti aspetti potrebbero andare per il verso sbagliato. Utilizzando hello **scambiare** funzionalità di slot, è possibile ridurre i tempi di inattività durante l'aggiornamento e ridurre il rischio di hello di errori che possono verificarsi quando si distribuiscono le modifiche.
* È possibile eseguire **A / B test** utilizzando hello [test nell'ambiente di produzione](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funzionalità.

Questo esempio si hello flessibilità della piattaforma hello in cui è possibile compilare moduli personalizzati simili toomanage distribuzione del tooUmbraco Courier modulo tutti gli ambienti.

## <a name="references"></a>Riferimenti
[Agile Software Development con il servizio app di Azure](app-service-agile-software-development.md)

[Configurare ambienti di staging per le app Web nel servizio app di Azure](web-sites-staged-publishing.md)

[Modalità di accesso di slot di distribuzione di produzione toonon tooblock web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
