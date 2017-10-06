---
title: domande frequenti per le macchine virtuali Linux in Azure aaaFrequently | Documenti Microsoft
description: Fornisce le risposte toosome di domande frequenti di hello relative macchine virtuali Linux create con il modello di gestione risorse hello.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Domande frequenti sulle macchine virtuali Linux
Questo articolo illustra alcune domande frequenti sulle macchine virtuali Linux create in Azure tramite il modello di distribuzione di gestione risorse di hello. La versione di Windows hello di questo argomento, vedere [domande frequenti sulle macchine virtuali di Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Cosa è possibile eseguire in una VM di Azure?
Tutti i sottoscrittori possono eseguire software del server in una macchina virtuale Azure. Per altre informazioni, vedere [Distribuzioni di Linux supportate da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanta memoria è possibile utilizzare con una macchina virtuale?
Ogni disco dati può essere backup too1 TB. numero di Hello di dischi di dati che è possibile utilizzare dipende dalle dimensioni hello della macchina virtuale hello. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Un account di archiviazione di Azure fornisce archiviazione per disco del sistema operativo hello e per eventuali dischi dati. Ogni disco è un file con estensione vhd archiviato come BLOB di pagine. Per informazioni sui prezzi, vedere [Dettagli prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Come si accede alla macchina virtuale?
Stabilire una connessione remota di toolog nella macchina virtuale toohello tramite Secure Shell (SSH). Vedere le istruzioni di hello sul tooconnect [da Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [da Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per impostazione predefinita, la SSH consente un massimo di 10 connessioni simultanee. È possibile aumentare questo numero modificando il file di configurazione di hello.

Se si verificano problemi, vedere l'argomento [Risolvere i problemi relativi alle connessioni Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>È possibile utilizzare i dati di toostore hello disco temporaneo (dev/sdb1)?
Non utilizzare dati di toostore hello disco temporaneo (dev/sdb1). Serve solo per l'archiviazione temporanea. I dati non ripristinabili rischiano di andare persi.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>È possibile copiare o clonare una VM di Azure esistente?
Sì. Per istruzioni, vedere [come toocreate una copia di una macchina virtuale di Linux in hello il modello di distribuzione di gestione risorse](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Perché non si vedono le aree del Canada centrale e del Canada orientale tramite Azure Resource Manager?
Hello due nuove aree di centrale Canada e Canada orientale non vengono registrate automaticamente per la creazione della macchina virtuale per le sottoscrizioni di Azure esistente. Questa registrazione viene eseguita automaticamente quando una macchina virtuale viene distribuita tramite hello tooany portale Azure altre aree di gestione risorse di Azure. Dopo una macchina virtuale è distribuita tooany altre aree di Azure, nuove aree hello devono essere disponibili per le macchine virtuali successive.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>È possibile aggiungere un toomy NIC VM dopo averla creata?
Sì, ora è possibile. Hello VM prima esigenze toobe arrestate deallocate. È possibile aggiungere o rimuovere una scheda di rete (a meno che non è hello ultimo NIC hello VM). 

## <a name="are-there-any-computer-name-requirements"></a>Esistono requisiti relativi al nome del computer?
Sì. nome del computer Hello può contenere un massimo di 64 caratteri. Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sulla denominazione delle risorse.

## <a name="are-there-any-resource-group-name-requirements"></a>Vi sono requisiti relativi al nome del gruppo di risorse?
Sì. nome del gruppo di risorse Hello può contenere un massimo di 90 caratteri. Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sui gruppi di risorse.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quali sono i requisiti di nome utente hello durante la creazione di una macchina virtuale?
I nomi utente devono contenere da 1 a 64 caratteri.

non è consentita Hello nomi utente di seguenti:

<table>
    <tr>
        <td style="text-align:center">entità </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> proprietario </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> support </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Quali sono i requisiti della password hello durante la creazione di una macchina virtuale?
Le password devono essere di 6-72 caratteri e soddisfare 3 fuori hello dopo 4 requisiti di complessità:

* Devono contenere caratteri minuscoli
* Devono contenere caratteri maiuscoli
* Devono contenere almeno un numero
* Devono contenere un carattere speciale (REGEX.CONFRONTA [\W_])

Hello seguendo le password non è consentito:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
