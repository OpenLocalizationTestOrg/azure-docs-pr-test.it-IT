---
title: criteri di base lab aaaManage in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come tooset alcuni criteri base hello (impostazioni) per un laboratorio di DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Gestire i criteri di base di un lab in Azure DevTest Labs

Azure DevTest Labs consente toocontrol costo e ridurre al minimo i rifiuti nei propri laboratori dalla gestione dei criteri (impostazioni) per ogni ambiente lab. In questo articolo, iniziare con i criteri da apprendere come tooset due dei criteri più critici hello - limitazione hello numero di macchine virtuali (VM) che può essere create o richiesto da un singolo utente e la configurazione automatica-arresto. tooview come tooset ogni criterio lab, vedere l'articolo hello, [definire criteri lab in Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Accesso ai criteri di lab in Azure DevTest Labs
Hello passaggi seguenti consentono di configurare i criteri per un ambiente lab in Azure DevTest Labs:

i criteri di hello tooview (ed eventualmente) per un ambiente lab, eseguire la procedura seguente:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

1. Elenco dei laboratori hello selezionare lab desiderato hello.   

1. Selezionare **Configuration and policies** (Configurazione e criteri).

    ![Pannello Impostazioni criteri](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Hello **criteri di configurazione e** pannello contiene un menu di impostazioni che è possibile specificare. Questo articolo vengono illustrate solo le impostazioni di hello per **macchine virtuali per utente** e **arresto automatici**. toolearn su hello rimanenti impostazioni, vedere [gestire tutti i criteri per un ambiente lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Impostazione delle macchine virtuali per utente
criteri per Hello **macchine virtuali per utente** consente un numero massimo di hello toospecify delle macchine virtuali che possono essere creati da un singolo utente. Se un utente tenta di toocreate o attestazione basata su una macchina virtuale quando è stato raggiunto il limite di utenti di hello, un messaggio di errore indica che hello che macchina virtuale non può essere creato/richiesta. 

1. Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per utente**.
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selezionare **Sì** toolimit hello numerose macchine virtuali per utente. Se non si desidera toolimit hello numerose macchine virtuali per utente, selezionare **n**. Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente. 

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

## <a name="next-steps"></a>Passaggi successivi

- [Definire i criteri di laboratorio in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informazioni su come toomodify altri criteri lab 
