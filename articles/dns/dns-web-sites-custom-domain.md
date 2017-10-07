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
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Creare record DNS per un'app Web in un dominio personalizzato

È possibile utilizzare toohost DNS di Azure un dominio personalizzato per le app web. Ad esempio, si sta creando un'app web di Azure e si desidera il tooaccess gli utenti da uno tramite contoso.com o www.contoso.com come un nome di dominio completo.

toodo, si dispone di due record toocreate:

* Un toocontoso.com puntamento record radice "A"
* Un "" record CNAME per nome www hello che punta toohello un record

Tenere presente che se si crea un record A per un'app web in Azure, un record deve essere aggiornato manualmente se hello hello sottostante indirizzo IP per le modifiche di hello web app.

## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare, è innanzitutto necessario creare una zona DNS di DNS di Azure e delegare zona hello il tooAzure registrazione DNS.

1. toocreate una zona DNS, seguire i passaggi hello [creare una zona DNS](dns-getstarted-create-dnszone.md).
2. toodelegate il tooAzure DNS DNS, seguire i passaggi hello [delega di dominio DNS](dns-domain-delegation.md).

Dopo la creazione di una zona e delegarla tooAzure DNS, è quindi possibile creare record per il dominio personalizzato.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Creare un record A per il dominio personalizzato

Un record è toomap usato un indirizzo IP tooits di nome. Nell'esempio seguente hello nella si assegnerà come un tooan di record di un indirizzo IPv4:

### <a name="step-1"></a>Passaggio 1

Creare un record A e assegnare tooa $rs variabile

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Passaggio 2

Aggiungere i set di record di hello IPv4 valore toohello creato in precedenza "@" utilizzando hello $rs variabile assegnato. Hello valore IPv4 assegnato sarà l'indirizzo IP hello per le app web.

indirizzo IP di hello toofind per un'app web, seguire i passaggi hello [configurare un nome di dominio personalizzato in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Passaggio 3

Eseguire il commit del set di record toohello modifiche hello. Utilizzare `Set-AzureRMDnsRecordSet` hello tooupload cambia toohello tooAzure di set di record DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Creare un record CNAME per il dominio personalizzato

Se il dominio è già gestito dal servizio DNS di Azure (vedere [delega di dominio DNS](dns-domain-delegation.md), è possibile utilizzare i seguenti toocreate esempio hello un record CNAME per contoso.azurewebsites.net hello.

### <a name="step-1"></a>Passaggio 1

Aprire PowerShell e creare un nuovo set di record CNAME e assegnare tooa $rs variabile. Questo esempio viene creato un tipo di set di record CNAME con"toolive" 600 secondi nella zona DNS denominato "contoso.com".

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Hello di esempio seguente è riportata la risposta hello.

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

### <a name="step-2"></a>Passaggio 2

Una volta creato hello set di record CNAME, è necessario toocreate un valore alias a cui punterà toohello web app.

Utilizzando hello assegnate in precedenza la variabile "$rs" è possibile utilizzare il comando di PowerShell hello sotto alias hello toocreate per hello web app contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Hello di esempio seguente è riportata la risposta hello.

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

### <a name="step-3"></a>Passaggio 3

Eseguire il commit delle modifiche di hello mediante hello `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

È possibile convalidare il record di hello è stato creato correttamente eseguendo una query hello "www.contoso.com" con nslookup, come illustrato di seguito:

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

## <a name="create-an-awverify-record-for-web-apps"></a>Creare un record "awverify" per le app Web

Se si decide di toouse un record A per l'app web, è necessario passare attraverso un tooensure di processo di verifica è dominio personalizzato hello personalizzati. Questo passaggio di verifica viene eseguito creando uno speciale record CNAME denominato "awverify". Questa sezione si applica solo i record tooA.

### <a name="step-1"></a>Passaggio 1

Creare record "awverify" hello. Nell'esempio hello seguente verrà creata record "aweverify" hello per la proprietà tooverify contoso.com per il dominio personalizzato hello.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Hello di esempio seguente è riportata la risposta hello.

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

### <a name="step-2"></a>Passaggio 2

Una volta creato il set di record hello "awverify", assegnare record CNAME hello impostare alias. Nell'esempio hello seguente, si assegnerà tooawverify.contoso.azurewebsites.net alias del set di record CNAMe di hello.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Hello di esempio seguente è riportata la risposta hello.

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

### <a name="step-3"></a>Passaggio 3

Eseguire il commit delle modifiche di hello mediante hello `Set-AzureRMDnsRecordSet cmdlet`, come illustrato nel comando hello riportato di seguito.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Passaggi successivi

Seguire i passaggi di hello in [configurazione di un nome di dominio personalizzato per il servizio App](../app-service-web/web-sites-custom-domain-name.md) tooconfigure il toouse app web un dominio personalizzato.
