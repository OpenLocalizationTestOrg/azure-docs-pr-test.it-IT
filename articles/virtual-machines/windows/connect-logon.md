---
title: aaaConnect tooa macchina virtuale Windows Server | Documenti Microsoft
description: Informazioni su come tooconnect e accedere utilizzando la macchina virtuale Windows tooa hello Azure portal e hello Gestione risorse modello di distribuzione.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows
Si userà hello **Connetti** pulsante hello Azure toostart portale una sessione di Desktop remoto (RDP) da un desktop di Windows. Prima connettersi macchina virtuale toohello, quindi si accede.

Se si sta tentando di tooconnect tooa macchina virtuale Windows da un Mac, è necessario un client RDP per Mac come tooinstall [Desktop remoto Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Connettere la macchina virtuale di toohello
1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **macchine virtuali**.
3. Selezionare macchina virtuale hello hello elenco.
4. Nel Pannello di hello per la macchina virtuale hello, fare clic su **Connetti**.
   
    ![Schermata di hello che Mostra portale Azure come tooconnect tooyour macchina virtuale.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Se hello **Connetti** pulsante nel portale di hello è disattivata e non si è connessi tooAzure tramite un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN Site-to-Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connessione, è necessario toocreate e assegnare la macchina virtuale un indirizzo IP pubblico per poter utilizzare il protocollo RDP. Altre informazioni sono disponibili in [Indirizzi IP pubblici in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Accedere alla macchina virtuale toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Passaggi successivi
Se si verificano problemi quando si tenta di tooconnect, vedere [le connessioni Desktop remoto di risolvere i problemi](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.

