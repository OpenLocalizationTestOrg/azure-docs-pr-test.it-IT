---
title: aaaAdd piani toorecovery runbook di automazione di Azure nel portale classico hello | Documenti Microsoft
description: "Questo articolo viene descritto come Azure Site Recovery consente ora i piani di ripristino tooextend con complesse attività di automazione di Azure toocomplete durante il ripristino tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Aggiungere i piani toorecovery runbook di automazione di Azure nel portale classico hello
In questa esercitazione viene descritta l'integrazione di Azure Site Recovery con automazione di Azure tooprovide estendibilità toorecovery piani. I piani di ripristino possono orchestrare il ripristino delle macchine virtuali protette mediante Azure Site Recovery per cloud di replica toosecondary e scenari di replica tooAzure. Consentono inoltre di effettuare il ripristino di hello **in modo coerente accurate**, **repeatable**, e **automatizzati**. Se viene eseguito il failover tooAzure le macchine virtuali, integrazione con automazione di Azure estende i piani di ripristino e offre funzionalità tooexecute runbook, consentendo in tal modo l'attività di automazione potente.

Se non si è ancora sentito parlare di Automazione di Azure, effettuare l'iscrizione [qui](https://azure.microsoft.com/services/automation/) e scaricare gli script di esempio [qui](https://azure.microsoft.com/documentation/scripts/). Altre informazioni sui [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e come tooorchestrate tooAzure di ripristino con ripristino prevede [qui](https://azure.microsoft.com/blog/?p=166264).

In questa breve esercitazione verrà illustrato come integrare i runbook di Automazione di Azure nei piani di ripristino. Ti consentono di automatizzare attività semplice precedenti richieste interventi manuali e vedere come tooconvert un multi passaggio ripristino in un'azione di ripristino con clic singolo. Verrà esaminato inoltre come risolvere eventuali problemi di un semplice script.

## <a name="protect-hello-application-tooazure"></a>Proteggere tooAzure applicazione hello
Si inizierà con una semplice applicazione costituita da due macchine virtuali. In questo caso, viene usata un'applicazione HRweb di Fabrikam. Fabrikam-HRweb-front-end e back-end Fabrikam Hrweb sono hello due macchine virtuali protette tooAzure usando Azure Site Recovery. macchine virtuali di hello tooprotect usando Azure Site Recovery, procedura hello riportata di seguito.

1. Abilitare la protezione per le macchine virtuali.
2. Verificare che le macchine virtuali hello aver completato la replica iniziale e sta eseguendo la replica.
3. Consente di attendere il completamento della replica iniziale hello e hello lo stato della replica afferma protetti.

## ![](media/site-recovery-runbook-automation/01.png)
In questa esercitazione si creerà un piano di ripristino per Fabrikam HRweb applicazione toofailover hello applicazione tooAzure hello. È quindi verrà integrarlo con un runbook che verrà creato un endpoint nel hello failover pagine web tooserve di macchina virtuale di Azure alla porta 80.

Innanzitutto, verrà creato un piano di ripristino per l’applicazione.

## <a name="create-hello-recovery-plan"></a>Creare il piano di ripristino hello
toorecover hello applicazione tooAzure, è necessario toocreate un piano di ripristino.
Utilizzo di un piano di ripristino che è possibile specificare l'ordine di hello del ripristino delle macchine virtuali. verranno avviati prima e ripristina macchina virtuale Hello inserito nel gruppo 1, e seguire hello di macchina virtuale nel gruppo 2.

Creare un piano di ripristino simile al seguente.

![](media/site-recovery-runbook-automation/12.png)

ulteriori informazioni sui piani di ripristino, leggere la documentazione tooread [qui](https://msdn.microsoft.com/library/azure/dn788799.aspx "qui").

Successivamente, creare hello gli elementi necessari in automazione di Azure.

## <a name="create-hello-automation-account-and-its-assets"></a>Creare account di automazione hello e gli asset
È necessario un runbook toocreate account di automazione di Azure. Se si dispone già di un account, passare indicata dalla scheda di automazione tooAzure ![](media/site-recovery-runbook-automation/02.png)e creare un nuovo account.

1. Assegnare all'account hello tooidentify un nome con.
2. Specificare un'area geografica in cui si desidera account hello tooplace.

È consigliabile tooplace account hello hello stessa area dell'insieme di credenziali di hello ripristino automatico di sistema.

![](media/site-recovery-runbook-automation/03.png)

Successivamente, creare hello asset in hello Account seguenti.

### <a name="add-a-subscription-name-as-asset"></a>Aggiungere un nome di sottoscrizione come asset
1. Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) in hello asset di automazione di Azure e selezionare troppo![](media/site-recovery-runbook-automation/05.png)
2. Selezionare tipo di variabile come hello **stringa**
3. Specificare **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Specificare il nome della sottoscrizione di Azure effettivo come valore della variabile hello.

   ![](media/site-recovery-runbook-automation/07_1.png)

