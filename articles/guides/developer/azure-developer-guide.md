---
title: Guida alla aaaGet introduttiva per sviluppatori in Azure | Documenti Microsoft
description: In questo argomento fornisce informazioni importanti per gli sviluppatori che desiderano tooget all'utilizzo della piattaforma Microsoft Azure hello per le esigenze di sviluppo.
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Guida introduttiva per gli sviluppatori in Azure

## <a name="what-is-azure"></a>Cos'è Azure?

Azure è una piattaforma cloud completa che può ospitare le applicazioni esistenti, semplificare lo sviluppo di hello di nuove applicazioni e anche migliorare le applicazioni locali. Azure consente di integrare servizi cloud hello che è necessario toodevelop, testare, distribuire e gestire le applicazioni, sfruttando l'efficienza di hello del cloud computing.

L'hosting delle applicazioni in Azure consente di iniziare da un'infrastruttura di dimensioni ridotte, ridimensionando l'applicazione con facilità man mano che la richiesta da parte dei clienti aumenta. Azure offre inoltre l'affidabilità di hello è sufficiente per le applicazioni a disponibilità elevata, anche se si include il failover tra aree diverse. Hello [portale di Azure](https://portal.azure.com) consente di gestire facilmente tutti i servizi di Azure. È anche possibile gestire i servizi a livello di codice usando API e modelli specifici del servizio.

**Destinatari questo**: in questa guida è un toohello introduzione della piattaforma Azure per gli sviluppatori di applicazioni. Fornisce informazioni aggiuntive e la direzione che è necessario toostart la creazione di nuove applicazioni in Azure o la migrazione tooAzure di applicazioni esistente.

## <a name="where-do-i-start"></a>Dove iniziare?

Con tutti i servizi di hello che offre Azure, può essere un toofigure attività complessa, i servizi è necessario toosupport dell'architettura della soluzione. Questo hello evidenzia sezione Azure services che è comunemente utilizzati dagli sviluppatori. Per un elenco di tutti i servizi di Azure, vedere hello [documentazione di Azure](../../index.md).

In primo luogo, è necessario decidere come toohost dell'applicazione in Azure. È necessario toomanage dell'intera infrastruttura come una macchina virtuale (VM). È possibile utilizzare funzioni di gestione della piattaforma hello forniti da Azure? Forse è necessario una framework senza toohost esecuzione del codice solo?

L'applicazione ha bisogno di archiviazione cloud, per la quale Azure offre diverse opzioni. È possibile sfruttare i vantaggi dell'autenticazione aziendale di Azure. In Azure sono disponibili anche strumenti per lo sviluppo e il monitoraggio basati sul cloud. La maggior parte dei servizi di hosting, poi, offre l'integrazione DevOps.

A questo punto, ecco alcuni dei servizi specifici hello che è consigliabile per le applicazioni in corso.

### <a name="application-hosting"></a>Hosting di applicazioni

Azure offre diverse toorun offerte di calcolo basate su cloud l'applicazione in modo che non si dispone di tooworry sui dettagli dell'infrastruttura hello. Man mano che l'utilizzo delle risorse da parte delle applicazioni aumenta, è possibile aumentare o scalare orizzontalmente le risorse con facilità.

Azure offre servizi a supporto dello sviluppo di applicazioni e per la soddisfazione di qualsiasi esigenza di hosting, Azure offre infrastructure-as-a-service (IaaS) toogive controllo completo sull'hosting di applicazioni. Offerte di Azure platform-as-a-service (PaaS) forniscono hello completamente gestiti servizi necessari toopower app. È anche true senza server di hosting in Azure è sufficiente toodo in cui scrivere il codice.

![Opzioni di hosting di applicazioni offerte da Azure](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Servizio app di Azure 

Quando si desidera che i progetti Web hello toopublish di percorso più rapido, prendere in considerazione il servizio App di Azure. Servizio App rende facile tooextend il web App toosupport i client mobili e pubblicare le API REST facilmente utilizzabile. Questa piattaforma consente l'autenticazione tramite provider basati su social network, il ridimensionamento automatico in base al traffico, l'esecuzione di test nell'ambiente di produzione e la distribuzione continua e basata sul contenitore.

Quando si crea un'app nel servizio App, selezionare uno dei seguenti tipi di hello:

- [App Web](../../app-service-web/app-service-web-overview.md): consente di ospitare siti e applicazioni Web scritte in .NET, Java, PHP, Node.js e Python.

- [App per dispositivi mobili](../../app-service-mobile/app-service-mobile-value-prop.md): accesso toosupport estende le app Web dai dispositivi mobili. abilita l'autenticazione con i provider basati su social network e Azure Active Directory (Azure AD), consente l'archiviazione back-end e si integra con [Hub di notifica di Azure](../../notification-hubs/notification-hubs-push-notification-overview.md) per le notifiche push.

- [App per le API](../../app-service-api/app-service-api-apps-why-best-platform.md): consente di esporre in modo sicuro le API nel cloud hello con i metadati Swagger in modo che possano essere facilmente utilizzati dal client.

Poiché tutti i tipi di app tre condividono hello runtime del servizio App, è possibile ospitare un sito Web, il supporto dei client per dispositivi mobili ed espongono le API in Azure, tutti gli elementi dal hello stesso progetto o soluzione. toolearn ulteriori informazioni sull'applicazione di servizio, vedere [il funzionamento del servizio App](../../app-service/app-service-how-works-readme.md).

Il servizio app, progettato su misura per DevOps, supporta vari strumenti per la pubblicazione e la distribuzione di integrazione continua, tra cui webhook GitHub, Jenkins, Visual Studio Team Services e TeamCity.

È possibile migrare i tooApp applicazioni esistenti del servizio tramite hello [strumento di migrazione online](https://www.migratetoazure.net/).

>**Quando toouse**: utilizzo del servizio App quando si esegue la migrazione tooAzure di applicazioni web esistenti, e quando è necessario una piattaforma di hosting completamente gestita per le app web. È inoltre possibile utilizzare servizio App quando è necessario client mobili toosupport o espongono le API REST con l'app.

>**Iniziare**: servizio App rende facile toocreate e distribuire il primo [app web](../../app-service-web/web-sites-dotnet-get-started.md), [app per dispositivi mobili](../../app-service-mobile/app-service-mobile-ios-get-started.md), o [app per le API](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Prova adesso**: il servizio App consente di eseguire il provisioning di una piattaforma di breve durata app tootry hello senza toosign a un account Azure. Provare a piattaforma hello e [creare l'applicazione di servizio App di Azure](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Macchine virtuali di Azure

Come provider di infrastructure-as-a-service (IaaS), Azure consente di distribuire tooor di eseguire la migrazione tooeither l'applicazione Windows o le macchine virtuali Linux. Rete virtuale di Azure, insieme a macchine virtuali di Azure supporta la distribuzione di hello di tooAzure VM Windows o Linux. Con le macchine virtuali, si dispone di controllo totale sulla configurazione di hello della macchina hello. Quando si usano VM, l'utente è responsabile di tutte le operazioni di installazione, configurazione e manutenzione del software server, nonché dell'applicazione di patch del sistema operativo.

A causa di livello hello di controllo che presentano con le macchine virtuali, è possibile eseguire un'ampia gamma di carichi di lavoro server in Azure che non rientrano in un modello PaaS. ad esempio server di database, Windows Server Active Directory e Microsoft SharePoint. Per ulteriori informazioni, vedere documentazione di macchine virtuali hello per uno [Linux](/azure/virtual-machines/linux/) o [Windows](/azure/virtual-machines/windows/).

>**Quando toouse**: controllare macchine virtuali di usare quando si desidera che completa l'applicazione dell'infrastruttura o toomigrate locale dell'applicazione i carichi di lavoro tooAzure senza toomake modifiche.

>**Iniziare**: creare un [VM Linux](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) o [macchina virtuale Windows](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) da hello portale di Azure.

#### <a name="azure-functions-serverless"></a>Funzioni di Azure (senza server)

Anziché di doversi preoccupare nello sviluppo e la gestione di un intero toorun di infrastruttura dell'applicazione o hello del codice. Cosa accade se si può solo scrivere il codice e viene eseguito in risposta tooevents o su una pianificazione?  [Funzioni di Azure](../../azure-functions/functions-overview.md) è un "server"-stile offerta che consente di scrivere solo hello codice necessario. Con Funzioni di Azure l'esecuzione del codice viene attivata da richieste HTTP, webhook o eventi del servizio cloud oppure in base a una pianificazione. È possibile scrivere il codice nel linguaggio preferito, ad esempio C\#, F\#, Node.js, Python o PHP. Con la fatturazione in base al consumo, si paga per ora hello che esegue il codice e Azure viene ridimensionata in base alle esigenze.

>**Quando toouse**: utilizzare le funzioni di Azure quando si dispone di codice che viene attivato da altri servizi di Azure, dagli eventi basato sul web o in una pianificazione. È inoltre possibile utilizzare funzioni quando si non necessario hello sovraccarico di un progetto di hosting completo o quando si desidera solo toopay per volta hello che il codice viene eseguito. vedere, più toolearn [panoramica delle funzioni di Azure](../../azure-functions/functions-overview.md).

>**Iniziare**: seguire esercitazione di avvio rapido funzioni hello troppo[creare la prima funzione](../../azure-functions/functions-create-first-azure-function.md) dal portale hello.

>**Prova adesso**: funzioni di Azure consente di eseguire il codice senza toosign a un account Azure. È possibile provare subito a [creare la prima funzione di Azure](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric è una piattaforma di sistemi distribuiti che rende facile toobuild, creare un pacchetto, distribuire e gestire microservizi scalabili e affidabili. Fornisce inoltre una gamma completa di funzionalità di gestione per il provisioning, la distribuzione, il monitoraggio, l'aggiornamento, l'esecuzione di patch e l'eliminazione di applicazioni distribuite. Le app, che vengono eseguite in un pool condiviso di macchine, possono iniziare e scalare toohundreds o migliaia di computer in base alle esigenze.

Service Fabric supporta API Web con Open Web Interface for .NET (OWIN) e ASP.NET Core e mette a disposizione SDK per la compilazione di servizi su Linux in .NET Core e Java. toolearn ulteriori informazioni su Service Fabric, vedere hello [percorso di apprendimento di Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Quando toouse:** Service Fabric è una scelta ottimale quando si crea un'applicazione o un toouse applicazione esistente, un'architettura microservizio di riscrittura. Quando è necessario più preciso, o accesso diretto alla, infrastruttura sottostante hello, utilizzare Service Fabric.

>**Come iniziare:** [creare la prima applicazione Azure Service Fabric](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Migliorare le applicazioni con i servizi di Azure

Tooapplication hosting, Azure fornisce inoltre le offerte di servizio che possono migliorare la funzionalità di hello, lo sviluppo e manutenzione delle applicazioni, sia nel cloud hello e locali.

#### <a name="hosted-storage-and-data-access"></a>Archiviazione ospitata e accesso ai dati

La maggior parte delle applicazioni deve archiviare i dati, indipendentemente dal come si decide di toohost l'applicazione in Azure, prendere in considerazione uno o più dei seguenti servizi di archiviazione e i dati hello.

-   **Database SQL di Azure**: basato su Azure una versione del motore di Microsoft SQL Server di hello per l'archiviazione dei dati tabulari relazionali nel cloud hello. Il database SQL offre prestazioni prevedibili, scalabilità senza tempi di inattività, continuità aziendale e protezione dei dati.

    >**Quando toouse**: quando l'applicazione richiede l'archiviazione dei dati con l'integrità referenziale, il supporto delle transazioni e il supporto per le query TSQL.

    >**Iniziare**: [creare un database SQL in minuti, tramite il portale di Azure hello](../../sql-database/sql-database-get-started.md).

-   **Archiviazione di Azure**: offre risorse di archiviazione durevoli e a disponibilità elevata per BLOB, code, file e altri tipi di dati non relazionali. Archiviazione fornisce foundation archiviazione hello per le macchine virtuali.

    >**Quando toouse**: quando l'applicazione archivia i dati non relazionali, ad esempio di coppie chiave-valore (tabelle), BLOB, condivisioni di file o messaggi (Code).

    >**Come iniziare**: scegliere uno dei tipi di archiviazione seguenti: [BLOB](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tabelle](../../cosmos-db/table-storage-how-to-use-dotnet.md), [code](../../storage/queues/storage-dotnet-how-to-use-queues.md) o [file](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB**: servizio di database NoSQL completamente gestito e scalabile con funzioni di query SQL sui dati di oggetto. È possibile accedere a DocumentDB tramite i driver di MongoDB esistenti.
    >**Quando toouse:** quando l'applicazione necessita di query SQL in grado di tooexecute toobe su documenti JSON, o se si usa MongoDB.

    >**Come iniziare**: [creare un'applicazione console DocumentDB in C#](../../documentdb/documentdb-get-started.md). Per gli sviluppatori MongoDB è consigliabile vedere [Supporto del protocollo di DocumentDB per MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

È possibile utilizzare [Data Factory di Azure](../../data-factory/data-factory-introduction.md) toomove locali esistenti tooAzure di dati. Se non si è pronti toomove toohello dati nel cloud, [connessioni ibride](../../biztalk-services/integration-hybrid-connection-overview.md) in consente di servizi BizTalk di connettersi al servizio App ospitato risorse tooon locale dell'app. È inoltre possibile connettere i servizi di archiviazione e dei dati tooAzure dalle applicazioni locali.

#### <a name="docker-support"></a>Supporto di Docker

I contenitori Docker, un tipo di virtualizzazione del sistema operativo, consente di distribuire le applicazioni in modo più efficiente e prevedibile. Un'applicazione nei contenitori funziona in hello produzione stesso modo per i sistemi di sviluppo e test. È possibile gestire i contenitori tramite gli strumenti di Docker standard. È possibile utilizzare le competenze esistenti e toodeploy strumenti open source più diffusi e gestire applicazioni basate sul contenitore in Azure.

Azure offre diversi modi contenitori toouse nelle applicazioni.

-   **L'estensione Docker VM Azure**: consente di configurare la macchina virtuale con Docker strumenti tooact come un host Docker.

    >**Quando toouse**: quando si desidera che le distribuzioni di toogenerate contenitore coerente per le applicazioni in una macchina virtuale, oppure quando si desidera toouse [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Iniziare**: [creare un ambiente di Docker in Azure utilizzando l'estensione della macchina virtuale Docker hello](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Il servizio contenitore Azure**: consente di creare, configurare e gestire un cluster di macchine virtuali che sono preconfigurati applicazioni toorun contenitore. toolearn ulteriori informazioni su servizio di contenitore, vedere [introduzione servizio contenitore di Azure](../../container-service/container-service-intro.md).

    >**Quando toouse**: quando è necessario toobuild ambiente di produzione, scalabile ambienti che forniscono gli strumenti di pianificazione e gestione aggiuntivi o quando si distribuisce un cluster di Docker Swarm.

    >**Come iniziare**: [distribuire un cluster di contenitori Docker](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker Machine**: consente di installare e gestire Docker Engine in host virtuali tramite comandi di Docker Machine.

    >**Quando toouse**: quando è necessario tooquickly prototipo di un'app mediante la creazione di un singolo host Docker.

-   **Immagine Docker personalizzata per il servizio app**: consente di distribuire un'app Web in Linux usando contenitori Docker di un registro contenitori o il contenitore di un cliente.

    >**Quando toouse**: quando si distribuisce un'app web sull'immagine di Docker tooa Linux.

    >**Come iniziare**: [usare un'immagine Docker personalizzata per il servizio app in Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Autenticazione

È fondamentale toonot solo conoscere chi sta utilizzando le applicazioni, ma anche accedere alle risorse di tooyour tooprevent non autorizzato. Azure offre diversi modi tooauthenticate i client di app.

-   **Azure Active Directory (Azure AD)**: hello multi-tenant cloud basato su identità e accessi servizio di gestione Microsoft. Grazie all'integrazione con Azure AD, è possibile aggiungere single sign-in applicazioni tooyour (SSO). Le proprietà della directory è possibile accedere tramite hello Azure AD Graph API direttamente o hello Microsoft Graph API. È possibile integrare con supporto di Azure AD per framework di autorizzazione OAuth 2.0 hello e aprire ID connettersi tramite endpoint HTTP/REST native e hello librerie di autenticazione multipiattaforma di Azure AD.

    >**Quando toouse**: quando si desidera che il servizio SSO tooprovide, lavorare con i dati basati su grafico o autenticare gli utenti basati su dominio.

    >**Iniziare**: toolearn informazioni, vedere hello [Guida per gli sviluppatori di Azure Active Directory](../../active-directory/active-directory-developers-guide.md).

-   **L'autenticazione del servizio app**: quando si sceglie di servizio App toohost l'app, viene visualizzato anche il supporto di autenticazione predefinito per Azure AD, insieme ai provider di identità di social networking, inclusi Facebook, Google, Microsoft e Twitter.

    >**Quando toouse**: quando si desidera eseguire l'autenticazione tooenable in un'applicazione di servizio App usando Azure AD, i provider di identità di social networking, o entrambi.

    >**Iniziare**: toolearn ulteriori informazioni sull'autenticazione nel servizio App, vedere [autenticazione e autorizzazione in Azure App Service](../../app-service/app-service-authentication-overview.md).

toolearn sulle procedure ottimali di protezione in Azure, vedere [le procedure consigliate di sicurezza di Azure e i pattern](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Monitoraggio

Con l'applicazione di backup e in esecuzione in Azure, è necessario toobe toomonitor in grado di prestazioni, controllare i problemi e vedere come i clienti stiano usando l'app. Azure offre diverse opzioni di monitoraggio.

-   **Visual Studio Application Insights**: il servizio ospitato da Azure un analitica estendibile che si integra con Visual Studio toomonitor le applicazioni web in tempo reale. Fornisce dati hello necessari toocontinuously migliorare le prestazioni di hello e usabilità delle applicazioni, se sono ospitati in Azure o non.

    >**Iniziare**: hello seguire [esercitazione Application Insights](../../application-insights/app-insights-overview.md).

-   **Monitoraggio Azure**: un servizio che consente di toovisualize, query, route, archiviazione e agiscono su metriche hello e i log generati dall'infrastruttura di Azure e risorse. Monitoraggio sono disponibili le visualizzazioni dati hello di vedere nel portale di Azure hello ed è un'unica origine per il monitoraggio delle risorse di Azure.
 
    >**Come iniziare**: [Introduzione al monitoraggio di Azure](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Integrazione di strumenti DevOps

Se è il provisioning di macchine virtuali o pubblicare App web con l'integrazione continua, Azure si integra con la maggior parte degli strumenti DevOps diffusi hello. Con supporto per strumenti come Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, Visual Studio Team Services e altri utenti, per lavorare con gli strumenti di hello è già configurato e ottimizzare l'esperienza esistente.

>**Prova adesso:** [provare diversi di integrazioni DevOps hello](https://azure.microsoft.com/try/devops/).

>**Iniziare**: toosee DevOps opzioni per un'applicazione di servizio App, vedere [tooAzure distribuzione continua servizio App](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Aree di Azure

Azure è una piattaforma cloud globali che è in genere disponibile in numerose aree geografiche in tutto HelloWorld. Quando si esegue il provisioning di un servizio, applicazione o macchina virtuale in Azure, sono frequenti tooselect un'area, che rappresenta un Data Center specifico in cui viene eseguita l'applicazione o in cui sono memorizzati i dati. Tali aree corrispondono a posizioni toospecific, che vengono pubblicati su hello [aree di Azure](https://azure.microsoft.com/regions/) pagina.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Scegliere hello area migliore per l'applicazione e dati

Uno dei vantaggi di hello dell'utilizzo di Azure è possibile distribuire i Data Center toovarious applicazioni mondo hello. Nell'area Hello scelta in termini di prestazioni hello dell'applicazione. Ad esempio, è meglio toochoose un'area più vicino toomost la latenza di tooreduce clienti nelle richieste di rete. È inoltre possibile tooselect i requisiti legali di hello toomeet area per la distribuzione dell'app in determinati paesi. È sempre un migliori dati dell'applicazione toostore pratica hello stesso Data Center o in un datacenter il più vicino come Data Center toohello possibili che ospita l'applicazione.

### <a name="multi-region-apps"></a>App con più aree

Anche se improbabile, non è possibile per un toogo intero Data Center offline a causa di un evento, ad esempio un errore di Internet o di calamità naturali. Le applicazioni aziendali di vitale importanza una migliore pratica toohost in più Data Center tooprovide la massima disponibilità è. L'uso di più aree può anche ridurre la latenza per gli utenti globali e offrire altre opportunità per una maggiore flessibilità durante l'aggiornamento delle applicazioni.

Alcuni servizi, ad esempio macchine virtuali e servizi di App, utilizzano [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) supporto multiarea tooenable con il failover tra le applicazioni di aree toosupport enterprise a disponibilità elevata. Per un esempio, vedere [Azure reference architecture: Web application with high availability](../../guidance/guidance-web-apps-multi-region.md) (Architettura di riferimento per Azure: applicazione Web a disponibilità elevata).

>**Quando toouse**: quando si dispone di applicazioni aziendali e a disponibilità elevata che traggono vantaggio dalla replica e failover.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Come gestire le applicazioni e i progetti

Azure offre un'ampia gamma di esperienze di toocreate e gestire le risorse di Azure, applicazioni e i progetti, sia a livello di codice e hello [portale di Azure](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Interfacce della riga di comando e PowerShell

Le applicazioni e servizi dalla riga di comando hello Azure offre due modi toomanage utilizzando Bash, Terminal, il prompt dei comandi di hello o lo strumento da riga di comando di scelta. In genere, è possibile eseguire hello stessa attività dalla riga di comando hello come hello portale di Azure, ad esempio la creazione e configurazione di macchine virtuali, reti virtuali, le applicazioni web e altri servizi.

-   [Azure interfaccia della riga di comando (CLI)](../../xplat-cli-install.md): consente di connettersi tooan sottoscrizione di Azure e varie attività con risorse di Azure dalla riga di comando hello del programma.

-   [Azure PowerShell](../../powershell-install-configure.md): fornisce un set di moduli con i cmdlet che consentono di toomanage Azure le risorse tramite Windows PowerShell.

### <a name="azure-portal"></a>Portale di Azure

Hello portale di Azure è un'applicazione basata su web che è possibile utilizzare toocreate, gestire e rimuovere servizi e risorse di Azure. Hello portale di Azure si trova in <https://portal.azure.com>. Include un dashboard personalizzabile, strumenti per la gestione delle risorse di Azure e le impostazioni di accesso toosubscription e informazioni di fatturazione. Per ulteriori informazioni, vedere hello [portale di Azure-Panoramica](../../azure-portal-overview.md).

### <a name="rest-apis"></a>API REST

Si basa su un set di API REST che supportano l'interfaccia utente del portale Azure hello. La maggior parte di queste API REST sono inoltre supportati toolet a livello di codice il provisioning e gestire le risorse di Azure e le applicazioni da qualsiasi dispositivo abilitate per Internet. Per hello intero set di documentazione dell'API REST, vedere hello [riferimento SDK REST Azure](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>API

Inoltre tooREST API, molti servizi di Azure anche consentono di gestire a livello di codice le risorse dalle applicazioni tramite specifico della piattaforma Azure SDK, incluso il SDK per hello seguenti piattaforme di sviluppo:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.JS](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Servizi, ad esempio [App per dispositivi mobili](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) e [servizi multimediali di Azure](../../media-services/media-services-dotnet-how-to-use.md) fornire sul lato client SDK toolet si accede ai servizi web e applicazioni client mobili.

### <a name="azure-resource-manager"></a>Gestione risorse di Azure 
    
Esegue l'app in Azure probabile implica l'utilizzo con più servizi di Azure, tutti di quali seguire hello stessa durata del ciclo e può essere considerato come un'unità logica. Ad esempio, un'app Web può usare i servizi app Web, database SQL, Archiviazione, Cache Redis di Azure e Rete di distribuzione dei contenuti di Microsoft Azure. [Gestione risorse di Azure](../../azure-resource-manager/resource-group-overview.md) consente di utilizzare le risorse di hello dell'applicazione come un gruppo. È possibile distribuire, aggiornare o eliminare tutte le risorse di hello in un'operazione singola, coordinata.

Inoltre i toologically raggruppare e gestire risorse correlate, Gestione risorse di Azure include funzionalità di distribuzione che consentono di personalizzare hello distribuzione e configurazione delle risorse correlate. Usando Resource Manager, ad esempio, è possibile distribuire e configurare un'applicazione costituita da più macchine virtuali, da un sistema di bilanciamento del carico e da un database SQL di Azure come unità singola.

Per sviluppare questo tipo di distribuzioni si usa un modello di Azure Resource Manager, che è un documento in formato JSON. I modelli consentono di definire la distribuzione e di gestire le applicazioni tramite modelli dichiarativi, anziché tramite script. I modelli possono funzionare in ambienti diversi, ad esempio negli ambienti di test, staging e produzione. Ad esempio, tramite i modelli, è possibile aggiungere un repository di GitHub tooa pulsante che consente di distribuire il codice hello nel set di tooa hello repository di servizi di Azure con un solo clic.

>**Quando toouse**: usare Gestione risorse modelli quando si desidera una distribuzione basata sul modello per l'app che è possibile gestire a livello di programmazione tramite le API REST, hello CLI di Azure e Azure PowerShell.

>**Iniziare**: tooget avviato utilizzando i modelli, vedere [modelli Authoring Azure Resource Manager](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Informazioni sugli account, sulle sottoscrizioni e sulla fatturazione

Gli sviluppatori, è come toodive direttamente nel codice hello e provare tooget più velocemente possibile rendere le applicazioni di eseguire l'avvio. Si desidera certamente tooencourage toostart Usa la stessa facilità con possibili Azure. toohelp rendono semplice, Azure offre un [versione di valutazione gratuita](https://azure.microsoft.com/free/). Alcuni servizi hanno anche una funzionalità "Provalo gratuitamente", ad esempio [Azure App Service](https://tryappservice.azure.com/), che non richiede troppo anche creare un account. Come fun perché è toodive in codifica e la distribuzione tooAzure l'applicazione, è inoltre importante tootake alcuni toounderstand ora il funzionamento di Azure da un punto di vista dell'account utente, le sottoscrizioni e fatturazione.

### <a name="what-is-an-azure-account"></a>Che cos'è un account di Azure?

toocreate in grado di toobe o lavoro con una sottoscrizione di Azure, è necessario disporre di un account di Azure. Un account di Azure è semplicemente un'identità in Azure AD o in una directory, ad esempio in un'organizzazione aziendale o in un istituto di istruzione, considerata attendibile da Azure AD. Se non si è membri toosuch un'organizzazione, è sempre possibile creare una sottoscrizione usando l'Account Microsoft, che è considerato attendibile da Azure AD. toolearn più sull'integrazione locale Windows Server Active Directory con Azure AD, vedere [integrazione delle identità locali con Azure Active Directory](../../active-directory/active-directory-aadconnect.md).

Ogni sottoscrizione di Azure ha una relazione di trust con un'istanza di Azure AD. Ciò significa che tale tooauthenticate directory considera attendibili gli utenti, servizi e dispositivi. Più sottoscrizioni possono considerare attendibile hello stessa directory, ma una sottoscrizione considera attendibile solo una directory. vedere, più toolearn [delle sottoscrizioni Azure sono associate con Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Inoltre le identità di singoli account Azure toodefining, chiamato anche *utenti*, è inoltre possibile definire *gruppi* in Azure AD. Creazione di gruppi di utenti è un tooresources di accesso toomanage efficace in una sottoscrizione tramite il controllo di accesso basato sui ruoli (RBAC). toolearn toocreate gruppi, vedere [creare un gruppo in anteprima di Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md). È possibile creare e gestire gruppi anche [tramite PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Gestire le sottoscrizioni

Una sottoscrizione è un'unità logica di servizi di Azure che è collegato tooan account Azure. In una sottoscrizione ogni account associato ha un ruolo. La fatturazione per i servizi di Azure si basa sulla sottoscrizione. Per un elenco di offerte di sottoscrizione disponibili hello dal tipo, vedere [dettagli dell'offerta Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Ruoli di amministratore

In una sottoscrizione di Azure sono disponibili più ruoli di amministratore account, che è possibile assegnare in qualsiasi momento.

-   **Account amministratore**: questo ruolo dispone del controllo completo sulla sottoscrizione hello e account hello che è responsabile per la fatturazione.

-   **Amministratore del servizio**: questo ruolo dispone di controllo su tutti i servizi di hello nella sottoscrizione hello. Per impostazione predefinita, questo è hello stesso account come amministratore dell'Account di hello.

-   **CO-amministratore**: questo ruolo dispone di hello stesso accedere come amministratore del servizio, hello ad eccezione del fatto che non può modificare l'associazione di hello di hello sottoscrizione tooan directory Azure.

toolearn ulteriori informazioni sui ruoli di amministratore, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Gruppi di risorse

Quando si esegue il provisioning di nuovi servizi di Azure, questa operazione viene eseguita nell'ambito di una sottoscrizione specifica. Singoli servizi di Azure, sono detti anche le risorse, vengono creati nel contesto di hello di un gruppo di risorse. Gruppi di risorse, rendono più semplice toodeploy e gestire le risorse dell'applicazione. Un gruppo di risorse deve contenere tutte le risorse di hello per l'applicazione che si desidera toowork con come unità. È possibile spostare le risorse tra gruppi di risorse e anche toodifferent sottoscrizioni. toolearn sullo spostamento di risorse, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../../resource-group-move-resources.md).

Hello Esplora inventario risorse di Azure è un ottimo strumento per la visualizzazione di risorse hello che è già stato creato nella sottoscrizione. vedere, più toolearn [tooview utilizzare Esplora risorse di Azure e modificare le risorse](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Concedere accesso tooresources

Quando si consentono l'accesso alle risorse tooAzure è sempre consigliabile fornire agli utenti con hello privilegi minimi tooperform necessario che un'attività specifica.

-   **Controllo di accesso basato sui ruoli (RBAC)**: In Azure, è possibile concedere l'accesso degli account toouser (entità) per un ambito specificato: sottoscrizione, gruppo di risorse o le singole risorse. RBAC consente di distribuire un set di risorse in un gruppo di risorse e concedere le autorizzazioni tooa utente o gruppo specifico. Inoltre consentono di limitare l'accesso tooonly hello risorse appartenenti al gruppo di risorse di destinazione toohello. È inoltre possibile concedere accesso tooa singola risorsa, ad esempio una macchina virtuale o di una rete virtuale. accesso toogrant, assegnare un utente toohello ruolo, gruppo o entità servizio. Sono disponibili molti ruoli predefiniti ed è anche possibile definire ruoli personalizzati.

    >**Quando toouse**: quando è necessario gestione accessi con granularità fine per utenti e gruppi.

    >**Iniziare**: toolearn informazioni, vedere [Introduzione alla gestione di accesso nel portale di Azure hello](../../active-directory/role-based-access-control-what-is.md).

-   **Gli oggetti dell'entità servizio**: inoltre tooproviding accedere toouser entità e gruppi, è possibile concedere hello stessa entità di servizio di accesso tooa.

    > **Quando toouse**: quando si è a livello di codice la gestione delle risorse di Azure o la concessione dell'accesso per le applicazioni. Per altre informazioni, vedere [Creare un'applicazione e un'entità servizio di Azure Active Directory](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Tag

Gestione risorse di Azure consente di assegnare tag personalizzati tooindividual risorse. Tag, che sono coppie chiave-valore, può essere utile quando è necessario tooorganize risorse per la fatturazione o di monitoraggio. Tag forniscono una risorse tootrack modo tra più gruppi di risorse. È possibile assegnare i tag nel portale di hello, nel modello di gestione risorse di Azure hello o a livello di programmazione utilizzando hello API REST, hello CLI di Azure o PowerShell. È possibile assegnare più tag risorsa tooeach. vedere, più toolearn [tramite tag tooorganize le risorse di Azure](../../resource-group-using-tags.md).

### <a name="billing"></a>Fatturazione

In hello spostamento dal calcolo i servizi ospitati toocloud on-premise, rilevamento e la stima dei costi correlati e utilizzo del servizio sono problemi significativi. È importante toobe in grado di tooestimate le nuove risorse toorun su base mensile dei costi. È inoltre necessario tooproject in grado di toobe aspetto di fatturazione hello per un determinato mese sulla base delle spese corrente hello.

#### <a name="get-resource-usage-data"></a>Ottenere dati sull'utilizzo delle risorse

Azure offre un set di API REST di fatturazione che forniscono accesso tooresource consumo e informazioni sui metadati per le sottoscrizioni di Azure. Questi consentono di API di fatturazione hello toobetter possibilità prevedere e gestire i costi di Azure. È possibile tenere traccia della spesa e analizzarla in incrementi di un'ora, creare avvisi relativi alla spesa e stimare la fatturazione futura in base alle tendenze di utilizzo correnti.

>**Iniziare**: toolearn ulteriori informazioni sull'utilizzo di hello le API di fatturazione, vedere [panoramica dell'utilizzo di fatturazione di Azure e RateCard APIs](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Stimare i costi futuri

Anche se è difficile costi tooestimate anticipatamente, Azure offre un [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/) che è possibile utilizzare per la stima dei costi di hello di distribuzione di risorse. È inoltre possibile utilizzare pannello fatturazione hello in portale hello e hello fatturazione API REST tooestimate costi futuri, in base al consumo corrente.

>**Come iniziare**: vedere [Panoramica delle API di utilizzo della fatturazione e delle API RateCard di Azure](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Impostare avvisi di fatturazione per le sottoscrizioni Microsoft Azure

Dopo aver distribuito l'applicazione o una soluzione in Azure, è possibile creare avvisi per l'invio di posta elettronica quando si tenta di hello i limiti definiti nell'avviso di hello di spesa.

>**Iniziare**: toolearn informazioni, vedere [configurare la fatturazione degli avvisi per le sottoscrizioni di Microsoft Azure](../../billing-set-up-alerts.md).
