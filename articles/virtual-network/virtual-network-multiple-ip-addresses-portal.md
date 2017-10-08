---
title: gli indirizzi IP aaaMultiple per macchine virtuali di Azure - portale | Documenti Microsoft
description: "Informazioni su come tooassign più gli indirizzi IP tooa macchina virtuale utilizzando hello portale di Azure | Gestore delle risorse."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Assegnare più computer di toovirtual gli indirizzi IP utilizzando hello portale di Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
In questo articolo viene illustrato come una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager hello utilizzando toocreate hello portale di Azure. Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello. ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creare una macchina virtuale con più indirizzi IP

Se si desidera toocreate una macchina virtuale con più indirizzi IP o un indirizzo IP privato statico, è necessario crearlo tramite PowerShell o hello CLI di Azure. Scegliere come hello PowerShell o le opzioni di CLI in cima di hello toolearn questo articolo. È possibile creare una macchina virtuale con un singolo indirizzo IP privato dinamico e (facoltativamente) un singolo indirizzo IP pubblico tramite il portale di hello seguendo procedure hello hello [creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [creare una VM Linux](../virtual-machines/linux/quick-create-portal.md) articoli. Dopo aver creato hello VM, è possibile modificare il tipo di indirizzo IP hello da toostatic dinamica e aggiungere altri indirizzi IP tramite il portale di hello eseguendo i passaggi in hello [tooa VM gli indirizzi di Aggiungi IP](#add) sezione di questo articolo.

## <a name="add"></a>Aggiungere tooa di indirizzi IP VM

È possibile aggiungere pubblica e privata IP indirizzi tooa NIC completando i passaggi di hello che seguono. Hello esempi in hello nelle sezioni che seguono si presuppone che si dispone di una macchina virtuale con le configurazioni IP hello tre descritte in hello [scenario](#Scenario) in questo articolo, ma non è necessario eseguire.

### <a name="coreadd"></a>Passaggi di base

1. Sfoglia toohello portale di Azure all'indirizzo https://portal.azure.com e accedere, se necessario.
2. Nel portale di hello, fare clic su **più servizi** > tipo *macchine virtuali* in hello casella filtro e quindi fare clic su **macchine virtuali**.
3. In hello **macchine virtuali** pannello, fare clic sulla macchina virtuale che si desidera tooadd IP indirizzi a hello. Fare clic su **interfacce di rete** nel pannello macchine virtuali hello che viene visualizzato e quindi hello rete interfaccia IP hello tooadd indirizzi per. Nell'esempio hello nella hello seguente immagine, hello NIC denominato *myNIC* dalla macchina virtuale denominata hello *myVM* è selezionata:

    ![Interfaccia di rete](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Nel pannello hello che viene visualizzata per hello NIC selezionato, fare clic su **le configurazioni IP**.

Hello completato i passaggi in una delle sezioni hello che seguono, in base al tipo di hello dell'indirizzo IP è tooadd.

### <a name="add-a-private-ip-address"></a>**Aggiungere un indirizzo IP privato**

Completare i seguenti passaggi tooadd un nuovo indirizzo IP privato hello:

1. Hello completato i passaggi in hello [passaggi di base](#coreadd) sezione di questo articolo.
2. Fare clic su **Aggiungi**. In hello **configurazione IP aggiungere** pannello visualizzato, creare una configurazione IP denominata *IPConfig 4* con *10.0.0.7* come un *statico* IP privato di indirizzi, quindi fare clic su **OK**.

    > [!NOTE]
    > Quando si aggiunge un indirizzo IP statico, è necessario specificare un indirizzo valido inutilizzato in hello subnet hello che è connessa al. Se l'indirizzo di hello selezionato non è disponibile, il portale di hello viene visualizzata una X per l'indirizzo IP hello e sarà necessario tooselect uno diverso.

3. Dopo aver selezionato OK, pannello hello verrà chiuso e verrà visualizzato hello nuova configurazione IP elencata. Fare clic su **OK** tooclose hello **configurazione IP aggiungere** blade.
4. È possibile fare clic su **Aggiungi** tooadd configurazioni aggiuntive di IP, o chiudere tutti aprire gli indirizzi IP di pannelli toofinish aggiunta.
5. Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.

### <a name="add-a-public-ip-address"></a>Aggiungere un indirizzo IP pubblico

Associando un tooeither di risorsa indirizzo IP pubblico, una nuova configurazione IP o una configurazione IP esistente, viene aggiunto un indirizzo IP pubblico.

> [!NOTE]
> Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.
> 

### <a name="create-public-ip"></a>Creare una risorsa indirizzo IP pubblico

Un indirizzo IP pubblico consiste in una singola impostazione per una risorsa indirizzo IP pubblico. Se si dispone di una risorsa di indirizzo IP pubblica che non è attualmente associato tooan la configurazione IP che si desidera tooassociate tooan la configurazione IP, ignorare hello alla procedura seguente e completare i passaggi di hello nelle sezioni che seguono, hello necessari. Se non si dispone di una risorsa di indirizzo IP pubblica disponibile, completare hello seguendo i passaggi toocreate uno:

1. Sfoglia toohello portale di Azure all'indirizzo https://portal.azure.com e accedere, se necessario.
3. Nel portale di hello, fare clic su **New** > **rete** > **indirizzo IP pubblico**.
4. In hello **creare l'indirizzo IP pubblico** blade che viene visualizzata, immettere un **nome**, selezionare un **assegnazione di indirizzi IP** tipo, un **sottoscrizione**, **Gruppo di risorse**e un **percorso**, quindi fare clic su **crea**, come illustrato nella seguente immagine hello:

    ![Creare una risorsa indirizzo IP pubblico](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Hello completato i passaggi in una delle sezioni hello che seguono tooassociate hello pubblica risorsa tooan IP configurazione degli indirizzi IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Associare hello pubblica risorsa tooa nuovo IP configurazione degli indirizzi IP

1. Hello completato i passaggi in hello [passaggi di base](#coreadd) sezione di questo articolo.
2. Fare clic su **Aggiungi**. In hello **configurazione IP aggiungere** pannello visualizzato, creare una configurazione IP denominata *IPConfig 4*. Abilitare hello **indirizzo IP pubblico** e di selezionarne un'esistente, disponibile pubblica risorsa indirizzo IP hello **scegliere l'indirizzo IP pubblico** pannello visualizzato.

    Dopo aver selezionato hello pubblica la risorsa indirizzo IP, fare clic su **OK** e blade hello verrà chiusa. Se non si dispone di un indirizzo IP pubblico esistente, è possibile creare uno completando i passaggi hello hello [creare una risorsa di indirizzo IP pubblica](#create-public-ip) sezione di questo articolo. 

3. Revisione hello nuova configurazione IP. Anche se non è stato assegnato in modo esplicito un indirizzo IP privato, uno è stato assegnato automaticamente la configurazione IP toohello, poiché tutte le configurazioni IP devono avere un indirizzo IP privato.
4. È possibile fare clic su **Aggiungi** tooadd configurazioni aggiuntive di IP, o chiudere tutti aprire gli indirizzi IP di pannelli toofinish aggiunta.
5. Aggiungere hello private IP indirizzo toohello macchina virtuale sistema operativo completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzo toohello del sistema operativo.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Associare hello pubblica risorsa tooan esistente IP configurazione degli indirizzi IP

1. Hello completato i passaggi in hello [passaggi di base](#coreadd) sezione di questo articolo.
2. Fare clic su desiderato tooadd hello pubblica risorsa indirizzo IP per la configurazione IP hello.
3. Nel Pannello di IPConfig hello che viene visualizzato, fare clic su **indirizzo IP**.
4. In hello **scegliere l'indirizzo IP pubblico** pannello visualizzato, selezionare un indirizzo IP pubblico.
5. Fare clic su **salvare** e pannelli hello verranno chiusa. Se non si dispone di un indirizzo IP pubblico esistente, è possibile creare uno completando i passaggi hello hello [creare una risorsa di indirizzo IP pubblica](#create-public-ip) sezione di questo articolo.
3. Revisione hello nuova configurazione IP.
4. È possibile fare clic su **Aggiungi** tooadd configurazioni aggiuntive di IP, o chiudere tutti aprire gli indirizzi IP di pannelli toofinish aggiunta. Non aggiungere hello pubblica IP indirizzo toohello del sistema operativo.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
