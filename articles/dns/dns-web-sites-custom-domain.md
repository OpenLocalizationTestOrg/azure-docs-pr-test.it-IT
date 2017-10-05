---
title: Creare record DNS personalizzati per un'app Web | Documentazione Microsoft
description: Come creare record DNS di un dominio personalizzato per un'app Web usando DNS di Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="2fd08-103">Creare record DNS per un'app Web in un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="2fd08-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="2fd08-104">È possibile usare DNS di Azure per ospitare un dominio personalizzato per le app Web.</span><span class="sxs-lookup"><span data-stu-id="2fd08-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="2fd08-105">Se, ad esempio, si crea un'app Web di Azure e si vuole che gli utenti vi accedano usando contoso.com o www.contoso.com come FQDN.</span><span class="sxs-lookup"><span data-stu-id="2fd08-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="2fd08-106">A tale scopo, è necessario creare due record:</span><span class="sxs-lookup"><span data-stu-id="2fd08-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="2fd08-107">Un record radice "A" che fa riferimento a contoso.com</span><span class="sxs-lookup"><span data-stu-id="2fd08-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="2fd08-108">Un record "CNAME" per il nome www che punta al record A</span><span class="sxs-lookup"><span data-stu-id="2fd08-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="2fd08-109">Tenere presente che, se si crea un record A per un'app Web in Azure, il record A deve essere aggiornato manualmente se l'indirizzo IP sottostante per l'app Web cambia.</span><span class="sxs-lookup"><span data-stu-id="2fd08-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2fd08-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2fd08-110">Before you begin</span></span>

<span data-ttu-id="2fd08-111">Prima di iniziare, è necessario innanzitutto creare una zona DNS in DNS di Azure e delegare la zona nel registrar a DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd08-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="2fd08-112">Per creare una zona DNS, seguire i passaggi in [Creare una zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="2fd08-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="2fd08-113">Per delegare il DNS a DNS di Azure, seguire i passaggi nell'articolo relativo alla [delega del dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2fd08-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="2fd08-114">Dopo la creazione di una zona e la relativa delega a DNS di Azure, è quindi possibile creare record per il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2fd08-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="2fd08-115">1. Creare un record A per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="2fd08-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="2fd08-116">Un record A viene usato per eseguire il mapping di un nome al relativo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2fd08-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="2fd08-117">Nell'esempio seguente si assegnerà @ come record A a un indirizzo IPv4:</span><span class="sxs-lookup"><span data-stu-id="2fd08-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="2fd08-118">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2fd08-118">Step 1</span></span>

<span data-ttu-id="2fd08-119">Creare un record A e assegnarlo a una variabile $rs</span><span class="sxs-lookup"><span data-stu-id="2fd08-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="2fd08-120">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2fd08-120">Step 2</span></span>

<span data-ttu-id="2fd08-121">Aggiungere al set di record "@" creato in precedenza il valore IPv4 usando la variabile $rs assegnata.</span><span class="sxs-lookup"><span data-stu-id="2fd08-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="2fd08-122">Il valore di IPv4 assegnato sarà l'indirizzo IP per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="2fd08-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="2fd08-123">Per trovare l'indirizzo IP per un'app Web, seguire i passaggi in [Configurare un nome di dominio personalizzato nel servizio app di Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="2fd08-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="2fd08-124">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2fd08-124">Step 3</span></span>

<span data-ttu-id="2fd08-125">Eseguire il commit delle modifiche al set di record.</span><span class="sxs-lookup"><span data-stu-id="2fd08-125">Commit the changes to the record set.</span></span> <span data-ttu-id="2fd08-126">Usare `Set-AzureRMDnsRecordSet` per caricare le modifiche al set di record in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd08-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="2fd08-127">2. Creare un record CNAME per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="2fd08-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="2fd08-128">Se il dominio è già gestito da DNS di Azure (vedere la [delega del dominio DNS](dns-domain-delegation.md)), è possibile usare l'esempio seguente per creare un record CNAME per contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="2fd08-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="2fd08-129">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2fd08-129">Step 1</span></span>

<span data-ttu-id="2fd08-130">Aprire PowerShell, creare un nuovo set di record CNAME e assegnarlo a una variabile $rs.</span><span class="sxs-lookup"><span data-stu-id="2fd08-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="2fd08-131">In questo esempio viene creato un tipo di set di record CNAME con una "durata (TTL)" di 600 secondi nella zona DNS denominata "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="2fd08-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="2fd08-132">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="2fd08-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="2fd08-133">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2fd08-133">Step 2</span></span>

<span data-ttu-id="2fd08-134">Una volta creato il set di record CNAME, è necessario creare un valore alias che farà riferimento all'app Web</span><span class="sxs-lookup"><span data-stu-id="2fd08-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="2fd08-135">Usando la variabile "$rs" assegnata in precedenza, è possibile usare il seguente comando di PowerShell per creare l'alias per l'app Web contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="2fd08-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="2fd08-136">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="2fd08-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="2fd08-137">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2fd08-137">Step 3</span></span>

<span data-ttu-id="2fd08-138">Confermare le modifiche usando il cmdlet `Set-AzureRMDnsRecordSet` :</span><span class="sxs-lookup"><span data-stu-id="2fd08-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="2fd08-139">È possibile verificare che il record sia stato creato correttamente eseguendo una query di "www.contoso.com" con nslookup, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2fd08-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="2fd08-140">Creare un record "awverify" per le app Web</span><span class="sxs-lookup"><span data-stu-id="2fd08-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="2fd08-141">Se si decide di usare un record A per l'app Web, è necessario eseguire un processo di verifica per assicurarsi che il dominio personalizzato sia di proprietà dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2fd08-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="2fd08-142">Questo passaggio di verifica viene eseguito creando uno speciale record CNAME denominato "awverify".</span><span class="sxs-lookup"><span data-stu-id="2fd08-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="2fd08-143">Questa sezione si applica solo ai record A.</span><span class="sxs-lookup"><span data-stu-id="2fd08-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="2fd08-144">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2fd08-144">Step 1</span></span>

<span data-ttu-id="2fd08-145">Creare il record "awverify".</span><span class="sxs-lookup"><span data-stu-id="2fd08-145">Create the "awverify" record.</span></span> <span data-ttu-id="2fd08-146">In questo esempio verrà creato il record "awverify" per consentire a contoso.com di verificare la proprietà del dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2fd08-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="2fd08-147">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="2fd08-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="2fd08-148">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2fd08-148">Step 2</span></span>

<span data-ttu-id="2fd08-149">Dopo aver creato il set di record "awverify", assegnare l'alias del set di record CNAME.</span><span class="sxs-lookup"><span data-stu-id="2fd08-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="2fd08-150">Nell'esempio seguente, si assegnerà l'alias del set di record CNAME a awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="2fd08-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="2fd08-151">L'esempio seguente corrisponde alla risposta.</span><span class="sxs-lookup"><span data-stu-id="2fd08-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="2fd08-152">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="2fd08-152">Step 3</span></span>

<span data-ttu-id="2fd08-153">Eseguire il commit delle modifiche usando `Set-AzureRMDnsRecordSet cmdlet`, come mostrato nel comando seguente.</span><span class="sxs-lookup"><span data-stu-id="2fd08-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="2fd08-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fd08-154">Next steps</span></span>

<span data-ttu-id="2fd08-155">Per configurare l'app Web per l'uso di un dominio personalizzato, seguire i passaggi in [Configurazione di un nome di dominio personalizzato nel servizio app](../app-service-web/web-sites-custom-domain-name.md) .</span><span class="sxs-lookup"><span data-stu-id="2fd08-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
