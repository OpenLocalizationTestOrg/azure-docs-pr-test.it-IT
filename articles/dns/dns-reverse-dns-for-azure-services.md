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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Configurare il DNS inverso per i servizi ospitati in Azure

Questo articolo spiega come tooconfigure DNS inverse per i servizi ospitati in Azure.

I servizi in Azure usano gli indirizzi IP assegnati da Azure e di proprietà di Microsoft. Questi record DNS inversi (record PTR) devono essere creati in hello corrispondente proprietà Microsoft ricerca le zone DNS inverse. Questo articolo viene illustrato come toodo questo.

Questo scenario non deve essere confuso con il possibilità hello troppo[host hello inverse zone di ricerca DNS per gli intervalli IP assegnati in Azure DNS](dns-reverse-dns-hosting.md). In questo caso, gli intervalli IP hello rappresentati da una zona di ricerca inversa hello devono essere assegnati tooyour organizzazione, in genere dal provider.

Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).

Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).
* Nel modello di distribuzione di gestione risorse hello, le risorse di calcolo (ad esempio macchine virtuali, i set di scalabilità di macchine virtuali o i cluster di Service Fabric) vengono esposti tramite una risorsa PublicIpAddress. Funzione di ricerca inverse DNS vengono configurate tramite proprietà 'ReverseFqdn' hello di hello PublicIpAddress.
* Nel modello di distribuzione classica hello, le risorse di calcolo vengono esposte utilizzando i servizi Cloud. Funzione di ricerca inverse DNS vengono configurate tramite proprietà 'ReverseDnsFqdn' hello di hello servizio Cloud.

DNS inversa non è attualmente supportato per hello servizio App di Azure.

## <a name="validation-of-reverse-dns-records"></a>Convalida dei record DNS inversi

Una terza parte non deve essere in grado di toocreate i record DNS inversi nei domini DNS tooyour mapping servizio di Azure. tooprevent, Azure consente solo di hello creare un record DNS inverso in cui il nome di dominio specificato nel record DNS inverso hello è hello identico o viene risolto, hello nome DNS o l'indirizzo IP di un PublicIpAddress o un Cloud servizio hello stessa sottoscrizione di Azure.

Questa convalida viene eseguita solo quando il record DNS inverso di hello viene impostato o modificato. La convalida non viene ripetuta periodicamente.

Ad esempio: si supponga che disponga di risorse PublicIpAddress hello contosoapp1.northus.cloudapp.azure.com nome DNS di hello e l'indirizzo IP 23.96.52.53. Hello ReverseFqdn per hello che publicipaddress può essere specificato come:
* nome DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Hello ai nomi DNS per un PublicIpAddress diversi in hello stessa sottoscrizione, ad esempio contosoapp2.westus.cloudapp.azure.com
* Un reindirizzamento a microsito nome DNS, ad esempio app1.contoso.com, purché questo nome è *prima* configurato come un record CNAME toocontosoapp1.northus.cloudapp.azure.com tooa PublicIpAddress diversi in hello stessa sottoscrizione.
* Un reindirizzamento a microsito nome DNS, ad esempio app1.contoso.com, purché questo nome è *prima* configurato come un indirizzo IP di un record toohello 23.96.52.53, o toohello l'indirizzo IP di un PublicIpAddress diversi in hello stessa sottoscrizione.

Hello stessi vincoli si applicano tooreverse DNS per i servizi Cloud.


## <a name="reverse-dns-for-publicipaddress-resources"></a>DNS inverso per le risorse PublicIpAddress

In questa sezione vengono fornite istruzioni dettagliate per la modalità tooconfigure inversa DNS per le risorse PublicIpAddress nel modello di distribuzione di gestione risorse hello, tramite Azure PowerShell, Azure CLI 1.0 o 2.0 CLI di Azure. Configurazione del DNS inverso per le risorse PublicIpAddress non è attualmente supportata tramite hello portale di Azure.

Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4. Non è supportato per IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Aggiungere inversa tooan DNS esistente PublicIpAddresses

