---
title: NSGs aaaManage utilizzando hello portale di Azure | Documenti Microsoft
description: Informazioni su come toomanage NSGs utilizzando hello portale di Azure esistente.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Gestire tramite il portale di hello NSGs

> [!div class="op_single_selector"]
> * [Portale](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Recuperare le informazioni
È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.

### <a name="view-existing-nsgs"></a>Visualizzare NSG esistenti

tooview tutti esistente NSGs in una sottoscrizione, hello completo alla procedura seguente:

1. Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.

2. Fare clic su **Sfoglia>** > **Gruppi di sicurezza di rete**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Controllare l'elenco hello di NSGs hello **gruppi di sicurezza di rete** blade.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Visualizzare gli NSG in un gruppo di risorse

elenco di hello tooview di NSGs in hello **RG NSG** gruppo di risorse, hello completo alla procedura seguente:

1. Fare clic su **Gruppi di risorse >** > **RG-NSG** > **...**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Nell'elenco di hello delle risorse, cercare gli elementi la visualizzazione dell'icona NSG hello, come illustrato nell'hello **risorse** blade riportata di seguito.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Elencare tutte le regole per un NSG

le regole di hello tooview di un gruppo denominato **front-end di NSG**completa hello i passaggi seguenti:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.

2. In hello **impostazioni** scheda, fare clic su **sicurezza regole connessioni in entrata**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Hello **sicurezza regole connessioni in entrata** pannello viene visualizzato come illustrato di seguito.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. In hello **impostazioni** scheda, fare clic su **regole di sicurezza in uscita** toosee hello regole in uscita.

    > [!NOTE]
    > tooview regole predefinite, fare clic su hello **regole predefinite** sull'icona nella parte superiore di hello del pannello hello che visualizza le regole di hello.
    >

### <a name="view-nsgs-associations"></a>Visualizzare le associazioni di NSG

tooview hello quali risorse **front-end di NSG** NSG è hello completo, associato alla procedura seguente:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.

2. In hello **impostazioni** scheda, fare clic su **subnet** tooview sono le subnet associata toohello gruppo.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. In hello **impostazioni** scheda, fare clic su **interfacce di rete** tooview quali schede di rete sono associate toohello gruppo.

## <a name="manage-rules"></a>Gestire le regole
È possibile aggiungere regole tooan gruppo esistente, modificare le regole esistenti e rimuovere le regole.

### <a name="add-a-rule"></a>Aggiungere una regola
tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, hello completo alla procedura seguente:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.
2. In hello **impostazioni** scheda, fare clic su **sicurezza regole connessioni in entrata**.
3. In hello **sicurezza regole connessioni in entrata** pannello, fare clic su **Aggiungi**. Quindi, nel hello **Aggiungi regola di sicurezza in ingresso** pannello riempire i valori hello, come illustrato di seguito e quindi fare clic su **OK**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Dopo alcuni secondi, si noti nuova regola di hello in hello **sicurezza regole connessioni in entrata** blade.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Modificare una regola
regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** hello completo, solo alla procedura seguente:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.
2. In hello **impostazioni** , fare clic sulla regola hello creato in precedenza.
3. In hello **https consentire** blade, hello modifica **origine** proprietà come illustrato di seguito e quindi fare clic su **salvare**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Eliminare una regola

toodelete hello regola creata in precedenza, completo hello alla procedura seguente:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.
2. In hello **impostazioni** , fare clic sulla regola hello creato in precedenza.
3. In hello **https consentire** pannello, fare clic su **eliminare**, quindi fare clic su **Sì**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Gestire le associazioni
È possibile associare un gruppo toosubnets e schede di rete. È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.

### <a name="associate-an-nsg-tooa-nic"></a>Associare un tooa gruppo NIC
hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, hello completo alla procedura seguente:

1. Da hello **gruppi di sicurezza di rete** pannello o hello **risorse** pannello illustrato in precedenza, fare clic su **front-end di NSG**.
2. In hello **impostazioni** scheda, fare clic su **interfacce di rete** > **associare** > **TestNICWeb1**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Annullare l'associazione tra un NSG e una NIC

hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, hello completo alla procedura seguente:

1. Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. In hello **TestNICWeb1** pannello, fare clic su **modificare la sicurezza...**   >  **Nessuno**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Inoltre, è possibile utilizzare questo tooany NIC di blade tooassociate hello gruppo esistente.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Annullare l'associazione tra un NSG e una subnet

hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, hello completo alla procedura seguente:

1. Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestVNet**.

2. In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Nessuno**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. In hello **front-end** pannello, fare clic su **salvare**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Associare una subnet tooa NSG

hello tooassociate **front-end di NSG** NSG toohello **FronEnd** subnet nuovamente, hello completo alla procedura seguente:

1. Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **TestVNet**.
2. In hello **impostazioni** pannello, fare clic su **subnet** > **front-end** > **il gruppo di sicurezza di rete**  >  **Front-end di NSG**.
3. In hello **front-end** pannello, fare clic su **salvare**.

> [!NOTE]
> È inoltre possibile associare una subnet tooa NSG da thh NSG **impostazioni** blade.
>

## <a name="delete-an-nsg"></a>Eliminare un gruppo di sicurezza di rete
È possibile eliminare un gruppo solo se non è associata la risorsa tooany. toodelete un gruppo, hello completo alla procedura seguente:.

1. Dal portale di Azure hello, fare clic su **gruppi di risorse >** > **RG NSG** > **...**   >  **Front-end di NSG**.
2. In hello **impostazioni** pannello, fare clic su **interfacce di rete**.
3. Se sono presenti eventuali schede di rete elencate, fare clic su hello NIC e seguire i passaggi 2 nel [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC).
4. Ripetere il passaggio 3 per ogni NIC.
5. In hello **impostazioni** pannello, fare clic su **subnet**.
6. Se sono presenti subnet elencati, fare clic su subnet hello e seguire i passaggi 2 e 3 in [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet).
7. Scorre verso sinistra toohello **front-end di NSG** pannello, quindi fare clic su **eliminare** > **Sì**.

    ![Portale di Azure - Gruppi di sicurezza di rete](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Passaggi successivi
* [Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.
