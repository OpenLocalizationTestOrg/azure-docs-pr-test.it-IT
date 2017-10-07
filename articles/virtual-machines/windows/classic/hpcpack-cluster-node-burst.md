---
title: cluster di HPC Pack tooan nodi burst aaaAdd | Documenti Microsoft
description: Informazioni su come tooexpand un pacchetto HPC cluster in Azure su richiesta tramite l'aggiunta di istanze del ruolo di lavoro in esecuzione in un servizio cloud
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Aggiungere su richiesta "potenziamento" nodi tooan cluster HPC Pack in Azure
Se si configura un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, è necessario un modo tooquickly scala hello cluster capacità verso l'alto o verso il basso, senza mantenere un set di macchine virtuali del nodo di calcolo preconfigurato. Questo articolo illustra come tooadd su richiesta "potenziamento" nodi (istanze del ruolo di lavoro in esecuzione in un servizio cloud) come nodo head tooa risorse di calcolo in Azure. 

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

![Nodi burst][burst]

procedura di Hello in questo articolo consente di aggiungere nodi di Azure rapidamente tooa basato su cloud HPC Pack nodo head macchina virtuale per una distribuzione di test o di prova. passaggi di alto livello Hello sono hello uguali a quelli passaggi hello troppo "potenziamento tooAzure" tooadd di calcolo cloud cluster HPC Pack locale tooan di capacità. Per un'esercitazione, vedere [Configurazione di un cluster di calcolo ibrido con Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Per istruzioni dettagliate e considerazioni per le distribuzioni di produzione, vedere [potenziamento tooAzure con Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Prerequisiti
* **Distribuzione di un nodo head HPC Pack in una VM Azure** : è possibile utilizzare una VM del nodo head autonoma oppure una che fa parte di un cluster più esteso. vedere un nodo head autonomo, toocreate [distribuire un nodo Head di HPC Pack in una macchina virtuale Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Per opzioni di distribuzione del cluster HPC Pack automatizzate, vedere [opzioni toocreate e gestire un cluster Windows HPC in Azure con Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Se si utilizza hello [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) toocreate hello del cluster in Azure, è possibile includere nodi di potenziamento in Azure nella distribuzione automatizzata. Vedere esempi hello in tale articolo.
  > 
  > 
* **Sottoscrizione di Azure** -tooadd Azure nodi, è possibile scegliere hello stessa sottoscrizione utilizzata nodo head hello toodeploy macchina virtuale, o una sottoscrizione diversa (o sottoscrizioni).
* **Quota di core** -potrebbe essere necessario quota hello tooincrease di core, soprattutto se si sceglie toodeploy diversi nodi di Azure con dimensioni multicore. una quota, tooincrease [aprire una richiesta di supporto clienti online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) senza alcun costo.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Passaggio 1: Creare un servizio cloud e un account di archiviazione per hello nodi di Azure
Utilizzare hello portale di Azure classico o hello tooconfigure strumenti equivalenti seguenti risorse che sono necessari toodeploy i nodi di Azure:

* Un nuovo servizio cloud di Azure
* Un nuovo account di archiviazione di Azure

> [!NOTE]
> Non riusare un servizio cloud esistente nella sottoscrizione. 
> 
> 

**Considerazioni**

* Configurare un servizio cloud separato per ogni modello di nodo di Azure che si prevede di toocreate. Tuttavia, è possibile utilizzare hello stesso account di archiviazione per più modelli di nodo.
* Si consiglia di individuare il servizio di cloud hello e account di archiviazione hello per la distribuzione di hello hello stessa area di Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Passaggio 2: Configurare un certificato di gestione di Azure
tooadd Azure nodi come risorse di calcolo, è necessario un certificato di gestione nel nodo head hello e caricamento di un corrispondente certificato toohello sottoscrizione di Azure usata per la distribuzione di hello.

Per questo scenario, è possibile scegliere hello **predefinito di certificato di gestione Azure HPC** che installa e configura automaticamente nel nodo head di HPC Pack. Questo certificato è utile a scopo di test e per distribuzioni con modello di verifica. toouse questo certificato, caricare il 2012\Bin\hpccert.cer c:\Programmi\Microsoft HPC Pack file dal nodo head hello sottoscrizione toothe macchina virtuale. certificato hello tooupload hello [portale di Azure classico](https://manage.windowsazure.com), fare clic su **impostazioni** > **i certificati di gestione**.

Opzioni aggiuntive tooconfigure hello certificato di gestione, vedere [hello tooConfigure scenari il certificato di gestione di Azure per distribuzioni di potenziamento di Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Passaggio 3: Distribuire cluster toohello nodi di Azure
Hello tooadd passaggi e avviare Azure nodi in questo scenario vengono in genere hello stesso come passaggi di hello con un nodo head locale. Per ulteriori informazioni, vedere hello seguenti sezioni in [passaggi tooDeploy nodi di Azure con Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):

* Creare un modello di nodo di Azure
* Aggiungere nodi di Azure toohello Windows HPC cluster
* Avvio (provisioning) hello nodi di Azure

Dopo aver aggiunto e avviare i nodi di hello, sono pronti per l'utente, i processi di toouse toorun cluster.

Se si verificano problemi durante la distribuzione di nodi di Azure, vedere [Risoluzione dei problemi delle distribuzioni di nodi di Azure con Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Passaggi successivi
* un'istanza con utilizzo intensivo di calcolo di dimensioni per hello toouse potenziamento nodi, vedere Considerazioni hello in [dimensioni delle macchine Virtuali di calcolo ad alte prestazioni](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Se si desidera aumentare o compattare automaticamente hello Azure le risorse in base al carico di lavoro di hello del cluster di elaborazione, vedere [automaticamente aumentare e ridurre le risorse di calcolo di Azure in un cluster HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
