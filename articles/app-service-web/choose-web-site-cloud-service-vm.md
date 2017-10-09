---
title: confronto di servizio App, macchine virtuali, Service Fabric e servizi Cloud aaaAzure | Documenti Microsoft
description: Informazioni su come toochoose tra servizio App di Azure, le macchine virtuali, Service Fabric e servizi Cloud per l'hosting di applicazioni web.
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Confronto tra Servizio app di Azure, Macchine virtuali, Service Fabric e Servizi cloud
## <a name="overview"></a>Panoramica
Azure offre diversi modi di siti web toohost: [Azure App Service][Azure App Service], [macchine virtuali][Virtual Machines], [Service Fabric ] [ Service Fabric], e [servizi Cloud][Cloud Services]. In questo articolo consente di comprendere le opzioni di hello e rendere hello adatta all'applicazione web.

Servizio App di Azure sia hello migliore per la maggior parte delle applicazioni web. Gestione e distribuzione sono integrati nella piattaforma hello, siti possono scalare rapidamente i carichi di traffico elevato toohandle e gestione di traffico e di bilanciamento del carico incorporati hello garantire un'elevata disponibilità. È possibile spostare tooAzure servizio App di esistenti dei siti con facilità un [strumento di migrazione online](https://www.migratetoazure.net/), utilizzare un'altra applicazione da hello raccolta applicazioni Web open source o creare un nuovo sito usando il framework di hello e gli strumenti di propria scelta. Hello [processi Web] [ WebJobs] funzionalità rende facile tooadd background processo elaborazione tooyour App del servizio web app.

Service Fabric è una buona scelta se si sta creando una nuova app o riscrivere un'app esistente toouse un'architettura microservizio. Le app, che vengono eseguite in un pool condiviso di macchine, è possono avviare piccole e aumento delle dimensioni di scala toomassive con centinaia o migliaia di computer in base alle esigenze. Servizi con stati rendono tooconsistently semplice e affidabile archiviano lo stato dell'app e Service Fabric gestisce automaticamente il partizionamento del servizio, scalabilità e disponibilità per l'utente.  Service Fabric supporta anche WebAPI con Open Web Interface for .NET (OWIN) e ASP.NET Core.  TooApp confrontati servizio, Service Fabric fornisce più controllo sulla o accesso diretto alla, infrastruttura sottostante hello. È possibile accedere in remoto ai server e configurarne le attività di avvio. Servizi cloud simili tooService infrastruttura in grado di controllo e semplicità di utilizzo, ma ora è un servizio legacy e Service Fabric è consigliato per nuove attività di sviluppo.

Se si dispone di un'applicazione esistente che richiederebbe toorun modifiche sostanziali nel servizio App o dall'infrastruttura di servizio, è possibile scegliere le macchine virtuali nella migrazione cloud toohello toosimplify di ordine. Tuttavia, correttamente la configurazione, protezione e gestione di macchine virtuali richiede molto tempo e competenze IT confrontato tooAzure servizio App e Service Fabric. Se si prevede di macchine virtuali di Azure, accertarsi di eseguire in account hello manutenzione sforzo necessario toopatch, aggiornare e gestire l'ambiente di VM. Macchine virtuali di Azure è un'infrastruttura distribuita come servizio (IaaS, Infrastructure-as-a-Service), mentre il servizio app e Service Fabric sono piattaforme distribuite come servizio (PaaS, Platform-as-a-Service). 

