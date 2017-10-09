---
title: aaaCreate una macchina virtuale con un indirizzo IP pubblico statico - portale di Azure | Documenti Microsoft
description: Informazioni su come una macchina virtuale con un indirizzo pubblico IP statico usando toocreate hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Creare una macchina virtuale con un indirizzo IP pubblico statico utilizzando hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modello](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Creare una VM con un IP pubblico statico

toocreate una macchina virtuale con un indirizzo IP pubblico statico di indirizzi in hello portale di Azure completo hello alla procedura seguente:

1. Da un browser, passare toohello [portale di Azure](https://portal.azure.com) e, se necessario, accedere con l'account di Azure.
2. Nell'angolo superiore sinistro di hello del portale hello, fare clic su **New**>>**calcolo**>**Windows Server 2012 R2 Datacenter**.
3. In hello **selezionare un modello di distribuzione** selezionare **Gestione risorse** e fare clic su **crea**.
4. In hello **nozioni di base** pannello, immettere le informazioni di VM hello, come illustrato di seguito e quindi fare clic su **OK**.
   
    ![Portale di Azure: Nozioni di base](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. In hello **scegliere una dimensione** pannello, fare clic su **A1 Standard** come illustrato di seguito, quindi fare clic su **selezionare**.
   
    ![Portale di Azure: Scegliere una dimensione](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. In hello **impostazioni** pannello, fare clic su **indirizzo IP pubblico**, quindi nella hello **creare l'indirizzo IP pubblico** pannello, in **assegnazione**, fare clic su **Statico** come illustrato di seguito. Fare quindi clic su **OK**.
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. In hello **impostazioni** pannello, fare clic su **OK**.
8. Hello revisione **riepilogo** pannello, come illustrato di seguito e quindi fare clic su **OK**.
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Si noti nuovo riquadro di hello nel dashboard.
   
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Una volta creato, hello VM hello **impostazioni** pannello verrà visualizzato come illustrato di seguito
    
    ![Portale di Azure: Creare l'indirizzo IP pubblico](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

