---
title: ambienti di test aaaUse Azure DevTest Labs per macchina virtuale e PaaS | Documenti Microsoft
description: Informazioni su come toouse Azure DevTest Labs per macchina virtuale e PaaS testare gli scenari di ambiente.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>Usare Azure DevTest Labs per macchine virtuali e ambienti di test PaaS

È possibile utilizzare Azure DevTest Labs tooimplement molti scenari chiavi, ma un scenario principale prevede l'uso di macchine toohost DevTest Labs per tester. 

In questo scenario DevTest Labs offre i vantaggi seguenti:

- I tester possono eseguire test più recente della propria applicazione hello rapidamente il provisioning di ambienti Windows e Linux utilizzando gli elementi e modelli riutilizzabili.
- Possono anche aumentare i test di carico eseguendo il provisioning di più agenti di test.
- Gli amministratori possono controllare i costi assicurandosi che:
  - I tester non possano ottenere più macchine virtuali del necessario per lo sviluppo.
  - Le VM vengano arrestate quando non sono in uso.

![Usare DevTest Labs per il training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

In questo articolo si informazioni sui requisiti dei vari Azure DevTest Labs funzionalità utilizzate toomeet tester e hello tooset toofollow la procedura dettagliata di un lab.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Implementazione di ambienti di test con Azure DevTest Labs
1. **Creare hello lab** 
   
    Esercitazioni sono hello Azure DevTest Labs al punto iniziale. Dopo aver creato un ambiente lab, è possibile eseguire attività quali l'aggiunta di lab toohello utenti (tester), l'impostazione criteri toocontrol i costi, la definizione di immagini di macchina virtuale che è possono creare rapidamente e altro ancora.  
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare un lab di sviluppo/test di Azure](devtest-lab-create-lab.md) |Informazioni su come toocreate un laboratorio di Azure DevTest Labs in hello portale di Azure. |
2. **Creare VM in pochi minuti usando immagini del marketplace predefinite e immagini personalizzate** 
   
    È possibile selezionare le immagini predefinite da una vasta gamma di immagini in Azure Marketplace hello e renderle disponibili nel lab hello. Se le immagini predefinite hello non soddisfano i requisiti, è possibile creare un'immagine personalizzata mediante la creazione di un macchina virtuale usando un'immagine da Azure Marketplace, l'installazione di tutto il software necessario, hello e salvataggio hello VM pronti all'uso come immagine personalizzata in lab hello lab.

    Se si utilizzano immagini personalizzate, è consigliabile usare un toocreate factory immagine e distribuire le immagini. Una factory di immagini è una soluzione di configurazione come codice che compila e distribuisce automaticamente le immagini configurate a intervalli regolari. Questo toomanually tempi di hello Salva configurare sistema hello dopo aver creata una macchina virtuale con hello del sistema operativo di base.
  
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Configurare le impostazioni dell'immagine di Azure Marketplace in un lab](devtest-lab-configure-marketplace-images.md) |Informazioni su come le immagini di Azure Marketplace whitelist, rendere disponibile per la selezione solo hello le immagini desiderato per i tester hello.|
   | [Creare un'immagine personalizzata](devtest-lab-create-template.md) |Per creare un'immagine personalizzata, pre-installare software hello che è necessario in modo che i tester di creare rapidamente una macchina virtuale utilizzando l'immagine personalizzata hello.|
   | [Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) (Informazioni sulla factory di immagini) |Guardare un video che descrive la modalità tooset configurare e utilizzare una factory dell'immagine.|

3. **Creare modelli riutilizzabili per i computer di test** 
   
    Una formula in Azure DevTest Labs è che un elenco di valori di proprietà predefiniti utilizzati toocreate una macchina virtuale. È possibile creare una formula nel lab hello selezionando un'immagine, una dimensione di macchina virtuale (una combinazione di CPU e RAM) e una rete virtuale. Ogni tester può vedere formula hello in lab hello e usarlo toocreate una macchina virtuale. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Gestire le formule di DevTest Labs toocreate macchine virtuali](devtest-lab-manage-formulas.md) |Informazioni su come creare una formula selezionando un'immagine, una dimensione per la VM (combinazione di CPU e RAM) e una rete virtuale.|

3. **Creare ambienti di test per più macchine virtuali** 
   
    È possibile utilizzare l'infrastruttura di Azure Resource Manager modelli toodefine hello e configurazione della soluzione Azure e distribuire ripetutamente test più macchine virtuali in uno stato coerente.

    È possibile eseguire il provisioning delle risorse di Azure PaaS in un ambiente usando un modello di Azure Resource Manager che verrà visualizzato nella verifica dei costi. Chiusura automatica di macchina virtuale, tuttavia, non si applica tooPaaS risorse.

    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare ambienti con più macchine virtuali e risorse PaaS con i modelli di Azure Resource Manager](devtest-lab-create-environment-from-arm.md) |Informazioni su come distribuire più macchine virtuali in modo coerente nell'ambiente di test.|

