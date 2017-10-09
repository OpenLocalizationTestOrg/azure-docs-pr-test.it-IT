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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="113e8-103">Usare efficacemente gli ambienti DevOps per le app Web</span><span class="sxs-lookup"><span data-stu-id="113e8-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="113e8-104">In questo articolo illustra come tooset configurare e gestire le distribuzioni di applicazioni web quando sono più versioni dell'applicazione in ambienti diversi, ad esempio sviluppo, gestione temporanea, qualità (QA) e produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="113e8-105">Ogni versione dell'applicazione può essere considerato come un ambiente di sviluppo per scopo specifico di hello del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="113e8-106">Ad esempio, gli sviluppatori possono utilizzare hello QA ambiente tootest hello di qualità del applicazione hello prima che essi push tooproduction modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="113e8-107">Più ambienti di sviluppo possono essere difficile perché è necessario utilizzare codice tootrack, gestire le risorse (calcolo, app web, database, cache, e così via) e distribuire codice tutti gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="113e8-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="113e8-108">Configurare un ambiente non di produzione (gestione temporanea, sviluppo, controllo qualità)</span><span class="sxs-lookup"><span data-stu-id="113e8-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="113e8-109">Dopo un'app web di produzione sia in esecuzione, hello è toocreate un ambiente non di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="113e8-110">toouse gli slot di distribuzione, assicurarsi che siano in esecuzione in modalità di piano Standard o Premium di Azure App Service hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="113e8-111">Gli slot di distribuzione sono App Web live con i propri nomi host.</span><span class="sxs-lookup"><span data-stu-id="113e8-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="113e8-112">Elementi di contenuto e la configurazione di app Web possono essere scambiati tra i due slot di distribuzione, compreso hello slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="113e8-113">Quando si distribuisce lo slot di distribuzione tooa l'applicazione, si ottiene hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="113e8-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="113e8-114">È possibile convalidare le modifiche tooa web app in uno slot di distribuzione di gestione temporanea prima che lo scambio di hello app con lo slot di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="113e8-115">Quando si distribuisce uno slot di tooa app web prima e si scambia nell'ambiente di produzione, tutte le istanze di slot hello sono riscaldate prima viene scambiato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="113e8-116">Questo processo consente di evitare i tempi di inattività al momento della distribuzione dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="113e8-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="113e8-117">Hello reindirizzamento del traffico è seamless e nessuna richiesta viene eliminata a causa di operazioni tooswap.</span><span class="sxs-lookup"><span data-stu-id="113e8-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="113e8-118">tooautomate l'intero flusso di lavoro, configurare [scambio automatico](web-sites-staged-publishing.md#configure-auto-swap) quando non è necessario lo pre-scambio di convalida.</span><span class="sxs-lookup"><span data-stu-id="113e8-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="113e8-119">Dopo uno scambio, slot hello con app web hello inserita in precedenza ora ha hello precedente dell'applicazione web di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="113e8-120">Se le modifiche di hello scambiate nello slot di produzione hello non corrisponda a quello desiderato, è possibile eseguire hello stesso scambio immediatamente tooget il "ultima" back app web.</span><span class="sxs-lookup"><span data-stu-id="113e8-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="113e8-121">tooset di uno slot di distribuzione di gestione temporanea, vedere [configurare ambienti per le app web in Azure App Service di gestione temporanea](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="113e8-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="113e8-122">Ogni ambiente deve includere un proprio set di risorse.</span><span class="sxs-lookup"><span data-stu-id="113e8-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="113e8-123">Ad esempio, se l'App Web usa un database, allora sia l'App Web di gestione temporanea che quella di produzione devono usare database diversi.</span><span class="sxs-lookup"><span data-stu-id="113e8-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="113e8-124">Aggiungere risorse gestione temporanea dell'ambiente di sviluppo, ad esempio database, l'archiviazione o cache tooset l'ambiente di sviluppo di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="113e8-125">Esempi di utilizzo di più ambienti di sviluppo</span><span class="sxs-lookup"><span data-stu-id="113e8-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="113e8-126">Qualsiasi progetto deve seguire la gestione del codice sorgente con almeno due ambienti: sviluppo e produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="113e8-127">Se si utilizzano sistemi di gestione dei contenuti (CMSs), il framework applicazione e così via, un'applicazione hello potrebbe non supportare questo scenario senza personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="113e8-128">Questa eventualità è true per alcuni popolari Framework hello che vengono discussi in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="113e8-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="113e8-129">Un numero elevato di domande toomind sono disponibili quando si lavora con CMS/Framework, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="113e8-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="113e8-130">Come si suddividerà il contenuto di hello out in ambienti diversi?</span><span class="sxs-lookup"><span data-stu-id="113e8-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="113e8-131">Quali file è possibile modificare senza influire sugli aggiornamenti di versione del framework?</span><span class="sxs-lookup"><span data-stu-id="113e8-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="113e8-132">Come si gestiscono le configurazioni per ambiente?</span><span class="sxs-lookup"><span data-stu-id="113e8-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="113e8-133">Come si gestiscono gli aggiornamenti di versione per i moduli plug-in e il framework di base hello?</span><span class="sxs-lookup"><span data-stu-id="113e8-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="113e8-134">Esistono molti modi tooset più ambienti per il progetto.</span><span class="sxs-lookup"><span data-stu-id="113e8-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="113e8-135">Hello esempi seguenti viene illustrato un metodo per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="113e8-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="113e8-136">WordPress</span></span>
<span data-ttu-id="113e8-137">In questa sezione si apprenderà come tooset un flusso di lavoro di distribuzione tramite gli slot per WordPress.</span><span class="sxs-lookup"><span data-stu-id="113e8-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="113e8-138">Come la maggior parte delle soluzioni CMS, WordPress non supporta l'uso di più ambienti di sviluppo senza personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="113e8-139">funzionalità di App Web Hello di servizio App di Azure presenta alcune funzionalità che rendono facilmente toostore le impostazioni di configurazione all'esterno del codice.</span><span class="sxs-lookup"><span data-stu-id="113e8-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="113e8-140">Prima di creare uno slot di gestione temporanea, impostare il toosupport codice dell'applicazione più ambienti.</span><span class="sxs-lookup"><span data-stu-id="113e8-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="113e8-141">toosupport più ambienti in WordPress, è necessario tooedit `wp-config.php` in sviluppo locale app web e aggiungere hello seguente codice all'inizio di hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="113e8-142">Questo processo consentirà di configurazione dell'applicazione toopick hello corretto in base a ambiente selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="113e8-143">Creare una cartella nella radice di app web chiamato `config`e aggiungere hello `wp-config.azure.php` e `wp-config.local.php` file, che rappresentano rispettivamente l'ambiente locale e l'ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="113e8-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="113e8-144">Copiare l'esempio hello in `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="113e8-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="113e8-145">Impostazione delle chiavi di sicurezza hello, come illustrato nel codice precedente hello, è possibile rendere la tua app web tooprevent da viene violata, pertanto utilizzare valori univoci.</span><span class="sxs-lookup"><span data-stu-id="113e8-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="113e8-146">Se è necessario stringa hello toogenerate per le chiavi di sicurezza indicate nel codice hello, è possibile [generatore automatico passare toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate nuove coppie chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="113e8-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="113e8-147">Copia hello seguente codice nel `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="113e8-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="113e8-148">Usare percorsi relativi</span><span class="sxs-lookup"><span data-stu-id="113e8-148">Use relative paths</span></span>
<span data-ttu-id="113e8-149">Uno tooconfigure cosa ultima nell'app WordPress hello è percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="113e8-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="113e8-150">WordPress archivia le informazioni sull'URL nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="113e8-151">Questa risorsa di archiviazione rende più difficile spostando il contenuto di un ambiente tooanother.</span><span class="sxs-lookup"><span data-stu-id="113e8-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="113e8-152">È necessario il database di hello tooupdate ogni volta che si spostano da toostage locale o in ambienti tooproduction fase.</span><span class="sxs-lookup"><span data-stu-id="113e8-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="113e8-153">rischio hello tooreduce dei problemi che possono essere causati con la distribuzione di un database ogni volta che si effettua distribuzione da un ambiente tooanother, utilizzare hello [relativo radice collega plug-in](https://wordpress.org/plugins/root-relative-urls/), che è possibile installare tramite hello WordPress amministratore dashboard.</span><span class="sxs-lookup"><span data-stu-id="113e8-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="113e8-154">Aggiungere hello seguenti voci tooyour `wp-config.php` file prima di hello `That's all, stop editing!` commento:</span><span class="sxs-lookup"><span data-stu-id="113e8-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="113e8-155">Attivare i plug-in di hello tramite hello `Plugins` menu nel dashboard di amministrazione di WordPress.</span><span class="sxs-lookup"><span data-stu-id="113e8-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="113e8-156">Salvare le impostazioni relative al collegamento permanente per l'app WordPress.</span><span class="sxs-lookup"><span data-stu-id="113e8-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="113e8-157">Hello finale `wp-config.php` file</span><span class="sxs-lookup"><span data-stu-id="113e8-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="113e8-158">Gli eventuali aggiornamenti principali di WordPress non avranno effetto sui file `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="113e8-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="113e8-159">Di seguito è una versione finale di hello `wp-config.php` file:</span><span class="sxs-lookup"><span data-stu-id="113e8-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="113e8-160">Configurare un ambiente di staging</span><span class="sxs-lookup"><span data-stu-id="113e8-160">Set up a staging environment</span></span>
1. <span data-ttu-id="113e8-161">Se si dispone già di un'app web WordPress in esecuzione nella sottoscrizione di Azure, effettuare l'accesso toohello [portale di Azure](http://portal.azure.com), quindi andare tooyour WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="113e8-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="113e8-162">Se non si dispone di un'app web WordPress, è possibile crearne uno da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="113e8-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="113e8-163">vedere, più toolearn [creare un'app web WordPress in Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="113e8-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="113e8-164">Fare clic su **impostazioni** > **gli slot di distribuzione** > **Aggiungi** toocreate uno slot di distribuzione con nome hello *fase*.</span><span class="sxs-lookup"><span data-stu-id="113e8-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="113e8-165">Uno slot di distribuzione è un'altra applicazione web che condivisioni hello stesse risorse di app web primario hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="113e8-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Creare lo slot di distribuzione "stage"](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="113e8-167">Aggiungere un altro database MySQL, ad esempio `wordpress-stage-db`, gruppo di risorse tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="113e8-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Aggiungi gruppo tooresource di database MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="113e8-169">Aggiornare le stringhe di connessione hello per fase distribuzione slot toopoint toohello nuovo database, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="113e8-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="113e8-170">L'app web di produzione, `wordpressprodapp`e app web di gestione temporanea `wordpressprodapp-stage`, deve punto toodifferent database.</span><span class="sxs-lookup"><span data-stu-id="113e8-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="113e8-171">Configurare impostazioni app specifiche dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="113e8-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="113e8-172">Gli sviluppatori possono memorizzare coppie chiave/valore della stringa in Azure come parte delle informazioni di configurazione hello, chiamate **impostazioni App**, che è associata a un'app web.</span><span class="sxs-lookup"><span data-stu-id="113e8-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="113e8-173">In fase di esecuzione, le applicazioni web automaticamente recuperano questi valori e rendono disponibili toocode che è in esecuzione in un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="113e8-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="113e8-174">Dal punto di vista della sicurezza, si tratta di un vantaggio significativo, perché le informazioni sensibili, ad esempio le stringhe di connessione di database e le relative password, non vengono mai visualizzate come testo normale in un file come `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="113e8-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="113e8-175">Questo processo è illustrato in hello dopo i paragrafi, è utile perché include sia le modifiche di file e database per app di WordPress hello:</span><span class="sxs-lookup"><span data-stu-id="113e8-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="113e8-176">Aggiornamento della versione di WordPress</span><span class="sxs-lookup"><span data-stu-id="113e8-176">WordPress version upgrade</span></span>
* <span data-ttu-id="113e8-177">Aggiungere, modificare o aggiornare i plug-in</span><span class="sxs-lookup"><span data-stu-id="113e8-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="113e8-178">Aggiungere, modificare o aggiornare i temi</span><span class="sxs-lookup"><span data-stu-id="113e8-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="113e8-179">Configurare le impostazioni app per:</span><span class="sxs-lookup"><span data-stu-id="113e8-179">Configure app settings for:</span></span>

* <span data-ttu-id="113e8-180">Informazioni sul database</span><span class="sxs-lookup"><span data-stu-id="113e8-180">Database information</span></span>
* <span data-ttu-id="113e8-181">Attivazione/disattivazione della registrazione a WordPress</span><span class="sxs-lookup"><span data-stu-id="113e8-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="113e8-182">impostazioni di sicurezza di WordPress</span><span class="sxs-lookup"><span data-stu-id="113e8-182">WordPress security settings</span></span>

![Impostazioni app per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="113e8-184">Assicurarsi di aggiungere hello seguendo le impostazioni dell'app per slot di produzione web app e fase.</span><span class="sxs-lookup"><span data-stu-id="113e8-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="113e8-185">Si noti che dell'applicazione web di produzione hello e app web di gestione temporanea database diversi.</span><span class="sxs-lookup"><span data-stu-id="113e8-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="113e8-186">Crittografato hello **impostazione Slot** casella di controllo per tutti i parametri di impostazioni di hello tranne WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="113e8-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="113e8-187">Questo processo verrà scambiato configurazione hello per le app web, contenuto del file e database.</span><span class="sxs-lookup"><span data-stu-id="113e8-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="113e8-188">Se **impostazione Slot** è selezionata, le impostazioni dell'app dell'app web hello e configurazione della stringa di connessione verrà *non* spostare tutti gli ambienti, quando si esegue un **scambiare** operazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="113e8-189">Eventuali modifiche al database non interrompono l'App Web di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="113e8-190">Distribuire hello sviluppo locale ambiente web app toohello fase web app e il database con gli strumenti di propria scelta, ad esempio FTP, Git o PhpMyAdmin o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="113e8-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Finestra di dialogo di pubblicazione di WebMatrix per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="113e8-192">Esplorare e testare l'app Web di staging.</span><span class="sxs-lookup"><span data-stu-id="113e8-192">Browse and test your staging web app.</span></span> <span data-ttu-id="113e8-193">Prendendo in considerazione uno scenario in cui il tema hello dell'app web hello toobe aggiornato, ecco hello app web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Esplorare l'app Web di staging prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="113e8-195">Se si verificano problemi, fare clic su hello **scambiare** pulsante la gestione temporanea toomove app web nell'ambiente di produzione toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="113e8-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="113e8-196">In questo caso, scambiare hello web app e database hello in ambienti durante ogni **scambio** operazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Anteprima modifiche dello scambio per WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="113e8-198">Se lo scenario richiede file di push tooonly (non gli aggiornamenti del database), quindi controllare **impostazione Slot** per hello tutti correlati al database *impostazioni app* e *impostazionistringhediconnessione*in hello **impostazioni App Web** pannello all'interno di hello portale di Azure prima di eseguire hello **scambiare**.</span><span class="sxs-lookup"><span data-stu-id="113e8-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="113e8-199">In questo caso le impostazioni DB_NAME, DB_HOST, DB_PASSWORD, DB_USER e la stringa di connessione predefinita non verranno visualizzate nell'anteprima modifiche quando si esegue un'operazione di **scambio**.</span><span class="sxs-lookup"><span data-stu-id="113e8-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="113e8-200">In questo momento, quando si completa hello **scambiare** operazione, verrà hanno hello app web WordPress hello Aggiorna solo i file.</span><span class="sxs-lookup"><span data-stu-id="113e8-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="113e8-201">Prima di eseguire un **scambiare**, ecco hello produzione WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="113e8-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="113e8-202">![App Web di produzione prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="113e8-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="113e8-203">Dopo aver hello **scambiare** tema hello operazione è stata aggiornata in un'applicazione web di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![App Web di produzione dopo lo scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="113e8-205">Quando è necessario tooroll nuovamente, è possibile passare web di produzione toohello **impostazioni App**, fare clic su hello **scambiare** pulsante tooswap hello web app e il database dallo slot di produzione toostaging.</span><span class="sxs-lookup"><span data-stu-id="113e8-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="113e8-206">Tenere presente che se le modifiche del database sono incluse in un **scambiare** l'operazione, quindi hello successivo si distribuisce l'app web di gestione temporanea tooyour toodeploy hello modifiche toohello corrente il database è necessario per l'app web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="113e8-207">database corrente Hello potrebbe essere database di produzione precedente hello o hello fase.</span><span class="sxs-lookup"><span data-stu-id="113e8-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="113e8-208">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="113e8-208">Summary</span></span>
<span data-ttu-id="113e8-209">Di seguito è illustrato un processo generalizzato per qualsiasi applicazione con un database:</span><span class="sxs-lookup"><span data-stu-id="113e8-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="113e8-210">Installare un'applicazione hello in ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="113e8-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="113e8-211">Includere le configurazioni specifiche dell'ambiente (locale e App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="113e8-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="113e8-212">Configurare l'ambiente di produzione e di gestione temporanea per le App Web.</span><span class="sxs-lookup"><span data-stu-id="113e8-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="113e8-213">Se si dispone di un'applicazione di produzione già in esecuzione in Azure, la sincronizzazione del contenuto (file/codice e database) di gestione temporanea e toolocal gli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="113e8-214">Sviluppare l'applicazione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="113e8-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="113e8-215">Inserire l'app web di produzione in modalità blocco o di manutenzione e la sincronizzazione del contenuto del database da ambienti di produzione toostaging e sviluppo.</span><span class="sxs-lookup"><span data-stu-id="113e8-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="113e8-216">Distribuire toohello ambiente e test di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="113e8-217">Distribuire l'ambiente tooproduction.</span><span class="sxs-lookup"><span data-stu-id="113e8-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="113e8-218">Ripetere i passaggi da 4 a 6.</span><span class="sxs-lookup"><span data-stu-id="113e8-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="113e8-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="113e8-219">Umbraco</span></span>
<span data-ttu-id="113e8-220">In questa sezione si apprenderà come hello Umbraco CMS Usa toodeploy un modulo personalizzato in diversi ambienti DevOps.</span><span class="sxs-lookup"><span data-stu-id="113e8-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="113e8-221">In questo esempio fornisce un approccio diverso di toomanaging più ambienti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="113e8-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="113e8-222">[Umbraco CMS](http://umbraco.com/) è una soluzione .NET CMS diffusa che viene usata da molti sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="113e8-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="113e8-223">Fornisce hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy modulo da ambienti di sviluppo toostaging tooproduction.</span><span class="sxs-lookup"><span data-stu-id="113e8-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="113e8-224">Per creare facilmente un ambiente di sviluppo locale per un'App Web Umbraco CMS è possibile usare Visual Studio o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="113e8-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="113e8-225">Creare un'App Web Umbraco con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="113e8-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="113e8-226">Creare un'App Web Umbraco con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="113e8-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="113e8-227">È sempre necessario hello tooremove `install` cartella dell'applicazione e non caricarlo mai le app web toostage o di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="113e8-228">In questa esercitazione viene usato WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="113e8-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="113e8-229">Configurare un ambiente di staging</span><span class="sxs-lookup"><span data-stu-id="113e8-229">Set up a staging environment</span></span>
1. <span data-ttu-id="113e8-230">Creare uno slot di distribuzione, come indicato in precedenza per hello Umbraco CMS web app, presupponendo che si dispone già di un'app web Umbraco CMS e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="113e8-231">In caso contrario, è possibile crearne uno da hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="113e8-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="113e8-232">Aggiornare la stringa di connessione hello per le nuove toohello fase distribuzione slot toopoint **umbraco-fase-db** database.</span><span class="sxs-lookup"><span data-stu-id="113e8-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="113e8-233">L'app web di produzione (umbraositecms-1) e l'app web di gestione temporanea (umbracositecms-1-fase) *deve* punto toodifferent database.</span><span class="sxs-lookup"><span data-stu-id="113e8-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Aggiornare la stringa di connessione per l'app Web di staging con il nuovo database di staging](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="113e8-235">Fare clic su **impostazioni di pubblicazione ottenere** per lo slot di distribuzione hello **fase**.</span><span class="sxs-lookup"><span data-stu-id="113e8-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="113e8-236">Questo processo verrà scaricato un file di impostazioni di pubblicazione che archivia tutte le informazioni di hello che Visual Studio o WebMatrix richiede toopublish l'applicazione da un'app web di Azure toohello di hello sviluppo locale web app.</span><span class="sxs-lookup"><span data-stu-id="113e8-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Ottenere l'impostazione di hello app web di gestione temporanea di pubblicazione](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="113e8-238">Aprire l'App Web di sviluppo locale in WebMatrix o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="113e8-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="113e8-239">In questa esercitazione viene usato WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="113e8-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="113e8-240">È innanzitutto necessario tooimport hello pubblicare file di impostazioni per l'app web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importare le impostazioni di pubblicazione per Umbraco tramite WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="113e8-242">Rivedere le modifiche apportate nella finestra di dialogo hello e distribuire l'app web di Azure tooyour app web locale, *umbracositecms-1-fase*.</span><span class="sxs-lookup"><span data-stu-id="113e8-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="113e8-243">Quando si distribuiscono file direttamente l'app web di gestione temporanea tooyour, si verranno omettere i file in hello `~/app_data/TEMP/` cartella poiché questi file verranno rigenerati quando app web di hello fase viene avviato.</span><span class="sxs-lookup"><span data-stu-id="113e8-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="113e8-244">È necessario omettere anche hello `~/app_data/umbraco.config` file, verrà rigenerato.</span><span class="sxs-lookup"><span data-stu-id="113e8-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Rivedere le modifiche da pubblicare in WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="113e8-246">Dopo aver pubblicato correttamente hello Umbraco web locale app toohello staging app web, selezionare l'app web di gestione temporanea tooyour ed eseguire alcuni test toorule gli eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="113e8-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="113e8-247">Impostare il modulo di distribuzione Courier2 hello</span><span class="sxs-lookup"><span data-stu-id="113e8-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="113e8-248">Con hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modulo, è possibile semplicemente fare doppio clic toopush contenuto, fogli di stile e lo sviluppo moduli da un'app di web di gestione temporanea di web app tooa produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="113e8-249">Questo processo riduce il rischio di hello di danneggiare l'app web di produzione quando si distribuisce un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="113e8-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="113e8-250">Acquistare una licenza per Courier2 per hello `*.azurewebsites.net` dominio e il dominio personalizzato (ad esempio http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="113e8-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="113e8-251">Dopo aver acquistato una licenza di hello, sul posto hello scaricato licenza (. File GCI) in hello `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="113e8-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Salvare il file di licenza nella cartella bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="113e8-253">[Scaricare il pacchetto di hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="113e8-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="113e8-254">Accedi tooyour fase web app, ad esempio http://umbracocms-site-stage.azurewebsites.net/umbraco, fare clic su hello **Developer** menu e quindi fare clic su **pacchetti** > **installare pacchetto locale**.</span><span class="sxs-lookup"><span data-stu-id="113e8-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Programma di installazione del pacchetto Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="113e8-256">Caricare il pacchetto di hello Courier2 tramite installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Caricare il pacchetto per il modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="113e8-258">pacchetto di hello tooconfigure, è necessario tooupdate hello courier.config file hello **Config** cartella dell'app web.</span><span class="sxs-lookup"><span data-stu-id="113e8-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="113e8-259">In `<repositories>`, immettere hello produzione sito URL e le informazioni utente.</span><span class="sxs-lookup"><span data-stu-id="113e8-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="113e8-260">Se si utilizza provider di appartenenze Umbraco hello predefinito, quindi aggiungere hello ID utente di amministrazione di hello in hello &lt;utente&gt; sezione.</span><span class="sxs-lookup"><span data-stu-id="113e8-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="113e8-261">Se si utilizza un provider di appartenenze personalizzato Umbraco, utilizzare `<login>`,`<password>` nel sito di produzione toohello tooconnect hello Courier2 modulo.</span><span class="sxs-lookup"><span data-stu-id="113e8-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="113e8-262">Per ulteriori dettagli, [, vedere la documentazione di hello per il modulo hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="113e8-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="113e8-263">Analogamente, installare il modulo di Courier2 hello nel sito di produzione e configurarlo toopoint toohello fase web app nel relativo file courier.config corrispondente, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="113e8-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="113e8-264">Fare clic su hello **Courier2** scheda hello del dashboard di Umbraco CMS web app e quindi fare clic su **percorsi**.</span><span class="sxs-lookup"><span data-stu-id="113e8-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="113e8-265">Verrà visualizzato il nome di repository hello come indicato in `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="113e8-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="113e8-266">Eseguire questo processo nell'App Web di produzione e di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-266">Do this process on both your production and staging web apps.</span></span>

    ![Visualizzare il repository dell'app Web di destinazione](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="113e8-268">toodeploy contenuto dal sito di produzione toohello del sito di gestione temporanea hello andare troppo**contenuto**e selezionare una pagina esistente oppure crearne una nuova pagina.</span><span class="sxs-lookup"><span data-stu-id="113e8-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="113e8-269">Selezionerà una pagina esistente dall'app web in cui titolo hello della pagina di hello è **Guida introduttiva: nuovo**, quindi fare clic su **salvare e pubblicare**.</span><span class="sxs-lookup"><span data-stu-id="113e8-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Modificare il titolo della pagina e pubblicare](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="113e8-271">Pulsante destro del mouse hello modificato tooview pagina tutte le opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="113e8-272">Fare clic su **Courier** tooopen hello **distribuzione** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="113e8-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="113e8-273">Fare clic su **Distribuisci** tooinitiate distribuzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="113e8-275">Rivedere le modifiche di hello e quindi fare clic su **continua**.</span><span class="sxs-lookup"><span data-stu-id="113e8-275">Review hello changes, and then click **Continue**.</span></span>

    ![Verifica delle modifiche nella finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="113e8-277">log di distribuzione Hello Mostra se la distribuzione di hello è riuscita.</span><span class="sxs-lookup"><span data-stu-id="113e8-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Visualizzare i log di distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="113e8-279">Se vengono riflesse hello, esplorare il toosee app web di produzione.</span><span class="sxs-lookup"><span data-stu-id="113e8-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Esplorare l'app Web di produzione](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="113e8-281">ulteriori informazioni sulla modalità toouse Courier, revisione hello documentazione toolearn.</span><span class="sxs-lookup"><span data-stu-id="113e8-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="113e8-282">Come tooupgrade hello versione Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="113e8-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="113e8-283">Verrà Courier non si esegue l'aggiornamento da una versione di Umbraco CMS tooanother come guida.</span><span class="sxs-lookup"><span data-stu-id="113e8-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="113e8-284">Quando si aggiorna una versione di Umbraco CMS, è necessario verificare la presenza di incompatibilità con i moduli personalizzati o da partner e le librerie di base di Umbraco hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="113e8-285">Alcune procedure consigliate:</span><span class="sxs-lookup"><span data-stu-id="113e8-285">Here are best practices:</span></span>

* <span data-ttu-id="113e8-286">Eseguire sempre un backup dell'App Web e del database prima di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="113e8-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="113e8-287">Nelle App web in Azure, è possibile configurare backup automatici per i siti Web utilizzando le funzionalità di backup hello e ripristino del sito, se necessario utilizzando la funzionalità Ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="113e8-288">Per ulteriori informazioni, vedere [come tooback backup dell'app web](web-sites-backup.md) e [come toorestore app web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="113e8-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="113e8-289">Verificare se sono compatibili con la versione di hello di che si esegue l'aggiornamento pacchetti da partner.</span><span class="sxs-lookup"><span data-stu-id="113e8-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="113e8-290">Pagina di download del pacchetto di hello, verificare di compatibilità del progetto con versione Umbraco CMS hello.</span><span class="sxs-lookup"><span data-stu-id="113e8-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="113e8-291">Per ulteriori informazioni su come tooupgrade in locale, l'app web [vedere indicazioni sull'aggiornamento generale di hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="113e8-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="113e8-292">Dopo l'aggiornamento del sito di sviluppo locale, pubblicare hello modifiche toohello app web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="113e8-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="113e8-293">Testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-293">Test your application.</span></span> <span data-ttu-id="113e8-294">Se si verificano problemi, utilizzare hello **scambiare** pulsante tooswap gestione temporanea del sito toohello produzione app web.</span><span class="sxs-lookup"><span data-stu-id="113e8-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="113e8-295">Quando si utilizza hello **scambiare** operazione, è possibile visualizzare le modifiche di hello che saranno interessate nella configurazione dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="113e8-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="113e8-296">Questo **scambiare** operazione Scambia hello web App e i database.</span><span class="sxs-lookup"><span data-stu-id="113e8-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="113e8-297">Dopo aver hello **scambiare**, database di produzione web app verrà toohello punto umbraco-fase-db hello e hello database di gestione temporanea web app verrà tooumbraco punto-op-db.</span><span class="sxs-lookup"><span data-stu-id="113e8-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Anteprima dello scambio per la distribuzione di Umbraco CMS.](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="113e8-299">Ecco i vantaggi di swapping sia hello web app e database hello:</span><span class="sxs-lookup"><span data-stu-id="113e8-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="113e8-300">È possibile eseguire il rollback toohello versione precedente dell'app web con un altro **scambiare** se sono presenti eventuali problemi di applicazione.</span><span class="sxs-lookup"><span data-stu-id="113e8-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="113e8-301">Per un aggiornamento, è necessario toodeploy file e database di gestione temporanea dell'applicazione web di produzione di web app toohello hello e il database.</span><span class="sxs-lookup"><span data-stu-id="113e8-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="113e8-302">Quando si distribuiscono file e database, molti aspetti potrebbero andare per il verso sbagliato.</span><span class="sxs-lookup"><span data-stu-id="113e8-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="113e8-303">Utilizzando hello **scambiare** funzionalità di slot, è possibile ridurre i tempi di inattività durante l'aggiornamento e ridurre il rischio di hello di errori che possono verificarsi quando si distribuiscono le modifiche.</span><span class="sxs-lookup"><span data-stu-id="113e8-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="113e8-304">È possibile eseguire **A / B test** utilizzando hello [test nell'ambiente di produzione](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funzionalità.</span><span class="sxs-lookup"><span data-stu-id="113e8-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="113e8-305">Questo esempio si hello flessibilità della piattaforma hello in cui è possibile compilare moduli personalizzati simili toomanage distribuzione del tooUmbraco Courier modulo tutti gli ambienti.</span><span class="sxs-lookup"><span data-stu-id="113e8-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="113e8-306">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="113e8-306">References</span></span>
[<span data-ttu-id="113e8-307">Agile Software Development con il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="113e8-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="113e8-308">Configurare ambienti di staging per le app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="113e8-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="113e8-309">Modalità di accesso di slot di distribuzione di produzione toonon tooblock web</span><span class="sxs-lookup"><span data-stu-id="113e8-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
