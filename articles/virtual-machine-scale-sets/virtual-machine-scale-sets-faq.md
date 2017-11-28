---
title: "scalabilità della macchina virtuale aaaAzure imposta domande frequenti | Documenti Microsoft"
description: "Ottenere risposte toofrequently domande frequenti su set di scalabilità di macchine virtuali."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="bbbe2-103">Domande frequenti sui set di scalabilità di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="bbbe2-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="bbbe2-104">Ottenere risposte imposta toofrequently domande frequenti sulla scalabilità della macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="bbbe2-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="bbbe2-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="bbbe2-106">Quali sono le procedure consigliate per la scalabilità automatica di Azure?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="bbbe2-107">Per informazioni sulle procedure consigliate per la scalabilità automatica, vedere [Procedure consigliate per la scalabilità automatica delle macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="bbbe2-108">Dove è possibile trovare i nomi delle metriche per la scalabilità automatica che usa metriche basate su host?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="bbbe2-109">Per informazioni sui nomi delle metriche per la scalabilità automatica che usa metriche basate su host, vedere [Metriche supportate con Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="bbbe2-110">Sono disponibili eventuali esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="bbbe2-111">Sì.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-111">Yes.</span></span> <span data-ttu-id="bbbe2-112">Per esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="bbbe2-113">Per una coda del Bus di servizio, utilizzare hello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="bbbe2-114">Per una coda di archiviazione, usare hello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="bbbe2-115">Sostituire i valori dell'esempio con gli URI (Uniform Resource Identifier) della risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="bbbe2-116">È consigliabile applicare la scalabilità automatica usando metriche basate su host oppure un'estensione di diagnostica?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="bbbe2-117">È possibile creare un'impostazione di scalabilità automatica su una delle metriche a livello di host di macchina virtuale toouse metriche di base del sistema operativo guest.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="bbbe2-118">Per un elenco delle metriche supportate, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="bbbe2-119">Per un esempio completo per i set di scalabilità di macchine virtuali, vedere [Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="bbbe2-120">esempio Hello utilizza metrica di CPU a livello di host hello e una metrica conteggio dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-121">Come si impostano le regole di avviso in un set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-122">È possibile creare avvisi sulle metriche per i set di scalabilità di macchine virtuali tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="bbbe2-123">Per altre informazioni, vedere [Esempi di avvio rapido con PowerShell per Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) ed [Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="bbbe2-124">ID risorsa di destinazione del set di scalabilità della macchina virtuale hello Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="bbbe2-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="bbbe2-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="bbbe2-126">È possibile scegliere qualsiasi contatore di prestazioni della macchina virtuale come tooset metrica hello un avviso per.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="bbbe2-127">Per ulteriori informazioni, vedere [le metriche del sistema operativo Guest per macchine virtuali basate su Gestione risorse di Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [le metriche del sistema operativo Guest per le macchine virtuali Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Monitor di Azure per la scalabilità automatica metriche di uso comune](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)articolo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="bbbe2-128">Come si configura la scalabilità automatica in un set di scalabilità di macchine virtuali tramite PowerShell?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="bbbe2-129">tooset di scalabilità automatica su una scala di macchina virtuale impostata per l'utilizzo di PowerShell, vedere post di blog hello [come tooan di scalabilità automatica tooadd scalabilità della macchina virtuale Azure impostare](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="bbbe2-130">Certificati</span><span class="sxs-lookup"><span data-stu-id="bbbe2-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="bbbe2-131">Come è forniti in modo sicuro un toohello certificato VM?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="bbbe2-132">Come è possibile implementare un toorun di set di scalabilità macchina virtuale un sito Web in cui hello SSL per il sito Web di hello viene fornito in modo sicuro da una configurazione del certificato?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="bbbe2-133">(operazione di rotazione hello comune certificato potrebbe essere quasi hello uguale a un'operazione di aggiornamento della configurazione.) Si dispone di un esempio di come toodo questo?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="bbbe2-134">toosecurely spedire toohello un certificato VM, è possibile installare un certificato cliente direttamente in un archivio certificati di Windows dall'insieme di credenziali chiave hello cliente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="bbbe2-135">Utilizzare hello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="bbbe2-136">codice Hello supporta Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="bbbe2-137">Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx) (Creare o aggiornare un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="bbbe2-138">Esempio di certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="bbbe2-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="bbbe2-139">Creare un certificato autofirmato in un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="bbbe2-140">Utilizzare hello i comandi di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="bbbe2-141">In questo modo di comando hello input per il modello di Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="bbbe2-142">Per un esempio di come toocreate un certificato autofirmato in un insieme di credenziali chiave, vedere [scenari di sicurezza di Service Fabric cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="bbbe2-143">Modificare il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="bbbe2-144">Aggiungere la proprietà troppo**virtualMachineProfile**, come parte di hello risorsa del set di scalabilità di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="bbbe2-145">È possibile specificare un toouse coppia di chiavi SSH per l'autenticazione SSH con un set da un modello di gestione risorse di scalabilità macchina virtuale Linux?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="bbbe2-146">Sì.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-146">Yes.</span></span> <span data-ttu-id="bbbe2-147">Hello API REST per **osProfile** è l'API REST di VM standard toohello simile.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="bbbe2-148">Includere **osProfile** nel modello:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="bbbe2-149">Questo blocco JSON viene utilizzato [modello di avvio rapido di hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="bbbe2-150">Hello profilo del sistema operativo viene usato anche in [grelayhost.json hello GitHub quick start modello](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="bbbe2-151">Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration) (Creare o aggiornare un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="bbbe2-152">Come si rimuovono i certificati deprecati?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="bbbe2-153">tooremove deprecata certificati, hello Rimuovi vecchio certificato dall'elenco di certificati dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="bbbe2-154">Lasciare tutti i certificati di hello che si desidera tooremain nel computer in uso nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="bbbe2-155">Ciò non rimuove il certificato di hello da tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="bbbe2-156">Non viene inoltre aggiunta hello certificato toonew le macchine virtuali che vengono creati nel set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="bbbe2-157">certificato di hello tooremove da macchine virtuali esistenti, scrivere uno script personalizzato estensione toomanually rimuovere hello certificati dall'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="bbbe2-158">Come inserisce una chiave pubblica SSH esistente nel livello SSH set di scalabilità di hello macchina virtuale durante il provisioning</span><span class="sxs-lookup"><span data-stu-id="bbbe2-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="bbbe2-159">Desiderano toostore hello SSH pubblici valori di chiave nell'insieme di credenziali chiave di Azure e quindi utilizzarle del modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="bbbe2-160">Se si desidera fornire hello macchine virtuali solo con una chiave SSH pubblica, non è necessario tooput hello le chiavi pubbliche nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="bbbe2-161">Le chiavi pubbliche non sono segrete.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="bbbe2-162">Quando si crea una VM Linux è possibile fornire le chiavi pubbliche SSH in testo normale:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="bbbe2-163">Nome dell'elemento linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="bbbe2-163">linuxConfiguration element name</span></span> | <span data-ttu-id="bbbe2-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bbbe2-164">Required</span></span> | <span data-ttu-id="bbbe2-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="bbbe2-165">Type</span></span> | <span data-ttu-id="bbbe2-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bbbe2-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="bbbe2-167">ssh</span><span class="sxs-lookup"><span data-stu-id="bbbe2-167">ssh</span></span> | <span data-ttu-id="bbbe2-168">No</span><span class="sxs-lookup"><span data-stu-id="bbbe2-168">No</span></span> | <span data-ttu-id="bbbe2-169">Raccolta</span><span class="sxs-lookup"><span data-stu-id="bbbe2-169">Collection</span></span> | <span data-ttu-id="bbbe2-170">Specifica di configurazione della chiave SSH hello per un sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="bbbe2-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="bbbe2-171">path</span><span class="sxs-lookup"><span data-stu-id="bbbe2-171">path</span></span> | <span data-ttu-id="bbbe2-172">Sì</span><span class="sxs-lookup"><span data-stu-id="bbbe2-172">Yes</span></span> | <span data-ttu-id="bbbe2-173">String</span><span class="sxs-lookup"><span data-stu-id="bbbe2-173">String</span></span> | <span data-ttu-id="bbbe2-174">Specifica percorso di file Linux hello in cui le chiavi SSH hello o un certificato deve essere collocato</span><span class="sxs-lookup"><span data-stu-id="bbbe2-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="bbbe2-175">keyData</span><span class="sxs-lookup"><span data-stu-id="bbbe2-175">keyData</span></span> | <span data-ttu-id="bbbe2-176">Sì</span><span class="sxs-lookup"><span data-stu-id="bbbe2-176">Yes</span></span> | <span data-ttu-id="bbbe2-177">String</span><span class="sxs-lookup"><span data-stu-id="bbbe2-177">String</span></span> | <span data-ttu-id="bbbe2-178">Specifica una chiave pubblica SSH con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="bbbe2-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="bbbe2-179">Per un esempio, vedere [modello di avvio rapido di hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="bbbe2-180">Durante l'esecuzione di `Update-AzureRmVmss` dopo l'aggiunta di più di un certificato da hello stessa chiave dell'insieme di credenziali, viene visualizzato hello il seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="bbbe2-181">Update-AzureRmVmss: L'elenco secrets contiene istanze ripetute di /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev. Questo scenario non è consentito.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="bbbe2-182">Questa situazione può verificarsi se si tenta di toore-aggiungere hello stesso insieme di credenziali invece di usare un nuovo certificato dell'insieme di credenziali per l'insieme di credenziali origine esistente hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="bbbe2-183">Hello `Add-AzureRmVmssSecret` comando non funziona correttamente se si aggiungono i segreti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="bbbe2-184">tooadd più segreti da hello stesso insieme di credenziali chiave, elenco $vmss.properties.osProfile.secrets[0].vaultCertificates hello di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="bbbe2-185">Per hello previsto struttura di input, vedere [crea o aggiorna una macchina virtuale impostata](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="bbbe2-186">Trovare segreto hello in hello macchina virtuale scala set oggetto nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="bbbe2-187">Aggiungere quindi l'elenco di toohello di riferimento (hello URL e il nome di archivio segreto hello) certificato associato all'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="bbbe2-188">Attualmente, è possibile rimuovere i certificati da macchine virtuali tramite API di set di scalabilità di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="bbbe2-189">Nuove macchine virtuali non avranno vecchio certificato hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="bbbe2-190">Tuttavia, le macchine virtuali che hanno certificato hello e che sono già state distribuite avranno vecchio certificato hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="bbbe2-191">È possibile il push scalabilità della macchina virtuale toohello certificati impostare senza specificare la password di hello, quando hello certificato si trova nell'archivio segreto hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="bbbe2-192">Le password hardcoded toohard negli script non è necessario.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="bbbe2-193">È possibile recuperare in modo dinamico le password con autorizzazioni di hello è utilizzare script di distribuzione toorun hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="bbbe2-194">Se si dispone di uno script che consente di spostare un certificato dall'insieme di credenziali chiave archivio segreto hello, hello archivio segreto `get certificate` comando genera anche la password di hello del file con estensione pfx hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="bbbe2-195">Impostazione di lavoro proprietà segreti hello di virtualMachineProfile.osProfile per la scala di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bbbe2-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="bbbe2-196">Perché necessario valore sourceVault hello quando si dispone di toospecify hello URI assoluto di un certificato utilizzando proprietà certificateUrl hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="bbbe2-197">Un riferimento al certificato di gestione remota Windows (WinRM) deve essere presente in hello proprietà segreti di hello profilo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="bbbe2-198">Hello indicante l'insieme di credenziali origine hello mira tooenforce controllo elenco (ACL) criteri di accesso esistono nel modello di servizio Cloud di Azure dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="bbbe2-199">Se non è specificato l'insieme di credenziali origine hello, gli utenti che non dispone delle autorizzazioni toodeploy o accesso segreti tooa insieme di credenziali chiave sarebbe in grado di toothrough un Provider di risorse di calcolo (CRP).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="bbbe2-200">Gli elenchi di controllo di accesso sono presenti anche per risorse inesistenti.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="bbbe2-201">Se si specifica un ID insieme di credenziali di origine non corretti ma un URL valido dell'insieme di credenziali chiave, viene restituito un errore quando si esegue il polling operazione hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="bbbe2-202">Se è possibile aggiungere i segreti tooan set di scalabilità della macchina virtuale esistente, i segreti hello vengono inseriti in macchine virtuali esistenti o solo in nuovi?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="bbbe2-203">I certificati vengono aggiunti tooall le macchine virtuali, preesistenti anche quelle.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="bbbe2-204">Se la scalabilità della macchina virtuale imposta proprietà upgradePolicy impostato è troppo**manuale**, certificato hello viene aggiunto toohello VM quando si esegue un aggiornamento manuale in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="bbbe2-205">Dove vengono inseriti i certificati per le macchine virtuali Linux?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="bbbe2-206">toolearn toodeploy certificati per le macchine virtuali Linux, vedere [distribuire certificati tooVMs da un insieme di credenziali chiave gestita dal cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="bbbe2-207">Come è possibile aggiungere un nuovo insieme di credenziali tooa nuovo certificato oggetto certificato?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="bbbe2-208">tooadd un insieme di credenziali tooan esistente chiave privata certificati, vedere hello esempio PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="bbbe2-209">Usare solo un oggetto segreto.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="bbbe2-210">Toocertificates cosa accade se si ricreare l'immagine di una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="bbbe2-211">Se si ricrea l'immagine di una macchina virtuale, i certificati vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="bbbe2-212">Ricreazione dell'immagine eliminazioni hello intero disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="bbbe2-213">Cosa accade se si elimina un certificato dall'insieme di credenziali chiave hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="bbbe2-214">Se il segreto hello viene eliminato dall'insieme di credenziali chiave hello e si eseguirà `stop deallocate` per tutte le macchine virtuali e riavviarle, si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="bbbe2-215">Errore Hello si verifica perché hello CRP deve segreti hello tooretrieve dall'insieme di credenziali chiave di hello, ma non è possibile.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="bbbe2-216">In questo scenario, è possibile eliminare i certificati di hello dal modello di set di scalabilità di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="bbbe2-217">componente CRP Hello non rende persistenti i segreti di cliente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="bbbe2-218">Se si esegue `stop deallocate` per tutte le macchine virtuali nel set di scalabilità della macchina virtuale hello cache di hello viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="bbbe2-219">In questo scenario, vengono recuperati i segreti dall'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="bbbe2-220">Quando la scalabilità perché è una copia memorizzata nella cache del segreto hello in Azure Service Fabric (nel modello di infrastruttura di singolo tenant hello), si non verifica questo problema.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="bbbe2-221">Perché hanno posizione esatta di hello toospecify per URL certificato hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), come indicato [scenari di sicurezza di Service Fabric cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="bbbe2-222">Hello documentazione insieme credenziali chiavi Azure si afferma che hello che ottenere API REST del segreto deve restituire più recente del segreto hello hello se hello versione non è specificata.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="bbbe2-223">Metodo</span><span class="sxs-lookup"><span data-stu-id="bbbe2-223">Method</span></span> | <span data-ttu-id="bbbe2-224">URL</span><span class="sxs-lookup"><span data-stu-id="bbbe2-224">URL</span></span>
--- | ---
<span data-ttu-id="bbbe2-225">GET</span><span class="sxs-lookup"><span data-stu-id="bbbe2-225">GET</span></span> | <span data-ttu-id="bbbe2-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="bbbe2-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="bbbe2-227">Sostituire {*secret-name*} con nome hello e sostituire {*secret-version*} con la versione di hello del segreto hello desiderato tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="bbbe2-228">versione del segreto Hello potrebbe essere escluse.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-228">hello secret version might be excluded.</span></span> <span data-ttu-id="bbbe2-229">In tal caso, la versione corrente di hello viene recuperata.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="bbbe2-230">Motivo per cui dispone la versione dei certificati hello toospecify quando si usa l'insieme di credenziali chiave?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="bbbe2-231">scopo di Hello della versione di hello insieme di credenziali chiave requisito toospecify hello certificato è toomake sia cancellare utente toohello il certificato viene distribuito in macchine virtuali di loro.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="bbbe2-232">Se si crea una macchina virtuale e quindi aggiorna il segreto nell'insieme di credenziali chiave di hello, hello nuovo certificato non è macchine virtuali tooyour scaricato.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="bbbe2-233">Ma le macchine virtuali e nuove macchine virtuali ottengono nuovo segreto hello tooreference.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="bbbe2-234">tooavoid, si è tooreference richiesto una versione del segreto.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-235">Il team collabora con diversi certificati che vengono distribuiti toous come chiavi pubbliche con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="bbbe2-236">Che cos'è l'approccio per la distribuzione di questi set di scalabilità della macchina virtuale tooa certificati consigliato hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-237">toodeploy con estensione cer chiavi pubbliche tooa scala set di macchine virtuali, è possibile generare un file con estensione pfx che contiene solo i file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="bbbe2-238">toodo questa operazione, utilizzare `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="bbbe2-239">Ad esempio, caricare il file con estensione cer hello come oggetto x509Certificate2 in c# o PowerShell e quindi chiamare il metodo hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="bbbe2-240">Per altre informazioni, vedere [Metodo X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="bbbe2-241">Un'opzione per gli utenti toopass nei certificati non vengono visualizzati come stringhe base64.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="bbbe2-242">disponibile nella maggior parte degli altri provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="bbbe2-243">tooemulate passando un certificato come una stringa base64, è possibile estrarre hello più recente con controllo delle versioni URL in un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="bbbe2-244">Includere hello proprietà JSON nel modello di gestione delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="bbbe2-245">È necessario che i certificati toowrap negli oggetti JSON in insiemi di credenziali chiave?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="bbbe2-246">Nei set di scalabilità di macchine virtuali e nelle macchine virtuali è necessario eseguire il wrapping dei certificati in oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="bbbe2-247">È anche supportata hello tipo di contenuto application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="bbbe2-248">Per istruzioni sull'uso di application/x-pkcs12, vedere [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificati PFX in Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="bbbe2-249">Non sono attualmente supportati i file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-249">We currently do not support .cer files.</span></span> <span data-ttu-id="bbbe2-250">file con estensione cer toouse, esportarli in contenitori con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="bbbe2-251">Conformità</span><span class="sxs-lookup"><span data-stu-id="bbbe2-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="bbbe2-252">I set di scalabilità di macchine virtuali sono compatibili con PCI?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="bbbe2-253">Set di scalabilità di macchine virtuali sono un livello API ridotto hello CRP.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="bbbe2-254">Entrambi i componenti fanno parte della piattaforma di calcolo hello in hello albero del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="bbbe2-255">Da una prospettiva di conformità, il set di scalabilità di macchine virtuali è una parte fondamentale della piattaforma di calcolo di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="bbbe2-256">Un team, strumenti, processi, metodologia di distribuzione, i controlli di sicurezza, just-in-time (JIT) compilazione, il monitoraggio, avvisi e così via, condividono con CRP hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="bbbe2-257">Set di scalabilità di macchine virtuali sono settore PCI (Payment Card)-conforme poiché hello CRP fa parte di attestazione di hello corrente PCI Data Security Standard (DSS).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="bbbe2-258">Per ulteriori informazioni, vedere [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="bbbe2-259">Estensioni</span><span class="sxs-lookup"><span data-stu-id="bbbe2-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="bbbe2-260">Come si elimina un'estensione del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="bbbe2-261">toodelete un scalabilità della macchina virtuale imposta l'estensione, usare hello esempio PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="bbbe2-262">È possibile trovare il valore extensionName hello in `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="bbbe2-263">È disponibile un esempio di modello di set di scalabilità di macchine virtuali che si integra con Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="bbbe2-264">Per un scalabilità della macchina virtuale del set di esempio di modello che si integra con Operations Management Suite, vedere hello secondo esempio [distribuire un cluster di Azure Service Fabric e abilitare il monitoraggio tramite Log Analitica](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="bbbe2-265">Estensioni sembrano toorun in parallelo in set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="bbbe2-266">In questo modo il toofail estensione script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="bbbe2-267">È possibile procedere toofix questo?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-267">What can I do toofix this?</span></span>

<span data-ttu-id="bbbe2-268">toolearn sulla sequenziazione di estensione nel set di scalabilità di macchine virtuali, vedere [la sequenza di estensione nel set di scalabilità di macchine virtuali di Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-269">Come reimpostare la password di hello per le macchine virtuali nel set di scalabilità della macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-270">la password tooreset hello per le macchine virtuali nella scalabilità della macchina virtuale impostata, utilizzare le estensioni di accesso VM.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="bbbe2-271">Utilizzare hello esempio PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-272">Come è possibile aggiungere un tooall estensione macchine virtuali nel set di scalabilità della macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-273">Se i criteri di aggiornamento sono stato impostato troppo**automatico**, modello di ridistribuzione hello con nuove proprietà di estensione hello Aggiorna tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="bbbe2-274">Se i criteri di aggiornamento sono stato impostato troppo**manuale**, prima di aggiornare estensione hello e quindi aggiornare manualmente tutte le istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="bbbe2-275">Se vengono aggiornate le estensioni di hello associate a un set di scalabilità macchina virtuale esistente, sono già macchine virtuali interessate?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="bbbe2-276">(Vale a dire verrà hello macchine virtuali *non* modello set di scalabilità macchina virtuale deve corrispondere hello?) O verranno ignorate?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="bbbe2-277">Quando un computer esistente viene riparato servizio o ricreata l'immagine, sono gli script hello attualmente configurate nel set di scalabilità della macchina virtuale hello eseguita o script hello che sono state configurate utilizzato hello che creazione macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="bbbe2-278">Se la definizione di estensione hello nella scalabilità della macchina virtuale hello Imposta modello viene aggiornato e hello upgradePolicy impostata troppo**automatico**, aggiorna le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="bbbe2-279">Se hello upgradePolicy impostata troppo**manuale**, le estensioni vengono contrassegnate come non corrisponde al modello hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="bbbe2-280">Se una macchina virtuale esistente viene riparato servizio, viene visualizzato come un riavvio ed estensioni hello non vengono eseguiti nuovamente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="bbbe2-281">Se ricreata l'immagine, è come sostituzione di unità del sistema operativo hello con immagine di origine hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="bbbe2-282">Qualsiasi specializzazione dal modello più recente di hello, ad esempio le estensioni, vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="bbbe2-283">Come posso iscrivermi a un dominio di Azure AD tooan set scala macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="bbbe2-284">un dominio di Azure Active Directory (Azure AD) la macchina virtuale scala set tooan toojoin, è possibile definire un'estensione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="bbbe2-285">toodefine un'estensione, usare proprietà JsonADDomainExtension hello:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="bbbe2-286">L'estensione della macchina virtuale scala set sta tentando di tooinstall qualcosa che richiede un riavvio.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="bbbe2-287">Ad esempio, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="bbbe2-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="bbbe2-288">Se l'estensione di set di scalabilità macchina virtuale tenta tooinstall qualcosa che richiede un riavvio, è possibile utilizzare l'estensione di hello Azure Automation Desired State Configuration (DSC di automazione).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="bbbe2-289">Se hello del sistema operativo è Windows Server 2012 R2, Azure effettua il pull di installazione di Windows Management Framework (WMF) 5.0 hello, riavvii e continua quindi con configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-290">Come si attiva l'antimalware nel set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-291">tooturn su antimalware nella scalabilità della macchina virtuale impostata, utilizzare hello esempio PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="bbbe2-292">È necessario tooexecute uno script personalizzato che è ospitato in un account di archiviazione privata.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="bbbe2-293">Hello script viene eseguito correttamente quando archiviazione hello è pubblico, ma quando si tenta di toouse una firma di accesso condiviso (SAS), si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="bbbe2-294">Viene visualizzato questo messaggio: "Parametri obbligatori mancanti per la firma di accesso condiviso valida".</span><span class="sxs-lookup"><span data-stu-id="bbbe2-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="bbbe2-295">Il collegamento e la firma di accesso condiviso funzionano correttamente.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="bbbe2-296">tooexecute uno script personalizzato che è ospitato in un account di archiviazione privato, configurare impostazioni protette con nome e chiave dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="bbbe2-297">Per altre informazioni, vedere [Estensione Script personalizzato per Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="bbbe2-298">Rete</span><span class="sxs-lookup"><span data-stu-id="bbbe2-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="bbbe2-299">È possibile tooassign imposta una scala tooa di sicurezza gruppo (rete), in modo che verrà applicato tooall hello, schede di rete VM nel set di hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="bbbe2-300">Sì.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-300">Yes.</span></span> <span data-ttu-id="bbbe2-301">Un gruppo di sicurezza di rete possono essere applicato direttamente il set di scalabilità di tooa per farvi riferimento nella sezione configurazioni hello hello di profilo di rete.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="bbbe2-302">Esempio:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="bbbe2-303">Come procedere uno scambio VIP per set di scalabilità della macchina virtuale in hello stessa sottoscrizione e la stessa regione?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="bbbe2-304">Se si dispone di due virtuale set di scalabilità della macchina con front-end di bilanciamento del carico di Azure e si trovano in hello stessa sottoscrizione e area, è Impossibile deallocare hello gli indirizzi IP pubblici da ognuno di essi e assegnare toohello altri.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="bbbe2-305">Per un esempio, vedere [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Scambio di indirizzi VIP: distribuzione di tipo "blu-verde" in Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="bbbe2-306">Se come hello risorse vengono deallocati allocata a livello di rete hello, ciò implica un ritardo.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="bbbe2-307">Un'opzione più rapida è toouse Gateway applicazione Azure con due pool back-end e una regola di routing.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="bbbe2-308">In alternativa, è possibile ospitare l'applicazione con [Servizio app di Azure](https://azure.microsoft.com/en-us/services/app-service/) che offre il supporto per commutare rapidamente gli slot di gestione temporanea in slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="bbbe2-309">Come è possibile specificare un intervallo di toouse di indirizzi IP privati per l'assegnazione di indirizzo IP privato statico?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="bbbe2-310">Gli indirizzi IP vengono selezionati da una subnet specificata.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="bbbe2-311">metodo di allocazione Hello di indirizzi IP di set di scalabilità macchina virtuale è sempre "dinamico", ma ciò non significa che è possono modificare questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="bbbe2-312">In questo caso, "dinamico" solo significa che non si specifica l'indirizzo IP hello in una richiesta PUT.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="bbbe2-313">Specificare hello statico impostata per l'utilizzo di subnet hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="bbbe2-314">Come distribuire una macchina virtuale scala set tooan esistente rete virtuale di Azure?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="bbbe2-315">toodeploy un scalabilità della macchina virtuale impostata tooan esistente rete virtuale di Azure, vedere [distribuire una macchina virtuale scala set tooan rete virtuale esistente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="bbbe2-316">Come aggiungere l'indirizzo IP hello di hello set toohello output di un modello della macchina virtuale prima nella scala di una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="bbbe2-317">indirizzo IP di hello tooadd di hello prima macchina virtuale in un output di toohello set di scalabilità macchina virtuale di un modello, vedere [ARM: indirizzi IP privati del VMSS ottenere](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="bbbe2-318">È possibile usare i set di scalabilità con la rete accelerata?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="bbbe2-319">Sì.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-319">Yes.</span></span> <span data-ttu-id="bbbe2-320">toouse accelerated rete, impostazioni enableAcceleratedNetworking tootrue la scala del set di configurazioni.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="bbbe2-321">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="bbbe2-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="bbbe2-322">Come è possibile configurare i server DNS hello utilizzati da un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="bbbe2-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="bbbe2-323">toocreate una scalabilità della macchina virtuale è impostato con una configurazione personalizzata di DNS, aggiungere che configurazioni sezione del set di una scala di toohello dnsSettings pacchetto JSON.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="bbbe2-324">Esempio:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="bbbe2-325">Come è possibile configurare un tooassign set scala un tooeach di indirizzo IP pubblico VM?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="bbbe2-326">toocreate set di scalabilità di macchine Virtuali che assegna un tooeach di indirizzo IP pubblico macchina virtuale, assicurarsi hello API versione di hello Microsoft.Compute/virtualMAchineScaleSets risorse 2017-03-30 e aggiungere un _publicipaddressconfiguration_ pacchetto JSON set di scalabilità toohello di sezione di configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="bbbe2-327">Esempio:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="bbbe2-328">È possibile configurare un toowork di set di scalabilità con più applicazioni gateway?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="bbbe2-329">Sì.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-329">Yes.</span></span> <span data-ttu-id="bbbe2-330">È possibile aggiungere hello id risorse per più Gateway applicazione back-end indirizzo pool toohello _applicationGatewayBackendAddressPools_ elenco hello _configurazioni IP_ sezione del set di scalabilità profilo di rete.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="bbbe2-331">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="bbbe2-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="bbbe2-332">In quale caso è consigliabile creare un set di scalabilità di macchine virtuali con meno di due macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="bbbe2-333">Uno dei motivi toocreate impostare un scalabilità della macchina virtuale con meno di due macchine virtuali verrebbero impostate le proprietà elastico toouse hello di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="bbbe2-334">Ad esempio, è possibile distribuire un set di scalabilità della macchina virtuale con zero toodefine macchine virtuali dell'infrastruttura senza sostenere i costi di esecuzione delle macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="bbbe2-335">Quindi, quando si è pronti toodeploy VM, aumentare hello "capacità" di hello set di scalabilità di macchina virtuale toohello numero di istanze di produzione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="bbbe2-336">È possibile creare un set di scalabilità di macchine virtuali con meno di due VM anche se si è interessati principalmente all'uso di un set di disponibilità con VM discrete, invece che alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="bbbe2-337">Set di scalabilità di macchine virtuali offrono un toowork modo con le unità di calcolo indifferenziato che fungibili.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="bbbe2-338">Questa uniformità è un elemento di differenziazione chiave tra set di scalabilità di macchine virtuali e set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="bbbe2-339">Molti carichi di lavoro senza stato non tengono traccia delle singole unità.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="bbbe2-340">Se si riduce il carico di lavoro di hello, è possibile scalare verso il basso tooone unità di calcolo e quindi applicare la scalabilità verticale toomany quando aumenta il carico di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-341">Come è possibile modificare il numero di hello di macchine virtuali in un set di scalabilità della macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-342">numero di hello toochange di macchine virtuali in un set di scalabilità della macchina virtuale, vedere [modificare il numero di istanze hello di un set di scalabilità della macchina virtuale](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="bbbe2-343">Come è possibile definire avvisi personalizzati per il raggiungimento di determinate soglie?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="bbbe2-344">La gestione degli avvisi per le soglie specificate offre una certa flessibilità.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="bbbe2-345">È ad esempio possibile definire webhook personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="bbbe2-346">Hello webhook esempio seguente è da un modello di gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="bbbe2-347">In questo esempio, un avviso diventa tooPagerduty.com quando viene raggiunta una soglia.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="bbbe2-348">Applicazione di patch e operazioni</span><span class="sxs-lookup"><span data-stu-id="bbbe2-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="bbbe2-349">Come si crea un set di scalabilità in un gruppo di risorse esistente?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="bbbe2-350">Creazione di set di scalabilità in una risorsa esistente gruppo non è ancora possibile da hello portale di Azure, ma è possibile specificare un gruppo di risorse esistente quando la distribuzione di una scala impostata da un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="bbbe2-351">È anche possibile specificare un gruppo di risorse esistente durante la creazione di un set di scalabilità usando Azure PowerShell o l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="bbbe2-352">È possibile spostare che una scala di imposta il gruppo di risorse tooanother?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="bbbe2-353">Sì, è possibile spostare la scala set di risorse tooa nuova sottoscrizione o gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="bbbe2-354">Come aggiornare tooI la scalabilità della macchina virtuale impostata tooa nuova immagine?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="bbbe2-355">Come si gestisce l'applicazione di patch?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-355">How do I manage patching?</span></span>

<span data-ttu-id="bbbe2-356">vedere la scalabilità della macchina virtuale impostata tooa nuova immagine e l'applicazione di patch toomanage, tooupdate [l'aggiornamento di un set di scalabilità della macchina virtuale](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="bbbe2-357">È possibile utilizzare tooreset operazione di ricreazione immagine hello una macchina virtuale senza modificare l'immagine di hello?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="bbbe2-358">(Vale a dire, desidera reimpostare un VM toofactory impostazioni anziché tooa nuova immagine.)</span><span class="sxs-lookup"><span data-stu-id="bbbe2-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="bbbe2-359">Sì, è possibile utilizzare tooreset operazione di ricreazione immagine hello una macchina virtuale senza modificare l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="bbbe2-360">Tuttavia, se è impostata la scalabilità della macchina virtuale fa riferimento a un'immagine della piattaforma con `version = latest`, la macchina virtuale è possibile aggiornare tooa successive del sistema operativo dell'immagine quando si chiama `reimage`.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="bbbe2-361">Per altre informazioni, vedere [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set) (Gestire tutte le VM in un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="bbbe2-362">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="bbbe2-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="bbbe2-363">Come si attiva la diagnostica di avvio?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="bbbe2-364">tooturn sulla diagnostica di avvio, creare innanzitutto un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="bbbe2-365">Quindi, inserire questo blocco JSON nel set di scalabilità di macchine virtuali **virtualMachineProfile**e aggiornare i set di scalabilità della macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="bbbe2-366">Quando viene creata una nuova macchina virtuale, hello proprietà InstanceView di hello VM Mostra i dettagli di hello schermata hello e così via.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="bbbe2-367">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="bbbe2-368">Proprietà della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bbbe2-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-369">Come si possono ottenere informazioni sulle proprietà di ogni macchina virtuale senza dover eseguire più chiamate?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="bbbe2-370">Ad esempio, come sarebbe? il dominio di errore hello per ognuna delle hello 100 macchine virtuali nel set di scalabilità della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bbbe2-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-371">informazioni proprietà di tooget per ogni macchina virtuale senza effettuare più chiamate, è possibile chiamare `ListVMInstanceViews` effettuando un'API REST `GET` su hello seguente URI di risorsa:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="bbbe2-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="bbbe2-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="bbbe2-373">È possibile passo degli argomenti dell'estensione diverse macchine virtuali toodifferent in un set di scalabilità della macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="bbbe2-374">No, è possibile passare argomenti estensione diverse macchine virtuali toodifferent in un set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="bbbe2-375">Tuttavia, le estensioni possono agire in base alle proprietà di univoco hello di hello VM vengono eseguiti in, ad esempio sul nome del computer hello.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="bbbe2-376">Estensioni anche possono eseguire una query i metadati dell'istanza in http://169.254.169.254 tooget ulteriori informazioni su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="bbbe2-377">Perché sono presenti gap tra i nomi delle macchine virtuali del set di scalabilità di macchine virtuali e gli ID,</span><span class="sxs-lookup"><span data-stu-id="bbbe2-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="bbbe2-378">ad esempio 0, 1, 3?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="bbbe2-379">Sono presenti interruzioni tra i nomi di computer VM set di scalabilità macchina virtuale e gli ID di macchina virtuale perché la scalabilità della macchina virtuale impostata **overprovision** proprietà è impostata un valore predefinito toohello di **true**.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="bbbe2-380">Se overprovisioning è troppo**true**, più macchine virtuali a quella richiesta vengono creati.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="bbbe2-381">Le VM aggiuntive vengono quindi eliminate.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="bbbe2-382">In questo caso, ottenere la distribuzione di una maggiore affidabilità ma spese hello di denominazione contigue e contigue Network Address Translation (NAT) delle regole.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="bbbe2-383">È possibile impostare questa proprietà troppo**false**.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-383">You can set this property too**false**.</span></span> <span data-ttu-id="bbbe2-384">Per i set di scalabilità di macchine virtuali di piccole dimensioni ciò non influisce significativamente sull'affidabilità della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="bbbe2-385">Qual è la differenza hello tra l'eliminazione di una macchina virtuale in un set di scalabilità della macchina virtuale e la deallocazione hello VM?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="bbbe2-386">Quando è consigliabile scegliere uno hello altri?</span><span class="sxs-lookup"><span data-stu-id="bbbe2-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="bbbe2-387">Hello differenza principale tra l'eliminazione di una macchina virtuale in un set di scalabilità della macchina virtuale e la deallocazione hello VM è che `deallocate` non comporta l'eliminazione hello dischi rigidi virtuali (VHD).</span><span class="sxs-lookup"><span data-stu-id="bbbe2-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="bbbe2-388">L'esecuzione di `stop deallocate` comporta costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="bbbe2-389">È possibile utilizzare uno o altro per uno dei seguenti motivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="bbbe2-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="bbbe2-390">Si desidera toostop sostenere i costi di calcolo, ma si desidera tookeep hello disco stato di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="bbbe2-391">Si desidera un set di macchine virtuali toostart più rapidamente è possibile scalare in orizzontale un set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="bbbe2-392">Scenario toothis correlati, si potrebbe essere creato il proprio motore di scalabilità automatica e si desidera una scala end-to-end più veloce.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="bbbe2-393">È presente un set di scalabilità di macchine virtuali distribuito in modo non uniforme nei domini di errore o nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="bbbe2-394">Questo problema può essere stato causato dall'eliminazione selettiva di VM o dall'eliminazione di VM dopo l'overprovisioning.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="bbbe2-395">Esecuzione `stop deallocate` seguito da `start` nella macchina virtuale hello scala impostata in modo uniforme distribuisce le macchine virtuali hello tra domini di errore o di domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe2-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

