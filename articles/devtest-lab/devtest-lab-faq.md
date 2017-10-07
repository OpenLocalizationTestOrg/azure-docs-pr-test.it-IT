---
title: domande frequenti di DevTest Labs aaaAzure | Documenti Microsoft
description: Trovare le risposte alle domande di Azure DevTest Labs toocommon
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Domande frequenti su Azure DevTest Labs
Questo articolo risponde ad alcune delle domande più comuni di hello su Azure DevTest Labs.

**Generale**
## <a name="what-if-my-question-isnt-answered-here"></a>Cosa fare se non è disponibile una risposta alla domanda?
Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.

* Pubblicare una domanda in hello [thread di Disqus](#comments) alla fine di hello di queste domande frequenti e contattare il team di Cache di Azure hello e altri membri della community su questo articolo.
* tooreach un gruppo di destinatari più ampio, inserire una domanda hello [forum MSDN di Azure DevTest Labs](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)e contattare il team di Azure DevTest Labs hello e altri membri della Comunità hello.
* toomake una richiesta di funzionalità, inviare toohello le richieste e idee [Azure DevTest Labs utente vocale](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Perché usare Azure DevTest Labs?
Azure DevTest Labs può far risparmiare tempo e denaro al team. Gli sviluppatori possono creare i propri ambienti con diverse basi diverse e utilizzare elementi tooquickly distribuire e configurare le applicazioni. Con le immagini e le formule personalizzate, le macchine virtuali possono essere salvate come modelli e riprodotte facilmente. Inoltre, labs offrono diversi criteri configurabili che consentono agli amministratori di lab tooreduce rifiuti e gestire gli ambienti del team. Questi criteri sono arresto automatico, soglia di costo, numero massimo di VM per utente e dimensioni massime delle VM. Per una spiegazione più dettagliata di Azure DevTest Labs, leggere hello [Panoramica](devtest-lab-overview.md) o espressioni di controllo hello [video introduttivo](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>Cosa significa "self-service senza preoccupazioni"?
"Tranquillità, Self-Service" significa che gli sviluppatori e tester creare i propri ambienti in base alle necessità e gli amministratori hanno la sicurezza hello di sapere che Azure DevTest Labs consente di ridurre al minimo i rifiuti e controllare i costi. Gli amministratori possono specificare le dimensioni delle macchine Virtuali sono consentiti, numero massimo di hello di macchine virtuali, e quando vengono avviate e quindi arrestare le macchine virtuali. Azure DevTest Labs rende facile toomonitor costi e set avvisi toostay conoscere come vengono utilizzate le risorse lab hello.

## <a name="how-can-i-use-azure-devtest-labs"></a>Come si usa Azure DevTest Labs?
Azure DevTest Labs è utile ogni volta che si richiedono dev o ambienti di test e si desidera tooreproduce li rapidamente e/o gestiti con costo salvataggio dei criteri.

Ecco alcuni scenari per cui i clienti usano Azure DevTest Labs:

* Gestione degli ambienti di sviluppo e test in un'unica posizione, che utilizzano criteri tooreduce costo e immagini personalizzate tooshare compilazioni Team hello.
* Sviluppo di un'applicazione che utilizza immagini personalizzate toosave hello dello stato del disco durante le fasi di sviluppo hello.
* Costo hello in relazione tooprogress di rilevamento.
* Creazione di ambienti di testing di massa per i test di controllo di qualità.
* Utilizzando gli elementi e le formule tooeasily configurare e riprodurre un'applicazione in vari ambienti.
* La distribuzione di macchine virtuali per hackathons (collaborative di sviluppo o test lavoro) e quindi facilmente deprovisioning li al termine dell'evento hello.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Come avviene la fatturazione di Azure DevTest Labs?
Azure DevTest Labs è un servizio gratuito, vale a dire che laboratori di creazione e configurazione di elementi, i modelli e criteri di hello è disponibile. Si pagano hello per le risorse di Azure utilizzate all'interno del lab, ad esempio macchine virtuali, gli account di archiviazione e reti virtuali. Per ulteriori informazioni sul costo hello risorse lab, conoscenza [dei prezzi di Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Sicurezza**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Quali sono hello diversi livelli di protezione in Azure DevTest Labs?
L'accesso sicuro è determinato dal [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-built-in-roles.md). toounderstand accedere come funziona, ma consente toounderstand hello differenze un'autorizzazione, un ruolo e un ambito, come definito da RBAC.

* **Autorizzazione** -un'autorizzazione è un'azione specifica tooa di accesso definito. Ad esempio, un'autorizzazione può essere macchine virtuali tooall e accesso in lettura.
* **Ruolo** -un ruolo è un set di autorizzazioni che possono essere raggruppati e tooa utente assegnato. Ad esempio, "proprietario di una sottoscrizione" tooall di accedere alle risorse all'interno di una sottoscrizione.
* **Ambito** -un ambito è un livello nella gerarchia di hello di risorse di Azure. Ad esempio, un ambito può essere un gruppo di risorse o una singola sottoscrizione intera lab o hello.

Nell'ambito di hello di Azure DevTest Labs, sono disponibili due tipi di autorizzazioni utente per i ruoli toodefine: proprietario del lab e utente lab.

* **Proprietario del lab** -hello accedere tooany alle risorse nell'ambiente lab hello dispone di un proprietario del lab. Pertanto, sono può modificare i criteri, leggere e scrivere tutte le macchine virtuali, modificare la rete virtuale hello e così via.
* **Utente del lab** : può visualizzare tutte le risorse del lab, ad esempio VM, criteri e reti virtuali, ma non può modificare i criteri o le VM create da altri utenti. È inoltre possibile toocreate ruoli personalizzati in Azure DevTest Labs, e viene descritta la modalità toodo nell'articolo hello, [concedere le autorizzazioni utente criteri lab toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Poiché gli ambiti sono gerarchici, quando un utente ha le autorizzazioni per un determinato ambito, gli vengono automaticamente concesse tali autorizzazioni per ogni ambito di livello inferiore incluso. Ad esempio, se un utente viene assegnato il ruolo di toohello del proprietario della sottoscrizione, quindi hanno tooall di accedere alle risorse in una sottoscrizione. Le risorse includono tutte le macchine virtuali, tutte le reti virtuali e tutti i lab. Di conseguenza, un proprietario della sottoscrizione eredita automaticamente ruolo hello del proprietario del lab. Tuttavia, hello opposto non è true. Il proprietario di un lab ha lab tooa accesso, ovvero un ambito inferiore rispetto a livello di sottoscrizione hello. Pertanto, il proprietario di un lab non è in grado di toosee le macchine virtuali o reti virtuali o le risorse che sono di fuori di lab hello.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Come creare un tooperform agli utenti di ruolo tooallow un'attività specifica?
Un articolo completo su come ruoli personalizzati toocreate e assegnare le autorizzazioni toothat ruolo sono disponibili qui. Di seguito è riportato un esempio di uno script che Crea ruolo hello "DevTest Labs avanzate User", che dispone dell'autorizzazione toostart e arrestare tutte le macchine virtuali nel lab hello:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Integrazione e automazione CI/CD**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs si integra con la toolchain CI/CD?
Se si utilizza Visual Studio Team Services, è un [estensione Azure DevTest Labs attività](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) che consente il rilascio della pipeline in Azure DevTest Labs tooautomate. Alcuni degli utilizzi di hello di questa estensione:

* Creazione e distribuisce automaticamente una macchina virtuale e configurarlo con build più recente di hello tramite operazioni di copia dei File di Azure o VSTS PowerShell.
* Automaticamente acquisizione dello stato di hello di una macchina virtuale al termine del test tooreproduce un bug in hello stessa macchina virtuale per un'analisi più approfondita.
* L'eliminazione di hello VM alla fine hello hello rilasciare pipeline quando non è più necessario.

Hello post di blog seguenti forniscono informazioni aggiuntive e informazioni sull'utilizzo di estensione di Visual Studio Team Services hello:

* [Azure DevTest Labs – VSTS extension (Azure DevTest Labs: estensione VSTS)](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Deploying a new VM in an existing AzureDevTestLab from VSTS (Distribuzione di una nuova VM in un'istanza di Azure DevTest Labs da VSTS)](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [Utilizzando Gestione del rilascio di Visual Studio Team Services per le distribuzioni continua tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Per altri toolchains CI/CD, hello tutti indicati in precedenza scenari che possono essere ottenuti tramite l'estensione di attività di Visual Studio Team Services in modo analogo è possibile tramite la distribuzione di hello [modelli di gestione risorse di Azure](https://aka.ms/dtlquickstarttemplate) utilizzando [ Cmdlet di Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md) e [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). È inoltre possibile utilizzare [API REST per DevTest Labs](http://aka.ms/dtlrestapis) toointegrate con la toolchain.  


**Macchine virtuali**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Impossibile visualizzare alcune macchine virtuali nel pannello macchine virtuali di Azure hello visibili all'interno di Azure DevTest Labs
Creazione di una macchina virtuale in Azure DevTest Labs, l'autorizzazione è dato tooaccess tale macchina virtuale. Si è in grado di tooview sia nel pannello labs hello e hello **macchine virtuali** blade. Gli utenti nel ruolo di DevTest Labs hello possono visualizzare tutte le macchine virtuali create nell'ambiente lab hello tramite lab è hello **tutte le macchine virtuali** blade. Tuttavia, gli utenti nel ruolo di DevTest Labs hello non vengono concessi automaticamente le risorse di accesso in lettura tooVM creati da altri. Pertanto, tali macchine virtuali non vengono visualizzati in hello **macchine virtuali** blade.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Qual è la differenza hello tra immagini personalizzate e le formule?
Un'immagine personalizzata è un disco rigido virtuale, mentre una formula è un'immagine che è possibile configurare con impostazioni aggiuntive che si possono salvare e riprodurre. Un'immagine personalizzata potrebbe essere preferibile se si desidera tooquickly creare ambienti diversi con hello stessa immagine di base, non modificabile. Una formula potrebbe essere consigliabile se si desidera tooreproduce hello configurazione della macchina virtuale con il bit più recente di hello, subnet una rete virtuale o una dimensione specifica. Per una spiegazione più dettagliata, vedere l'articolo hello [il confronto di immagini personalizzate e le formule in DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Come creare più macchine virtuali da hello stesso modello in una sola volta?
È possibile utilizzare hello [VSTS attività estensione](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) o [generare un modello di gestione risorse di Azure](devtest-lab-add-vm.md#save-azure-resource-manager-template) durante la creazione di una macchina virtuale e [distribuire il modello di gestione risorse di Azure hello da Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Come si spostano le VM di Azure esistenti nel lab Azure DevTest Labs?
Eseguire le operazioni di hello seguito toocopy il tooAzure macchine virtuali esistenti di DevTest Labs:

1. Copia i file di disco rigido virtuale hello della macchina virtuale esistente usando questa [script di Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Creare l'immagine personalizzata hello](devtest-lab-create-template.md) all'interno del laboratorio di DevTest Labs di Azure.
3. Creare una macchina virtuale nell'ambiente lab hello dall'immagine personalizzata

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>È possibile associare più dischi toomy macchine virtuali?
Collegamento di più dischi tooVMs è supportato.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Se desidera toouse un'immagine del sistema operativo Windows per il test, è necessario toopurchase un abbonamento a MSDN?
Se è necessario toouse immagini di sistema operativo client Windows (Windows 7 o versioni successive) per lo sviluppo o test in Azure, quindi Sì, è necessario:

- [Acquistare un abbonamento a MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Se si dispone di un contratto Enterprise Agreement, creare una sottoscrizione di Azure con hello [offerta di sviluppo/Test Enterprise](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Per ulteriori informazioni su hello crediti di Azure per ogni offerta di MSDN, vedere [credito Azure mensile per i sottoscrittori di Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Come automatizzare il processo di hello di caricamento di immagini personalizzate toocreate i file di disco rigido virtuale
Sono disponibili due opzioni:

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) possibile toocopy usato o caricare account archiviazione toohello file disco rigido virtuale associato lab hello.
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma che esegue Windows, OSX e Linux.   

toofind account di archiviazione destinazione hello associato nel lab, eseguire la procedura seguente:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **gruppi di risorse** dal pannello sinistro hello.
3. Individuare e selezionare il gruppo di risorse hello associato con l'ambiente lab.
4. In hello **Panoramica** pannello, selezionare uno degli account di archiviazione hello.
5. Selezionare **BLOB**.
6. Cercare nell'elenco di hello caricamenti. Se ne esiste alcuno, restituire tooStep #4 e provare un altro account di archiviazione.
7. Hello utilizzare **URL** come destinazione di nel comando AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Come è possibile automatizzare il processo di hello di eliminazione hello tutte le macchine virtuali nel mio laboratorio?
Inoltre toodeleting macchine virtuali dal lab in hello portale di Azure, è possibile eliminare tutte le macchine virtuali hello nell'ambiente lab tramite uno script di PowerShell. In hello seguente esempio, modificare i valori di parametro hello in hello **toochange valori** commento. È possibile recuperare hello `subscriptionId`, `labResourceGroup`, e `labName` valori dal pannello lab hello in hello portale di Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Elementi**
## <a name="what-are-artifacts"></a>Cosa sono gli elementi?
Gli elementi sono elementi personalizzabili che possono essere utilizzati toodeploy i bit più recenti o i dev degli strumenti in una macchina virtuale. Sono collegati tooyour macchina virtuale durante la creazione con pochi semplici clic e una volta che viene eseguito il provisioning di hello macchina virtuale, gli elementi di hello distribuire e configurare la macchina virtuale. Nell'[archivio GitHub pubblico](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) sono disponibili svariati elementi preesistenti, ma è anche possibile [creare i propri elementi](devtest-lab-artifact-author.md) facilmente.


**Configurazione del lab**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Come si crea un lab da un modello di Azure Resource Manager?
È stato fornito un [repository GitHub dei modelli di Azure Resource Manager lab](https://aka.ms/dtlquickstarttemplate) che è possibile distribuire come- o modificarle toocreate modelli personalizzati per il lab. Ognuno di questi modelli è un collegamento che è possibile scegliere come il lab hello toodeploy-sotto la propria sottoscrizione Azure, oppure è possibile personalizzare il modello di hello e [distribuire tramite PowerShell o Azure CLI](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Perché le VM vengono create in gruppi di risorse diversi con nomi arbitrari? È possibile rinominare o modificare questi gruppi di risorse?
Gruppi di risorse vengono creati in questo modo affinché le autorizzazioni utente di Azure DevTest Labs toomanage hello e accesso toovirtual macchine. Mentre con il nome desiderato, è possibile spostare gruppo di risorse tooanother VM hello, ciò non è consigliabile. Stiamo lavorando su come migliorare questa esperienza tooallow una maggiore flessibilità.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Quanti lab è possibile creare in hello stessa sottoscrizione?
Non sussiste alcun limite specifico per il numero di hello di esercitazioni che possono essere creati per ogni sottoscrizione. Tuttavia, le risorse di hello usate sono limitate per ogni sottoscrizione. Per ulteriori informazioni hello [limiti e quote imposto sulle sottoscrizioni Azure](../azure-subscription-service-limits.md) e [come tooincrease questi limiti](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Quante VM è possibile creare per ogni lab?
Non sussiste alcun limite specifico per il numero di hello di macchine virtuali che possono essere creati per lab. Tuttavia, le risorse di hello utilizzate sono limitate per ogni sottoscrizione (ad esempio core di macchina virtuale, gli indirizzi IP pubblici, ecc.). Per ulteriori informazioni hello [limiti e quote imposto sulle sottoscrizioni Azure](../azure-subscription-service-limits.md) e [come tooincrease questi limiti](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>La modalità di condivisione di un ambiente lab toomy collegamento diretto
un collegamento diretto tooshare tooyour gli utenti, è possibile eseguire hello seguente procedura:

1. Sfoglia toohello lab in hello portale di Azure.
2. Copiare l'URL lab hello dal browser e condividerlo con gli utenti del lab.

> [!NOTE]
> Se il lab di utenti è esterni con una [account Microsoft](#what-is-a-microsoft-account) e non appartengono tooyour Active directory aziendale, potrebbe ricevere un errore durante il passaggio di collegamento toohello fornito. Se si riceve un errore, indicare loro tooclick al nome nell'angolo superiore destro di hello di hello portale di Azure e directory selezionare hello in cui è presente lab hello da hello **Directory** sezione del menu hello.
>
>

## <a name="what-is-a-microsoft-account"></a>Che cos'è un account Microsoft?
Un account Microsoft è ciò che si usa per quasi tutte le operazioni eseguite con servizi e dispositivi di Microsoft. È un indirizzo di posta elettronica e una password che è utilizzare toosign in tooSkype, Outlook.com, OneDrive, Windows Phone e Xbox LIVE: significa che il file, foto, contatti e le impostazioni possono seguire tooany dispositivo.

> [!NOTE]
> Account Microsoft usato toobe denominato "Windows Live ID".
>
>


**Risoluzione dei problemi**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Si è verificato un errore per l'elemento durante la creazione della VM. Come si risolve il problema?
Fare riferimento troppo[come errori di artefatto toodiagnose in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn modalità di registrazione tooobtain riguardanti l'elemento non riuscito.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Perché la rete virtuale esistente non viene salvata correttamente?
È possibile che il nome della rete virtuale contenga dei punti. Se in tal caso, provare a rimuovere hello periodi o sostituirli con un trattino e quindi ripetere il salvataggio hello nuovamente rete virtuale.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Perché quando si esegue il provisioning di una macchina virtuale da PowerShell viene visualizzato un errore del tipo "Risorsa padre non trovata"?
Quando una risorsa è una risorsa di tooanother padre, risorsa padre hello deve esistere prima di creare la risorsa figlio hello. Se non esiste ancora, viene visualizzato l'errore **ParentResourceNotFound**. Se non si specifica una dipendenza sulla risorsa padre hello, la risorsa figlio hello potrà essere distribuita prima padre hello.

Le macchine virtuali sono risorse figlio di un lab in un gruppo di risorse. Quando si usa Azure Resource Manager modelli toodeploy tramite PowerShell, nome gruppo di risorse hello cui hello script di PowerShell deve essere nome gruppo di risorse hello lab hello. Per altre informazioni, vedere [Risolvere errori comuni durante la distribuzione in Azure ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Se la distribuzione di una macchina virtuale ha esito negativo, dove è possibile trovare maggiori informazioni sul tipo di errore?
Errori di distribuzione di macchina virtuale vengono acquisiti nel log attività hello. È possibile trovare log attività di macchine virtuali tramite hello lab **log di controllo** o **diagnostica macchina virtuale** menu risorse hello nel pannello VM del lab hello (blade hello viene visualizzato dopo aver selezionato hello VM da **Macchine virtuali** elenco).

In alcuni casi, errore di distribuzione hello si verifica prima dell'avvio hello distribuzione della macchina virtuale, ad esempio quando viene superato limite della sottoscrizione per una risorsa creata con hello VM hello. In questo caso, i dettagli dell'errore hello vengono acquisiti nel livello lab hello **log attività** che può essere trova nella parte inferiore di hello di hello **criteri di configurazione e** impostazioni. Per ulteriori informazioni sull'utilizzo di attività registra in Azure, vedere [visualizzazione attività registra le azioni sulle risorse tooaudit](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