#### <a name="powershell"></a>PowerShell

tooadd inversa DNS tooan PublicIpAddress esistente:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

tooadd inversa DNS tooan PublicIpAddress esistente:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

tooadd inversa DNS tooan PublicIpAddress esistente:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd inversa DNS tooan PublicIpAddress che non dispone già di un nome DNS esistente, è inoltre necessario specificare un nome DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Creare un indirizzo IP pubblico con il DNS inverso

toocreate un PublicIpAddress di nuovo con proprietà DNS inverso hello già specificato:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Visualizzare il DNS inverso di un PublicIpAddress esistente

valore tooview hello configurato per un PublicIpAddress esistente:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Rimuovere il DNS inverso da indirizzi IP pubblici esistenti

tooremove una proprietà DNS inversa da un PublicIpAddress esistente:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Configurare il DNS inverso per i servizi cloud

In questa sezione vengono fornite istruzioni dettagliate per la modalità tooconfigure inversa DNS per i servizi Cloud nel modello di distribuzione classica hello, tramite Azure PowerShell. Configurazione del DNS inversa per i servizi Cloud non è supportata tramite il portale di Azure, hello Azure CLI 1.0 o 2.0 CLI di Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Aggiungere servizi di Cloud tooexisting DNS inversa

tooadd un tooan di record DNS inverso servizio Cloud esistente:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Creare un servizio cloud con il DNS inverso

toocreate un nuovo servizio Cloud con proprietà DNS inversa hello già specificata:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Visualizzare il DNS inverso per i servizi cloud esistenti

hello tooview inverso proprietà DNS per un servizio Cloud esistente:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Rimuovere il DNS inverso dai servizi cloud esistenti

tooremove una proprietà DNS inversa da un servizio Cloud esistente:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>domande frequenti

### <a name="how-much-do-reverse-dns-records-cost"></a>Quanto costano i record DNS inversi?

Sono gratuiti.  Non sono previsti costi aggiuntivi per i record DNS inversi o le query.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Sarà la risoluzione di record DNS inverso da hello internet?

Sì. Dopo aver impostato la proprietà DNS inversa hello per il servizio di Azure, Azure gestisce tutte le deleghe DNS di hello e zone DNS necessarie risolve tooensure che i record DNS inversa per tutti gli utenti di Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Vengono creati record DNS inversi per i servizi di Azure?

No. Il DNS inverso sarà una funzionalità che prevede il consenso esplicito. Nessuna impostazione predefinita vengono creati i record DNS inversi, se si sceglie di non tooconfigure li.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Che cos'è il formato di hello per il nome di dominio completo (FQDN) di hello?

I nomi di dominio completi vengono specificati in ordine progressivo e devono terminare con un punto, ad esempio "app1.contoso.com.".

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Cosa accade se il controllo di convalida hello per hello inversa DNS è stato specificato ha esito negativo?

Dove hello inversa DNS convalida ha esito negativo, hello operazione tooconfigure hello record DNS inverso ha esito negativo. Correggere hello inversa DNS valore come richiesto e riprovare.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>È possibile configurare il DNS inverso per il servizio app di Azure?

No. DNS inversa non è supportata per hello servizio App di Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>È possibile configurare più record DNS inversi per il servizio di Azure?

No. Azure supporta un solo record DNS inverso per ogni servizio cloud di Azure o PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>È possibile configurare il DNS inverso per le risorse PublicIpAddress IPv6?

No. Azure supporta attualmente il DNS inverso solo per le risorse PublicIpAddress IPv4 e i servizi cloud.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>È possibile inviare messaggi di posta elettronica tooexternal domini dai servizi di calcolo di Azure?

No. [Servizi di calcolo di Azure non supportano l'invio messaggi di posta elettronica tooexternal domini](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Informazioni su come troppo[zona di ricerca inversa hello host per l'intervallo di IP assegnato dal provider di servizi Internet in Azure DNS](dns-reverse-dns-for-azure-services.md).

