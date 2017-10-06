---
title: aaaDelegate il tooAzure di dominio DNS | Documenti Microsoft
description: Comprendere come usare DNS di Azure e delega di dominio toochange denominati server tooprovide dominio ospita.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Delegato tooAzure un dominio DNS

DNS di Azure consente una zona DNS toohost e gestire i record DNS hello per un dominio in Azure. Per le query DNS per tooreach un dominio DNS di Azure, il dominio hello deve toobe delegato tooAzure DNS del dominio padre hello. Tenere presente il DNS di Azure non è il registrar di dominio hello. Questo articolo viene illustrato come toodelegate il tooAzure di dominio DNS.

Per i domini acquistati presso un registrar, registrar offre hello opzione tooset questi record NS. Non si dispone tooown toocreate un dominio una zona DNS con lo stesso nome di dominio in DNS di Azure. Tuttavia, è necessario tooown hello dominio tooset backup hello tooAzure di delega DNS presso il registrar hello.

Si supponga, ad esempio, si acquista il dominio di hello 'contoso.net' e crea una zona con il nome di hello 'contoso.net' in DNS di Azure. Come proprietario del dominio hello hello registrar offre che Hello opzione tooconfigure hello indirizzi del server (ovvero, i record di hello NS) per il dominio. registrar Hello archivia questi record NS nel dominio padre hello, in questo caso ".net". I client in tutto il mondo hello possono quindi essere dominio diretto tooyour nella zona DNS di Azure durante il tentativo di record DNS tooresolve 'contoso.net'.

## <a name="create-a-dns-zone"></a>Creare una zona DNS

1. Accedi toohello portale di Azure
1. Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:

   | **Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|contoso.net|nome Hello della zona DNS hello|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare un gateway applicazione di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Crea nuovo:** contosoRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

> [!NOTE]
> gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello. percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.

## <a name="retrieve-name-servers"></a>Recuperare i server dei nomi

Per poter delegare il tooAzure di zona DNS di DNS, è necessario innanzitutto tooknow hello server nomi per la zona attiva. DNS Azure alloca i server dei nomi da un pool ogni volta che viene creata una zona.

1. Zona DNS hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **contoso.net** zona DNS in hello **tutte le risorse** blade. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **contoso.net** in hello filtro in base al nome... gateway applicazione hello di accesso tooeasily di casella. 

1. Recuperare i server dei nomi hello dal pannello della zona DNS hello. In questo esempio è stato assegnato zona hello 'contoso.net', server dei nomi ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS di Azure crea automaticamente i record NS autorevoli nella zona contenente hello server dei nomi assegnato.  i nomi di server dei nomi hello toosee tramite Azure PowerShell o l'interfaccia CLI di Azure, è sufficiente tooretrieve questi record.

Hello negli esempi seguenti vengono forniscono anche passaggi hello server dei nomi hello tooretrieve per una zona DNS di Azure con PowerShell e CLI di Azure.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Hello di esempio seguente è riportata la risposta hello.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Hello di esempio seguente è riportata la risposta hello.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Dominio hello delegato

Ora che è creare la zona DNS hello e si dispone di server dei nomi hello, dominio padre hello deve toobe aggiornato con i server dei nomi DNS di Azure hello. Ogni registrar dispone di propri DNS management tools toochange hello record server dei nomi per un dominio. Nella pagina di gestione DNS del registrar hello, modificare i record NS hello e sostituire i record NS hello con hello quelli creati DNS di Azure.

Quando la delega tooAzure un dominio DNS, è necessario utilizzare nomi di server di nome hello forniti da DNS di Azure. È consigliabile toouse tutti i quattro nomi i nomi di server, indipendentemente dal nome hello del dominio. La delega di dominio non richiede hello Nome server name toouse hello nello stesso dominio del dominio principale.

È necessario utilizzare 'glue record' toopoint toohello DNS di Azure nome indirizzi IP del server, non dopo questi indirizzi IP potrebbero cambiare nelle future. Le deleghe che usano nomi dei server dei nomi nella propria zona, definiti a volte "server dei nomi personali", non sono attualmente supportate in DNS di Azure.

## <a name="verify-name-resolution-is-working"></a>Verificare che la risoluzione dei nomi funzioni

Dopo aver completato la delega di hello, è possibile verificare che la risoluzione dei nomi funziona tramite uno strumento, ad esempio "nslookup" tooquery hello record SOA per la zona (che viene creata automaticamente anche quando si crea la zona hello).

È non dispone di server dei nomi DNS di Azure hello toospecify, se è stata impostata correttamente, hello normale DNS processo di risoluzione delega hello hello Nome server trovati automaticamente.

```
nslookup -type=SOA contoso.com
```

di seguito Hello è una risposta di esempio da hello precedente comando:

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Delegare sottodomini in DNS di Azure

