---
title: Cluster Resource Manager di Service Fabric - Costo dello spostamento | Microsoft Docs
description: Panoramica del costo di spostamento per i servizi di Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Costo di spostamento dei servizi
Un fattore che hello gestione delle risorse Cluster dell'infrastruttura del servizio prende in considerazione durante il tentativo toodetermine quali cluster tooa toomake di modifiche è il costo di hello di tali modifiche. il concetto di Hello "costo" verrà scambiato con quanti cluster hello possono essere migliorate. Il factoring del costo avviene durante lo spostamento di servizi di bilanciamento del carico, la deframmentazione e altri requisiti. obiettivo di Hello è requisiti hello toomeet hello almeno modo dannose o costosa. 

Lo spostamento dei servizi comporta costi, come minimo in termini di tempo della CPU e ampiezza di banda della rete. Per i servizi con stati, è necessario copiando hello stato di tali servizi, utilizzo disco e memoria aggiuntiva. Ridurre il costo di hello di soluzioni che hello gestione delle risorse Cluster di Azure Service Fabric è dotato della contribuisce a garantire che le risorse del cluster di hello non impiegate inutilmente. Tuttavia, non si desideri tooignore soluzioni che possono migliorare notevolmente allocazione hello di risorse cluster hello.

Gestione delle risorse Cluster Hello ha due modalità di calcolo dei costi e servirsi mentre tenta di cluster hello toomanage. primo meccanismo Hello è semplicemente il conteggio ogni spostamento che renderebbe. Se vengono generate due soluzioni con hello stesso bilancia (punteggio), quindi hello gestione delle risorse Cluster preferito hello uno con costo più basso (numero totale degli spostamenti) hello.

Questa strategia funziona bene. Ma come con i carichi predefiniti o statici, è improbabile che in qualsiasi sistema complesso tutti gli spostamenti siano uguali. Alcuni sono probabilmente toobe molto più costoso.

## <a name="setting-move-costs"></a>Impostazione dei costi di spostamento 
Quando viene creato, è possibile specificare hello costo predefinito dello spostamento di un servizio:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

È anche possibile specificare o aggiornare in modo dinamico MoveCost per un servizio dopo aver creato il servizio hello: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Specificare in modo dinamico il costo di spostamento su base di replica

Hello frammenti di codice precedente sono tutti per specificare MoveCost per un intero servizio contemporaneamente dal servizio esterno hello stesso. Tuttavia, spostare il costo è più utile è quando cambia costo di spostamento hello di un oggetto servizio specifico per la sua durata. Poiché hello servizi probabilmente che hello migliore di come costose sono toomove un determinato momento, è un'API per servizi tooreport i propri singolo spostamento dei costi in fase di esecuzione. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Impatto del costo di spostamento
MoveCost ha quattro livelli: Zero, Low, Medium e High. MoveCosts sono relativo tooeach altri, ad eccezione di Zero. Costo pari a zero spostamento significa che lo spostamento è gratuito e deve non inclusi nel conteggio per il punteggio di hello della soluzione hello. Impostazione Sposta costo tooHigh *non* garantisce che la replica hello rimane in un'unica posizione.

<center>
![Costo di spostamento come fattore da considerare per la selezione delle repliche da spostare][Image1]
</center>

MoveCost consente di individuare soluzioni hello che causa hello complessiva di un'interruzione minima del e è ancora che pervengono a bilanciare equivalente tooachieve più semplice. Nozione di un servizio di costo può essere di tipo toomany relativo. Hello più comuni per il calcolo del costo di spostamento sono fattori:

- quantità di Hello di dati che il servizio di hello è toomove o dello stato.
- costo di Hello di disconnessione dei client. Lo spostamento di una replica primaria è in genere più costoso costo hello dello spostamento di una replica secondaria.
- costo di Hello di interrompere un'operazione in corso. Alcune operazioni dati hello archiviano livello o operazioni eseguite nella chiamata di risposta tooa client sono dispendiose. Dopo un certo punto, non si desidera toostop, se non è necessario. In modo durante l'operazione di hello in corso, aumento dei costi di spostamento hello di probabilità hello tooreduce oggetto servizio che si sposta. Al termine dell'operazione di hello, impostare hello costo indietro toonormal.

## <a name="enabling-move-cost-in-your-cluster"></a>Abilitazione del costo di spostamento del cluster
Affinché hello più granulare MoveCosts toobe, prendere in considerazione, MoveCost deve essere abilitata nel cluster. Senza questa impostazione, modalità predefinita di hello del conteggio spostamenti viene utilizzata per calcolare MoveCost e MoveCost report vengono ignorati.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Passaggi successivi
- Gestore di risorse Cluster dell'infrastruttura del servizio utilizza consumo toomanage metriche e la capacità in cluster hello. ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [consumo delle risorse di gestione e il carico in Service Fabric con le metriche](service-fabric-cluster-resource-manager-metrics.md).
- toolearn sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, estrarre [bilanciamento del carico del cluster di Service Fabric](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
