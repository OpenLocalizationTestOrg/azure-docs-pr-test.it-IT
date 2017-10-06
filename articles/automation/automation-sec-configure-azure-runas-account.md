---
title: aaaConfigure eseguire come Account di Azure | Documenti Microsoft
description: "In questa esercitazione viene tramite l'utilizzo di creazione, test e l'esempio hello di autenticazione di entità di sicurezza in automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nome entità servizio, setspn, autenticazione di Azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Autenticare runbook con un account RunAs di Azure
In questo articolo viene illustrato come l'account tooconfigure un'automazione di Azure hello portale di Azure. toodo in tal caso, utilizzare hello Run As account funzionalità tooauthenticate runbook di gestione delle risorse di Azure Resource Manager o Gestione servizi di Azure.

Quando si crea un account di automazione in hello portale di Azure, viene creata automaticamente due account:

* Un account RunAs. Questo account crea un'entità servizio in Azure Active Directory (Azure AD) e un certificato. Assegna inoltre hello collaboratore basata sui ruoli access control (RBAC), che gestisce le risorse di gestione delle risorse con i runbook.
* Un account RunAs classico. Questo account consente di caricare un certificato di gestione, viene utilizzato toomanage gestione dei servizi o le risorse classiche utilizzando runbook.

Creazione di un account semplifica il processo di hello per l'utente e consente di che iniziare rapidamente la creazione e distribuzione toosupport runbook di automazione dell'automazione è necessario.

Con un account RunAs e un account RunAs classico è possibile:

* Fornire un modo standardizzato di tooauthenticate Azure quando si gestiscono Gestione risorse o le risorse di gestione dei servizi da runbook nel portale di Azure hello.
* Automatizzare l'uso di hello dei runbook globale, che è possibile configurare avvisi di Azure.

> [!NOTE]
> Hello [funzionalità di integrazione di Azure avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) con l'automazione runbook globale richiede un account di automazione che è configurato con un account RunAs e un classico account RunAs. È possibile selezionare un account di automazione già definito account RunAs e classico runas oppure è possibile scegliere un nuovo account di automazione toocreate.
>  

Questo articolo illustra come toocreate un account di automazione da hello portale di Azure, aggiornare un account di automazione usando Azure PowerShell, gestire la configurazione di account hello e l'autenticazione dei runbook.

Prima di iniziare la creazione di un account di automazione, è una buona idea toounderstand e considerare hello seguenti:

* Creazione di un account di automazione non influenza gli account di automazione che è potrebbe essere già stato creato in hello classic o il modello di distribuzione di gestione risorse.
* il processo di Hello funziona solo per gli account di automazione creati in hello portale di Azure. Il tentativo di un account dal portale di Azure classico hello toocreate, configurazione runas hello dell'account non viene replicato.
* Se si dispone già runbook e risorse, quali le pianificazioni o variabili, le risorse classiche di toomanage sul posto, e si desidera tooauthenticate runbook con hello nuovo classico account RunAs, eseguire una delle seguenti hello:

  * toocreate un classico account RunAs, seguire le istruzioni di hello nella sezione "Gestire l'account Esegui come" hello. 
  * tooupdate account esistente, utilizzare hello PowerShell script nella sezione "Aggiornare l'account di automazione usando PowerShell" hello.
