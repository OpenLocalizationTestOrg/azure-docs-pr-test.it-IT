---
title: tooLinux aaaIntroduction in Azure | Documenti Microsoft
description: Informazioni sull'uso delle macchine virtuali Linux in Azure.
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Introduzione tooLinux in Azure
In questo argomento viene fornita una panoramica di alcuni aspetti dell'utilizzo di macchine virtuali Linux in hello cloud di Azure. La distribuzione di una macchina virtuale Linux è un processo semplice utilizzo di un'immagine dalla raccolta hello.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Autenticazione: nomi utente, password e chiavi SSH
Quando si crea una macchina virtuale di Linux mediante hello portale di Azure, viene chiesto tooprovide un nome utente e password o una chiave pubblica SSH. scelta di un nome utente per la distribuzione di una macchina virtuale di Linux in Azure Hello è soggetto toohello seguenti vincoli: i nomi degli account di sistema (UID < 100) è già presente in hello macchina virtuale non sono consentiti, 'radice', ad esempio.

* Vedere [Creare una macchina virtuale che esegue Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Vedere [come tooUse SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Ottenere privilegi utente avanzato tramite `sudo`
account utente di Hello specificato durante la distribuzione di istanza di macchina virtuale in Azure è un account con privilegi. Questo account viene configurato per l'utilizzo di hello hello agente Linux di Azure toobe tooelevate in grado di privilegi tooroot (account utente avanzato) `sudo` utilità. Una volta effettuato l'accesso usando questo account utente, sarà in grado di toorun comandi come radice utilizzando la sintassi del comando hello:

    # sudo <COMMAND>

Facoltativamente, è possibile ottenere una shell di root usando **sudo -s**.

* Vedere [Uso di privilegi root sulle macchine virtuali Linux in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Configurazione del firewall
Azure offre un filtro di pacchetti in ingresso che limita la connettività tooports specificato nel portale di Azure hello. Per impostazione predefinita, hello consentita è solo la porta SSH. È possibile aprire le porte di accesso tooadditional sulla macchina virtuale Linux tramite la configurazione di endpoint in hello portale di Azure:

* Vedere: [come configurare gli endpoint di tooSet tooa macchina virtuale](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

le immagini Linux Hello in hello raccolta Azure non abilitare hello *iptables* firewall per impostazione predefinita. Se lo si desidera, può essere configurata firewall hello tooprovide altre opzioni di filtro.

## <a name="hostname-changes"></a>Modifica del nome host
Durante la distribuzione iniziale di un'istanza di un'immagine Linux, verrà richiesto tooprovide un nome host per macchina virtuale hello. Dopo l'esecuzione della macchina virtuale hello, questo nome host è server DNS di piattaforma toohello pubblicato in modo che più macchine virtuali connesse tooeach altri possono eseguire ricerche di indirizzi IP utilizzando i nomi host.

Se dopo la distribuzione di una macchina virtuale, si desidera apportare modifiche di nome host, utilizzare il comando hello

    # sudo hostname <newname>

Hello agente Linux di Azure include funzionalità tooautomatically rilevare questa modifica del nome e configurare hello macchina virtuale toopersist questa modifica e pubblicare i server DNS piattaforma toohello questa modifica in modo appropriato.

* [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>cloud-init
Le immagini **Ubuntu** e **CoreOS** usano cloud-init in Azure, che offre capacità aggiuntive per il bootstrap di una macchina virtuale.

* [Come tooInject dati personalizzati](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Dati personalizzati e cloud-init in Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Creare partizioni di scambio di Azure con cloud-init](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Come tooUse CoreOS in Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Acquisizione di immagini di macchine virtuali
Azure offre stato di hello possibilità toocapture hello di una macchina virtuale esistente in un'immagine che può successivamente essere istanze di macchina virtuale aggiuntiva toodeploy utilizzato. Hello agente Linux di Azure può essere utilizzato toorollback alcune hello personalizzazione che è stata eseguita durante il processo di provisioning hello. È possibile eseguire operazioni di hello seguenti toocapture una macchina virtuale come un'immagine:

1. Eseguire **waagent-deprovision** tooundo il provisioning di personalizzazione. O **waagent-deprovision + user** toooptionally eliminare account utente di hello specificato durante il provisioning e tutti i dati associati.
2. Shut down/spegnimento della macchina virtuale hello.
3. Fare clic su **acquisire** hello Azure hello portale o usare PowerShell o CLI strumenti macchina virtuale di hello toocapture come immagine.
   
   * Vedere: [come tooCapture tooUse una macchina virtuale Linux come modello](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Collegamento di dischi
Ogni macchina virtuale ha un *disco risorse* temporaneo locale collegato. Perché i dati su un disco di risorsa non siano durevoli dopo il riavvio, viene spesso utilizzato dalle applicazioni e processi in esecuzione nella macchina virtuale hello per temporaneo e **temporaneo** archiviazione dei dati. È inoltre usato toostore hello scambio file di paging o per sistema operativo hello.

In genere gestito da hello agente Linux di Azure e montato automaticamente troppo su Linux, il disco di risorsa hello**/mnt/Retention/ risorse** (o **/mnt** sulle immagini Ubuntu).

> [!NOTE]
> Si noti il disco di risorsa hello è un **temporaneo** disco e potrebbero essere eliminate e riformattati quando hello VM è stato riavviato.
> 
> 

In Linux potrebbe essere denominata disco dati hello dal kernel hello come `/dev/sdc`, e gli utenti dovranno toopartition, formattare e montare tale risorsa. Questo argomento viene trattato dettagliate nell'esercitazione hello: [come tooAttach tooa un disco dati macchina virtuale](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Vedere anche:** [Configurare RAID software in Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configurare LVM su una macchina virtuale Linux in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