## <a name="features"></a>Confronto delle funzionalità
Servizi Cloud, macchine virtuali e Service Fabric toohelp apportate migliore hello Hello nella tabella seguente vengono confrontate le funzionalità di hello del servizio App. Per informazioni aggiornate sulla hello contratto di servizio per ogni opzione, vedere [contratti di servizio di Azure](https://azure.microsoft.com/support/legal/sla/).

| Funzionalità | Servizio app (app Web) | Servizi cloud (ruoli Web) | Macchine virtuali | Service Fabric | Note |
| --- | --- | --- | --- | --- | --- |
| Distribuzione quasi istantanea |X | | |X |Distribuire un'applicazione o un tooa aggiornamento applicazione del servizio Cloud o la creazione di una macchina virtuale, potrebbe impiegare diversi minuti almeno; distribuzione di un'app web di applicazione tooa richiedono pochi secondi. |
| Applicare la scalabilità verticale macchine toolarger senza ridistribuzione |X | | |X | |
| Istanze del server Web di condividere il contenuto e la configurazione, che significa che non hanno tooredeploy o riconfigurare quando si scala. |X | | |X | |
| Più ambienti di distribuzione (produzione e gestione temporanea) |X |X | |X |Service Fabric consente toohave più ambienti per App o toodeploy diverse versioni dell'app side-by-side. |
| Gestione automatica dell'aggiornamento del sistema operativo |X |X | | |Sono previsti aggiornamenti automatici del sistema operativo per una versione futura di Service Fabric. |
| Commutazione di piattaforma trasparente (è possibile passare facilmente tra 32 bit e 64 bit) |X |X | | | |
| Distribuzione codice con GIT, FTP |X | |X | | |
| Distribuzione codice con distribuzione Web |X | |X | |Servizi cloud supporta utilizzare hello distribuzione Web toodeploy aggiornamenti tooindividual di istanze del ruolo. Tuttavia, non può essere utilizzato per la distribuzione iniziale di un ruolo, mentre se si utilizza distribuzione Web per un aggiornamento separatamente necessario toodeploy tooeach istanza di un ruolo. In ordine tooqualify per hello contratto di servizio Cloud per ambienti di produzione sono necessari più istanze. |
| Supporto WebMatrix |X | |X | | |
| Accesso tooservices Bus di servizio, archiviazione, Database SQL |X |X |X |X | |
| Hosting del livello Web o dei servizi Web di un'architettura multilivello |X |X |X |X | |
| Hosting del livello intermedio di un'architettura multilivello |X |X |X |X |App del servizio web App facilmente possibile ospitare un livello intermedio di API REST e hello [processi Web](http://go.microsoft.com/fwlink/?linkid=390226) funzionalità può ospitare i processi di elaborazione in background. È possibile eseguire i processi Web in una sito Web dedicato tooachieve indipendente una scalabilità per il livello di hello. Anteprima Hello [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md) funzionalità offre anche altre funzionalità per ospitare i servizi REST. |
| Supporto integrato di MySQL distribuito come servizio |X |X |X | |Servizi cloud è possono integrare MySQL come servizio tramite offerte di ClearDB, ma non come parte del flusso di lavoro di hello portale di Azure. |
| Supporto per ASP.NET, ASP classico, Node.js, PHP, Python |X |X |X |X |Service Fabric supporta la creazione di hello di una web front-end tramite [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) o è possibile distribuire qualsiasi tipo di applicazione (Node.js, Java e così via) come un [eseguibile guest](../service-fabric/service-fabric-deploy-existing-app.md). |
| Scalabilità orizzontale toomultiple istanze senza ridistribuzione |X |X |X |X |Macchine virtuali è possibile scalare orizzontalmente toomultiple istanze, ma i servizi di hello in esecuzione su di essi devono essere scritto toohandle questo scalabilità orizzontale. Avere tooconfigure un tooroute delle richieste di servizio di bilanciamento carico tra più computer hello e creare un gruppo di affinità di tooprevent simultanei riavvii di tutte le istanze a causa di errori hardware o toomaintenance. |
| Supporto per SSL |X |X |X |X |Per App Web del servizio app, SSL per i nomi di dominio personalizzati è supportato solo nella modalità Basic e Standard. Per informazioni sull'uso di SSL con app Web, vedere [Configurazione di un certificato SSL per un sito Web di Azure](app-service-web-tutorial-custom-ssl.md). |
| Integrazione di Visual Studio |X |X |X |X | |
| Debug remoto |X |X |X | | |
| Distribuzione codice con TFS |X |X |X |X | |
| Isolamento rete con la [rete virtuale di Azure](/azure/virtual-network/) |X |X |X |X |Vedere anche [Integrazione della rete virtuale di Siti Web di Azure](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Supporto per [Gestione traffico di Azure](/azure/traffic-manager/) |X |X |X |X | |
| Monitoraggio integrato degli endpoint |X |X |X | | |
| Tooservers accesso desktop remoto | |X |X |X | |
| Installazione di qualsiasi MSI personalizzato | |X |X |X |Service Fabric consente toohost qualsiasi file eseguibile file come un [eseguibile guest](../service-fabric/service-fabric-deploy-existing-app.md) o è possibile installare qualsiasi applicazione in hello macchine virtuali. |
| Attività di avvio/esecuzione toodefine possibilità | |X |X |X | |
| Può restare in ascolto degli eventi tooETW | |X |X |X | |

## <a name="scenarios"></a>Scenari e indicazioni
Ecco alcuni scenari comuni di applicazione con le raccomandazioni come opzione di hosting web di Azure toowhich potrebbe essere più appropriata per ognuno.

* [È necessario un front-end web con l'elaborazione in background e applicazioni di database back-end toorun business integrate con risorse locali.](#onprem)
* [È necessario un toohost affidabile raggiungere il sito Web aziendale che viene ridimensionata anche e offerte globale.](#corp)
* [Ho un'applicazione IIS6 in esecuzione su Windows Server 2003.](#iis6)
* [Sto piccole aziende ed è necessario un toohost conveniente sito personale, ma con la crescita futura presente.](#smallbusiness)
* [Sono un web o un progettista grafico e si desidera toodesign e compilare siti web per i propri clienti.](#designer)
* [In corso la migrazione dell'applicazione multilivello con un toohello front-end web Cloud.](#multitier)
* [L'applicazione dipende da Windows altamente personalizzati o ambienti Linux e si desidera toomove è toohello cloud.](#custom)
* [Il sito utilizza software open source e si desidera toohost in Azure.](#oss)
* [Dispone di un'applicazione line-of-business che deve tooconnect toohello alla rete aziendale.](#lob)
* [Si desidera toohost un'API REST o il servizio web per client mobili.](#mobile)

### <a id="onprem"></a>È necessario un front-end web con l'elaborazione in background e applicazioni di database back-end toorun business integrate con risorse locali.
Azure App Service è un'ottima soluzione per applicazioni aziendali complesse. Consente di sviluppare applicazioni che ridimensionare automaticamente su una piattaforma con bilanciamento del carico, sono protetti con Active Directory e connettono le risorse locali tooyour. Facilita la gestione di tali App semplice tramite un portale di altissimo livello e le API e consentono di comprendere come i clienti vengano utilizzati con gli strumenti insight app toogain. Hello [processi Web] [ Webjobs] funzionalità consente di eseguire i processi in background e le risorse locali tooon indietro di facile tooconnect renderlo attività come parte del livello web, mentre la connettività ibrida e le funzionalità di rete virtuale. Azure App Service offre contratti di servizio con garanzia di disponibilità del 99,999% per le app Web e consente di:

* Eseguire le applicazioni in modo affidabile su una piattaforma cloud con funzionalità automatiche di riparazione e di applicazione di patch.
* Scalare automaticamente in una rete globale di data center.
* Eseguire il backup e il ripristino per il ripristino di emergenza.
* Essere conformi a ISO, SOC2 e PCI.
* Effettuare l'integrazione con Active Directory.

### <a id="corp"></a>È necessario un toohost affidabile raggiungere il sito Web aziendale che viene ridimensionata anche e offerte globale.
Azure App Service è un'ottima soluzione per l'hosting di siti Web aziendali. Consente tooscale App web rapidamente e facilmente toomeet richiedono una rete globale dei centri dati. Offre portata locale, tolleranza di errore e gestione intelligente del traffico, Tutto su una piattaforma che fornisce gli strumenti di gestione di livello mondiale, consentono di toogain approfondite integrità del sito e il traffico del sito in modo semplice e rapido. Azure App Service offre contratti di servizio con garanzia di disponibilità del 99,999% per le app Web e consente di:

* Eseguire i siti Web in modo affidabile su una piattaforma cloud con funzionalità automatiche di riparazione e di applicazione di patch.
* Scalare automaticamente in una rete globale di data center.
* Eseguire il backup e il ripristino per il ripristino di emergenza.
* Gestire i log e il traffico con strumenti integrati.
* Essere conformi a ISO, SOC2 e PCI.
* Effettuare l'integrazione con Active Directory.

### <a id="iis6"></a> Ho un'applicazione IIS6 in esecuzione su Windows Server 2003.
Servizio App di Azure rende facile tooavoid hello costi di infrastruttura associati alla migrazione di applicazioni IIS 6 precedente. Microsoft ha creato [strumenti di migrazione semplice toouse e al materiale sussidiario di migrazione dettagliato](https://www.movemetowebsites.net/) che consentono di compatibilità toocheck e identificare le modifiche necessarie toobe apportate. Integrazione con Visual Studio e TFS strumenti comuni di CMS rende facile toodeploy IIS6 applicazioni direttamente toohello cloud. Una volta distribuito, hello portale di Azure fornisce gli strumenti di gestione affidabile che consentono di tooscale i costi toomanage e toomeet richiesta in base alle esigenze. Con lo strumento di migrazione hello è possibile:

* Rapidamente e facilmente la migrazione legacy Windows Server 2003 web applicazione toohello cloud.
* Scegliere tooleave il toocreate un'applicazione ibrida locale database associata di SQL.
* Spostare automaticamente il database SQL insieme all'applicazione legacy.

### <a id="smallbusiness"></a>Sto piccole aziende ed è necessario un toohost conveniente sito personale, ma con la crescita futura presente.
Azure App Service è un'ottima soluzione per questo scenario, perché è possibile iniziare a usarlo gratuitamente e quindi aggiungere funzionalità man mano che si rendano necessarie. Ogni app web gratuito dotato di un dominio fornito da Azure (*nome_società*. azurewebsites.net), e piattaforma hello include strumenti di distribuzione e gestione integrati, nonché una raccolta di applicazioni che rendono facilmente tooget avviato. Esistono molti altri servizi e le opzioni di ridimensionamento che consentono di hello sito tooevolve richieste utente maggiore di. Con il Azure App Service, è possibile:

* Iniziare con livello gratuito hello e quindi applicare la scalabilità verticale in base alle esigenze.
* Utilizzare hello tooquickly di raccolta di applicazioni per configurare le applicazioni web più comuni, ad esempio WordPress.
* Aggiungere altri servizi e le funzionalità tooyour applicazione Azure in base alle esigenze.
* Proteggere l'app Web con HTTPS.

### <a id="designer"></a>Sono un web o un progettista grafico e si desidera toodesign e creare siti Web per i clienti
Per gli sviluppatori e i progettisti Azure App Service si integra facilmente con una varietà di framework e strumenti, include il supporto della distribuzione per Git e FTP e offre una stretta integrazione con strumenti e servizi quali Visual Studio e il database SQL. Con il servizio app, è possibile:

* Usare strumenti da riga di comando per [attività automatiche][scripting].
* Lavorare con i linguaggi più diffusi, ad esempio [.Net][dotnet], [PHP][PHP], [Node.js][nodejs], e [Python][Python].
* Selezionare i tre diversi livelli di scalabilità per la scalabilità verticale toovery ad alta capacità.
* Integrazione con altri servizi di Azure, ad esempio [Database SQL][sqldatabase], [Bus di servizio] [ servicebus] e [archiviazione] [ Storage], o partner offerte da hello [Azure Store][azurestore], ad esempio MySQL e MongoDB.
* Effettuare l'integrazione con strumenti quali Visual Studio, Git, WebMatrix, WebDeploy, TFS e FTP.

### <a id="multitier"></a>In corso la migrazione dell'applicazione multilivello con un toohello front-end web Cloud
Se si esegue un'applicazione multilivello, ad esempio un server web che si connette tooa database, servizio App di Azure è una buona soluzione che offre una stretta integrazione con Database SQL di Azure. Ed è possibile utilizzare funzionalità processi Web hello per l'esecuzione di processi di back-end.

Se è necessario più controllo sull'ambiente server hello, ad esempio hello possibilità tooremote nel server o configurare le attività di avvio server, scegliere Service Fabric per uno o più i livelli.

Scegliere le macchine virtuali per uno o più i livelli se si desidera toouse la propria immagine di macchina o eseguire i servizi che non è possibile configurare nell'infrastruttura del servizio o software del server.

### <a id="custom"></a>L'applicazione dipende da Windows altamente personalizzati o ambienti Linux e si desidera toomove è toohello cloud.
Se l'applicazione richiede l'installazione complessi o la configurazione di software e hello del sistema operativo, le macchine virtuali è probabilmente la soluzione migliore hello. Con Macchine virtuali è possibile:

* Utilizzare toostart raccolta di hello macchina virtuale con un sistema operativo, ad esempio Windows o Linux e quindi personalizzarla per i requisiti dell'applicazione.
* Creare e caricare un'immagine personalizzata di un toorun del server locale esistente in una macchina virtuale in Azure.

### <a id="oss"></a>Il sito utilizza software open source e si desidera toohost in Azure
Se il framework open source è supportato nel servizio App, linguaggi hello e Framework necessari per l'applicazione vengono configurate automaticamente. Il servizio app consente di:

* Usare molti linguaggi open source tra i più diffusi, ad esempio [.NET][dotnet], [PHP][PHP], [Node.js][nodejs] e [Python][Python].
* Configurare WordPress, Drupal, Umbraco, DNN e molte altre applicazioni Web di terze parti.
* Eseguire la migrazione di un'applicazione esistente o crearne uno nuovo da hello raccolta di applicazioni.

Se il framework open source non è supportato nel servizio App, è possibile eseguire è in uno dei hello altre opzioni di hosting web Azure. Con le macchine virtuali, installare e configurare il software di hello sull'immagine di macchina hello, che può essere Windows o basata su Linux.

### <a id="lob"></a>Un'applicazione line-of-business che deve tooconnect toohello alla rete aziendale
Se si desidera toocreate un'applicazione line-of-business, il sito Web potrebbe richiedere l'accesso diretto tooservices o dati nella rete aziendale hello. Ciò è possibile nel servizio App, Service Fabric e macchine virtuali tramite hello [servizio di rete virtuale di Azure](/azure/virtual-network/). Nel servizio App è possibile utilizzare hello [funzionalità di integrazione di rete virtuale](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), che consente il toorun applicazioni Azure come se fossero nella rete aziendale.

### <a id="mobile"></a>Voglio toohost un'API REST o il servizio web per client mobili
Servizi web basati su HTTP consentono toosupport un'ampia gamma di client, inclusi i client mobili. Framework di ASP.NET Web API integrarlo con Visual Studio toomake toocreate più semplice e utilizzare i servizi REST.  Questi servizi vengono esposti da un endpoint web, pertanto è possibile toouse qualsiasi web hosting tecnica su Azure toosupport questo scenario. Servizio app è tuttavia un'ottima scelta per l'hosting di API REST. Con il servizio app, è possibile:

* Consente di creare rapidamente un [app per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md) o [app per le API](../app-service-api/app-service-api-apps-why-best-platform.md) servizio web di hello HTTP toohost in uno dei data center distribuiti in modo globale di Azure.
* Eseguire la migrazione di servizi esistenti o crearne di nuovi.
* Ottenere contratto di servizio per la disponibilità per una singola istanza o scalabilità macchine toomultiple dedicato.
* Hello utilizzare pubblicati sito tooprovide API REST tooany client HTTP, inclusi i client mobili.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account, Vai troppo<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, in cui è possibile creare immediatamente un'app di breve durata starter in Azure App Service gratuitamente. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a id="nextsteps"></a> Passaggi successivi
Per ulteriori informazioni sulle opzioni di hosting web hello tre, vedere [Introduzione ad Azure](../fundamentals-introduction-to-azure.md).

tooget avviato con le opzioni di hello scelto per l'applicazione, vedere hello seguenti risorse:

* [servizio app di Azure](/azure/app-service/)
* [Servizi cloud di Azure](/azure/cloud-services/)
* [Macchine virtuali di Azure](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
