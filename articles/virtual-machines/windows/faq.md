---
title: aaaFAQ sulle macchine virtuali di Windows in Azure | Documenti Microsoft
description: Fornisce le risposte toosome di domande frequenti di hello sulle macchine virtuali di Windows create con il modello di gestione risorse hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Domande frequenti sulle Macchine virtuali Windows
Questo articolo illustra alcune domande comuni sulle macchine virtuali di Windows create in Azure tramite il modello di distribuzione di gestione risorse di hello. La versione di Linux hello di questo argomento, vedere [domande frequenti sulle macchine virtuali Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Cosa è possibile eseguire in una VM di Azure?
Tutti i sottoscrittori possono eseguire software del server in una macchina virtuale Azure. Per informazioni sui criteri di supporto hello per il software server Microsoft in esecuzione in Azure, vedere [supporto del software server Microsoft per macchine virtuali di Azure](https://support.microsoft.com/kb/2721672)

Alcune versioni di Windows 7, Windows 8.1 e Windows 10 sono disponibili tooMSDN Azure sottoscrittori di benefit e i sottoscrittori MSDN sviluppo e Test pagamento a consumo, per le attività di sviluppo e test. Per ulteriori informazioni, incluse le istruzioni e limitazioni, vedere [Immagini Client Windows per gli abbonati MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanta memoria è possibile utilizzare con una macchina virtuale?
Ogni disco dati può essere backup too1 TB. numero di Hello di dischi di dati che è possibile utilizzare dipende dalle dimensioni hello della macchina virtuale hello. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

I dischi di Azure gestiti sono hello disco consigliato e nuove offerte di archiviazione per l'utilizzo con macchine virtuali di Azure per l'archiviazione permanente dei dati. Puoi usare più dischi gestiti con ogni macchina virtuale. Il servizio Managed Disks offre due tipi di opzioni di archiviazione durevole: Managed Disks Premium e Standard. Per informazioni sui prezzi, vedere [Prezzi di Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).

Gli account di archiviazione di Azure possono anche offrire archiviazione per disco del sistema operativo hello e per eventuali dischi dati. Ogni disco è un file con estensione vhd archiviato come BLOB di pagine. Per informazioni sui prezzi, vedere [Dettagli prezzi di archiviazione](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Come si accede alla macchina virtuale?
Stabilire una connessione remota mediante la Connessione desktop remoto (RDP) per una VM Windows. Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Sono supportati un massimo di due connessioni simultanee, a meno che non hello server è configurato come un host di sessione di Servizi Desktop remoto.  

Se si verificano problemi con Desktop remoto, vedere [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Se si ha familiarità con Hyper-V, si potrebbe cercando un tooVMConnect simile dello strumento. Azure non offre uno strumento simile perché macchina virtuale di tooa accesso console non è supportato.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>È possibile utilizzare i dati di toostore disco temporaneo (Buongiorno unità d: per impostazione predefinita) hello?
Non utilizzare dati di toostore hello disco temporaneo. Si tratta solo di memorie temporanee, pertanto si rischierebbe di perdere dati che non possono essere recuperati. Perdita di dati può verificarsi quando macchina virtuale hello Sposta tooa un host diverso. Ridimensionamento di una macchina virtuale, l'aggiornamento host hello o un errore hardware nell'host di hello è riportati alcuni dei motivi hello che potrebbe spostare una macchina virtuale.

Se si dispone di un'applicazione che richiede una lettera di unità d: hello toouse, è possibile riassegnare le lettere di unità in modo che hello disco temporaneo viene utilizzato un valore diverso da d. Per istruzioni, vedere [lettera di unità di modifica hello del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Come è possibile modificare la lettera di unità hello del disco temporaneo hello?
È possibile modificare la lettera di unità hello per lo spostamento del file pagina hello e riassegnando le lettere di unità, ma è necessario toomake che si hello passaggi in un ordine specifico. Per istruzioni, vedere [lettera di unità di modifica hello del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>È possibile aggiungere un set di disponibilità tooan VM esistente?
No. Se si desidera la parte toobe VM di un set di disponibilità, è necessario toocreate hello VM all'interno di hello set. Attualmente non è disponibile un tooadd modo una macchina virtuale tooan set di disponibilità dopo che è stato creato.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>È possibile caricare tooAzure una macchina virtuale?
Sì. Per istruzioni, vedere [migrazione locale macchine virtuali tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>È possibile ridimensionare disco del sistema operativo hello?
Sì. Per istruzioni, vedere [come tooexpand hello unità del sistema operativo di una macchina virtuale in un gruppo di risorse di Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>È possibile copiare o clonare una VM di Azure esistente?
Sì. Utilizzo di immagini gestite, è possibile creare un'immagine di una macchina virtuale e quindi utilizzare hello immagine toobuild più nuove macchine virtuali. Per istruzioni, vedere [Creare un'immagine personalizzata di una macchina virtuale](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Perché non si vedono le aree del Canada centrale e del Canada orientale tramite Azure Resource Manager?

Hello due nuove aree di centrale Canada e Canada orientale non vengono registrate automaticamente per la creazione della macchina virtuale per le sottoscrizioni di Azure esistente. Questa registrazione viene eseguita automaticamente quando una macchina virtuale viene distribuita tramite hello tooany portale Azure altre aree di gestione risorse di Azure. Dopo una macchina virtuale è distribuita tooany altre aree di Azure, nuove aree hello devono essere disponibili per le macchine virtuali successive.

## <a name="does-azure-support-linux-vms"></a>Le VM di Linux sono supportate da Azure?
Sì. tooquickly creare una VM Linux di tootry out, vedere [creare una VM Linux in Azure mediante portale hello](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>È possibile aggiungere un toomy NIC VM dopo averla creata?
Sì, ora è possibile. Hello VM prima esigenze toobe arrestate deallocate. È possibile aggiungere o rimuovere una scheda di rete (a meno che non è hello ultimo NIC hello VM). 

## <a name="are-there-any-computer-name-requirements"></a>Esistono requisiti relativi al nome del computer?
Sì. nome del computer Hello può contenere un massimo di 15 caratteri. Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sulla denominazione delle risorse.

## <a name="are-there-any-resource-group-name-requirements"></a>Vi sono requisiti relativi al nome del gruppo di risorse?
Sì. nome del gruppo di risorse Hello può contenere un massimo di 90 caratteri. Vedere [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Regole e restrizioni per le convenzioni di denominazione) per altre informazioni sui gruppi di risorse.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quali sono i requisiti di nome utente hello durante la creazione di una macchina virtuale?

I nomi utente possono contenere un massimo di 20 caratteri e non possono terminare con un punto ("."). 


non è consentita Hello nomi utente di seguenti:
<table>
    <tr>
        <td style="text-align:center">entità </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
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
Le password devono essere 12 123 caratteri e soddisfare 3 fuori hello dopo 4 requisiti di complessità:

* Devono contenere caratteri minuscoli
* Devono contenere caratteri maiuscoli
* Devono contenere almeno un numero
* Devono contenere un carattere speciale (REGEX.CONFRONTA [\W_])

Hello seguendo le password non è consentito:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
