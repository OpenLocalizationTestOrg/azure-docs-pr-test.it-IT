---
title: aaaConfigure web App in Azure App Service
description: Come tooconfigure un'app web di servizi di App di Azure
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
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="823f0-103">Configurazione delle app Web in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="823f0-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="823f0-104">Questo argomento viene illustrato come un'app web utilizzando tooconfigure hello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="823f0-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="823f0-105">Impostazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="823f0-105">Application settings</span></span>
1. <span data-ttu-id="823f0-106">In hello [portale Azure], aprire il pannello hello per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="823f0-107">Fare clic su **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="823f0-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="823f0-108">Fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="823f0-108">Click **Application Settings**.</span></span>

![Impostazioni dell'applicazione][configure01]

<span data-ttu-id="823f0-110">Hello **le impostazioni dell'applicazione** blade dispone di impostazioni raggruppate in categorie diverse.</span><span class="sxs-lookup"><span data-stu-id="823f0-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="823f0-111">Impostazioni generali</span><span class="sxs-lookup"><span data-stu-id="823f0-111">General settings</span></span>
<span data-ttu-id="823f0-112">**Versioni del framework**.</span><span class="sxs-lookup"><span data-stu-id="823f0-112">**Framework versions**.</span></span> <span data-ttu-id="823f0-113">Impostare le opzioni seguenti se l'app usa uno dei seguenti framework:</span><span class="sxs-lookup"><span data-stu-id="823f0-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="823f0-114">**.NET framework**: versione di .NET framework di Set hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="823f0-115">**PHP**: imposta la versione PHP hello, o **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="823f0-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="823f0-116">**Java**: versione di Java selezionare hello o **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="823f0-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="823f0-117">Hello utilizzare **contenitore Web** toochoose opzione tra le versioni di Tomcat e Jetty.</span><span class="sxs-lookup"><span data-stu-id="823f0-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="823f0-118">**Python**: versione di Python hello selezionare, o **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="823f0-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="823f0-119">Per motivi tecnici, l'abilitazione di Java per l'app disabilita le opzioni di hello .NET, PHP e Python.</span><span class="sxs-lookup"><span data-stu-id="823f0-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="823f0-120"><a name="platform"></a>
**Piattaforma**.</span><span class="sxs-lookup"><span data-stu-id="823f0-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="823f0-121">Scegliere se eseguire l'app Web in un ambiente a 32 bit o a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="823f0-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="823f0-122">ambiente a 64 bit Hello richiede la modalità Basic o Standard.</span><span class="sxs-lookup"><span data-stu-id="823f0-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="823f0-123">Le modalità Gratuito e Condiviso vengono eseguite sempre in un ambiente a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="823f0-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="823f0-124">**Web Socket**.</span><span class="sxs-lookup"><span data-stu-id="823f0-124">**Web Sockets**.</span></span> <span data-ttu-id="823f0-125">Impostare **ON** tooenable hello protocollo WebSocket, ad esempio, se l'app web Usa [ASP.NET SignalR] o [socket.io].</span><span class="sxs-lookup"><span data-stu-id="823f0-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="823f0-126"><a name="alwayson"></a>
**Always On**.</span><span class="sxs-lookup"><span data-stu-id="823f0-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="823f0-127">Per impostazione predefinita, le app Web vengono scaricate se restano inattive per un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="823f0-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="823f0-128">Ciò consente di risparmiare risorse di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="823f0-129">In modalità Basic o Standard, è possibile abilitare **Always On** tookeep hello app caricato tutto il tempo hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="823f0-130">Se i processi Web continui l'esecuzione dell'app o esecuzioni di processi Web attivata utilizzando un'espressione CRON, è consigliabile abilitare **Always On**, o i processi web hello potrebbero non essere eseguita in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="823f0-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="823f0-131">**Versione pipeline gestita**.</span><span class="sxs-lookup"><span data-stu-id="823f0-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="823f0-132">Set di hello IIS [modalità pipeline].</span><span class="sxs-lookup"><span data-stu-id="823f0-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="823f0-133">Lasciare questo impostato tooIntegrated (impostazione predefinita hello), a meno che non si dispone di un'applicazione legacy che richiede una versione precedente di IIS.</span><span class="sxs-lookup"><span data-stu-id="823f0-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="823f0-134">**Scambio automatico**.</span><span class="sxs-lookup"><span data-stu-id="823f0-134">**Auto Swap**.</span></span> <span data-ttu-id="823f0-135">Se si abilita lo scambio automatico per uno slot di distribuzione, il servizio App automaticamente scambiare hello web app nell'ambiente di produzione quando si esegue il push uno slot toothat di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="823f0-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="823f0-136">Per ulteriori informazioni, vedere [distribuire toostaging slot per le app web in Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="823f0-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="823f0-137">Debug</span><span class="sxs-lookup"><span data-stu-id="823f0-137">Debugging</span></span>
<span data-ttu-id="823f0-138">**Debug remoto**.</span><span class="sxs-lookup"><span data-stu-id="823f0-138">**Remote Debugging**.</span></span> <span data-ttu-id="823f0-139">Abilita il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="823f0-139">Enables remote debugging.</span></span> <span data-ttu-id="823f0-140">Quando abilitata, è possibile utilizzare debugger remoto hello in Visual Studio tooconnect direttamente tooyour app web.</span><span class="sxs-lookup"><span data-stu-id="823f0-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="823f0-141">Il debug remoto resterà abilitato per 48 ore.</span><span class="sxs-lookup"><span data-stu-id="823f0-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="823f0-142">Impostazioni app</span><span class="sxs-lookup"><span data-stu-id="823f0-142">App settings</span></span>
<span data-ttu-id="823f0-143">In questa sezione vengono riportate coppie di nome/valore che verranno caricate all'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="823f0-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="823f0-144">Per le app.NET, queste impostazioni verranno inserite nella configurazione .NET `AppSettings` in fase di esecuzione, sostituendo le impostazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="823f0-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="823f0-145">Le applicazioni PHP, Python, Java e Node possono accedere a queste impostazioni come variabili di ambiente durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="823f0-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="823f0-146">Per ogni impostazione dell'app, vengono create due variabili di ambiente. uno con nome hello specificato dalla voce di impostazione app hello e un altro con un prefisso di APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="823f0-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="823f0-147">Entrambi contengono hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="823f0-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="823f0-148">Stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="823f0-148">Connection strings</span></span>
<span data-ttu-id="823f0-149">Stringhe di connessione per le risorse collegate.</span><span class="sxs-lookup"><span data-stu-id="823f0-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="823f0-150">Per le applicazioni .NET, queste stringhe di connessione vengono inserite in una configurazione di .NET `connectionStrings` impostazioni in fase di esecuzione, sovrascrivendo le voci esistenti laddove la chiave hello corrisponde hello nome del database collegato.</span><span class="sxs-lookup"><span data-stu-id="823f0-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="823f0-151">Per le applicazioni Java, Python, PHP e del nodo, queste impostazioni saranno disponibili come variabili di ambiente in fase di esecuzione con il tipo di connessione hello preceduta.</span><span class="sxs-lookup"><span data-stu-id="823f0-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="823f0-152">di seguito sono riportati i prefissi variabile di ambiente Hello:</span><span class="sxs-lookup"><span data-stu-id="823f0-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="823f0-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="823f0-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="823f0-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="823f0-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="823f0-155">Database SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="823f0-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="823f0-156">Personalizzato: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="823f0-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="823f0-157">Ad esempio, se una stringa di connessione MySql nominata `connectionstring1`, viene eseguito tramite la variabile di ambiente hello `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="823f0-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="823f0-158">Documenti predefiniti</span><span class="sxs-lookup"><span data-stu-id="823f0-158">Default documents</span></span>
<span data-ttu-id="823f0-159">documento predefinito Hello è una pagina web hello che viene visualizzato all'URL radice hello per un sito Web.</span><span class="sxs-lookup"><span data-stu-id="823f0-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="823f0-160">Hello primo corrispondente file hello elenco viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="823f0-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="823f0-161">Le app Web potrebbero usare moduli che vengono instradati in base all'URL invece di visualizzare contenuto statico, nel caso in cui non sia presente alcun documento predefinito.</span><span class="sxs-lookup"><span data-stu-id="823f0-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="823f0-162">Mapping dei gestori</span><span class="sxs-lookup"><span data-stu-id="823f0-162">Handler mappings</span></span>
<span data-ttu-id="823f0-163">Usare questo richieste toohandle di processori di area tooadd script personalizzato per le estensioni di file specifico.</span><span class="sxs-lookup"><span data-stu-id="823f0-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="823f0-164">**Estensione**.</span><span class="sxs-lookup"><span data-stu-id="823f0-164">**Extension**.</span></span> <span data-ttu-id="823f0-165">toobe estensione di file Hello gestito, ad esempio *.php o fcgi.</span><span class="sxs-lookup"><span data-stu-id="823f0-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="823f0-166">**Percorso processore script**.</span><span class="sxs-lookup"><span data-stu-id="823f0-166">**Script Processor Path**.</span></span> <span data-ttu-id="823f0-167">percorso assoluto di Hello del processore script hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="823f0-168">Verranno elaborati dal processore script hello toofiles le richieste che corrispondono l'estensione del file hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="823f0-169">Usa percorso hello `D:\home\site\wwwroot` directory radice dell'applicazione tooyour toorefer.</span><span class="sxs-lookup"><span data-stu-id="823f0-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="823f0-170">**Argomenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="823f0-170">**Additional Arguments**.</span></span> <span data-ttu-id="823f0-171">Argomenti della riga di comando facoltativi per il processore script hello</span><span class="sxs-lookup"><span data-stu-id="823f0-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="823f0-172">Applicazioni e directory virtuali</span><span class="sxs-lookup"><span data-stu-id="823f0-172">Virtual applications and directories</span></span>
<span data-ttu-id="823f0-173">tooconfigure applicazioni e directory virtuali, specificare ogni directory virtuale e la radice del sito Web di toohello relativo percorso fisico corrispondente.</span><span class="sxs-lookup"><span data-stu-id="823f0-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="823f0-174">Facoltativamente, è possibile selezionare hello **applicazione** casella di controllo toomark una directory virtuale come un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="823f0-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="823f0-175">Abilitazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="823f0-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="823f0-176">log di diagnostica tooenable:</span><span class="sxs-lookup"><span data-stu-id="823f0-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="823f0-177">Nel Pannello di hello per le app web, fare clic su **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="823f0-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="823f0-178">Fare clic su **Log diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="823f0-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="823f0-179">Opzioni per la scrittura dei log di diagnostica da un'applicazione Web che supporta la registrazione:</span><span class="sxs-lookup"><span data-stu-id="823f0-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="823f0-180">**Registrazione applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="823f0-180">**Application Logging**.</span></span> <span data-ttu-id="823f0-181">Scrive i log di applicazione di sistema di file toohello.</span><span class="sxs-lookup"><span data-stu-id="823f0-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="823f0-182">La registrazione ha una durata di 12 ore.</span><span class="sxs-lookup"><span data-stu-id="823f0-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="823f0-183">**Livello**.</span><span class="sxs-lookup"><span data-stu-id="823f0-183">**Level**.</span></span> <span data-ttu-id="823f0-184">Quando è abilitata la registrazione dell'applicazione, questa opzione specifica quantità hello di informazioni che saranno registrati (errore, avviso, informazioni o dettagliato).</span><span class="sxs-lookup"><span data-stu-id="823f0-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="823f0-185">**Registrazione del server Web**.</span><span class="sxs-lookup"><span data-stu-id="823f0-185">**Web server logging**.</span></span> <span data-ttu-id="823f0-186">I log vengono salvati nel formato di file registro esteso W3C hello.</span><span class="sxs-lookup"><span data-stu-id="823f0-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="823f0-187">**Messaggi di errore dettagliati**.</span><span class="sxs-lookup"><span data-stu-id="823f0-187">**Detailed error messages**.</span></span> <span data-ttu-id="823f0-188">Consente di salvare messaggi di errore dettagliati in file htm.</span><span class="sxs-lookup"><span data-stu-id="823f0-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="823f0-189">Hello file vengono salvati in /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="823f0-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="823f0-190">**Traccia delle richieste non riuscite**.</span><span class="sxs-lookup"><span data-stu-id="823f0-190">**Failed request tracing**.</span></span> <span data-ttu-id="823f0-191">Log non è stato possibile richieste tooXML file.</span><span class="sxs-lookup"><span data-stu-id="823f0-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="823f0-192">Hello i file vengono salvati in file di registro/W3SVC*xxx*, dove xxx è un identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="823f0-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="823f0-193">Questa cartella contiene un file XSL e uno o più file XML.</span><span class="sxs-lookup"><span data-stu-id="823f0-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="823f0-194">Verificare che hello toodownload file XSL, perché fornisce funzionalità per la formattazione e filtrare il contenuto di hello hello dei file di XML.</span><span class="sxs-lookup"><span data-stu-id="823f0-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="823f0-195">file di log hello tooview, è necessario creare le credenziali FTP, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="823f0-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="823f0-196">Nel Pannello di hello per le app web, fare clic su **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="823f0-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="823f0-197">Fare clic su **Credenziali distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="823f0-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="823f0-198">Immettere un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="823f0-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="823f0-199">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="823f0-199">Click **Save**.</span></span>

![Reimpostare le credenziali di distribuzione][configure03]

<span data-ttu-id="823f0-201">il nome utente FTP completo di Hello è "app\username" in cui *app* hello nome dell'app web.</span><span class="sxs-lookup"><span data-stu-id="823f0-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="823f0-202">Hello nome utente è elencato nel pannello app web hello in **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="823f0-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Credenziali di distribuzione FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="823f0-204">Altre attività di configurazione</span><span class="sxs-lookup"><span data-stu-id="823f0-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="823f0-205">SSL</span><span class="sxs-lookup"><span data-stu-id="823f0-205">SSL</span></span>
<span data-ttu-id="823f0-206">In modalità Basic o Standard è possibile caricare certificati SSL per un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="823f0-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="823f0-207">Per altre informazioni, vedere [Abilitare HTTPS per un'app Web].</span><span class="sxs-lookup"><span data-stu-id="823f0-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="823f0-208">i certificati caricati, fare clic su tooview **tutte le impostazioni** > **i domini personalizzati e SSL**.</span><span class="sxs-lookup"><span data-stu-id="823f0-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="823f0-209">Nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="823f0-209">Domain names</span></span>
<span data-ttu-id="823f0-210">Aggiungere nomi di dominio personalizzati per la propria app Web.</span><span class="sxs-lookup"><span data-stu-id="823f0-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="823f0-211">Per ulteriori informazioni, vedere [Configurare un nome di dominio personalizzato per un'app Web nel servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="823f0-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="823f0-212">i nomi di dominio, fare clic su tooview **tutte le impostazioni** > **i domini personalizzati e SSL**.</span><span class="sxs-lookup"><span data-stu-id="823f0-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="823f0-213">Deployments</span><span class="sxs-lookup"><span data-stu-id="823f0-213">Deployments</span></span>
* <span data-ttu-id="823f0-214">Configurare la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="823f0-214">Set up continuous deployment.</span></span> <span data-ttu-id="823f0-215">Vedere [toodeploy Git usando le app Web in Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="823f0-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="823f0-216">Slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="823f0-216">Deployment slots.</span></span> <span data-ttu-id="823f0-217">Vedere [distribuire ambienti tooStaging per le app Web in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="823f0-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="823f0-218">gli intervalli di distribuzione, fare clic su tooview **tutte le impostazioni** > **gli slot di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="823f0-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="823f0-219">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="823f0-219">Monitoring</span></span>
<span data-ttu-id="823f0-220">In modalità Basic o Standard, è possibile verificare la disponibilità di hello di endpoint HTTP o HTTPS, da backup posizioni geograficamente distribuite toothree.</span><span class="sxs-lookup"><span data-stu-id="823f0-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="823f0-221">Un test di monitoraggio non riesce se hello codice di risposta HTTP è un errore (4xx o 5xx) o risposta hello richiede più di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="823f0-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="823f0-222">Un endpoint viene considerato disponibile se i test di monitoraggio hello esito positivo da tutte hello specificati percorsi.</span><span class="sxs-lookup"><span data-stu-id="823f0-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="823f0-223">Per ulteriori informazioni, vedere [Procedura: monitorare lo stato degli endpoint].</span><span class="sxs-lookup"><span data-stu-id="823f0-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="823f0-224">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App], in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="823f0-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="823f0-225">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="823f0-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="823f0-226">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="823f0-226">Next steps</span></span>
* <span data-ttu-id="823f0-227">[Configurare un nome di dominio personalizzato nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="823f0-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="823f0-228">[Abilitare HTTPS per un'app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="823f0-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="823f0-229">[Scalare un'app Web nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="823f0-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="823f0-230">[Informazioni di base sul monitoraggio di App Web nel servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="823f0-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[portale Azure]: https://portal.azure.com/
[Configurare un nome di dominio personalizzato nel servizio app di Azure]: ./app-service-web-tutorial-custom-domain.md
[distribuire ambienti tooStaging per le app Web in Azure App Service]: ./web-sites-staged-publishing.md
[Abilitare HTTPS per un'app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[Procedura: monitorare lo stato degli endpoint]: http://go.microsoft.com/fwLink/?LinkID=279906
[Informazioni di base sul monitoraggio di App Web nel servizio app di Azure]: ./web-sites-monitor.md
[modalità pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Scalare un'app Web nel servizio app di Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[tenta di servizio App]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
