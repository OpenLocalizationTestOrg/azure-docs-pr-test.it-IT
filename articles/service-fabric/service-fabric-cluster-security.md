---
title: un cluster di Service Fabric aaaSecure | Documenti Microsoft
description: Descrive gli scenari di sicurezza hello per tooimplement di diverse tecnologie utilizzate hello e di cluster di Service Fabric tali scenari.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Scenari di sicurezza di un cluster di Service Fabric
Un cluster di Service Fabric è una risorsa di cui si è proprietari. I cluster devono essere utenti di tooprevent protetto non autorizzato dalla connessione tooyour cluster, in particolare quando dispone i carichi di lavoro in esecuzione su di esso. Sebbene sia possibile toocreate un cluster non protetto, in questo modo consente agli utenti anonimi tooconnect tooit, se espone Gestione endpoint toohello rete Internet pubblica. 

In questo articolo viene fornita una panoramica di hello scenari di sicurezza per i cluster in esecuzione in Azure o autonomo e hello varie tecnologie utilizzate tooimplement tali scenari. scenari di sicurezza cluster Hello sono:

* Sicurezza da nodo a nodo
* Sicurezza da client a nodo
* Controllo degli accessi in base al ruolo

## <a name="node-to-node-security"></a>Sicurezza da nodo a nodo
Consente di proteggere la comunicazione tra macchine virtuali hello o computer cluster hello. In questo modo si garantisce che solo i computer che sono autorizzati toojoin hello cluster possono prendere parte all'hosting di applicazioni e servizi in cluster hello.

![Diagramma della comunicazione da nodo a nodo][Node-to-Node]

