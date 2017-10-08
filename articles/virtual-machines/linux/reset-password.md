---
title: password locale Linux aaaHow tooreset su macchine virtuali di Azure | Documenti Microsoft
description: Introdurre hello passaggi tooreset hello Linux password locale nella macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Come password Linux locale tooreset nelle macchine virtuali di Azure

Questo articolo descrive le password di Linux macchina virtuale (VM) di diversi metodi tooreset locale. Se l'account utente hello è scaduto o è toocreate un nuovo account, è possibile utilizzare hello seguenti metodi toocreate un nuovo account di amministratore locale e ottenere nuovamente accesso toohello macchina virtuale.

## <a name="symptoms"></a>Sintomi

Non è possibile accedere toohello VM e viene visualizzato un messaggio che indica che la password hello utilizzato non è corretta. Inoltre, è possibile utilizzare VMAgent tooreset la password nel portale di Azure hello. 

## <a name="manual-password-reset-procedure"></a>Procedura di reimpostazione manuale della password

1.  Eliminare hello VM e mantenere i dischi collegato hello.

2.  Collegare l'unità del sistema operativo come una tooanother disco dati hello temporale macchina virtuale in hello nello stesso percorso.

3.  Eseguire hello successivo comando SSH su hello temporale VM toobecome un utente avanzato.


    ~~~~
    sudo su
    ~~~~

4.  Eseguire **fdisk -l** o esaminare hello toofind i registri di sistema il disco appena collegato. Individuare hello unità nome toomount. Quindi in hello VM temporale, Cerca in hello rilevante file di log.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    esempio Hello è riportato l'output del comando grep hello:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Creare un punto di montaggio denominato **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Montare il disco di hello del sistema operativo nel punto di montaggio hello. In genere, è necessario toomount sdc1 o sdc2. Questo dipende hello hosting partizione di directory /etc/hosts dal disco di macchina interrotti hello.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Eseguire un backup prima di apportare modifiche:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Reimpostare la password dell'utente hello che è necessario:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Spostamento hello modificati file toohello percorso corretto hello suddiviso disco della macchina.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
