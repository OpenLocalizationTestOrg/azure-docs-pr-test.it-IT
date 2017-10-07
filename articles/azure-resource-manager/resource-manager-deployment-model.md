---
title: aaaResource gestione e distribuzione classica | Documenti Microsoft
description: Descrive il modello di distribuzione del hello differenze tra modello di distribuzione di gestione risorse di hello e hello classic (o gestione del servizio).
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Gestione risorse di Azure e distribuzione classica: comprendere i modelli di distribuzione e hello lo stato delle risorse
In questo argomento informazioni su Gestione risorse di Azure e i modelli di distribuzione classica, lo stato di hello delle risorse, e il motivo per cui le risorse sono state distribuite con uno o altri hello. Gestione risorse di Hello e modelli di distribuzione classica rappresentano due diversi modi di distribuzione e gestione di soluzioni di Azure. Si lavora con essi tramite due diversi set di API e le risorse di hello distribuito possono contenere importanti differenze. due modelli di Hello non sono completamente compatibili tra loro. Questo argomento descrive tali differenze.

toosimplify hello distribuzione e la gestione delle risorse, Microsoft consiglia di utilizzare Gestione risorse per tutte le risorse di nuovo. e, se possibile, ridistribuire le risorse esistenti con Resource Manager.

Nel caso di nuova tooResource Manager, si consiglia la terminologia di hello revisione toofirst definita in hello [Panoramica di gestione risorse di Azure](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Cronologia di modelli di distribuzione hello
Solo il modello di distribuzione classica hello originariamente fornito da Azure. In questo modello, ogni risorsa esistente in modo indipendente; si è verificato in alcun modo toogroup risorse correlate. In alternativa, è necessario toomanually verificare quali risorse composta da una soluzione o applicazione e ricordare toomanage multipla in un approccio coordinato. toodeploy una soluzione, è necessario tooeither creare ogni risorsa singolarmente tramite portale classico hello o creare uno script che tutte le risorse di hello nell'ordine corretto hello distribuito. toodelete una soluzione, è necessario toodelete ogni risorsa singolarmente. Non era semplice applicare e aggiornare i criteri di controllo di accesso per le risorse correlate. Infine, è Impossibile applicare tag tooresources toolabel con condizioni che consentono di monitorare le risorse e gestire la fatturazione.

In 2014, Azure ha introdotto Gestione risorse, aggiunto il concetto di hello di un gruppo di risorse. Un gruppo di risorse è un contenitore di risorse che condividono un ciclo di vita comune. modello di distribuzione di gestione risorse di Hello offre diversi vantaggi:

* È possibile distribuire, gestire e monitorare tutti i servizi di hello per la soluzione in un gruppo, piuttosto che gestisce i servizi singolarmente.
* È possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente.
* È possibile applicare tooall controllo di accesso alle risorse nel gruppo di risorse, e tali criteri vengono applicati automaticamente quando nuove risorse vengono aggiunti toohello gruppo di risorse.
* È possibile applicare tag tooresources toologically organizzare tutte le risorse di hello nella sottoscrizione.
* È possibile utilizzare l'infrastruttura di hello toodefine JavaScript Object Notation (JSON) per la soluzione. file JSON Hello è noto come un modello di gestione risorse.
* È possibile definire le dipendenze di hello tra risorse e pertanto vengono distribuiti in ordine corretto hello.

Quando si aggiunge, Gestione risorse di tutte le risorse sono stati aggiunti modo retroattivo toodefault gruppi di risorse. Se si crea una risorsa tramite ora distribuzione classica, hello viene automaticamente creata risorsa all'interno di un gruppo di risorse predefinito per tale servizio, anche se non è stato specificato il gruppo di risorse in fase di distribuzione. Tuttavia, solo esistenti all'interno di un gruppo di risorse non significa che risorse hello sono stato convertito toohello Gestione risorse modello. Verrà esaminato il modo in cui ogni servizio gestisce hello due modelli di distribuzione nella sezione successiva hello. 

## <a name="understand-support-for-hello-models"></a>Comprendere i modelli di hello
Quando si decide quale toouse del modello di distribuzione per le risorse, esistono tre scenari toobe, conoscere:

1. servizio Hello supporta Gestione risorse e fornisce un solo tipo.
2. Hello servizio supporta la gestione delle risorse, ma sono disponibili due tipi: uno per Gestione risorse e uno per classica. Questo scenario si applica solo toovirtual macchine, gli account di archiviazione e reti virtuali.
3. servizio Hello non supporta Gestione risorse.

toodiscover indica se un servizio supporta Gestione risorse, vedere [tipi e i provider di risorse](resource-manager-supported-services.md).

Se servizio hello desiderato toouse non supporta la gestione delle risorse, è necessario continuare a usare distribuzione classica.

Se il servizio hello supporta la gestione delle risorse e **non** una macchina virtuale, un account di archiviazione o una rete virtuale, è possibile utilizzare Gestione risorse senza problemi.

Per le macchine virtuali, gli account di archiviazione e reti virtuali, se la risorsa hello è stata creata tramite distribuzione classica, è necessario continuare toooperate su di esso tramite operazioni classiche. Macchina virtuale hello, account di archiviazione o rete virtuale è stato creato tramite la distribuzione di gestione delle risorse, è necessario continuare a usare le operazioni di gestione risorse. Questa distinzione può creare confusione quando la sottoscrizione contiene una combinazione di risorse create con Resource Manager e con la distribuzione classica. Questa combinazione di risorse può produrre risultati imprevisti perché hello risorse non supportano hello stesse operazioni.

In alcuni casi, un comando di gestione delle risorse può recuperare informazioni su una risorsa viene creata attraverso la distribuzione classica o può eseguire un'attività amministrativa, ad esempio lo spostamento di un gruppo di risorse tooanother classico. Tuttavia, questi casi, non concedere impressione hello che tipo di hello supporta operazioni di gestione risorse. Si supponga ad esempio di avere un gruppo di risorse che contiene una macchina virtuale creata con la distribuzione classica. Se si esegue il comando di PowerShell di gestione risorse seguente hello:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Macchina virtuale hello restituisce:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Tuttavia, hello cmdlet di gestione risorse **Get AzureRmVM** restituisce solo le macchine virtuali distribuite tramite Gestione risorse. Hello comando riportato di seguito non riportare hello macchina virtuale viene creata attraverso la distribuzione classica.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Solo le risorse create tramite il tag di supporto di Gestione risorse. Non è possibile applicare tag tooclassic risorse.

## <a name="resource-manager-characteristics"></a>Caratteristiche di Gestione risorse
toohelp comprendere hello due modelli, è opportuno esaminare le caratteristiche di hello dei tipi di gestione risorse:

* Viene creata attraverso la hello [portale di Azure](https://portal.azure.com/).
  
     ![Portale di Azure](./media/resource-manager-deployment-model/portal.png)
  
     Per l'elaborazione, archiviazione e risorse di rete, è possibile hello mediante la distribuzione di gestione risorse o classica. Selezionare **Gestione risorse**.
  
     ![Distribuzione di Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Creato con la versione di hello Gestione risorse di hello cmdlet di Azure PowerShell. Questi comandi hanno formato hello *verbo AzureRmNoun*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Viene creata attraverso la hello [REST API di gestione risorse di Azure](https://docs.microsoft.com/rest/api/resources/) per le operazioni REST.
* Creati tramite i comandi CLI di Azure eseguiti in hello **arm** modalità.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* non include il tipo di risorsa Hello **(classico)** nel nome hello. Hello immagine seguente viene illustrato come tipo di hello **account di archiviazione**.
  
    ![App Web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Caratteristiche della distribuzione classica
Inoltre, si potrebbe sapere il modello di distribuzione classica hello come modello di gestione dei servizi hello.

Risorse create in hello condivisione modello distribuzione classica di hello seguenti caratteristiche:

* Viene creata attraverso la hello [portale classico](https://manage.windowsazure.com)
  
     ![portale classico](./media/resource-manager-deployment-model/classic-portal.png)
  
     In alternativa, hello portale di Azure e si specifica **classico** distribuzione (per il calcolo, archiviazione e rete).
  
     ![Distribuzione classica](./media/resource-manager-deployment-model/select-classic.png)
* Creati tramite una versione di gestione dei servizi hello di hello cmdlet di Azure PowerShell. Questi nomi di comando hanno il formato di hello *verbo AzureNoun*.

  ```powershell
  New-AzureVM
  ```

* Viene creata attraverso la hello [API REST di gestione](https://msdn.microsoft.com/library/azure/ee460799.aspx) per le operazioni REST.
* Risorse create tramite i comandi dell'interfaccia della riga di comando di Azure nella modalità **asm** .

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* tipo di risorsa Hello include **(classico)** nel nome hello. Hello immagine seguente viene illustrato come tipo di hello **account di archiviazione (classico)**.
  
    ![tipo classico](./media/resource-manager-deployment-model/classic-type.png)

È possibile utilizzare le risorse di Azure toomanage portale hello che sono state create tramite distribuzione classica.

## <a name="changes-for-compute-network-and-storage"></a>Cambiamenti a livello di calcolo, rete e archiviazione
Hello seguente diagramma Visualizza le risorse di calcolo, rete e archiviazione distribuite tramite Gestione risorse.

![Architettura di Resource Manager](./media/resource-manager-deployment-model/arm_arch3.png)

Si noti hello segue le relazioni tra le risorse di hello:

* Tutte le risorse di hello esistono all'interno di un gruppo di risorse.
* macchina virtuale Hello dipende da un account di archiviazione specifico definito in hello archiviazione risorse provider toostore i dischi nel blob di archiviazione (obbligatorio).
* macchina virtuale Hello fa riferimento a una scheda di rete specifico definito nel provider di risorse di rete hello (obbligatorio) e un set definito in provider di risorse di calcolo hello (facoltativo) di disponibilità.
* Hello NIC riferimenti hello della macchina virtuale assegnato l'indirizzo IP (obbligatorio), subnet hello della rete virtuale di hello per macchina virtuale hello (obbligatorio) e tooa Network Security Group (facoltativo).
* subnet Hello all'interno di una rete virtuale fa riferimento a un gruppo di sicurezza di rete (facoltativo).
* istanza del servizio di bilanciamento del carico Hello fa riferimento il pool back-end hello di indirizzi IP che includono hello NIC di una macchina virtuale (facoltativa) e fa riferimento a un indirizzo Bilanciamento del carico pubblico o privato IP (facoltativo).

Ecco i componenti di hello e le relative relazioni per la distribuzione classica:

![architettura classica](./media/resource-manager-deployment-model/arm_arch1.png)

Hello soluzione classico per ospitare una macchina virtuale include:

* Un servizio cloud obbligatorio che funge da contenitore per l'hosting di macchine virtuali (calcolo). Le macchine virtuali sono fornite automaticamente con una scheda di rete (NIC) e un indirizzo IP assegnati da Azure. Servizio cloud hello contiene inoltre un'istanza di servizio di bilanciamento del carico esterno, un indirizzo IP pubblico e gli endpoint tooallow remoto remoto e desktop PowerShell traffico predefinita per le macchine virtuali basate su Windows e il traffico di Secure Shell (SSH) per basati su Linux macchine virtuali.
* Un account di archiviazione richiesto che archivi hello dischi rigidi virtuali per una macchina virtuale, inclusi sistema operativo hello, i dischi dati temporanei e aggiuntive (archiviazione).
* Una rete virtuale facoltativa che funge da contenitore aggiuntivo, in cui è possibile creare una struttura di subnet e definire subnet hello in cui hello macchina virtuale si trova (rete).

Hello nella tabella seguente descrive le modifiche in modalità di interazione di provider di risorse di calcolo, rete e archiviazione:

| Elemento | Classico | Gestione risorse |
| --- | --- | --- |
| Servizio cloud per macchine virtuali |Servizio cloud è un contenitore per l'archiviazione di macchine virtuali hello necessari disponibilità dalla piattaforma hello e bilanciamento del carico. |Servizio cloud non è più un oggetto richiesto per la creazione di una macchina virtuale utilizzando il nuovo modello di hello. |
| Reti virtuali |Una rete virtuale è facoltativa per la macchina virtuale hello. Se incluso, la rete virtuale hello non è distribuita con Gestione risorse. |La macchina virtuale richiede una rete virtuale distribuita con Resource Manager. |
| Account di archiviazione |macchina virtuale Hello richiede un account di archiviazione contenente dischi rigidi virtuali hello per sistema operativo hello, i dischi dati temporanei e aggiuntive. |macchina virtuale Hello richiede un toostore di account di archiviazione relativi dischi nell'archiviazione blob. |
| SET DI DISPONIBILITÀ |Piattaforma toohello disponibilità indicata configurando hello stesso "AvailabilitySetName" su hello macchine virtuali. numero massimo di Hello di domini di errore: 2. |Il set di disponibilità è una risorsa esposta dal provider Microsoft.Compute. Macchine virtuali che richiedono un'elevata disponibilità deve essere incluso nel Set di disponibilità hello. numero massimo di Hello di domini di errore è 3. |
| Gruppi di affinità |I gruppi di affinità erano necessari per la creazione di reti virtuali. Tuttavia, con l'introduzione di hello di reti virtuali regionali, che non è stato necessario più. |toosimplify, il concetto di gruppi di affinità hello non esiste in hello API esposte tramite Gestione risorse di Azure. |
| Bilanciamento del carico. |Creazione di un servizio Cloud fornisce un servizio di bilanciamento del carico implicita per hello macchine virtuali distribuite. |Hello bilanciamento del carico è una risorsa esposta dal provider di Microsoft. Network hello. servizio di bilanciamento del carico hello deve fare riferimento ad interfaccia di rete primaria Hello di hello macchine virtuali che deve toobe con carico bilanciato. I servizi di bilanciamento del carico possono essere interni o esterni. Un'istanza del servizio di bilanciamento del carico fa riferimento il pool back-end hello di indirizzi IP che includono hello NIC di una macchina virtuale (facoltativa) e fa riferimento a un indirizzo Bilanciamento del carico pubblico o privato IP (facoltativo). [Per ulteriori informazioni.](../virtual-network/resource-groups-networking.md) |
| Indirizzo IP virtuale |Servizi cloud ottenere un indirizzo VIP predefinito (indirizzo IP virtuale), quando una macchina virtuale viene aggiunto il servizio di cloud tooa. Indirizzo IP virtuale Hello è indirizzo hello associata a bilanciamento del carico implicita hello. |Indirizzo IP pubblico è una risorsa esposta dal provider di Microsoft. Network hello. L’indirizzo IP pubblico può essere statico (riservato) o dinamico. Gli IP pubblici dinamici possono essere assegnati tooa bilanciamento del carico. Gli indirizzi IP pubblici possono essere protetti tramite gruppi di protezione. |
| Indirizzo IP riservato |È possibile riservare un indirizzo IP in Azure e associare con tooensure un servizio Cloud che hello indirizzo IP è permanente. |Indirizzo IP pubblico può essere creato in modalità "Statica" e offerte hello stessa funzionalità come "Indirizzo IP riservato". Gli indirizzi IP pubblici statici può essere solo servizio di bilanciamento del carico tooa ora. |
| Indirizzo IP pubblico per macchina virtuale |Gli indirizzi IP pubblici possono essere associato tooa VM direttamente. |Indirizzo IP pubblico è una risorsa esposta dal provider di Microsoft. Network hello. L’indirizzo IP pubblico può essere statico (riservato) o dinamico. Tuttavia, solo gli IP pubblici dinamici può essere ora tooget di interfaccia di rete tooa assegnato un indirizzo IP pubblico per ogni macchina virtuale. |
| Endpoint |Endpoint di input necessari toobe configurato nel toobe macchina virtuale aprire connettività per determinate porte. Uno dei modi comuni di hello di connessione macchine toovirtual eseguite mediante la configurazione di endpoint di input. |Le regole NAT in ingresso può essere configurate in servizi di bilanciamento del carico tooachieve hello stessa funzionalità dell'abilitazione dell'endpoint su porte specifiche per la connessione delle macchine virtuali toohello. |
| Nome DNS |Un servizio cloud otterrebbe un nome DNS univoco globale implicito. Ad esempio: `mycoffeeshop.cloudapp.net`. |I nomi DNS sono parametri facoltativi che possono essere specificati in una risorsa di indirizzo IP pubblico. Hello FQDN è il seguente hello formato - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfacce di rete |Interfacce di rete primarie e secondarie e le relative proprietà sono state definite come configurazione di rete di una macchina virtuale. |L’interfaccia di rete è una risorsa esposta dal provider Microsoft.Network. ciclo di vita di Hello di hello che interfaccia di rete non è legata tooa macchina virtuale. Fa riferimento indirizzo IP assegnato della macchina virtuale hello (obbligatorio), subnet hello della rete virtuale di hello per macchina virtuale hello (obbligatorio) e tooa Network Security Group (facoltativo). |

toolearn sulla connessione di reti virtuali da modelli di distribuzione diversi, vedere [connettere reti virtuali da diversi modelli di distribuzione nel portale di hello](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Eseguire la migrazione da tooResource classico Manager
Se si è pronti toomigrate le risorse dalla distribuzione classica tooResource deployment Manager, vedere:

1. [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Piattaforma supportata la migrazione delle risorse IaaS da classica tooAzure Gestione risorse](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Eseguire la migrazione di risorse IaaS da tooAzure classico Gestione risorse tramite Azure PowerShell](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Eseguire la migrazione di risorse IaaS da tooAzure classico Resource Manager tramite l'interfaccia CLI di Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Domande frequenti
**È possibile creare una macchina virtuale tramite Gestione risorse di Azure toodeploy in una rete virtuale creata utilizzando la distribuzione classica?**

Questa operazione non è supportata. Non è possibile utilizzare Gestione risorse di Azure toodeploy una macchina virtuale in una rete virtuale che è stata creata utilizzando una distribuzione classica.

**È possibile creare una macchina virtuale utilizzando hello Azure Resource Manager da un'immagine utente creato tramite API di gestione del servizio Azure hello?**

Questa operazione non è supportata. Tuttavia, è possibile copiare i file VHD hello da un account di archiviazione che è stato creato utilizzando hello API gestione dei servizi e aggiungere li tooa nuovo account creato tramite Gestione risorse di Azure.

**Che cos'è l'impatto di hello sulla quota di hello per la sottoscrizione?**

le quote di Hello per le macchine virtuali hello, reti virtuali e account di archiviazione creati tramite hello Azure Resource Manager sono separate da altre quote. Ogni sottoscrizione Ottiene quote toocreate hello risorse usando hello nuove API. Altre informazioni sulle quote aggiuntive hello [qui](../azure-subscription-service-limits.md).

**È possibile continuare toouse gli script automatizzati per il provisioning di macchine virtuali, reti virtuali e gli account di archiviazione tramite le API di gestione risorse di hello?**

Tutti i automazione hello e gli script create continuano toowork per hello macchine virtuali, reti virtuali create in modalità di gestione del servizio Azure hello. Tuttavia, gli script di hello hanno toobe toouse aggiornato hello nuovo schema per la creazione di hello stesse risorse attraverso la modalità di gestione risorse di hello.

**Dove è possibile trovare esempi di modelli di gestione risorse di Azure?**

È possibile trovare un set completo di modelli di base in [Modelli di avvio rapido di Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Passaggi successivi
* toowalk tramite la creazione di hello di modello che definisce una macchina virtuale, account di archiviazione e rete virtuale, vedere [procedura dettagliata di modello di gestione risorse](resource-manager-template-walkthrough.md).
* toosee hello comandi per la distribuzione di un modello, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

