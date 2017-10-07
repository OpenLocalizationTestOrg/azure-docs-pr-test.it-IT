---
title: aaaService gestione delle risorse dell'infrastruttura Cluster - criteri di posizionamento | Documenti Microsoft
description: Panoramica su altre politiche e regole per i servizi di Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>Criteri di posizionamento per i servizi di Service Fabric
Criteri di posizionamento sono regole aggiuntive che possono essere utilizzati toogovern posizione del servizio in alcuni scenari specifici, meno comuni. Alcuni esempi di questi scenari sono:

- Il cluster di Service Fabric si estende nelle distanze geografiche, come più data center locali o in diverse aree di Azure
- L'ambiente si estende su più aree di controllo di natura geopolitica o legale o un altro caso in cui si dispone dei limiti dei criteri è necessario tooenforce
- Vi sono considerazioni sulle prestazioni o latenza comunicazioni scadenza toolarge distanze o l'utilizzo di collegamenti di rete lenta o meno affidabile
- È necessario tookeep determinati carichi di lavoro con condivisione percorso come sforzo, con altri carichi di lavoro o in prossimità toocustomers

La maggior parte di questi requisiti si allineano ai layout fisico di hello del cluster di hello, rappresentati come hello domini di errore del cluster di hello. 

Hello avanzata dei criteri di posizionamento che consentono di risolvere che questi scenari sono:

1. Domini non validi
2. Domini obbligatori
3. Domini preferiti
4. Divieto di compressione della replica

La maggior parte dei seguenti controlli hello è stato possibile configurare le proprietà di nodo e i vincoli di posizionamento, ma alcune sono più complesse. toomake cose più semplici, hello gestione delle risorse Cluster dell'infrastruttura del servizio fornisce questi criteri di posizionamento aggiuntivo. I criteri di posizionamento sono configurati in una base all'istanza singola del servizio. Possono anche essere aggiornati in modo dinamico.

## <a name="specifying-invalid-domains"></a>Specifica di domini non validi
Hello **InvalidDomain** toospecify che un particolare dominio di errore non è valido per uno specifico servizio consentono criteri di selezione. Questo criterio garantisce che un particolare servizio non sia mai eseguito in una determinata area, ad esempio per motivi geopolitici o criteri aziendali. È possibile specificare più domini non validi tramite criteri separati.

<center>
![Esempio di dominio non valido][Image1]
</center>

Codice:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Specifica dei domini obbligatori
Hello necessari criteri di posizionamento di dominio richiedono che il servizio di hello è presente solo nel dominio specificato hello. È possibile specificare più domini richiesti tramite criteri separati.

<center>
![Esempio di dominio obbligatorio][Image2]
</center>

Codice:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Specificare un dominio preferito per le repliche primarie hello di un servizio con stato
Dominio primario preferito Hello specifica hello errore dominio tooplace hello primario. Hello primario finisce in questo dominio quando tutto è integro. Se il dominio hello o la replica primaria hello ha esito negativo o viene chiuso, hello primario Sposta toosome altra posizione, idealmente in hello nello stesso dominio. Se non è il nuovo percorso nel dominio preferito hello, hello gestione delle risorse Cluster passa nuovamente dominio preferito toohello appena possibile. Naturalmente questa impostazione è adatta solo ai servizi con stati. Questo criterio è particolarmente utile in cluster distribuiti tra più data center o aree di Azure, ma hanno dei data center che preferiscono la collocazione in una determinata posizione. Conservazione primari chiudere tootheir utenti o altri servizi consente di fornire una latenza più bassa, in particolare per le letture, che sono gestite da componenti primari, per impostazione predefinita.

<center>
![Failover e domini primari preferiti][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Necessità di distribuzione della replica e divieto di compressione
Le repliche sono _normalmente_ distribuiti in domini di errore e di aggiornamento quando hello cluster è integro. Tuttavia, vi sono casi in cui più di una replica per una determinata partizione rischia di essere temporaneamente compressa in un singolo dominio. Ad esempio, supponiamo che tale cluster hello dispone di nove nodi in tre domini di errore, fd: / 0, fd: / 1 e fd: / 2. Si supponga anche che il servizio disponga di tre repliche. Si supponga che hello nodi che sono stati utilizzati per le repliche in fd: / 1 e fd: / 2 si è arrestato. In genere hello gestione delle risorse Cluster preferisce altri nodi in tali domini di errore stesso. In questo caso, si supponga che a causa di problemi toocapacity nessuno di hello altri nodi in tali domini sono valide. Se Gestione delle risorse Cluster hello compilazioni sostituzioni per tali repliche, avrebbe toochoose nodi in fd: / 0. Tuttavia, in questo _che_ crea una situazione in cui viene violata hello vincolo di dominio di errore. Compressione aumenta repliche probabilità hello che hello set di repliche intero Impossibile inattività o persi. 

> [!NOTE]
> Per altre informazioni sui vincoli e sulle priorità dei vincoli in generale, vedere [questo argomento](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Se viene visualizzato un messaggio di integrità come "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", allora si verifica questa condizione o una condizione simile. In genere solo una o due repliche vengono compresse insieme temporaneamente. Finché sono presenti meno di un quorum di repliche in un dominio specifico, si è sicuri. Compressione rara, ma può verificarsi, e in genere, queste situazioni sono temporanee poiché i nodi di hello tornare. Se i nodi di hello rimanere verso il basso e hello gestione delle risorse Cluster deve toobuild sostituzioni, in genere sono disponibili altri nodi in domini di errore ideale di hello.

Alcuni carichi di lavoro preferiscono sempre con numero di destinazione hello di repliche, anche se essi vengono compressi in un minor numero di domini. Questi carichi di lavoro puntano contro la presenza di errori di dominio permanenti totali e simultanei e in genere sono in grado di ripristinare lo stato locale. Altri carichi di lavoro invece richiede tempi di inattività hello precedenti a correttezza rischio o perdita di dati. La maggior parte dei carichi di lavoro di produzione viene eseguita con più di tre repliche, più di tre domini di errore e numerosi nodi validi per ogni dominio di errore. Per questo motivo, hello predefinito che consente la compressione di dominio per impostazione predefinita. comportamento predefinito di Hello consente normale di bilanciamento del carico e failover toohandle questi casi estremi, anche se ciò significa che la compressione dominio temporaneo.

Se si desidera toodisable tale compressione per un determinato carico di lavoro, è possibile specificare hello `RequireDomainDistribution` criteri sul servizio hello. Quando questo criterio è impostato, hello gestione delle risorse Cluster non garantisce alcun due repliche da hello stessa partizione eseguiti in hello stesso errore o di dominio di aggiornamento.

Codice:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

A questo punto, sarebbe possibile toouse possibili queste configurazioni per i servizi in un cluster che non è stato geograficamente occupate? È possibile, ma non ce n'è motivo. Hello configurazioni di dominio richiesto non valido e Preferiti devono essere evitate a meno che non li richiedono scenari hello. Può non essere qualsiasi tooforce tootry senso toorun un determinato carico di lavoro in un singolo rack tooprefer alcuni segmenti del cluster locale rispetto a un altro. È necessario distribuire diverse configurazioni hardware tra i domini di errore e gestirle tramite normali vincoli di posizionamento e proprietà dei nodi.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
