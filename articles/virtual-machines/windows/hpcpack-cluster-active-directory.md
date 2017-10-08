---
title: aaaHPC Pack cluster con Azure Active Directory | Documenti Microsoft
description: Informazioni su come toointegrate un' 2016 Pack HPC cluster in Azure con Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Gestire un cluster HPC Pack in Azure con Azure Active Directory
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supporta l'integrazione con [Azure Active Directory](../../active-directory/index.md) (Azure AD) per gli amministratori che distribuiscono un cluster HPC Pack in Azure.



Seguire i passaggi di hello in questo articolo per hello seguenti attività di livello elevata: 
* Integrare manualmente il cluster HPC Pack con il proprio tenant di Azure AD
* Gestire e pianificare i processi nel cluster HPC Pack in Azure 

Integrazione di una soluzione di cluster HPC Pack con Azure AD segue i passaggi standard toointegrate altri servizi e applicazioni. In questo articolo si presuppone di avere dimestichezza con la gestione utente di base in Azure AD. Per ulteriori informazioni e in background, vedere hello [documentazione di Azure Active Directory](../../active-directory/index.md) e hello seguente sezione.

## <a name="benefits-of-integration"></a>Vantaggi dell'integrazione


Azure Active Directory (Azure AD) è un multi-tenant basati su cloud directory e identità del servizio di gestione che fornisce accesso single sign-on (SSO) toocloud soluzioni.

Integrazione di un cluster HPC Pack con Azure AD è possibile realizzare hello gli obiettivi seguenti:

* Rimuovere i controller di dominio Active Directory tradizionale hello dal cluster HPC Pack hello. Questo può ridurre i costi di hello di Gestione cluster di hello se questo non è necessario per l'azienda e processo di distribuzione di velocizzare hello.
* Sfruttare hello seguenti vantaggi che vengono attivata la modalità da Azure AD:
    *   Single sign-on 
    *   Uso di un'identità di Active Directory locale per il cluster HPC Pack hello in Azure 

    ![Ambiente di Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Prerequisiti
* **Cluster HPC Pack 2016 distribuito nelle macchine virtuali di Azure**: per la procedura vedere [Distribuire un cluster HPC Pack 2016 in Azure](hpcpack-2016-cluster.md). È necessario il nome DNS hello del nodo head hello e credenziali di hello di un amministratore cluster per completare i passaggi di hello in questo articolo.

  > [!NOTE]
  > L'integrazione di Azure Active Directory non è supportata nelle versioni di HPC Pack precedenti a quella del 2016.



* **Computer client** -è necessario un Windows o Windows Server client computer eseguito troppo HPC Pack utilità client. Se si desidera solo portale web di HPC Pack hello toouse o processi toosubmit API REST, è possibile utilizzare tutti i computer client di propria scelta.

* **Utilità client di HPC Pack** -installare le utilità client di HPC Pack hello nel computer client hello tramite pacchetto di installazione gratuito hello disponibile da Microsoft Download Center hello.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Passaggio 1: Registrare i server di cluster HPC hello con tenant di Azure AD
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Fare clic su **Active Directory** in hello menu a sinistra e quindi fare clic sulla directory desiderata di hello nella sottoscrizione. È necessario disporre risorse tooaccess autorizzazione nella directory hello.
3. Fare clic su **Utenti** e verificare la presenza di account utente già creati o configurati.
4. Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**. Immettere le seguenti informazioni nella procedura guidata hello hello:
    * **Nome**: HPCPackClusterServer
    * **Tipo**: selezionare **Applicazione Web e/o API Web**
    * **URL di accesso**: hello URL di base per un esempio di hello, per impostazione predefinita`https://hpcserver`
    * **URI ID app** - `https://<Directory_name>/<application_name>`. Sostituire `<Directory_name`> con nome completo del tenant di Azure AD, ad esempio, hello `hpclocal.onmicrosoft.com`e sostituire `<application_name>` con nome hello scelto in precedenza.

5. Dopo aver aggiunto l'applicazione hello, fare clic su **configura**. Configurare hello le proprietà seguenti:
    * Selezionare **Sì** per **L'applicazione è multi-tenant**
    * Selezionare **Sì** per **utente assegnazione tooaccess obbligatorio app**.

6. Fare clic su **Salva**. Al termine del salvataggio, fare clic su **Gestisci manifesto**. Questa azione permette di scaricare il file JavaScript Object Notation (JSON) del manifesto dell'applicazione. Modifica manifesto di hello scaricato individuando hello `appRoles` impostazione e l'aggiunta di hello ruolo applicazione seguente:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Salvare il file hello. Quindi, nel portale di hello, fare clic su **Gestisci manifesto** > **carica manifesto**. È quindi possibile caricare hello modificato manifesto.
8. Fare clic su **Utenti**, selezionare un utente e fare clic su **Assegna**. Assegnare un utente toohello (HpcUsers o HpcAdminMirror) hello ruoli disponibili. Ripetere questo passaggio con altri utenti nella directory hello. Per informazioni generali sugli utenti del cluster, vedere [Gestione di utenti cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > gli utenti toomanage, è consigliabile utilizzare Pannello di anteprima di Azure Active Directory hello hello [portale di Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Passaggio 2: Registrare i client di cluster HPC hello con tenant di Azure AD

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Fare clic su **Active Directory** in hello menu a sinistra e quindi fare clic sulla directory desiderata di hello nella sottoscrizione. È necessario disporre risorse tooaccess autorizzazione nella directory hello.
3. Fare clic su **Applicazioni** > **Aggiungi**, quindi selezionare **Aggiungi un'applicazione che l'organizzazione sta sviluppando**. Immettere le seguenti informazioni nella procedura guidata hello hello:

    * **Nome**: HPCPackClusterClient
    * **Tipo**: selezionare **Applicazione client nativa**
    * **URI di reindirizzamento** - `http://hpcclient`

4. Dopo aver aggiunto l'applicazione hello, fare clic su **configura**. Hello copia **ID Client** valore e salvarlo. poiché servirà in un secondo momento durante la configurazione dell'applicazione.

5. In **autorizzazioni tooother applicazioni**, fare clic su **Aggiungi applicazione**. Cercare e aggiungere un'applicazione hello HpcPackClusterServer (creata nel passaggio 1).

6. In hello **autorizzazioni delegate** elenco a discesa Seleziona **HpcClusterServer accesso**. Fare quindi clic su **Salva**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Passaggio 3: Configurare un cluster HPC hello

1. Connettersi toohello HPC Pack 2016 nodo head in Azure.

2. Avviare HPC PowerShell.

3. Eseguire hello comando seguente:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    dove

    * `AADTenant`Specifica nome del tenant hello Azure AD, ad esempio`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Specifica l'ID client hello per le app hello creata nel passaggio 2.

4. Riavviare il servizio di HpcSchedulerStateful hello.

    In un cluster con più nodi head, è possibile eseguire i seguenti comandi PowerShell hello nodo head tooswitch hello replica primaria per il servizio HpcSchedulerStateful hello hello:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Passaggio 4: Gestire e inviare i processi da client hello

utilità client di HPC Pack tooinstall hello nel computer in uso, scaricare i file di installazione di HPC Pack 2016 (installazione completa) dal Microsoft Download Center hello. Quando si inizia installazione hello, scegliere l'opzione di installazione di hello per hello **utilità client di HPC Pack**.

tooprepare hello client computer, installare il certificato di hello utilizzato durante [l'installazione del cluster HPC](hpcpack-2016-cluster.md) nel computer client hello. Usa Windows standard certificato gestione procedure tooinstall hello certificato pubblico toohello **certificati – utente corrente** > **autorità di certificazione radice attendibili** archiviare. 

È ora possibile eseguire i comandi di HPC Pack hello o utilizzare hello GUI di gestione di processi di HPC Pack toosubmit e gestire i processi di cluster con l'account di hello Azure AD. Per le opzioni invio del processo, vedere [cluster HPC di inviare processi tooan HPC Pack in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Quando si tenta di tooconnect toohello cluster HPC Pack in Azure per hello prima volta, viene visualizzata una finestra popup. Immettere il toolog le credenziali di Azure AD in. token Hello viene quindi memorizzato nella cache. Cluster di toohello le connessioni successive in Azure usare hello memorizzati nella cache di token, a meno che le modifiche di autenticazione o hello memorizzati nella cache viene cancellata.
>
  
Ad esempio, dopo aver completato i passaggi precedenti hello, è possibile eseguire query per i processi da un client locale come indicato di seguito:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Cmdlet utili per l'invio di processi con l'integrazione di Azure AD 

### <a name="manage-hello-local-token-cache"></a>Gestire cache locale del token hello

HPC Pack 2016 fornisce due nuovi cmdlet di PowerShell HPC toomanage hello locale della cache dei token. Questi cmdlet sono utili per inviare processi in modo non interattivo. Vedere hello di esempio seguente:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Impostare le credenziali di hello per l'invio di processi tramite account hello Azure AD 

In alcuni casi, è consigliabile toorun del processo hello nell'utente del cluster HPC hello (per un cluster HPC con dominio, eseguire come utente di un dominio, per un cluster HPC non appartenenti a un dominio, eseguire con un account utente locale nel nodo head hello).

1. Utilizzare hello le credenziali di hello tooset i comandi seguenti:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Quindi inviare il processo di hello come indicato di seguito. Hello processo/attività viene eseguita in $localUser sui nodi di calcolo hello.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Se `–Credential` non è specificato con `Submit-HpcJob`, hello processo o attività viene eseguito con un account utente locale mappato come hello account Azure AD. (cluster HPC hello crea un utente locale con stesso nome come attività di Azure AD account toorun hello hello hello).
    
3. Impostare i dati estesi per hello account Azure AD. Ciò è utile quando si esegue un processo MPI in nodi di Linux utilizzando account hello Azure AD.

   * Impostare i dati estesi per hello account AD Azure stesso

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Impostare i dati estesi ed eseguire come utente del cluster HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