È possibile identificare il nome di hello della sottoscrizione dalla pagina Impostazioni hello dell'account nel portale di Azure hello.

### <a name="add-an-azure-login-credential-as-asset"></a>Aggiungere una credenziale di accesso di Azure come asset
Automazione di Azure Usa una sottoscrizione di Azure PowerShell tooconnect toothe e opera sugli elementi hello non esiste. A tale scopo, è necessario eseguire l'autenticazione usando l'account Microsoft o un account aziendale o dell’istituto di istruzione.
È possibile archiviare le credenziali dell'account hello in toobe un asset in modo sicuro utilizzato dal runbook hello.

1. Aggiungere una nuova impostazione ![](media/site-recovery-runbook-automation/04.png) in hello asset di automazione di Azure e selezionare![](media/site-recovery-runbook-automation/09.png)
2. Selezionare il tipo di credenziale hello come **credenziali di Windows PowerShell**
3. Specificare il nome di hello come **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Specificare nome utente hello e una password toosign-con.

Entrambe queste impostazioni sono ora disponibili negli asset.

![](media/site-recovery-runbook-automation/11.png)

Ulteriori informazioni sulla modalità in cui viene assegnato tooconnect tooyour sottoscrizione tramite PowerShell [qui](/powershell/azure/overview).

Successivamente, si creerà un runbook in automazione di Azure che è possibile aggiungere un endpoint per la macchina virtuale front-end hello dopo il failover.

## <a name="azure-automation-context"></a>Contesto di Automazione di Azure
Ripristino automatico di sistema passa un toohelp runbook toohello variabile di contesto è scrivere script deterministico. È possibile sostenere che i nomi di hello di hello servizio Cloud e hello macchina virtuale sono prevedibili, ma si verifica che non è sempre case hello dovuti toocertain scenari, ad esempio hello uno in cui il nome di hello del nome della macchina virtuale hello potrebbe essere stato modificato a causa caratteri toounsupported in Azure. Di conseguenza queste informazioni vengono passate piano di ripristino toohello ripristino automatico di sistema come parte di hello *contesto*.

Di seguito è riportato un esempio dell'aspetto di variabile di contesto hello.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


tabella Hello riportata di seguito contiene nome e una descrizione per ogni variabile nel contesto di hello.

| **Nome variabile** | **Descrizione** |
| --- | --- |
| RecoveryPlanName |Nome del piano di esecuzione. Consente di sfruttare l'azione in base a nome utilizzando hello stesso script |
| FailoverType |Specifica se hello failover è il test, pianificato o non pianificato. |
| FailoverDirection |Specificare se il ripristino è tooprimary o secondario |
| GroupID |Identificare il numero di gruppo hello nel piano di ripristino hello quando piano hello è in esecuzione |
| VmMap |Matrice di tutte le macchine virtuali hello gruppo hello |
| VMMap key |Chiave univoca (GUID) per ciascuna VM. È hello uguali a quelli hello VMM ID della macchina virtuale hello dove applicabile. |
| RoleName |Nome della macchina virtuale di Azure che viene ripristinato hello |
| CloudServiceName |Nome del servizio Cloud Azure in cui hello viene creata la macchina virtuale. |

hello tooidentify VmMap Key nel contesto di hello è possibile anche passare toohello pagina delle proprietà macchina virtuale in ASR e osservare hello proprietà GUID di VM.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Creare un runbook di Automazione
A questo punto creare hello runbook tooopen porta 80 nella macchina virtuale front-end hello.

