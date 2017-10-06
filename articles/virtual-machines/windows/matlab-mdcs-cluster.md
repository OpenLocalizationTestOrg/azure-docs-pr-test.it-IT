---
title: aaaMATLAB cluster nelle macchine virtuali | Documenti Microsoft
description: Utilizzare macchine virtuali di Microsoft Azure toocreate MATLAB Distributed Computing Server cluster toorun i carichi di lavoro con utilizzo intensivo di calcolo paralleli MATLAB
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Creare cluster MATLAB Distributed Computing Server in VM di Azure
Utilizzare Microsoft Azure virtuale macchine toocreate uno o più MATLAB Distributed Computing Server cluster toorun i carichi di lavoro con utilizzo intensivo di calcolo paralleli MATLAB. Installa il software MATLAB Distributed Computing Server in una macchina virtuale toouse come un'immagine di base e utilizzare un modello di avvio rapido di Azure o uno script di PowerShell di Azure (disponibile in [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy e gestire cluster hello. Dopo la distribuzione, connettersi toohello cluster toorun i carichi di lavoro.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Informazioni su MATLAB e MATLAB Distributed Computing Server
Hello [MATLAB](http://www.mathworks.com/products/matlab/) è con ottimizzazione per la piattaforma per la risoluzione dei problemi di scientifici e tecnici. Gli utenti MATLAB simulazioni su larga scala e le attività di elaborazione dei dati possono utilizzare toospeed prodotti dei relativi carichi di lavoro con uso intensivo di calcolo avvalersi dei servizi di griglia e i cluster di calcolo parallelo MathWorks. [Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) consente agli utenti di MATLAB di parallelizzare le applicazioni e sfruttare i vantaggi di processori multicore, GPU e cluster di elaborazione. [MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) consente MATLAB utenti tooutilize molti computer in un cluster di calcolo.

Tramite macchine virtuali di Azure, è possibile creare cluster MATLAB Distributed Computing Server che hanno tutti hello stessi meccanismi disponibili toosubmit un lavoro parallelo come cluster locale, ad esempio i processi interattivi, i processi batch attività indipendenti, e attività di comunicazione. L'utilizzo di Azure in combinazione con la piattaforma MATLAB hello presenta molti vantaggi rispetto tooprovisioning utilizzando tradizionale in locale e hardware: dimensioni di un intervallo di macchina virtuale, creazione di cluster su richiesta in modo si paga solo per le risorse di calcolo hello si utilizza, e modelli di tootest Hello possibilità su larga scala.  

## <a name="prerequisites"></a>Prerequisiti
* **Computer client** -è necessario un toocommunicate di computer client basati su Windows con Azure e hello cluster MATLAB Distributed Computing Server dopo la distribuzione.
* **Azure PowerShell** -vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) tooinstall sul computer client.
* **Sottoscrizione di Azure** : se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti. Per cluster di maggiori dimensioni, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto.
* **Quota di core** -tooincrease hello core quota toodeploy potrebbe essere necessario un cluster di grandi dimensioni o più cluster MATLAB Distributed Computing Server. una quota, tooincrease [aprire una richiesta di supporto clienti online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) senza alcun costo.
* **MATLAB, casella degli strumenti di elaborazione parallela e MATLAB Distributed Computing Server licenze** -script di hello presuppongono che hello [MathWorks ospitato License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) viene utilizzato per tutte le licenze.  
* **Software MATLAB Distributed Computing Server** -verrà installato in una macchina virtuale che verrà utilizzata come immagine di macchina virtuale di base hello per le macchine virtuali del cluster di hello.

## <a name="high-level-steps"></a>Passaggi di livello elevato
toouse macchine virtuali di Azure per i cluster di MATLAB Distributed Computing Server hello passaggi di alto livello seguenti sono necessari. Vengono fornite istruzioni dettagliate nella documentazione di hello che accompagna il modello di avvio rapido hello e script in [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Creare un'immagine di VM di base**  

   * Scaricare e installare il software MATLAB Distributed Computing Server in questa VM.

     > [!NOTE]
     > Questo processo può richiedere alcune ore, ma è sufficiente toodo, una volta per ogni versione di MATLAB è utilizzare.   
     >
     >
2. **Creare uno o più cluster**  

   * Utilizzare uno script di PowerShell hello fornito oppure hello delle Guide rapide modello toocreate un cluster dall'immagine di macchina virtuale di base hello.   
   * Gestire i cluster hello hello fornito lo script di PowerShell che consente di toolist, sospendere, riprendere e i cluster di eliminazione.

## <a name="cluster-configurations"></a>Configurazioni dei cluster
Attualmente, modello e script di creazione di cluster hello consentono toocreate una singola topologia MATLAB Distributed Computing Server. È possibile creare uno o più cluster aggiuntivi e ogni cluster può avere un numero diverso di VM di lavoro, con dimensioni di VM diverse e così via.

### <a name="matlab-client-and-cluster-in-azure"></a>Client e cluster MATLAB in Azure
Nella figura Hello MATLAB client nodi, il pianificatore di processi MATLAB e MATLAB Distributed Computing Server "di lavoro" nodi configurati come macchine virtuali di Azure in una rete virtuale, come illustrato nell'esempio hello.


* toouse hello del cluster, eseguire la connessione dal nodo client toohello di Desktop remoto. nodo Hello del client viene eseguito il client MATLAB hello.
* nodo client hello è una condivisione di file accessibili da tutti i processi di lavoro.
* MathWorks ospitato License Manager viene utilizzato per i controlli di licenza hello per tutto il software MATLAB.
* Per impostazione predefinita, un lavoratore MATLAB Distributed Computing Server per ogni core viene creato nel ruolo di lavoro hello macchine virtuali, ma è possibile specificare qualsiasi numero.

## <a name="use-an-azure-based-cluster"></a>Usare un cluster basato su Azure
Come con altri tipi di MATLAB Distributed Computing Server cluster, è necessario toouse Ciao gestione profilo Cluster hello MATLAB client (nel client hello VM) toocreate un profilo cluster pianificatore di processi MATLAB.

![Cluster Profile Manager](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Passaggi successivi
* Per istruzioni dettagliate toodeploy e gestire i cluster MATLAB Distributed Computing Server in Azure, vedere hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repository che contiene modelli hello e script.
* Passare toohello [MathWorks sito](http://www.mathworks.com/) per la documentazione dettagliata per MATLAB e MATLAB Distributed Computing Server.
