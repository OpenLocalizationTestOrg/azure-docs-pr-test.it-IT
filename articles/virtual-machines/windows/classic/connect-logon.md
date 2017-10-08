---
title: aaaLog su tooa macchina virtuale di Azure classico | Documenti Microsoft
description: Utilizzare hello toolog portale Azure nella macchina virtuale di Windows tooa creato con il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Accedere tooa macchina virtuale Windows usando hello portale di Azure
Nel portale di Azure hello, utilizzare hello **Connetti** pulsante toostart una sessione Desktop remoto e accedere tooa macchina virtuale di Windows.

Si desidera tooconnect tooa VM Linux? Vedere [come toolog nella macchina virtuale tooa che eseguono Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni su come toolog sull'utilizzo delle VM tooa hello Gestione risorse del modello, vedere [qui](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Connettere la macchina virtuale di toohello
1. Accedi toohello portale di Azure.
2. Fare clic sulla macchina virtuale hello che si desidera tooaccess. nome Hello è elencato in hello **tutte le risorse** riquadro.

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. Fare clic su **Connetti** hello barra dei comandi nella parte superiore del dashboard di hello macchina virtuale.

    ![Icona per la macchina virtuale hello della connessione](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Accedere alla macchina virtuale toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Passaggi successivi
* Se hello **Connetti** pulsante è attivo o di altri problemi con connessione Desktop remoto hello, provare a reimpostare la configurazione hello. Fare clic su **reimpostare l'accesso remoto** dal dashboard macchina virtuale hello.

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Per problemi con la password, provare a reimpostarla. Fare clic su **reimpostazione password** lungo hello bordo sinistro del dashboard macchina virtuale, in **supporto + Troubleshooting**.

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Se tali suggerimenti non funzionano o non sono quelli desiderati, vedere [tooa connessioni Desktop remoto di risoluzione dei problemi basato su Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.
