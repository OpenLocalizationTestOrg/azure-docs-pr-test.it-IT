---
title: aaaAdd piani toorecovery runbook di automazione di Azure in Azure Site Recovery | Documenti Microsoft
description: "Informazioni su come Azure Site Recovery può essere utile per estendere i piani di ripristino tramite Automazione di Azure. Informazioni su come le attività durante il ripristino tooAzure toocomplete complesso."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Aggiungere i piani toorecovery runbook di automazione di Azure
In questo articolo viene descritto l'integrazione di Azure Site Recovery con toohelp di automazione di Azure estendere i piani di ripristino. I piani di ripristino possono orchestrare il ripristino di macchine virtuali protette con Site Recovery. I piani di ripristino di lavoro per il cloud secondario tooa di replica e per la replica tooAzure. I piani di ripristino consentono inoltre di garantire il ripristino di hello **in modo coerente accurate**, **repeatable**, e **automatizzati**. Se si esegue il failover tooAzure le macchine virtuali, integrazione con automazione di Azure estende i piani di ripristino. È possibile utilizzarlo tooexecute runbook, che offrono l'attività di automazione potenti.

Nel caso di nuova tooAzure automazione, è possibile [iscriversi](https://azure.microsoft.com/services/automation/) e [scaricare gli script di esempio](https://azure.microsoft.com/documentation/scripts/). Per ulteriori informazioni e toolearn come tooorchestrate ripristino tooAzure utilizzando [i piani di ripristino](https://azure.microsoft.com/blog/?p=166264), vedere [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Questo articolo descrive come è possibile integrare i runbook di Automazione di Azure nei piani di ripristino. Utilizziamo esempi tooautomate attività di base che richiedevano in precedenza un intervento manuale. È inoltre possibile descrivere come tooconvert tooa un ripristino di più passaggi con clic singolo un'operazione di ripristino.

## <a name="customize-hello-recovery-plan"></a>Personalizzare il piano di ripristino hello
1. Passare toohello **Site Recovery** pannello risorsa piano di ripristino. Per questo esempio, il piano di ripristino di hello ha due tooit aggiunte le macchine virtuali, per il ripristino. toobegin aggiunta di un runbook, fare clic su hello **Personalizza** scheda.

    ![Fare clic sul pulsante Personalizza hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Fare clic con il pulsante destro del mouse su **Gruppo 1: Avvio** e quindi scegliere **Aggiungi post-azione**.

    ![Fare clic con il pulsante destro del mouse su Gruppo 1: Avvio e scegliere Aggiungi post-azione](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Fare clic su **Choose a script** (Scegli uno script).

4. In hello **azione Aggiorna** blade, script hello nome **Hello World**.

    ![Pannello di azione di aggiornamento Hello](media/site-recovery-runbook-automation-new/update-rp.png)

5. Immettere il nome di un account di Automazione.
    >[!NOTE]
    > account di automazione Hello può trovarsi in qualsiasi area di Azure. account di automazione Hello deve essere in hello stessa sottoscrizione dell'insieme di credenziali di Azure Site Recovery hello.

6. Nell'account di Automazione selezionare un runbook. Questo runbook è hello dello script eseguito durante l'esecuzione di hello hello del piano di ripristino, dopo il ripristino di hello del primo gruppo di hello.

7. script di hello toosave, fare clic su **OK**. script di Hello viene aggiunto troppo**gruppo 1: post-passaggi**.

    ![Post-azione Gruppo 1: Avvio](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Considerazioni per l'aggiunta di uno script

* Per le opzioni troppo**eliminare un passaggio** o **aggiornare script hello**, fare doppio clic su script hello.
* Uno script è possibile eseguire in Azure durante il failover da un tooAzure macchina locale. Inoltre possibile eseguire in Azure come sito primario di script prima della chiusura, durante il failback da tooan Azure nel computer locale.
* Quando è in esecuzione, inserisce un contesto del piano di ripristino. Hello di esempio seguente viene illustrata una variabile di contesto:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Hello nella tabella seguente sono elencati il nome di hello e una descrizione di ogni variabile nel contesto di hello.

    | **Nome variabile** | **Descrizione** |
    | --- | --- |
    | RecoveryPlanName |nome Hello del piano di hello in esecuzione. Questa variabile consente di eseguire azioni diverse in base a nome piano di ripristino hello. È inoltre possibile utilizzare script hello. |
    | FailoverType |Specifica se il failover hello è un test, pianificato o non pianificato. |
    | FailoverDirection |Specifica se il ripristino del sito primario o secondario di tooa. |
    | GroupID |Identifica il numero di gruppo hello nel piano di ripristino hello quando piano hello è in esecuzione. |
    | VmMap |Matrice di tutte le macchine virtuali nel gruppo di hello. |
    | VMMap key |Chiave univoca (GUID) per ogni macchina virtuale. Di hello identico hello Azure Virtual Machine Manager (VMM) ID di hello macchina virtuale, se applicabile. |
    | SubscriptionId |ID sottoscrizione di Azure Hello in cui hello VM è stato creato. |
    | RoleName |nome Hello di hello macchina virtuale di Azure che viene ripristinato. |
    | CloudServiceName |nome del servizio cloud di Azure Hello che in cui hello VM è stato creato. |
    | ResourceGroupName|nome del gruppo di risorse di Azure Hello che in cui hello VM è stato creato. |
    | RecoveryPointId|timestamp di Hello per quando viene recuperato hello macchina virtuale. |

* Verificare che account di automazione di hello disponga hello seguenti moduli:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Tutti i moduli devono essere di versioni compatibili. Un modo semplice di tooensure che tutti i moduli siano compatibili è versioni più recenti di hello toouse di tutti i moduli di hello.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Accedere a tutte le macchine virtuali di hello VMMap in un ciclo
Utilizzare hello seguendo tooloop codice tra tutte le macchine virtuali di Microsoft VMMap hello:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hello risorsa nome e il ruolo nome valori di gruppo sono vuoti quando script hello è un gruppo di avvio tooa pre-azione. i valori Hello vengono popolati solo se ha esito positivo hello VM del gruppo di failover. script Hello è post-un'azione del gruppo di avvio hello.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Utilizzare hello stesso runbook di automazione in più piani di ripristino

È possibile usare un unico script in più piani di ripristino servendosi di variabili esterne. È possibile utilizzare [le variabili di automazione di Azure](../automation/automation-variables.md) toostore parametri che è possibile passare per il ripristino di un piano di esecuzione. Aggiungendo nome piano di ripristino hello come variabile toohello prefisso, è possibile creare le singole variabili per ogni piano di ripristino. Quindi, è possibile usare le variabili di hello come parametri. È possibile modificare un parametro senza modificare script hello, ma ancora modifica hello hello modo il funzionamento di script.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Usare una variabile di tipo stringa semplice nello script di un runbook

In questo esempio, uno script accetta input hello di un gruppo di sicurezza di rete (gruppo) e le applica toohello macchine virtuali di un piano di ripristino.

Per toodetect di script hello piano di ripristino è in esecuzione, utilizzare contesto piano di ripristino hello:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply un gruppo esistente, è necessario conoscere il nome di gruppo hello e nome del gruppo di risorse gruppo hello. Usare queste variabili come input per gli script dei piani di ripristino. toodo, creare due variabili in hello asset di account di automazione. Aggiungere nome hello hello del piano di ripristino che si siano creando parametri hello per come nome di variabile toohello prefisso.

1. Creare un nome di gruppo hello toostore variabile. Aggiungere un nome di variabile toohello prefisso utilizzando il nome di hello hello del piano di ripristino.

    ![Creare una variabile per il nome del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var1.png)

2. Creare nome gruppo di risorse del gruppo una variabile toostore hello. Aggiungere un nome di variabile toohello prefisso utilizzando il nome di hello hello del piano di ripristino.

    ![Creare un nome del gruppo di risorse del gruppo sicurezza di rete](media/site-recovery-runbook-automation-new/var2.png)


3.  Nello script hello utilizzare hello seguente i valori delle variabili riferimento codice tooget hello:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Utilizzare le variabili di hello in hello runbook tooapply hello NSG toohello interfaccia di rete di hello failover VM:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Per ogni piano di ripristino, creare variabili indipendenti, in modo che è possibile riutilizzare script hello. Aggiungere un prefisso con nome piano di ripristino hello. Per uno script completo, end-to-end per questo scenario, vedere [aggiungere un tooVMs IP e di gruppo pubblico durante il failover di test di un piano di ripristino di Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Utilizzare una variabile complessa di toostore ulteriori informazioni

Si consideri uno scenario in cui si desidera tooturn un singolo script in un indirizzo IP pubblico in macchine virtuali specifiche. In un altro scenario, è opportuno tooapply NSGs diversi in diverse macchine virtuali (non su tutte le macchine virtuali). È possibile creare uno script riutilizzabile per qualsiasi piano di ripristino. Ogni piano di ripristino può avere un numero variabile di macchine virtuali. Ad esempio, un ripristino di SharePoint ha due front-end. Un'applicazione line-of-business (LOB) semplice ha un solo front-end. Non è possibile creare variabili separate per ogni piano di ripristino. 

Nell'esempio seguente di hello, usare una tecnica di nuovo e creare un [variabile complessa](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) nell'asset di account di automazione di Azure hello. Questo risultato si ottiene specificando più valori. È necessario usare Azure PowerShell toocomplete hello alla procedura seguente:

1. In PowerShell, eseguire l'accesso tooyour sottoscrizione di Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. parametri di hello toostore, creare hello complesso variabile utilizzando il nome di hello hello del piano di ripristino:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. In questa variabile complesso, **VMDetails** è hello ID macchina virtuale per hello protetto macchina virtuale. tooget hello, ID di macchina virtuale, nel portale di Azure hello visualizzare le proprietà VM hello. Hello schermata riportata di seguito viene illustrata una variabile che archivia i dettagli di hello di due macchine virtuali:

    ![Utilizzare hello ID macchina virtuale come hello GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Usare questa variabile nel runbook. Se hello indicato che GUID di VM viene trovato nel contesto di piano di ripristino hello, applicare hello NSG hello VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. Nel runbook, scorrere in ciclo hello macchine virtuali del contesto di piano di ripristino hello. Verificare l'esistenza di hello VM in **$VMDetailsObj**. Se esiste, è possibile accedere alle proprietà di hello di hello tooapply variabile hello gruppo:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

È possibile utilizzare hello stesso script per i piani di ripristino diverso. Immettere i parametri diversi archiviando hello corrispondente il piano di ripristino tooa in variabili diverse.

## <a name="sample-scripts"></a>Script di esempio

tooyour gli script di esempio toodeploy account di automazione, fare clic su hello **distribuire tooAzure** pulsante.

[![Distribuire tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Per un altro esempio, vedere hello video seguenti. Viene illustrato come toorecover tooAzure di applicazione WordPress una a due livelli:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Risorse aggiuntive
* [Account RunAs per il servizio Automazione di Azure](../automation/automation-sec-configure-azure-runas-account.md)
* [Panoramica di Automazione di Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Panoramica di Automazione di Azure")
* [Script di esempio di Automazione di Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Script di esempio di Automazione di Azure")
