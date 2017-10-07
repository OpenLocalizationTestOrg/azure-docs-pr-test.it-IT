---
title: "hello aaaInstall servizio di mobilità per la replica di server fisici tooAzure | Documenti Microsoft"
description: "In questo articolo viene descritto come tooinstall hello agente del servizio di mobilità nei server fisici, replica tooAzure con il servizio di Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Passaggio 9: Installare il servizio di mobilità hello


In questo articolo viene descritto come componente del servizio Mobility di hello tooinstall durante la replica locale tooAzure server fisici Windows/Linux, usando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

servizio di mobilità Hello acquisisce scritture di dati in un computer e li inoltra toohello server di elaborazione. È necessario installarlo in ogni server che si desidera tooreplicate tooAzure.

È possibile installare manualmente il servizio di mobilità hello o utilizzando un'installazione push da hello a elaborare il ripristino del sito quando è abilitata la replica di server o utilizzando uno strumento come System Center Configuration Manager. Se si utilizza l'installazione push, il servizio di hello è installato nel server di hello quando si abilita la replica.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Eseguire l'installazione manuale

1. Controllare hello [prerequisiti](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) per l'installazione manuale.
2. Seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) per l'installazione manuale tramite il portale di hello.
3. Se si preferisce tooinstall dalla riga di comando hello, seguire [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installare dal server di elaborazione hello

Se si desidera toopush hello installazione del servizio Mobility dal server di elaborazione hello quando si abilita la replica per un computer, è necessario un account che possa essere usato da hello processo server tooaccess hello macchina. account di Hello viene utilizzato solo per l'installazione push hello.

1. Se non è stato ancora creato un account, eseguire questa operazione usando le linee guida seguenti:

    - È possibile usare un account di dominio o locale
    - Per Windows, se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. toodo, in hello registrare in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, aggiungere una voce DWORD hello **LocalAccountTokenFilterPolicy**, con un valore pari a 1.
    - Se si desidera una voce del Registro di sistema di hello tooadd per Windows da CLI, digitare:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Per Linux, account hello devono essere radice nel server di hello origine Linux.

2. Seguire quindi [queste istruzioni](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se si desidera servizio di mobilità toopush hello in macchine virtuali in esecuzione Windows o Linux.

## <a name="other-installation-methods"></a>Altri metodi di installazione

- [Informazioni su](site-recovery-install-mobility-service-using-sccm.md) installazione del servizio di mobilità hello con Configuration Manager
- [Ulteriori informazioni](site-recovery-automate-mobility-service-install.md) sull'installazione con la piattaforma DSC di Automazione di Azure.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 10: abilitare la replica](physical-walkthrough-enable-replication.md)
