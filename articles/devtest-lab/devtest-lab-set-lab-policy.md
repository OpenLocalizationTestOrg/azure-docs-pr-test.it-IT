---
title: criteri di lab aaaManage in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come criteri di lab toodefine, ad esempio macchine Virtuali con dimensioni, massime macchine virtuali per utente e l'automazione di arresto.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Gestire tutti i criteri per un lab in Azure DevTest Labs

Azure DevTest Labs consente di gestire i criteri (impostazioni) in ogni lab, in modo da controllare i costi e ridurre al minimo gli sprechi. In questo articolo illustra in dettaglio dettagliata come tooset tutti i criteri.  

## <a name="set-allowed-virtual-machine-sizes"></a>Impostazione delle dimensioni consentite per le macchine virtuali
Hello criteri per hello impostazione consentito dimensioni delle macchine Virtuali consente toominimize lab rifiuti abilitando toospecify sono consentite le dimensioni delle macchine Virtuali nel lab hello. Se questo criterio è attivato, solo le dimensioni di macchina virtuale da questo elenco possono essere macchine virtuali toocreate utilizzato.

1. Nel lab di hello **criteri di configurazione e** pannello seleziona **dimensioni delle macchine virtuali è consentita**.
   
    ![Dimensioni consentite per le macchine virtuali](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Selezionare **su** tooenable questo criterio, e **Off** toodisable è.

1. Se si abilitano questi criteri, selezionare una o più dimensioni per definire quali possono essere usate per creare macchine virtuali nel lab.

1. Selezionare **Salva**.

## <a name="set-virtual-machines-per-user"></a>Impostazione delle macchine virtuali per utente
criteri per Hello **macchine virtuali per utente** consente un numero massimo di hello toospecify delle macchine virtuali che possono essere creati da un singolo utente. Se un utente tenta di toocreate o attestazione basata su una macchina virtuale quando è stato raggiunto il limite di utenti di hello, un messaggio di errore indica che hello che macchina virtuale non può essere creato/richiesta. 

1. Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per utente**.
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selezionare **Sì** toolimit hello numerose macchine virtuali per utente. Se non si desidera toolimit hello numerose macchine virtuali per utente, selezionare **n**. Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente. 

1. Selezionare **Sì** numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD (disco SSD). Se non si desidera numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD, selezionare **n**. Se si seleziona **Sì**, immettere un valore che indica il numero massimo di hello di macchine virtuali che possono essere creati utilizzando unità SSD. 

1. Selezionare **Salva**.

## <a name="set-virtual-machines-per-lab"></a>Impostazione delle macchine virtuali per lab
criteri per Hello **macchine virtuali per lab** consente numero massimo di hello toospecify delle macchine virtuali che possono essere creati per il lab di hello corrente. Se un utente tenta di toocreate una macchina virtuale quando è stato raggiunto il limite di lab hello, un messaggio di errore indica che hello che macchina virtuale non può essere creata. 

1. Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per lab**.
   
    ![Macchine virtuali per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Selezionare **Sì** toolimit un numero di hello di macchine virtuali per lab. Se non si desidera toolimit un numero di hello di macchine virtuali per lab, selezionare **n**. Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente. 

1. Selezionare **Sì** numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD (disco SSD). Se non si desidera numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD, selezionare **n**. Se si seleziona **Sì**, immettere un valore che indica il numero massimo di hello di macchine virtuali che possono essere creati utilizzando unità SSD. 

1. Selezionare **Salva**.

## <a name="set-auto-shutdown"></a>Impostazione dell'arresto automatico
criteri di arresto automatici Hello consente toominimize lab rifiuti consentono ora di hello toospecify arrestare le macchine virtuali dell'ambiente di test.

1. Nel lab di hello **criteri di configurazione e** pannello seleziona **arresto automatici**.
   
    ![Arresto automatico](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Selezionare **su** tooenable questo criterio, e **Off** toodisable è.

1. Se si abilita questo criterio, è possibile specificare tooshut (ora e fuso orario) di hello verso il basso tutte le macchine virtuali nel lab corrente hello.

1. Specificare **Sì** o **n** per hello opzione toosend un toohello precedente 15 minuti di notifica specificato il tempo di arresto automatici. Se si specifica **Sì**, immettere una notifica di hello webhook URL endpoint tooreceive. Per altre informazioni sui webhook, vedere [Creare un webhook o una funzione API di Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Selezionare **Salva**.

    Per impostazione predefinita, una volta abilitato, questi criteri si applicano tooall macchine virtuali nel lab corrente hello. tooremove questa impostazione di una macchina virtuale specifica, aprire Pannello hello della macchina virtuale e modificare il relativo **arresto automatici** impostazione 

## <a name="set-auto-start"></a>Impostazione dell'avvio automatico
criteri di avvio automatico di Hello consentono toospecify quando hello macchine virtuali nel lab corrente hello deve essere avviato.  

1. Nel lab di hello **criteri di configurazione e** pannello seleziona **avvio automatico**.
   
    ![Avvio automatico](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Selezionare **su** tooenable questo criterio, e **Off** toodisable è.

3. Se si abilita questo criterio, specificare l'ora di inizio pianificata hello, fuso orario e hello giorni della settimana hello per cui hello Applica ora. 

4. Selezionare **Salva**.

    Una volta abilitato, questo criterio non è macchine virtuali tooany applicato automaticamente nel lab corrente hello. tooapply tooa questa impostazione macchina virtuale specifica, della macchina virtuale aprire hello blade e modificare il relativo **avvio automatico** impostazione 

## <a name="set-expiration-date"></a>Impostare la data di scadenza
È possibile impostare la scadenza della data è [creare hello VM](devtest-lab-add-vm.md). In **impostazioni avanzate**, scegliere toospecify icona di calendario hello una data in cui hello VM verrà eliminata automaticamente.  Per impostazione predefinita, hello VM non ha scadenza.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver definito e applicato hello diverse impostazioni di criteri di macchina virtuale per l'ambiente lab, ecco alcuni aspetti tootry successivamente:

* [Comprendere gli indirizzi IP condivisi](devtest-lab-shared-ip.md) -illustra come condiviso IP vengono utilizzati indirizzi in numero di hello toominimize DevTest Labs pubblica IP indirizzi necessari tooconnect tooyour lab di macchine virtuali.
* [Configurare la gestione dei costi](devtest-lab-configure-cost-management.md) -illustra come hello toouse **tendenza mensile del costo stimato** grafico  
  tooview hello stimato costo-to-date del mese corrente e i costi di fine mese hello proiettato.
* [Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace. Questo articolo illustra come toocreate immagine personalizzata da un file VHD.
* [Configurare immagini del Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace. Questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab.
* [Creare una macchina virtuale in un ambiente lab](devtest-lab-add-vm-with-artifacts.md) -illustra come toocreate una macchina virtuale da un'immagine di base (entrambi personalizzato o Marketplace) e come toowork con gli elementi di una macchina virtuale.

