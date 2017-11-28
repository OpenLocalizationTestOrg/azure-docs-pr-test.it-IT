---
title: Usare efficacemente gli ambienti DevOps per l'App Web | Microsoft Docs
description: "Informazioni su come usare gli slot di distribuzione per configurare e gestire più ambienti di sviluppo per l'applicazione"
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
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="e8120-103">Usare efficacemente gli ambienti DevOps per le app Web</span><span class="sxs-lookup"><span data-stu-id="e8120-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="e8120-104">Questo articolo illustra come configurare e gestire le distribuzioni di applicazioni Web per più versioni dell'applicazione, ad esempio sviluppo, gestione temporanea, controllo qualità e produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="e8120-105">Ogni versione dell'applicazione può essere considerata come un ambiente di sviluppo per lo scopo specifico del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="e8120-106">Ad esempio, gli sviluppatori possono usare l'ambiente di controllo di qualità per testare la qualità dell'applicazione prima di effettuare il push delle modifiche in produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="e8120-107">La presenza di più ambienti di sviluppo può creare difficoltà, perché prevede il tracciamento del codice, la gestione delle risorse (calcolo, App Web, database, cache e così via) e la distribuzione del codice in diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="e8120-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="e8120-108">Configurare un ambiente non di produzione (gestione temporanea, sviluppo, controllo qualità)</span><span class="sxs-lookup"><span data-stu-id="e8120-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="e8120-109">Quando l'App Web è operativa, il passaggio successivo prevede la creazione di un ambiente non di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="e8120-110">Per usare gli slot di distribuzione, assicurarsi che sia in esecuzione la modalità Standard o Premium del piano di servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8120-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="e8120-111">Gli slot di distribuzione sono App Web live con i propri nomi host.</span><span class="sxs-lookup"><span data-stu-id="e8120-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="e8120-112">È possibile scambiare il contenuto dell'app Web e gli elementi delle configurazioni tra i due slot di distribuzione, incluso lo slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="e8120-113">Quando si distribuisce l'applicazione in uno slot di distribuzione, si ottengono i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8120-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="e8120-114">È possibile convalidare le modifiche alle App Web in uno slot di distribuzione di gestione temporanea prima di scambiare l'app con lo slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="e8120-115">Quando si esegue la distribuzione preliminare di un'App Web in uno slot e poi la si implementa in un ambiente di produzione, tutte le istanze dello slot vengano effettivamente eseguite prima di passare alla fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="e8120-116">Questo processo consente di evitare i tempi di inattività al momento della distribuzione dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="e8120-117">Il reindirizzamento del traffico è lineare e nessuna richiesta viene eliminata in seguito alle operazioni di scambio.</span><span class="sxs-lookup"><span data-stu-id="e8120-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="e8120-118">Per automatizzare l'intero flusso di lavoro, configurare lo [scambio automatico](web-sites-staged-publishing.md#configure-auto-swap) quando non è necessaria la convalida preliminare.</span><span class="sxs-lookup"><span data-stu-id="e8120-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="e8120-119">Dopo uno scambio, lo slot con l'App Web gestita temporaneamente include l'App Web di produzione precedente.</span><span class="sxs-lookup"><span data-stu-id="e8120-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="e8120-120">Se le modifiche applicate nello slot di produzione non sono quelle previste, è possibile ripetere immediatamente lo scambio per recuperare l'ultima App Web con i dati corretti.</span><span class="sxs-lookup"><span data-stu-id="e8120-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="e8120-121">Per configurare uno slot di distribuzione di staging, vedere [Configurare gli ambienti di staging per le app Web nel Servizio app di Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e8120-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="e8120-122">Ogni ambiente deve includere un proprio set di risorse.</span><span class="sxs-lookup"><span data-stu-id="e8120-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="e8120-123">Ad esempio, se l'App Web usa un database, allora sia l'App Web di gestione temporanea che quella di produzione devono usare database diversi.</span><span class="sxs-lookup"><span data-stu-id="e8120-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="e8120-124">Aggiungere le risorse dell'ambiente di sviluppo di gestione temporanea, ad esempio il database, l'archiviazione o la cache, per impostare l'ambiente di sviluppo di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="e8120-125">Esempi di utilizzo di più ambienti di sviluppo</span><span class="sxs-lookup"><span data-stu-id="e8120-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="e8120-126">Qualsiasi progetto deve seguire la gestione del codice sorgente con almeno due ambienti: sviluppo e produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="e8120-127">Se si usano sistemi di gestione dei contenuti (CMS), framework di applicazione e così via, l'applicazione potrebbe non supportare questo scenario senza personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="e8120-128">Questa eventualità è vera per alcuni dei framework più diffusi di cui si parla nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="e8120-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="e8120-129">Quando si usano framework o CMS, possono sorgere gli interrogativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8120-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="e8120-130">Come si suddivide il contenuto in ambienti diversi?</span><span class="sxs-lookup"><span data-stu-id="e8120-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="e8120-131">Quali file è possibile modificare senza influire sugli aggiornamenti di versione del framework?</span><span class="sxs-lookup"><span data-stu-id="e8120-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="e8120-132">Come si gestiscono le configurazioni per ambiente?</span><span class="sxs-lookup"><span data-stu-id="e8120-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="e8120-133">Come si gestiscono gli aggiornamenti delle versioni per i moduli, i plug-in e il framework di base?</span><span class="sxs-lookup"><span data-stu-id="e8120-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="e8120-134">Esistono diversi modi per configurare più ambienti per il progetto.</span><span class="sxs-lookup"><span data-stu-id="e8120-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="e8120-135">Negli esempi seguenti viene illustrato un metodo per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="e8120-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="e8120-136">WordPress</span></span>
<span data-ttu-id="e8120-137">Questa sezione descrive come configurare un flusso di lavoro di distribuzione usando gli slot per WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="e8120-138">Come la maggior parte delle soluzioni CMS, WordPress non supporta l'uso di più ambienti di sviluppo senza personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="e8120-139">La funzionalità App Web del servizio app di Azure offre alcune funzionalità che semplificano l'archiviazione delle impostazioni di configurazione all'esterno del codice.</span><span class="sxs-lookup"><span data-stu-id="e8120-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="e8120-140">Prima di creare uno slot di gestione temporanea, configurare il codice dell'applicazione in modo che supporti più ambienti.</span><span class="sxs-lookup"><span data-stu-id="e8120-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="e8120-141">Per supportare più ambienti in WordPress, è necessario modificare `wp-config.php` nell'App Web di sviluppo locale e aggiungere il codice seguente all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="e8120-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="e8120-142">Con questo processo, l'applicazione selezionerà la configurazione corretta in base all'ambiente selezionato.</span><span class="sxs-lookup"><span data-stu-id="e8120-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
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
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="e8120-143">Nella directory radice dell'App Web creare una cartella denominata `config` e aggiungere i file `wp-config.azure.php` e `wp-config.local.php`, che rappresentano rispettivamente l'ambiente Azure e l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="e8120-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="e8120-144">Copiare quanto segue in `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="e8120-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
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

    <span data-ttu-id="e8120-145">Impostando le chiavi di sicurezza come illustrato nel codice precedente è possibile impedire eventuali attacchi all'App Web, quindi è necessario usare valori univoci.</span><span class="sxs-lookup"><span data-stu-id="e8120-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="e8120-146">Per generare la stringa per le chiavi di sicurezza indicate nel codice, [accedere al generatore automatico](https://api.wordpress.org/secret-key/1.1/salt) e creare nuove coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="e8120-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="e8120-147">Copiare il codice seguente in `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="e8120-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

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
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="e8120-148">Usare percorsi relativi</span><span class="sxs-lookup"><span data-stu-id="e8120-148">Use relative paths</span></span>
<span data-ttu-id="e8120-149">Infine è necessario configurare i percorsi relativi nell'app WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="e8120-150">WordPress archivia le informazioni relative all'URL nel database.</span><span class="sxs-lookup"><span data-stu-id="e8120-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="e8120-151">Questo tipo di archiviazione rende più difficile il trasferimento dei contenuti da un ambiente all'altro.</span><span class="sxs-lookup"><span data-stu-id="e8120-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="e8120-152">È necessario aggiornare il database ogni volta che si spostano contenuti da ambiente locale ad ambiente di gestione temporanea o da ambiente di gestione temporanea ad ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="e8120-153">Per ridurre i rischi associati alla distribuzione del database ogni volta che si esegue la distribuzione da un ambiente a un altro, usare il [plug-in per i collegamenti relativi alla radice](https://wordpress.org/plugins/root-relative-urls/), che può essere installato usando il dashboard di amministrazione di WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="e8120-154">Aggiungere le voci seguenti al file `wp-config.php` prima del commento `That's all, stop editing!`:</span><span class="sxs-lookup"><span data-stu-id="e8120-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="e8120-155">Attivare il plug-in dal menu `Plugins` nel dashboard di amministrazione di WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="e8120-156">Salvare le impostazioni relative al collegamento permanente per l'app WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="e8120-157">Il file `wp-config.php` finale</span><span class="sxs-lookup"><span data-stu-id="e8120-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="e8120-158">Gli eventuali aggiornamenti principali di WordPress non avranno effetto sui file `wp-config.php`, `wp-config.azure.php` e `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="e8120-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="e8120-159">Di seguito è riportata la versione finale del file `wp-config.php`:</span><span class="sxs-lookup"><span data-stu-id="e8120-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="e8120-160">Configurare un ambiente di staging</span><span class="sxs-lookup"><span data-stu-id="e8120-160">Set up a staging environment</span></span>
1. <span data-ttu-id="e8120-161">Se l'App Web WordPress è già in esecuzione nella sottoscrizione di Azure, accedere al [Portale di Azure](http://portal.azure.com) e passare all'App Web WordPress.</span><span class="sxs-lookup"><span data-stu-id="e8120-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="e8120-162">Se non si dispone di un'App Web WordPress, è possibile crearne una da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e8120-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="e8120-163">Per altre informazioni, vedere [Creare un'App Web WordPress nel servizio app di Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="e8120-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="e8120-164">Fare clic su **Impostazioni** > **Slot di distribuzione** > **Aggiungi** per creare uno slot di distribuzione con il nome *stage*.</span><span class="sxs-lookup"><span data-stu-id="e8120-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="e8120-165">Uno slot di distribuzione è un'altra applicazione Web che condivide le stesse risorse dell'App Web primaria creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e8120-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Creare lo slot di distribuzione "stage"](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="e8120-167">Aggiungere un altro database MySQL, `wordpress-stage-db`, al gruppo di risorse `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="e8120-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Aggiungere il database MySQL al gruppo di risorse](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="e8120-169">Aggiornare le stringhe di connessione per lo slot di distribuzione di gestione temporanea affinché scelgano il nuovo database, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="e8120-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="e8120-170">L'App Web di produzione `wordpressprodapp` e l'App Web di gestione temporanea `wordpressprodapp-stage` devono scegliere database diversi.</span><span class="sxs-lookup"><span data-stu-id="e8120-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="e8120-171">Configurare impostazioni app specifiche dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="e8120-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="e8120-172">Gli sviluppatori possono archiviare le coppie di stringhe chiave-valore in Azure come parte delle informazioni di configurazione associate a un'App Web, denominate **Impostazioni app**.</span><span class="sxs-lookup"><span data-stu-id="e8120-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="e8120-173">In fase di esecuzione, le App Web recuperano automaticamente questi valori e li rendono disponibili al codice in esecuzione nell'App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="e8120-174">Dal punto di vista della sicurezza, si tratta di un vantaggio significativo, perché le informazioni sensibili, ad esempio le stringhe di connessione di database e le relative password, non vengono mai visualizzate come testo normale in un file come `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="e8120-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="e8120-175">Questo processo, spiegato nei paragrafi seguenti, è utile perché include le modifiche sia ai file che ai database per l'app WordPress:</span><span class="sxs-lookup"><span data-stu-id="e8120-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="e8120-176">Aggiornamento della versione di WordPress</span><span class="sxs-lookup"><span data-stu-id="e8120-176">WordPress version upgrade</span></span>
* <span data-ttu-id="e8120-177">Aggiungere, modificare o aggiornare i plug-in</span><span class="sxs-lookup"><span data-stu-id="e8120-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="e8120-178">Aggiungere, modificare o aggiornare i temi</span><span class="sxs-lookup"><span data-stu-id="e8120-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="e8120-179">Configurare le impostazioni app per:</span><span class="sxs-lookup"><span data-stu-id="e8120-179">Configure app settings for:</span></span>

* <span data-ttu-id="e8120-180">Informazioni sul database</span><span class="sxs-lookup"><span data-stu-id="e8120-180">Database information</span></span>
* <span data-ttu-id="e8120-181">Attivazione/disattivazione della registrazione a WordPress</span><span class="sxs-lookup"><span data-stu-id="e8120-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="e8120-182">impostazioni di sicurezza di WordPress</span><span class="sxs-lookup"><span data-stu-id="e8120-182">WordPress security settings</span></span>

![Impostazioni app per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="e8120-184">Assicurarsi di aver aggiunto le impostazioni app seguenti per l'App Web di produzione e lo slot di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="e8120-185">Si noti che l'App Web di produzione e quella di gestione temporanea usano database diversi.</span><span class="sxs-lookup"><span data-stu-id="e8120-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="e8120-186">Deselezionare la casella di controllo **Impostazione slot** per tutti i parametri delle impostazioni, ad eccezione di WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="e8120-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="e8120-187">Grazie a questo processo, la configurazione per l'App Web, il contenuto del file e il database verrà scambiata.</span><span class="sxs-lookup"><span data-stu-id="e8120-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="e8120-188">Se la casella di controllo **Impostazione slot** è selezionata, le impostazioni app dell'App Web e la configurazione delle stringhe di connessione *non* verranno spostate da un ambiente all'altro durante un'operazione di **scambio**.</span><span class="sxs-lookup"><span data-stu-id="e8120-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="e8120-189">Eventuali modifiche al database non interrompono l'App Web di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="e8120-190">Distribuire l'App Web dell'ambiente di sviluppo locale nell'App Web e nel database dell'area di gestione temporanea usando WebMatrix o altri strumenti, ad esempio FTP, Git o PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="e8120-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Finestra di dialogo di pubblicazione di WebMatrix per l'app Web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="e8120-192">Esplorare e testare l'app Web di staging.</span><span class="sxs-lookup"><span data-stu-id="e8120-192">Browse and test your staging web app.</span></span> <span data-ttu-id="e8120-193">Si consideri uno scenario in cui è necessario aggiornare il tema dell'app Web. Ecco l'app Web di staging.</span><span class="sxs-lookup"><span data-stu-id="e8120-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Esplorare l'app Web di staging prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="e8120-195">Se tutto sembra corretto, fare clic sul pulsante **Scambia** nell'App Web di gestione temporanea per spostare il contenuto all'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="e8120-196">In questo caso l'App Web e il database vengono scambiati da un ambiente all'altro nel corso di ogni operazione di **scambio**.</span><span class="sxs-lookup"><span data-stu-id="e8120-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Anteprima modifiche dello scambio per WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="e8120-198">Se invece è presente uno scenario in cui è solo necessario effettuare il push dei file (senza aggiornamenti del database), selezionare **Impostazione slot** per tutte le *impostazioni app* e le *impostazioni delle stringhe di connessione* relative al database nel pannello **Impostazioni app Web** del Portale di Azure prima di procedere con lo **scambio**.</span><span class="sxs-lookup"><span data-stu-id="e8120-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="e8120-199">In questo caso le impostazioni DB_NAME, DB_HOST, DB_PASSWORD, DB_USER e la stringa di connessione predefinita non verranno visualizzate nell'anteprima modifiche quando si esegue un'operazione di **scambio**.</span><span class="sxs-lookup"><span data-stu-id="e8120-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="e8120-200">In questa fase, al termine dell'operazione di **scambio** l'App Web WordPress conterrà solo i file aggiornati.</span><span class="sxs-lookup"><span data-stu-id="e8120-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="e8120-201">Ecco l'App Web WordPress di produzione prima dell'operazione di **scambio**.</span><span class="sxs-lookup"><span data-stu-id="e8120-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="e8120-202">![App Web di produzione prima dello scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="e8120-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="e8120-203">Dopo l'operazione di **scambio**, il tema è stato aggiornato nell'App Web di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![App Web di produzione dopo lo scambio degli slot](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="e8120-205">Quando è necessario eseguire il rollback, è possibile accedere alle **impostazioni dell'App** Web di produzione e fare clic su pulsante **Scambia** per eseguire lo scambio dell'App Web e del database dallo slot di produzione a quello di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="e8120-206">È importante ricordare che se un'operazione di **scambio** include modifiche del database, alla ridistribuzione successiva nell'App Web di gestione temporanea sarà necessario distribuire le modifiche del database nel database corrente per l'App Web di gestione temporanea,</span><span class="sxs-lookup"><span data-stu-id="e8120-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="e8120-207">che può essere un database di produzione o di gestione temporanea precedente.</span><span class="sxs-lookup"><span data-stu-id="e8120-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="e8120-208">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e8120-208">Summary</span></span>
<span data-ttu-id="e8120-209">Di seguito è illustrato un processo generalizzato per qualsiasi applicazione con un database:</span><span class="sxs-lookup"><span data-stu-id="e8120-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="e8120-210">Installare l'applicazione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="e8120-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="e8120-211">Includere le configurazioni specifiche dell'ambiente (locale e App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="e8120-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="e8120-212">Configurare l'ambiente di produzione e di gestione temporanea per le App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="e8120-213">Se è già presente un'applicazione di produzione in esecuzione in Azure, sincronizzare il contenuto di produzione (file/codice e database) con l'ambiente locale e di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="e8120-214">Sviluppare l'applicazione nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="e8120-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="e8120-215">Impostare l'App Web di produzione nella modalità di manutenzione o di blocco e sincronizzare il contenuto del database dall'ambiente di produzione agli ambienti di gestione temporanea e di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e8120-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="e8120-216">Eseguire la distribuzione nell'ambiente di gestione temporanea e procedere al test.</span><span class="sxs-lookup"><span data-stu-id="e8120-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="e8120-217">Eseguire la distribuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="e8120-218">Ripetere i passaggi da 4 a 6.</span><span class="sxs-lookup"><span data-stu-id="e8120-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="e8120-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="e8120-219">Umbraco</span></span>
<span data-ttu-id="e8120-220">In questa sezione verrà illustrato il modo in cui Umbraco CMS usa un modulo personalizzato per la distribuzione in più ambienti DevOps.</span><span class="sxs-lookup"><span data-stu-id="e8120-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="e8120-221">Questo esempio illustra un approccio diverso alla gestione di più ambienti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e8120-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="e8120-222">[Umbraco CMS](http://umbraco.com/) è una soluzione .NET CMS diffusa che viene usata da molti sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="e8120-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="e8120-223">Offre il modulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) per la distribuzione dall'ambiente di sviluppo a quello di gestione temporanea a quello di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="e8120-224">Per creare facilmente un ambiente di sviluppo locale per un'App Web Umbraco CMS è possibile usare Visual Studio o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e8120-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="e8120-225">Creare un'App Web Umbraco con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8120-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="e8120-226">Creare un'App Web Umbraco con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="e8120-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="e8120-227">È necessario ricordare sempre di rimuovere la cartella `install` nell'applicazione e di non caricarla mai nelle App Web di gestione temporanea o di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="e8120-228">In questa esercitazione viene usato WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e8120-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="e8120-229">Configurare un ambiente di staging</span><span class="sxs-lookup"><span data-stu-id="e8120-229">Set up a staging environment</span></span>
1. <span data-ttu-id="e8120-230">Creare uno slot di distribuzione come indicato in precedenza per un'App Web Umbraco CMS, presupponendo esista già un'App Web Umbraco CMS operativa.</span><span class="sxs-lookup"><span data-stu-id="e8120-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="e8120-231">In caso contrario, è possibile crearne una dal Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e8120-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="e8120-232">Aggiornare la stringa di connessione per lo slot di distribuzione di gestione temporanea perché scelga il nuovo database, **umbraco-stage-db**.</span><span class="sxs-lookup"><span data-stu-id="e8120-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="e8120-233">L'App Web di produzione (umbraositecms-1) e l'App Web di gestione temporanea (umbracositecms-1-stage) *devono* scegliere database diversi.</span><span class="sxs-lookup"><span data-stu-id="e8120-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Aggiornare la stringa di connessione per l'app Web di staging con il nuovo database di staging](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="e8120-235">Fare clic su **Get Publish settings** (Ottieni impostazioni di pubblicazione) per lo slot di distribuzione di **gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="e8120-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="e8120-236">Con questo processo verrà scaricato un file di impostazioni di pubblicazione in cui sono archiviate tutte le informazioni richieste da Visual Studio o WebMatrix per pubblicare l'applicazione dall'App Web di sviluppo locale all'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8120-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Ottenere le impostazioni di pubblicazione per l'app Web di staging](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="e8120-238">Aprire l'App Web di sviluppo locale in WebMatrix o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8120-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="e8120-239">In questa esercitazione viene usato WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e8120-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="e8120-240">È innanzitutto necessario importare il file di impostazioni di pubblicazione per l'App Web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Importare le impostazioni di pubblicazione per Umbraco tramite WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="e8120-242">Esaminare le modifiche nella finestra di dialogo e distribuire l'App Web locale nell'App Web di Azure, *umbracositecms-1-stage*.</span><span class="sxs-lookup"><span data-stu-id="e8120-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="e8120-243">Quando si distribuiscono i file direttamente nell'App Web di gestione temporanea è necessario omettere i file nella cartella `~/app_data/TEMP/`, perché verranno rigenerati al primo avvio dell'App Web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="e8120-244">Omettere il file `~/app_data/umbraco.config` perché verrà rigenerato anch'esso.</span><span class="sxs-lookup"><span data-stu-id="e8120-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Rivedere le modifiche da pubblicare in WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="e8120-246">Dopo aver pubblicato l'App Web locale Umbraco nell'App Web di gestione temporanea, esplorarla ed eseguire alcuni test per rilevare eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="e8120-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="e8120-247">Configurare il modulo di distribuzione Courier2</span><span class="sxs-lookup"><span data-stu-id="e8120-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="e8120-248">Con il modulo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) è possibile semplicemente fare doppio clic per effettuare il push di contenuti, fogli di stile e moduli di sviluppo da un'App Web di gestione temporaea a un'App Web di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="e8120-249">Questo processo riduce il rischio di interrompere l'App Web di produzione quando si distribuisce un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e8120-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="e8120-250">Acquistare una licenza per Courier2 per il dominio `*.azurewebsites.net` e il dominio personalizzato (ad esempio http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="e8120-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="e8120-251">Dopo aver acquistato la licenza, posizionare la licenza scaricata (file .LIC) nella cartella `bin`.</span><span class="sxs-lookup"><span data-stu-id="e8120-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Salvare il file di licenza nella cartella bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="e8120-253">[Scaricare il pacchetto di Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="e8120-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="e8120-254">Accedere all'App Web di gestione temporanea, ad esempio http://umbracocms-site-stage.azurewebsites.net/umbraco, fare clic sul menu **Sviluppatore**, quindi fare clic su **Pacchetti** > **Install local package** (Installa pacchetto locale).</span><span class="sxs-lookup"><span data-stu-id="e8120-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Programma di installazione del pacchetto Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="e8120-256">Caricare il pacchetto Courier2 usando il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-256">Upload the Courier2 package by using the installer.</span></span>

    ![Caricare il pacchetto per il modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="e8120-258">Per configurare il pacchetto, è necessario aggiornare il file courier.config nella cartella **Config** dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="e8120-259">In `<repositories>`immettere l’URL del sito di produzione e le informazioni dell’utente.</span><span class="sxs-lookup"><span data-stu-id="e8120-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="e8120-260">Se si usa il provider di appartenenze Umbraco predefinito, aggiungere l'ID per l'utente Administration nella sezione &lt;user&gt;.</span><span class="sxs-lookup"><span data-stu-id="e8120-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="e8120-261">Se si usa un provider di appartenenze Umbraco personalizzato, usare `<login>`,`<password>` nel modulo Courier2 per connettersi al sito di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="e8120-262">Per altre informazioni, [consultare la documentazione relativa al modulo Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="e8120-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="e8120-263">Analogamente, installare il modulo Courier2 nel sito di produzione e configurarlo affinché scelga l'App Web di gestione temporanea nel relativo file courier.config, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e8120-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="e8120-264">Fare clic sulla scheda **Courier2** nel dashboard dell'App Web Umbraco CMS, quindi fare clic su **Posizioni**.</span><span class="sxs-lookup"><span data-stu-id="e8120-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="e8120-265">Verrà visualizzato il nome del repository, come indicato in `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="e8120-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="e8120-266">Eseguire questo processo nell'App Web di produzione e di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-266">Do this process on both your production and staging web apps.</span></span>

    ![Visualizzare il repository dell'app Web di destinazione](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="e8120-268">Per distribuire il contenuto dal sito di gestione temporanea al sito di produzione, andare su **Contenuto**e selezionare una pagina esistente oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="e8120-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="e8120-269">In questo caso, verrà selezionata una pagina esistente dell'App Web in cui il titolo della pagina è **Getting Started – new** (Introduzione - Nuovo) e quindi fare clic su **Salva e pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e8120-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Modificare il titolo della pagina e pubblicare](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="e8120-271">Fare clic con il pulsante destro del mouse sulla pagina modificata per visualizzare tutte le opzioni.</span><span class="sxs-lookup"><span data-stu-id="e8120-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="e8120-272">Fare clic su **Courier** per aprire la finestra di dialogo **Distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="e8120-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="e8120-273">Fare clic su **Distribuisci** per avviare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-273">Click **Deploy** to initiate deployment.</span></span>

    ![Finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="e8120-275">Esaminare le modifiche, quindi fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="e8120-275">Review the changes, and then click **Continue**.</span></span>

    ![Verifica delle modifiche nella finestra di dialogo per la distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="e8120-277">Il log di distribuzione indica se la distribuzione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e8120-277">The deployment log shows if the deployment was successful.</span></span>

     ![Visualizzare i log di distribuzione del modulo Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="e8120-279">Passare all'app Web di produzione per vedere se riflette le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e8120-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Esplorare l'app Web di produzione](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="e8120-281">Per altre informazioni su come usare Courier, vedere la documentazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="e8120-282">Come aggiornare la versione di Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="e8120-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="e8120-283">Courier non aiuta nell'aggiornamento da una versione di Umbraco CMS a un'altra.</span><span class="sxs-lookup"><span data-stu-id="e8120-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="e8120-284">Durante l'aggiornamento della versione di Umbraco CMS, è necessario controllare le eventuali incompatibilità con i moduli personalizzati o i moduli dei partner e le librerie di base di Umbraco.</span><span class="sxs-lookup"><span data-stu-id="e8120-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="e8120-285">Alcune procedure consigliate:</span><span class="sxs-lookup"><span data-stu-id="e8120-285">Here are best practices:</span></span>

* <span data-ttu-id="e8120-286">Eseguire sempre un backup dell'App Web e del database prima di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e8120-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="e8120-287">Nelle App Web di Azure è possibile configurare i backup automatici per i siti Web tramite la funzionalità di backup e ripristinare il sito, se necessario, con l'apposita funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e8120-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="e8120-288">Per altri dettagli, vedere [Come eseguire il backup dell'app Web](web-sites-backup.md) e [Come ripristinare l'app Web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e8120-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="e8120-289">Verificare se i pacchetti dei partner sono compatibili con la versione a cui si esegue l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e8120-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="e8120-290">Nella pagina di download del pacchetto vedere le informazioni sulla compatibilità del progetto con la versione di Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="e8120-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="e8120-291">Per altre informazioni su come aggiornare l'App Web locale, [vedere le indicazioni generali sull'aggiornamento](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="e8120-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="e8120-292">Dopo aver aggiornato il sito di sviluppo locale, pubblicare le modifiche nell'App Web di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e8120-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="e8120-293">Testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-293">Test your application.</span></span> <span data-ttu-id="e8120-294">Se tutto sembra corretto, fare clic sul pulsante **Scambia** per scambiare il sito di gestione temporanea con l'App Web di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="e8120-295">Durante l'operazione di **scambio**, è possibile visualizzare le modifiche alla configurazione dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="e8120-296">Con l'operazione di **scambio** vengono scambiati i database e le App Web.</span><span class="sxs-lookup"><span data-stu-id="e8120-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="e8120-297">Dopo lo **scambio**, l'App Web di produzione sceglie il database umbraco-stage-db e l'App Web di gestione temporanea sceglie il database umbraco-prod-db.</span><span class="sxs-lookup"><span data-stu-id="e8120-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Anteprima dello scambio per la distribuzione di Umbraco CMS.](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="e8120-299">I vantaggi dello scambio dell'App Web e del database sono:</span><span class="sxs-lookup"><span data-stu-id="e8120-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="e8120-300">È possibile eseguire il rollback alla versione precedente dell'App Web con un'altra operazione di **scambio** in caso di errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e8120-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="e8120-301">Per gli aggiornamenti, è necessario distribuire i file e i database dall'App Web di gestione temporanea all'App Web e al database di produzione.</span><span class="sxs-lookup"><span data-stu-id="e8120-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="e8120-302">Quando si distribuiscono file e database, molti aspetti potrebbero andare per il verso sbagliato.</span><span class="sxs-lookup"><span data-stu-id="e8120-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="e8120-303">La funzionalità di **scambio** degli slot consente di ridurre i tempi di inattività durante gli aggiornamenti e di ridurre i rischi di errori che possono verificarsi durante la distribuzione delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="e8120-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="e8120-304">È possibile eseguire **test A/B** usando la funzionalità [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/).</span><span class="sxs-lookup"><span data-stu-id="e8120-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="e8120-305">Questo esempio illustra la flessibilità della piattaforma in cui è possibile creare moduli personalizzati simili al modulo Umbraco Courier per gestire la distribuzione in più ambienti.</span><span class="sxs-lookup"><span data-stu-id="e8120-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="e8120-306">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="e8120-306">References</span></span>
[<span data-ttu-id="e8120-307">Agile Software Development con il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e8120-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="e8120-308">Configurare ambienti di staging per le app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e8120-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="e8120-309">Come bloccare l'accesso Web agli slot di distribuzione non di produzione</span><span class="sxs-lookup"><span data-stu-id="e8120-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
