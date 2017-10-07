---
title: 'Sicurezza di un cluster di Service Fabric: ruoli client | Microsoft Docs'
description: Questo articolo descrive i due ruoli hello del client e le autorizzazioni di hello toohello ruoli fornite.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Controllo di accesso basato sui ruoli per i client di Service Fabric
Azure Service Fabric supporta due tipi di controllo di accesso diversi per i client che sono connessi tooa cluster di Service Fabric: amministratore e utente. Controllo degli accessi consente hello cluster amministratore toolimit accesso toocertain le operazioni del cluster per diversi gruppi di utenti, di rendere più sicuro cluster hello.  

**Gli amministratori** hanno capacità di toomanagement accesso completo (incluse le funzionalità di lettura/scrittura). Per impostazione predefinita, **utenti** dispone solo dell'accesso in lettura toomanagement funzionalità (ad esempio, funzionalità di query), hello possibilità tooresolve applicazioni e servizi e.

Specificare i ruoli client hello due (amministratore e client) in fase di creazione del cluster di hello fornendo certificati separati per ogni. Per informazioni dettagliate su come configurare un cluster di Service Fabric protetto, vedere l'articolo relativo alla [sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md) .

## <a name="default-access-control-settings"></a>Impostazioni predefiniti di controllo di accesso
tipo di controllo di accesso amministratore Hello è hello tooall accesso completo FabricClient APIs. Può eseguire tutte le letture e scritture nel cluster di Service Fabric hello, inclusi hello seguenti operazioni:

### <a name="application-and-service-operations"></a>Operazioni dell’applicazione e di servizio
* **CreateService**: creazione del servizio                             
* **CreateServiceFromTemplate**: creazione del servizio da un modello                             
* **UpdateService**: aggiornamenti del servizio                             
* **DeleteService**: eliminazione del servizio                             
* **ProvisionApplicationType**: provisioning del tipo applicazione                             
* **CreateApplication**: creazione dell'applicazione                               
* **DeleteApplication**: eliminazione dell'applicazione                             
* **UpgradeApplication**: avvio o interruzione degli aggiornamenti dell'applicazione                             
* **UnprovisionApplicationType**: annullamento del provisioning del tipo applicazione                             
* **MoveNextUpgradeDomain**: ripresa degli aggiornamenti dell'applicazione con un dominio di aggiornamento esplicito                             
* **ReportUpgradeHealth**: riprendere gli aggiornamenti dell'applicazione con lo stato dell'aggiornamento corrente hello                             
* **ReportHealth**: report d'integrità                             
* **PredeployPackageToNode**: API di pre-distribuzione                            
* **CodePackageControl**: riavvio dei pacchetti di codice                             
* **RecoverPartition**: ripristino di una partizione                             
* **RecoverPartitions**: ripristino di partizioni                             
* **RecoverServicePartitions**: ripristino di partizioni del servizio                             
* **RecoverSystemPartitions**: ripristino di partizioni del servizio di sistema                             

### <a name="cluster-operations"></a>Operazioni del cluster
* **ProvisionFabric**: provisioning del manifesto del cluster e/o del file con estensione msi                             
* **UpgradeFabric**: avvio degli aggiornamenti del cluster                             
* **UnprovisionFabric**: annullamento del provisioning del manifesto del cluster e/o del file con estensione msi                         
* **MoveNextFabricUpgradeDomain**: ripresa degli aggiornamenti del cluster con un dominio di aggiornamento esplicito                             
* **ReportFabricUpgradeHealth**: riprendere gli aggiornamenti di cluster con lo stato dell'aggiornamento corrente hello                             
* **StartInfrastructureTask**: avvio delle attività di infrastruttura                             
* **FinishInfrastructureTask**: completamento delle attività di infrastruttura                             
* **InvokeInfrastructureCommand**: comandi di gestione delle attività di infrastruttura                              
* **ActivateNode**: attivazione di un nodo                             
* **DeactivateNode**: disattivazione di un nodo                             
* **DeactivateNodesBatch**: disattivazione di più nodi                             
* **RemoveNodeDeactivations**: ripristino della disattivazione in più nodi                             
* **GetNodeDeactivationStatus**: controllo dello stato di disattivazione                             
* **NodeStateRemoved**: report dello stato del nodo rimosso                             
* **ReportFault**: report dell'errore                             
* **FileContent**: l'immagine di trasferimento di file di archivio client (toocluster esterni)                             
* **FileDownload**: l'immagine di avvio di download file di archivio client (toocluster esterni)                             
* **InternalList**: operazione di elenco dei file del client dell'archivio immagini (interno)                             
* **Delete**: operazione di eliminazione del client dell'archivio immagini                              
* **Upload**: operazione di caricamento del client dell'archivio immagini                             
* **NodeControl**: avvio, arresto e riavvio di nodi                             
* **MoveReplicaControl**: spostamento di repliche da un nodo tooanother                             

### <a name="miscellaneous-operations"></a>Operazioni varie
* **Ping**: ping del client                             
* **Query**: tutte le query consentite
* **NameExists**: verifiche dell'esistenza dell'URI di denominazione                             

tipo di controllo di accesso utente Hello è, per impostazione predefinita, toohello limitato le operazioni seguenti: 

* **EnumerateSubnames**: enumerazione dell'URI di denominazione                             
* **EnumerateProperties**: enumerazione delle proprietà di denominazione                             
* **PropertyReadBatch**: operazioni di lettura delle proprietà di denominazione                             
* **GetServiceDescription**: notifiche del servizio di long polling e lettura delle descrizioni dei servizi                             
* **ResolveService**: risoluzione del servizio basata sui reclami                             
* **ResolveNameOwner**: risoluzione del proprietario dei nomi URI                             
* **ResolvePartition**: risoluzione dei servizi di sistema                             
* **ServiceNotifications**: notifiche di servizio basate su eventi                             
* **GetUpgradeStatus**: stato dell'aggiornamento dell'applicazione di polling                             
* **GetFabricUpgradeStatus**: stato dell'aggiornamento del cluster del polling                             
* **InvokeInfrastructureQuery**: attività dell'infrastruttura di esecuzione di query                             
* **List**: operazione di elenco dei file del client dell'archivio immagini                             
* **ResetPartitionLoad**: reimpostazione del carico per un'unità di failover                             
* **ToggleVerboseServicePlacementHealthReporting**: creazione di report sull'integrità del posizionamento dettagliato del servizio                             

controllo dell'accesso amministratore Hello dispone inoltre di accesso toohello operazioni precedenti.

## <a name="changing-default-settings-for-client-roles"></a>Modifica delle impostazioni predefinite per i ruoli del client
Nel file manifesto del cluster di hello, è possibile fornire il client di amministrazione funzionalità toohello se necessario. È possibile modificare le impostazioni predefinite hello passare toohello **le impostazioni dell'infrastruttura** opzione durante [creazione di un cluster](service-fabric-cluster-creation-via-portal.md)e fornendo hello precedenti impostazioni in hello **nome**, **admin**, **utente**, e **valore** campi.

## <a name="next-steps"></a>Passaggi successivi
[Sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md)

[Creazione del cluster di Service Fabric](service-fabric-cluster-creation-via-portal.md)

