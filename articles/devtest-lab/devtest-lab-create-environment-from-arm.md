---
title: aaaCreate ambienti multi-VM e PaaS risorse con i modelli di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate ambienti multi-VM e risorse di PaaS in Azure DevTest Labs da un modello di gestione risorse di Azure
services: devtest-lab,virtual-machines,visual-studio-online
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
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Creare ambienti con più macchine virtuali e risorse PaaS con i modelli di Azure Resource Manager

Hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) consente tooeasily [creare e aggiungere un ambiente lab tooa VM](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Ciò vale per la creazione di una macchina virtuale alla volta. Tuttavia, se l'ambiente di hello contiene più macchine virtuali, ogni macchina virtuale ha toobe create individualmente. Per gli scenari, ad esempio un'app Web a più livelli o una farm di SharePoint, un meccanismo è tooallow necessari per la creazione di hello di più macchine virtuali in un unico passaggio. Tramite i modelli di gestione risorse di Azure, è possibile definire ora infrastruttura hello e configurazione della soluzione Azure e distribuire ripetutamente più macchine virtuali in uno stato coerente. Questa funzionalità offre hello seguenti vantaggi:

- I modelli di Azure Resource Manager vengono caricati direttamente dal repository di controllo del codice sorgente (GitHub o Team Services Git).
- Una volta configurato, gli utenti possono creare un ambiente scegliendo un modello di gestione risorse di Azure dal portale di Azure come le operazioni eseguite con altri tipi di hello [VM basi](./devtest-lab-comparing-vm-base-image-types.md).
- Risorse di Azure PaaS possano eseguirne il provisioning in un ambiente da un modello di gestione risorse di Azure in tooIaaS inoltre le macchine virtuali.
- costo Hello degli ambienti può essere registrato in lab hello in aggiunta tooindividual macchine virtuali create da altri tipi di base.
- Risorse PaaS vengono create e verranno visualizzato nel costo rilevamento; chiusura automatica di macchina virtuale, tuttavia, non si applica tooPaaS risorse.
- Gli utenti hanno hello stesso controllo dei criteri per gli ambienti di macchina virtuale in cui per le macchine virtuali singolo lab.

Altre informazioni su hello molti [vantaggi dell'utilizzo di modelli di gestione risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, aggiornare o eliminare tutte le risorse lab in un'unica operazione.

> [!NOTE]
> Quando si utilizza un modello di gestione risorse come un toocreate base lab altre macchine virtuali, esistono alcuni tookeep differenze presente per la creazione di macchine virtuali Multi o macchine virtuali di singolo. Use a virtual machine's Azure Resource Manager template (Usare un modello di Azure Resource Manager di una macchina virtuale) spiega più dettagliatamente queste differenze.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Configurare i repository del modello di Azure Resource Manager

Come una delle procedure consigliate di hello con infrastruttura come codice e come codice di configurazione, i modelli di ambiente deve essere gestita in controllo del codice sorgente. Azure Labs DevTest applica questa procedura e carica tutti i modelli Azure Resource Manager direttamente dai repository VSTS Git o GitHub. Di conseguenza, è possono utilizzare modelli di gestione risorse tra hello intero ciclo di rilascio di da hello test toohello ambiente di produzione.

Esistono un paio di regole toofollow tooorganize i modelli di gestione risorse di Azure in un repository:

- file di modello master Hello deve essere denominato `azuredeploy.json`. 

    ![File principali del modello di Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Se si desidera che i valori di parametro toouse definiti in un file di parametro, il file di parametro hello deve essere denominato `azuredeploy.parameters.json`.
- È possibile utilizzare parametri hello `_artifactsLocation` e `_artifactsLocationSasToken` tooconstruct hello parametersLink valore dell'URI, consentendo di DevTest Labs tooautomatically gestire modelli nidificati. Per altre informazioni, vedere [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments (Come Azure DevTest Labs semplifica le distribuzioni di modelli di Resource Manager nidificati negli ambienti di test)](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/).
- I metadati possono essere descrizione e nome visualizzato del modello definito toospecify hello. I metadati deve essere contenuti in un file denominato `metadata.json`. Hello file di metadati di esempio seguente viene illustrato come hello toospecify nome visualizzato e la descrizione: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hello passaggi seguenti consentono di eseguire l'aggiunta di un lab tooyour repository utilizzando hello portale di Azure. 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Elenco dei laboratori hello selezionare lab desiderato hello.   
1. Nel pannello del lab hello, selezionare **criteri di configurazione e**.

    ![Configurazione e criteri](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Da hello **criteri di configurazione e** elenco di impostazioni, seleziona **repository**. Hello **repository** blade sono elencati i repository hello che sono stati aggiunti toohello lab. Un repository denominato `Public Repo` viene generato automaticamente per tutte le esercitazioni e si connette toohello [repository GitHub di DevTest Labs](https://github.com/Azure/azure-devtestlab) che contiene più elementi di macchina virtuale per l'uso.

    ![Repository pubblico](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Selezionare **Aggiungi +** tooadd il repository di modello di gestione risorse di Azure.
1. Quando hello secondo **repository** pannello visualizzata, immettere le informazioni necessarie hello come segue:
    - **Nome** -nome hello repository utilizzato nell'ambiente lab hello.
    - **URL clone GIT** -immettere l'URL del clone GIT HTTPS hello da GitHub o Visual Studio Team Services.  
    - **Ramo** -immettere hello ramo nome tooaccess le definizioni di modello di gestione risorse di Azure. 
    - **Token di accesso personale** -viene utilizzato il token di accesso personale hello toosecurely accedere il repository. Selezionare il token da Visual Studio Team Services tooget  **&lt;YourName >> profilo personale > sicurezza > token di accesso pubblico**. tooget il token da GitHub, selezionare l'avatar seguito selezionando **Impostazioni > token di accesso pubblico**. 
    - **I percorsi delle cartelle** : utilizzando uno dei campi di input hello due, immettere percorso della cartella hello che inizia con una barra rovesciata - / - ed è relativo tooyour Git clone URI tooeither definizioni degli artefatti (primo campo di input) o il modello di gestione risorse di Azure definizioni.   
    
        ![Repository pubblico](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Dopo aver creato tutti i campi necessario hello vengono immessi e superare la convalida di hello, selezionare **salvare**.

Nella sezione successiva Hello verrà illustrata la creazione di ambienti da un modello di gestione risorse di Azure.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Creare un ambiente da un modello di Azure Resource Manager

Una volta un repository di modello di gestione risorse di Azure è stato configurato nell'ambiente lab hello, gli utenti di lab possono creare un ambiente tramite il portale di Azure con hello alla procedura seguente:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
1. Elenco dei laboratori hello selezionare lab desiderato hello.   
1. Nel pannello del lab hello, selezionare **Aggiungi +**.
1. Hello **scegliere una base** pannello consente di visualizzare le immagini di base hello è possibile utilizzare con i modelli di Azure Resource Manager hello elencati per primo. Seleziona hello desiderato modello di gestione risorse di Azure.

    ![Scegli una base](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. In hello **Aggiungi** pannello immettere hello **nome ambiente** valore. nome di ambiente Hello è ciò che gli utenti visualizzati tooyour lab hello. campi di input rimanenti Hello definiti nel modello di gestione risorse di Azure hello. Se i valori predefiniti sono definiti nel modello di hello o hello `azuredeploy.parameter.json` file è presente, vengono visualizzati i valori predefiniti in tali campi di input. Per i parametri di tipo *stringa sicura*, è possibile utilizzare informazioni segrete hello del lab hello [archivio segreto personale](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Pannello Aggiungi](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Esistono diversi valori di parametro che, anche se specificati, vengono visualizzati come valori vuoti. Pertanto, se gli utenti assegnare tooparameters tali valori in un modello di gestione risorse di Azure, DevTest Labs non visualizza valori hello; invece che mostra i campi di input vuoti in cui gli utenti lab hello necessario tooenter un valore durante la creazione ambiente hello.
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. Selezionare **Aggiungi** ambiente hello toocreate. avvio dell'ambiente Hello immediatamente il provisioning con stato hello visualizzazione in hello **macchine virtuali** elenco. Un nuovo gruppo di risorse viene creato automaticamente da hello lab tooprovision tutte le risorse di hello definite nel modello di gestione risorse di Azure hello.
1. Una volta creato l'ambiente di hello, selezionare l'ambiente hello in hello **macchine virtuali** elenco pannello gruppo della risorsa tooopen hello e individuare tutte le risorse di hello eseguito il provisioning in ambiente hello.
    
    ![Elenco delle macchine virtuali](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   È anche possibile espandere hello ambiente tooview hello solo elenco delle macchine virtuali nell'ambiente di hello sottoposti a provisioning.
    
    ![Elenco delle macchine virtuali](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Fare clic su uno di hello ambienti tooview hello azioni disponibili, ad esempio l'applicazione di elementi, collegare dischi dati, la modifica ora di arresto automatici e altro ancora.

    ![Azioni dell'ambiente](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver creata una macchina virtuale, è possibile connettersi toohello VM selezionando **Connetti** nel pannello hello della macchina virtuale.
* Consente di visualizzare e gestire le risorse in un ambiente selezionando ambiente hello in hello **macchine virtuali** elenco nell'ambiente lab. 
* Esplorare hello [modelli di gestione risorse di Azure dalla raccolta di modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates)
