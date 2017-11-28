---
title: aaaReverse DNS per servizi di Azure | Documenti Microsoft
description: Informazioni su come tooconfigure DNS inverse per i servizi ospitati in Azure
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="bd9ad-103">Configurare il DNS inverso per i servizi ospitati in Azure</span><span class="sxs-lookup"><span data-stu-id="bd9ad-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="bd9ad-104">Questo articolo spiega come tooconfigure DNS inverse per i servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="bd9ad-105">I servizi in Azure usano gli indirizzi IP assegnati da Azure e di proprietà di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="bd9ad-106">Questi record DNS inversi (record PTR) devono essere creati in hello corrispondente proprietà Microsoft ricerca le zone DNS inverse.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="bd9ad-107">Questo articolo viene illustrato come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-107">This article explains how toodo this.</span></span>

<span data-ttu-id="bd9ad-108">Questo scenario non deve essere confuso con il possibilità hello troppo[host hello inverse zone di ricerca DNS per gli intervalli IP assegnati in Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ad-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="bd9ad-109">In questo caso, gli intervalli IP hello rappresentati da una zona di ricerca inversa hello devono essere assegnati tooyour organizzazione, in genere dal provider.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="bd9ad-110">Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ad-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="bd9ad-111">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ad-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="bd9ad-112">Nel modello di distribuzione di gestione risorse hello, le risorse di calcolo (ad esempio macchine virtuali, i set di scalabilità di macchine virtuali o i cluster di Service Fabric) vengono esposti tramite una risorsa PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="bd9ad-113">Funzione di ricerca inverse DNS vengono configurate tramite proprietà 'ReverseFqdn' hello di hello PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="bd9ad-114">Nel modello di distribuzione classica hello, le risorse di calcolo vengono esposte utilizzando i servizi Cloud.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="bd9ad-115">Funzione di ricerca inverse DNS vengono configurate tramite proprietà 'ReverseDnsFqdn' hello di hello servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="bd9ad-116">DNS inversa non è attualmente supportato per hello servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="bd9ad-117">Convalida dei record DNS inversi</span><span class="sxs-lookup"><span data-stu-id="bd9ad-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="bd9ad-118">Una terza parte non deve essere in grado di toocreate i record DNS inversi nei domini DNS tooyour mapping servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="bd9ad-119">tooprevent, Azure consente solo di hello creare un record DNS inverso in cui il nome di dominio specificato nel record DNS inverso hello è hello identico o viene risolto, hello nome DNS o l'indirizzo IP di un PublicIpAddress o un Cloud servizio hello stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="bd9ad-120">Questa convalida viene eseguita solo quando il record DNS inverso di hello viene impostato o modificato.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="bd9ad-121">La convalida non viene ripetuta periodicamente.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="bd9ad-122">Ad esempio: si supponga che disponga di risorse PublicIpAddress hello contosoapp1.northus.cloudapp.azure.com nome DNS di hello e l'indirizzo IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="bd9ad-123">Hello ReverseFqdn per hello che publicipaddress può essere specificato come:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="bd9ad-124">nome DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd9ad-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="bd9ad-125">Hello ai nomi DNS per un PublicIpAddress diversi in hello stessa sottoscrizione, ad esempio contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd9ad-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="bd9ad-126">Un reindirizzamento a microsito nome DNS, ad esempio app1.contoso.com, purché questo nome è *prima* configurato come un record CNAME toocontosoapp1.northus.cloudapp.azure.com tooa PublicIpAddress diversi in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="bd9ad-127">Un reindirizzamento a microsito nome DNS, ad esempio app1.contoso.com, purché questo nome è *prima* configurato come un indirizzo IP di un record toohello 23.96.52.53, o toohello l'indirizzo IP di un PublicIpAddress diversi in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="bd9ad-128">Hello stessi vincoli si applicano tooreverse DNS per i servizi Cloud.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="bd9ad-129">DNS inverso per le risorse PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="bd9ad-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="bd9ad-130">In questa sezione vengono fornite istruzioni dettagliate per la modalità tooconfigure inversa DNS per le risorse PublicIpAddress nel modello di distribuzione di gestione risorse hello, tramite Azure PowerShell, Azure CLI 1.0 o 2.0 CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="bd9ad-131">Configurazione del DNS inverso per le risorse PublicIpAddress non è attualmente supportata tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="bd9ad-132">Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="bd9ad-133">Non è supportato per IPv6.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="bd9ad-134">Aggiungere inversa tooan DNS esistente PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="bd9ad-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="bd9ad-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd9ad-135">PowerShell</span></span>

<span data-ttu-id="bd9ad-136">tooadd inversa DNS tooan PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="bd9ad-137">tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="bd9ad-138">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-138">Azure CLI 1.0</span></span>

<span data-ttu-id="bd9ad-139">tooadd inversa DNS tooan PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="bd9ad-140">tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="bd9ad-141">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-141">Azure CLI 2.0</span></span>

<span data-ttu-id="bd9ad-142">tooadd inversa DNS tooan PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="bd9ad-143">tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="bd9ad-144">Creare un indirizzo IP pubblico con il DNS inverso</span><span class="sxs-lookup"><span data-stu-id="bd9ad-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="bd9ad-145">toocreate un PublicIpAddress di nuovo con proprietà DNS inverso hello già specificato:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="bd9ad-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd9ad-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="bd9ad-147">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="bd9ad-148">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="bd9ad-149">Visualizzare il DNS inverso di un PublicIpAddress esistente</span><span class="sxs-lookup"><span data-stu-id="bd9ad-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="bd9ad-150">valore tooview hello configurato per un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="bd9ad-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd9ad-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="bd9ad-152">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="bd9ad-153">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="bd9ad-154">Rimuovere il DNS inverso da indirizzi IP pubblici esistenti</span><span class="sxs-lookup"><span data-stu-id="bd9ad-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="bd9ad-155">tooremove una proprietà DNS inversa da un PublicIpAddress esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="bd9ad-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd9ad-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="bd9ad-157">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="bd9ad-158">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd9ad-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="bd9ad-159">Configurare il DNS inverso per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="bd9ad-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="bd9ad-160">In questa sezione vengono fornite istruzioni dettagliate per la modalità tooconfigure inversa DNS per i servizi Cloud nel modello di distribuzione classica hello, tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="bd9ad-161">Configurazione del DNS inversa per i servizi Cloud non è supportata tramite il portale di Azure, hello Azure CLI 1.0 o 2.0 CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="bd9ad-162">Aggiungere servizi di Cloud tooexisting DNS inversa</span><span class="sxs-lookup"><span data-stu-id="bd9ad-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="bd9ad-163">tooadd un tooan di record DNS inverso servizio Cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="bd9ad-164">Creare un servizio cloud con il DNS inverso</span><span class="sxs-lookup"><span data-stu-id="bd9ad-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="bd9ad-165">toocreate un nuovo servizio Cloud con proprietà DNS inversa hello già specificata:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="bd9ad-166">Visualizzare il DNS inverso per i servizi cloud esistenti</span><span class="sxs-lookup"><span data-stu-id="bd9ad-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="bd9ad-167">hello tooview inverso proprietà DNS per un servizio Cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="bd9ad-168">Rimuovere il DNS inverso dai servizi cloud esistenti</span><span class="sxs-lookup"><span data-stu-id="bd9ad-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="bd9ad-169">tooremove una proprietà DNS inversa da un servizio Cloud esistente:</span><span class="sxs-lookup"><span data-stu-id="bd9ad-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="bd9ad-170">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="bd9ad-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="bd9ad-171">Quanto costano i record DNS inversi?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="bd9ad-172">Sono gratuiti.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-172">They're free!</span></span>  <span data-ttu-id="bd9ad-173">Non sono previsti costi aggiuntivi per i record DNS inversi o le query.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="bd9ad-174">Sarà la risoluzione di record DNS inverso da hello internet?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="bd9ad-175">Sì.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-175">Yes.</span></span> <span data-ttu-id="bd9ad-176">Dopo aver impostato la proprietà DNS inversa hello per il servizio di Azure, Azure gestisce tutte le deleghe DNS di hello e zone DNS necessarie risolve tooensure che i record DNS inversa per tutti gli utenti di Internet.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="bd9ad-177">Vengono creati record DNS inversi per i servizi di Azure?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="bd9ad-178">No.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-178">No.</span></span> <span data-ttu-id="bd9ad-179">Il DNS inverso sarà una funzionalità che prevede il consenso esplicito.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="bd9ad-180">Nessuna impostazione predefinita vengono creati i record DNS inversi, se si sceglie di non tooconfigure li.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="bd9ad-181">Che cos'è il formato di hello per il nome di dominio completo (FQDN) di hello?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="bd9ad-182">I nomi di dominio completi vengono specificati in ordine progressivo e devono terminare con un punto, ad esempio "app1.contoso.com.".</span><span class="sxs-lookup"><span data-stu-id="bd9ad-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="bd9ad-183">Cosa accade se il controllo di convalida hello per hello inversa DNS è stato specificato ha esito negativo?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="bd9ad-184">Dove hello inversa DNS convalida ha esito negativo, hello operazione tooconfigure hello record DNS inverso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="bd9ad-185">Correggere hello inversa DNS valore come richiesto e riprovare.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="bd9ad-186">È possibile configurare il DNS inverso per il servizio app di Azure?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="bd9ad-187">No.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-187">No.</span></span> <span data-ttu-id="bd9ad-188">DNS inversa non è supportata per hello servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="bd9ad-189">È possibile configurare più record DNS inversi per il servizio di Azure?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="bd9ad-190">No.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-190">No.</span></span> <span data-ttu-id="bd9ad-191">Azure supporta un solo record DNS inverso per ogni servizio cloud di Azure o PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="bd9ad-192">È possibile configurare il DNS inverso per le risorse PublicIpAddress IPv6?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="bd9ad-193">No.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-193">No.</span></span> <span data-ttu-id="bd9ad-194">Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4 e i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="bd9ad-195">È possibile inviare messaggi di posta elettronica tooexternal domini dai servizi di calcolo di Azure?</span><span class="sxs-lookup"><span data-stu-id="bd9ad-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="bd9ad-196">No.</span><span class="sxs-lookup"><span data-stu-id="bd9ad-196">No.</span></span> [<span data-ttu-id="bd9ad-197">Servizi di calcolo di Azure non supportano l'invio messaggi di posta elettronica tooexternal domini</span><span class="sxs-lookup"><span data-stu-id="bd9ad-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="bd9ad-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd9ad-198">Next steps</span></span>

<span data-ttu-id="bd9ad-199">Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="bd9ad-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="bd9ad-200">Informazioni su come troppo[zona di ricerca inversa hello host per l'intervallo di IP assegnato dal provider di servizi Internet in Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="bd9ad-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

