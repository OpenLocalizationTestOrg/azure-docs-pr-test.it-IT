---
title: aaaSecure un cluster in esecuzione su Windows tramite la sicurezza di Windows | Documenti Microsoft
description: Informazioni su come tooconfigure nodi a e nodo client per la sicurezza autonoma cluster in esecuzione in Windows tramite la sicurezza di Windows.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Proteggere un cluster autonomo in Windows usando la protezione di Windows
cluster di Service Fabric tooa accesso non autorizzato di tooprevent, è necessario proteggere il cluster hello. Protezione è particolarmente importante quando il cluster hello esegue i carichi di lavoro. Questo articolo viene descritto come protezione tooconfigure di nodo a nodo e al nodo client utilizzando la sicurezza di Windows hello *Clusterconfig* file.  processo Hello corrisponde toohello configurare il passaggio di sicurezza di [creare un cluster autonoma in esecuzione su Windows](service-fabric-cluster-creation-for-windows-server.md). Per altre informazioni sull'uso della protezione di Windows in Service Fabric, vedere [Scenari di sicurezza del cluster](service-fabric-cluster-security.md).

> [!NOTE]
> Poiché non esiste alcun aggiornamento del cluster da una protezione scelta tooanother occorre considerare attentamente selezione hello di sicurezza di nodo per nodo. selezione di sicurezza hello toochange, si dispone di toorebuild hello completo cluster.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Configurare la funzionalità di sicurezza di Windows usando l'approccio account del servizio gestito del gruppo  
esempio Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* scaricare file di configurazione con hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) autonomo pacchetto del cluster contiene un modello per la configurazione di sicurezza di Windows utilizzando [gruppo Account del servizio gestito (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Impostazioni di configurazione** | **Descrizione** |  
| --- | --- |  
| WindowsIdentities |Contiene le identità di hello del client e del cluster. |  
| ClustergMSAIdentity |Configura la sicurezza da nodo a nodo. Account del servizio gestito del gruppo. |  
| ClusterSPN |SPN di dominio completo per l'account del servizio gestito del gruppo|  
| ClientIdentities |Configura la sicurezza da client a nodo. Matrice di account utente del client. |  
| Identità |identità del client Hello, un utente di dominio. |  
| IsAdmin |True specifica il che utente di dominio hello dispone di accesso client come amministratore, false per l'accesso client utente. |  
  
[Sicurezza del nodo toonode](service-fabric-cluster-security.md#node-to-node-security) configurato impostando **ClustergMSAIdentity** quando service fabric deve toorun in gMSA. In ordine toobuild le relazioni di trust tra i nodi, è necessario essere informati del loro. Questa operazione può essere eseguita in due modi diversi: specificare hello gruppo Account del servizio gestito che include tutti i nodi nel cluster hello o gruppo di computer di dominio hello che include tutti i nodi nel cluster hello. È consigliabile utilizzare hello [gruppo Account del servizio gestito (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approccio, in particolare per i cluster di grandi dimensioni (oltre 10 nodi) o per i cluster sono probabilmente toogrow o riduzione.  
Questo approccio non richiede hello creazione di un gruppo di dominio per il quale gli amministratori di cluster sono state concesse tooadd diritti di accesso e rimuovere membri. Questi account si rivelano utili anche nella gestione automatica delle password. Per altre informazioni, vedere [Introduzione gli account del servizio gestiti del gruppo](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Sicurezza di client toonode](service-fabric-cluster-security.md#client-to-node-security) viene configurato usando **ClientIdentities**. In ordine tooestablish trust tra un client e hello di cluster, è necessario configurare hello cluster tooknow quali identità del client che è attendibile. Questa operazione può essere eseguita in due modi diversi: specificare gli utenti al gruppo di dominio hello che possono connettersi o specificare hello agli utenti di nodo di dominio in grado di connettersi. Service Fabric supporta due tipi di controllo di accesso diversi per i client che sono connessi tooa cluster di Service Fabric: amministratore e utente. Controllo di accesso offre possibilità hello hello tipi cluster amministratore toolimit accesso toocertain delle operazioni di cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello.  Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e. Per altre informazioni sul controllo degli accessi, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric](service-fabric-cluster-security-roles.md).  
 
Hello seguente esempio **sicurezza** sezione Configura la sicurezza di Windows utilizzando l'account e specifica che hello macchine *ServiceFabric.clusterA.contoso.com* gMSA fanno parte del cluster hello e che *CONTOSO\usera* dispone di accesso client di amministrazione:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Configurare la funzionalità di sicurezza di Windows usando un gruppo di computer  
esempio Hello *ClusterConfig.Windows.MultiMachine.JSON* scaricare file di configurazione con hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) autonomo pacchetto del cluster contiene un modello per la configurazione di sicurezza di Windows.  Sicurezza di Windows è configurata in hello **proprietà** sezione: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Impostazione di configurazione** | **Descrizione** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** è troppo*Windows* se ClusterIdentity specifica un nome gruppo di computer Active Directory. |  
| ServerCredentialType |Impostare troppo*Windows* tooenable la sicurezza di Windows per i client.<br /><br />Ciò indica che i client hello di hello e cluster hello stesso siano in esecuzione all'interno di un dominio Active Directory. |  
| WindowsIdentities |Contiene le identità di hello del client e del cluster. |  
| ClusterIdentity |Utilizzare un nome del gruppo di computer, domain\machinegroup, protezione da nodo a nodo tooconfigure. |  
| ClientIdentities |Configura la sicurezza da client a nodo. Matrice di account utente del client. |  
| Identità |Aggiungere l'utente di dominio hello, DOMINIO\nome utente, per l'identità del client hello. |  
| IsAdmin |Set tootrue toospecify che hello utente di dominio dispone di accesso client come amministratore o false per l'accesso client utente. |  

[Sicurezza del nodo toonode](service-fabric-cluster-security.md#node-to-node-security) viene configurato tramite l'impostazione **ClusterIdentity** se si desidera toouse un gruppo di computer all'interno di un dominio Active Directory. Per altre informazioni, vedere l'articolo su come [Creare un gruppo di computer in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

La [sicurezza da client a nodo](service-fabric-cluster-security.md#client-to-node-security) viene configurata usando **ClientIdentities**. tooestablish attendibilità tra un client e hello cluster, è necessario configurare hello cluster tooknow hello client identità hello cluster è attendibile. È possibile stabilire una relazione di trust in due modi diversi:

- Specificare gli utenti al gruppo di dominio hello in grado di connettersi.
- Specificare gli utenti al nodo di dominio hello in grado di connettersi.

Service Fabric supporta due tipi di controllo di accesso diversi per i client che sono connessi tooa cluster di Service Fabric: amministratore e utente. Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain i tipi di operazioni di cluster per diversi gruppi di utenti, che rende più sicura cluster hello.  Gli amministratori hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Gli utenti, per impostazione predefinita, dispongono solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.  

Hello seguente esempio **sicurezza** sezione Configura la sicurezza di Windows, specifica che hello macchine *ServiceFabric/clusterA.contoso.com* fanno parte del cluster hello e specifica che  *CONTOSO\usera* dispone di accesso client di amministrazione:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Service Fabric non devono essere distribuito in un controller di dominio. Assicurarsi che Clusterconfig non include l'indirizzo IP hello hello del controller di dominio quando si utilizza un gruppo di computer o gruppo Account del servizio gestito (gMSA).
>
>

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato la sicurezza di Windows in hello *Clusterconfig* file, riprendere il processo di creazione di cluster hello in [creare un cluster autonoma in esecuzione su Windows](service-fabric-cluster-creation-for-windows-server.md).

Per altre informazioni sulla sicurezza da nodo a nodo e da client a nodo e sul controllo degli accessi in base al ruolo, vedere [Scenari di sicurezza del cluster](service-fabric-cluster-security.md).

Vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md) per esempi di connessione tramite PowerShell o FabricClient.
