---
title: DNS inverso per i servizi di Azure | Microsoft Docs
description: Informazioni su come configurare ricerche DNS inverse per i servizi ospitati in Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="93308-103">Configurare il DNS inverso per i servizi ospitati in Azure</span><span class="sxs-lookup"><span data-stu-id="93308-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="93308-104">Questo articolo illustra come configurare ricerche DNS inverse per i servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="93308-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="93308-105">I servizi in Azure usano gli indirizzi IP assegnati da Azure e di proprietà di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93308-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="93308-106">Questi record DNS inversi (record PTR) devono essere creati nelle zone di ricerca DNS inversa corrispondenti di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93308-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="93308-107">Questo articolo illustra come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="93308-107">This article explains how to do this.</span></span>

<span data-ttu-id="93308-108">Questo scenario non deve essere confuso con la possibilità di [eseguire l'hosting di zone di ricerca DNS inversa per gli intervalli di indirizzi IP assegnati in DNS Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="93308-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="93308-109">In questo caso, gli intervalli di indirizzi IP rappresentati dalle zone di ricerca inversa devono essere assegnati all'organizzazione, in genere dal provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="93308-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="93308-110">Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93308-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="93308-111">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="93308-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="93308-112">Nel modello di distribuzione di Resource Manager, le risorse di calcolo, ad esempio macchine virtuali, set di scalabilità di macchine virtuali o cluster di Service Fabric, vengono esposte tramite una risorsa PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="93308-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="93308-113">Le ricerche DNS inverse vengono configurate usando la proprietà 'ReverseFqdn' di PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="93308-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="93308-114">Nel modello di distribuzione classica, le risorse di calcolo vengono esposte tramite i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="93308-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="93308-115">Le ricerche DNS inverse vengono configurate usando la proprietà 'ReverseDnsFqdn' del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="93308-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="93308-116">Il DNS inverso non è attualmente supportato per il servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="93308-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="93308-117">Convalida dei record DNS inversi</span><span class="sxs-lookup"><span data-stu-id="93308-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="93308-118">Le terze parti non devono poter creare record DNS inversi per il mapping di servizi di Azure nei domini DNS dell'utente.</span><span class="sxs-lookup"><span data-stu-id="93308-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="93308-119">Per evitare che questo accada, Azure consente di creare un record DNS inverso solo quando il nome di dominio specificato nel record DNS inverso è identico a, o si risolve con, il nome DNS o l'indirizzo IP di un PublicIpAddress o di un servizio cloud nella stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="93308-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="93308-120">Questa convalida viene eseguita solo quando il record DNS inverso viene impostato o modificato.</span><span class="sxs-lookup"><span data-stu-id="93308-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="93308-121">La convalida non viene ripetuta periodicamente.</span><span class="sxs-lookup"><span data-stu-id="93308-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="93308-122">Si supponga ad esempio che la risorsa PublicIpAddress abbia il nome DNS contosoapp1.northus.cloudapp.azure.com e l'indirizzo IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="93308-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="93308-123">La proprietà ReverseFqdn per PublicIpAddress può essere specificata come segue:</span><span class="sxs-lookup"><span data-stu-id="93308-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="93308-124">Il nome DNS di PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="93308-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="93308-125">Il nome DNS di un PublicIpAddress diverso nella stessa sottoscrizione, ad esempio contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="93308-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="93308-126">Un nome DNS personale, ad esempio app1.contoso.com, purché questo nome sia *prima* configurato come record CNAME per contosoapp1.northus.cloudapp.azure.com o per un PublicIpAddress diverso nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93308-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="93308-127">Un nome DNS personale, ad esempio app1.contoso.com, purché questo nome sia *prima* configurato come record A per l'indirizzo IP 23.96.52.53 o per l'indirizzo IP di un PublicIpAddress diverso nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93308-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="93308-128">Gli stessi vincoli si applicano al DNS inverso per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="93308-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="93308-129">DNS inverso per le risorse PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="93308-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="93308-130">Questa sezione offre istruzioni dettagliate sulla configurazione del DNS inverso per risorse PublicIpAddress nel modello di distribuzione di Resource Manager tramite Azure PowerShell, l'interfaccia della riga di comando di Azure 1.0 o l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="93308-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="93308-131">La configurazione del DNS inverso per le risorse PublicIpAddress non è attualmente supportata dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="93308-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="93308-132">Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4.</span><span class="sxs-lookup"><span data-stu-id="93308-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="93308-133">Non è supportato per IPv6.</span><span class="sxs-lookup"><span data-stu-id="93308-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="93308-134">Aggiungere il DNS inverso a un PublicIpAddress esistente</span><span class="sxs-lookup"><span data-stu-id="93308-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="93308-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93308-135">PowerShell</span></span>

<span data-ttu-id="93308-136">Per aggiungere il DNS inverso a un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="93308-137">Per aggiungere il DNS inverso a un PublicIpAddress esistente che non ha già un nome DNS è necessario specificare anche un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="93308-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="93308-138">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="93308-138">Azure CLI 1.0</span></span>

<span data-ttu-id="93308-139">Per aggiungere il DNS inverso a un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="93308-140">Per aggiungere il DNS inverso a un PublicIpAddress esistente che non ha già un nome DNS è necessario specificare anche un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="93308-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="93308-141">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93308-141">Azure CLI 2.0</span></span>

<span data-ttu-id="93308-142">Per aggiungere il DNS inverso a un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="93308-143">Per aggiungere il DNS inverso a un PublicIpAddress esistente che non ha già un nome DNS è necessario specificare anche un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="93308-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="93308-144">Creare un indirizzo IP pubblico con il DNS inverso</span><span class="sxs-lookup"><span data-stu-id="93308-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="93308-145">Per creare un nuovo PublicIpAddress con la proprietà di DNS inverso già specificata:</span><span class="sxs-lookup"><span data-stu-id="93308-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="93308-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93308-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="93308-147">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="93308-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="93308-148">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93308-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="93308-149">Visualizzare il DNS inverso di un PublicIpAddress esistente</span><span class="sxs-lookup"><span data-stu-id="93308-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="93308-150">Per visualizzare il valore configurato per un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="93308-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93308-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="93308-152">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="93308-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="93308-153">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93308-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="93308-154">Rimuovere il DNS inverso da indirizzi IP pubblici esistenti</span><span class="sxs-lookup"><span data-stu-id="93308-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="93308-155">Per rimuovere una proprietà di DNS inverso da un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="93308-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93308-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="93308-157">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="93308-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="93308-158">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93308-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="93308-159">Configurare il DNS inverso per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="93308-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="93308-160">Questa sezione offre istruzioni dettagliate sulla configurazione del DNS inverso per i servizi cloud nel modello di distribuzione classica tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93308-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="93308-161">La configurazione del DNS inverso per i servizi cloud non è supportata nel portale di Azure, nell'interfaccia della riga di comando di Azure 1.0 e nell'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="93308-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="93308-162">Aggiungere il DNS inverso ai servizi cloud esistenti</span><span class="sxs-lookup"><span data-stu-id="93308-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="93308-163">Per aggiungere un record DNS inverso a un servizio cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="93308-164">Creare un servizio cloud con il DNS inverso</span><span class="sxs-lookup"><span data-stu-id="93308-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="93308-165">Per creare un nuovo servizio cloud con la proprietà di DNS inverso già specificata:</span><span class="sxs-lookup"><span data-stu-id="93308-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="93308-166">Visualizzare il DNS inverso per i servizi cloud esistenti</span><span class="sxs-lookup"><span data-stu-id="93308-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="93308-167">Per visualizzare la proprietà di DNS inverso per un servizio cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="93308-168">Rimuovere il DNS inverso dai servizi cloud esistenti</span><span class="sxs-lookup"><span data-stu-id="93308-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="93308-169">Per rimuovere una proprietà di DNS inverso da un servizio cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="93308-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="93308-170">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="93308-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="93308-171">Quanto costano i record DNS inversi?</span><span class="sxs-lookup"><span data-stu-id="93308-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="93308-172">Sono gratuiti.</span><span class="sxs-lookup"><span data-stu-id="93308-172">They're free!</span></span>  <span data-ttu-id="93308-173">Non sono previsti costi aggiuntivi per i record DNS inversi o le query.</span><span class="sxs-lookup"><span data-stu-id="93308-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="93308-174">I record DNS inversi verranno risolti da Internet?</span><span class="sxs-lookup"><span data-stu-id="93308-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="93308-175">Sì.</span><span class="sxs-lookup"><span data-stu-id="93308-175">Yes.</span></span> <span data-ttu-id="93308-176">Dopo aver impostato la proprietà di DNS inverso per il servizio di Azure, Azure gestisce tutte le deleghe DNS e le zone DNS necessarie per assicurare che il record di DNS inverso si risolva per tutti gli utenti di Internet.</span><span class="sxs-lookup"><span data-stu-id="93308-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="93308-177">Vengono creati record DNS inversi per i servizi di Azure?</span><span class="sxs-lookup"><span data-stu-id="93308-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="93308-178">No.</span><span class="sxs-lookup"><span data-stu-id="93308-178">No.</span></span> <span data-ttu-id="93308-179">Il DNS inverso sarà una funzionalità che prevede il consenso esplicito.</span><span class="sxs-lookup"><span data-stu-id="93308-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="93308-180">Se si sceglie di non configurare alcun record DNS inverso predefinito, non ne verrà creato alcuno.</span><span class="sxs-lookup"><span data-stu-id="93308-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="93308-181">Qual è il formato per il nome di dominio completo (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="93308-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="93308-182">I nomi di dominio completi vengono specificati in ordine progressivo e devono terminare con un punto, ad esempio "app1.contoso.com.".</span><span class="sxs-lookup"><span data-stu-id="93308-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="93308-183">Cosa accade se i controlli di convalida per il DNS inverso specificati danno esito negativo?</span><span class="sxs-lookup"><span data-stu-id="93308-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="93308-184">Se il controllo di convalida per il DNS dà esito negativo, la configurazione del record DNS inverso non riesce.</span><span class="sxs-lookup"><span data-stu-id="93308-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="93308-185">Correggere il valore DNS inverso e riprovare.</span><span class="sxs-lookup"><span data-stu-id="93308-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="93308-186">È possibile configurare il DNS inverso per il servizio app di Azure?</span><span class="sxs-lookup"><span data-stu-id="93308-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="93308-187">No.</span><span class="sxs-lookup"><span data-stu-id="93308-187">No.</span></span> <span data-ttu-id="93308-188">Il DNS inverso non è supportato per il servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="93308-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="93308-189">È possibile configurare più record DNS inversi per il servizio di Azure?</span><span class="sxs-lookup"><span data-stu-id="93308-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="93308-190">No.</span><span class="sxs-lookup"><span data-stu-id="93308-190">No.</span></span> <span data-ttu-id="93308-191">Azure supporta un solo record DNS inverso per ogni servizio cloud di Azure o PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="93308-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="93308-192">È possibile configurare il DNS inverso per le risorse PublicIpAddress IPv6?</span><span class="sxs-lookup"><span data-stu-id="93308-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="93308-193">No.</span><span class="sxs-lookup"><span data-stu-id="93308-193">No.</span></span> <span data-ttu-id="93308-194">Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4 e i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="93308-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="93308-195">È possibile inviare messaggi di posta elettronica a domini esterni dai servizi di calcolo di Azure?</span><span class="sxs-lookup"><span data-stu-id="93308-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="93308-196">No.</span><span class="sxs-lookup"><span data-stu-id="93308-196">No.</span></span> [<span data-ttu-id="93308-197">I servizi di calcolo di Azure non supportano l'invio di messaggi di posta elettronica a domini esterni</span><span class="sxs-lookup"><span data-stu-id="93308-197">Azure Compute services do not support sending emails to external domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="93308-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93308-198">Next steps</span></span>

<span data-ttu-id="93308-199">Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="93308-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="93308-200">Informazioni su come eseguire l'[hosting della zona di ricerca inversa per l'intervallo di indirizzi IP assegnato dal provider di servizi Internet in DNS Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="93308-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

