---
title: aaaCreate i record DNS personalizzati per un'app web | Documenti Microsoft
description: Come toocreate DNS del dominio personalizzato registrato per l'app web con DNS di Azure.
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
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="86e13-103">Creare record DNS per un'app Web in un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="86e13-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="86e13-104">È possibile utilizzare toohost DNS di Azure un dominio personalizzato per le app web.</span><span class="sxs-lookup"><span data-stu-id="86e13-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="86e13-105">Ad esempio, si sta creando un'app web di Azure e si desidera il tooaccess gli utenti da uno tramite contoso.com o www.contoso.com come un nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="86e13-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="86e13-106">toodo, si dispone di due record toocreate:</span><span class="sxs-lookup"><span data-stu-id="86e13-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="86e13-107">Un toocontoso.com puntamento record radice "A"</span><span class="sxs-lookup"><span data-stu-id="86e13-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="86e13-108">Un "" record CNAME per nome www hello che punta toohello un record</span><span class="sxs-lookup"><span data-stu-id="86e13-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="86e13-109">Tenere presente che se si crea un record A per un'app web in Azure, un record deve essere aggiornato manualmente se hello hello sottostante indirizzo IP per le modifiche di hello web app.</span><span class="sxs-lookup"><span data-stu-id="86e13-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86e13-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="86e13-110">Before you begin</span></span>

<span data-ttu-id="86e13-111">Prima di iniziare, è innanzitutto necessario creare una zona DNS di DNS di Azure e delegare zona hello il tooAzure registrazione DNS.</span><span class="sxs-lookup"><span data-stu-id="86e13-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="86e13-112">toocreate una zona DNS, seguire i passaggi hello [creare una zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="86e13-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="86e13-113">toodelegate il tooAzure DNS DNS, seguire i passaggi hello [delega di dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="86e13-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="86e13-114">Dopo la creazione di una zona e delegarla tooAzure DNS, è quindi possibile creare record per il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="86e13-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="86e13-115">1. Creare un record A per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="86e13-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="86e13-116">Un record è toomap usato un indirizzo IP tooits di nome.</span><span class="sxs-lookup"><span data-stu-id="86e13-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="86e13-117">Nell'esempio seguente hello nella si assegnerà come un tooan di record di un indirizzo IPv4:</span><span class="sxs-lookup"><span data-stu-id="86e13-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="86e13-118">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="86e13-118">Step 1</span></span>

<span data-ttu-id="86e13-119">Creare un record A e assegnare tooa $rs variabile</span><span class="sxs-lookup"><span data-stu-id="86e13-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="86e13-120">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="86e13-120">Step 2</span></span>

<span data-ttu-id="86e13-121">Aggiungere i set di record di hello IPv4 valore toohello creato in precedenza "@" utilizzando hello $rs variabile assegnato.</span><span class="sxs-lookup"><span data-stu-id="86e13-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="86e13-122">Hello valore IPv4 assegnato sarà l'indirizzo IP hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="86e13-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="86e13-123">indirizzo IP di hello toofind per un'app web, seguire i passaggi hello [configurare un nome di dominio personalizzato in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="86e13-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="86e13-124">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="86e13-124">Step 3</span></span>

<span data-ttu-id="86e13-125">Eseguire il commit del set di record toohello modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="86e13-126">Utilizzare `Set-AzureRMDnsRecordSet` hello tooupload cambia toohello tooAzure di set di record DNS:</span><span class="sxs-lookup"><span data-stu-id="86e13-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="86e13-127">2. Creare un record CNAME per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="86e13-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="86e13-128">Se il dominio è già gestito dal servizio DNS di Azure (vedere [delega di dominio DNS](dns-domain-delegation.md), è possibile utilizzare i seguenti toocreate esempio hello un record CNAME per contoso.azurewebsites.net hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="86e13-129">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="86e13-129">Step 1</span></span>

<span data-ttu-id="86e13-130">Aprire PowerShell e creare un nuovo set di record CNAME e assegnare tooa $rs variabile.</span><span class="sxs-lookup"><span data-stu-id="86e13-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="86e13-131">Questo esempio viene creato un tipo di set di record CNAME con"toolive" 600 secondi nella zona DNS denominato "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="86e13-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="86e13-132">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="86e13-133">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="86e13-133">Step 2</span></span>

<span data-ttu-id="86e13-134">Una volta creato hello set di record CNAME, è necessario toocreate un valore alias a cui punterà toohello web app.</span><span class="sxs-lookup"><span data-stu-id="86e13-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="86e13-135">Utilizzando hello assegnate in precedenza la variabile "$rs" è possibile utilizzare il comando di PowerShell hello sotto alias hello toocreate per hello web app contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="86e13-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="86e13-136">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="86e13-137">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="86e13-137">Step 3</span></span>

<span data-ttu-id="86e13-138">Eseguire il commit delle modifiche di hello mediante hello `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86e13-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="86e13-139">È possibile convalidare il record di hello è stato creato correttamente eseguendo una query hello "www.contoso.com" con nslookup, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="86e13-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="86e13-140">Creare un record "awverify" per le app Web</span><span class="sxs-lookup"><span data-stu-id="86e13-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="86e13-141">Se si decide di toouse un record A per l'app web, è necessario passare attraverso un tooensure di processo di verifica è dominio personalizzato hello personalizzati.</span><span class="sxs-lookup"><span data-stu-id="86e13-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="86e13-142">Questo passaggio di verifica viene eseguito creando uno speciale record CNAME denominato "awverify".</span><span class="sxs-lookup"><span data-stu-id="86e13-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="86e13-143">Questa sezione si applica solo i record tooA.</span><span class="sxs-lookup"><span data-stu-id="86e13-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="86e13-144">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="86e13-144">Step 1</span></span>

<span data-ttu-id="86e13-145">Creare record "awverify" hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-145">Create hello "awverify" record.</span></span> <span data-ttu-id="86e13-146">Nell'esempio hello seguente verrà creata record "aweverify" hello per la proprietà tooverify contoso.com per il dominio personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="86e13-147">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="86e13-148">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="86e13-148">Step 2</span></span>

<span data-ttu-id="86e13-149">Una volta creato il set di record hello "awverify", assegnare record CNAME hello impostare alias.</span><span class="sxs-lookup"><span data-stu-id="86e13-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="86e13-150">Nell'esempio hello seguente, si assegnerà tooawverify.contoso.azurewebsites.net alias del set di record CNAMe di hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="86e13-151">Hello di esempio seguente è riportata la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="86e13-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="86e13-152">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="86e13-152">Step 3</span></span>

<span data-ttu-id="86e13-153">Eseguire il commit delle modifiche di hello mediante hello `Set-AzureRMDnsRecordSet cmdlet`, come illustrato nel comando hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="86e13-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="86e13-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86e13-154">Next steps</span></span>

<span data-ttu-id="86e13-155">Seguire i passaggi di hello in [configurazione di un nome di dominio personalizzato per il servizio App](../app-service-web/web-sites-custom-domain-name.md) tooconfigure il toouse app web un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="86e13-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
