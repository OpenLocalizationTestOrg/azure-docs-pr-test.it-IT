---
title: aaaInstall e configurare le macchine virtuali tooprovision Terraform e altre infrastrutture in Azure | Documenti Microsoft
description: Informazioni su come tooinstall e Terraform toocreate Azure di configurare le risorse
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Installare e configurare le macchine virtuali tooprovision Terraform e altre infrastrutture in Azure 
Questo articolo descrive tooinstall necessarie hello e configurare le risorse di tooprovision Terraform quali macchine virtuali in Azure. Si apprenderà come toocreate e utilizzare Azure credenziali tooenable Terraform tooprovision risorse del cloud in modo sicuro.

HashiCorp Terraform fornisce un modo semplice di toodefine e distribuire un'infrastruttura cloud utilizzando un linguaggio di modelli personalizzati denominato HashiCorp linguaggio di configurazione (elenco). Questa lingua personalizzata è [toowrite semplice e facile toounderstand](terraform-create-complete-vm.md). Inoltre, tramite hello `terraform plan` comando, è possibile visualizzare l'infrastruttura di hello modifiche tooyour prima del commit. Seguire questi toostart passaggi utilizzando Terraform con Azure.

## <a name="install-terraform"></a>Installazione di Terraform
tooinstall Terraform, [scaricare](https://www.terraform.io/downloads.html) pacchetto hello appropriato per il sistema operativo in una directory di installazione separato. download di Hello contiene un singolo file eseguibile per il quale è inoltre necessario definire un percorso globale. Per istruzioni su come tooset hello percorso su Linux e Mac, visitare troppo[questa pagina Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Per istruzioni su come tooset hello percorso in Windows, visitare troppo[questa pagina Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify l'installazione, eseguire hello `terraform` comando. Si dovrebbe vedere un elenco di opzioni Terraform disponibili come output.

Successivamente, è necessario tooallow Terraform accesso tooyour sottoscrizione di Azure tooperform il provisioning dell'infrastruttura.

## <a name="set-up-terraform-access-tooazure"></a>Impostare Terraform accesso tooAzure
tooenable Terraform tooprovision risorse in Azure, è necessario toocreate due entità in Azure Active Directory (Azure AD): un'applicazione Azure AD e un'entità servizio di Azure AD. Gli identificatori di queste entità verranno usati negli script Terraform. L'entità servizio è un'istanza locale di un'applicazione Azure AD globale. Un'entità servizio consente risorse tooglobal del controllo di accesso locale granulare.

Esistono diversi modi toocreate un'applicazione Azure AD e un'entità servizio di Azure AD. Hello rapido e semplice è modo oggi toouse CLI di Azure 2.0, che [è possibile scaricare e installare su Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). È inoltre possibile utilizzare infrastruttura di sicurezza necessarie hello toocreate PowerShell o Azure CLI 1.0. Hello istruzioni che seguono viene illustrato come tooconfigure Terraform per Azure tramite tutti questi approcci.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Usare l'interfaccia della riga di comando di Azure 2.0 (per gli utenti di Windows, Linux o Mac) 
Dopo aver scaricato e installato hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), accedi tooadminister la sottoscrizione di Azure mediante l'emissione di hello comando seguente:

```
az login
```

>[!NOTE]
>Se si utilizza hello Cina, Azure in Germania o cloud di Azure per enti pubblici, è necessario toofirst configurare hello Azure CLI toowork con il cloud. È possibile farlo eseguendo hello:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Se si dispone di più sottoscrizioni di Azure, i relativi dettagli vengono restituiti da hello `az login` comando. Set hello `SUBSCRIPTION_ID` ambiente toohold variabile hello hello restituito `id` campo sottoscrizione hello desiderato toouse. 

Impostare una sottoscrizione di hello che si desidera toouse per questa sessione.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

ID sottoscrizione di hello account tooget hello di query e i valori di ID del tenant.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Successivamente, creare credenziali separate per Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

Vengono restituiti appId, password, sp_name e tenant. Prendere nota dell'ID applicazione hello e una password.

tooconfirm le credenziali (entità servizio), aprire una nuova shell ed eseguire hello i comandi seguenti. Hello Substitute restituito valori per sp_name, password e tenant:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Uso di PowerShell (per gli utenti di Windows) 
toouse Windows toowrite del computer ed eseguire il Terraform toouse PowerShell per attività di configurazione e script di configurazione del computer con gli strumenti di PowerShell destra hello. 

1. Installare gli strumenti di PowerShell alla procedura seguente hello in [installare e configurare Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Scaricare ed eseguire hello [script azure setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) dalla console di PowerShell hello.

3. script di azure setup.ps1 toorun hello, scaricarla ed eseguire hello `./azure-setup.ps1 setup` comando dalla console di PowerShell hello. Accedere quindi tooyour sottoscrizione di Azure con privilegi amministrativi.

4. Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto. Facoltativamente, scegliere una password complessa quando viene richiesto. Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Usare l'interfaccia della riga di comando di Azure 1.0 (per gli utenti Linux o Mac)
tooget avviato con Terraform nel computer Linux o Mac con Azure CLI 1.0, librerie di installazione hello appropriate nel computer.  

1. Installare gli strumenti CLI di Azure xPlat seguendo procedure hello [installare Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Scaricare e installare un processore JSON seguendo le istruzioni hello [scaricare jq](https://stedolan.github.io/jq/download/).

3. Scaricare ed eseguire hello [script azure setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script dalla console hello.

4. script di azure setup.sh toorun hello, scaricarla ed eseguire hello `./azure-setup setup` comando dalla console hello. Accedere quindi tooyour sottoscrizione di Azure con privilegi amministrativi.
 
5. Specificare un nome di applicazione (stringa arbitraria, richiesto) quando richiesto. Facoltativamente, scegliere una password complessa quando viene richiesto. Se non si fornisce la password, viene automaticamente generata una password complessa mediante le librerie di sicurezza .NET.

Tutti gli script precedenti di hello creano un'applicazione Azure AD e il servizio principale. entità servizio Hello Ottiene un collaboratore o l'accesso a livello di proprietario della sottoscrizione hello. A causa di hello elevato livello di accesso, è consigliabile proteggere sempre le informazioni di sicurezza hello generate da tali script. Prendere nota di tutte e quattro le informazioni di sicurezza fornite da tali script: appId, password, subscription_id e tenant_id.

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente
Dopo aver creato e configurare un'entità servizio di Azure AD, è necessario toolet Terraform conoscere hello tenant ID, ID sottoscrizione, ID client e client secret toouse. A tale scopo, incorporare tali valori negli script Terraform, come descritto in [Creare un'infrastruttura di base usando Terraform](terraform-create-complete-vm.md). In alternativa, è possibile impostare hello seguenti variabili di ambiente (e pertanto evitare di archiviare accidentalmente o condividere le proprie credenziali):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

È possibile utilizzare questo tooset script della shell di esempio di tali variabili:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Inoltre, se si utilizza Terraform con Azure in Cina o di Azure per enti pubblici o di Azure in Germania, è necessario variabile di ambiente tooset hello in modo appropriato.

## <a name="next-steps"></a>Passaggi successivi
Abbiamo installato Terraform e configurato le credenziali di Azure per avviare la distribuzione dell'infrastruttura nella sottoscrizione di Azure. Per ulteriori informazioni come troppo[creare infrastruttura con Terraform](terraform-create-complete-vm.md).
