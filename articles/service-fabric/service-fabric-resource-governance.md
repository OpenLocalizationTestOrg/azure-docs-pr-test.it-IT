---
title: governance delle risorse dell'infrastruttura di servizio per contenitori e i servizi aaaAzure | Documenti Microsoft
description: Azure Service Fabric consente toospecify i limiti delle risorse per i servizi in esecuzione all'interno o esterno contenitori.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>Governance delle risorse 

Quando si eseguono più servizi hello allo stesso nodo o un cluster, è possibile che un servizio può utilizzare più risorse di memoria destinata altri servizi. Problema di cui viene fatto riferimento tooas hello vicino fastidioso è il problema. Service Fabric consente le prenotazioni di toospecify developer hello e limitazioni per le risorse del servizio tooguarantee e anche di limitare l'utilizzo di risorse. 

## <a name="resource-governance-metrics"></a>Metriche di governance delle risorse 

In Service Fabric la governance delle risorse è supportata per [pacchetto del servizio](service-fabric-application-model.md). risorse Hello assegnati tooService pacchetto possono essere ulteriormente suddivisi tra pacchetti di codice. i limiti delle risorse Hello specificati anche trattarsi di prenotazione hello delle risorse di hello. Service Fabric supporta la specifica di CPU e memoria per pacchetto del servizio mediante due [metriche](service-fabric-cluster-resource-manager-metrics.md) predefinite:

* CPU (nome della metrica `ServiceFabric:/_CpuCores`): un core è un core logico disponibile nel computer host hello e tutti i core in tutti i nodi vengono ponderati hello stesso.
* Memoria (il nome della metrica `ServiceFabric:/_MemoryInMB`): viene eseguito il mapping toophysical memoria disponibile nel computer di hello e memoria viene espressa in megabyte.

Solo le garanzie di riserva soft sono fornite - runtime hello rifiuta l'apertura del nuovo servizio vengono superate le risorse disponibili pacchetti. Tuttavia, se un altro file eseguibile o un contenitore viene posizionato sul nodo hello, che potrebbe violare le garanzie di riserva originale hello.

Per questi due metriche, hello [gestione delle risorse Cluster](service-fabric-cluster-resource-manager-cluster-description.md) tiene traccia delle relative capacità totale del cluster, carico hello in ogni nodo cluster hello, e le risorse cluster hello rimanenti. Questi due metriche sono equivalenti tooany altro utente o una metrica personalizzata e possono utilizzare tutte le funzionalità esistenti:
* Può essere cluster [bilanciato](service-fabric-cluster-resource-manager-balancing.md) in base a metriche toothese due (comportamento predefinito).
* Può essere cluster [deframmentati](service-fabric-cluster-resource-manager-defragmentation-metrics.md) in base a metriche toothese due.
* Quando si [descrive un cluster](service-fabric-cluster-resource-manager-cluster-description.md), è possibile impostare il buffer di capacità per queste due metriche.

La [creazione di report sul carico dinamico](service-fabric-cluster-resource-manager-metrics.md) non è supportata per queste metriche e i relativi carichi vengono definiti al momento della creazione.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Configurazione del cluster per l'abilitazione della governance delle risorse

La capacità deve essere definita manualmente in ogni tipo di nodo nel cluster hello come indicato di seguito:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
La governance delle risorse è consentita solo per i servizi utente, non per qualsiasi servizio di sistema. Quando si specifica la capacità, è necessario lasciare non allocate alcune memorie centrali e parte della memoria per i servizi di sistema. Per prestazioni ottimali, hello dopo l'impostazione deve inoltre essere attivata nel manifesto del cluster hello: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Specifica della governance delle risorse 

I limiti di governance delle risorse vengono specificati nel manifesto dell'applicazione hello (sezione oggetto ServiceManifestImport) come illustrato nell'esempio seguente hello:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
In questo esempio, pacchetto del servizio ServicePackageA Ottiene uno dei core nei nodi hello in cui viene inserito. Questo pacchetto del servizio contiene due pacchetti di codice (CodeA1 e CodeA2) e specificano hello `CpuShares` parametro. percentuale di Hello di CpuShares 512:256 divide core hello tra due pacchetti di codice hello. Pertanto, in questo esempio, CodeA1 Ottiene due terzi di un core e CodeA2 Ottiene un terzo di un core e una prenotazione soft garanzia di hello stesso. Nel caso in cui CpuShares quando non vengono specificati per i pacchetti di codice, Service Fabric divide core hello in modo uniforme tra essi.

I limiti di memoria sono assoluti, in modo che entrambi i pacchetti di codice siano limitate too1024 MB di memoria (e una prenotazione soft garanzia di hello stesso). Pacchetti di codice (contenitori o processi) non sono in grado di tooallocate più memoria rispetto a questo limite e il tentativo di toodo operazione genera un'eccezione di memoria insufficiente. Per risorse limite imposizione toowork, tutti i pacchetti di codice all'interno di un pacchetto del servizio devono avere i limiti di memoria specificati.


## <a name="next-steps"></a>Passaggi successivi
* toolearn più sulla gestione delle risorse Cluster, leggere questo [articolo](service-fabric-cluster-resource-manager-introduction.md).
* toolearn più sul modello di applicazione, pacchetti, pacchetti di codice e toothem le corrispondenze tra le repliche di leggere questo [articolo](service-fabric-application-model.md).
