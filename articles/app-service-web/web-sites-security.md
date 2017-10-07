---
title: aaaSecure un'app in Azure App Service
description: Informazioni su come toosecure un'app web, un back-end dell'app mobile o app per le API in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Garantire la sicurezza di un'app in Servizio app di Azure
Questo articolo offre informazioni iniziali sulla sicurezza di app Web, back-end per app per dispositivi mobili o app per le API in Servizio app di Azure. 

Servizio app di Azure offre due livelli di sicurezza: 

* **Protezione dell'infrastruttura e piattaforma** -trust hello Azure toohave services è necessario tooactually eseguire operazioni in modo protetto nel cloud hello.
* **Sicurezza delle applicazioni** -è necessario toodesign hello app stessa, in modo sicuro. Sono inclusi come si integra con Azure Active Directory, come gestire i certificati e come è assicurarsi che è possibile comunicare in modo sicuro toodifferent servizi. 

#### <a name="infrastructure-and-platform-security"></a>Sicurezza dell'infrastruttura e della piattaforma:
Poiché il servizio App mantiene macchine virtuali di Azure hello, archiviazione, le connessioni di rete, Framework web, gestione e le funzionalità di integrazione e molto altro ancora, è attivamente protetta e finalizzato e attraversa conformità violenta e assicurarsi che i controlli su un toomake continua che:

* Le applicazioni di servizio App sono isolate da entrambi hello Internet e da hello risorse di Azure di altri clienti.
* La comunicazione di segreti (ad esempio, stringhe di connessione) tra l'app del servizio app e altre risorse di Azure (ad esempio, database SQL) in un gruppo di risorse rimanga all'interno di Azure e non superi i limiti di rete. I segreti siano sempre crittografati.
* Tutte le comunicazioni tra l'app del servizio app e le risorse esterne, ad esempio gestione di PowerShell, interfaccia della riga di comando, Azure SDK, API REST e connessioni ibride, siano crittografate correttamente.
* La gestione delle minacce 24 ore su 24 protegge le risorse del servizio app da malware, attacchi Distributed Denial of Service (DDoS), attacchi man-in-the-middle (MITM) e altre minacce. 

Per altre informazioni sulla sicurezza della piattaforma e dell'infrastruttura in Azure, vedere [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Sicurezza delle applicazioni:
Sebbene Azure è responsabile per la protezione dell'infrastruttura di hello e una piattaforma che l'applicazione viene eseguita in, è toosecure la responsabilità dell'applicazione stessa. In altre parole, è necessario toodevelop, distribuire e gestire il codice dell'applicazione e i contenuti in modo sicuro. In caso contrario, il codice dell'applicazione o il contenuto può ancora essere toothreats vulnerabile ad esempio:

* Attacchi SQL injection
* Hijack della sessione
* Script da altri siti
* Attacchi MITM a livello di applicazione
* Attacchi DDoS a livello di applicazione

