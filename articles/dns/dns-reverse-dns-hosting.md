---
title: aaaHosting invertire le zone di ricerca DNS nel sistema DNS di Azure | Documenti Microsoft
description: Informazioni su come hello toohost DNS di Azure di toouse invertire le zone di ricerca DNS per gli intervalli IP
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Hosting di zone DNS di ricerca inversa in DNS Azure

Questo articolo spiega come toohost hello invertire le zone di ricerca DNS per gli intervalli IP assegnati in DNS di Azure. gli intervalli IP Hello rappresentati da una zona di ricerca inversa hello devono essere assegnati tooyour organizzazione, in genere dal provider di servizi Internet.

tooconfigure inversa DNS per Azure di proprietà IP indirizzo assegnato tooyour servizio di Azure, vedere [configurare ricerca inversa hello per gli indirizzi IP di hello allocati tooyour servizio Azure](dns-reverse-dns-for-azure-services.md).

Prima di leggere questo articolo, è necessario leggere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md).

In questo articolo illustra hello passaggi toocreate prima zona di ricerca inversa DNS il record utilizzando hello portale di Azure PowerShell di Azure, Azure CLI 1.0 o 2.0 CLI di Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Creare una zona DNS di ricerca inversa

1. Accedi toohello [portale di Azure](https://portal.azure.com)
1. Nel menu Hub hello, fare clic su e fare clic su **New** > **rete** > e quindi fare clic su **zona DNS** tooopen hello **zona di DNS creare**blade.

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. In hello **zona DNS creare** pannello denominare la zona DNS. nome Hello della zona di hello è impostata in modo diverso per i prefissi IPv4 e IPv6. Utilizzare le istruzioni entrambi hello per [IPV4](#ipv4) o [IPv6](#ipv6) tooname la zona. Al termine fare clic su **crea** zona hello toocreate.

### <a name="ipv4"></a>IPv4

nome Hello di una zona di ricerca inversa IPv4 è basato sull'intervallo IP hello che rappresenta. Deve essere nel seguente formato hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Quando si crea una notazione classless zone di ricerca DNS inverse in DNS di Azure, è necessario usare un trattino (`-`) anziché una barra rovesciata ('/ ') nel nome della zona hello.
>
> Ad esempio, per hello IP intervallo 192.0.2.128/26, è necessario utilizzare `128-26.2.0.192.in-addr.arpa` come nome della zona hello anziché `128/26.2.0.192.in-addr.arpa`.
>
> Questo avviene perché, anche se entrambi sono supportate dagli standard DNS hello, i nomi contenenti una barra rovesciata hello della zona DNS (`/`) in DNS di Azure non sono supportati i caratteri.

Hello esempio seguente viene illustrato come toocreate 'Classe C' inversa zona DNS denominato `2.0.192.in-addr.arpa` nel sistema DNS di Azure tramite hello portale di Azure:

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

Ciao 'Posizione gruppo di risorse' definisce hello posizione per il gruppo di risorse hello e non influisce sulla zona DNS hello. percorso di zona DNS Hello è sempre 'global' e non viene visualizzato.

Hello esempi seguenti viene illustrato come toocomplete questa attività con Azure PowerShell e hello CLI di Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

nome Hello di una zona di ricerca inversa IPv6 deve essere nel seguente modulo hello: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Per esempi, vedere [Panoramica del DNS inverso e supporto in Azure](dns-reverse-dns-overview.md#ipv6).


Hello esempio seguente viene illustrato come toocreate una zona di ricerca DNS inversa IPv6 denominati `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` nel sistema DNS di Azure tramite hello portale di Azure:

 ![Creare una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

Ciao 'Posizione gruppo di risorse' definisce hello posizione per il gruppo di risorse hello e non influisce sulla zona DNS hello. percorso di zona DNS Hello è sempre 'global' e non viene visualizzato.

Hello esempi seguenti viene illustrato come toocomplete questa attività con Azure PowerShell e hello CLI di Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Delegare una zona DNS di ricerca inversa

Dopo aver creato la zona di ricerca DNS inversa, è necessario verificare che tale zona hello viene delegata dalla zona padre hello. Delega DNS consente hello Nome risoluzione processo toofind hello Nome server DNS che ospitano la zona di ricerca DNS inversa. In questo modo tali nome server tooanswer inversa query DNS per gli indirizzi IP hello l'intervallo di indirizzi.

Per le zone di ricerca diretta, il processo di hello di delega di una zona DNS è descritto nella sezione [delegare il tooAzure di dominio DNS](dns-delegate-domain-azure-dns.md). Delega di zone di ricerca inversa hello allo stesso modo. Hello unica differenza è che è necessario che server dei nomi tooconfigure hello con hello ISP che ha fornito l'intervallo di IP, anziché il registrar.

## <a name="create-a-dns-ptr-record"></a>Creare un record PTR DNS

### <a name="ipv4"></a>IPv4

Hello seguente esempio illustra hello processo di creazione di un record PTR in una zona DNS inversa in DNS di Azure. Per altri tipi di record e i record esistenti toomodify, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md).

1.  Nella parte superiore di hello di hello **zona DNS** pannello seleziona **+ registrare set** tooopen hello **aggiungere set di record** blade.

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. In hello **aggiungere set di record** blade. 
1. Selezionare **PTR** dal record hello "**tipo**" dal menu.  
1. Hello nome del set di record hello per un record PTR deve rest hello toobe di hello indirizzo IPv4 in ordine inverso. In questo esempio hello primi tre ottetti sono già popolati come parte del nome della zona hello (.2.0.192). Pertanto, solo hello ultimo ottetto viene fornito nel campo nome hello. Ad esempio, è possibile assegnare il nome "**15**" a un set di record per una risorsa il cui indirizzo IP è 192.0.2.15.  
1. In hello "**nome di dominio**" Immettere il nome di dominio completo hello (FQDN) della risorsa hello con IP hello.
1. Selezionare **OK** nella parte inferiore di hello del record DNS di hello pannello toocreate hello.

 ![Aggiungi set di record](./media/dns-reverse-dns-hosting/figure5.png)

di seguito Hello sono esempi su come toocomplete questa attività con PowerShell e hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Hello di esempio seguente viene illustrato il processo di hello di creazione di nuovi record 'PTR'. Per altri tipi di record e i record esistenti toomodify, vedere [record DNS di gestire e set di record mediante il portale di Azure di hello](dns-operations-recordsets-portal.md).

1. Nella parte superiore di hello di hello **blade di zona DNS**selezionare **+ registrare set** tooopen hello **aggiungere set di record** blade.

  ![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. In hello **aggiungere set di record** blade. 
3. Selezionare **PTR** dal record hello "**tipo**" dal menu.  
4. Hello nome del set di record hello per un record PTR deve rest hello toobe di hello indirizzo IPv6 in ordine inverso. Non deve includere alcuna compressione degli zeri. In questo esempio hello primi 64 bit di hello IPv6 sono già popolati come parte del nome della zona hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Pertanto, solo hello ultimi 64 bit vengono specificati nel campo nome hello. ultimi 64 bit dell'indirizzo IP hello Hello vengono immessi in ordine inverso, utilizzando un punto come delimitatore di hello tra ogni numero esadecimale. Ad esempio, è possibile specificare "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" come nome di un set di record per una risorsa il cui indirizzo IP è 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. In hello "**nome di dominio**" Immettere il nome di dominio completo hello (FQDN) della risorsa hello con IP hello.
6. Selezionare **OK** nella parte inferiore di hello del record DNS di hello pannello toocreate hello.

![Pannello Aggiungi set di record](./media/dns-reverse-dns-hosting/figure7.png)

di seguito Hello sono esempi su come toocomplete questa attività con PowerShell e hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>Interfaccia della riga di comando di Azure 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Visualizzare i record

i record di hello tooview è stato creato, passare tooyour zona DNS in hello portale di Azure. In hello inferiore parte di hello **zona DNS** pannello, è possibile visualizzare i record per la zona DNS hello hello. Dovrebbe essere hello NS e SOA record predefiniti, che vengono create in ogni area, oltre a qualsiasi nuovo record che è stato creato.

### <a name="ipv4"></a>IPv4

Pannello Zona DNS con i record PTR IPv4:

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

Hello negli esempi seguenti mostrano come tooview hello PTR registra l'utilizzo di PowerShell o hello CLI di Azure:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Pannello Zona DNS con i record PTR IPv6:

![Pannello Zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

di seguito Hello sono esempi su come tooview hello registra con PowerShell e hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>domande frequenti

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>È possibile ospitare zone DNS di ricerca inversa per i blocchi di indirizzi IP assegnati dal provider di servizi Internet in DNS Azure?

Sì. Hosting di zone di ricerca inversa (ARPA) hello per intervalli IP in DNS di Azure è completamente supportato.

Creare la zona di ricerca inversa hello in DNS di Azure come descritto in questo articolo e quindi di usare con l'ISP troppo[delegato hello zona](dns-domain-delegation.md).  È quindi possibile gestire i record PTR hello per ogni ricerca inversa in hello come altri tipi di record.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Quanto costa l'hosting della zona DNS di ricerca inversa?

Zona di ricerca DNS inversa hello di hosting per il blocco IP assegnato dal provider di servizi Internet in DNS di Azure viene addebitato ai [tariffe DNS di Azure standard](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>È possibile ospitare zone DNS di ricerca inversa per indirizzi IPv4 e IPv6 in DNS Azure?

Sì. Questo articolo viene illustrato come toocreate sia IPv4 che IPv6 invertire le zone di ricerca DNS nel sistema DNS di Azure.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>È possibile importare una zona DNS di ricerca inversa esistente?

Sì. È possibile utilizzare hello Azure CLI tooimport esistente le zone DNS in DNS di Azure. Questo approccio è applicabile alle zone di ricerca diretta e alle zone DNS di ricerca inversa.

Per ulteriori informazioni, vedere [importazione ed esportazione di un file di zona DNS mediante hello Azure CLI](dns-import-export.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul DNS inverso, vedere [Risoluzione DNS inversa su Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Informazioni su come troppo[gestire record di ricerca inversa DNS per i servizi di Azure](dns-reverse-dns-for-azure-services.md).
