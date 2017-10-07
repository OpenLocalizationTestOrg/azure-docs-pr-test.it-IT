---
title: procedure ottimali di protezione dell'infrastruttura a servizio aaaAzure | Documenti Microsoft
description: Questo articolo offre un set di procedure consigliate per la sicurezza di Azure Service Fabric.
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Procedure consigliate per la sicurezza di Azure Service Fabric
Distribuire un'applicazione in Azure è veloce, semplice ed economico. Prima di distribuire l'applicazione cloud in produzione utile toohave una procedura consigliata tooassist nella valutazione dell'applicazione in un elenco di procedure consigliate essenziali e consigliate.

Azure Service Fabric è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire microservizi scalabili e affidabili. Service Fabric risolve inoltre le sfide significativo hello nello sviluppo e la gestione delle applicazioni cloud. Gli sviluppatori e gli amministratori non devono più occuparsi di risolvere complessi problemi di infrastruttura e possono concentrarsi sull'implementazione di carichi di lavoro cruciali e impegnativi, con la certezza di assicurare scalabilità, affidabilità e gestibilità. 

Per ogni procedura consigliata verrà illustrato:

-   Quali consigliabile hello
-   Motivo per cui si desidera tooenable consigliata
-   Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
-   Informazioni come procedura consigliata hello tooenable

Attualmente sono hello Azure Service Fabric sicurezza procedure consigliate seguenti:

-   Utilizzare il modello Manager(ARM) risorse di Azure e cluster sicuro toocreate di modulo di PowerShell Azure Service Fabric
-   Usare certificati X.509
-   Configurare criteri di sicurezza
-   Configurazione della sicurezza in Reliable Actors
-   Configurare l'autenticazione SSL per Azure Service Fabric
-   Isolamento/sicurezza di rete con Azure Service Fabric
-   Configurare un insieme di credenziali delle chiavi per la sicurezza
-   Assegnare gli utenti tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Procedure consigliate per proteggere il cluster

**Quadro generale**

Usare sempre un cluster sicuro
-   Sicurezza del cluster: usare i certificati
-   Accesso client (Admin e sola lettura): usare AAD

Usare distribuzioni automatiche
-   Utilizzare gli script toogenerate, distribuire e, il rollover di segreti
-   Tenere i segreti hello KV, usare Active Directory per tutti gli altri accessi client
-   Nessun umane devono avere accesso toothem senza autenticazione.

Inoltre, prendere in considerazione seguente hello:
-   Creare reti perimetrali usando gruppi di sicurezza di rete (NSG)
-   Usare Jump tooRDP di server in macchine virtuali del cluster o toomanage in un cluster

I cluster devono essere utenti di tooprevent protetto non autorizzato dalla connessione tooyour cluster, in particolare quando dispone i carichi di lavoro in esecuzione su di esso. Sebbene sia possibile toocreate un cluster non protetto, in questo modo consente agli utenti anonimi tooconnect tooit, se espone Gestione endpoint toohello rete Internet pubblica.

Utilizzare le tecnologie tooimplement tali scenari. Hello [degli scenari di sicurezza cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) sono:

-   Nodo a nodo sicurezza This protegge le comunicazioni tra hello macchine virtuali e i computer nel cluster hello. In questo modo si garantisce che solo i computer che sono autorizzati toojoin hello cluster possono prendere parte all'hosting di applicazioni e servizi in cluster hello.
I cluster eseguiti in Azure o i cluster autonomi eseguiti in Windows possono usare la [sicurezza basata su certificati](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) o la [sicurezza di Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) per computer Windows Server.
-   Da client a nodo sicurezza This protegge le comunicazioni tra un client di Service Fabric e i singoli nodi cluster hello.
-   Controllo di accesso basato sui ruoli (RBAC) - hello ruoli amministratore e utente client è specificare in fase di creazione del cluster di hello fornendo identità separate (certificati, e così via AAD) per ognuno.
-   Consigli sulla sicurezza-cluster per Azure, è consigliabile usare i client tooauthenticate di sicurezza di Azure ad e i certificati per la sicurezza del nodo per nodo.

