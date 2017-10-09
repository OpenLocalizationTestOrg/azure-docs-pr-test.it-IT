---
title: aaaUse Azure DevTest Labs per il training | Documenti Microsoft
description: Informazioni su come toouse Azure DevTest Labs per scenari di training.
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Usare Azure DevTest Labs per il training
Azure DevTest Labs può essere utilizzato tooimplement molti degli scenari chiavi aggiunta toodev/test. Uno di questi scenari è tooset di un lab per il training. Azure DevTest Labs consente toocreate un ambiente lab in cui è possibile specificare i modelli personalizzati che ogni utente del training è possibile usare gli ambienti identici e isolato toocreate per il training. È possibile applicare criteri tooensure che gli ambienti di training sono utente del training tooeach disponibile solo quando necessario e contengono risorse insufficienti, ad esempio macchine virtuali - necessarie per il training hello. Infine, è possibile condividere facilmente lab hello con personale in addestramento, che può accedere a un solo clic.

![Usare DevTest Labs per il training](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs soddisfa hello training tooconduct richiesto in qualsiasi ambiente virtuale i requisiti seguenti: 

* I partecipanti non possono visualizzare le VM create da altri partecipanti
* Ogni computer di training deve essere identico
* I partecipanti possono effettuare rapidamente il provisioning degli ambienti di training
* Controllare i costi assicurando che personale in addestramento non è possibile ottenere più macchine virtuali di formazione hello e anche l'arresto di macchine virtuali quando vengono utilizzati
* Condividere facilmente formazione hello con ogni utente del training
* Riutilizzo hello formazione più volte

In questo articolo si informazioni sulle funzionalità di Azure DevTest Labs diversi che può essere usata hello toomeet descritto in precedenza i requisiti di training e la procedura dettagliata che è possibile seguire tooset di un lab per il training.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Implementazione del training con Azure DevTest Labs
1. **Creare hello lab** 
   
    Esercitazioni sono hello Azure DevTest Labs al punto iniziale. Dopo aver creato un ambiente lab, è possibile eseguire le attività, che ad esempio come aggiungere lab toohello utenti (personale in addestramento), i costi di set di criteri toocontrol, definire le immagini di macchina virtuale che è possono creare rapidamente e altro ancora.   
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare un lab di sviluppo/test di Azure](devtest-lab-create-lab.md) |Informazioni su come toocreate un laboratorio di Azure DevTest Labs in hello portale di Azure. |
2. **Creare VM di training in pochi minuti usando immagini del marketplace predefinite e immagini personalizzate** 
   
    È possibile selezionare le immagini predefinite da una vasta gamma di immagini in Azure Marketplace hello e renderli disponibili per personale in addestramento hello in lab hello. Se le immagini predefinite hello non soddisfano i requisiti, è possibile creare un'immagine personalizzata mediante la creazione di un macchina virtuale usando un'immagine pronti all'uso da Azure Marketplace, l'installazione di tutti i software hello necessari per il training hello e salvataggio hello VM come immagine personalizzata in lab hello lab. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Configurare le impostazioni dell'immagine di Azure Marketplace in un lab](devtest-lab-configure-marketplace-images.md) |Informazioni su come immagini di Azure Marketplace whitelist. rendere disponibile per la selezione solo hello le immagini desiderato per il training hello. |
   | [Creare un'immagine personalizzata](devtest-lab-create-template.md) |Per creare un'immagine personalizzata, pre-installare software hello che è necessario per il training hello in modo che personale in addestramento è possibile creare rapidamente una macchina virtuale utilizzando l'immagine personalizzata hello. |
3. **Creare modelli riutilizzabili per i computer di training** 
   
    Una formula in Azure DevTest Labs è che un elenco di valori di proprietà predefiniti utilizzati toocreate una macchina virtuale. È possibile creare una formula nel lab hello selezionando un'immagine, una dimensione di macchina virtuale (una combinazione di CPU e RAM) e una rete virtuale. Ogni utente del training vedere formula hello in lab hello e usarlo toocreate una macchina virtuale. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Gestire le formule di DevTest Labs toocreate macchine virtuali](devtest-lab-manage-formulas.md) |Informazioni su come creare una formula selezionando un'immagine, una dimensione per la VM (combinazione di CPU e RAM) e una rete virtuale. |
4. **Controllare i costi**
   
    Azure DevTest Labs consente tooset un criterio hello lab toospecify hello numero massimo di macchine virtuali che possono essere creati da un utente nell'ambiente lab hello del training. 
   
    Se si sta eseguendo il training di più giorni e si desidera toostop hello tutte le macchine virtuali a una determinata ora del giorno hello e automaticamente riavviarle hello giorno, è possibile facilmente eseguire tale operazione impostazione auto-arresto e avvio automatico di criteri nell'ambiente lab hello. 
   
    Infine, una volta completata la formazione è possibile eliminare tutte le macchine virtuali hello in una sola volta tramite l'esecuzione di un singolo script di PowerShell. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Definire i criteri del lab](devtest-lab-set-lab-policy.md) |Controllare i costi tramite l'impostazione di criteri nell'ambiente lab hello. |
   | [Eliminare lab hello tutte le macchine virtuali tramite uno script di PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Eliminare tutti i laboratori di hello in un'unica operazione una volta completato il training di hello. |
5. **Condividere lab hello con ogni utente del training**
   
    I lab sono direttamente accessibili con un collegamento condiviso con i partecipanti. I personale in addestramento anche dispone toohave un account Azure, come hanno un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). I partecipanti non possono visualizzare le VM create da altri partecipanti.  
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Aggiungere un ambiente lab tooa utente del training in Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Utilizzare hello Azure tooadd portale personale in addestramento tooyour training lab. |
   | [Aggiungere lab toohello personale in addestramento tramite uno script di PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilizzare l'aggiunta di formazione di personale in addestramento tooyour tooautomate di PowerShell. |
   | [Ottenere un ambiente lab toohello collegamento](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Informazioni su come un lab sia direttamente accessibile tramite un collegamento ipertestuale. |
6. **Riutilizzare più volte lab hello** 
   
    È possibile automatizzare la creazione di lab, incluse le impostazioni personalizzate, creazione di un modello di gestione delle risorse e utilizzandolo labs identici toocreate ripetutamente. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare un lab usando un modello di Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Creare lab in Azure DevTest Labs usando modelli di Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

