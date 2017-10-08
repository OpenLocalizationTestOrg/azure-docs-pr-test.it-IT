---
title: Cenni preliminari sulla sicurezza dell'infrastruttura di servizio aaaAzure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di hello protezione dell'infrastruttura del servizio di Azure.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Panoramica della sicurezza di Azure Service Fabric
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire servizi micro scalabili e affidabili. Service Fabric per affrontare sfide significativi di hello nello sviluppo e la gestione delle applicazioni cloud. Gli sviluppatori e gli amministratori non devono più occuparsi di risolvere complessi problemi di infrastruttura e possono concentrarsi sull'implementazione di carichi di lavoro cruciali e impegnativi, con la certezza di assicurare scalabilità, affidabilità e gestibilità.

Cenni preliminari sulla sicurezza di Azure Service Fabric viene descritta la hello seguenti aree:

-   Protezione del cluster
-   Monitoraggio e diagnostica
-   Protezione con certificati
-   Controllo degli accessi in base al ruolo
-   Protezione di un cluster con la sicurezza di Windows
-   Configurazione della sicurezza dell'applicazione in Service Fabric
-   Protezione della comunicazione per i servizi nella sicurezza di Azure Service Fabric

## <a name="securing-your-cluster"></a>Protezione del cluster
Azure Service Fabric è un agente di orchestrazione dei servizi in un cluster di macchine, i cluster devono essere utenti tooprevent protetto non autorizzato dalla connessione tooyour cluster, in particolare quando dispone i carichi di lavoro in esecuzione su di esso. Sebbene sia possibile toocreate un cluster non protetto, in questo modo consente agli utenti anonimi tooconnect tooit, se espone Gestione endpoint toohello rete Internet pubblica.

In questa sezione viene fornita una panoramica di hello scenari di sicurezza per i cluster in esecuzione in Azure o autonomo e hello varie tecnologie utilizzate tooimplement tali scenari. scenari di sicurezza cluster Hello sono:

-   Sicurezza da nodo a nodo
-   Sicurezza da client a nodo

### <a name="node-to-node-security"></a>Sicurezza da nodo a nodo
Consente di proteggere la comunicazione tra macchine virtuali hello o computer cluster hello. In questo modo si garantisce che solo i computer che sono autorizzati toojoin hello cluster possono prendere parte all'hosting di applicazioni e servizi in cluster hello.