* tooauthenticate utilizzando hello nuovo account RunAs e classico eseguire come account di automazione di, è necessario che i runbook esistenti con il codice di esempio fornito nella sezione hello di hello toomodify [esempi di codice di autenticazione](#authentication-code-examples).

    >[!NOTE]
    >account RunAs Hello è per l'autenticazione rispetto alle risorse di gestione risorse usando hello entità di servizio basata su certificati. Hello Classic account RunAs è per l'autenticazione nel servizio Gestione risorse con un certificato di gestione.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Creare un account di automazione da hello portale di Azure
In questa sezione creare un account di automazione di Azure dal portale di Azure, che a sua volta crea un account RunAs sia un classico account RunAs hello.

>[!NOTE]
>toocreate un account di automazione, è necessario essere un membro del ruolo Amministratori servizio hello o coamministratori della sottoscrizione hello che concede l'accesso toohello sottoscrizione. È inoltre necessario essere aggiunto come istanza di Active Directory della sottoscrizione di toothat utente predefinito. account Hello non è necessario toobe assegnato un ruolo con privilegi.
>
>Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di ruoli di toohello CO-amministratore della sottoscrizione di hello, verranno aggiunti tooActive Directory come guest. In questo caso, si riceverà un "non si dispone delle autorizzazioni toocreate..." visualizzazione dell'avviso hello **aggiungere Account di automazione** blade.
>
>Gli utenti che sono stati aggiunti al ruolo di CO-amministratore toohello innanzitutto può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake loro un utente in Active Directory completa. tooverify tale situazione hello **Azure Active Directory** riquadro nel portale di Azure selezionando hello **utenti e gruppi**, se si seleziona **tutti gli utenti** e, dopo aver selezionato utente specifico di Hello, selezionando **profilo**. valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.
>

1. Accedi a portale di Azure con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello toohello.

2. Selezionare **Account di automazione**.

3. In hello **gli account di automazione** pannello, fare clic su **Aggiungi**.
Hello **aggiungere Account di automazione** apre blade.

 ![pannello "Aggiungi Account di automazione" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Se l'account non è un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione di hello, hello seguente avviso è visualizzato nella hello **aggiungere Account di automazione** pannello:
   >
   >![Aggiungi account di Automazione, avviso](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. In hello **aggiungere Account di automazione** pannello in hello **nome** , digitare un nome per il nuovo account di automazione.

5. Se si dispone di più di una sottoscrizione, hello seguenti:

    a. In **sottoscrizione**, specificare un nuovo account hello.

    b. In **Gruppo di risorse** fare clic su **Crea nuovo** o **Usa esistente**.

    c. In **Località** specificare un data center di Azure.

6. In **Crea un account RunAs di Azure** scegliere **Sì** e quindi fare clic su **Crea**.

   > [!NOTE]
   > Se si sceglie di non toocreate hello account RunAs selezionando **n**, viene visualizzato un messaggio di avviso hello **aggiungere Account di automazione** blade. Nonostante hello account viene creato nel portale di Azure hello, non presenta un'identità di autenticazione corrispondente all'interno del classica o servizio directory di gestione risorse di sottoscrizione. Di conseguenza, hello non disponga di alcun tooresources accesso nella sottoscrizione. Questo scenario impedisce ai runbook che fanno riferimento a questo account di autenticarsi ed eseguire attività sulle risorse in tali modelli di distribuzione.
   >
   > ![Messaggio di avviso nel Pannello di "Aggiungere Account di automazione" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Inoltre, poiché non viene creata un'entità servizio hello, ruolo di collaboratore hello non è assegnato.
   >

7. Mentre Azure crea account di automazione hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

### <a name="resources"></a>Risorse
Quando viene creato correttamente hello account di automazione, varie risorse vengono create automaticamente per l'utente. risorse Hello sono riepilogate nella hello le due tabelle seguenti:

#### <a name="run-as-account-resources"></a>Risorse dell'account RunAs

| Risorsa | Descrizione |
| --- | --- |
| Runbook AzureAutomationTutorial | Un runbook grafico di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello. |
| Runbook AzureAutomationTutorialScript | Un runbook di PowerShell di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello. |
| AzureRunAsCertificate | asset del certificato Hello che viene creato automaticamente quando si crea un account di automazione o utilizza hello seguente script di PowerShell per un account esistente. certificato Hello consente tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure Resource Manager dai runbook. certificato Hello ha una durata di un anno. |
| AzureRunAsConnection | asset della connessione Hello che viene creato automaticamente quando si crea un account di automazione o utilizza uno script di PowerShell hello per un account esistente. |

#### <a name="classic-run-as-account-resources"></a>Risorse dell'account RunAs classico

| Risorsa | Descrizione |
| --- | --- |
| Runbook AzureClassicAutomationTutorial | Un runbook grafico di esempio che ottiene tutte le macchine virtuali hello che vengono creati usando il modello di distribuzione classica hello in una sottoscrizione con hello Classic account RunAs (certificato) e quindi scrive lo stato e nome della macchina virtuale hello. |
| Runbook di script AzureClassicAutomationTutorial | Un runbook di PowerShell di esempio che ottiene tutti hello delle macchine virtuali classiche in una sottoscrizione utilizzando hello Classic account RunAs (certificato) e quindi scrive hello lo stato e nome della macchina virtuale. |
| AzureClassicRunAsCertificate | asset del certificato creato automaticamente Hello usare tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook. certificato Hello ha una durata di un anno. |
| AzureClassicRunAsConnection | asset di connessione creati automaticamente Hello usare tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook. |

## <a name="verify-run-as-authentication"></a>Verificare l'autenticazione con RunAs
Eseguire un test di piccole dimensioni di tooconfirm che può eseguire l'autenticazione tramite hello nuovo account RunAs.

1. Nel portale di Azure hello, aprire l'account di automazione hello creato in precedenza.

2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.

3. Seleziona hello **AzureAutomationTutorialScript** runbook, quindi fare clic su **avviare** toostart hello runbook. si verifica Hello seguenti eventi:
 * Oggetto [processo del runbook](automation-runbook-execution.md) viene creato, hello **processo** blade viene visualizzata e viene visualizzato lo stato del processo hello in hello **riepilogo** riquadro.
 * lo stato del processo Hello inizia come **in coda**, che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.
 * stato Hello diventa **iniziale** quando un thread di lavoro attestazioni processo hello.
 * stato Hello diventa **esecuzione** quando runbook hello viene avviata l'esecuzione.
 * Completamento dell'esecuzione di processo del runbook hello, verrà visualizzato lo stato **completato**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.  
Hello **Output** pannello è visualizzato, contenente runbook hello autenticato e ha restituito un elenco di tutte le risorse disponibili nel gruppo di risorse hello correttamente.

5. Chiude hello **Output** pannello tooreturn toohello **riepilogo** blade.

6. Chiude hello **riepilogo** blade e hello corrispondente **AzureAutomationTutorialScript** pannello runbook.

## <a name="verify-classic-run-as-authentication"></a>Verificare l'autenticazione con RunAs classico
Eseguire una piccola simile test tooconfirm che può eseguire l'autenticazione tramite hello nuovo classico account RunAs.

1. Nel portale di Azure hello, aprire l'account di automazione hello creato in precedenza.

2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.

3. Seleziona hello **AzureClassicAutomationTutorialScript** runbook, quindi fare clic su **avviare** troppo avviare runbook hello. si verifica Hello seguenti eventi:

 * Oggetto [processo del runbook](automation-runbook-execution.md) viene creato, hello **processo** blade viene visualizzata e viene visualizzato lo stato del processo hello in hello **riepilogo** riquadro.
 * lo stato del processo Hello inizia come **in coda**, che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.
 * stato Hello diventa **iniziale** quando un thread di lavoro attestazioni processo hello.
 * stato Hello diventa **esecuzione** quando runbook hello viene avviata l'esecuzione.
 * Completamento dell'esecuzione di processo del runbook hello, verrà visualizzato lo stato **completato**.

    ![Verifica del runbook dell'entità di sicurezza](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.  
Hello **Output** pannello è visualizzato, contenente runbook hello autenticato e ha restituito un elenco di tutte le macchine virtuali classiche nella sottoscrizione hello correttamente.

5. Chiude hello **Output** pannello tooreturn toohello **riepilogo** blade.

6. Chiude hello **riepilogo** blade e hello corrispondente **AzureAutomationTutorialScript** pannello runbook.

## <a name="managing-your-run-as-account"></a>Gestire l'account RunAs
A un certo punto prima che scada l'account di automazione, sarà necessario toorenew hello certificato. Se si ritiene che hello account RunAs sia stata compromessa, è possibile eliminare e ricrearlo. Questa sezione viene descritto come tooperform queste operazioni.

### <a name="self-signed-certificate-renewal"></a>Rinnovo del certificato autofirmato
il certificato autofirmato Hello creato per l'account RunAs hello scade un anno dalla data di hello di creazione. È possibile rinnovarlo in qualsiasi momento prima della scadenza. Quando si rinnovarlo, certificato valido corrente hello è conservate tooensure che tutti i runbook che vengono messe in coda fino o attivamente in esecuzione e che l'autenticazione con hello account RunAs, non sono influenzati negativamente. certificato Hello rimane valido fino alla relativa data di scadenza.

> [!NOTE]
> Se si utilizza questa opzione è stata configurata l'automazione Run As account toouse un certificato emesso da un'autorità di certificazione dell'organizzazione, certificato aziendale hello verrà sostituito da un certificato autofirmato.

hello toorenew certificati, hello seguenti:

1. Nel portale di Azure hello, aprire l'account di automazione hello.

2. In hello **Account di automazione** pannello in hello **Account proprietà** riquadro, in **impostazioni Account**selezionare **account RunAs**.

    ![Riquadro delle proprietà dell'account di Automazione](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. In hello **account RunAs** Pannello proprietà, seleziona entrambi hello eseguiti come account o hello Classic account RunAs che si desidera che il certificato hello toorenew per.

4. In hello **proprietà** pannello hello account selezionato, fare clic su **Rinnova certificato**.

    ![Rinnovare il certificato per l'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Mentre viene rinnovato il certificato di hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Eliminare un account RunAs o un account RunAs classico
Questa sezione viene descritto come toodelete e ricreare un account RunAs o classico runas. Quando si esegue questa azione, viene mantenuto hello account di automazione. Dopo aver eliminato un account RunAs o classico runas, è possibile crearlo nuovamente in hello portale di Azure.

1. Nel portale di Azure hello, aprire l'account di automazione hello.

2. In hello **account di automazione** in hello account riquadro proprietà, seleziona pannello **account RunAs**.

3. In hello **account RunAs** Pannello proprietà, selezionare entrambi hello account RunAs classico RunAs dell'account che si desidera toodelete. Quindi, nella hello **proprietà** pannello hello account selezionato, fare clic su **eliminare**.

 ![Eliminare un account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Durante l'eliminazione di account hello in corso, è possibile monitorare i progressi di hello in **notifiche** dal menu di hello.

5. Dopo aver eliminato l'account di hello, è possibile crearlo nuovamente su hello **account RunAs** Pannello proprietà selezionando hello opzione create **Azure Account runas**.

 ![Ricreare hello automazione account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Errore di configurazione
Alcuni elementi di configurazione necessari per toofunction di account RunAs o classico runas hello correttamente potrebbe essere stati eliminati o creati in modo non corretto durante l'installazione iniziale. gli elementi di Hello includono:

* Asset del certificato
* Asset di connessione
* Account RunAs è stato rimosso dal ruolo di collaboratore hello
* Entità servizio o applicazione in Azure AD

In altre istanze di una configurazione errata e hello precedente hello account di automazione rileva hello cambia e visualizza lo stato di *incompleto* su hello **account RunAs** Pannello proprietà per hello account.

![Stato di configurazione Incompleto dell'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Quando si seleziona account RunAs hello, hello account **proprietà** riquadro Visualizza hello seguente messaggio di errore:

![Messaggio di avviso relativo alla configurazione incompleta dell'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Per risolvere rapidamente i problemi di account RunAs, eliminazione e ricreazione account hello.

## <a name="update-your-automation-account-by-using-powershell"></a>Aggiornare l'account di Automazione usando PowerShell
È possibile utilizzare l'account di automazione esistente PowerShell tooupdate se:

* Si crea un account di automazione, ma rifiuta toocreate account RunAs hello.
* Già in uso un risorse di gestione risorse di automazione account toomanage e si desidera tooupdate hello account tooinclude hello account RunAs per l'autenticazione di runbook.
* Già in uso un'automazione account toomanage classico alle risorse e si desidera tooupdate è toouse hello Classic account RunAs anziché creare un nuovo account e la migrazione tooit i runbook e le risorse.   
* Si desidera toocreate Esegui come e un classico account RunAs utilizzando un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA).

script Hello è hello seguenti prerequisiti:

* script di Hello può essere eseguito solo in Windows 10 e Windows Server 2016 con moduli di gestione risorse di Azure 2.01 e versioni successive. Non sono supportate le versioni precedenti di Windows.
* Azure PowerShell 1.0 e versioni successive. Per informazioni sulla versione di hello PowerShell 1.0, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* Un account di automazione cui viene fatto riferimento come valore hello hello *– AutomationAccountName* e *- ApplicationDisplayName* parametri hello lo script di PowerShell seguente.

i valori hello tooget per *SubscriptionID*, *gruppo di risorse*, e *AutomationAccountName*, che sono parametri obbligatori per gli script hello, hello seguenti:
1. In hello portale di Azure, selezionare l'account di automazione in hello **account di automazione** blade e quindi selezionare **tutte le impostazioni**. 
2. In hello **tutte le impostazioni** pannello, in **impostazioni Account**selezionare **proprietà**. 
3. Notare i valori hello in hello **proprietà** blade.

![Pannello di "Proprietà" Hello automazione account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Creare lo script di PowerShell per l'account RunAs
Questo script di PowerShell include il supporto per hello seguenti configurazioni:

* Creare un account RunAs usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato enterprise.
* Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici.

A seconda opzione di configurazione hello selezionata, lo script di hello crea hello seguenti elementi.

**Per gli account RunAs:**

* Crea un Azure AD applicazione toobe esportato con entrambi hello autofirmato o chiave pubblica del certificato dell'organizzazione, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna hello ruolo Collaboratore per conto di hello in corrente sottoscrizione. È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).
* Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.
* Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.

**Per gli account RunAs classici:**

* Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.
* Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.

>[!NOTE]
> Se si seleziona l'opzione desiderata per la creazione di un classico account RunAs, dopo l'esecuzione di script hello, caricamento hello pubblica Gestione toohello (estensione del nome file con estensione cer) dell'archivio certificati per la sottoscrizione di hello che hello account di automazione è stato creato.
> 

tooexecute hello script e caricare il certificato di hello, hello seguenti:

1. Salvare lo script seguente nel computer in uso hello. In questo esempio, salvarlo con il nome file hello *New RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Fare clic sul menu **Start** del computer e avviare **Windows PowerShell** con diritti utente elevati.

3. Da hello elevati shell della riga di comando di PowerShell, passare toohello cartella che contiene lo script hello creato nel passaggio 1.

4. Eseguire script hello utilizzando i valori dei parametri hello per la configurazione di hello desiderate.

    **Creare un account RunAs usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Creare un account RunAs e un account RunAs classico usando un certificato enterprise**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Dopo l'esecuzione di script hello è, sarà richiesta tooauthenticate con Azure. Accedere con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello.
    >
    >

Dopo l'esecuzione dello script hello completata, si noti seguenti hello:
* Se è stato creato un classico account RunAs con un certificato pubblico autofirmato (file con estensione cer), script hello crea e Salva toohello cartella dei file temporanei nel computer in uso nel profilo utente hello *%USERPROFILE%\AppData\Local\Temp*, sessione di PowerShell hello tooexecute utilizzati.
* Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato. Seguire le istruzioni di hello per [caricando un toohello certificato API di Gestione portale di Azure classico](../azure-api-management-certs.md)e convalidare una configurazione di hello delle credenziali con risorse di gestione dei servizi tramite hello [codice di esempio tooauthenticate con servizio di gestione delle risorse](#sample-code-to-authenticate-with-service-management-resources). 
* Se è stato eseguito *non* creare un classico account RunAs, l'autenticazione con le risorse di gestione delle risorse e convalidare la configurazione di credenziali di hello utilizzando hello [codice per l'autenticazione con gestione del servizio di esempio risorse](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Tooauthenticate codice di esempio con le risorse di gestione risorse
È possibile utilizzare il seguente hello aggiornato codice di esempio, prelevato hello *AzureAutomationTutorialScript* runbook di esempio, tooauthenticate utilizzando hello Run As account toomanage Gestione risorse alle risorse con i runbook.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp è tooeasily funziona tra più sottoscrizioni, script hello include due ulteriori righe di codice che supportano che fanno riferimento a un contesto di sottoscrizione. Un asset della variabile denominato *SubscriptionId* contiene hello ID di sottoscrizione hello. Dopo aver hello `Add-AzureRmAccount` cmdlet istruzione hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet viene dichiarata con il set di parametri di hello *- SubscriptionId*. Se il nome di variabile hello è troppo generico, è possibile correggerlo tooinclude un prefisso o utilizzare un altro toomake convenzione denominazione si tooidentify più semplice. In alternativa, è possibile utilizzare il set di parametri di hello *- SubscriptionName* anziché *- SubscriptionId* con un asset della variabile corrispondente.

i cmdlet utilizzati per l'autenticazione in runbook hello, Hello `Add-AzureRmAccount`, hello utilizza *ServicePrincipalCertificate* set di parametri. Consente l'autenticazione tramite certificato principale hello del servizio, non le credenziali utente hello.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Tooauthenticate codice di esempio con le risorse di gestione dei servizi
È possibile utilizzare hello seguente codice di esempio aggiornato, che viene utilizzato da hello *AzureClassicAutomationTutorialScript* runbook di esempio, tooauthenticate utilizzando hello Classic account RunAs toomanage le risorse classiche con il runbook.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Passaggi successivi
* [Oggetti applicazione e oggetti entità servizio in Azure AD](../active-directory/active-directory-application-objects.md)
* [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md)
* [Panoramica sui certificati per i servizi cloud di Azure](../cloud-services/cloud-services-certs-create.md)
