---
title: indirizzi IP privati aaaConfigure per le macchine virtuali - portale di Azure | Documenti Microsoft
description: Informazioni su come indirizzi IP privati tooconfigure per macchine virtuali tramite hello portale di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Configurare gli indirizzi IP privati per una macchina virtuale utilizzando hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Portale di Azure (classico)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (Classic)](virtual-networks-static-private-ip-classic-ps.md) (PowerShell (classico))
> * [Interfaccia della riga di comando di Azure (versione classica)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [gestire l'indirizzo IP privato statico in modello di distribuzione classica hello](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

procedura di esempio Hello seguente prevede un ambiente semplice già creato. Se si desidera passaggi hello toorun così come sono visualizzati in questo documento, innanzitutto compilare descritto nell'ambiente di test di hello [creare una rete virtuale](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Come gli indirizzi toocreate una macchina virtuale per il testing di indirizzo IP privato statico
È possibile impostare un indirizzo IP privato statico durante la creazione di una macchina virtuale in modalità di distribuzione di gestione risorse di hello hello utilizzando hello portale di Azure. È necessario creare innanzitutto hello macchina virtuale, quindi impostare il relativo toobe IP privato statico.

una macchina virtuale denominata toocreate *DNS01* in hello *front-end* subnet di una rete virtuale denominata *TestVNet*, attenersi alla procedura hello riportata di seguito.

1. Da un browser, passare toohttp://portal.azure.com e, se necessario, per accedere all'account Azure.
2. Fare clic su **NEW** > **calcolo** > **Windows Server 2012 R2 Datacenter**, si noti che hello **selezionare un modello di distribuzione** elenco già illustrato **Gestione risorse**, quindi fare clic su **crea**, come illustrato nella figura che segue hello.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. In hello **nozioni di base** pannello, immettere il nome di hello di hello VM toobe creato (*DNS01* nello scenario di esempio), hello account amministratore locale e la password, come illustrato nella figura che segue hello.
   
    ![Pannello Nozioni di base](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Verificare che hello **percorso** selezionato è *Stati Uniti centro*, quindi fare clic su **selezionare esistente** in **gruppo di risorse**, quindi fare clic su **Gruppo di risorse** nuovamente, quindi fare clic su *TestRG*, quindi fare clic su **OK**.
   
    ![Pannello Nozioni di base](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. In hello **scegliere una dimensione** pannello seleziona **A1 Standard**, quindi fare clic su **selezionare**.
   
    ![Pannello Scegliere una dimensione](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. Nel **impostazioni** pannello, vengono impostate hello assicurarsi di verificare le proprietà seguenti vengono impostate con i valori hello seguenti e quindi fare clic su **OK**.
   
    -**Account di archiviazione**: *vnetstorage*
   
   * **Rete**: *TestVNet*
   * **Subnet**: *FrontEnd*
     
     ![Pannello Scegliere una dimensione](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. In hello **riepilogo** pannello, fare clic su **OK**. Si noti hello sezione riportata di seguito visualizzati nel dashboard.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Come indirizzo IP privato statico tooretrieve informazioni sull'indirizzo di una macchina virtuale
tooview hello private informazioni indirizzi IP statici per hello macchina virtuale creata con i passaggi di hello precedenti, eseguire i passaggi di hello riportato di seguito.

1. Dal portale di Azure di Azure hello, fare clic su **Esplora tutto** > **macchine virtuali** > **DNS01** > **tutti impostazioni** > **interfacce di rete** e quindi fare clic su hello solo l'interfaccia di rete elencata.
   
    ![Distribuzione di un riquadro VM](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. In hello **interfaccia di rete** pannello, fare clic su **tutte le impostazioni** > **gli indirizzi IP** e notifica hello **assegnazione** e **Indirizzo IP** valori.
   
    ![Distribuzione di un riquadro VM](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Come un indirizzo IP privato statico tooadd indirizzo tooan macchina virtuale esistente
tooadd un statico privato IP indirizzo toohello macchina virtuale creata seguendo i passaggi di hello sopra riportati, procedura hello riportata di seguito:

1. Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **statico** in **assegnazione**.
2. Digitare *192.168.1.101* per **Indirizzo IP** e quindi fare clic su **Salva**.
   
    ![Creare VM nel portale di Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Se dopo aver fatto clic **salvare** l'assegnazione di hello è ancora impostato troppo**dinamica**, significa che l'indirizzo IP hello digitato è già in uso. Provare un indirizzo IP diverso.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Come tooremove un indirizzo IP privato statico di indirizzi da una macchina virtuale
tooremove hello indirizzo IP privato statico dalla macchina virtuale creata in precedenza, hello completare hello seguente passaggio:

Da hello **gli indirizzi IP** pannello illustrato in precedenza, fare clic su **dinamica** in **assegnazione**, quindi fare clic su **salvare**.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .
* Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consultare hello [API REST per IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).

