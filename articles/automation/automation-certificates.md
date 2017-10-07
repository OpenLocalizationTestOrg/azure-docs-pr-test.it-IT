---
title: Asset aaaCertificate in automazione di Azure | Documenti Microsoft
description: I certificati possono essere archiviati in modo sicuro in automazione di Azure in modo da renderli accessibili dal runbook o tooauthenticate configurazioni DSC da Azure e risorse di terze parti.  In questo articolo vengono illustrati i dettagli di hello dei certificati e come toowork con essi in creazione grafica e testuale.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="e7a39-104">Asset di tipo certificato in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e7a39-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="e7a39-105">I certificati possono essere archiviati in modo sicuro in automazione di Azure in modo da renderli accessibili dal runbook o delle configurazioni DSC tramite hello **Get AzureRmAutomationRmCertificate** attività per le risorse di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a39-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="e7a39-106">Questo consente toocreate runbook e le configurazioni DSC che utilizzano i certificati per l'autenticazione o li aggiunge risorse tooAzure o di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e7a39-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="e7a39-107">Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate.</span><span class="sxs-lookup"><span data-stu-id="e7a39-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="e7a39-108">Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="e7a39-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="e7a39-109">La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a39-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="e7a39-110">Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="e7a39-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="e7a39-111">Cmdlet di Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a39-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="e7a39-112">cmdlet Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire asset certificato di automazione con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a39-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="e7a39-113">Vengono forniti come parte di hello [modulo Azure PowerShell](../powershell-install-configure.md) disponibile per l'uso nei runbook di automazione e le configurazioni DSC.</span><span class="sxs-lookup"><span data-stu-id="e7a39-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="e7a39-114">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e7a39-114">Cmdlets</span></span>|<span data-ttu-id="e7a39-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7a39-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="e7a39-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e7a39-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="e7a39-117">Recupera informazioni su toouse un certificato in un runbook o di una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e7a39-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="e7a39-118">È possibile recuperare solo il certificato hello stesso dall'attività Get-Automationcredential.</span><span class="sxs-lookup"><span data-stu-id="e7a39-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="e7a39-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e7a39-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="e7a39-120">Crea un nuovo certificato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a39-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="e7a39-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e7a39-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="e7a39-122">Rimuove un certificato da Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a39-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="e7a39-123">Crea un nuovo certificato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a39-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="e7a39-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="e7a39-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="e7a39-125">Imposta le proprietà di hello per un certificato esistente, incluso il caricamento di file di certificato hello e impostazione password hello per un file pfx.</span><span class="sxs-lookup"><span data-stu-id="e7a39-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="e7a39-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="e7a39-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="e7a39-127">Caricamento di un servizio del certificato per hello specificato servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e7a39-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="e7a39-128">Creazione di un nuovo certificato</span><span class="sxs-lookup"><span data-stu-id="e7a39-128">Creating a new certificate</span></span>

<span data-ttu-id="e7a39-129">Quando si crea un nuovo certificato, caricare un tooAzure file con estensione cer o pfx automazione.</span><span class="sxs-lookup"><span data-stu-id="e7a39-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="e7a39-130">Se si contrassegna certificato hello come esportabile, è possibile trasferirla dall'archivio certificati di automazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e7a39-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="e7a39-131">Se non è esportabile, quindi può solo essere utilizzato per la firma all'interno di runbook hello o configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="e7a39-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="e7a39-132">toocreate un nuovo certificato con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e7a39-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="e7a39-133">Scegliere l'account di automazione, hello **asset** riquadro tooopen hello **asset** blade.</span><span class="sxs-lookup"><span data-stu-id="e7a39-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="e7a39-134">Fare clic su hello **certificati** riquadro tooopen hello **certificati** blade.</span><span class="sxs-lookup"><span data-stu-id="e7a39-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="e7a39-135">Fare clic su **aggiungere un certificato** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="e7a39-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="e7a39-136">Digitare un nome per il certificato di hello hello **nome** casella.</span><span class="sxs-lookup"><span data-stu-id="e7a39-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="e7a39-137">Fare clic su **selezionare un file** in **caricare un file di certificato** toobrowse per un file con estensione cer o pfx.</span><span class="sxs-lookup"><span data-stu-id="e7a39-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="e7a39-138">Se si seleziona un file con estensione pfx, specificare una password e se che dovrebbe essere consentito toobe esportato.</span><span class="sxs-lookup"><span data-stu-id="e7a39-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="e7a39-139">Fare clic su **crea** toosave hello nuovo certificato asset.</span><span class="sxs-lookup"><span data-stu-id="e7a39-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="e7a39-140">toocreate un nuovo certificato con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a39-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="e7a39-141">Hello esempio seguente viene illustrato come toocreate automazione un nuovo certificato e contrassegnarlo come esportabile.</span><span class="sxs-lookup"><span data-stu-id="e7a39-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="e7a39-142">Verrà importato un file con estensione pfx esistente.</span><span class="sxs-lookup"><span data-stu-id="e7a39-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="e7a39-143">Utilizzo di un certificato</span><span class="sxs-lookup"><span data-stu-id="e7a39-143">Using a certificate</span></span>

<span data-ttu-id="e7a39-144">È necessario utilizzare hello **Get-Automationcredential** attività toouse un certificato.</span><span class="sxs-lookup"><span data-stu-id="e7a39-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="e7a39-145">Non è possibile utilizzare hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet perché restituisce informazioni su asset del certificato di hello ma non certificato hello stesso.</span><span class="sxs-lookup"><span data-stu-id="e7a39-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="e7a39-146">Esempio di Runbook testuale</span><span class="sxs-lookup"><span data-stu-id="e7a39-146">Textual runbook sample</span></span>

<span data-ttu-id="e7a39-147">Hello seguente codice di esempio mostra come del cloud tooadd tooa un certificato di servizio in un runbook.</span><span class="sxs-lookup"><span data-stu-id="e7a39-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="e7a39-148">In questo esempio, la password di hello viene recuperata dalla variabile di automazione crittografata.</span><span class="sxs-lookup"><span data-stu-id="e7a39-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="e7a39-149">Esempio di Runbook grafico</span><span class="sxs-lookup"><span data-stu-id="e7a39-149">Graphical runbook sample</span></span>

<span data-ttu-id="e7a39-150">Si aggiunge un **Get-Automationcredential** tooa runbook grafico facendo clic sul certificato hello nel riquadro libreria hello dell'editor grafico hello e selezionando **aggiungere toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="e7a39-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Aggiungere l'area di disegno toohello certificato](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="e7a39-152">Hello immagine seguente mostra un esempio di utilizzo di un certificato in un runbook grafico.</span><span class="sxs-lookup"><span data-stu-id="e7a39-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="e7a39-153">Si tratta di hello stesso esempio illustrato in precedenza per l'aggiunta di un servizio cloud tooa di certificato da un runbook testuale.</span><span class="sxs-lookup"><span data-stu-id="e7a39-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="e7a39-154">Esempio di creazione grafica</span><span class="sxs-lookup"><span data-stu-id="e7a39-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="e7a39-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7a39-155">Next steps</span></span>

- <span data-ttu-id="e7a39-156">informazioni sull'utilizzo di collegamenti toocontrol hello un flusso logico delle attività del runbook è toolearn progettato tooperform, vedere [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="e7a39-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