1. Creare un nuovo runbook nell'account di automazione di Azure con nome hello hello **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Passare toohello Visualizza di autore del runbook hello e passare alla modalità di bozza hello.
3. Specificare innanzitutto toouse variabile hello come contesto di piano di ripristino hello

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Riconnette toohello sottoscrizione utilizzando un nome delle credenziali e sottoscrizione hello

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Si noti che è utilizzare hello Azure principali: **AzureCredential** e **AzureSubscriptionName** qui.
5. GUID della macchina virtuale hello per cui si desidera endpoint hello tooexpose hello ora specificare i dettagli degli endpoint hello. In questa macchina virtuale front-end hello case.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Questo valore specifica hello protocollo dell'endpoint di Azure, porta locale hello macchina virtuale e la relativa porta pubblica mappata. Queste variabili sono i parametri necessari per hello Azure comandi che aggiungono tooVMs endpoint. Hello VMGUID contiene hello GUID della macchina virtuale hello in che è necessario toooperate.
6. script Hello ora estrarre contesto hello per hello dato GUID di VM e creare un endpoint nella macchina virtuale hello contiene i riferimenti.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Al termine, premere pubblica ![](media/site-recovery-runbook-automation/20.png) tooallow il toobe script disponibili per l'esecuzione.

script completo di Hello è indicato di seguito per riferimento

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Aggiungi piano di ripristino toohello script hello
Una volta script hello è pronto, è possibile aggiungere toohello piano di ripristino creato in precedenza.

1. Nel piano di ripristino hello che è stato creato, scegliere tooadd uno script dopo il gruppo 2. ![](media/site-recovery-runbook-automation/15.png)
2. Specificare un nome per lo script. Questo è solo un nome descrittivo per questo script per la visualizzazione nel piano di ripristino hello.
3. Nello script di tooAzure failover hello: selezionare il nome dell'Account di automazione di Azure hello.
4. Hello runbook di Azure, selezionare runbook hello che è stato creato.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Script sul lato primario
Quando si eseguono tooAzure un failover, è anche possibile scegliere tooexecute script lato primario. Questi script vengono eseguiti nel server VMM hello durante il failover.
Gli script sul lato primario sono disponibili solo nelle fasi precedente e successiva all’arresto. Questo avviene perché è probabile che hello toobe di sito primario non è in genere quando un'eventuale emergenza.
Durante un failover non pianificato, solo se si sceglie di partecipare per operazioni del sito primario, verrà eseguito un tentativo script lato primario di hello toorun. Se non sono raggiungibili o timeout, il failover di hello continuerà toorecover hello macchine virtuali.
Script lato primario sono non disponibili per i siti di VMware/fisici, Hyper-v senza tooAzure VMM protetto - durante il failover tooAzure.
Tuttavia, quando il failback da Azure tooon sedi locali, gli script lato primario (runbook) è possibile utilizzare per tutte le destinazioni, ad eccezione di VMware.

## <a name="test-hello-recovery-plan"></a>Piano di ripristino hello di test
Dopo aver aggiunto piano toohello di hello runbook è possibile avviare un failover di test e visualizzarlo in azione. È sempre consigliabile toorun un tootest di failover di test del tooensure piano ripristino di hello e di applicazione che non siano presenti errori.

1. Selezionare il piano di ripristino hello e avviare un failover di test.
2. Durante l'esecuzione di piani hello, è possibile visualizzare se hello runbook è stato eseguito o non mediante il relativo stato.

   ![](media/site-recovery-runbook-automation/17.png)
3. È inoltre possibile visualizzare hello dettagliate sullo stato di esecuzione di runbook nella pagina processi di automazione di Azure hello per hello runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. Dopo aver completato il failover hello, oltre al risultato dell'esecuzione runbook hello, è possibile visualizzare se l'esecuzione di hello ha esito positivo o non visita pagina macchina virtuale di Azure hello e analizzando gli endpoint hello.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Script di esempio
Anche se abbiamo esaminato in dettaglio automazione uno comunemente utilizzato l'operazione di aggiunta di una macchina virtuale di Azure di tooan endpoint in questa esercitazione, è possibile eseguire un numero di altre attività di automazione potente utilizzando l'automazione di Azure. Microsoft e hello community di automazione di Azure forniscono i runbook di esempio che consentono di iniziare a creare la propria soluzioni e i runbook di utilità, che è possibile utilizzare come blocchi predefiniti per le attività di automazione più grandi. Iniziare a utilizzare dalla raccolta hello e compilare i piani di ripristino di un solo clic potente per le applicazioni con Azure Site Recovery.

## <a name="additional-resources"></a>Risorse aggiuntive
[Panoramica di Automazione di Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")

[Script di esempio di Automazione di Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")
