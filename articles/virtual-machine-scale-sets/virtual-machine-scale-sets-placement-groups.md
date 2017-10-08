---
title: "aaaWorking con grandi set di scalabilità macchina virtuale di Azure | Documenti Microsoft"
description: "È necessario set di scalabilità tooknow toouse grandi dimensioni macchina virtuale di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Uso di set di scalabilità di macchine virtuali di grandi dimensioni
È ora possibile creare Azure [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) con una capacità di backup too1, 000 macchine virtuali. In questo documento, un _set di scalabilità della macchina virtuale di grandi dimensioni_ è definito come un set di scalabilità toogreater di 100 macchine virtuali in grado di supportare di scalabilità. Tale funzionalità è impostata da una proprietà del set di scalabilità (_singlePlacementGroup=False_). 

Alcuni aspetti di su larga scala imposta, ad esempio domini di errore e bilanciamento del carico si comportano in modo diverso tooa scala standard set. Questo documento illustra le caratteristiche di hello del set su larga scala e descrive ciò che si necessario tooknow toosuccessfully usarli nelle applicazioni. 

Un approccio comune per la distribuzione dell'infrastruttura cloud in larga scala è toocreate un set di _unità di scala_, ad esempio ridimensionare set in più reti virtuali e gli account di archiviazione tramite la creazione di più macchine virtuali. Questo approccio fornisce più semplice gestione confrontati toosingle macchine virtuali e più unità di scala sono utili per molte applicazioni, in particolare quelle che richiedono altri componenti duplicabile come più reti virtuali e gli endpoint. Se l'applicazione richiede un singolo cluster di grandi dimensioni, tuttavia, può essere più semplice toodeploy una singola scala di imposta too1, 000 macchine virtuali. Gli scenari di esempio includono distribuzioni centralizzate di Big Data o griglie di calcolo che richiedono una gestione semplice di un esteso pool di nodi di lavoro. Combinata con set di scalabilità della macchina virtuale [i dischi dati collegati](virtual-machine-scale-sets-attached-disks.md), set di scalabilità di grandi dimensioni consentono di toodeploy un'infrastruttura scalabile, composta da migliaia di core e petabyte di spazio di archiviazione, come una singola operazione.

## <a name="placement-groups"></a>Gruppi di posizionamento 
Il modo in cui un _grandi_ set speciale di scalabilità non è il numero di hello di macchine virtuali, ma il numero di hello di _gruppi posizionamento_ contiene. Un gruppo di selezione host è un costrutto simile tooan Azure set di disponibilità, con i propri domini di errore e domini di aggiornamento. Per impostazione predefinita, un set di scalabilità è costituito da un singolo gruppo di posizionamento con una dimensione massima di 100 VM. Se una scala impostata chiamato _singlePlacementGroup_ è impostato too_false_, set di scalabilità hello può essere composto da più gruppi di posizionamento e dispone di un intervallo di 0-1000 macchine virtuali. Impostare quando il valore predefinito toohello di _true_, un set di scalabilità è costituito da un gruppo di selezione host singolo e dispone di un intervallo 0-100 macchine virtuali.

## <a name="checklist-for-using-large-scale-sets"></a>Elenco di controllo per l'uso di set di scalabilità di grandi dimensioni
toodecide se l'applicazione può stabilire un uso efficace di set su larga scala, considerare hello seguenti requisiti:

