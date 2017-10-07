---
title: aaa "Creazione di un pool di Azure Batch evento | Documenti di Microsoft"
description: "Riferimento per l’evento di creazione del pool di batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Evento di creazione di pool

 Questo evento viene generato dopo aver creato un pool. il contenuto di Hello del Registro di hello espone informazioni generali sul pool hello. Si noti che se la dimensione di destinazione hello del pool di hello è maggiore di 0 nodi di calcolo, un evento di avvio del ridimensionamento pool seguirà immediatamente dopo questo evento.

 Hello seguente illustra il corpo di hello di un pool di creare un evento per un pool creato utilizzando proprietà CloudServiceConfiguration hello.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Note|
|-------------|----------|-----------|
|id|String|id di Hello del pool di hello.|
|displayName|String|nome del pool di hello è visualizzato Hello.|
|vmSize|String|dimensioni Hello di hello le macchine virtuali in pool hello. Tutte le macchine virtuali in un pool sono hello stessa dimensione. <br/><br/> Per informazioni sulle dimensioni disponibili per le macchine virtuali per i pool dei Servizi cloud (pool creati con cloudServiceConfiguration), vedere [Dimensioni dei servizi Cloud](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Batch supporta tutte le dimensioni delle VM dei Servizi cloud, ad eccezione di `ExtraSmall`.<br/><br/> Per informazioni sulla macchina virtuale a disponibilità vedere dimensioni per i pool di utilizzo di immagini da hello Marketplace di macchine virtuali (pool creati con virtualMachineConfiguration) [dimensioni per le macchine virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) o [dimensioni per Macchine virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Batch supporta tutte le dimensioni delle VM di Azure tranne `STANDARD_A0` e quelle con l'archiviazione Premium (serie `STANDARD_GS`, `STANDARD_DS` e `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Tipo complesso|configurazione del servizio cloud Hello per pool hello.|
|[virtualMachineConfiguration](#bk_vmconf)|Tipo complesso|configurazione della macchina virtuale Hello per pool hello.|
|[networkConfiguration](#bk_netconf)|Tipo complesso|configurazione di rete Hello per pool hello.|
|resizeTimeout|Tempo|Hello timeout per l'allocazione del pool di toohello nodi di calcolo specificato per l'operazione di ridimensionamento sul pool hello ultimo hello.  (Buongiorno iniziale ridimensionamento quando si crea i conteggi come un ridimensionamento pool di hello).|
|targetDedicated|Int32|numero di Hello di nodi di calcolo che sono richieste per il pool di hello.|
|enableAutoScale|Booleano|Specifica se le dimensioni del pool di hello viene ridimensionato automaticamente nel corso del tempo.|
|enableInterNodeCommunication|Booleano|Specifica se il pool di hello è configurato per la comunicazione diretta tra i nodi.|
|isAutoPool|Booleano|Specifica se il pool di hello è stato creato tramite il meccanismo di pool automatico di un processo.|
|maxTasksPerNode|Int32|numero massimo di Hello di attività che è possibile eseguire contemporaneamente in un singolo nodo di calcolo nel pool di hello.|
|vmFillType|String|Definisce come hello servizio Batch distribuisce le attività tra i nodi di calcolo nel pool di hello. I valori validi sono Spread o Pack.|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|osFamily|String|Hello del sistema operativo Guest Azure famiglia toobe installato nelle macchine virtuali hello nel pool di hello.<br /><br /> I valori possibili sono:<br /><br /> **2** – 2 famiglia del sistema operativo, tooWindows equivalente Server 2008 R2 SP1.<br /><br /> **3** : famiglia di sistemi operativi 3, equivalente tooWindows Server 2012.<br /><br /> **4** – 4 famiglia del sistema operativo, tooWindows equivalente Server 2012 R2.<br /><br /> Per altre informazioni, vedere [Rilasci del sistema operativo guest Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|String|Hello toobe di versione del sistema operativo Guest Azure installato nelle macchine virtuali hello nel pool di hello.<br /><br /> valore predefinito di Hello è  **\***  che specifica di versione del sistema operativo più recente di hello per hello specificato famiglia.<br /><br /> Per altri valori consentiti, vedere [Rilasci del sistema operativo guest Azure ](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Tipo complesso|Specifica informazioni sulla piattaforma hello o toouse immagine Marketplace.|
|nodeAgentSKUId|String|Hello SKU dell'agente di nodo hello Batch eseguito il provisioning nel nodo di calcolo hello.|
|[windowsConfiguration](#bk_winconf)|Tipo complesso|Specifica impostazioni del sistema operativo Windows nella macchina virtuale hello. Questa proprietà non deve essere specificato se hello imageReference fa riferimento a un'immagine del sistema operativo Linux.|

###  <a name="bk_imgref"></a> imageReference

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|publisher|String|server di pubblicazione Hello dell'immagine di hello.|
|offer|String|offerta Hello dell'immagine di hello.|
|sku|String|Hello SKU dell'immagine di hello.|
|version|String|versione di Hello dell'immagine di hello.|

###  <a name="bk_winconf"></a> windowsConfiguration

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|enableAutomaticUpdates|Boolean|Indica se macchina virtuale hello è abilitato per gli aggiornamenti automatici. Se questa proprietà non è specificata, il valore predefinito di hello è true.|

###  <a name="bk_netconf"></a> networkConfiguration

|Nome dell'elemento|Tipo|Note|
|------------------|--------------|----------|
|subnetId|String|Specifica l'identificatore di risorsa di hello della subnet hello nel calcolo del pool che hello nodi vengono creati.|
