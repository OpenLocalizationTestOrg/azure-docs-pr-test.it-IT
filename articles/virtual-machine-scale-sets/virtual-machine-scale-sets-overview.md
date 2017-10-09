---
title: "scalabilità della macchina virtuale aaaAzure Imposta panoramica | Documenti Microsoft"
description: "Informazioni sui set di scalabilità di macchine virtuali di Azure"
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
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>Informazioni sui set di scalabilità di macchine virtuali in Azure
Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure che è possibile utilizzare toodeploy e gestire un set di macchine virtuali identiche. Con tutte le macchine virtuali configurate hello stesso, set di scalabilità sono scalabilità automatica true toosupport progettato e non pre-provisioning di macchine virtuali è obbligatorio. Pertanto, è più facile servizi su larga scala toobuild destinati a una soluzione big compute, dati e i carichi di lavoro nei contenitori.

Per applicazioni che richiedono risorse di calcolo tooscale in scala e le operazioni sono bilanciate in modo implicito tra i domini di errore e di aggiornamento. Per un ulteriore tooscale introduzione set, vedere toohello [annuncio sul blog di Azure](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Per altre informazioni sui set di scalabilità, guardare questi video:

* [Mark Russinovich talks Azure scale sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/) (Mark Russinovich illustra i set di scalabilità di Azure)  
* [Set di scalabilità di macchine virtuali con Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Creazione e gestione dei set di scalabilità
È possibile creare un set in hello di scalabilità [portale di Azure](https://portal.azure.com) selezionando **nuova** e digitando **scala** sulla barra di ricerca hello. **Set di scalabilità della macchina virtuale** è elencato nei risultati di hello. Da qui, è possibile toocustomize campi hello necessario compilare e distribuire il set di scalabilità. È inoltre opzioni tooset le regole di base di scalabilità automatica in base all'utilizzo della CPU nel portale di hello.

I set di scalabilità possono essere definiti e distribuiti con modelli JSON e [API REST](https://msdn.microsoft.com/library/mt589023.aspx), esattamente come le singole VM di Azure Resource Manager. È quindi possibile usare qualsiasi metodo di distribuzione Azure Resource Manager standard. Per altre informazioni sui modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

È possibile trovare un set di modelli di esempio per la scalabilità della macchina virtuale imposta in hello [repository GitHub modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates). (Cercare modelli con **vmss** nel titolo hello.)

Per esempi di modelli delle Guide rapide di hello, un pulsante "Distribuisci tooAzure" nel file Leggimi di hello per le singole funzionalità di distribuzione del portale toohello collegamenti modello. scala hello toodeploy impostare, fare clic sul pulsante hello e quindi immettere i parametri richiesti nel portale di hello. 

## <a name="scaling-a-scale-set-out-and-in"></a>Aumento e riduzione delle istanze di un set di scalabilità
È possibile modificare la capacità di hello di una scala impostata nel portale di Azure hello facendo hello **Scaling** sezione nel **impostazioni**. 

scala toochange imposta capacità nella riga di comando hello, utilizzare hello **scala** comando [CLI di Azure](https://github.com/Azure/azure-cli). Ad esempio, utilizzare questo tooset comando una capacità di tooa set di scalabilità di macchine 10 virtuali:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

numero di hello tooset di macchine virtuali in una scala impostata per l'utilizzo di PowerShell, usare hello **aggiornamento AzureRmVmss** comando:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

numero di hello tooincrease o diminuzione delle macchine virtuali in una scala impostata utilizzando un modello di gestione risorse di Azure, modificare hello **capacità** proprietà e ridistribuire il modello di hello. Questa semplicità rende facile toointegrate i set di scalabilità con scalabilità automatica di Azure o toowrite che proprio livello di scalabilità personalizzato se gli eventi di scala personalizzata toodefine è necessario che tale funzionalità di Azure non supporta. 

Se si intende ridistribuire una capacità di hello toochange modello Gestione risorse di Azure, è possibile definire un modello molto più piccolo che include solo hello **SKU** pacchetto proprietà con hello aggiornato capacità. Per un esempio, vedere [qui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Autoscale

Un set di scalabilità può essere facoltativamente configurato con impostazioni di scalabilità automatica quando viene creato nel portale di Azure hello. numero di Hello di macchine virtuali possa quindi aumentare o diminuire in base all'utilizzo medio della CPU. 

Molte delle hello ridimensionare il set di modelli in hello [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates) definire impostazioni di scalabilità automatica. È anche possibile aggiungere tooan le impostazioni di scalabilità automatica esistenti di set di scalabilità. Ad esempio, questo script di PowerShell Azure aggiunge set di scalabilità automatica basata sulla CPU tooa scalabilità:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

È disponibile un elenco delle metriche valido tooscale in [metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md) in hello titolo "Microsoft.Compute/virtualMachineScaleSets". Opzioni di scalabilità automatica più avanzate sono inoltre disponibili, tra cui ridimensionamento automatico basato su pianificazione e l'utilizzo di webhook toointegrate con i sistemi di allarme.

## <a name="monitoring-your-scale-set"></a>Monitoraggio del set di scalabilità
Hello [portale di Azure](https://portal.azure.com) elenchi scala imposta e Mostra le relative proprietà. portale Hello supporta anche le operazioni di gestione. che possono essere eseguite sia sui set di scalabilità che sulle singole VM all'interno di un set, portale di Hello offre anche un grafico di utilizzo di risorse personalizzabile. 

Se è necessario toosee o modificare hello sottostante definizione JSON di una risorsa di Azure, è inoltre possibile utilizzare [Esplora inventario risorse di Azure](https://resources.azure.com). Set di scalabilità sono una risorsa con il provider di risorse di Azure a Microsoft. COMPUTE hello. Da questo sito, è possibile visualizzarli espandendo hello seguenti collegamenti:

**Sottoscrizioni** > **sottoscrizione dell'utente** > **Gruppi di risorse** > **Provider** > **Microsoft.Compute** > **virtualMachineScaleSets** > **set di scalabilità dell'utente** > e così via

## <a name="scale-set-scenarios"></a>Scenari dei set di scalabilità
Questa sezione contiene un elenco di alcuni scenari tipici dei set di scalabilità. Questi scenari vengono usati anche da alcuni servizi di Azure di livello superiore, come Batch, Service Fabric e Servizio contenitore.

* **Utilizzare il protocollo RDP o tooconnect tooscale SSH imposta istanze**: viene creato un set di scalabilità all'interno di una rete virtuale e non singole macchine virtuali nel set di scalabilità hello vengono allocate gli indirizzi IP pubblici per impostazione predefinita. Questo criterio consente di evitare spese hello e overhead di gestione di allocazione distinto indirizzo IP pubblico tooall hello nodi il calcolo degli indirizzi. Se è necessario indirizzare le connessioni esterne tooscale imposta macchine virtuali, è possibile configurare una scala set tooautomatically assegnare pubblica IP indirizzi toonew macchine virtuali. In alternativa è possibile connettersi tooVMs da altre risorse nella rete virtuale che può essere allocata gli indirizzi IP pubblici, ad esempio, servizi di bilanciamento del carico e delle macchine virtuali autonome. 
* **Connettersi con le regole NAT tooVMs**: creare un indirizzo IP pubblico, assegnare a tale servizio di bilanciamento del carico tooa e definire un pool NAT in ingresso. Queste azioni mapping delle porte in hello indirizzo IP tooa porta in una macchina virtuale nel set di scalabilità hello. ad esempio:
  
  | Sorgente | Porta di origine | Destination | Porta di destinazione |
  | --- | --- | --- | --- |
  |  IP pubblico |Porta 50000 |vmss\_0 |Porta 22 |
  |  IP pubblico |Porta 50001 |vmss\_1 |Porta 22 |
  |  IP pubblico |Porta 50002 |vmss\_2 |Porta 22 |
  
   In [in questo esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), NAT regole vengono definite tooenable un tooevery di connessione SSH macchina virtuale in un set di scalabilità, utilizzando un singolo indirizzo IP pubblico indirizzo.
  
   [In questo esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) hello stesso con RDP e Windows.
* **Connettersi con una "jumpbox" tooVMs**: se si crea un set di scalabilità e una macchina virtuale autonoma in hello stesso virtuale di rete, hello autonomo macchina virtuale e hello set di scalabilità della macchina virtuale possa connettersi tooone indirizzi di un'altra tramite i relativi IP interno, come definito da hello virtuale rete o subnet. Se si crea un indirizzo IP pubblico e assegnarla a tale macchina virtuale autonoma toohello, è possibile utilizzare il protocollo RDP o SSH tooconnect toohello macchina virtuale autonoma. È quindi possibile connettersi dalla scalabilità della macchina tooyour impostato istanze. Si noterà quindi che un semplice set di scalabilità è intrinsecamente più sicuro di una semplice VM autonoma con un indirizzo IP pubblico nella configurazione predefinita.
  
   [Questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox), ad esempio, distribuisce un set di scalabilità semplice con una VM autonoma. 
* **Il bilanciamento del carico delle istanze di set di tooscale**: se si desidera toodeliver lavoro tooa cluster di calcolo delle macchine virtuali utilizzando un approccio round robin, è possibile configurare un servizio di bilanciamento del carico di Azure con le regole di bilanciamento del carico di livello 4 di conseguenza. È possibile definire probe tooverify che l'applicazione è in esecuzione eseguendo il ping di porte con un protocollo specificato, l'intervallo e percorso della richiesta. Il [gateway applicazione di Azure](https://azure.microsoft.com/services/application-gateway/) supporta anche set di scalabilità, insieme a scenari di bilanciamento del carico più sofisticati e di livello 7.
  
   [In questo esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) crea un set di scalabilità che esegue Server web Apache e Usa un carico di hello toobalance di bilanciamento carico che ogni VM riceve. (Ricercare il tipo di risorsa Microsoft.Network/loadBalancers hello e profilo ed extensionProfile in virtualMachineScaleSet.)

   Questi esempi [Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) e [Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) usano il gateway applicazione.  

* **Distribuzione di un set di scalabilità come cluster di elaborazione in uno strumento di gestione cluster PaaS**: i set di scalabilità sono talvolta descritti come un ruolo di lavoro di prossima generazione. Se una descrizione valida, corre il rischio di hello della scala confusione set di funzionalità con le funzionalità di servizi Cloud di Azure. In un certo senso, i set di scalabilità offrono un effettivo ruolo di lavoro o una risorsa del ruolo di lavoro. Sono una risorsa di calcolo generalizzata indipendente dalla piattaforma o dal runtime, personalizzabile e integrata nel servizio IaaS di Azure Resource Manager.
  
   Un ruolo di lavoro di Servizi cloud è limitato in termini di supporto per la piattaforma o il runtime (sono supportate solo immagini della piattaforma Windows), ma include anche servizi come lo scambio di indirizzi VIP, le impostazioni di aggiornamento configurabili e le impostazioni specifiche della distribuzione del runtime o delle app. Questi servizi non sono *ancora* disponibili nei set di scalabilità o vengono forniti da altri servizi PaaS di livello superiore come Azure Service Fabric. I set di scalabilità possono essere considerati come un'infrastruttura che supporta PaaS. Soluzioni PaaS come [Service Fabric](https://azure.microsoft.com/services/service-fabric/) si basano su questa infrastruttura.
  
   In [questo esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) di questo approccio, [Servizio contenitore di Azure](https://azure.microsoft.com/services/container-service/) distribuisce un cluster basato su set di scalabilità con un agente di orchestrazione contenitore.

## <a name="scale-set-performance-and-scale-guidance"></a>Indicazioni sulla scalabilità e le prestazioni dei set di scalabilità
* Una scala set supporta backup too1, 000 macchine virtuali. Se si crea e carica le immagini VM personalizzate, il limite di hello è 100. Per le considerazioni da tenere presenti per usare set di scalabilità di grandi dimensioni, vedere [Uso di set di scalabilità di macchine virtuali di grandi dimensioni](virtual-machine-scale-sets-placement-groups.md).
* Non è toopre-creare set di scalabilità toouse gli account di archiviazione di Azure. Supporto di set di scalabilità Azure gestito dischi, negare i problemi di prestazioni sul numero di hello dei dischi per ogni account di archiviazione. Per altre informazioni, vedere [Set di scalabilità di macchine virtuali di Azure e dischi gestiti](virtual-machine-scale-sets-managed-disks.md).
* Per tempi di provisioning delle VM più rapidi e prevedibili e prestazioni di I/O migliori, valutare la possibilità di usare Archiviazione Premium di Azure invece di Archiviazione di Azure.
* quota di core Hello in area hello in cui si sta distribuendo limita il numero di hello di macchine virtuali è possibile creare. Potrebbe essere necessario toocontact il supporto tecnico tooincrease il limite di quota di calcolo, anche se si dispone di un limite più elevato di core per l'utilizzo con servizi Cloud di Azure oggi. tooquery la quota, eseguire questo comando CLI di Azure: `azure vm list-usage`. In alternativa, eseguire il comando `Get-AzureRmVMUsage` di PowerShell.

## <a name="frequently-asked-questions-for-scale-sets"></a>Domande frequenti sui set di scalabilità
**D.** Quante VM si possono includere in un set di scalabilità?

**R.** Un set di scalabilità può avere too1 0, 000 macchine virtuali in base alle immagini della piattaforma o in base 0 macchine virtuali too100 immagini personalizzate. 

**D.** I dischi dati sono supportati nei set di scalabilità?

**R.** Sì. Un set di scalabilità è possibile definire una configurazione di dischi dati collegati che si applica tooall macchine virtuali nel set di hello. Per altre informazioni, vedere l'articolo relativo a [set di scalabilità di Azure e dischi dati collegati](virtual-machine-scale-sets-attached-disks.md). Le altre opzioni per l'archiviazione dei dati includono:

* File di Azure (unità condivise SMB)
* Unità del sistema operativo
* Unità temporanea (locale, non supportata da Archiviazione di Azure)
* Servizio dati di Azure (ad esempio, tabelle di Azure e BLOB di Azure)
* Servizio dati esterno (ad esempio, un database remoto)

**D.** Quali aree di Azure supportano i set di scalabilità?

**R.** Tutte le aree supportano i set di scalabilità.

**D.** Come si crea un set di scalabilità con un'immagine personalizzata?

**R.** Creare un disco gestito basato sul disco rigido virtuale dell'immagine personalizzata e fare riferimento a tale disco gestito nel modello del set di scalabilità. Per un esempio, vedere [qui](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**D.** Se riduce la scala, imposta la capacità too15 20, che vengono rimosse le macchine virtuali?

**R.** Macchine virtuali vengono rimosse dalla scala hello impostate in modo uniforme in tutti i domini di aggiornamento e la disponibilità di toomaximize domini di errore. Macchine virtuali con hello che ID più alto verranno rimosse per prime.

**D.** Se quindi aumentare la capacità di hello da 15 too18?

**R.** Se si aumenta la capacità too18, vengono create 3 nuove macchine virtuali. Ogni volta, ID di istanza VM hello viene incrementato a hello più elevato del valore precedente (ad esempio, 20, 21, 22). Le VM vengono bilanciate tra domini di errore e domini di aggiornamento.

**D.** Quando si usano più estensioni in un set di scalabilità, è possibile imporre una sequenza di esecuzione?

**R.** Non direttamente, ma per l'estensione customScript hello, lo script può attendere da un'altra estensione toofinish. È possibile ottenere informazioni aggiuntive in sequenza di estensione nel post di blog hello [la sequenza di estensione nel set di scalabilità di macchine Virtuali di Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**D.** I set di scalabilità si integrano con i set di disponibilità di Azure?

**R.** Sì. Un set di scalabilità è un set di disponibilità implicito con 5 domini di errore e 5 domini di aggiornamento. Scala sono estese a più set di macchine virtuali di più di 100 *gruppi posizionamento*, che sono equivalenti toomultiple set di disponibilità. Per altre informazioni sui gruppi di posizionamento, vedere [Uso di set di scalabilità di macchine virtuali di grandi dimensioni](virtual-machine-scale-sets-placement-groups.md). Può esistere un set di disponibilità delle macchine virtuali in hello stessa rete virtuale come un set di scalabilità di macchine virtuali. Una configurazione comune è tooput controllo macchine virtuali del nodo (che richiedono spesso una configurazione univoca) in un disponibilità impostata e inserire nodi di dati in set di scalabilità hello.

È possibile trovare ulteriori risposte tooquestions sulla scalabilità imposta in hello [scalabilità della macchina virtuale Azure imposta domande frequenti su](virtual-machine-scale-sets-faq.md).
