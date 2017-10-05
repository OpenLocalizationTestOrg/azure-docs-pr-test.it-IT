---
title: "Domande frequenti sui set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Risposte alle domande frequenti sui set di scalabilità di macchine virtuali."
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
ms.openlocfilehash: f320dd5d1f8c99317792f4ae9e09bc5adaf79e25
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="e9c96-103">Domande frequenti sui set di scalabilità di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="e9c96-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="e9c96-104">Risposte alle domande frequenti sui set di scalabilità di macchine virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c96-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="e9c96-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="e9c96-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="e9c96-106">Quali sono le procedure consigliate per la scalabilità automatica di Azure?</span><span class="sxs-lookup"><span data-stu-id="e9c96-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="e9c96-107">Per informazioni sulle procedure consigliate per la scalabilità automatica, vedere [Procedure consigliate per la scalabilità automatica delle macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="e9c96-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="e9c96-108">Dove è possibile trovare i nomi delle metriche per la scalabilità automatica che usa metriche basate su host?</span><span class="sxs-lookup"><span data-stu-id="e9c96-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="e9c96-109">Per informazioni sui nomi delle metriche per la scalabilità automatica che usa metriche basate su host, vedere [Metriche supportate con Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="e9c96-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="e9c96-110">Sono disponibili eventuali esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure?</span><span class="sxs-lookup"><span data-stu-id="e9c96-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="e9c96-111">Sì.</span><span class="sxs-lookup"><span data-stu-id="e9c96-111">Yes.</span></span> <span data-ttu-id="e9c96-112">Per esempi di scalabilità automatica basata sull'argomento o sulla lunghezza della coda del bus di servizio di Azure, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="e9c96-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="e9c96-113">Per una coda del bus di servizio, usare il codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="e9c96-114">Per una coda di archiviazione, usare il codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="e9c96-115">Sostituire i valori dell'esempio con gli URI (Uniform Resource Identifier) della risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="e9c96-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="e9c96-116">È consigliabile applicare la scalabilità automatica usando metriche basate su host oppure un'estensione di diagnostica?</span><span class="sxs-lookup"><span data-stu-id="e9c96-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="e9c96-117">È possibile creare un'impostazione di scalabilità automatica in una macchina virtuale per l'uso di metriche a livello di host o per l'uso di metriche basate sul sistema operativo guest.</span><span class="sxs-lookup"><span data-stu-id="e9c96-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="e9c96-118">Per un elenco delle metriche supportate, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="e9c96-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="e9c96-119">Per un esempio completo per i set di scalabilità di macchine virtuali, vedere [Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="e9c96-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="e9c96-120">L'esempio usa la metrica relativa alla CPU a livello di host e una metrica di conteggio dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="e9c96-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-121">Come si impostano le regole di avviso in un set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-122">È possibile creare avvisi sulle metriche per i set di scalabilità di macchine virtuali tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c96-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="e9c96-123">Per altre informazioni, vedere [Esempi di avvio rapido con PowerShell per Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) ed [Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="e9c96-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="e9c96-124">Il valore TargetResourceId del set di scalabilità di macchine virtuali ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="e9c96-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="e9c96-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="e9c96-126">È possibile scegliere qualsiasi contatore delle prestazioni delle macchine virtuali come metrica per cui impostare un avviso.</span><span class="sxs-lookup"><span data-stu-id="e9c96-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="e9c96-127">Per altre informazioni, vedere [Metriche del sistema operativo guest per le VM Windows basate su Resource Manager](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [Metriche del sistema operativo guest per le VM Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) nell'articolo [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="e9c96-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="e9c96-128">Come si configura la scalabilità automatica in un set di scalabilità di macchine virtuali tramite PowerShell?</span><span class="sxs-lookup"><span data-stu-id="e9c96-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="e9c96-129">Per configurare la scalabilità automatica in un set di scalabilità di macchine virtuali tramite PowerShell, vedere il post di blog [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/) (Come aggiungere la scalabilità automatica in un set di scalabilità di macchine virtuali di Azure).</span><span class="sxs-lookup"><span data-stu-id="e9c96-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="e9c96-130">Certificati</span><span class="sxs-lookup"><span data-stu-id="e9c96-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="e9c96-131">Come si invia un certificato alla VM in modo sicuro?</span><span class="sxs-lookup"><span data-stu-id="e9c96-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="e9c96-132">Come si effettua il provisioning di un set di scalabilità di macchine virtuali per eseguire un sito Web in cui il certificato SSL per il sito Web viene inviato in modo sicuro da una configurazione del certificato?</span><span class="sxs-lookup"><span data-stu-id="e9c96-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="e9c96-133">L'operazione di rotazione del certificato comune è quasi uguale a un'operazione di aggiornamento della configurazione. È disponibile un esempio per questa operazione?</span><span class="sxs-lookup"><span data-stu-id="e9c96-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="e9c96-134">Per inviare in modo sicuro un certificato alla macchina virtuale, è possibile installare un certificato cliente direttamente nell'archivio certificati Windows dall'insieme di credenziali delle chiavi del cliente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="e9c96-135">Usare il codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-135">Use the following JSON:</span></span>

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

<span data-ttu-id="e9c96-136">Il codice supporta Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="e9c96-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="e9c96-137">Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx) (Creare o aggiornare un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="e9c96-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="e9c96-138">Esempio di certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="e9c96-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="e9c96-139">Creare un certificato autofirmato in un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="e9c96-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="e9c96-140">Usare i comandi di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="e9c96-140">Use the following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="e9c96-141">Questo comando fornisce l'input per il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c96-141">This command gives you the input for the Azure Resource Manager template.</span></span>

    <span data-ttu-id="e9c96-142">Per un esempio della creazione di un certificato autofirmato in un insieme di credenziali delle chiavi, vedere [Scenari di sicurezza di un cluster di Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="e9c96-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="e9c96-143">Modificare il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c96-143">Change the Resource Manager template.</span></span>

    <span data-ttu-id="e9c96-144">Aggiungere questa proprietà a **virtualMachineProfile**, come parte della risorsa del set di scalabilità di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="e9c96-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

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
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="e9c96-145">È possibile specificare una coppia di chiavi SSH da usare per l'autenticazione SSH con un set di scalabilità di macchine virtuali Linux da un modello di Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="e9c96-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="e9c96-146">Sì.</span><span class="sxs-lookup"><span data-stu-id="e9c96-146">Yes.</span></span> <span data-ttu-id="e9c96-147">L'API REST per **osProfile** è simile all'API REST delle macchine virtuali standard.</span><span class="sxs-lookup"><span data-stu-id="e9c96-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="e9c96-148">Includere **osProfile** nel modello:</span><span class="sxs-lookup"><span data-stu-id="e9c96-148">Include **osProfile** in your template:</span></span>

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
 
<span data-ttu-id="e9c96-149">Questo blocco JSON viene usato nel [modello di avvio rapido 101-vm-sshkey di GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e9c96-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="e9c96-150">Il profilo del sistema operativo viene usato anche nel [modello di avvio rapido grelayhost.json di GitHub](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="e9c96-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="e9c96-151">Per altre informazioni, vedere [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration) (Creare o aggiornare un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="e9c96-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="e9c96-152">Come si rimuovono i certificati deprecati?</span><span class="sxs-lookup"><span data-stu-id="e9c96-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="e9c96-153">Per rimuovere i certificati deprecati, rimuovere il certificato precedente dall'elenco di certificati dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="e9c96-154">Lasciare nell'elenco tutti i certificati da conservare nel computer.</span><span class="sxs-lookup"><span data-stu-id="e9c96-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="e9c96-155">Questa operazione non rimuove il certificato da tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="e9c96-156">Non aggiunge inoltre il certificato alle nuove macchine virtuali create nel set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="e9c96-157">Per rimuovere il certificato dalle macchine virtuali esistenti, scrivere un'estensione personalizzata dello script per rimuovere manualmente i certificati dall'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="e9c96-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="e9c96-158">Come si inserisce una chiave pubblica SSH esistente nel livello SSH del set di scalabilità di macchine virtuali durante il provisioning?</span><span class="sxs-lookup"><span data-stu-id="e9c96-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="e9c96-159">Si vuole archiviare i valori della chiave pubblica SSH in Azure Key Vault e quindi usarli nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c96-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="e9c96-160">Se si fornisce alle macchine virtuali solo una chiave SSH pubblica, non è necessario inserire le chiavi pubbliche in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e9c96-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="e9c96-161">Le chiavi pubbliche non sono segrete.</span><span class="sxs-lookup"><span data-stu-id="e9c96-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="e9c96-162">Quando si crea una VM Linux è possibile fornire le chiavi pubbliche SSH in testo normale:</span><span class="sxs-lookup"><span data-stu-id="e9c96-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

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
 
<span data-ttu-id="e9c96-163">Nome dell'elemento linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="e9c96-163">linuxConfiguration element name</span></span> | <span data-ttu-id="e9c96-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e9c96-164">Required</span></span> | <span data-ttu-id="e9c96-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9c96-165">Type</span></span> | <span data-ttu-id="e9c96-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9c96-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="e9c96-167">ssh</span><span class="sxs-lookup"><span data-stu-id="e9c96-167">ssh</span></span> | <span data-ttu-id="e9c96-168">No</span><span class="sxs-lookup"><span data-stu-id="e9c96-168">No</span></span> | <span data-ttu-id="e9c96-169">Raccolta</span><span class="sxs-lookup"><span data-stu-id="e9c96-169">Collection</span></span> | <span data-ttu-id="e9c96-170">Specifica la configurazione delle chiavi SSH per un sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="e9c96-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="e9c96-171">path</span><span class="sxs-lookup"><span data-stu-id="e9c96-171">path</span></span> | <span data-ttu-id="e9c96-172">Sì</span><span class="sxs-lookup"><span data-stu-id="e9c96-172">Yes</span></span> | <span data-ttu-id="e9c96-173">String</span><span class="sxs-lookup"><span data-stu-id="e9c96-173">String</span></span> | <span data-ttu-id="e9c96-174">Specifica il percorso del file Linux in cui devono essere salvate le chiavi SSH o il certificato</span><span class="sxs-lookup"><span data-stu-id="e9c96-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="e9c96-175">keyData</span><span class="sxs-lookup"><span data-stu-id="e9c96-175">keyData</span></span> | <span data-ttu-id="e9c96-176">Sì</span><span class="sxs-lookup"><span data-stu-id="e9c96-176">Yes</span></span> | <span data-ttu-id="e9c96-177">String</span><span class="sxs-lookup"><span data-stu-id="e9c96-177">String</span></span> | <span data-ttu-id="e9c96-178">Specifica una chiave pubblica SSH con codifica Base64</span><span class="sxs-lookup"><span data-stu-id="e9c96-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="e9c96-179">Per un esempio, vedere il [modello di avvio rapido 101-vm-sshkey di GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e9c96-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="e9c96-180">Quando si esegue `Update-AzureRmVmss` dopo avere aggiunto più di un certificato dallo stesso insieme di credenziali delle chiavi, viene visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
><span data-ttu-id="e9c96-181">Update-AzureRmVmss: L'elenco secrets contiene istanze ripetute di /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev. Questo scenario non è consentito.</span><span class="sxs-lookup"><span data-stu-id="e9c96-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="e9c96-182">Questo problema si può verificare se si prova ad aggiungere di nuovo lo stesso insieme di credenziali invece di usare un nuovo certificato dell'insieme di credenziali per l'insieme di credenziali di origine esistente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="e9c96-183">Il comando `Add-AzureRmVmssSecret` non funziona correttamente se si aggiungono altri segreti.</span><span class="sxs-lookup"><span data-stu-id="e9c96-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="e9c96-184">Per aggiungere altri segreti dallo stesso insieme di credenziali delle chiavi, aggiornare l'elenco $vmss.properties.osProfile.secrets[0].vaultCertificates.</span><span class="sxs-lookup"><span data-stu-id="e9c96-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="e9c96-185">Per la struttura di input prevista, vedere [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx) (Creare o aggiornare un set di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="e9c96-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="e9c96-186">Trovare il segreto nell'oggetto del set di scalabilità di macchine virtuali presente nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="e9c96-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="e9c96-187">Aggiungere quindi il riferimento al certificato, ovvero l'URL e il nome dell'archivio di certificati, all'elenco associato all'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="e9c96-188">Non è attualmente possibile rimuovere i certificati dalle macchine virtuali usando l'API del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="e9c96-189">Le nuove macchine virtuali non includeranno il certificato precedente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="e9c96-190">Le VM che includono il certificato e che sono già distribuite avranno tuttavia il certificato precedente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="e9c96-191">È possibile inserire i certificati nel set di scalabilità di macchine virtuali senza specificare la password quando il certificato si trova nell'archivio di segreti?</span><span class="sxs-lookup"><span data-stu-id="e9c96-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="e9c96-192">Non è necessario usare password hardcoded negli script.</span><span class="sxs-lookup"><span data-stu-id="e9c96-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="e9c96-193">È possibile recuperare in modo dinamico le password con le autorizzazioni usate per eseguire lo script di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="e9c96-194">Se è presente uno script che sposta un certificato dall'insieme di credenziali delle chiavi dell'archivio di segreti, il comando `get certificate` dell'archivio di segreti restituisce la password del file con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="e9c96-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="e9c96-195">Come funziona la proprietà Secrets di virtualMachineProfile.osProfile per un set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="e9c96-196">Perché è necessario il valore sourceVault quando occorre specificare l'URI assoluto per un certificato usando la proprietà certificateUrl?</span><span class="sxs-lookup"><span data-stu-id="e9c96-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="e9c96-197">Un riferimento al certificato Windows Remote Management (WinRM) deve essere presente nella proprietà Secrets del profilo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="e9c96-198">L'indicazione dell'insieme di credenziali di origine consente di applicare i criteri dell'elenco di controllo di accesso esistenti nel modello di Servizi cloud di Azure di un utente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="e9c96-199">Se l'insieme di credenziali di origine non è specificato, gli utenti che non sono autorizzati a distribuire o ad accedere ai segreti in un insieme di credenziali delle chiavi potrebbero eseguire l'accesso tramite provider di risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="e9c96-200">Gli elenchi di controllo di accesso sono presenti anche per risorse inesistenti.</span><span class="sxs-lookup"><span data-stu-id="e9c96-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="e9c96-201">Se si specifica un ID errato per l'insieme di credenziali di origine ma un URL valido per l'insieme di credenziali delle chiavi, viene segnalato un errore quando si esegue il polling dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="e9c96-202">Se si aggiungono segreti a un set di scalabilità di macchine virtuali, i segreti vengono inseriti nelle VM esistenti o solo nelle nuove macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="e9c96-203">I certificati vengono aggiunti a tutte le macchine virtuali, comprese quelle già esistenti.</span><span class="sxs-lookup"><span data-stu-id="e9c96-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="e9c96-204">Se la proprietà upgradePolicy del set di scalabilità di macchine virtuali è impostata su **manual**, il certificato viene aggiunto alla VM quando si esegue un aggiornamento manuale nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e9c96-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="e9c96-205">Dove vengono inseriti i certificati per le macchine virtuali Linux?</span><span class="sxs-lookup"><span data-stu-id="e9c96-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="e9c96-206">Per informazioni su come distribuire i certificati per le macchine virtuali Linux, vedere [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) (Distribuire certificati nelle VM da un insieme di credenziali delle chiavi gestito dai clienti).</span><span class="sxs-lookup"><span data-stu-id="e9c96-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="e9c96-207">Come si aggiunge un nuovo certificato dell'insieme di credenziali a un nuovo oggetto certificato?</span><span class="sxs-lookup"><span data-stu-id="e9c96-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="e9c96-208">Per aggiungere un certificato dell'insieme di credenziali a un segreto esistente, vedere l'esempio di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="e9c96-209">Usare solo un oggetto segreto.</span><span class="sxs-lookup"><span data-stu-id="e9c96-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="e9c96-210">Cosa accade ai certificati se si ricrea l'immagine di una macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="e9c96-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="e9c96-211">Se si ricrea l'immagine di una macchina virtuale, i certificati vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="e9c96-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="e9c96-212">La ricreazione dell'immagine elimina l'intero disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="e9c96-213">Cosa accade se si elimina un certificato dall'insieme di credenziali delle chiavi?</span><span class="sxs-lookup"><span data-stu-id="e9c96-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="e9c96-214">Se si elimina il segreto dall'insieme di credenziali delle chiavi, si esegue `stop deallocate` per tutte le macchine virtuali e quindi si riavviano le VM, si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="e9c96-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="e9c96-215">L'errore si verifica perché il provider di risorse di calcolo deve recuperare i segreti dall'insieme di credenziali delle chiavi ma non riesce.</span><span class="sxs-lookup"><span data-stu-id="e9c96-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="e9c96-216">In questo scenario è possibile eliminare i certificati dal modello del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="e9c96-217">Il provider di risorse di calcolo non rende persistenti i segreti dei clienti.</span><span class="sxs-lookup"><span data-stu-id="e9c96-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="e9c96-218">Se si esegue `stop deallocate` per tutte le macchine virtuali nel set di scalabilità di macchine virtuali, la cache viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="e9c96-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="e9c96-219">In questo scenario, i segreti vengono recuperati dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="e9c96-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="e9c96-220">Questo problema non si verifica durante l'aumento del numero di istanze, perché è disponibile una copia del segreto memorizzata nella cache in Azure Service Fabric nel modello di tenant a infrastruttura singola.</span><span class="sxs-lookup"><span data-stu-id="e9c96-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="e9c96-221">Per quale motivo è necessario specificare la posizione esatta per l'URL di certificato (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), come indicato in [Scenari di sicurezza di un cluster di Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="e9c96-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="e9c96-222">La documentazione di Azure Key Vault indica che l'API REST di recupero del segreto deve restituire la versione più recente del segreto nel caso in cui la versione non sia specificata.</span><span class="sxs-lookup"><span data-stu-id="e9c96-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="e9c96-223">Metodo</span><span class="sxs-lookup"><span data-stu-id="e9c96-223">Method</span></span> | <span data-ttu-id="e9c96-224">URL</span><span class="sxs-lookup"><span data-stu-id="e9c96-224">URL</span></span>
--- | ---
<span data-ttu-id="e9c96-225">GET</span><span class="sxs-lookup"><span data-stu-id="e9c96-225">GET</span></span> | <span data-ttu-id="e9c96-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="e9c96-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="e9c96-227">Sostituire {*secret-name*} con il nome e {*secret-version*} con la versione del segreto da recuperare.</span><span class="sxs-lookup"><span data-stu-id="e9c96-227">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="e9c96-228">È possibile che la versione del segreto venga esclusa.</span><span class="sxs-lookup"><span data-stu-id="e9c96-228">The secret version might be excluded.</span></span> <span data-ttu-id="e9c96-229">In questo caso viene recuperata la versione corrente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-229">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="e9c96-230">Per quale motivo è necessario specificare la versione del certificato quando si usa Key Vault?</span><span class="sxs-lookup"><span data-stu-id="e9c96-230">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="e9c96-231">Il requisito di Key Vault che richiede di specificare la versione del specificato consente di indicare chiaramente all'utente il certificato che viene distribuito nelle rispettive macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-231">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="e9c96-232">Se si crea una macchina virtuale e quindi si aggiorna il segreto nell'insieme di credenziali delle chiavi, il nuovo certificato non viene scaricato nelle VM.</span><span class="sxs-lookup"><span data-stu-id="e9c96-232">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="e9c96-233">Le macchine virtuali fanno tuttavia riferimento al certificato e le nuove VM ottengono il nuovo segreto.</span><span class="sxs-lookup"><span data-stu-id="e9c96-233">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="e9c96-234">Per evitare questo problema, è necessario fare riferimento a una versione del segreto.</span><span class="sxs-lookup"><span data-stu-id="e9c96-234">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-235">Il team lavora con diversi certificati che vengono distribuiti come chiavi pubbliche CER.</span><span class="sxs-lookup"><span data-stu-id="e9c96-235">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="e9c96-236">Qual è l'approccio consigliato per la distribuzione dei certificati nel set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-236">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-237">Per distribuire le chiavi pubbliche con estensione cer in un set di scalabilità di macchine virtuali, è possibile generare un file con estensione pfx che contiene solo file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="e9c96-237">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="e9c96-238">A questo scopo, usare `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="e9c96-238">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="e9c96-239">Caricare ad esempio il file con estensione cer come oggetto x509Certificate2 in C# o PowerShell, quindi chiamare il metodo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-239">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="e9c96-240">Per altre informazioni, vedere [Metodo X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e9c96-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="e9c96-241">Non è presente un'opzione per passare i certificati sotto forma di stringhe Base64,</span><span class="sxs-lookup"><span data-stu-id="e9c96-241">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="e9c96-242">disponibile nella maggior parte degli altri provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9c96-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="e9c96-243">Per emulare il passaggio di un certificato come stringa Base64, è possibile estrarre l'URL con versione più recente in un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c96-243">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="e9c96-244">Includere la proprietà JSON seguente nel modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e9c96-244">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="e9c96-245">È necessario eseguire il wrapping dei certificati in oggetti JSON negli insiemi di credenziali delle chiavi?</span><span class="sxs-lookup"><span data-stu-id="e9c96-245">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="e9c96-246">Nei set di scalabilità di macchine virtuali e nelle macchine virtuali è necessario eseguire il wrapping dei certificati in oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="e9c96-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="e9c96-247">È anche supportato il tipo di contenuto application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="e9c96-247">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="e9c96-248">Per istruzioni sull'uso di application/x-pkcs12, vedere [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificati PFX in Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="e9c96-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="e9c96-249">Non sono attualmente supportati i file con estensione cer.</span><span class="sxs-lookup"><span data-stu-id="e9c96-249">We currently do not support .cer files.</span></span> <span data-ttu-id="e9c96-250">Per usare i file con estensione cer, esportarli in contenitori PFX.</span><span class="sxs-lookup"><span data-stu-id="e9c96-250">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="e9c96-251">Conformità</span><span class="sxs-lookup"><span data-stu-id="e9c96-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="e9c96-252">I set di scalabilità di macchine virtuali sono compatibili con PCI?</span><span class="sxs-lookup"><span data-stu-id="e9c96-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="e9c96-253">I set di scalabilità di macchine virtuali sono un sottile livello API disponibile sopra il provider di risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-253">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="e9c96-254">Entrambi i componenti sono parte della piattaforma di calcolo nell'albero dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c96-254">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="e9c96-255">Dal punto di vista della conformità, i set di scalabilità di macchine virtuali sono una parte essenziale della piattaforma di calcolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c96-255">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="e9c96-256">Condividono un team, strumenti, processi, metodologia di distribuzione, controlli di sicurezza, compilazione Just-In-Time (JIT), monitoraggio, avvisi e così via con il provider di risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="e9c96-257">I set di scalabilità di macchine virtuali sono compatibili con PCI (Payment Card Industry) perché il provider di risorse di calcolo è parte dell'attestazione PCI Data Security Standard (DSS) corrente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="e9c96-258">Per altre informazioni, vedere il [Centro protezione Microsoft](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="e9c96-258">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="e9c96-259">Estensioni</span><span class="sxs-lookup"><span data-stu-id="e9c96-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="e9c96-260">Come si elimina un'estensione del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="e9c96-261">Per eliminare un'estensione del set di scalabilità di macchine virtuali, usare l'esempio di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-261">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="e9c96-262">È possibile trovare il valore extensionName in `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="e9c96-262">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="e9c96-263">È disponibile un esempio di modello di set di scalabilità di macchine virtuali che si integra con Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="e9c96-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="e9c96-264">Per un esempio di modello di set di scalabilità di macchine virtuali che si integra con Operations Management Suite, vedere il secondo esempio in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric) (Distribuire un cluster di Azure Service Fabric e abilitare il monitoraggio usando Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="e9c96-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="e9c96-265">Le estensioni vengono eseguite apparentemente in parallelo nei set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-265">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="e9c96-266">Ciò provoca un errore dell'estensione di script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e9c96-266">This causes my custom script extension to fail.</span></span> <span data-ttu-id="e9c96-267">Come si può risolvere questo problema?</span><span class="sxs-lookup"><span data-stu-id="e9c96-267">What can I do to fix this?</span></span>

<span data-ttu-id="e9c96-268">Per informazioni sulla sequenziazione di estensioni nei set di scalabilità di macchine virtuali, vedere [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/) (Sequenziazione delle estensioni nei set di scalabilità di macchine virtuali di Azure).</span><span class="sxs-lookup"><span data-stu-id="e9c96-268">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-269">Come si reimposta la password per le VM nel set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-269">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-270">Per reimpostare la password per le VM nel set di scalabilità di macchine virtuali, usare le estensioni di accesso delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-270">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="e9c96-271">Usare l'esempio di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-271">Use the following PowerShell example:</span></span>

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
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-272">Come si aggiunge un'estensione a tutte le macchine virtuali del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-272">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-273">Se i criteri impostati prevedono l'aggiornamento **automatico**, ridistribuendo il modello con le nuove proprietà di estensione verranno aggiornate tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-273">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="e9c96-274">Se i criteri di aggiornamento sono impostati su **manuale**, aggiornare prima di tutto l'estensione e quindi aggiornare manualmente tutte le istanze nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-274">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="e9c96-275">Se le estensioni associate a un set di scalabilità di macchine virtuali esistente vengono aggiornate, l'operazione influisce sulle VM esistenti,</span><span class="sxs-lookup"><span data-stu-id="e9c96-275">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="e9c96-276">ovvero, le VM *non* corrisponderanno al modello di set di scalabilità di macchine virtuali? O verranno ignorate?</span><span class="sxs-lookup"><span data-stu-id="e9c96-276">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="e9c96-277">Quando una macchina virtuale esistente viene sottoposta a ripristino del servizio o ricreazione dell'immagine, gli script attualmente configurati nel set di scalabilità di macchine virtuali vengono eseguiti o vengono usati gli script configurati durante la creazione iniziale della macchina virtuale?</span><span class="sxs-lookup"><span data-stu-id="e9c96-277">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="e9c96-278">Se la definizione dell'estensione nel modello di set di scalabilità di macchine virtuali viene aggiornata e la proprietà upgradePolicy è impostata su **automatic**, le macchine virtuali vengono aggiornate.</span><span class="sxs-lookup"><span data-stu-id="e9c96-278">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="e9c96-279">Se la proprietà upgradePolicy è impostata su **manual**, le estensioni vengono contrassegnate come non corrispondenti al modello.</span><span class="sxs-lookup"><span data-stu-id="e9c96-279">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="e9c96-280">Il ripristino del servizio di una VM esistente viene considerato un riavvio e le estensioni non vengono eseguite di nuovo.</span><span class="sxs-lookup"><span data-stu-id="e9c96-280">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="e9c96-281">Se viene ricreata l'immagine, tale operazione è simile alla sostituzione dell'unità del sistema operativo con l'immagine di origine.</span><span class="sxs-lookup"><span data-stu-id="e9c96-281">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="e9c96-282">Vengono eseguite eventuali specializzazioni dal modello più recente, ad esempio le estensioni.</span><span class="sxs-lookup"><span data-stu-id="e9c96-282">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="e9c96-283">Come si aggiunge un set di scalabilità di macchine virtuali a un dominio di Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e9c96-283">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="e9c96-284">Per aggiungere un set di scalabilità di macchine virtuali a un dominio di Azure Active Directory (Azure AD), è possibile definire un'estensione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-284">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="e9c96-285">Per definire un'estensione, usare la proprietà JsonADDomainExtension:</span><span class="sxs-lookup"><span data-stu-id="e9c96-285">To define an extension, use the JsonADDomainExtension property:</span></span>

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="e9c96-286">L'estensione del set di scalabilità di macchine virtuali sta provando a installare un programma che richiede un riavvio.</span><span class="sxs-lookup"><span data-stu-id="e9c96-286">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="e9c96-287">Ad esempio, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="e9c96-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="e9c96-288">Se l'estensione del set di scalabilità di macchine virtuali prova a installare un programma che richiede un riavvio, è possibile usare l'estensione Automation DSC (Desired State Configuration) per Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c96-288">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="e9c96-289">Se il sistema operativo è Windows Server 2012 R2, Azure esegue il pull del programma di installazione di Windows Management Framework (WMF) 5.0, esegue il riavvio e quindi prosegue con la configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-289">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-290">Come si attiva l'antimalware nel set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-291">Per attivare l'antimalware nel set di scalabilità di macchine virtuali, usare l'esempio di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-291">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="e9c96-292">È necessario eseguire uno script personalizzato ospitato in un account di archiviazione privato.</span><span class="sxs-lookup"><span data-stu-id="e9c96-292">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="e9c96-293">Lo script viene eseguito correttamente quando la risorsa di archiviazione è pubblica, ma si verifica un errore quando si prova a usare una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="e9c96-293">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="e9c96-294">Viene visualizzato questo messaggio: "Parametri obbligatori mancanti per la firma di accesso condiviso valida".</span><span class="sxs-lookup"><span data-stu-id="e9c96-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="e9c96-295">Il collegamento e la firma di accesso condiviso funzionano correttamente.</span><span class="sxs-lookup"><span data-stu-id="e9c96-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="e9c96-296">Per eseguire uno script personalizzato ospitato in un account di archiviazione provato, configurare le impostazioni protette con la chiave e il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-296">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="e9c96-297">Per altre informazioni, vedere [Estensione Script personalizzato per Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="e9c96-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="e9c96-298">Rete</span><span class="sxs-lookup"><span data-stu-id="e9c96-298">Networking</span></span>
 
### <a name="is-it-possible-to-assign-a-network-security-group-nsg-to-a-scale-set-so-that-it-will-apply-to-all-the-vm-nics-in-the-set"></a><span data-ttu-id="e9c96-299">È possibile assegnare un gruppo di sicurezza di rete (NSG) a un set di scalabilità, in modo che venga applicato a tutte le schede di interfaccia di rete della VM presenti in tale set?</span><span class="sxs-lookup"><span data-stu-id="e9c96-299">Is it possible to assign a Network Security Group (NSG) to a scale set, so that it will apply to all the VM NICs in the set?</span></span>

<span data-ttu-id="e9c96-300">Sì.</span><span class="sxs-lookup"><span data-stu-id="e9c96-300">Yes.</span></span> <span data-ttu-id="e9c96-301">È possibile applicare un gruppo di sicurezza di rete direttamente a un set di scalabilità facendovi riferimento nella sezione networkInterfaceConfigurations del profilo di rete.</span><span class="sxs-lookup"><span data-stu-id="e9c96-301">A Network Security Group can be applied directly to a scale set by referencing it in the networkInterfaceConfigurations section of the network profile.</span></span> <span data-ttu-id="e9c96-302">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e9c96-302">Example:</span></span>

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="e9c96-303">Come si esegue lo scambio di indirizzi VIP per i set di scalabilità di macchine virtuali che si trovano nella stessa sottoscrizione e nella stessa area?</span><span class="sxs-lookup"><span data-stu-id="e9c96-303">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="e9c96-304">Se si hanno due set di scalabilità di macchine virtuali con front-end di Azure Load Balancer, che sono nella stessa sottoscrizione e area, è possibile deallocare gli indirizzi IP pubblici da uno e assegnarli all'altro.</span><span class="sxs-lookup"><span data-stu-id="e9c96-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in the same subscription and region, you could deallocate the public IP addresses from each one, and assign to the other.</span></span> <span data-ttu-id="e9c96-305">Per un esempio, vedere [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Scambio di indirizzi VIP: distribuzione di tipo "blu-verde" in Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="e9c96-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="e9c96-306">Ciò implica un ritardo anche se le risorse vengono deallocate/allocate a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="e9c96-306">This does imply a delay though as the resources are deallocated/allocated at the network level.</span></span> <span data-ttu-id="e9c96-307">Un'opzione più rapida consiste nell'usare il Gateway applicazione di Azure con due pool di back-end e una regola di routing.</span><span class="sxs-lookup"><span data-stu-id="e9c96-307">A faster option is to use Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="e9c96-308">In alternativa, è possibile ospitare l'applicazione con [Servizio app di Azure](https://azure.microsoft.com/en-us/services/app-service/) che offre il supporto per commutare rapidamente gli slot di gestione temporanea in slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="e9c96-309">Come è possibile specificare un intervallo di indirizzi IP privati per l'allocazione di indirizzi IP privati statici?</span><span class="sxs-lookup"><span data-stu-id="e9c96-309">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="e9c96-310">Gli indirizzi IP vengono selezionati da una subnet specificata.</span><span class="sxs-lookup"><span data-stu-id="e9c96-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="e9c96-311">Il metodo di allocazione degli indirizzi IP del set di scalabilità di macchine virtuali è sempre "dinamico", ma ciò non significa che è possibile modificare questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="e9c96-311">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="e9c96-312">In questo caso, per "dinamico" si intende solo che non è necessario specificare l'indirizzo IP in una richiesta PUT.</span><span class="sxs-lookup"><span data-stu-id="e9c96-312">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="e9c96-313">Specificare il set statico usando la subnet.</span><span class="sxs-lookup"><span data-stu-id="e9c96-313">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="e9c96-314">Come si distribuisce un set di scalabilità di macchine virtuali in una rete virtuale di Azure esistente?</span><span class="sxs-lookup"><span data-stu-id="e9c96-314">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="e9c96-315">Per distribuire un set di scalabilità di macchine virtuali in una rete virtuale di Azure esistente, vedere [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet) (Distribuire un set di scalabilità di macchine virtuali in una rete virtuale esistente).</span><span class="sxs-lookup"><span data-stu-id="e9c96-315">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="e9c96-316">Come si aggiunge l'indirizzo IP della prima VM di un set di scalabilità di macchine virtuali all'output di un modello?</span><span class="sxs-lookup"><span data-stu-id="e9c96-316">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="e9c96-317">Per aggiungere l'indirizzo IP della prima VM di un set di scalabilità di macchine virtuali all'output di un modello, vedere [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips) (ARM: Ottenere gli indirizzi IP privati di VMSS).</span><span class="sxs-lookup"><span data-stu-id="e9c96-317">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="e9c96-318">È possibile usare i set di scalabilità con la rete accelerata?</span><span class="sxs-lookup"><span data-stu-id="e9c96-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="e9c96-319">Sì.</span><span class="sxs-lookup"><span data-stu-id="e9c96-319">Yes.</span></span> <span data-ttu-id="e9c96-320">Per usare la rete accelerata, impostare enableAcceleratedNetworking su true nelle impostazioni networkInterfaceConfigurations del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-320">To use accelerated networking, set enableAcceleratedNetworking to true in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="e9c96-321">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="e9c96-321">E.g.</span></span>
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

### <a name="how-can-i-configure-the-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="e9c96-322">Come è possibile configurare i server DNS usati da un set di scalabilità?</span><span class="sxs-lookup"><span data-stu-id="e9c96-322">How can I configure the DNS servers used by a scale set?</span></span>

<span data-ttu-id="e9c96-323">Per creare un set di scalabilità di macchine virtuali con una configurazione DNS personalizzata, aggiungere un pacchetto JSON dnsSettings alla sezione networkInterfaceConfigurations del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-323">To create a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="e9c96-324">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e9c96-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-to-assign-a-public-ip-address-to-each-vm"></a><span data-ttu-id="e9c96-325">Come è possibile configurare un set di scalabilità per assegnare un indirizzo IP pubblico a ogni VM?</span><span class="sxs-lookup"><span data-stu-id="e9c96-325">How can I configure a scale set to assign a public IP address to each VM?</span></span>

<span data-ttu-id="e9c96-326">Per creare un set di scalabilità di macchine virtuali che assegni un indirizzo IP pubblico a ogni VM, verificare che la versione API della risorsa Microsoft.Compute/virtualMAchineScaleSets sia 2017-03-30 e aggiungere un pacchetto JSON _publicipaddressconfiguration_ alla sezione ipConfigurations del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-326">To create a VM scale set that assigns a public IP address to each VM, make sure the API version of the Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet to the scale set ipConfigurations section.</span></span> <span data-ttu-id="e9c96-327">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e9c96-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-to-work-with-multiple-application-gateways"></a><span data-ttu-id="e9c96-328">È possibile configurare un set di scalabilità da usare con più gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="e9c96-328">Can I configure a scale set to work with multiple Application Gateways?</span></span>

<span data-ttu-id="e9c96-329">Sì.</span><span class="sxs-lookup"><span data-stu-id="e9c96-329">Yes.</span></span> <span data-ttu-id="e9c96-330">È possibile aggiungere ID risorsa per più pool di indirizzi di back-end del gateway applicazione all'elenco _applicationGatewayBackendAddressPools_ nella sezione _ipConfigurations_ del profilo della rete del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-330">You can add the resource id's for multiple Application Gateway backend address pools to the _applicationGatewayBackendAddressPools_ list in the _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="e9c96-331">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="e9c96-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="e9c96-332">In quale caso è consigliabile creare un set di scalabilità di macchine virtuali con meno di due macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="e9c96-333">Un motivo per la creazione di un set di scalabilità di macchine virtuali con meno di due VM può essere relativo all'uso delle proprietà elastiche di un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-333">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="e9c96-334">È ad esempio possibile distribuire un set di scalabilità di macchine virtuali con zero VM per definire l'infrastruttura senza sostenere i costi operativi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-334">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="e9c96-335">Per distribuire le macchine virtuali, aumentare la "capacità" del set di scalabilità di macchine virtuali fino al numero di istanze di produzione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-335">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="e9c96-336">È possibile creare un set di scalabilità di macchine virtuali con meno di due VM anche se si è interessati principalmente all'uso di un set di disponibilità con VM discrete, invece che alla disponibilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="e9c96-337">I set di scalabilità di macchine virtuali consentono di usare unità di calcolo non differenziate e fungibili.</span><span class="sxs-lookup"><span data-stu-id="e9c96-337">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="e9c96-338">Questa uniformità è un elemento di differenziazione chiave tra set di scalabilità di macchine virtuali e set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="e9c96-339">Molti carichi di lavoro senza stato non tengono traccia delle singole unità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="e9c96-340">In caso di riduzione del carico di lavoro, è possibile passare a una sola unità di calcolo e quindi aumentare il numero di unità con l'aumento del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e9c96-340">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-341">Come si cambia il numero di VM in un set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-341">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-342">Per cambiare il numero di VM in un set di scalabilità di macchine virtuali, vedere [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/) (Cambiare il numero di istanze di un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="e9c96-342">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="e9c96-343">Come è possibile definire avvisi personalizzati per il raggiungimento di determinate soglie?</span><span class="sxs-lookup"><span data-stu-id="e9c96-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="e9c96-344">La gestione degli avvisi per le soglie specificate offre una certa flessibilità.</span><span class="sxs-lookup"><span data-stu-id="e9c96-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="e9c96-345">È ad esempio possibile definire webhook personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e9c96-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="e9c96-346">L'esempio di webhook seguente è tratto da un modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e9c96-346">The following webhook example is from a Resource Manager template:</span></span>

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

<span data-ttu-id="e9c96-347">In questo esempio viene inviato un avviso a Pagerduty.com al raggiungimento di una soglia.</span><span class="sxs-lookup"><span data-stu-id="e9c96-347">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="e9c96-348">Applicazione di patch e operazioni</span><span class="sxs-lookup"><span data-stu-id="e9c96-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="e9c96-349">Come si crea un set di scalabilità in un gruppo di risorse esistente?</span><span class="sxs-lookup"><span data-stu-id="e9c96-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="e9c96-350">La creazione di set di scalabilità in un gruppo di risorse esistente non è ancora possibile dal portale di Azure, ma è possibile specificare un gruppo di risorse esistente quando si distribuisce un set di scalabilità da un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c96-350">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="e9c96-351">È anche possibile specificare un gruppo di risorse esistente durante la creazione di un set di scalabilità usando Azure PowerShell o l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="e9c96-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="e9c96-352">È possibile spostare un set di scalabilità in un altro gruppo di risorse?</span><span class="sxs-lookup"><span data-stu-id="e9c96-352">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="e9c96-353">Sì, è possibile spostare le risorse di un set di scalabilità in una nuova sottoscrizione o in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9c96-353">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="e9c96-354">Come si aggiorna il set di scalabilità di macchine virtuali a una nuova immagine?</span><span class="sxs-lookup"><span data-stu-id="e9c96-354">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="e9c96-355">Come si gestisce l'applicazione di patch?</span><span class="sxs-lookup"><span data-stu-id="e9c96-355">How do I manage patching?</span></span>

<span data-ttu-id="e9c96-356">Per aggiornare il set di scalabilità di macchine virtuali a una nuova immagine e gestire l'applicazione di patch, vedere [Aggiornare un set di scalabilità di macchine virtuali](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="e9c96-356">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="e9c96-357">È possibile usare l'operazione di ricreazione dell'immagine per ripristinare una macchina virtuale senza modificare l'immagine,</span><span class="sxs-lookup"><span data-stu-id="e9c96-357">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="e9c96-358">ovvero ripristinare le impostazioni predefinite di una VM invece di usare una nuova immagine?</span><span class="sxs-lookup"><span data-stu-id="e9c96-358">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="e9c96-359">Sì, è possibile usare l'operazione di ricreazione dell'immagine per ripristinare una macchina virtuale senza modificare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="e9c96-359">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="e9c96-360">Se tuttavia il set di scalabilità di macchine virtuali fa riferimento a un'immagine di piattaforma con `version = latest`, la macchina virtuale può essere aggiornata a un'immagine del sistema operativo successiva quando si chiama `reimage`.</span><span class="sxs-lookup"><span data-stu-id="e9c96-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="e9c96-361">Per altre informazioni, vedere [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set) (Gestire tutte le VM in un set di scalabilità di macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="e9c96-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="e9c96-362">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e9c96-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="e9c96-363">Come si attiva la diagnostica di avvio?</span><span class="sxs-lookup"><span data-stu-id="e9c96-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="e9c96-364">Per attivare la diagnostica di avvio, creare prima di tutto un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-364">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="e9c96-365">Inserire quindi il blocco JSON nella proprietà **virtualMachineProfile** set di scalabilità di macchine virtuali, quindi aggiornare il JSON:</span><span class="sxs-lookup"><span data-stu-id="e9c96-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="e9c96-366">Quando viene creata una nuova VM, la proprietà InstanceView della VM mostra i dettagli per lo screenshot e così via.</span><span class="sxs-lookup"><span data-stu-id="e9c96-366">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="e9c96-367">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e9c96-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="e9c96-368">Proprietà della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e9c96-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-369">Come si possono ottenere informazioni sulle proprietà di ogni macchina virtuale senza dover eseguire più chiamate?</span><span class="sxs-lookup"><span data-stu-id="e9c96-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="e9c96-370">Come si ottiene ad esempio il dominio di errore per ognuna delle 100 VM del set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-370">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-371">Per ottenere informazioni sulle proprietà per ogni macchina virtuale senza eseguire più chiamate, è possibile chiamare `ListVMInstanceViews` tramite un'operazione `GET` dell'API REST nell'URI di risorsa seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c96-371">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="e9c96-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="e9c96-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="e9c96-373">È possibile passare argomenti di estensione diversi a diverse VM in un set di scalabilità di macchine virtuali?</span><span class="sxs-lookup"><span data-stu-id="e9c96-373">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="e9c96-374">No, non è possibile passare argomenti di estensione diversi a diverse VM in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-374">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="e9c96-375">Le estensioni possono tuttavia funzionare in base alle proprietà univoche della macchina virtuale sulla quale sono in esecuzione, ad esempio il nome della macchina.</span><span class="sxs-lookup"><span data-stu-id="e9c96-375">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="e9c96-376">Le estensioni possono anche eseguire query sui metadati delle istanze in http://169.254.169.254 per ottenere altre informazioni sulla VM.</span><span class="sxs-lookup"><span data-stu-id="e9c96-376">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="e9c96-377">Perché sono presenti gap tra i nomi delle macchine virtuali del set di scalabilità di macchine virtuali e gli ID,</span><span class="sxs-lookup"><span data-stu-id="e9c96-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="e9c96-378">ad esempio 0, 1, 3?</span><span class="sxs-lookup"><span data-stu-id="e9c96-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="e9c96-379">Sono presenti gap tra i nomi delle macchine virtuali del set di scalabilità di macchine virtuali e gli ID delle VM perché la proprietà **overprovision** del set di scalabilità di macchine virtuali è impostata sul valore predefinito **true**.</span><span class="sxs-lookup"><span data-stu-id="e9c96-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="e9c96-380">Se la proprietà overprovision è impostata su **true**, viene creato un numero di VM superiore al necessario.</span><span class="sxs-lookup"><span data-stu-id="e9c96-380">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="e9c96-381">Le VM aggiuntive vengono quindi eliminate.</span><span class="sxs-lookup"><span data-stu-id="e9c96-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="e9c96-382">In questo caso si ottiene una maggiore affidabilità per la distribuzione, a scapito tuttavia delle regole di contiguità di denominazione e di NAT (Network Address Translation).</span><span class="sxs-lookup"><span data-stu-id="e9c96-382">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="e9c96-383">È possibile impostare questa proprietà su **false**.</span><span class="sxs-lookup"><span data-stu-id="e9c96-383">You can set this property to **false**.</span></span> <span data-ttu-id="e9c96-384">Per i set di scalabilità di macchine virtuali di piccole dimensioni ciò non influisce significativamente sull'affidabilità della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="e9c96-385">Qual è la differenza tra l'eliminazione di una VM in un set di scalabilità di macchine virtuali e la deallocazione della VM?</span><span class="sxs-lookup"><span data-stu-id="e9c96-385">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="e9c96-386">Quando scegliere l'una o l'altra?</span><span class="sxs-lookup"><span data-stu-id="e9c96-386">When should I choose one over the other?</span></span>

<span data-ttu-id="e9c96-387">La differenza principale tra l'eliminazione di una VM in un set di scalabilità di macchine virtuali e la deallocazione della VM consiste nel fatto che `deallocate` non elimina i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-387">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="e9c96-388">L'esecuzione di `stop deallocate` comporta costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e9c96-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="e9c96-389">È possibile usare una delle due opzioni per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e9c96-389">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="e9c96-390">Non si vogliono più sostenere i costi dei servizi di calcolo, mantenendo tuttavia lo stato dei dischi delle VM.</span><span class="sxs-lookup"><span data-stu-id="e9c96-390">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="e9c96-391">Si vuole avviare un set di VM con una velocità maggiore rispetto all'aumento del numero di istanze di un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e9c96-391">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="e9c96-392">In relazione a questo scenario è stato creato un motore di ridimensionamento automatico proprio e si vuole ottenere una scalabilità end-to-end più rapida.</span><span class="sxs-lookup"><span data-stu-id="e9c96-392">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="e9c96-393">È presente un set di scalabilità di macchine virtuali distribuito in modo non uniforme nei domini di errore o nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e9c96-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="e9c96-394">Questo problema può essere stato causato dall'eliminazione selettiva di VM o dall'eliminazione di VM dopo l'overprovisioning.</span><span class="sxs-lookup"><span data-stu-id="e9c96-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="e9c96-395">L'esecuzione di `stop deallocate` seguito da `start` nel set di scalabilità di macchine virtuali consente di distribuire uniformemente le VM nei domini di errore o nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e9c96-395">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

