---
title: domande frequenti sull'integrazione di Log aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="34788-103">Domande frequenti sull'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="34788-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="34788-104">Questo articolo contiene le risponde alle domande frequenti sull'integrazione dei log di Azure.</span><span class="sxs-lookup"><span data-stu-id="34788-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="34788-105">Integrazione di Log di Azure è un servizio di sistema operativo Windows che è possibile utilizzare i registri non elaborato toointegrate dalle risorse di Azure in locale sicurezza informazioni ed eventi (SIEM) sistemi di gestione dei.</span><span class="sxs-lookup"><span data-stu-id="34788-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="34788-106">Questa integrazione fornisce un dashboard unificato per tutte le attività, locale o nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="34788-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="34788-107">È possibile aggregare, correlare, analizzare e inviare avvisi per gli eventi di sicurezza associati alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="34788-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="34788-108">È disponibile il software di integrazione di Log di Azure hello?</span><span class="sxs-lookup"><span data-stu-id="34788-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="34788-109">Sì.</span><span class="sxs-lookup"><span data-stu-id="34788-109">Yes.</span></span> <span data-ttu-id="34788-110">Non è previsto alcun addebito per hello software di integrazione di Log di Azure.</span><span class="sxs-lookup"><span data-stu-id="34788-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="34788-111">Dove è disponibile l'integrazione dei log di Azure?</span><span class="sxs-lookup"><span data-stu-id="34788-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="34788-112">Attualmente è disponibile nell'area commerciale di Azure e in Azure per enti pubblici e non è disponibile in Cina né in Germania.</span><span class="sxs-lookup"><span data-stu-id="34788-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="34788-113">Come è possibile visualizzare gli account di archiviazione hello da cui integrazione di Log di Azure effettua il pull di registri di macchina virtuale di Azure?</span><span class="sxs-lookup"><span data-stu-id="34788-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="34788-114">Eseguire il comando hello **elenco origine azlog**.</span><span class="sxs-lookup"><span data-stu-id="34788-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="34788-115">Come individuare quale hello sottoscrizione Azure Integration Log i registri sono da</span><span class="sxs-lookup"><span data-stu-id="34788-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="34788-116">In caso di hello dei registri di controllo che vengono inseriti in hello **AzureResourcemanagerJson** directory, l'ID sottoscrizione hello è nel nome del file di log hello.</span><span class="sxs-lookup"><span data-stu-id="34788-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="34788-117">Ciò vale anche per i log di hello **AzureSecurityCenterJson** cartella.</span><span class="sxs-lookup"><span data-stu-id="34788-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="34788-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="34788-118">For example:</span></span>

<span data-ttu-id="34788-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="34788-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="34788-120">Registri di controllo di Azure Active Directory includono l'ID tenant hello come parte del nome hello.</span><span class="sxs-lookup"><span data-stu-id="34788-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="34788-121">ID sottoscrizione hello come parte del nome di hello non includono i log di diagnostica che vengono letti da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="34788-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="34788-122">Includono invece soprannome hello specificato come parte della creazione di hello di origine di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="34788-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="34788-123">Come è possibile aggiornare la configurazione del proxy hello?</span><span class="sxs-lookup"><span data-stu-id="34788-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="34788-124">Se l'impostazione proxy non consente l'accesso di archiviazione di Azure direttamente, aprire hello **AZLOG. FILE EXE. CONFIGURAZIONE** file **c:\Program Files\Microsoft Azure Log integrazione**.</span><span class="sxs-lookup"><span data-stu-id="34788-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="34788-125">Hello tooinclude file di aggiornamento hello **defaultProxy** sezione con l'indirizzo del proxy hello dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="34788-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="34788-126">Al termine dell'aggiornamento di hello, arrestare e avviare il servizio hello tramite comandi hello **net stop azlog** e **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="34788-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="34788-127">È possibile vedere informazioni sulla sottoscrizione hello negli eventi di Windows?</span><span class="sxs-lookup"><span data-stu-id="34788-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="34788-128">Aggiungere nome descrittivo toohello ID sottoscrizione hello durante l'aggiunta di origine hello:</span><span class="sxs-lookup"><span data-stu-id="34788-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="34788-129">evento Hello XML ha hello metadati, inclusi ID sottoscrizione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="34788-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![XML dell'evento][1]