Se si desidera tooset di una zona figlio separata, è possibile delegare un sottodominio nel sistema DNS di Azure. Ad esempio, dopo aver creato una e delegato 'contoso.net' nel sistema DNS di Azure, si supponga che si desidera tooset di una zona figlio separata, 'partners.contoso.net'.

1. Creare una zona figlio hello 'partners.contoso.net' nel sistema DNS di Azure.
2. Cercare hello autorevole i record NS hello figlio zona tooobtain hello Nome server ospita una zona figlio hello in DNS di Azure.
3. Delegare zona figlio hello configurando i record NS nella zona padre hello verso zona figlio toohello.

### <a name="create-a-dns-zone"></a>Creare una zona DNS

1. Accedi toohello portale di Azure
1. Nel menu Hub hello, fare clic su e fare clic su **nuovo > rete >** e quindi fare clic su **zona DNS** blade di zona DNS creare hello tooopen.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. In hello **zona DNS creare** pannello immettere i seguenti valori hello, quindi fare clic su **crea**:

   | **Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|partners.contoso.net|nome Hello della zona DNS hello|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare un gateway applicazione di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Utilizza esistente:** contosoRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

> [!NOTE]
> gruppo di risorse Hello fa riferimento il percorso toohello hello del gruppo di risorse e non influisce sulla zona DNS hello. percorso di zona DNS Hello sono sempre "globale" e non viene visualizzato.

### <a name="retrieve-name-servers"></a>Recuperare i server dei nomi

1. Zona DNS hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **partners.contoso.net** zona DNS in hello **tutte le risorse** blade. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **partners.contoso.net** in hello filtro in base al nome... zona DNS hello accesso tooeasily casella.

1. Recuperare i server dei nomi hello dal pannello della zona DNS hello. In questo esempio è stato assegnato zona hello 'contoso.net', server dei nomi ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

DNS di Azure crea automaticamente i record NS autorevoli nella zona contenente hello server dei nomi assegnato.  i nomi di server dei nomi hello toosee tramite Azure PowerShell o l'interfaccia CLI di Azure, è sufficiente tooretrieve questi record.

### <a name="create-name-server-record-in-parent-zone"></a>Creare un record del server dei nomi in una zona padre

1. Passare toohello **contoso.net** zona DNS in hello portale di Azure.
1. Fare clic su **+ Set di record**.
1. In hello **aggiungere set di record** pannello, immettere i seguenti valori hello, quindi fare clic su **OK**:

   | **Impostazione** | **Valore** | **Dettagli** |
   |---|---|---|
   |**Nome**|partners|nome di Hello della zona DNS di hello figlio|
   |**Tipo**|NS|Usare NS per i record del server dei nomi.|
   |**TTL**|1|Ora toolive.|
   |**Unità TTL**|Ore|Imposta toohours toolive unità di tempo|
   |**SERVER DEI NOMI**|{server dei nomi dalla zona partners.contoso.net}|Immettere tutti i 4 hello server dei nomi da partners.contoso.net zona. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Delega di sottodomini in DNS di Azure con altri strumenti

Hello seguito sono riportati alcuni passaggi hello toodelegate i sottodomini in DNS di Azure con PowerShell e CLI:

#### <a name="powershell"></a>PowerShell

Hello esempio PowerShell seguente viene illustrato il funzionamento. Hello stessi passaggi possono essere eseguiti tramite hello portale di Azure o tramite hello multipiattaforma CLI di Azure.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Utilizzare `nslookup` tooverify che tutto sia installato correttamente eseguendo la ricerca di record SOA di zona figlio hello hello.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Recuperare i server di nome hello per hello `partners.contoso.net` zona dall'output di hello.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Creare set di record hello e i record NS per ogni server dei nomi.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:

1. Nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **contosorg** gruppo di risorse in hello tutti pannello risorse. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **contosorg** in hello **filtrare in base al nome...** gruppo di risorse hello accesso tooeasily casella.
1. In hello **contosorg** pannello, fare clic su hello **eliminare** pulsante.
1. Hello portale richiede nome hello tootype di hello tooconfirm di gruppo di risorse che si desidera toodelete è. Tipo *contosorg* per nome gruppo di risorse hello, quindi fare clic su **eliminare**. Elimina un gruppo di risorse, tutte le risorse nel gruppo di risorse hello, pertanto sempre certi tooconfirm contenuto hello di un gruppo di risorse prima di eliminarlo. portale Hello Elimina tutte le risorse contenute nel gruppo di risorse hello, quindi Elimina gruppo di risorse hello stesso. Questo processo richiede alcuni minuti.

## <a name="next-steps"></a>Passaggi successivi

[Gestire le zone DNS](dns-operations-dnszones.md)

[Gestire i record DNS](dns-operations-recordsets.md)