I cluster eseguiti in Azure o i cluster autonomi eseguiti in Windows possono usare la [sicurezza basata su certificati](https://msdn.microsoft.com/library/ff649801.aspx) o la [sicurezza di Windows](https://msdn.microsoft.com/library/ff649396.aspx) per computer Windows Server.

**Sicurezza basata su certificati da nodo a nodo**

Service Fabric utilizza i certificati server x. 509 specificato come parte delle configurazioni di tipo di nodo hello quando si crea un cluster. Questo articolo include una rapida panoramica di questi certificati e di [come è possibile acquisirli o crearli](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Sicurezza di certificato è stata configurata durante la creazione di cluster hello tramite hello portale di Azure, i modelli di gestione risorse di Azure o un modello JSON autonoma. È possibile specificare un certificato primario e un certificato secondario facoltativo che viene usato per i rollover dei certificati. Hello certificati primari e secondari, si specifica devono essere diversi da client di amministrazione di hello e i certificati client di sola lettura specificati per [sicurezza Client a nodo](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Sicurezza da client a nodo
Sicurezza toonode client viene configurato tramite le identità del Client. tooestablish attendibilità tra un client e hello cluster, è necessario configurare hello cluster tooknow quali identità del client che è attendibile. È possibile, a questo scopo, eseguire una delle due operazioni seguenti:

-   Specificare gli utenti al gruppo di dominio hello in grado di connettersi o
-   Specificare gli utenti al nodo di dominio hello in grado di connettersi.

Service Fabric supporta due tipi di controllo di accesso diversi per i client appartenenti a cluster di Service Fabric tooa connessa:

-   Amministratore
-   Utente

Controllo di accesso offre possibilità hello hello tipi cluster amministratore toolimit accesso toocertain delle operazioni di cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello. Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.

**Sicurezza basata su certificati da client a nodo**

Certificato client da nodo sicurezza configurata durante la creazione di cluster hello tramite hello portale di Azure, modelli di gestione risorse o un modello JSON autonoma specificando un certificato client di amministrazione e/o di un certificato client utente. Hello amministrazione utente client i certificati client e che si specifica devono essere diversi rispetto ai certificati primari e secondari hello specificate per la sicurezza del nodo per nodo.

Client che si connettono toohello cluster utilizzando il certificato di amministrazione hello dispongano di funzionalità di toomanagement accesso completo. Client che si connettono toohello cluster utilizzando hello utente di sola lettura del certificato client dispone solo dell'accesso in lettura toomanagement funzionalità. In altre parole, che questi certificati vengono usati per hello ruolo si basa il controllo di accesso (RBAC).

Per leggere Azure [configurazione di un cluster utilizzando un modello di gestione risorse di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn tooconfigure come certificato di sicurezza in un cluster.

**Sicurezza di Azure Active Directory (AAD) da client a nodo in Azure**

I cluster in esecuzione in Azure possono inoltre proteggere accesso toohello gli endpoint di gestione tramite Azure Active Directory (AAD). Vedere [configurazione di un cluster utilizzando un modello di gestione risorse di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) per informazioni su come toocreate hello gli elementi necessari di AAD, come toopopulate durante cluster la creazione e la modalità tooconnect toothose cluster in un secondo momento.

AAD consente alle organizzazioni (note come tenant) toomanage utente accesso tooapplications, sono suddivise nelle applicazioni con un account di accesso dell'interfaccia utente basata sul web e applicazioni con un'esperienza di native client.

Un cluster di Service Fabric offre tooits punti di ingresso diverse funzionalità di gestione, tra cui hello basata sul web Service Fabric Explorer e Visual Studio. Di conseguenza, creare due AAD applicazioni toocontrol accesso toohello cluster, un'applicazione web e un'applicazione nativa.
Per i cluster di Azure, è consigliabile usare i client tooauthenticate di sicurezza di Azure ad e i certificati per la sicurezza del nodo per nodo.

Per i cluster di Windows Server autonomi è consigliabile usare la sicurezza di Windows con account gestiti di gruppo, se sono presenti Windows Server 2012 R2 e Active Directory. In caso contrario, usare comunque la sicurezza di Windows con account di Windows.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitoraggio e diagnostica in Azure Service Fabric
[Monitoraggio e diagnostica](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) sono critici toodeveloping, test e distribuzione di applicazioni e servizi in qualsiasi ambiente. Le soluzioni di Service Fabric funzionano meglio quando si pianifica e si implementa il monitoraggio e la diagnostica che consentono di verificare che le applicazioni e i servizi funzionino come previsto in un ambiente di sviluppo locale o in fase di produzione.

Da una prospettiva di sicurezza, hello obiettivi principali di monitoraggio e la diagnostica:

-   Rilevare e diagnosticare i problemi di hardware e l'infrastruttura che potrebbero essere dovuti tooa eventi di protezione.
-   Rilevare i problemi di app e software che potrebbero presentare indicatori di compromissione (IoC).
-   Risorse di comprendere il consumo toohelp impedire accidentale di tipo denial of service.

Hello generale del flusso di lavoro di monitoraggio e diagnostica è costituito da tre passaggi:

-   **Generazione di eventi:** infrastruttura hello (cluster) sia a livello di applicazione / servizio sono inclusi gli eventi (log, le tracce, gli eventi personalizzati). Altre informazioni sui [eventi a livello di infrastruttura](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) e [eventi a livello di applicazione](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand quello fornito e come tooadd ulteriormente strumentazione.
-   **Aggregazione evento:** gli eventi generati necessario toobe raccolti e aggregati prima che possano essere visualizzati. In genere, è consigliabile utilizzare [diagnostica Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (raccolta di log basato su tooagent più simile) o [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (in-process la raccolta di log).
-   **Analisi:** gli eventi devono toobe visualizzato e accessibile in un formato, tooallow per l'analisi e visualizzazione in base alle esigenze. Esistono diverse piattaforme grande che esistono nel mercato hello per quanto riguarda toohello analisi e la visualizzazione dei dati di monitoraggio e diagnostica. Hello consigliati sono due [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) e [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) scadenza tootheir una migliore integrazione con Service Fabric.

È inoltre possibile utilizzare [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor molte delle risorse di Azure in cui viene compilato un cluster di Service Fabric di hello.

Un controllo è un servizio separato che può controllare l'integrità e il carico tra servizi e segnalare l'integrità per tutti gli elementi nella gerarchia del modello di integrità hello. Ciò consente di evitare gli errori che non verrebbero rilevati in base a visualizzazione hello di un singolo servizio. Watchdog sono inoltre un codice di toohost buona che esegue le azioni correttive senza interazione dell'utente (ad esempio, pulizia dei file di log nell'archiviazione a determinati intervalli di tempo). È possibile trovare un'implementazione di esempio del servizio watchdog [qui](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Protezione con certificati
Utilizzo di certificati, viene indicato come toosecure hello comunicazione hello vari nodi del cluster di Windows autonoma, nonché il modo tooauthenticate client che si connettono toothis cluster, utilizzando i certificati x. 509. Ciò garantisce che solo gli utenti autorizzati possono accedere cluster hello, hello applicazioni distribuite e attività di gestione. Sicurezza di certificato deve essere abilitata nel cluster hello quando viene creato il cluster hello.

### <a name="x509-certificates-and-service-fabric"></a>Certificati X.509 e Service Fabric
I certificati digitali x. 509 sono utilizzati tooauthenticate client e server e tooencrypt e firmare digitalmente i messaggi.

Hello nella tabella seguente elenca i certificati di hello che sarà necessario nel programma di installazione del cluster:

|Impostazione Informazioni sul certificato |Descrizione|
|-------------------------------|-----------|
|ClusterCertificate|    Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster. È possibile usare due diversi certificati, uno primario e uno secondario per l'aggiornamento.|
|ServerCertificate| Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster. È possibile usare due diversi certificati del server, uno primario e uno secondario per l'aggiornamento.|
|ClientCertificateThumbprints|  Si tratta di un set di certificati che si desidera tooinstall nei client hello autenticato.|
|ClientCertificateCommonNames|  Impostare hello nome comune del certificato client prima di hello hello CertificateCommonName. Hello CertificateIssuerThumbprint è l'identificazione personale hello per emittente hello del certificato.|
|ReverseProxyCertificate|   Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Per altre informazioni sulla protezione dei certificati, [fare clic qui](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo
Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello. Sono supportati due tipi di controllo di accesso diverso per client che si connettono tooa cluster: ruolo di amministratore e il ruolo utente.

Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.

Specificare hello ruoli amministratore e utente client in fase di creazione del cluster di hello fornendo identità separate (certificati, e così via AAD) per ognuno. Per ulteriori informazioni su impostazioni di controllo di accesso predefinito hello e come toochange hello le impostazioni predefinite, vedere [controllo di accesso basato sui ruoli per i client di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Protezione di un cluster con la sicurezza di Windows
cluster di Service Fabric tooa accesso non autorizzato di tooprevent, è necessario proteggere il cluster hello. Protezione è particolarmente importante quando il cluster hello esegue i carichi di lavoro. Vengono descritte la sicurezza del nodo a nodo e al nodo client tooconfigure utilizzando la sicurezza in Windows hello file Clusterconfig.

**Configurare la sicurezza di Windows usando l'approccio account del servizio gestito di gruppo**

Tramite l'impostazione viene configurata la sicurezza di toonode nodo [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) quando service fabric deve toorun in gMSA. In ordine toobuild le relazioni di trust tra i nodi, è necessario essere informati del loro.

Sicurezza toonode client viene configurato tramite ClientIdentities. In ordine tooestablish trust tra un client e hello di cluster, è necessario configurare hello cluster tooknow quali identità del client che è attendibile.

**Configurare la sicurezza di Windows usando un gruppo di computer**

Sicurezza toonode del nodo è configurato per l'impostazione utilizzando ClusterIdentity se si desidera toouse un gruppo di computer all'interno di un dominio Active Directory. Per altre informazioni, vedere l'articolo su come [Creare un gruppo di computer in Active Directory](https://msdn.microsoft.com/library/aa545347).

La sicurezza da client a nodo viene configurata tramite le identità dei client. tooestablish attendibilità tra un client e hello cluster, è necessario configurare hello cluster tooknow hello client identità hello cluster è attendibile. È possibile stabilire una relazione di trust in due modi diversi:

-   Specificare gli utenti al gruppo di dominio hello in grado di connettersi.
-   Specificare gli utenti al nodo di dominio hello in grado di connettersi.

## <a name="configure-application-security-in-service-fabric"></a>Configurazione della sicurezza dell'applicazione in Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Gestione dei segreti nelle applicazioni di Service Fabric
Questa modalità consente di gestire i segreti in un'applicazione di Service Fabric. I segreti possono essere informazioni riservate, ad esempio le stringhe di connessione di archiviazione, le password o altri valori che non devono essere gestiti in testo normale.

Questo approccio utilizza [insieme credenziali chiavi Azure](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage chiavi e segreti. Tuttavia, utilizzando i segreti in un'applicazione è cluster cloud tooallow indipendente dalla piattaforma applicazioni toobe distribuito tooa con ospitati in qualsiasi punto. In questo flusso sono presenti quattro passaggi principali:

-   Ottenere un certificato di crittografia dei dati.
-   Installare il certificato di hello del cluster.
-   Crittografare i valori dei segreti quando si distribuisce un'applicazione con certificato hello e li inserisce nel file di configurazione di un servizio Settings.
-   I valori di lettura crittografato fuori Settings decrittografando con hello stesso certificato di crittografia.

>[!Note]
>Per altre informazioni, vedere [Gestione dei segreti nelle applicazioni di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Configurare i criteri di sicurezza per l'applicazione
Utilizzando la protezione dell'infrastruttura di Azure servizio, è possibile la protezione delle applicazioni che sono in esecuzione in cluster hello con account utente diversi. Protezione dell'infrastruttura del servizio consente inoltre di hello sicuro le risorse usate dalle applicazioni in fase di hello della distribuzione con account utente di hello, ad esempio, file, directory e i certificati. In questo modo le applicazioni in esecuzione, anche in un ambiente ospitato condiviso, sono reciprocamente protette.
Hello passaggi includono:

-   Configurare i criteri di hello per un punto di ingresso del programma di installazione del servizio.
-   Avviare i comandi di PowerShell da un punto di ingresso dell'installazione.
-   Usare il reindirizzamento della console per il debug locale.
-   Configurare i criteri per i pacchetti di codice del servizio.
-   Assegnare criteri di accesso di sicurezza per gli endpoint HTTP e HTTPS.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Protezione della comunicazione per i servizi nella sicurezza di Azure Service Fabric
La sicurezza è uno degli aspetti più importanti di hello di comunicazione. Hello servizi affidabili application framework fornisce alcuni stack di comunicazione predefiniti e gli strumenti che possono essere utilizzati tooimprove sicurezza.

-   [Proteggere un servizio quando si usa la comunicazione remota dei servizi](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Proteggere un servizio quando si usa uno stack di comunicazione basato su WCF](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Passaggi successivi
- Per informazioni concettuali sulla protezione del cluster, vedere [Creare un cluster di Service Fabric usando Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) e il [Creare un cluster di Service Fabric in Azure tramite il portale di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Per altre informazioni, vedere [Scenari di sicurezza di un cluster di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