## <a name="error-messages"></a><span data-ttu-id="34788-131">messaggi di errore</span><span class="sxs-lookup"><span data-stu-id="34788-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="34788-132">Quando si esegue il comando hello **azlog createazureid**, perché viene visualizzato il seguente errore hello?</span><span class="sxs-lookup"><span data-stu-id="34788-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="34788-133">Error:</span><span class="sxs-lookup"><span data-stu-id="34788-133">Error:</span></span>

  <span data-ttu-id="34788-134">*Non è stato possibile toocreate applicazione AAD - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Non consentito', messaggio = 'dispone di privilegi sufficienti operazione hello toocomplete'.*</span><span class="sxs-lookup"><span data-stu-id="34788-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="34788-135">Hello **azlog createazureid** comando tenta di un'entità servizio in tutti i tenant di Azure AD hello per le sottoscrizioni hello hello accesso di Azure ha accesso a toocreate.</span><span class="sxs-lookup"><span data-stu-id="34788-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="34788-136">Se l'account di accesso di Azure è solo un utente guest nel tenant di Azure AD, il comando di hello non riesce con "operazione di hello toocomplete di privilegi sufficienti."</span><span class="sxs-lookup"><span data-stu-id="34788-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="34788-137">Chiedere tenant hello tooadd amministratore account come utente nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="34788-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="34788-138">Quando si esegue il comando hello **azlog autorizzare**, perché viene visualizzato il seguente errore hello?</span><span class="sxs-lookup"><span data-stu-id="34788-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="34788-139">Error:</span><span class="sxs-lookup"><span data-stu-id="34788-139">Error:</span></span>

  <span data-ttu-id="34788-140">*Avviso di creazione di assegnazione di ruolo - AuthorizationFailed: client hello janedo@microsoft.com' con l'oggetto 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' id non è stata autorizzazione tooperform azione 'Microsoft.Authorization/roleAssignments/write' sull'ambito ' / le sottoscrizioni / 70d 95299-d689-4c 97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="34788-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="34788-141">Hello **azlog autorizzare** comando Assegna hello ruolo dell'entità servizio di Azure AD toohello lettore (creata con **azlog createazureid**) sottoscrizioni toohello fornito.</span><span class="sxs-lookup"><span data-stu-id="34788-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="34788-142">Se hello accesso di Azure non è un CO-amministratore o un proprietario della sottoscrizione di hello, operazione non riesce con un messaggio di errore "Autorizzazione non riuscita".</span><span class="sxs-lookup"><span data-stu-id="34788-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="34788-143">Azure Role-Based Access controllo (RBAC) di CO-amministratore o il proprietario è necessario toocomplete questa azione.</span><span class="sxs-lookup"><span data-stu-id="34788-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="34788-144">Dove trovare definizione hello delle proprietà di hello nel log di controllo hello?</span><span class="sxs-lookup"><span data-stu-id="34788-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="34788-145">Vedere:</span><span class="sxs-lookup"><span data-stu-id="34788-145">See:</span></span>

* [<span data-ttu-id="34788-146">Operazioni di controllo con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="34788-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="34788-147">Elenco eventi di gestione di hello in una sottoscrizione in hello API REST di monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="34788-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="34788-148">Dove sono disponibili altre informazioni sugli avvisi del Centro sicurezza di Azure?</span><span class="sxs-lookup"><span data-stu-id="34788-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="34788-149">Vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="34788-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="34788-150">Come è possibile scegliere quali informazioni raccogliere con la diagnostica delle VM?</span><span class="sxs-lookup"><span data-stu-id="34788-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="34788-151">Per ulteriori informazioni su come tooget, modificare e impostare la configurazione di diagnostica Azure hello, vedere [tooenable PowerShell utilizzare diagnostica Azure in una macchina virtuale che esegue Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34788-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="34788-152">Hello seguente esempio ottiene una configurazione di diagnostica di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="34788-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="34788-153">Hello di esempio seguente modifica una configurazione di diagnostica Azure hello.</span><span class="sxs-lookup"><span data-stu-id="34788-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="34788-154">In questa configurazione, solo l'evento ID 4624 e l'evento ID 4625 vengono raccolti dal registro eventi di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="34788-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="34788-155">Microsoft Antimalware per gli eventi di Azure vengono raccolti dal registro eventi di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="34788-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="34788-156">Per informazioni dettagliate sull'utilizzo di hello delle espressioni XPath, vedere [utilizzo degli eventi](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="34788-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="34788-157">Hello esempio seguente imposta la configurazione di diagnostica Azure hello:</span><span class="sxs-lookup"><span data-stu-id="34788-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="34788-158">Dopo aver apportato modifiche, controllare tooensure account di archiviazione hello che hello corretto gli eventi vengono raccolti.</span><span class="sxs-lookup"><span data-stu-id="34788-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="34788-159">Se si dispone di eventuali problemi durante l'installazione di hello e configurazione, aprire un [richiesta di supporto](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="34788-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="34788-160">Selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.</span><span class="sxs-lookup"><span data-stu-id="34788-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="34788-161">È possibile utilizzare i log di integrazione di Azure Log toointegrate Watcher di rete in my SIEM?</span><span class="sxs-lookup"><span data-stu-id="34788-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="34788-162">Azure Network Watcher genera grandi quantità di informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="34788-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="34788-163">Questi log non sono adatti toobe inviati tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="34788-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="34788-164">destinazione Hello è supportato solo per i log di controllo di rete è un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="34788-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="34788-165">Integrazione di Log di Azure non supporta la lettura di questi registri e rendendoli disponibile tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="34788-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
