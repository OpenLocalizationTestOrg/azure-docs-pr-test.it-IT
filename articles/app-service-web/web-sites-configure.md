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
# <a name="configure-web-apps-in-azure-app-service"></a>Configurazione delle app Web in Servizio app di Azure
Questo argomento viene illustrato come un'app web utilizzando tooconfigure hello [portale Azure].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Impostazioni dell'applicazione
1. In hello [portale Azure], aprire il pannello hello per l'app web hello.
2. Fare clic su **Tutte le impostazioni**.
3. Fare clic su **Impostazioni applicazione**.

![Impostazioni dell'applicazione][configure01]

Hello **le impostazioni dell'applicazione** blade dispone di impostazioni raggruppate in categorie diverse.

### <a name="general-settings"></a>Impostazioni generali
**Versioni del framework**. Impostare le opzioni seguenti se l'app usa uno dei seguenti framework: 

* **.NET framework**: versione di .NET framework di Set hello. 
* **PHP**: imposta la versione PHP hello, o **OFF** toodisable PHP. 
* **Java**: versione di Java selezionare hello o **OFF** toodisable Java. Hello utilizzare **contenitore Web** toochoose opzione tra le versioni di Tomcat e Jetty.
* **Python**: versione di Python hello selezionare, o **OFF** toodisable Python.

Per motivi tecnici, l'abilitazione di Java per l'app disabilita le opzioni di hello .NET, PHP e Python.

<a name="platform"></a>
**Piattaforma**. Scegliere se eseguire l'app Web in un ambiente a 32 bit o a 64 bit. ambiente a 64 bit Hello richiede la modalità Basic o Standard. Le modalità Gratuito e Condiviso vengono eseguite sempre in un ambiente a 32 bit.

**Web Socket**. Impostare **ON** tooenable hello protocollo WebSocket, ad esempio, se l'app web Usa [ASP.NET SignalR] o [socket.io].

<a name="alwayson"></a>
**Always On**. Per impostazione predefinita, le app Web vengono scaricate se restano inattive per un determinato periodo di tempo. Ciò consente di risparmiare risorse di sistema hello. In modalità Basic o Standard, è possibile abilitare **Always On** tookeep hello app caricato tutto il tempo hello. Se i processi Web continui l'esecuzione dell'app o esecuzioni di processi Web attivata utilizzando un'espressione CRON, è consigliabile abilitare **Always On**, o i processi web hello potrebbero non essere eseguita in modo affidabile.

**Versione pipeline gestita**. Set di hello IIS [modalità pipeline]. Lasciare questo impostato tooIntegrated (impostazione predefinita hello), a meno che non si dispone di un'applicazione legacy che richiede una versione precedente di IIS.

**Scambio automatico**. Se si abilita lo scambio automatico per uno slot di distribuzione, il servizio App automaticamente scambiare hello web app nell'ambiente di produzione quando si esegue il push uno slot toothat di aggiornamento. Per ulteriori informazioni, vedere [distribuire toostaging slot per le app web in Azure App Service](web-sites-staged-publishing.md).

### <a name="debugging"></a>Debug
**Debug remoto**. Abilita il debug remoto. Quando abilitata, è possibile utilizzare debugger remoto hello in Visual Studio tooconnect direttamente tooyour app web. Il debug remoto resterà abilitato per 48 ore. 

### <a name="app-settings"></a>Impostazioni app
In questa sezione vengono riportate coppie di nome/valore che verranno caricate all'avvio dell'app. 

* Per le app.NET, queste impostazioni verranno inserite nella configurazione .NET `AppSettings` in fase di esecuzione, sostituendo le impostazioni esistenti. 
* Le applicazioni PHP, Python, Java e Node possono accedere a queste impostazioni come variabili di ambiente durante il runtime. Per ogni impostazione dell'app, vengono create due variabili di ambiente. uno con nome hello specificato dalla voce di impostazione app hello e un altro con un prefisso di APPSETTING_. Entrambi contengono hello stesso valore.

### <a name="connection-strings"></a>Stringhe di connessione
Stringhe di connessione per le risorse collegate. 

Per le applicazioni .NET, queste stringhe di connessione vengono inserite in una configurazione di .NET `connectionStrings` impostazioni in fase di esecuzione, sovrascrivendo le voci esistenti laddove la chiave hello corrisponde hello nome del database collegato. 

Per le applicazioni Java, Python, PHP e del nodo, queste impostazioni saranno disponibili come variabili di ambiente in fase di esecuzione con il tipo di connessione hello preceduta. di seguito sono riportati i prefissi variabile di ambiente Hello: 

* SQL Server: `SQLCONNSTR_`
* MySQL: `MYSQLCONNSTR_`
* Database SQL: `SQLAZURECONNSTR_`
* Personalizzato: `CUSTOMCONNSTR_`

Ad esempio, se una stringa di connessione MySql nominata `connectionstring1`, viene eseguito tramite la variabile di ambiente hello `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Documenti predefiniti
documento predefinito Hello è una pagina web hello che viene visualizzato all'URL radice hello per un sito Web.  Hello primo corrispondente file hello elenco viene utilizzato. 

Le app Web potrebbero usare moduli che vengono instradati in base all'URL invece di visualizzare contenuto statico, nel caso in cui non sia presente alcun documento predefinito.    

### <a name="handler-mappings"></a>Mapping dei gestori
Usare questo richieste toohandle di processori di area tooadd script personalizzato per le estensioni di file specifico. 

* **Estensione**. toobe estensione di file Hello gestito, ad esempio *.php o fcgi. 
* **Percorso processore script**. percorso assoluto di Hello del processore script hello. Verranno elaborati dal processore script hello toofiles le richieste che corrispondono l'estensione del file hello. Usa percorso hello `D:\home\site\wwwroot` directory radice dell'applicazione tooyour toorefer.
* **Argomenti aggiuntivi**. Argomenti della riga di comando facoltativi per il processore script hello 

### <a name="virtual-applications-and-directories"></a>Applicazioni e directory virtuali
tooconfigure applicazioni e directory virtuali, specificare ogni directory virtuale e la radice del sito Web di toohello relativo percorso fisico corrispondente. Facoltativamente, è possibile selezionare hello **applicazione** casella di controllo toomark una directory virtuale come un'applicazione.

## <a name="enabling-diagnostic-logs"></a>Abilitazione dei log di diagnostica
log di diagnostica tooenable:

1. Nel Pannello di hello per le app web, fare clic su **tutte le impostazioni**.
2. Fare clic su **Log diagnostici**. 

Opzioni per la scrittura dei log di diagnostica da un'applicazione Web che supporta la registrazione: 

* **Registrazione applicazioni**. Scrive i log di applicazione di sistema di file toohello. La registrazione ha una durata di 12 ore. 

**Livello**. Quando è abilitata la registrazione dell'applicazione, questa opzione specifica quantità hello di informazioni che saranno registrati (errore, avviso, informazioni o dettagliato).

**Registrazione del server Web**. I log vengono salvati nel formato di file registro esteso W3C hello. 

**Messaggi di errore dettagliati**. Consente di salvare messaggi di errore dettagliati in file htm. Hello file vengono salvati in /LogFiles/DetailedErrors. 

**Traccia delle richieste non riuscite**. Log non è stato possibile richieste tooXML file. Hello i file vengono salvati in file di registro/W3SVC*xxx*, dove xxx è un identificatore univoco. Questa cartella contiene un file XSL e uno o più file XML. Verificare che hello toodownload file XSL, perché fornisce funzionalità per la formattazione e filtrare il contenuto di hello hello dei file di XML.

file di log hello tooview, è necessario creare le credenziali FTP, come indicato di seguito:

1. Nel Pannello di hello per le app web, fare clic su **tutte le impostazioni**.
2. Fare clic su **Credenziali distribuzione**.
3. Immettere un nome utente e una password.
4. Fare clic su **Salva**.

![Reimpostare le credenziali di distribuzione][configure03]

il nome utente FTP completo di Hello è "app\username" in cui *app* hello nome dell'app web. Hello nome utente è elencato nel pannello app web hello in **Essentials**.  

![Credenziali di distribuzione FTP][configure02]

## <a name="other-configuration-tasks"></a>Altre attività di configurazione
### <a name="ssl"></a>SSL
In modalità Basic o Standard è possibile caricare certificati SSL per un dominio personalizzato. Per altre informazioni, vedere [Abilitare HTTPS per un'app Web]. 

i certificati caricati, fare clic su tooview **tutte le impostazioni** > **i domini personalizzati e SSL**.

### <a name="domain-names"></a>Nomi di dominio
Aggiungere nomi di dominio personalizzati per la propria app Web. Per ulteriori informazioni, vedere [Configurare un nome di dominio personalizzato per un'app Web nel servizio app di Azure].

i nomi di dominio, fare clic su tooview **tutte le impostazioni** > **i domini personalizzati e SSL**.

### <a name="deployments"></a>Deployments
* Configurare la distribuzione continua. Vedere [toodeploy Git usando le app Web in Azure App Service](web-sites-deploy.md).
* Slot di distribuzione. Vedere [distribuire ambienti tooStaging per le app Web in Azure App Service].

gli intervalli di distribuzione, fare clic su tooview **tutte le impostazioni** > **gli slot di distribuzione**.

### <a name="monitoring"></a>Monitoraggio
In modalità Basic o Standard, è possibile verificare la disponibilità di hello di endpoint HTTP o HTTPS, da backup posizioni geograficamente distribuite toothree. Un test di monitoraggio non riesce se hello codice di risposta HTTP è un errore (4xx o 5xx) o risposta hello richiede più di 30 secondi. Un endpoint viene considerato disponibile se i test di monitoraggio hello esito positivo da tutte hello specificati percorsi. 

Per ulteriori informazioni, vedere [Procedura: monitorare lo stato degli endpoint].

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App], in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Configurare un nome di dominio personalizzato nel servizio app di Azure]
* [Abilitare HTTPS per un'app in Azure App Service]
* [Scalare un'app Web nel servizio app di Azure]
* [Informazioni di base sul monitoraggio di App Web nel servizio app di Azure]

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