4. **Creare elementi tooenable flessibile VM personalizzazione**

   Gli elementi vengono utilizzati toodeploy e configurare l'applicazione dopo il provisioning di una macchina virtuale. Gli elementi possono essere:

   - Strumenti che si desidera tooinstall su hello - VM, ad esempio gli agenti, Fiddler e Visual Studio.
   - Azioni che si desidera toorun su hello - VM, come la clonazione di un repository.
   - Applicazioni che si desidera tootest.

   Molti elementi sono già immediatamente disponibili. È possibile creare elementi personalizzati per le proprie esigenze specifiche.

   Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare elementi personalizzati per le macchine virtuali di DevTest Labs](devtest-lab-artifact-author.md) |Creare i propri elementi personalizzati per le macchine virtuali hello nell'ambiente lab.|
   | [Aggiungere un artefatti della toostore repository Git personalizzati e modelli di gestione risorse di Azure per l'uso in Azure DevTest Labs](devtest-lab-add-artifact-repo.md) |Informazioni su come toostore gli elementi personalizzati in proprio repository Git privato.|

5. **Controllare i costi**
   
    Azure DevTest Labs consente tooset un criterio hello lab toospecify hello numero massimo di macchine virtuali che possono essere creati da un tester nell'ambiente lab hello. 
   
    Se il team di test dispone di un set di lavoro Pianificazione e si desidera toostop hello tutte le macchine virtuali a una determinata ora del giorno hello automaticamente riavviarle hello giorno, è possibile eseguire facilmente che l'impostazione auto-arresto e avvio automatico criteri nell'ambiente lab hello. 
   
    Infine, una volta completato lo sviluppo di app, è possibile eliminare tutte le macchine virtuali hello in una sola volta tramite l'esecuzione di un singolo script di PowerShell. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Definire i criteri del lab](devtest-lab-set-lab-policy.md) |Controllare i costi tramite l'impostazione di criteri nell'ambiente lab hello. |
   | [Eliminare lab hello tutte le macchine virtuali tramite uno script di PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Eliminare tutti i laboratori di hello in un'unica operazione quando il test è stato completato.|

1. **Aggiungere un tooa di rete virtuale Lab** 
   
    DevTest Labs crea una nuova rete virtuale quando viene creato un lab. Se è stata configurata la propria rete virtuale: ad esempio, tramite ExpressRoute o VPN site-to-site: è possibile aggiungere le impostazioni di rete virtuale del lab tooyour questa rete virtuale in modo che sia disponibile durante la creazione di macchine virtuali.

    Inoltre, vi è un Azure Active Directory dominio join elemento disponibile che viene aggiunto a un dominio di tooa VM quando viene creato hello VM. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Configurare una rete virtuale per Azure DevTest Labs](devtest-lab-configure-vnet.md) |Informazioni su come una rete virtuale in Azure DevTest Labs utilizzando tooconfigure hello portale di Azure.|

6. **Condividere lab hello con ogni tester**
   
    I lab sono direttamente accessibili con un collegamento condiviso con i tester, Non ancora hanno toohave un account Azure, come hanno un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). I tester non possono visualizzare le macchine virtuali create da altri tester.  
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Aggiungere un ambiente lab tooa tester in Azure DevTest Labs](devtest-lab-add-devtest-user.md) |Utilizzare hello tooadd portale Azure tester tooyour lab.|
   | [Aggiungere lab toohello tester tramite uno script di PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilizzare PowerShell tooautomate aggiunta lab tooyour tester. |
   | [Ottenere un ambiente lab toohello collegamento](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Informazioni su come i tester possono accedere direttamente a un lab tramite un collegamento ipertestuale.|

7. **Automatizzare la creazione del lab per più team** 
   
    È possibile automatizzare la creazione di lab, incluse le impostazioni personalizzate, creazione di un modello di gestione delle risorse e utilizzandolo labs identici toocreate ripetutamente. 
   
    Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:
   
   | Attività | Contenuto dell'esercitazione |
   | --- | --- |
   | [Creare un lab usando un modello di Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Creare lab in Azure DevTest Labs usando modelli di Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

