---
title: aaaGetting avviato con DSC di automazione di Azure | Documenti Microsoft
description: "Descrizione ed esempi di attività più comuni di hello in Azure Automation DSC Desired State Configuration)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Introduzione ad Automation DSC per Azure
In questo argomento viene illustrato come toodo hello attività più comuni con Azure Automation DSC Desired State Configuration (), ad esempio la creazione, l'importazione e la compilazione di configurazioni, gestiscono troppo macchine, caricamento e visualizzazione di report. Per una panoramica delle caratteristiche di Automation DSC per Azure, vedere [Panoramica della piattaforma DSC di Automazione di Azure](automation-dsc-overview.md). Per la documentazione di DSC, vedere [Panoramica di Windows PowerShell DSC (Desired State Configuration)](https://msdn.microsoft.com/PowerShell/dsc/overview).

In questo argomento fornisce una toousing Guida dettagliata Automation DSC per Azure. Se si desidera un ambiente di esempio che è già impostato senza seguire passaggi hello descritti in questo argomento, è possibile utilizzare [hello seguenti modello ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Tale modello configura un ambiente Automation DSC per Azure completo, che include una VM di Azure gestita da Automation DSC per Azure.

## <a name="prerequisites"></a>Prerequisiti
esempi di hello toocomplete in questo argomento, hello elementi seguenti sono necessari:

* Un account di automazione di Azure. Per istruzioni sulla creazione di un account RunAs di Automazione di Azure, vedere [Autenticare runbook con account RunAs di Azure](automation-sec-configure-azure-runas-account.md).
* Una VM di Azure Resource Manager (non classica) che esegue Windows Server 2008 R2 o versioni successive. Per istruzioni sulla creazione di una macchina virtuale, vedere [creare la prima macchina virtuale Windows hello portale di Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Creazione di una configurazione DSC
Verrà creata una semplice [configurazione DSC](https://msdn.microsoft.com/powershell/dsc/configurations) che garantisce la presenza di hello o l'assenza di hello **Server Web** Windows funzionalità (IIS), a seconda della modalità di assegnazione di nodi.

1. Avviare Windows PowerShell ISE hello (o qualsiasi editor di testo).
2. Digitare hello seguente testo:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Salvare il file hello come `TestConfig.ps1`.

Questa configurazione chiama una risorsa in ogni blocco di nodo, hello [risorsa WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), che garantisce la presenza di hello o l'assenza di hello **Server Web** funzionalità.

## <a name="importing-a-configuration-into-azure-automation"></a>Importazione di una configurazione in Automazione di Azure
Successivamente, si importerà configurazione hello in hello account di automazione.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**.
4. In hello **le configurazioni DSC** pannello, fare clic su **aggiungere una configurazione**.
5. In hello **Importa configurazione** blade, Sfoglia toohello `TestConfig.ps1` file nel computer.
   
    ![Schermata di hello * * blade Importa configurazione * *](./media/automation-dsc-getting-started/AddConfig.png)
6. Fare clic su **OK**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Visualizzazione di una configurazione in Automazione di Azure
Dopo avere importato una configurazione, è possibile visualizzarlo nel portale di Azure hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**
4. In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (questo è il nome di hello della configurazione di hello è stato importato nella procedura precedente hello).
5. In hello **TestConfig configurazione** pannello, fare clic su **Visualizza origine configurazione**.
   
    ![Schermata del Pannello di configurazione TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    Oggetto **origine configurazione TestConfig** pannello visualizzata codice PowerShell hello per la configurazione di hello.

## <a name="compiling-a-configuration-in-azure-automation"></a>Compilazione di una configurazione in Automazione di Azure
Prima di poter applicare un nodo tooa dello stato desiderato, una configurazione DSC che definisce lo stato deve essere compilata in uno o più configurazioni del nodo (documento MOF) e sul Server di Pull DSC di automazione hello. Per una descrizione più dettagliata della compilazione di configurazioni in Automation DSC per Azure, vedere [Compilazione di configurazioni in Automation DSC per Azure](automation-dsc-compile.md). Per altre informazioni sulla compilazione di configurazioni, vedere [Configurazioni DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**
4. In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (nome hello di hello precedentemente importata configurazione).
5. In hello **TestConfig configurazione** pannello, fare clic su **compilare**, quindi fare clic su **Sì**. Verrà avviato un processo di compilazione.
   
    ![Schermata del Pannello di configurazione TestConfig hello evidenziazione pulsante di compilazione](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Quando si compila una configurazione in automazione di Azure, distribuisce automaticamente qualsiasi server di pull creato nodo toohello file MOF di configurazione.
> 
> 

## <a name="viewing-a-compilation-job"></a>Visualizzazione di un processo di compilazione
Dopo avere avviato una compilazione, è possibile visualizzare in hello **i processi di compilazione** riquadro in hello **configurazione** blade. Hello **i processi di compilazione** riquadro Mostra attualmente in esecuzione, completato e processi non riusciti. Quando si apre un pannello di processo di compilazione, vengono visualizzate informazioni su tale processo, inclusi eventuali errori o avvisi durante, parametri di input di compilazione e configurazione di hello registri.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **le configurazioni DSC**.
4. In hello **le configurazioni DSC** pannello, fare clic su **TestConfig** (nome hello di hello precedentemente importata configurazione).
5. In hello **i processi di compilazione** affiancato di hello **TestConfig configurazione** pannello, fare clic su uno dei processi di hello elencati. Oggetto **processo di compilazione** si apre Pannello etichetta con data hello hello processo di compilazione è stata avviata.
   
    ![Schermata del Pannello di processo di compilazione hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. Fare clic su qualsiasi riquadro in hello **processo di compilazione** pannello toosee ulteriormente i dettagli sul processo hello.

## <a name="viewing-node-configurations"></a>Visualizzazione delle configurazioni di nodo
Con il completamento di un processo di compilazione vengono create una o più configurazioni di nodo. Una configurazione del nodo è un documento MOF è il server di pull toohello distribuito e pronto toobe estratti e applicato da uno o più nodi. È possibile visualizzare le configurazioni del nodo hello nell'account di automazione in hello **configurazioni del nodo DSC** blade. Una configurazione del nodo con un nome con il modulo hello *ConfigurationName*. *NodeName*.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **configurazioni del nodo DSC**.
   
    ![Schermata del Pannello di configurazioni del nodo DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Caricamento di una VM di Azure per la gestione con Automation DSC per Azure
È possibile utilizzare macchine virtuali di Azure toomanage DSC di automazione di Azure (classica e Gestione risorse), le macchine virtuali locali, macchine Linux, le macchine virtuali AWS e computer fisici locali. In questo argomento viene illustrata la modalità tooonboard solo macchine virtuali di gestione risorse di Azure. Per informazioni sul caricamento di altri tipi di computer, vedere [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard una VM di Azure Resource Manager per la gestione da Automation DSC per Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **i nodi DSC**.
4. In hello **i nodi DSC** pannello, fare clic su **macchina virtuale di Azure aggiungere**.
   
    ![Schermata del pannello i nodi DSC hello evidenziazione pulsante Aggiungi macchina virtuale di Azure hello](./media/automation-dsc-getting-started/OnboardVM.png)
5. In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **selezionare le macchine virtuali tooonboard**.
6. In hello **selezionare le macchine virtuali** seleziona hello VM tooonboard desiderato e fare clic su pannello **OK**.
   
   > [!IMPORTANT]
   > Deve trattarsi di una VM di Azure Resource Manager che esegue Windows Server 2008 R2 o versioni successive.
   > 
   > 
7. In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **configurare i dati di registrazione**.
8. In hello **registrazione** pannello, immettere il nome di hello della configurazione nodo hello desiderato tooapply toohello VM in hello **nome configurazione nodo** casella. Nome hello di una configurazione in hello account di automazione deve corrispondere esattamente. Specificare un nome in questo passaggio è facoltativo. È possibile modificare una configurazione del nodo hello assegnato dopo il nodo di hello onboarding.
   Selezionare **Riavvia il nodo se necessario** e fare clic su **OK**.
   
    ![Schermata del pannello registrazione hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    configurazione nodo Hello specificata verrà applicata toohello VM a intervalli determinati dall'hello **frequenza della modalità di configurazione**, e verifica hello VM per la configurazione di nodo toohello gli aggiornamenti a intervalli determinati dall'hello  **Frequenza di aggiornamento**. Per ulteriori informazioni sull'utilizzo di questi valori, vedere [hello configurazione Gestione configurazione locale](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. In hello **aggiungere macchine virtuali di Azure** pannello, fare clic su **crea**.

Azure verrà avviato il processo di hello di onboarding hello macchina virtuale. Al termine, verrà visualizzato hello VM nella hello **i nodi DSC** pannello in hello account di automazione.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Visualizzazione elenco hello dei nodi DSC
È possibile visualizzare l'elenco di hello di tutti i computer che sono state caricate per la gestione di account di automazione in hello **i nodi DSC** blade.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **i nodi DSC**.

## <a name="viewing-reports-for-dsc-nodes"></a>Visualizzazione di report per i nodi DSC
Ogni volta che l'automazione di Azure DSC esegue una verifica coerenza su un nodo gestito, il nodo di hello invia un server di pull toohello back-report di stato. È possibile visualizzare questi report nel Pannello di hello per tale nodo.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **i nodi DSC**.
4. In hello **report** riquadro, fare clic su uno dei report hello nell'elenco di hello.
   
    ![Schermata del pannello Report hello](./media/automation-dsc-getting-started/NodeReport.png)

Nel Pannello di hello per un singolo report, è possibile visualizzare le seguenti informazioni di stato per la coerenza corrispondente hello hello controllare:

* Hello segnalare lo stato, se il nodo hello è "Conformi," configurazione hello "Failed", o nodo hello è "Non conforme" (quando il nodo hello è **applyandmonitor** modalità e hello macchina non è in stato di hello desiderato).
* Hello ora di inizio per il controllo di coerenza hello.
* fase di esecuzione totale Hello per garantire l'uniformità hello controllare.
* controllo di tipo Hello di verifica di coerenza.
* Eventuali errori, inclusi i messaggio di errore e codice di errore hello. 
* Le risorse DSC utilizzate in configurazione hello e hello stato di ogni risorsa (se il nodo hello è nello stato desiderato di hello per tale risorsa), è possibile fare clic su ogni risorsa tooget ulteriori informazioni per tale risorsa.
* nome Hello, indirizzo IP e la modalità di configurazione del nodo hello.

È anche possibile fare clic su **visualizzare i report non elaborati** toosee hello dati effettivi che hello nodo invia toohello server. Per altre informazioni sull'uso di tali dati, vedere [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver)(Uso di un server di report DSC).

Può richiedere qualche tempo dopo un nodo è caricate prima hello primo report è disponibile. Potrebbe essere necessario toowait backup too30 minuti per primo report hello dopo avere incorporato un nodo.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Riassegnazione di una configurazione di un nodo diverso nodo tooa
È possibile assegnare una configurazione di un nodo diverso toouse un nodo di hello inizialmente assegnato un oggetto.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **i nodi DSC**.
4. In hello **i nodi DSC** pannello, fare clic sul nome hello del nodo hello desiderato tooreassign.
5. Nel Pannello di hello per tale nodo, fare clic su **nodo Assign**.
   
    ![Schermata del pannello nodo hello evidenziazione pulsante assegnare nodo hello](./media/automation-dsc-getting-started/AssignNode.png)
6. In hello **assegnare configurazione nodo** blade, hello selezionare nodo Configurazione toowhich desidera tooassign hello nodo e quindi fare clic su **OK**.
   
    ![Schermata del Pannello di configurazione del nodo assegnare hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Annullamento della registrazione di un nodo
Se non si desidera più toobe un nodo gestito da Automation DSC per Azure, è possibile annullarne.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **tutte le risorse** e hello quindi il nome dell'account di automazione.
3. In hello **account di automazione** pannello, fare clic su **i nodi DSC**.
4. In hello **i nodi DSC** pannello, fare clic sul nome hello del nodo hello desiderato toounregister.
5. Nel Pannello di hello per tale nodo, fare clic su **Unregister**.
   
    ![Schermata del pannello nodo hello evidenziazione pulsante di annullamento della registrazione hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Articoli correlati
* [Panoramica di Automation DSC per Azure](automation-dsc-overview.md)
* [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md)
* [Panoramica di Windows PowerShell DSC (Desired State Configuration)](https://msdn.microsoft.com/powershell/dsc/overview)
* [Cmdlet di Automation DSC per Azure](/powershell/module/azurerm.automation/#automation)
* [Prezzi di Automation DSC per Azure](https://azure.microsoft.com/pricing/details/automation/)

