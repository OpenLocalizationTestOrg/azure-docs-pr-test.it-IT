---
title: "aaaCreate un Set di scalabilità della macchina virtuale utilizzando hello portale di Azure | Documenti Microsoft"
description: "Distribuire i set di scalabilità tramite il portale di Azure."
keywords: "set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Come toocreate un Set di scalabilità di macchine virtuali con hello portale di Azure
Questa esercitazione viene illustrato come è facile toocreate un Set di scalabilità della macchina virtuale in pochi minuti, utilizzando hello portale di Azure. Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Scegliere l'immagine di macchina virtuale hello Marketplace hello
Dal portale di hello, è possibile distribuire facilmente un set di scalabilità con CentOS, CoreOS, Debian, aprire Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, il Ubuntu Server o immagini di Windows Server.

Passare innanzitutto toohello [portale di Azure](https://portal.azure.com) in un web browser. Fare clic su `New`, cercare `scale set`, quindi selezionare hello `Virtual machine scale set` voce:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Creare set di scalabilità hello
È ora possibile utilizzare le impostazioni predefinite di hello e creare rapidamente il set di scalabilità di hello.

* In hello `Basics` pannello, immettere un nome per il set di scalabilità di hello. Questo nome viene hello base hello FQDN del servizio di bilanciamento del carico hello davanti a set di scalabilità di hello, pertanto assicurarsi nome hello è univoco tra tutti Azure.
* Selezionare il tipo di sistema operativo desiderato, immettere il nome utente desiderato e selezionare il tipo di autenticazione preferito. Se si sceglie una password, deve essere almeno 12 caratteri lungo e soddisfano tre hello quattro seguenti i requisiti di complessità: una lettera minuscola, una lettera maiuscola, un numero e un carattere speciale. Sono disponibili altre informazioni sui [requisiti relativi a nome utente e password](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Se si sceglie `SSH public key`essere Incolla tooonly che la chiave pubblica, non la chiave privata:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Scegliere se si scala hello toolimit impostato gruppo singolo posizionamento tooa o se deve estendersi a più gruppi di posizionamento. Set di scalabilità di hello toospan gruppi posizionamento consentono per scala imposta più di 100 macchine virtuali in capacità (backup too1 000) con determinate limitazioni. Per altre informazioni, vedere [questa documentazione](./virtual-machine-scale-sets-placement-groups.md).
* Immettere il nome del gruppo di risorse desiderato e il percorso e fare clic su `OK`.
* In hello `Virtual machine scale set service settings` pannello: immettere l'etichetta del nome di dominio desiderato (base hello di hello FQDN servizio di bilanciamento del carico hello davanti a set di scalabilità hello). Questa etichetta deve essere univoca nell'ambiente Azure.
* Scegliere l'immagine del disco del sistema operativo desiderata, il numero di istanze e le dimensioni del computer.
* Scegliere il tipo di disco desiderato: gestito o non gestito. Per altre informazioni, vedere [questa documentazione](./virtual-machine-scale-sets-managed-disks.md). Se si sceglie di set di scalabilità hello toohave estendersi su più gruppi di posizionamento, questa opzione non sarà disponibile perché è necessaria per la selezione gruppi di scala set toospan disco gestito.
* Abilitare o disabilitare il ridimensionamento automatico e, se abilitato, configurarlo:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* In hello `Summary` pannello quando la convalida viene eseguita, fare clic su `OK` set di scalabilità di hello toostart di distribuzione.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Connettersi tooa macchina virtuale nel set di scalabilità hello
Se si sceglie toolimit la scala imposta il gruppo di selezione host singolo tooa, quindi il set di scalabilità di hello viene distribuito con NAT regole configurate toolet ci si connette facilmente set di scalabilità di toohello (se non, macchine virtuali di toohello tooconnect nella scala hello impostato, è possibile sia necessario toocreate un jumpbox in hello stessa rete virtuale come set di scalabilità hello). toosee, passare toohello `Inbound NAT Rules` scheda di bilanciamento del carico hello per set di scalabilità hello:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

È possibile connettersi tooeach set della macchina virtuale nella scala hello usando queste regole NAT. Ad esempio, per un set di scalabilità di Windows, se è una regola NAT sulla porta in ingresso 50000, è Impossibile connettersi toothat macchina tramite RDP su `<load-balancer-ip-address>:50000`. Per un set di scalabilità di Linux, si connetterebbe utilizzando il comando hello `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulla modalità scala toodeploy imposta da hello CLI, vedere [questa documentazione](virtual-machine-scale-sets-cli-quick-create.md).

Per informazioni sulla modalità scala toodeploy imposta da PowerShell, vedere [questa documentazione](virtual-machine-scale-sets-windows-create.md).

Per informazioni sulla modalità scala toodeploy imposta da Visual Studio, vedere [questa documentazione](virtual-machine-scale-sets-vs-create.md).

Per informazioni generali, estrarre hello [pagina Panoramica della documentazione per set di scalabilità](virtual-machine-scale-sets-overview.md).

Per informazioni generali, vedere hello [pagina principale per set di scalabilità](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