- I set di scalabilità di grandi dimensioni richiedono Azure Managed Disks. Per i set di scalabilità non creati con Managed Disks sono necessari più account di archiviazione (uno ogni 20 VM). Imposta su larga scala è toowork progettato esclusivamente con i dischi gestiti tooreduce limita il rischio di hello overhead di gestione e tooavoid archiviazione della sottoscrizione per gli account di archiviazione. Se non si utilizzano dischi gestiti, il set di scalabilità è macchine virtuali too100 limitato.
- Set di scalabilità di create da immagini di Azure Marketplace possono applicare la scalabilità verticale too1, 000 macchine virtuali.
- Set di scalabilità di create da immagini personalizzate (immagini di macchina virtuale creare e caricare manualmente) attualmente è possibile ridimensionare le VM too100.
- Livello 4 bilanciamento del carico con hello bilanciamento del carico di Azure non è ancora supportata per i set di scalabilità composti da più gruppi di posizionamento. Se è necessario hello toouse bilanciamento del carico di Azure rendere scala hello che è un gruppo di posizionamento singolo, che è l'impostazione predefinita hello toouse configurato.
- Livello 7 bilanciamento del carico con hello Gateway applicazione Azure è supportata per tutti i set di scalabilità.
- Un set di scalabilità è definito con una sola subnet, verificare che la subnet disponga di uno spazio degli indirizzi sufficiente per tutte le macchine virtuali hello è necessario. Per impostazione predefinita, una scala impostata overprovisions (Crea ulteriori macchine virtuali in fase di distribuzione o quando la scalabilità orizzontale, che non vengono addebitati i) tooimprove distribuzione affidabilità e prestazioni. Consente un maggiore numero hello di macchine virtuali che si prevede di tooscale a indirizzo spazio 20%.
- Se si intende toodeploy più macchine virtuali, i limiti di quota core di calcolo potrebbe essere necessario toobe aumentato.
- I domini di errore e di aggiornamento sono coerenti solo all'interno di un gruppo di posizionamento. Questa architettura non modifica hello complessiva set di disponibilità di una scala, come le macchine virtuali sono distribuite uniformemente tra i componenti hardware fisici distinti, ma non significa che se è necessario tooguarantee due macchine virtuali sono in un hardware diverso, assicurarsi che siano in errore i domini hello nello stesso gruppo di posizionamento. ID gruppo di dominio e il posizionamento di errore vengono visualizzati in hello _Vista istanza_ di scala di una set di VM. È possibile visualizzare visualizzazione hello dell'istanza di un set di scalabilità della macchina virtuale in hello [Esplora inventario risorse di Azure](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Creazione di un set di scalabilità di grandi dimensioni
Quando si crea un set nel portale di Azure hello di scalabilità, è possibile consentirne gruppi di posizionamento toomultiple tooscale dall'impostazione hello _gruppo di selezione host singolo limite tooa_ too_False_ opzione in hello _nozioni di base_ blade. Con too_False_ impostare questa opzione, è possibile specificare un _numero_ valore backup too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

È possibile creare una vasta gamma di macchina virtuale impostata utilizzando hello [CLI di Azure](https://github.com/Azure/azure-cli) _vmss az creare_ comando. Questo comando imposta le impostazioni predefinite intelligenti, ad esempio la dimensione della subnet in base a hello _-conteggio delle istanze_ argomento:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Si noti che hello _vmss creare_ comando per impostazione predefinita di determinati valori di configurazione, se non si specifica. toosee hello opzioni disponibili che è possibile eseguire l'override, provare:
```bash
az vmss create --help
```

Se si sta creando una su larga scala impostata tramite la composizione di un modello di gestione risorse di Azure, assicurarsi che il modello di hello consente di creare un set di scalabilità in base a dischi gestiti di Azure. È possibile impostare hello _singlePlacementGroup_ too_false_ proprietà in hello _proprietà_ sezione di hello _Microsoft.Compute/virtualMAchineScaleSets_ risorse. il frammento JSON seguente Hello viene inizio hello di un modello di set di scalabilità, tra cui la capacità di macchine Virtuali hello 1.000 e hello _"singlePlacementGroup": false_ impostazione:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Per un esempio completo di una vasta gamma di modello di set, fare riferimento troppo[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Conversione di una scala esistente impostare toospan più gruppi di posizionamento
toomake una scalabilità della macchina virtuale esistente definito che consenta di ridimensionamento toomore di 100 macchine virtuali, è necessario hello toochange _singplePlacementGroup_ too_false_ proprietà nella scala hello impostare modello. È possibile verificare la modifica della proprietà con hello [Esplora inventario risorse di Azure](https://resources.azure.com/). Trovare un set scala esistente, selezionare _modifica_ e modificare hello _singlePlacementGroup_ proprietà. Se questa proprietà non viene visualizzata, è possibile che visualizzare hello set di scalabilità con una versione precedente di hello API Microsoft. COMPUTE.

>[!NOTE] 
È possibile modificare un set di supportare una singola posizione gruppo solo (comportamento predefinito di hello) tooa che supporta più gruppi di posizionamento di scalabilità, ma non è possibile convertire hello viceversa. Verificare pertanto che la conoscenza delle proprietà hello dei set di grandi dimensioni prima della conversione. Verificare in particolare, che non è necessario con bilanciamento del carico di Azure hello di bilanciamento del carico di livello 4.


