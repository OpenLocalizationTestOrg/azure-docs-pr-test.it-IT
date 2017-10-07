---
title: una rete virtuale in Azure DevTest Labs aaaConfigure | Documenti Microsoft
description: Informazioni su come tooconfigure una subnet e la rete virtuale esistente e usati in una macchina virtuale con Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Configurare una rete virtuale per Azure DevTest Labs
Come illustrato nell'articolo hello [aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md), quando si crea una macchina virtuale in un lab, è possibile specificare una rete virtuale configurata. Uno scenario per eseguire questa operazione è se è necessario tooaccess le risorse di rete aziendale dalle macchine virtuali utilizzando hello rete virtuale che è stato configurato con ExpressRoute o VPN da sito a sito. Hello nelle sezioni seguenti viene illustrato come tooadd la rete virtuale esistente nelle impostazioni di rete virtuale dell'ambiente di test in modo che sia disponibile toochoose durante la creazione di macchine virtuali.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Configurare una rete virtuale per un ambiente lab tramite hello portale di Azure
Hello passaggi seguenti consentono di aggiungere un laboratorio di tooa rete (e la subnet) virtuale esistente in modo che può essere utilizzato durante la creazione di una macchina virtuale in hello lab stesso. 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello. 
4. Nel pannello del lab hello, selezionare **configurazione**.
5. Nel lab di hello **configurazione** pannello seleziona **le reti virtuali**.
6. In hello **le reti virtuali** pannello viene visualizzato un elenco di reti virtuali configurate per lab corrente hello nonché hello predefinito rete virtuale creata per l'ambiente lab. 
7. Selezionare **+ Aggiungi**.
   
    ![Aggiungere un laboratorio di tooyour di rete virtuale esistente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. In hello **rete virtuale** pannello seleziona **[rete virtuale selezionare]**.
   
    ![Selezionare una rete virtuale esistente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. In hello **rete virtuale scegliere** blade, rete virtuale desiderato selezionare hello. Pannello Hello Mostra tutte le reti virtuali hello che sono in hello stessa regione nella sottoscrizione hello lab hello.  
10. Dopo aver selezionato una rete virtuale, viene visualizzato toohello **rete virtuale** clic hello subnet nell'elenco di hello nella parte inferiore di hello del pannello hello.

    ![Elenco di subnet](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    viene visualizzato il pannello di Subnet Lab Hello.

    ![Pannello Lab Subnet (Subnet lab)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Specificare un **nome per la subnet del lab**.
12. tooallow toobe una subnet usati nel lab la creazione di VM, selezionare **utilizzare nella creazione della macchina virtuale**.
13. tooenable un [condiviso l'indirizzo IP pubblico](devtest-lab-shared-ip.md)selezionare **Abilita condivisa IP pubblico**.
14. tooallow gli indirizzi IP pubblici in una subnet, selezionare **consentire la creazione di IP pubblica**.
15. In hello **massimo di macchine virtuali per utente** specificare hello massime macchine virtuali per utente per ogni subnet. Se si desidera un numero illimitato di VM, lasciare vuoto questo campo.
16. Selezionare **OK** blade di Subnet Lab tooclose hello.
17. Selezionare **salvare** blade di rete virtuale hello tooclose.
18. Ora che hello rete virtuale è configurata, può essere selezionato quando si crea una macchina virtuale. 
    toosee come toocreate una macchina virtuale e specificare una rete virtuale, vedere l'articolo toohello [aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver aggiunto hello desiderato lab tooyour di rete virtuale, hello è troppo[aggiungere un ambiente lab tooyour VM](devtest-lab-add-vm-with-artifacts.md).

