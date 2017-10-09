---
title: aaaManage DNS record in DNS di Azure con Azure PowerShell | Documenti Microsoft
description: Gestione dei set di record e dei record DNS in DNS di Azure quando si ospita il dominio in DNS di Azure. Tutti i comandi di PowerShell per le operazioni sui set di record e i record.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Gestire record e recordset DNS in DNS di Azure con Azure PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](dns-operations-recordsets-portal.md)
> * [Interfaccia della riga di comando di Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Questo articolo illustra come toomanage DNS i record per la zona DNS tramite Azure PowerShell. I record DNS possono essere gestiti anche tramite hello multipiattaforma [CLI di Azure](dns-operations-recordsets-cli.md) o hello [portale di Azure](dns-operations-recordsets-portal.md).

esempi di Hello in questo articolo si supponga di avere già [installato Azure PowerShell, connesso e creata una zona DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Introduzione

Prima di creare record DNS nel sistema DNS di Azure, è innanzitutto necessario toounderstand come DNS di Azure consente di organizzare i record DNS nel set di record DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Per altre informazioni sui record DNS nel servizio DNS di Azure, vedere [Zone e record DNS](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Creare un nuovo record DNS

Se il nuovo record ha hello stesso nome e tipo come un record esistente, è necessario troppo[aggiungerlo come set di record esistenti toohello](#add-a-record-to-an-existing-record-set). Se il nuovo record ha un diverso tooall nome e tipo di record esistenti, è necessario toocreate un nuovo set di record. 

### <a name="create-a-records-in-a-new-record-set"></a>Creare record di tipo "A" in un nuovo set di record

Per creare set di record, utilizzare hello `New-AzureRmDnsRecordSet` cmdlet. Quando si crea un set di record, è necessario zona hello, nome del set di record hello toospecify il tempo di hello toolive (TTL), il tipo di record hello e hello record toobe creati.

i parametri di Hello per l'aggiunta di set di record tooa record dipendono dal tipo di hello del set di record di hello. Ad esempio, quando si utilizza un set di record di tipo 'A', è necessario indirizzo IP di hello toospecify tramite il parametro hello `-IPv4Address`. Per altri tipi di record vengono usati altri parametri. Per altre informazioni, vedere la sezione [Altri esempi di tipi di record](#additional-record-type-examples).

Hello seguente viene creato un set con il nome relativo hello 'www' nella zona DNS 'contoso.com' hello di record. nome completo di Hello del set di record hello è 'www.contoso.com'. tipo di record Hello è 'A' e hello TTL è 3600 secondi. set di record Hello contiene un singolo record con indirizzo IP '1.2.3.4'.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate un set di record in hello 'apice' di una zona (in questo caso, 'il dominio contoso.com'), utilizza il nome di set di record hello ' @' (escluse le virgolette):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Se è necessario un set di record che contiene più di un record toocreate, creare una matrice locale e aggiungere record hello, quindi passare la matrice hello troppo`New-AzureRmDnsRecordSet` come indicato di seguito:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore. Hello esempio seguente viene illustrato come toocreate un set di record con due voci di metadati, ' dept = finance' e ' ambiente di produzione ='.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

DNS di Azure supporta anche i set di record "empty", che può agire come un segnaposto tooreserve un nome DNS prima di creare record DNS. Set di record vuoti sono visibili nel piano di controllo di hello DNS di Azure, ma vengono visualizzati nel server dei nomi DNS di Azure hello. Hello di esempio seguente crea un set di record vuoto:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Creare record di altri tipi

Dopo aver visto in dettaglio come toocreate 'A' Registra, hello seguenti esempi viene illustrato come record toocreate di altri tipi di record di DNS di Azure è supportati.

In ogni caso, vengono dimostrati come un record toocreate imposta contenente un singolo record. Hello esempi precedenti per record 'A' possono essere adattato toocreate set di record di altri tipi contenente più record, con i metadati, o i set di record vuoto toocreate.

Non fornita è un esempio toocreate un set di record SOA, poiché viene creati SOA ed eliminato con ogni zona DNS e non è possibile creare o eliminare separatamente. Tuttavia, [hello SOA possa essere modificato, come illustrato nell'esempio versione successiva](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Creare un set di record AAAA con un singolo record

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Creare un set di record CNAME con un singolo record

> [!NOTE]
> standard DNS Hello non consentono i record CNAME al vertice hello di una zona (`-Name '@'`), né che consentono i set di record che contiene più di un record.
> 
> Per altre informazioni, vedere[Record CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Creare un set di record MX con un singolo record

In questo esempio, si usa nome set di record hello ' @' record toocreate un MX al vertice zona hello (in questo caso, 'il dominio contoso.com').


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Creare un set di record NS con un singolo record

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Creare un set di record PTR con un singolo record

In questo caso, "my-arpa-zone.com' rappresenta hello zona di ricerca inversa ARPA che rappresenta l'intervallo di IP. Ogni record PTR impostato in questa zona corrisponde tooan di indirizzo IP in questo intervallo IP. nome del record '10' Hello è ultimo ottetto di hello dell'indirizzo IP hello in questo intervallo IP rappresentato da questo record.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Creare un set di record SRV con un singolo record

Quando si crea un [set di record SRV](dns-zones-records.md#srv-records), specificare hello  *\_servizio* e  *\_protocollo* in hello Nome set di record. Non è alcuna necessità tooinclude ' @' in hello set di record nome durante la creazione di un record SRV set al vertice zona hello.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Creare un set di record TXT con un singolo record

Hello esempio seguente viene illustrato come toocreate un TXT record. Per ulteriori informazioni sulla lunghezza massima della stringa hello è supportata nei record TXT, vedere [record TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Ottenere un set di record

Utilizzare un set di record esistente, tooretrieve `Get-AzureRmDnsRecordSet`. Questo cmdlet restituisce un oggetto locale che rappresenta hello set di record in DNS di Azure.

Come con `New-AzureRmDnsRecordSet`, il nome di set di record hello specificato deve essere un *relativo* nome, pertanto è necessario escludere nome zona hello. È inoltre necessario toospecify hello tipo record e contenente i set di record hello zona di hello.

Hello esempio seguente viene illustrato come tooretrieve un set di record. In questo esempio, la zona hello viene specificata con hello `-ZoneName` e `-ResourceGroupName` parametri.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

In alternativa, è inoltre possibile specificare zona hello mediante un oggetto fuso passato usando hello `-Zone` parametro.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Elencare i set di record

È inoltre possibile utilizzare `Get-AzureRmDnsZone` toolist i set di record in una zona, omettendo hello `-Name` e/o `-RecordType` parametri.

Hello esempio seguente restituisce i set di tutti i record nella zona hello:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Hello esempio seguente viene illustrato come tutti i set di un determinato tipo di record possono essere recuperati specificando un tipo di record hello mentre il nome del set di record hello l'omissione:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Imposta tutti i record con un nome specificato, tooretrieve tra tipi di record, è necessario tooretrieve tutti i set di record e quindi filtro hello risultati:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

In hello tutti gli esempi sopra riportati, la zona hello può essere specificato tramite l'utilizzo di hello `-ZoneName` e `-ResourceGroupName`parametri (come illustrato), oppure specificando un oggetto fuso orario:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Aggiungere un record tooan esistente del set di record

un record esistente tooan record tooadd impostato, seguire hello tre passaggi:

1. Ottiene il set di record esistenti hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Aggiungere hello nuovi record toohello locale set di record. Si tratta di un'operazione offline.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Eseguire il commit hello modifica indietro toohello servizio DNS di Azure. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Utilizzando `Set-AzureRmDnsRecordSet` *sostituisce* hello esistente set di record in DNS di Azure (e tutti i record contiene) con il set di record hello specificato. [Controllo eTag](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti. È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.

Questa sequenza di operazioni può anche essere *reindirizzato*, vale a dire si passa l'oggetto set di record hello utilizzando pipe hello, anziché passarlo come parametro:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

esempi di Hello sopra riportati illustrano come impostare di tooadd un record esistente 'A' tooan record di tipo 'A'. Una sequenza di operazioni simile viene utilizzato tooadd i set di record toorecord di altri tipi, sostituendo hello `-Ipv4Address` parametro di `Add-AzureRmDnsRecordConfig` con altri tipi di record tooeach specifico di parametri. Hello parametri per ogni tipo di record sono hello uguale a quello di hello `New-AzureRmDnsRecordConfig` cmdlet come mostrato [esempi aggiuntivi di tipo record](#additional-record-type-examples) sopra.

I set di record di tipo "CNAME" o "SOA" non possono contenere più di un record. Questo vincolo viene visualizzato dagli standard DNS hello. non è una limitazione del servizio DNS di Azure.

## <a name="remove-a-record-from-an-existing-record-set"></a>Rimuovere un record da un set di record esistente

processo tooremove un record da un set di record Hello è un record tooan esistente simile tooadd di processo toohello set di record:

1. Ottiene il set di record esistenti hello

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Rimuovere i record di hello dall'oggetto set di record locale hello. Si tratta di un'operazione offline. record di Hello corso di rimozione deve essere una corrispondenza esatta con un record esistente in tutti i parametri.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Eseguire il commit hello modifica indietro toohello servizio DNS di Azure. Hello utilizzo facoltativo `-Overwrite` passare toosuppress [Etag controlla](dns-zones-records.md#etags) per modifiche simultanee.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Utilizzando hello sopra sequenza tooremove hello ultimo record da un set di record non comporta l'eliminazione del set di record hello, ma lascia un set di record vuoto. vedere un set di record, tooremove [eliminare un set di record](#delete-a-record-set).

Allo stesso modo tooadding record tooa set di record, sequenza hello di un set di record può anche essere reindirizzato tooremove di operazioni:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Sono supportati i tipi di record diversi passando i parametri specifici del tipo appropriato di hello troppo`Remove-AzureRmDnsRecordSet`. Hello parametri per ogni tipo di record sono hello uguale a quello di hello `New-AzureRmDnsRecordConfig` cmdlet come mostrato [esempi aggiuntivi di tipo record](#additional-record-type-examples) sopra.


## <a name="modify-an-existing-record-set"></a>Modificare un set di record esistente

passaggi per la modifica di un set di record esistenti in Hello sono simili toohello effettuate durante l'aggiunta o rimozione di record da un set di record:

1. Recuperare il record esistente hello impostato utilizzando `Get-AzureRmDnsRecordSet`.
2. Modificare l'oggetto set di record locale hello:
    * Aggiungere o rimuovere record.
    * La modifica dei parametri di hello dei record esistenti
    * Modifica di record hello del set di metadati e toolive TTL (time)
3. Eseguire il commit delle modifiche tramite hello `Set-AzureRmDnsRecordSet` cmdlet. Questo *sostituisce* hello esistente set di record in DNS di Azure con i set di record hello specificato.

Quando si utilizza `Set-AzureRmDnsRecordSet`, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono sovrascritti. È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>Imposta tooupdate un record in un record esistente

In questo esempio, si modifica l'indirizzo IP hello del 'A' record esistente:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>un record SOA toomodify

È possibile aggiungere o rimuovere i record da hello automaticamente creato un record SOA impostato al vertice zona hello (`-Name "@"`, tra virgolette). Tuttavia, è possibile modificare i parametri di hello all'interno di hello record SOA (ad eccezione di "Host") e impostare il valore TTL record hello.

Hello seguente esempio viene illustrato come hello toochange *posta elettronica* proprietà del record SOA hello:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>record NS toomodify al vertice zona hello

record NS Hello impostato al vertice zona hello viene creato automaticamente con ogni zona DNS. Contiene i nomi hello della zona di hello DNS di Azure nome server toohello assegnato.

È possibile aggiungere nomi aggiuntivi server toothis NS set di record, toosupport CO-ospitano i domini con più di un provider DNS. È inoltre possibile modificare hello durata (TTL) e i metadati per questo set di record. Tuttavia, è Impossibile rimuovere o modificare server dei nomi DNS di Azure prepopolato hello.

Si noti che questo si applica solo toohello NS set di record al vertice zona hello. Altri set di record NS nella zona (come le aree figlio toodelegate usato) possono essere modificati senza vincoli.

Hello di esempio seguente viene illustrato come tooadd un record NS di nomi aggiuntivi server toohello imposta al vertice zona hello:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>record toomodify impostare i metadati

[Set di record dei metadati](dns-zones-records.md#tags-and-metadata) può essere utilizzato tooassociate i dati specifici dell'applicazione con ogni set di record, come coppie chiave-valore.

Hello esempio seguente viene illustrato come impostare di toomodify hello metadati di un record esistente:

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Eliminare un set di record

Set di record possono essere eliminate utilizzando hello `Remove-AzureRmDnsRecordSet` cmdlet. L'eliminazione di un set di record elimina inoltre tutti i record all'interno del set di record hello.

> [!NOTE]
> Non è possibile eliminare hello SOA e NS set di record al vertice zona hello (`-Name '@'`).  DNS di Azure creata questi automaticamente quando è stato creato, zona hello e li elimina automaticamente quando viene eliminata hello.

Hello esempio seguente viene illustrato come toodelete un set di record. In questo esempio, il nome di set di record hello, tipo di set di record, nome della zona e gruppo di risorse sono ogni specificati in modo esplicito.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

In alternativa, è possibile specificare un set di record hello dal nome e il tipo e hello zona specificata utilizzando un oggetto:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Come una terza opzione, è possibile specificare record hello impostare autonomamente l'utilizzo di un oggetto set di record:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Quando si specifica il set di record hello toobe eliminato utilizzando un oggetto set di record, [Etag controlla](dns-zones-records.md#etags) vengono utilizzate le modifiche simultanee tooensure non vengono eliminate. È possibile utilizzare hello facoltativo `-Overwrite` passare toosuppress questi controlli.

oggetto set di record Hello può anche essere reindirizzato anziché passato come parametro:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Richieste di conferma

Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, e `Remove-AzureRmDnsRecordSet` tutti i cmdlet supportano richieste di conferma.

Ogni cmdlet chiede conferma se hello `$ConfirmPreference` variabile di preferenza PowerShell ha un valore di `Medium` o inferiore. Poiché il valore predefinito hello per `$ConfirmPreference` è `High`, queste richieste non vengono assegnate quando si usa PowerShell le impostazioni predefinite di hello.

È possibile eseguire l'override di hello corrente `$ConfirmPreference` impostazione utilizzando hello `-Confirm` parametro. Se si specifica `-Confirm` o `-Confirm:$True` , hello cmdlet chiede conferma prima dell'esecuzione. Se si specifica `-Confirm:$False` , hello cmdlet non viene chiesto di confermare. 

Per altre informazioni su `-Confirm` e `$ConfirmPreference`, vedere [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Informazioni sulle variabili di preferenza).

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su [zone e record nel servizio DNS di Azure](dns-zones-records.md).
<br>
Informazioni su come troppo[proteggere le zone e record](dns-protect-zones-recordsets.md) quando si utilizza il DNS di Azure.
<br>
Hello revisione [la documentazione di riferimento di Azure PowerShell DNS](/powershell/module/azurerm.dns).
