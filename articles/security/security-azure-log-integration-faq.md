---
title: Domande frequenti sull'integrazione dei log di Azure | Microsoft Docs
description: Questo articolo contiene le risponde alle domande sull'integrazione dei log di Azure.
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="4d1b2-103">Domande frequenti sull'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="4d1b2-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="4d1b2-104">Questo articolo contiene le risponde alle domande frequenti sull'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="4d1b2-105">L'integrazione dei log di Azure è un servizio del sistema operativo Windows che consente di integrare log non elaborati delle risorse di Azure nei sistemi di gestione di informazioni ed eventi di sicurezza (SIEM) locali.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="4d1b2-106">Questa integrazione fornisce un dashboard unificato per tutti gli asset locali o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="4d1b2-107">È possibile aggregare, correlare, analizzare e inviare avvisi per gli eventi di sicurezza associati alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="4d1b2-108">Il software di integrazione dei log di Azure è gratuito?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="4d1b2-109">Sì.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-109">Yes.</span></span> <span data-ttu-id="4d1b2-110">Non è previsto alcun addebito per il software di integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="4d1b2-111">Dove è disponibile l'integrazione dei log di Azure?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="4d1b2-112">Attualmente è disponibile nell'area commerciale di Azure e in Azure per enti pubblici e non è disponibile in Cina né in Germania.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="4d1b2-113">Come è possibile individuare gli account di archiviazione da cui il servizio di integrazione dei log di Azure estrae i log delle VM di Azure?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="4d1b2-114">Eseguire il comando **azlog source list**.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="4d1b2-115">Come è possibile stabilire da quale sottoscrizione provengono i log di integrazione dei log di Azure?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="4d1b2-116">Nel caso dei log di controllo presenti nella directory **AzureResourcemanagerJson**, l'ID della sottoscrizione è il nome del file di log.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="4d1b2-117">Questo vale anche per i log nella cartella **AzureSecurityCenterJson**.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="4d1b2-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-118">For example:</span></span>

<span data-ttu-id="4d1b2-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="4d1b2-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="4d1b2-120">I log di controllo di Azure Active Directory includono l'ID tenant come parte del nome.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="4d1b2-121">I log di diagnostica che vengono letti da un hub eventi non includono l'ID di sottoscrizione come parte del nome.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="4d1b2-122">Includono invece il nome descrittivo specificato nell'ambito della creazione dell'origine dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="4d1b2-123">Come è possibile aggiornare la configurazione del proxy?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="4d1b2-124">Se la configurazione del proxy non consente l'accesso di archiviazione di Azure direttamente, aprire il file **AZLOG.EXE.CONFIG** in **c:\Programmi\Integrazione dei log di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="4d1b2-125">Aggiornare il file in modo che includa la sezione **defaultProxy** con l'indirizzo del proxy dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="4d1b2-126">Al termine dell'aggiornamento, arrestare e avviare il servizio usando i comandi **net stop azlog** e **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="4d1b2-127">Come è possibile vedere le informazioni sulla sottoscrizione negli eventi di Windows?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="4d1b2-128">Aggiungere l'ID sottoscrizione al nome descrittivo quando si aggiunge l'origine:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="4d1b2-129">L'XML dell'evento include i metadati seguenti, compreso l'ID sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-129">The event XML has the following metadata, including the subscription ID:</span></span>

