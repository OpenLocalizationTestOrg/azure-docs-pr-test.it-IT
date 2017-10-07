---
title: aaaCreate un nodo head di HPC Pack in una macchina virtuale di Azure | Documenti Microsoft
description: Informazioni su come toouse hello distribuzione di gestione risorse di hello e del portale Azure modello toocreate un nodo head di Microsoft HPC Pack 2012 R2 in una macchina virtuale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Creare il nodo head di hello di un cluster HPC Pack in una macchina virtuale di Azure con un'immagine del Marketplace
Utilizzare un [immagine di macchina virtuale di Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) da hello Azure Marketplace e hello toocreate portale Azure hello nodo head di un cluster HPC. L'immagine di macchina virtuale HPC Pack è basata su Windows Server 2012 R2 Datacenter con HPC Pack 2012 R2 Update 3 preinstallato. Usare questo nodo head per una distribuzione basata sul modello di verifica di HPC Pack in Azure. È quindi possibile aggiungere calcolo nodi toohello toorun HPC i carichi di lavoro.

> [!TIP]
> completamento del cluster HPC Pack 2012 R2 in Azure che include nodi di calcolo e del nodo head hello toodeploy, è consigliabile utilizzare un metodo automatico. Le opzioni includono hello [script di distribuzione IaaS di HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e modelli di gestione risorse, ad esempio hello [cluster HPC Pack per i carichi di lavoro di Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). I modelli di Resource Manager sono disponibili anche per i [cluster Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Considerazioni sulla pianificazione
Come illustrato nella seguente illustrazione hello, si distribuisce nodo head di HPC Pack hello in un dominio di Active Directory in una rete virtuale di Azure.

![Nodo head HPC Pack][headnode]

* **Dominio di Active Directory**: hello deve essere un nodo head HPC Pack 2012 R2 aggiunti a un dominio di Active Directory tooan in Azure prima di avviare i servizi HPC hello nei hello macchina virtuale. Come illustrato in questo articolo per una prova di distribuzione, è possibile alzare di livello macchina virtuale creata per il nodo head hello come controller di dominio prima di avviare i servizi HPC hello hello. Un'altra opzione è toodeploy un controller di dominio separato e foresta in Azure toowhich join hello macchina virtuale del nodo head.

* **Modello di distribuzione**: per la maggior parte delle nuove distribuzioni, Microsoft consiglia di utilizzare il modello di distribuzione del hello Gestione risorse. Questo articolo presuppone che si usi questo modello di distribuzione.

* **Rete virtuale di Azure**: quando si usa hello Gestione risorse distribuzione toodeploy hello head nodo del modello, specificare o creare una rete virtuale di Azure. È possibile utilizzare la rete virtuale hello è necessario toojoin hello nodo head tooan dominio Active Directory esistente. È inoltre necessario successive tooadd del nodo di calcolo cluster toohello macchine virtuali.

## <a name="steps-toocreate-hello-head-node"></a>Nodo head di passaggi toocreate hello
Di seguito sono passaggi di alto livello toouse hello toocreate portale Azure una macchina virtuale di Azure per il nodo head di HPC Pack hello con modello di distribuzione di gestione risorse di hello. 

1. Se si desidera toocreate una nuova foresta di Active Directory in Azure con il controller di dominio separato macchine virtuali, è toouse un [modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Per un semplice modello di prova di distribuzione, ha un preciso tooomit questo passaggio e configurare il nodo head hello macchina virtuale come controller di dominio. Le opzioni sono descritte più avanti in questo articolo.
2. In hello [HPC Pack 2012 R2 in Windows Server 2012 R2 pagina](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketplace, fare clic su **crea macchina virtuale**. 
3. Nel portale hello hello **HPC Pack 2012 R2 in Windows Server 2012 R2** pagina, seleziona hello **Gestione risorse** modello di distribuzione e quindi fare clic su **crea**.
   
    ![Immagine di HPC Pack][marketplace]
4. Utilizzare le impostazioni di hello tooconfigure portale hello e creare hello macchina virtuale. Se si tooAzure nuovo, seguire l'esercitazione hello [creare una macchina virtuale di Windows nel portale di Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Per una prova di distribuzione, è in genere accettare hello predefinita o impostazioni consigliate.
   
   > [!NOTE]
   > Se si desidera toojoin hello nodo head tooan esistente di dominio Active Directory in Azure, assicurarsi di che specificare la rete virtuale di hello per quel dominio durante la creazione di hello macchina virtuale.
   > 
   > 
5. Dopo aver creato hello VM e hello macchina virtuale è in esecuzione, [connettersi toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) da Desktop remoto. 
6. Creare un join foresta di domini di Active Directory di hello VM tooan scegliendo una delle seguenti opzioni hello:
   
   * Hello VM è stato creato in una rete virtuale Azure con una foresta di domini esistente, unire in join dell'insieme di strutture di hello VM toohello utilizzando gli strumenti di Server Manager o Windows PowerShell standard. Eseguire quindi il riavvio.
   * Se si crea una nuova rete virtuale (senza una foresta di domini esistente) hello VM, quindi alzare di livello hello VM come controller di dominio. Utilizzare i passaggi standard tooinstall e configurare il ruolo di servizi di dominio Active Directory hello nel nodo head hello. Per informazioni dettagliate, vedere [Installare una nuova foresta di Active Directory di Windows Server 2012](https://technet.microsoft.com/library/jj574166.aspx).
7. Dopo aver hello macchina virtuale è in esecuzione e tooan aggiunti a un insieme di strutture Active Directory, avviare i servizi di HPC Pack hello come indicato di seguito:
   
    a. Connessione macchina virtuale utilizzando un account di dominio che è un membro del gruppo Administrators locale hello del nodo head toohello. Ad esempio, utilizzare account di amministratore hello impostate al momento della creazione macchina virtuale del nodo head hello.
   
    b. Per una configurazione del nodo head predefinito, avviare Windows PowerShell come amministratore e digitare hello riportato di seguito:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Può richiedere alcuni minuti per hello HPC Pack servizi toostart.
   
    Per ulteriori opzioni per la configurazione del nodo head, digitare `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Passaggi successivi
* È ora possibile lavorare con i nodi head hello del cluster HPC Pack. Ad esempio, avviare Gestione Cluster HPC e hello completo [elenco attività di distribuzione](https://technet.microsoft.com/library/jj884141.aspx).
* Se si desidera tooincrease hello del cluster di calcolo della capacità su richiesta, aggiungere [nodi di potenziamento di Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in un servizio cloud. 
* Provare a eseguire un test di carico nel cluster hello. Per un esempio, vedere hello HPC Pack [Guida introduttiva](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
