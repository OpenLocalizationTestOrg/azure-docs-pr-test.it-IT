---
title: insieme di credenziali di chiave con SQL Server in macchine virtuali di Windows in Azure (versione classica) aaaIntegrate | Documenti Microsoft
description: Informazioni su come tooautomate hello configurazione di crittografia di SQL Server per l'utilizzo con l'insieme di credenziali chiave di Azure. Questo argomento viene illustrato come creare di toouse integrazione dell'insieme di credenziali chiave di Azure con le macchine virtuali di SQL Server nel modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (distribuzione classica)
> [!div class="op_single_selector"]
> * [Gestione risorse](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Classico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Panoramica
Esistono più funzionalità di crittografia di SQL Server, ad esempio [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [crittografia a livello di colonna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) e [crittografia di backup](https://msdn.microsoft.com/library/dn449489.aspx). I moduli di crittografia occorre toomanage e archiviano le chiavi di crittografia hello che è utilizzare per la crittografia. Hello servizio insieme di credenziali chiave di Azure (insieme) è progettata tooimprove hello sicurezza e la gestione di queste chiavi in una posizione sicura e altamente disponibile. Hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) consente di SQL Server toouse queste chiavi dall'insieme di credenziali chiave di Azure.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Se si esegue SQL Server con il computer locale, esistono [è possibile attenersi alla procedura tooaccess insieme credenziali chiavi Azure dal computer di SQL Server on-premise](https://msdn.microsoft.com/library/dn198405.aspx). Ma per SQL Server in macchine virtuali di Azure, è possibile risparmiare tempo utilizzando hello *integrazione dell'insieme di credenziali chiave di Azure* funzionalità. Con alcuni tooenable i cmdlet di Azure PowerShell è possibile automatizzare questa funzionalità, hello credenziali delle chiavi di configurazione necessarie per tooaccess una VM SQL.

Quando questa funzionalità è abilitata, automaticamente installa hello connettore SQL Server, configura hello EKM provider tooaccess insieme credenziali chiavi Azure e crea hello credenziali tooallow si tooaccess l'insieme di credenziali. Se è stato esaminato passaggi hello hello indicato in precedenza documentazione locale, è possibile vedere che questa funzionalità consente di automatizzare i passaggi 2 e 3. Hello è comunque necessario toodo manualmente è chiavi e l'insieme di credenziali chiave hello toocreate. Da qui, hello intero il programma di installazione della VM SQL è automatizzato. Quando questa funzionalità viene completato il programma di installazione, è possibile eseguire toobegin istruzioni T-SQL la crittografia del database o backup in modo analogo.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configurare l'integrazione di AKV
Utilizzare PowerShell tooconfigure integrazione dell'insieme di credenziali chiave di Azure. Hello le sezioni seguenti fornisce una panoramica dei parametri di hello necessarie e quindi un esempio di script di PowerShell.

### <a name="install-hello-sql-server-iaas-extension"></a>Installare l'estensione di SQL Server IaaS hello
Prima di tutto, [installare estensione di SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Comprendere i parametri di input hello
Hello seguente tabella elenca hello parametri necessari script di PowerShell toorun hello nella sezione successiva hello.

| . | Descrizione | Esempio |
| --- | --- | --- |
| **$akvURL** |**URL dell'insieme di credenziali chiave Hello** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Nome entità servizio** |"fde2b411-33d5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Segreto entità servizio** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=" |
| **$credName** |**Nome delle credenziali**: integrazione AKV crea una credenziale all'interno di SQL Server, consentendo di hello VM toohave accesso toohello chiave dell'insieme di credenziali. Scegliere un nome per la credenziale. |"mycred1" |
| **$vmName** |**Nome della macchina virtuale**: nome hello di una VM SQL creato in precedenza. |"myvmname" |
| **$serviceName** |**Nome del servizio**: nome del servizio Cloud hello associato hello SQL VM. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>Abilitare l'integrazione di AKV con PowerShell
Hello **New AzureVMSqlServerKeyVaultCredentialConfig** cmdlet crea un oggetto di configurazione per la funzionalità di integrazione dell'insieme di credenziali chiave di Azure hello. Hello **Set AzureVMSqlServerExtension** consente di configurare l'integrazione con hello **KeyVaultCredentialSettings** parametro. Hello seguente procedura mostra come toouse questi comandi.

1. In Azure PowerShell, configurare i parametri di input hello con i valori specifici come descritto nelle sezioni precedenti di hello di questo argomento. Hello lo script seguente è riportato un esempio.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Quindi seguito hello utilizzare script tooconfigure e abilita l'integrazione di insieme.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Hello estensione SQL IaaS Agent aggiornerà hello VM SQL con questa nuova configurazione.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

