---
title: aaaGet avviato con il DNS di Azure tramite PowerShell | Documenti Microsoft
description: "Informazioni su come toocreate un DNS zona e questo record in DNS di Azure. Questo è un toocreate Guida dettagliata e la zona DNS prima di gestire e registrare l'utilizzo di PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Introduzione a DNS Azure con PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-getstarted-cli.md)

In questo articolo illustra hello passaggi toocreate prima zona DNS il record utilizzando Azure PowerShell. È anche possibile eseguire questi passaggi tramite il portale di Azure hello o hello multipiattaforma CLI di Azure.

Una zona DNS è utilizzato toohost hello DNS record per un particolare dominio. toostart hosting del dominio DNS di Azure, è necessario toocreate una zona DNS per il nome di dominio. Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS. Infine, toopublish della zona DNS toohello Internet, server dei nomi tooconfigure hello è necessario per il dominio hello. Ogni passaggio è illustrato di seguito.

Queste istruzioni presuppongono aver già installato e connesso tooAzure PowerShell. Per ulteriori informazioni, vedere [come toomanage DNS zone tramite PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Prima di creare una zona DNS hello, un gruppo di risorse viene creato toocontain zona di DNS hello. Hello seguito è riportato il comando hello.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Creare una zona DNS

Una zona DNS viene creata utilizzando hello `New-AzureRmDnsZone` cmdlet. esempio Hello crea una zona DNS denominata *contoso.com* nel gruppo di risorse hello chiamato *MyResourceGroup*. Utilizzare l'esempio toocreate hello una zona DNS, sostituendo i valori hello per uso personale.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Creare un record DNS

Per creare set di record, utilizzare hello `New-AzureRmDnsRecordSet` cmdlet. Hello seguente viene creato un record con il nome relativo hello "www" hello "contoso.com", nel gruppo di risorse "MyResourceGroup" zona di DNS. nome completo di Hello del set di record hello è "www.contoso.com". tipo di record Hello è "A", con l'indirizzo IP "1.2.3.4" e hello TTL è 3600 secondi.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Per altri tipi di record, per i set di record con più di un record e i record esistenti toomodify, vedere [record DNS di gestione e i set di record con Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Visualizzare i record

i record DNS di hello toolist nella zona, utilizzare:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Aggiornare i server dei nomi

Dopo aver soddisfatto che la zona DNS e i record sono stati impostati correttamente, è necessario tooconfigure il nome di dominio toouse server dei nomi DNS di Azure hello. In questo modo altri utenti nel hello Internet toofind i record DNS.

Server dei nomi per l'area Hello forniti tramite hello `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Questi server dei nomi deve essere configurato con hello registrar (in cui è stato acquistato il nome di dominio hello). Registrar offrirà hello opzione tooset dei server dei nomi per il dominio hello hello. Per ulteriori informazioni, vedere [delegare il tooAzure di dominio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, hello take seguente passaggio:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su DNS di Azure, vedere [Panoramica di DNS di Azure](dns-overview.md).

toolearn informazioni su gestione delle zone DNS di DNS di Azure, vedere [le zone DNS di gestione in DNS di Azure con PowerShell](dns-operations-dnszones.md).

toolearn informazioni su gestione dei record DNS nel sistema DNS di Azure, vedere [Manage DNS record e record imposta nel sistema DNS di Azure con PowerShell](dns-operations-recordsets.md).