I cluster eseguiti in Azure o i cluster autonomi eseguiti in Windows possono usare la [sicurezza basata su certificati](https://msdn.microsoft.com/library/ff649801.aspx) o la [sicurezza di Windows](https://msdn.microsoft.com/library/ff649396.aspx) per computer Windows Server.

### <a name="node-to-node-certificate-security"></a>Sicurezza basata su certificati da nodo a nodo
Service Fabric utilizza i certificati server x. 509 specificato come parte delle configurazioni di tipo di nodo hello quando si crea un cluster. Alla fine di hello di questo articolo, viene fornita una rapida panoramica di questi certificati sono e come è possibile acquisire o crearli.

Sicurezza di certificato è stata configurata durante la creazione di cluster hello tramite hello portale di Azure, i modelli di gestione risorse di Azure o un modello JSON autonoma. È possibile specificare un certificato primario e un certificato secondario facoltativo che viene usato per i rollover dei certificati. Hello certificati primari e secondari, si specifica devono essere diversi da client di amministrazione di hello e i certificati client di sola lettura specificati per [sicurezza Client a nodo](#client-to-node-security).

Per leggere Azure [configurazione di un cluster utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md) toolearn tooconfigure come certificato di sicurezza in un cluster.

Per cluster Windows Server autonomi, vedere [Proteggere un cluster autonomo in Windows con certificati X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Sicurezza di Windows da nodo a nodo
Per cluster Windows Server autonomi, vedere [Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Sicurezza da client a nodo
Autentica i client e consente di proteggere la comunicazione tra un client e i singoli nodi cluster hello. Questo tipo di sicurezza autentica e protegge le comunicazioni client, che garantisce che solo gli utenti autorizzati possano accedere al cluster hello e applicazioni hello distribuite in cluster hello. I client vengono identificati in modo univoco con le credenziali di sicurezza di Windows o le credenziali di sicurezza del relativo certificato.

![Diagramma della comunicazione da client a nodo][Client-to-Node]

I cluster eseguiti in Azure o i cluster autonomi eseguiti in Windows possono usare la [sicurezza basata su certificati](https://msdn.microsoft.com/library/ff649801.aspx) o la [sicurezza di Windows](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>Sicurezza basata su certificati da client a nodo
 Certificato client da nodo sicurezza configurata durante la creazione di cluster hello tramite hello portale di Azure, modelli di gestione risorse o un modello JSON autonoma specificando un certificato client di amministrazione e/o di un certificato client utente.  Hello amministrazione utente client i certificati client e si specifica devono essere diversi da quello primario hello e certificati secondari per specificare per [sicurezza nodo a nodo](#node-to-node-security) come procedura consigliata. Per impostazione predefinita, i certificati di hello cluster per la sicurezza del nodo a nodo vengono aggiunti toohello consentito Admin elenco di certificati client.

Client che si connettono toohello cluster utilizzando il certificato di amministrazione hello dispongano di funzionalità di toomanagement accesso completo.  Client che si connettono toohello cluster utilizzando hello utente di sola lettura del certificato client dispone solo dell'accesso in lettura toomanagement funzionalità. In altre parole, questi certificati vengono utilizzati per il controllo di accesso hello ruoli basi (RBAC) descritto più avanti in questo articolo.

Per leggere Azure [configurazione di un cluster utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md) toolearn tooconfigure come certificato di sicurezza in un cluster.

Per cluster Windows Server autonomi, vedere [Proteggere un cluster autonomo in Windows con certificati X.509 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Sicurezza di Azure Active Directory (AAD) da client a nodo in Azure
I cluster in esecuzione in Azure possono inoltre proteggere accesso toohello gli endpoint di gestione tramite Azure Active Directory (AAD). Vedere [configurazione di un cluster utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md) per informazioni su come toocreate hello gli elementi necessari di AAD, come toopopulate durante cluster la creazione e la modalità tooconnect toothose cluster in un secondo momento.

## <a name="security-recommendations"></a>Raccomandazioni sulla sicurezza
Per i cluster di Azure, è consigliabile usare i client tooauthenticate di sicurezza di Azure ad e i certificati per la sicurezza del nodo per nodo.

È consigliabile usare la sicurezza di Windows con account gestiti di gruppo Per i cluster Windows Server autonomi, se sono presenti Windows Server 2012 R2 e Active Directory. In caso contrario, usare comunque la sicurezza di Windows con account di Windows.

## <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo (RBAC)
Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello. Sono supportati due tipi di controllo di accesso diverso per client che si connettono tooa cluster: ruolo di amministratore e il ruolo utente.

Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.

Specificare hello ruoli amministratore e utente client in fase di creazione del cluster di hello fornendo identità separate (certificati, e così via AAD) per ognuno. Per ulteriori informazioni su impostazioni di controllo di accesso predefinito hello e come toochange hello le impostazioni predefinite, vedere [controllo di accesso basato sui ruoli per i client di Service Fabric](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>Certificati X.509 e Service Fabric
I certificati digitali x. 509 sono utilizzati tooauthenticate client e server e tooencrypt e firmare digitalmente i messaggi. Per ulteriori informazioni su questi certificati, andare troppo[utilizzo dei certificati](http://msdn.microsoft.com/library/ms731899.aspx).

Tooconsider alcuni aspetti importanti:

* È consigliabile creare i certificati usati nei cluster che eseguono carichi di lavoro di produzione con un servizio certificati di Windows Server configurato correttamente oppure ottenerli da un' [autorità di certificazione (CA)](https://en.wikipedia.org/wiki/Certificate_authority)approvata.
* Non usare mai in fase di produzione certificati temporanei o di test creati con strumenti come MakeCert.exe.
* È possibile usare un certificato autofirmato, ma lo si deve fare solo per i cluster di test e non nell'ambiente di produzione.

### <a name="server-x509-certificates"></a>Certificati server X.509
I certificati del server sono attività primaria hello di autenticare un tooclients server (nodo) o autenticazione di un server di tooa server (nodo) (nodo). Uno dei controlli di hello iniziali quando un client o un nodo esegue l'autenticazione di un nodo è valore hello toocheck del nome comune di hello nel campo oggetto hello. Questo nome comune o uno dei nomi alternativi del soggetto dei certificati hello deve essere presente nell'elenco di hello di nomi comuni consentiti.

Hello articolo viene descritto come toogenerate certificati con nomi alternativi del soggetto (SAN): [come tooadd un tooa nome alternativo soggetto proteggere certificato LDAP](http://support.microsoft.com/kb/931351).

campo Subject Hello può contenere più valori, ognuno preceduto da un tipo di valore di inizializzazione tooindicate hello. In genere, l'inizializzazione di hello è "CN" per il nome comune. ad esempio "CN = www.contoso.com". È anche possibile che per l'oggetto hello campo toobe vuoto. Se il campo nome alternativo del soggetto facoltativo di hello è popolato, deve contenere nome comune di hello del certificato hello e una voce per ogni nome alternativo del soggetto. Queste voci vengono immesse come valori di nomi DNS.

il valore di Hello del campo di hello scopi designati del certificato hello deve includere un valore appropriato, ad esempio "Server Authentication" o "Autenticazione Client".

### <a name="client-x509-certificates"></a>Certificati client X.509
I certificati client in genere non vengono rilasciati da un'autorità di certificazione di terze parti. In alternativa, hello archivio personale hello corrente della località dell'utente in genere contiene i certificati client inseriti da un'autorità radice, con un obiettivo di "Autenticazione Client". Hello client potrà utilizzare tale certificato è necessaria l'autenticazione reciproca.

> [!NOTE]
> Tutte le operazioni di gestione in un cluster di Service Fabric richiedono certificati server. I certificati client non possono essere usati per la gestione.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Passaggi successivi
Questo articolo contiene informazioni di carattere generale sulla protezione del cluster. Successivamente,


1.  [creare un cluster in Azure con un modello di Resource Manager](service-fabric-cluster-creation-via-arm.md) 
2.  [portale di Azure](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
