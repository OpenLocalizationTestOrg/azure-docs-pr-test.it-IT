---
title: aaaOpen porte tooa VM utilizzando hello portale di Azure | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una macchina virtuale Windows di tooyour endpoint utilizzando il modello di distribuzione Gestione risorse di hello in hello portale di Azure
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Come tooopen porte tooa la macchina virtuale con hello portale di Azure
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandi rapidi
È possibile [eseguire questi passaggi anche tramite Azure PowerShell](nsg-quickstart-powershell.md).

Come prima operazione, creare il gruppo di sicurezza di rete. Selezionare un gruppo di risorse nel portale di hello, scegliere **Aggiungi**, quindi cercare e selezionare **il gruppo di sicurezza di rete**:

![Aggiungere un gruppo di sicurezza di rete](./media/nsg-quickstart-portal/add-nsg.png)

Immettere un nome per il gruppo di sicurezza di rete e selezionare o creare un gruppo di risorse, quindi selezionare una posizione. Al termine selezionare **Crea**:

![Creare un gruppo di sicurezza di rete](./media/nsg-quickstart-portal/create-nsg.png)

Selezionare il nuovo gruppo di sicurezza di rete. Selezionare 'Regole di sicurezza in ingresso', quindi selezionare hello **Aggiungi** toocreate pulsante una regola:

![Aggiungere una regola in entrata](./media/nsg-quickstart-portal/add-inbound-rule.png)

Scegliere un comune **servizio** dal menu a discesa hello, ad esempio *HTTP*. È inoltre possibile selezionare *personalizzato* tooprovide toouse una porta specifica. Se si desidera, modificare la priorità hello o il nome. Hello priorità influisce sull'ordine hello in cui vengono applicate regole - valore numerico di hello inferiore hello, hello precedenti hello regola viene applicata. È inoltre possibile selezionare **avanzate** nella parte superiore di hello di tooenter questa schermata uno specifico intervallo di origine IP blocco o la porta, ad esempio. Quando si è pronti, selezionare **OK** regola hello toocreate:

![Creare una regola in entrata](./media/nsg-quickstart-portal/create-inbound-rule.png)

Il passaggio finale consiste tooassociate la sicurezza della rete di gruppo con una subnet o un'interfaccia di rete specifici. Associare si hello il gruppo di sicurezza di rete a una subnet. Selezionare **Subnet**, quindi scegliere **Associa**:

![Associare un gruppo di sicurezza di rete con una subnet](./media/nsg-quickstart-portal/associate-subnet.png)

Selezionare la rete virtuale e quindi selezionare la subnet appropriata hello:

![Associare un gruppo di sicurezza di rete con una rete virtuale](./media/nsg-quickstart-portal/select-vnet-subnet.png)

È stato creato un gruppo di sicurezza di rete, è stata creata una regola in entrata che consente il traffico sulla porta 80 ed è stata associata a una subnet. Tutte le macchine virtuali si connettono toothat subnet sono raggiungibili sulla porta 80.

## <a name="more-information-on-network-security-groups"></a>Altre informazioni sui gruppi di sicurezza di rete
Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale. Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse. Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer. bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico. Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).

## <a name="next-steps"></a>Passaggi successivi
In questo esempio è stato creato il traffico HTTP tooallow una semplice regola. È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:

* [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)