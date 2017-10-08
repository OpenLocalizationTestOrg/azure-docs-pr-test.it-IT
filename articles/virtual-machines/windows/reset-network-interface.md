---
title: aaaHow tooreset di interfaccia di rete per la macchina virtuale Windows Azure | Documenti Microsoft
description: Viene illustrato come tooreset interfaccia di rete per la macchina virtuale Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Come tooreset interfaccia di rete per la macchina virtuale Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

È Impossibile connettersi tooMicrosoft macchina virtuale Windows Azure (VM) dopo aver disabilitato predefinito hello interfaccia di rete (NIC) o si imposta manualmente un indirizzo IP statico per una scheda di rete hello. Questo articolo illustra come tooreset hello interfaccia di rete per la macchina virtuale Windows Azure, che consentirà di risolvere il problema di connessione remota hello.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Reimpostare l'interfaccia di rete

### <a name="for-classic-vms"></a>Per VM classiche

rete tooreset interfaccia, seguire questi passaggi:

1.  Passare toohello [portale di Azure]( https://ms.portal.azure.com).
2.  Selezionare **Macchine virtuali (classiche)**.
3.  Seleziona hello interessate macchina virtuale.
4.  Selezionare **Indirizzi IP**.
5.  Se hello **assegnazione IP privato** non **statico**, modificarlo troppo**statico**.
6.  Hello modifica **indirizzo IP** indirizzo IP tooanother disponibile in hello Subnet.
7.  Selezionare Salva.
8.  macchina virtuale Hello riavvierà tooinitialize hello nuovo NIC toohello sistema.
9.  Provare a tooRDP tooyour macchina. Se ha esito positivo, è possibile modificare hello IP privato indirizzo back toohello originale se si desidera. In caso contrario è possibile mantenerlo. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Per le VM distribuite nel modello di gruppo di risorse

1.  Passare toohello [portale di Azure]( https://ms.portal.azure.com).
2.  Seleziona hello interessate macchina virtuale.
3.  Selezionare **Interfacce di rete**.
4.  Selezionare hello che associato all'interfaccia di rete con il computer
5.  Selezionare **Configurazioni IP**.
6.  Selezionare IP hello. 
7.  Se hello **assegnazione IP privato** non **statico**, modificarlo troppo**statico**.
8.  Hello modifica **indirizzo IP** indirizzo IP tooanother disponibile in hello Subnet.
9. macchina virtuale Hello riavvierà tooinitialize hello nuovo NIC toohello sistema.
10. Provare a tooRDP tooyour macchina. Se ha esito positivo, è possibile modificare hello IP privato indirizzo back toohello originale se si desidera. In caso contrario è possibile mantenerlo. 

## <a name="delete-hello-unavailable-nics"></a>Eliminare hello schede di rete non disponibile
Dopo che è possibile macchina toohello desktop remoto, è necessario eliminare hello precedente NIC tooavoid hello potenziale problema:

1.  Aprire Gestione dispositivi.
2.  Selezionare **Vista** > **Mostra dispositivi nascosti**.
3.  Selezionare **Schede di rete**. 
4.  Controllo per le schede di hello denominata come "Scheda di rete Microsoft Hyper-V".
5.  Si potrebbe vedere una scheda non disponibile che appare in grigio. Il pulsante destro adapter hello e quindi scegliere Disinstalla.

    ![immagine di Hello di hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Disinstallare solo le schede disponibili hello con nome hello "Scheda di rete Microsoft Hyper-V". Se si disinstalla uno qualsiasi dei hello altre schede nascoste, potrebbe provocare altri problemi.
    >
    >

6.  Ora tutte le schede disponibili devono essere eliminate dal sistema.