Una trattazione completa delle considerazioni sulla sicurezza per le applicazioni basate su web esula dall'ambito di hello di questo documento. Come punto di partenza per ulteriori informazioni sulla sicurezza dell'applicazione, vedere hello [aprire Web applicazione sicurezza progetto (OWASP)](https://www.owasp.org/index.php/Main_Page), in particolare hello [progetto primi 10.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), che elenchi hello primi 10 corrente web critici applicazione difetti di protezione, come determinato dai membri OWASP.

## <a name="perform-penetration-testing-on-your-app"></a>Eseguire test di penetrazione sull'app
Uno dei tooget modi più semplici hello avviato un test per le vulnerabilità nella tua app di servizio App è hello toouse [integrazione con Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) vulnerabilità di un solo clic tooperform analisi nella tua app. È possibile visualizzare i risultati dei test hello in un report per comprendere e informazioni su come toofix ogni vulnerabilità con istruzioni dettagliate.

Se si preferisce tooperform proprio penetrazione di test o desidera toouse suite scanner altro provider, è necessario seguire hello [Azure penetrazione approvazione](https://security-forms.azure.com/penetration-testing/terms) e ottenere penetrazione hello desiderato di tooperform preventiva approvazione test.

## <a name="https"></a> Garantire la sicurezza delle comunicazioni con i clienti
Se si utilizza hello  **\*. azurewebsites.net** nome di dominio creato per l'applicazione di servizio App, è possibile utilizzare immediatamente HTTPS, viene fornito un certificato SSL per tutti i  **\*. azurewebsites.net** i nomi di dominio. Se il sito utilizza un [nome di dominio personalizzato](app-service-web-tutorial-custom-domain.md), è possibile caricare un certificato SSL troppo[abilitare HTTPS](app-service-web-tutorial-custom-ssl.md) per il dominio personalizzato hello.

Abilitazione [HTTPS](https://en.wikipedia.org/wiki/HTTPS) possono aiutare a proteggere la comunicazione hello tra l'app e gli utenti dagli attacchi MITM.

## <a name="secure-data-tier"></a>Sicurezza del livello dati
Servizio App elevata si integra con il Database SQL, tale che tutte le stringhe di connessione hello vengono crittografate Lavagna hello e vengono decrittografate solo su hello VM app hello viene eseguito sul *e* solo hello quando l'app viene eseguita. Database SQL di Azure include inoltre molte toohelp di funzionalità di sicurezza è proteggere i dati delle applicazioni da eventuali minacce informatici, tra cui [a riposo crittografia](https://msdn.microsoft.com/library/dn948096.aspx), [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx), [ La maschera dati dinamica](../sql-database/sql-database-dynamic-data-masking-get-started.md), e [rilevamento delle minacce](../sql-database/sql-database-threat-detection.md). Se si dispone di dati sensibili o i requisiti di conformità, vedere [la protezione del Database SQL](../sql-database/sql-database-security-overview.md) per ulteriori informazioni su come toosecure i dati.

Se si utilizza un provider di database di terze parti, ad esempio ClearDB, è consigliabile consultare la documentazione del provider di hello direttamente sulle procedure consigliate di sicurezza.  

## <a name="develop"></a> Garantire la sicurezza dello sviluppo e della distribuzione
### <a name="publishing-profiles-and-publish-settings"></a>Profili e impostazioni di pubblicazione
Durante lo sviluppo di applicazioni, eseguire le attività di gestione o l'automazione delle attività tramite utilità come **Visual Studio**, **Web Matrix**, **Azure PowerShell** o hello **Interfaccia della riga di comando di azure (Azure CLI)**, è possibile utilizzare un *le impostazioni di pubblicazione* file o un *profilo di pubblicazione*. Entrambi i tipi di file è l'autenticazione con Azure e devono essere protetto accesso tooprevent non autorizzato.

* Un file di **impostazioni di pubblicazione** contiene
  
  * L'ID sottoscrizione di Azure
  * Un certificato di gestione che consente attività di gestione tooperform per la sottoscrizione *senza un nome account o password tooprovide*.
* Un file **profilo di pubblicazione** contiene
  
  * Informazioni per la pubblicazione di app tooyour

Se si usa un'utilità che utilizza un file di impostazioni di pubblicazione o di un file del profilo di pubblicazione, importare il file di hello contenente impostazioni di pubblicazione hello o nell'utilità di hello del profilo e quindi **eliminare** file hello. Se è necessario mantenere i file hello, tooshare con altri utenti che lavorano su progetto hello, ad esempio, archiviarlo in una posizione sicura, ad esempio un *crittografati* directory con autorizzazioni limitate.

Inoltre, assicurarsi che le credenziali di hello importato sono protette. Ad esempio, **Azure PowerShell** hello e **interfaccia della riga di comando di Azure (Azure CLI)** entrambi archiviare le informazioni importate le **home directory** ( *~*  nei sistemi Linux o OS X e */utenti/nomeutente* nei sistemi Windows.) Per una maggiore sicurezza, è preferibile troppo**crittografare** questi percorsi utilizzando strumenti di crittografia disponibili per il sistema operativo.

### <a name="configuration-settings-and-connection-strings"></a>Impostazioni di configurazione e stringhe di connessione
È comune stringhe di connessione toostore pratica, le credenziali di autenticazione e altre informazioni riservate nel file di configurazione. Purtroppo questi file possono essere esposti nel sito Web o inseriti in un repository pubblico che ne espone le informazioni. Una ricerca semplice in [GitHub](https://github.com), ad esempio, può rivelare numerosi file di configurazione con segreti esposti in repository pubblici hello.

Hello consigliata è tookeep queste informazioni dai file di configurazione dell'applicazione. Servizio App consente di archiviare le informazioni di configurazione come parte dell'ambiente di runtime hello come **impostazioni app** e **le stringhe di connessione**. i valori Hello sono esposti tooyour applicazione in fase di esecuzione tramite *le variabili di ambiente* per la maggior parte dei linguaggi di programmazione. Per le applicazioni .NET questi valori vengono inseriti nella configurazione .NET al runtime. Oltre a queste situazioni, queste impostazioni di configurazione restano crittografate, a meno che non si visualizza o configurarli utilizzando hello [portale Azure](https://portal.azure.com) o utilità, ad esempio PowerShell o hello CLI di Azure. 

L'archiviazione delle informazioni di configurazione nel servizio App rende possibile toolock amministratore dell'applicazione hello verso il basso le informazioni riservate per le applicazioni di produzione hello. Gli sviluppatori possono utilizzare un set separato di impostazioni di configurazione per lo sviluppo di app e impostazioni hello possono essere sostituite automaticamente dalle impostazioni di hello configurate nel servizio App. Gli sviluppatori di hello nemmeno necessitano segreti hello tooknow configurati per l'applicazione di produzione hello. Per altre informazioni sulla configurazione delle impostazioni e delle stringhe di connessione delle app nel servizio app, vedere l'articolo relativo alla [configurazione di app Web](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Servizio App di Azure fornisce protezione FTP accesso toohello file system per l'app tramite **FTPS**. In questo modo è codice dell'applicazione hello accesso toosecurely sul hello web app, nonché diagnostics log. È consigliabile usare sempre FTPS anziché FTP. 

Hello FTPS collegamento per l'app è disponibile con hello alla procedura seguente:

1. Aprire hello [portale Azure](https://portal.azure.com).
2. Selezionare **Esplora tutto**.
3. Da hello **Sfoglia** pannello seleziona **servizi App**.
4. Da hello **servizi App** blade, app desiderata hello selezionare.
5. Pannello hello dell'app, selezionare **tutte le impostazioni**.
6. Da hello **impostazioni** pannello seleziona **proprietà**.
7. Hello FTP e FTPS vengono forniti collegamenti in hello **impostazioni** blade. 

Per altre informazioni su FTPS, vedere [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla sicurezza hello di hello piattaforma Azure, informazioni sulla segnalazione di un **abuso o sicurezza**, o tooinform Microsoft che si intende eseguire **penetrazione** del del sito, vedere la sezione relativa sicurezza hello di hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Per altre informazioni sui file **web.config** o **applicationhost.config** nelle app del servizio app, vedere l'articolo relativo alle [opzioni di configurazione non bloccate nelle app Web del servizio app di Azure](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Per informazioni sulla registrazione di informazioni nelle app del servizio app, che potrebbero essere utili per il rilevamento di attacchi, vedere l'articolo relativo all' [abilitazione della registrazione diagnostica](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