![XML dell'evento][1]

## <a name="error-messages"></a><span data-ttu-id="4d1b2-131">messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="4d1b2-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="4d1b2-132">Durante l'esecuzione del comando **azlog createazureid**, perché viene visualizzato il seguente errore?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="4d1b2-133">Error:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-133">Error:</span></span>

  <span data-ttu-id="4d1b2-134">*Impossibile creare l'applicazione AAD - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Motivo = "Accesso negato" - Messaggio = "Privilegi insufficienti per completare l'operazione".*</span><span class="sxs-lookup"><span data-stu-id="4d1b2-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="4d1b2-135">Il comando **azlog createazureid** tenta di creare un'entità servizio in tutti i tenant di Azure AD per le sottoscrizioni a cui l'account di accesso di Azure può accedere.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="4d1b2-136">Se l'account di accesso di Azure è solo un utente guest nel tenant di Azure AD, il comando non riesce e mostra l'errore "I privilegi non sono insufficienti per completare l'operazione".</span><span class="sxs-lookup"><span data-stu-id="4d1b2-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="4d1b2-137">Richiedere all'amministratore del tenant di aggiungere l'account come utente nel tenant.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="4d1b2-138">Durante l'esecuzione del comando **azlog authorize**, perché viene visualizzato il seguente errore?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="4d1b2-139">Error:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-139">Error:</span></span>

  <span data-ttu-id="4d1b2-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.* (Avviso durante la creazione dell'assegnazione del ruolo - Autorizzazione non riuscita: il client " con ID oggetto "fe9e03e4-4dad-4328-910f-fd24a9660bd2' non dispone di autorizzazione per eseguire l'azione 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000").</span><span class="sxs-lookup"><span data-stu-id="4d1b2-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="4d1b2-141">Il comando **azlog authorize** assegna il ruolo di Lettore all'entità servizio di Azure AD (creata con **azlog createazureid**) per le sottoscrizioni fornite.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="4d1b2-142">Se l'account di accesso di Azure non è un coamministratore o un proprietario della sottoscrizione, l'operazione ha esito negativo con il messaggio di errore "Autorizzazione non riuscita".</span><span class="sxs-lookup"><span data-stu-id="4d1b2-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="4d1b2-143">Per completare l'azione è necessario il controllo degli accessi in base al ruolo di coamministratore o proprietario.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="4d1b2-144">Dove si trova la definizione delle proprietà nel log di controllo?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="4d1b2-145">Vedere:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-145">See:</span></span>

* [<span data-ttu-id="4d1b2-146">Operazioni di controllo con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4d1b2-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="4d1b2-147">Elencare gli eventi di gestione in una sottoscrizione nell'API REST di Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="4d1b2-147">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="4d1b2-148">Dove sono disponibili altre informazioni sugli avvisi del Centro sicurezza di Azure?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="4d1b2-149">Vedere [Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4d1b2-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="4d1b2-150">Come è possibile scegliere quali informazioni raccogliere con la diagnostica delle VM?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="4d1b2-151">Per informazioni dettagliate su come ottenere, modificare e impostare la configurazione di Diagnostica di Azure vedere [Usare PowerShell per abilitare la Diagnostica di Azure in una macchina virtuale che esegue Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d1b2-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="4d1b2-152">L'esempio seguente ottiene la configurazione di Diagnostica di Azure:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="4d1b2-153">L'esempio seguente modifica la configurazione di Diagnostica di Azure:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="4d1b2-154">In questa configurazione, solo l'evento ID 4624 e l'evento ID 4625 vengono raccolti dal log eventi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="4d1b2-155">Gli eventi Microsoft Antimalware per Azure vengono raccolti dal registro eventi di sistema.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="4d1b2-156">Per informazioni dettagliate sull'uso di espressioni XPath, vedere [Utilizzo degli eventi](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="4d1b2-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="4d1b2-157">L'esempio seguente imposta la configurazione di Diagnostica di Azure:</span><span class="sxs-lookup"><span data-stu-id="4d1b2-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="4d1b2-158">Dopo aver apportato modifiche, verificare l'account di archiviazione per assicurarsi che vengano raccolti gli eventi corretti.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="4d1b2-159">Se si verificano problemi durante l'installazione e la configurazione, aprire una [richiesta di supporto](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="4d1b2-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="4d1b2-160">Selezionare **Integrazione log** come servizio per cui richiedere il supporto.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="4d1b2-161">È possibile usare l'integrazione dei log di Azure per integrare i log di Network Watcher nel sistema SIEM personale?</span><span class="sxs-lookup"><span data-stu-id="4d1b2-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="4d1b2-162">Azure Network Watcher genera grandi quantità di informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="4d1b2-163">Questi log non sono concepiti per essere inviati a un sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="4d1b2-164">L'unica destinazione supportata per i log di controllo di rete è un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="4d1b2-165">L'integrazione dei log di Azure non supporta la lettura di questi log e la relativa disponibilità in un sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="4d1b2-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
