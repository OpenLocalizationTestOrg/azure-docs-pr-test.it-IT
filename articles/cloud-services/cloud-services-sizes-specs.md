---
title: le dimensioni delle macchine aaaVirtual per i servizi Cloud di Azure | Documenti Microsoft
description: Vengono elencate le dimensioni di macchina virtuale diversa hello (ID) per ruoli web e di lavoro del servizio cloud di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Dimensioni dei servizi cloud
Questo argomento descrive le dimensioni disponibili hello e le opzioni per le istanze del ruolo del servizio Cloud (ruoli web e ruoli di lavoro). Fornisce inoltre toobe considerazioni sulla distribuzione conoscere quando si pianifica toouse queste risorse. Ogni dimensione dispone di un ID da inserire nel [file di definizione del servizio](cloud-services-model-and-package.md#csdef). I prezzi per ogni dimensione sono disponibili sul hello [prezzi servizi Cloud](https://azure.microsoft.com/pricing/details/cloud-services/) pagina.

> [!NOTE]
> toosee correlati i limiti di Azure, vedere [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Dimensioni delle istanze del ruolo Web e di lavoro
Non sono presenti più dimensioni standard toochoose da in Azure. Si tengano presenti le considerazioni seguenti per alcune di queste dimensioni:

* Macchine virtuali serie D sono progettate toorun applicazioni che richiedono maggiore potenza di calcolo e le prestazioni del disco temporaneo. Macchine virtuali serie D offrono processori più veloci, un rapporto memoria-core superiore e un'unità SSD (unità SSD) per il disco temporaneo hello. Per informazioni dettagliate, vedere annuncio hello sul blog di Azure, hello [nuove dimensioni delle macchine virtuali di serie D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Dv2-series, un toohello successivi serie D originale, dotato di una CPU più potente. Hello Dv2 serie CPU è circa 35% più rapida rispetto hello serie D CPU. Si basa su hello ultima generazione 2,4 GHz Intel Xeon® E5-2673 v3 processore (Haswalle) e con hello Intel turbina Boost tecnologia 2.0, possono aumentare fino too3.1 GHz. Hello Dv2 serie è hello stesse configurazioni di memoria e disco come hello serie D.
* Macchine virtuali serie G offrono hello maggior quantità di memoria ed eseguiti su host che dispongono di processori della famiglia Intel Xeon E5 V3.
* Hello macchine virtuali serie può essere distribuito in vari tipi di hardware e i processori. dimensioni Hello sono limitata, in base hello hardware, le prestazioni del processore coerente toooffer per hello in esecuzione l'istanza, indipendentemente dall'hardware hello in che viene distribuita. toodetermine hello hardware fisico in cui viene distribuita questa dimensione, query hello hardware virtuale all'interno di hello macchina virtuale.
* dimensione A0 Hello è eccessiva sottoscritto nell'hardware fisico hello. Per queste dimensioni specifiche, altre distribuzioni dei clienti possono rallentare le prestazioni di hello del carico di lavoro in esecuzione. prestazioni relative di Hello viene indicata di seguito come linea di base hello previsto, la variabilità approssimativo soggetto tooan del 15%.

le dimensioni di Hello della macchina virtuale hello influiscono sui prezzi hello. dimensioni di Hello influiscono inoltre sulla capacità di elaborazione, memoria e archiviazione hello della macchina virtuale hello. I costi di archiviazione vengono calcolati separatamente in base alle pagine usate nell'account di archiviazione hello. Per informazioni dettagliate, vedere i [dettagli sui prezzi dei servizi cloud](https://azure.microsoft.com/pricing/details/cloud-services/) e [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).

Hello seguenti considerazioni potrebbe consentire di decidere la dimensione:

* Hello dimensioni A8 A11 e H serie sono noti anche come *istanze con utilizzo intensivo di calcolo*. progettato e ottimizzato per un utilizzo intensivo di calcolo hardware Hello che esegue queste dimensioni e applicazioni a elevato utilizzo di rete, calcolo ad alte prestazioni (HPC) tra cluster di applicazioni, modellazione e simulazioni. Hello A8 A11 serie utilizza Intel Xeon E5-2670 2,6 GHz e hello H serie utilizza 2667 con Intel Xeon E5 v3 @ 3,2 GHz. Per informazioni e considerazioni dettagliate sull'uso di queste dimensioni, vedere [Dimensioni delle VM High Performance Computing (HPC)](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* La serie Dv2, D e G sono ideali per le applicazioni che richiedono CPU più veloci, prestazioni migliori del disco locale o requisiti di memoria superiori. Offrono una potente combinazione per molte applicazioni di livello aziendale.
* Alcuni degli host fisici di hello in data center di Azure potrebbero non supportare macchine virtuali dimensioni superiori, ad esempio dalla A5 A11. Di conseguenza, venga visualizzato il messaggio di errore hello **macchina virtuale tramite tooconfigure Failed {nome}** o **macchina virtuale tramite toocreate Failed {nome}** quando si ridimensiona un tooa macchina virtuale esistente nuovo dimensioni. creazione di una nuova macchina virtuale in una rete virtuale creata prima del 16 aprile 2013; o l'aggiunta di un nuova macchina virtuale tooan servizio cloud esistente. Vedere [errore: "Macchina virtuale di tooconfigure non riuscito"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) sul forum di supporto hello per soluzioni alternative per ogni scenario di distribuzione.
* La sottoscrizione anche potrebbe limitare il numero di hello di core, che è possibile distribuire in determinati gruppi di dimensioni. tooincrease una quota, contattare il supporto tecnico di Azure.

## <a name="performance-considerations"></a>Considerazioni sulle prestazioni
È stato creato il concetto di hello di hello Azure Compute Unit (ACU) tooprovide un modo per confrontare le prestazioni di calcolo (CPU) in SKU di Azure e tooidentify che SKU è probabilmente toosatisfy le prestazioni è necessario.  L'unità ACU adotta come standard una macchina virtuale Small (Standard_A1), a cui attribuisce il valore 100. Per tutte le altre SKU sarà quindi possibile valutare la maggiore velocità di elaborazione con cui sono in grado di eseguire un benchmark standard.

> [!IMPORTANT]
> Hello ACU è solo un'indicazione. Hello risultati per il carico di lavoro possono variare.
>
>

<br>

| Famiglia SKU | ACU/Core |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Small-ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

ACUs contrassegnati con un * utilizzare frequenza tooincrease CPU di tecnologia Intel® turbina e fornire un incremento delle prestazioni. Hello quantità di incremento hello può variare in base alle dimensioni della macchina virtuale hello, carico di lavoro e altri carichi di lavoro in esecuzione su hello stesso host.

## <a name="size-tables"></a>Tabelle delle dimensioni
Hello tabelle seguenti illustrano le dimensioni di hello e forniscono capacità di hello.

* La capacità di archiviazione viene visualizzata in unità di GiB o 1.024^3 byte. Quando il confronto dei dischi espresso in GB (1000 ^ 3 byte) toodisks misurata in GiB (1024 ^ 3) tenere presente che i numeri di capacità specificati in GiB potrebbero apparire più piccoli. Ad esempio, 1.023 GiB = 1.098,4 GB
* La velocità effettiva del disco viene misurata in operazioni di input/output al secondo (IOPS) e MBps, dove il valore di MBps corrisponde a 10^6 byte al secondo.
* I dischi dati possono operare in modalità memorizzata nella cache o non memorizzata nella cache. Per l'operazione del disco dati memorizzati nella cache, la modalità cache di hello host è troppo**ReadOnly** o **ReadWrite**. Per l'operazione del disco dati non memorizzato nella cache, la modalità cache di hello host è impostata troppo**Nessuno**.
* Larghezza di banda massima è hello aggregati larghezza di banda massima allocata e assegnato al tipo di macchina virtuale. larghezza di banda massima Hello fornisce indicazioni per la selezione di hello destra VM tipo tooensure sufficiente capacità della rete sono disponibile. Quando si passa da bassa, moderata, ad alta e molto elevato, la velocità effettiva hello aumenta di conseguenza. Le prestazioni di rete effettive dipenderanno da molti fattori, tra cui carichi di rete e dell'applicazione e le impostazioni di rete dell'applicazione.

## <a name="a-series"></a>Serie A
| Dimensione            | Core CPU | Memoria: GiB  | Unità HDD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Molto piccola      | 1         | 0,768        | 20                   | 1/bassa |
| Small           | 1         | 1,75         | 225                  | 1/moderata |
| Media          | 2         | 3,5 GB       | 490                  | 1/moderata |
| Large           | 4         | 7            | 1000                 | 2/alta |
| Molto grande      | 8         | 14           | 2040                 | 4/alta |
| A5              | 2         | 14           | 490                  | 1/moderata |
| A6              | 4         | 28           | 1000                 | 2/alta |
| A7              | 8         | 56           | 2040                 | 4/alta |

## <a name="a-series---compute-intensive-instances"></a>Serie A - Istanze a elevato utilizzo di calcolo
Per informazioni e considerazioni sull'uso di queste dimensioni, vedere [Dimensioni delle VM High Performance Computing (HPC)](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Dimensione            | Core CPU | Memoria: GiB  | Unità HDD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2/alta |
| A9*             |16         | 112          | 1817                 | 4/molto alta |
| A10             |8          | 56           | 1817                 | 2/alta |
| A11             |16         | 112          | 1817                 | 4/molto alta |

\*Con supporto di RDMA

## <a name="av2-series"></a>Serie Av2

| Dimensione            | Core CPU | Memoria: GiB  | Unità SSD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1/moderata                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2/moderata                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4/alta                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8/alta                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2/moderata                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4/alta                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8/alta                     |


## <a name="d-series"></a>Serie D
| Dimensione            | Core CPU | Memoria: GiB  | Unità SSD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3,5          | 50                   | 1/moderata |
| Standard_D2     | 2         | 7            | 100                  | 2/alta |
| Standard_D3     | 4         | 14           | 200                  | 4/alta |
| Standard_D4     | 8         | 28           | 400                  | 8/alta |
| Standard_D11    | 2         | 14           | 100                  | 2/alta |
| Standard_D12    | 4         | 28           | 200                  | 4/alta |
| Standard_D13    | 8         | 56           | 400                  | 8/alta |
| Standard_D14    | 16        | 112          | 800                  | 8/molto alta |

## <a name="dv2-series"></a>Serie Dv2
| Dimensione            | Core CPU | Memoria: GiB  | Unità SSD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1/moderata |
| Standard_D2_v2  | 2         | 7            | 100                  | 2/alta |
| Standard_D3_v2  | 4         | 14           | 200                  | 4/alta |
| Standard_D4_v2  | 8         | 28           | 400                  | 8/alta |
| Standard_D5_v2  | 16        | 56           | 800                  | 8/estremamente alta |
| Standard_D11_v2 | 2         | 14           | 100                  | 2/alta |
| Standard_D12_v2 | 4         | 28           | 200                  | 4/alta |
| Standard_D13_v2 | 8         | 56           | 400                  | 8/alta |
| Standard_D14_v2 | 16        | 112          | 800                  | 8/estremamente alta |
| Standard_D15_v2 | 20        | 140          | 1.000                | 8/estremamente alta |

## <a name="g-series"></a>Serie G
| Dimensione            | Core CPU | Memoria: GiB  | Unità SSD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1/alta |
| Standard_G2     | 4         | 56           | 768                  |2/alta |
| Standard_G3     | 8         | 112          | 1.536                |4/molto alta |
| Standard_G4     | 16        | 224          | 3.072                |8/estremamente alta |
| Standard_G5     | 32        | 448          | 6.144                |8/estremamente alta |

## <a name="h-series"></a>Serie H
Macchine virtuali di Azure H serie sono hello successiva generazione elaborazione a elevate prestazioni esigenze di elaborazione di fascia alta, come la modellazione molecolare e fluidodinamica computazionale intese a macchine virtuali. Questi 8 e 16 core VM sono basate sulla tecnologia di processore Intel-2667 Haswalle E5 V3 hello con DDR4 memoria e archiviazione basate su SSD locale.

Offre inoltre la potenza della CPU sostanziale di toohello, hello H serie diverse opzioni per la rete RDMA di bassa latenza utilizzando FDR InfiniBand e diverse configurazioni toosupport memoria con utilizzo intensivo calcolo i requisiti di memoria.

| Dimensione            | Core CPU | Memoria: GiB  | Unità SSD locale: GiB       | Larghezza di banda della rete/scheda NIC max |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8/alta |
| Standard_H16    | 16        | 112          | 2000                 | 8/molto alta |
| Standard_H8m    | 8         | 112          | 1000                 | 8/alta |
| Standard_H16m   | 16        | 224          | 2000                 | 8/molto alta |
| Standard_H16r*  | 16        | 112          | 2000                 | 8/molto alta |
| Standard_H16mr* | 16        | 224          | 2000                 | 8/molto alta |

\*Con supporto di RDMA

## <a name="configure-sizes-for-cloud-services"></a>Configurare le dimensioni per i servizi Cloud
È possibile specificare una dimensione di un'istanza del ruolo macchina virtuale hello come parte del modello di servizio hello descritto da hello [file di definizione del servizio](cloud-services-model-and-package.md#csdef). dimensioni Hello del ruolo hello determinano il numero di hello di core CPU, la capacità di memoria hello e hello locale dimensioni del file system allocata tooa esegue l'istanza. Scegliere le dimensioni di ruolo hello in base ai requisiti di risorse dell'applicazione.

Di seguito è riportato un esempio per l'impostazione hello ruolo dimensioni toobe [Standard_D2](#general-purpose-d) per un'istanza del ruolo Web:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Modifica delle dimensioni di hello di un ruolo esistente

Come natura hello delle nuove dimensioni delle macchine Virtuali saranno disponibili le modifiche del carico di lavoro, è opportuno dimensioni hello toochange del ruolo. toodo in modo, è necessario cambiare dimensioni della VM hello nel file di definizione del servizio (come illustrato in precedenza), riassemblare il servizio Cloud e distribuirlo. Non è possibile toochange dimensioni di macchina virtuale direttamente dal portale di hello o PowerShell.

>[!TIP]
> È toouse diverse dimensioni di macchina virtuale per il ruolo in ambienti diversi (ad es. test e produzione). Toodo unidirezionale questo è toocreate più file di definizione (con estensione csdef) del servizio nel progetto, quindi creare i pacchetti del servizio per l'ambiente cloud diverso durante la compilazione automatica con lo strumento CSPack hello. pacchetto services toolearn ulteriori informazioni su elementi hello di un cloud e toocreate, vedere [novità cloud hello servizi modello e come pacchetto?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Ottenere un elenco di dimensioni
È possibile utilizzare PowerShell o hello API REST tooget un elenco di dimensioni. Hello API REST è documentata [qui](https://msdn.microsoft.com/library/azure/dn469422.aspx). Hello codice seguente è un comando di PowerShell che elencherà tutte le dimensioni di hello attualmente disponibili per il servizio Cloud.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).
* Altre informazioni [sulle Dimensioni delle VM High Performance Computing (HPC)](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per carichi di lavoro HPC.
