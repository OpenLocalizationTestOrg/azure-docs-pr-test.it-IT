---
title: Configurazione delle app Web in Servizio app di Azure
description: Come configurare un'app Web nel servizio app di Azure
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="a1b65-103">Configurazione delle app Web in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a1b65-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="a1b65-104">Questo argomento descrive come configurare un'app Web usando il [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="a1b65-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="a1b65-105">Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a1b65-105">Application settings</span></span>
1. <span data-ttu-id="a1b65-106">Nel [portale di Azure]aprire il pannello relativo all'app Web.</span><span class="sxs-lookup"><span data-stu-id="a1b65-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="a1b65-107">Fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="a1b65-108">Fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-108">Click **Application Settings**.</span></span>

![Impostazioni dell'applicazione][configure01]

<span data-ttu-id="a1b65-110">Nel pannello **Impostazioni applicazione** le impostazioni sono raggruppate in diverse categorie.</span><span class="sxs-lookup"><span data-stu-id="a1b65-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="a1b65-111">Impostazioni generali</span><span class="sxs-lookup"><span data-stu-id="a1b65-111">General settings</span></span>
<span data-ttu-id="a1b65-112">**Versioni del framework**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-112">**Framework versions**.</span></span> <span data-ttu-id="a1b65-113">Impostare le opzioni seguenti se l'app usa uno dei seguenti framework:</span><span class="sxs-lookup"><span data-stu-id="a1b65-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="a1b65-114">**.NET Framework**: consente di impostare la versione di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a1b65-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="a1b65-115">**PHP**: impostare la versione PHP oppure scegliere **DISATTIVATO** per disabilitare PHP.</span><span class="sxs-lookup"><span data-stu-id="a1b65-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="a1b65-116">**Java**: selezionare la versione di Java oppure **DISATTIVATO** per disabilitare Java.</span><span class="sxs-lookup"><span data-stu-id="a1b65-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="a1b65-117">Utilizzare l'opzione **Contenitore Web** per scegliere tra le versioni Tomcat e Jetty.</span><span class="sxs-lookup"><span data-stu-id="a1b65-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="a1b65-118">**Python**: selezionare la versione Python oppure **DISATTIVATO** per disabilitare Python.</span><span class="sxs-lookup"><span data-stu-id="a1b65-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="a1b65-119">Per motivi tecnici, l'abilitazione di Java per le proprie app disabilita le opzioni di .NET, PHP e Python.</span><span class="sxs-lookup"><span data-stu-id="a1b65-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="a1b65-120"><a name="platform"></a>
**Piattaforma**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="a1b65-121">Scegliere se eseguire l'app Web in un ambiente a 32 bit o a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="a1b65-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="a1b65-122">L'ambiente a 64 bit richiede la modalità Basic o Standard.</span><span class="sxs-lookup"><span data-stu-id="a1b65-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="a1b65-123">Le modalità Gratuito e Condiviso vengono eseguite sempre in un ambiente a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="a1b65-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="a1b65-124">**Web Socket**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-124">**Web Sockets**.</span></span> <span data-ttu-id="a1b65-125">Impostare **ATTIVATO** per abilitare il protocollo WebSocket, ad esempio se l'app Web usa [ASP.NET SignalR] o [socket.io].</span><span class="sxs-lookup"><span data-stu-id="a1b65-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="a1b65-126"><a name="alwayson"></a>
**Always On**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="a1b65-127">Per impostazione predefinita, le app Web vengono scaricate se restano inattive per un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="a1b65-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="a1b65-128">Ciò consente al sistema di conservare le risorse.</span><span class="sxs-lookup"><span data-stu-id="a1b65-128">This lets the system conserve resources.</span></span> <span data-ttu-id="a1b65-129">In modalità Basic o Standard è possibile abilitare **Always On** affinché l'app rimanga sempre caricata.</span><span class="sxs-lookup"><span data-stu-id="a1b65-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="a1b65-130">Se nell'app vengono eseguiti processi Web continui o processi Web attivati mediante un'espressione CRON è necessario abilitare **Always On**, altrimenti l'esecuzione dei processi Web potrebbe non avvenire in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="a1b65-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="a1b65-131">**Versione pipeline gestita**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="a1b65-132">Consente di impostare la [modalità pipeline]IIS.</span><span class="sxs-lookup"><span data-stu-id="a1b65-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="a1b65-133">Lasciare questa opzione impostata su Integrato (predefinita), tranne nel caso in cui un'app meno recente richieda una versione precedente di IIS.</span><span class="sxs-lookup"><span data-stu-id="a1b65-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="a1b65-134">**Scambio automatico**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-134">**Auto Swap**.</span></span> <span data-ttu-id="a1b65-135">Se si abilita l'opzione Scambio automatico per uno slot di distribuzione, il servizio app immette automaticamente l'app Web in produzione quando si esegue un aggiornamento di quello slot.</span><span class="sxs-lookup"><span data-stu-id="a1b65-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="a1b65-136">Per altre informazioni, vedere [Eseguire la distribuzione negli slot di memorizzazione temporanea per le app Web nel servizio app di Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a1b65-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="a1b65-137">Debug</span><span class="sxs-lookup"><span data-stu-id="a1b65-137">Debugging</span></span>
<span data-ttu-id="a1b65-138">**Debug remoto**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-138">**Remote Debugging**.</span></span> <span data-ttu-id="a1b65-139">Abilita il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="a1b65-139">Enables remote debugging.</span></span> <span data-ttu-id="a1b65-140">Quando viene abilitato, è possibile utilizzare il debugger remoto in Visual Studio per connettersi direttamente all'app Web.</span><span class="sxs-lookup"><span data-stu-id="a1b65-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="a1b65-141">Il debug remoto resterà abilitato per 48 ore.</span><span class="sxs-lookup"><span data-stu-id="a1b65-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="a1b65-142">Impostazioni app</span><span class="sxs-lookup"><span data-stu-id="a1b65-142">App settings</span></span>
<span data-ttu-id="a1b65-143">In questa sezione vengono riportate coppie di nome/valore che verranno caricate all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="a1b65-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="a1b65-144">Per le app.NET, queste impostazioni verranno inserite nella configurazione .NET `AppSettings` in fase di esecuzione, sostituendo le impostazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="a1b65-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="a1b65-145">Le applicazioni PHP, Python, Java e Node possono accedere a queste impostazioni come variabili di ambiente durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="a1b65-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="a1b65-146">Per ciascuna impostazione dell'app vengono create due variabili di ambiente, una con il nome specificato dalla voce dell'impostazione dell'app e l'altra con il prefisso APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="a1b65-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="a1b65-147">Entrambe contengono lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="a1b65-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="a1b65-148">Stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="a1b65-148">Connection strings</span></span>
<span data-ttu-id="a1b65-149">Stringhe di connessione per le risorse collegate.</span><span class="sxs-lookup"><span data-stu-id="a1b65-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="a1b65-150">Per le app .NET, tali stringhe di connessione vengono inserite nelle impostazioni `connectionStrings` della configurazione .NET in fase di runtime, sostituendo le voci esistenti in cui la chiave è uguale al nome del database collegato.</span><span class="sxs-lookup"><span data-stu-id="a1b65-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="a1b65-151">Per le applicazioni PHP, Python, Java e Node queste impostazioni saranno disponibili come variabili di ambiente durante il runtime, con il tipo di connessione come prefisso.</span><span class="sxs-lookup"><span data-stu-id="a1b65-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="a1b65-152">I prefissi delle variabili di ambiente sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1b65-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="a1b65-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="a1b65-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="a1b65-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="a1b65-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="a1b65-155">Database SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="a1b65-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="a1b65-156">Personalizzato: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="a1b65-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="a1b65-157">Ad esempio, se una stringa di connessione MySql venisse denominata `connectionstring1`, l'accesso avverrebbe attraverso la variabile di ambiente`MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="a1b65-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="a1b65-158">Documenti predefiniti</span><span class="sxs-lookup"><span data-stu-id="a1b65-158">Default documents</span></span>
<span data-ttu-id="a1b65-159">Il documento predefinito è rappresentato dalla pagina Web visualizzata nell'URL radice di un sito Web.</span><span class="sxs-lookup"><span data-stu-id="a1b65-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="a1b65-160">Viene utilizzato il primo file corrispondente dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a1b65-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="a1b65-161">Le app Web potrebbero usare moduli che vengono instradati in base all'URL invece di visualizzare contenuto statico, nel caso in cui non sia presente alcun documento predefinito.</span><span class="sxs-lookup"><span data-stu-id="a1b65-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="a1b65-162">Mapping dei gestori</span><span class="sxs-lookup"><span data-stu-id="a1b65-162">Handler mappings</span></span>
<span data-ttu-id="a1b65-163">Usare quest'area per aggiungere processori script personalizzati allo scopo di gestire le richieste di estensioni di file specifiche.</span><span class="sxs-lookup"><span data-stu-id="a1b65-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="a1b65-164">**Estensione**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-164">**Extension**.</span></span> <span data-ttu-id="a1b65-165">L'estensione file da gestire, ad esempio *.php o handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="a1b65-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="a1b65-166">**Percorso processore script**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-166">**Script Processor Path**.</span></span> <span data-ttu-id="a1b65-167">Il percorso assoluto del processore script.</span><span class="sxs-lookup"><span data-stu-id="a1b65-167">The absolute path of the script processor.</span></span> <span data-ttu-id="a1b65-168">Le richieste di file che corrispondono a questo modello saranno elaborate dal processore script.</span><span class="sxs-lookup"><span data-stu-id="a1b65-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="a1b65-169">Utilizzare il percorso `D:\home\site\wwwroot` per fare riferimento alla directory radice della propria app.</span><span class="sxs-lookup"><span data-stu-id="a1b65-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="a1b65-170">**Argomenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-170">**Additional Arguments**.</span></span> <span data-ttu-id="a1b65-171">Argomenti facoltativi della riga dei comando per il processore script</span><span class="sxs-lookup"><span data-stu-id="a1b65-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="a1b65-172">Applicazioni e directory virtuali</span><span class="sxs-lookup"><span data-stu-id="a1b65-172">Virtual applications and directories</span></span>
<span data-ttu-id="a1b65-173">Per configurare applicazioni e directory virtuali, specificare ogni directory virtuale e il corrispondente percorso fisico relativo alla radice del sito.</span><span class="sxs-lookup"><span data-stu-id="a1b65-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="a1b65-174">È facoltativamente possibile selezionare la casella di controllo **Applicazione** in modo da contrassegnare una directory virtuale come applicazione.</span><span class="sxs-lookup"><span data-stu-id="a1b65-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="a1b65-175">Abilitazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="a1b65-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="a1b65-176">Per abilitare i log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="a1b65-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="a1b65-177">Nel pannello dell'app Web, fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="a1b65-178">Fare clic su **Log diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="a1b65-179">Opzioni per la scrittura dei log di diagnostica da un'applicazione Web che supporta la registrazione:</span><span class="sxs-lookup"><span data-stu-id="a1b65-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="a1b65-180">**Registrazione applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-180">**Application Logging**.</span></span> <span data-ttu-id="a1b65-181">Consente di scrivere i log delle applicazioni nel file system.</span><span class="sxs-lookup"><span data-stu-id="a1b65-181">Writes application logs to the file system.</span></span> <span data-ttu-id="a1b65-182">La registrazione ha una durata di 12 ore.</span><span class="sxs-lookup"><span data-stu-id="a1b65-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="a1b65-183">**Livello**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-183">**Level**.</span></span> <span data-ttu-id="a1b65-184">Quando viene abilitata la registrazione, questa opzione consente di specificare la quantità di informazioni registrata (Errore, Avviso, Informazioni, Dettagliato).</span><span class="sxs-lookup"><span data-stu-id="a1b65-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="a1b65-185">**Registrazione del server Web**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-185">**Web server logging**.</span></span> <span data-ttu-id="a1b65-186">I log vengono salvati nel formato file di log esteso W3C.</span><span class="sxs-lookup"><span data-stu-id="a1b65-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="a1b65-187">**Messaggi di errore dettagliati**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-187">**Detailed error messages**.</span></span> <span data-ttu-id="a1b65-188">Consente di salvare messaggi di errore dettagliati in file htm.</span><span class="sxs-lookup"><span data-stu-id="a1b65-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="a1b65-189">I file vengono salvati nel percorso /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="a1b65-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="a1b65-190">**Traccia delle richieste non riuscite**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-190">**Failed request tracing**.</span></span> <span data-ttu-id="a1b65-191">Consente di registrare le richieste non riuscite ai file XML.</span><span class="sxs-lookup"><span data-stu-id="a1b65-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="a1b65-192">I file vengono salvati in /LogFiles/W3SVC*xxx*, dove xxx è un identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="a1b65-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="a1b65-193">Questa cartella contiene un file XSL e uno o più file XML.</span><span class="sxs-lookup"><span data-stu-id="a1b65-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="a1b65-194">Assicurarsi di scaricare il file XSL, perché fornisce la funzionalità di formattazione e filtro dei contenuti dei file XML.</span><span class="sxs-lookup"><span data-stu-id="a1b65-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="a1b65-195">Per visualizzare i file di log, è necessario creare le credenziali FTP, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="a1b65-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="a1b65-196">Nel pannello dell'app Web, fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="a1b65-197">Fare clic su **Credenziali distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="a1b65-198">Immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="a1b65-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="a1b65-199">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-199">Click **Save**.</span></span>

![Reimpostare le credenziali di distribuzione][configure03]

<span data-ttu-id="a1b65-201">Il nome utente completo FTP è "app\nomeutente", dove *app* è il nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a1b65-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="a1b65-202">Il nome utente è elencato nel pannello dell'app Web in **Elementi essenziali**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![Credenziali di distribuzione FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="a1b65-204">Altre attività di configurazione</span><span class="sxs-lookup"><span data-stu-id="a1b65-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="a1b65-205">SSL</span><span class="sxs-lookup"><span data-stu-id="a1b65-205">SSL</span></span>
<span data-ttu-id="a1b65-206">In modalità Basic o Standard è possibile caricare certificati SSL per un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a1b65-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="a1b65-207">Per altre informazioni, vedere [Abilitare HTTPS per un'app Web].</span><span class="sxs-lookup"><span data-stu-id="a1b65-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="a1b65-208">Per visualizzare i certificati caricati, fare clic su **Tutte le impostazioni** > **Domini e SSL personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="a1b65-209">Nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="a1b65-209">Domain names</span></span>
<span data-ttu-id="a1b65-210">Aggiungere nomi di dominio personalizzati per la propria app Web.</span><span class="sxs-lookup"><span data-stu-id="a1b65-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="a1b65-211">Per ulteriori informazioni, vedere [Configurare un nome di dominio personalizzato per un'app Web nel servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="a1b65-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="a1b65-212">Per visualizzare i nomi di dominio, fare clic su **Tutte le impostazioni** > **Domini e SSL personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="a1b65-213">Deployments</span><span class="sxs-lookup"><span data-stu-id="a1b65-213">Deployments</span></span>
* <span data-ttu-id="a1b65-214">Configurare la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="a1b65-214">Set up continuous deployment.</span></span> <span data-ttu-id="a1b65-215">Vedere [Uso di Git per distribuire app Web nel servizio App di Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a1b65-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="a1b65-216">Slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a1b65-216">Deployment slots.</span></span> <span data-ttu-id="a1b65-217">Vedere [Configurare ambienti di staging per le app Web nel servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="a1b65-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="a1b65-218">Per visualizzare gli slot di distribuzione, fare clic su **Tutte le impostazioni** > **Slot di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="a1b65-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="a1b65-219">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="a1b65-219">Monitoring</span></span>
<span data-ttu-id="a1b65-220">In modalità Basic o Standard è possibile testare la disponibilità degli endpoint HTTP o HTTPS, da un numero massimo di tre posizioni geograficamente distribuite.</span><span class="sxs-lookup"><span data-stu-id="a1b65-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="a1b65-221">Un test di monitoraggio ha esito negativo se il codice della risposta HTTP è un errore (4xx o 5xx) o se la risposta richiede più di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="a1b65-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="a1b65-222">Un endpoint è considerato disponibile se il test di monitoraggio ha esito positivo da tutte le posizioni specificate.</span><span class="sxs-lookup"><span data-stu-id="a1b65-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="a1b65-223">Per ulteriori informazioni, vedere [Procedura: monitorare lo stato degli endpoint].</span><span class="sxs-lookup"><span data-stu-id="a1b65-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="a1b65-224">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app], dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="a1b65-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a1b65-225">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="a1b65-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a1b65-226">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1b65-226">Next steps</span></span>
* <span data-ttu-id="a1b65-227">[Configurare un nome di dominio personalizzato nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="a1b65-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="a1b65-228">[Abilitare HTTPS per un'app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="a1b65-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="a1b65-229">[Scalare un'app Web nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="a1b65-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="a1b65-230">[Informazioni di base sul monitoraggio di App Web nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="a1b65-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="a1b65-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="a1b65-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="a1b65-232">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="a1b65-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="a1b65-233">[Configurare un nome di dominio personalizzato nel servizio app di Azure]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="a1b65-234">[Configurare ambienti di staging per le app Web nel servizio app di Azure]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="a1b65-235">[Abilitare HTTPS per un'app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="a1b65-236">[Procedura: monitorare lo stato degli endpoint]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="a1b65-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="a1b65-237">[Informazioni di base sul monitoraggio di App Web nel servizio app di Azure]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="a1b65-238">[modalità pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="a1b65-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="a1b65-239">[Scalare un'app Web nel servizio app di Azure]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="a1b65-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="a1b65-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="a1b65-241">[Prova il servizio app]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="a1b65-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