tooconfigure hello autonomo cluster di Windows, vedere [configurare le impostazioni per i cluster di windows autonoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Utilizzare i modelli di gestione risorse di Azure e cluster sicuro toocreate di modulo di PowerShell Azure Service Fabric.
Le istruzioni per configurare un cluster sicuro di Azure Service Fabric in Azure tramite Azure Resource Manager sono disponibili [qui](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Usare un cluster di hello Azure Resource Manager modello toocustomize
-   Archiviazione gestita tramite il programma di installazione per i dischi rigidi virtuali delle macchine virtuali

Utilizzare hello Azure Resource Manager modello toodrive modifiche tooyour gruppo di risorse
-   Gestione facilitata della configurazione
-   Controllo

Gestire la configurazione del cluster come codice
-   Eseguire il controllo delle configurazioni di hello prescelto toodeploy la diagnostica
-   Evitare di utilizzare direttamente le risorse tootweak comandi implicita

Molti aspetti di hello [ciclo di vita dell'applicazione Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) possono essere automatizzate. Il [modulo Azure PowerShell di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatizza le attività di uso più comune per la distribuzione, l'aggiornamento, la rimozione e il test delle applicazioni di Azure Service Fabric. Sono disponibili anche API gestite e HTTP per la gestione delle app.

## <a name="use-x509-certificates"></a>Usare certificati X.509
I cluster devono sempre essere protetti con certificati x.509 o la sicurezza di Windows. Al momento della creazione del cluster viene configurata solo la sicurezza e non è possibile tooenable sicurezza dopo la creazione di cluster hello.

Se si specifica un [certificato cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), impostare il valore di hello di ClusterCredentialType tooX509. Se si specifica il certificato server per le connessioni esterne, impostare tooX509 ServerCredentialType hello.

-   È consigliabile creare i certificati usati nei cluster che eseguono carichi di lavoro di produzione con un servizio certificati di Windows Server configurato correttamente oppure ottenerli da un'Autorità di certificazione (CA) approvata.
-   Non usare mai in fase di produzione certificati temporanei o di test creati con strumenti come MakeCert.exe.
-   È possibile usare un certificato autofirmato, ma lo si deve fare solo per i cluster di test e non nell'ambiente di produzione.

Se il cluster hello è protetto. Chiunque si può connettere in modo anonimo ed eseguire operazioni di gestione. È quindi necessario proteggere sempre i cluster di produzione usando certificati X.509 o la sicurezza di Windows.

più certificati tooenable in cluster di service fabric vedere, toolearn [aggiungere o rimuovere i certificati per un cluster di service fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Configurare criteri di sicurezza
Service Fabric consente anche di hello sicuro le risorse usate dalle applicazioni in fase di hello della distribuzione con account utente di hello, ad esempio, file, directory e i certificati. In questo modo le applicazioni in esecuzione, anche in un ambiente ospitato condiviso, sono reciprocamente protette.

-   Usare un utente o gruppo di dominio Active Directory: È possibile eseguire hello servizio con le credenziali di hello per un account utente o gruppo di Active Directory. Si tratta di Active Directory locale nel dominio e non di Azure Active Directory (Azure AD). Usando un utente di dominio o un gruppo, possono quindi accedere altre risorse nel dominio hello (ad esempio, le condivisioni di file) che sono state concesse autorizzazioni.

-   Assegnare un criterio di accesso di sicurezza per gli endpoint HTTP e HTTPS: se si applica un servizio di tooa criteri RunAs e manifesto del servizio hello dichiara le risorse di endpoint con protocollo hello HTTP, è necessario specificare un tooensure SecurityAccessPolicy che porte allocata toothese gli endpoint sono correttamente ad accesso controllato elencati per l'account utente RunAs cui viene eseguito il servizio hello hello. In caso contrario, http.sys non dispone di accesso toohello servizio e ricevere errori con le chiamate client hello.
toolearn abilitare più criteri di sicurezza dell'infrastruttura di servizio, vedere [configurare criteri di sicurezza per l'applicazione](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Configurazione della sicurezza in Reliable Actors
Servizio Fabric Reliable Actors è un'implementazione del modello di progettazione di hello attore. Come con qualsiasi modello di progettazione del software, decisione hello se toouse un pattern specifico viene eseguito in base a o meno un software per progettare problema soddisfa il criterio di hello.

Come indicazione generale, prendere in considerazione hello attore modello toomodel il problema o scenario se:
-   Il problema riguarda un gran numero (migliaia o più) di piccole unità indipendenti e isolate di stato e logica.
-   Si desidera toowork con oggetti a thread singolo che non richiedono una notevole interazione da componenti esterni, incluse l'esecuzione di query dello stato in un set di attori.
-   Le istanze degli attori non bloccano i chiamanti con ritardi imprevedibili eseguendo operazioni I/O.

In Service Fabric, attori vengono implementati in framework Reliable Actors hello: un framework di applicazione basato su attori modello compilato in cima [affidabili servizi dell'infrastruttura](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Ogni servizio di tipo Reliable Actor che viene scritto è di fatto un servizio Reliable partizionato con stato.
Ogni attore è definito come un'istanza di un tipo attore, identici toohello modo un oggetto .NET è un'istanza di un tipo .NET. Potrebbe esserci più attori di quel tipo distribuiti su vari nodi in un cluster, ad esempio, potrebbe esserci un tipo actor che implementa la funzionalità di hello di una calcolatrice. Ciascuno di questi attori è identificato in modo univoco da un ID.

[Le configurazioni di sicurezza Replicator](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) sono canale di comunicazione utilizzati toosecure hello utilizzato durante la replica. Ciò significa che i servizi non è possibile vedere di altro traffico di replica, assicurandosi che i dati hello resi altamente disponibili anche siano sicuri. Per impostazione predefinita, una sezione di configurazione della sicurezza vuota non abilita la sicurezza della replica.
Le configurazioni di Replicator configurare replicator hello che è responsabile di garantire lo stato del Provider di stato attore hello altamente affidabile.

## <a name="configure-ssl-for-azure-service-fabric"></a>Configurare l'autenticazione SSL per Azure Service Fabric

L'autenticazione del server: [conferma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello client di gestione tooa endpoint Gestione cluster, in modo che hello client management sa stia comunicando toohello reale cluster. Questo certificato fornisce inoltre un [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) per hello API di gestione HTTPS e per Service Fabric Explorer tramite HTTPS.
È necessario ottenere un nome di dominio personalizzato per il cluster. Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.

tooconfigure SSL per un'applicazione, è innanzitutto necessario tooget un certificato SSL firmato da un'autorità di certificazione, una terza parte attendibile che rilascia certificati a questo scopo. Se non hai già uno, è necessario tooobtain da una società che vende i certificati SSL.

certificato Hello deve soddisfare i seguenti requisiti per i certificati SSL in Azure hello:
-   certificato di Hello deve contenere una chiave privata.
-   Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).
-   Hello nome soggetto del certificato deve corrispondere il servizio cloud hello di hello dominio utilizzato tooaccess. È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per il dominio cloudapp.net hello. È necessario acquisire un toouse nome di dominio personalizzato durante l'accesso al servizio. Quando si richiede un certificato da un'autorità di certificazione, nome del soggetto del certificato hello deve corrispondere tooaccess nome di dominio personalizzato hello l'applicazione. Se ad esempio il nome di dominio personalizzato è contoso.com, occorre richiedere alla CA un certificato per **.contoso.com** o **www.contoso.com.**
-   certificato di Hello deve utilizzare almeno la crittografia a 2048 bit.

HTTP non è protetto ed è soggetto tooeavesdropping attacchi perché hello dati trasferiti dal server web toohello di hello web browser o tra gli altri endpoint, viene trasmesso in testo non crittografato. Ciò significa che gli utenti malintenzionati possono intercettare e visualizzare i dati sensibili, ad esempio i dati della carta di credito e gli account di accesso. Quando i dati vengono inviati o pubblicati tramite un browser che usa il protocollo HTTPS, l'autenticazione SSL assicura che tali informazioni siano crittografate e protette da intercettazione.

vedere, più toolearn, [configurare SSL per l'applicazione azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Isolamento/sicurezza di rete con Azure Service Fabric
Utilizzare [modello di Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) come esempio per la configurazione di un tipo di nodo tre cluster protetto e toocontrol hello in ingresso e in uscita il traffico di rete tramite gruppi di sicurezza di rete.

modello Hello è associato un gruppo di sicurezza di rete per ogni hello scala set(VMSS) toocontrol hello traffico delle macchine virtuali da e verso hello VMSS. Per impostazione predefinita, tooallow che tutti hello traffico Necessito vengono impostate regole hello da hello sistema hello e servizi alle porte dell'applicazione specificate nel modello di hello. Esaminare le regole e apportare modifiche toofit delle esigenze, tra cui aggiungere quelli nuovi per le applicazioni.

Per altre informazioni, vedere [Azure Service Fabric: Modelli di rete di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Configurare un insieme di credenziali delle chiavi per la sicurezza
I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni.

Service Fabric utilizza toosecure certificati x. 509 un cluster e fornisce le funzionalità di sicurezza dell'applicazione. Utilizzare insieme di credenziali chiave troppo[gestire i certificati](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) per i cluster di Service Fabric in Azure. Quando viene distribuito un cluster in Azure, i provider di risorse di Azure hello che è responsabili della creazione di cluster di Service Fabric estrae i certificati dall'insieme di credenziali chiave e li installa nel cluster hello macchine virtuali.

relazione tra Hello [insieme credenziali chiavi Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), un cluster di service fabric e provider di risorse di Azure hello che utilizza i certificati archiviati in un insieme di credenziali chiave durante la creazione di un cluster.

**Creare un gruppo di risorse** hello primo passaggio consiste toocreate un gruppo di risorse in modo specifico per l'insieme di credenziali chiave. Si consiglia di inserire l'insieme di credenziali chiave hello nel proprio gruppo di risorse. Questa azione consente di rimuovere hello calcolo e archiviazione gruppi di risorse, tra cui gruppo di risorse hello che contiene il cluster di Service Fabric, senza perdere le chiavi e segreti. gruppo di risorse Hello che contiene l'insieme di credenziali chiave deve essere in hello stessa area geografica hello cluster che lo usa.

**Creare un insieme di credenziali chiave nel nuovo gruppo di risorse hello** hello insieme di credenziali deve essere abilitato per la distribuzione tooallow hello calcolo certificati tooget provider di risorse da esso e installarla su istanze di macchine virtuali.
toolearn più tooset di insieme di credenziali chiave di Azure vedere, [introduzione insieme credenziali chiavi Azure](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Assegnare utenti ai ruoli
Dopo aver creato hello toorepresent di applicazioni del cluster, assegnare gli utenti ruoli toohello supportati dall'infrastruttura di servizio: sola lettura e l'amministratore. È possibile assegnare ruoli hello utilizzando hello portale di Azure classico.

>[!Note]
> Per altre informazioni sui ruoli in Service Fabric, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric supporta due tipi di controllo di accesso diversi per i client che sono connesso tooa [cluster di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): amministratore e utente. Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello.

## <a name="next-steps"></a>Passaggi successivi
- Configurazione dell'[ambiente di sviluppo di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Informazioni sulle [opzioni di supporto di Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

