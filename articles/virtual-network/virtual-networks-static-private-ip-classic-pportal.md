---
title: indirizzi IP privati aaaConfigure per le macchine virtuali (classico) - portale di Azure | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per le macchine virtuali (classico) utilizzando hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Configurare gli indirizzi IP privati per una macchina virtuale (classico) utilizzando hello portale di Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [gestire un indirizzo IP privato statico nel modello di distribuzione di gestione risorse di hello](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

procedura di esempio Hello seguente prevede un ambiente semplice già creato. Se si desidera passaggi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Come toospecify un indirizzo IP privato statico di indirizzi durante la creazione di una macchina virtuale
una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet* con un indirizzo IP privato statico di *192.168.1.101*, attenersi alla procedura hello riportata di seguito:

1. Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.
2. Fare clic su **NEW** > **calcolo** > **Windows Server 2012 R2 Datacenter**, si noti che hello **selezionare un modello di distribuzione** elenco già illustrato **classico**, quindi fare clic su **crea**.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. In hello **creare VM** pannello, immettere il nome di hello di hello VM toobe creato (*DNS01* nello scenario di esempio), hello account amministratore locale e la password.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Fare clic su **Configurazione facoltativa** > **Rete** > **Rete virtuale**, poi fare clic su **TestVNet**. Se **TestVNet** non è disponibile, assicurarsi che si sta eseguendo hello *centrale Usa* posizione e aver creato l'ambiente di testing hello descritto all'inizio di hello di questo articolo.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. In hello **rete** pannello, verificare che hello la subnet attualmente selezionata è *front-end*, quindi fare clic su **gli indirizzi IP**in **assegnazionedegliindirizziIP** fare clic su **statico**, quindi immettere *192.168.1.101* per **indirizzo IP** come illustrato di seguito.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Fare clic su **OK** in hello **gli indirizzi IP** pannello, quindi fare clic su **OK** in hello **rete** pannello e fare clic su **OK**in hello **configurazione facoltativa** blade.
7. In hello **creare VM** pannello, fare clic su **crea**. Si noti hello sezione riportata di seguito visualizzati nel dashboard.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale
tooview hello private informazioni indirizzi IP statici per hello macchina virtuale creata con i passaggi di hello precedenti, eseguire i passaggi di hello riportato di seguito.

1. Dal portale di Azure di Azure hello, fare clic su **Esplora tutto** > **macchine virtuali (classico)** > **DNS01**  >   **Tutte le impostazioni** > **gli indirizzi IP** e notare hello assegnazione di indirizzi IP e l'indirizzo IP, come illustrato di seguito.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale
tooremove hello indirizzo IP privato statico dalla macchina virtuale creata in precedenza, hello procedura hello riportata di seguito.

1. Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **dinamica** toohello destra **assegnazione di indirizzi IP**, quindi fare clic su **salvare**e quindi Fare clic su **Sì**.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente
tooadd un statico privato IP indirizzo toohello macchina virtuale creata seguendo i passaggi di hello sopra riportati, procedura hello riportata di seguito:

1. Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **statico** toohello destra **assegnazione di indirizzi IP**.
2. Digitare *192.168.1.101* per **indirizzo IP**, fare clic su **Salva**, quindi fare clic su **Sì**.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

