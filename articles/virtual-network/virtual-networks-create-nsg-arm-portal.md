---
title: gruppi di sicurezza di rete aaaManage - portale di Azure | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete toomanage utilizzando hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a>Gestire i gruppi di sicurezza di rete usando hello portale di Azure

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

esempio Hello PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale. Hello passaggi sottostanti utilizzano **RG NSG** come nome hello del modello di hello gruppo di risorse hello è stato distribuito.

## <a name="create-hello-nsg-frontend-nsg"></a>Creare hello NSG front-end di NSG
hello toocreate **front-end di NSG** gruppo come illustrato nell'esempio hello di cui sopra, procedura hello riportata di seguito.

1. Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.
2. Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. In hello **gruppi di sicurezza di rete** pannello, fare clic su **Aggiungi**.
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. In hello **Crea gruppo di sicurezza di rete** pannello, creare un gruppo denominato *front-end di NSG* in hello *RG NSG* gruppo di risorse e quindi fare clic su **crea**.
   
    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Creare regole in un gruppo di sicurezza di rete esistente
le regole di toocreate in un gruppo esistente dal portale di Azure hello procedura hello riportata di seguito.

1. Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.
2. Selezionare nell'elenco hello di NSGs **front-end di NSG** > **regole di sicurezza in ingresso**
   
    ![Portale di Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Nell'elenco di hello di **sicurezza regole connessioni in entrata**, fare clic su **Aggiungi**.
   
    ![Portale di Azure - Aggiungi regola](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. In hello **Aggiungi regola di sicurezza in ingresso** pannello, creare una regola denominata *regola web* con priorità di *200* che consente l'accesso tramite *TCP* tooport *80* tooany macchina virtuale da qualsiasi origine e quindi fare clic su **OK**. Notare che la maggior parte di queste impostazioni ha già i valori predefiniti.
   
    ![Portale di Azure - Impostazioni delle regole](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Regola di nuovo hello in hello gruppo sarà presente dopo alcuni secondi.
   
    ![Portale di Azure - Nuova regola](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Ripetere i passaggi too6 toocreate una regola in ingresso denominata *rdp regola* con una priorità di *250* che consente l'accesso tramite *TCP* tooport *3389* tooany macchina virtuale da qualsiasi origine.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Associare subnet front-end di hello NSG toohello
1. Fare clic su **Sfoglia >** > **Gruppi di risorse** > **RG-NSG**.
2. In hello **RG NSG** pannello, fare clic su **...**   >  **TestVNet**.
   
    ![Portale di Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Front-end di NSG**.
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. In hello **front-end** pannello, fare clic su **salvare**.
   
    ![Portale di Azure - Impostazioni della subnet](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Creare hello NSG back-end di NSG
hello toocreate **back-end di NSG** NSG e associarlo toohello **back-end** subnet, seguire hello passaggi riportati di seguito.

1. Passaggi di ripetizione hello [hello Crea gruppo di front-end di NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un gruppo denominato *back-end di gruppo*
2. Passaggi di ripetizione hello [creare regole in un gruppo esistente](#Create-rules-in-an-existing-NSG) toocreate hello **in ingresso** regole riportate nella tabella hello riportato di seguito.
   
   | Regola in entrata | Regola in uscita |
   | --- | --- |
   | ![Portale di Azure - Regola in entrata](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portale di Azure - Regola in uscita](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Hello ripetere i passaggi [associare subnet front-end di hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **back-end di NSG** NSG toohello **back-end** subnet.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[gestire NSGs esistente](virtual-network-manage-nsg-arm-portal.md)
* [Abilitare la registrazione](virtual-network-nsg-manage-log.md) per i gruppi di sicurezza di rete.

