---
title: aaaImport e una zona del dominio di esportazione file tooAzure DNS mediante Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come tooimport ed esportare un DNS zone file tooAzure DNS mediante Azure CLI 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importare ed esportare un file di zona DNS mediante hello Azure CLI 1.0 

In questo articolo illustra come tooimport ed esportare file di zona DNS per l'utilizzo di DNS di Azure hello Azure CLI 1.0.

## <a name="introduction-toodns-zone-migration"></a>Migrazione di zona tooDNS introduzione

Un file di zona DNS è un file di testo che contiene i dettagli di tutti i record nella zona hello sistema DNS (Domain Name). Segue un formato standard, ideale per il trasferimento dei record DNS tra sistemi DNS. Utilizzando un file di zona è un veloce, affidabile e un modo pratico tootransfer una zona DNS interno o all'esterno di DNS di Azure.

DNS di Azure supporta l'importazione ed esportazione di file di zona utilizzando hello Azure interfaccia della riga di comando (CLI). Importazione di file di zona è **non** attualmente supportate tramite Azure PowerShell o hello portale di Azure.

Hello Azure CLI 1.0 è uno strumento da riga di comando multipiattaforma utilizzato per la gestione dei servizi di Azure. È disponibile per le piattaforme Windows, Mac e Linux hello da hello [pagina di download di Azure](https://azure.microsoft.com/downloads/). Supporto multipiattaforma è importante per importare ed esportare file di zona, in quanto hello Nome server del software più comuni, [ASSOCIARE](https://www.isc.org/downloads/bind/), in genere viene eseguito in Linux.

> [!NOTE]
> Esistono attualmente due versioni di hello CLI di Azure. CLI1.0 è basata su Node.js e ha comandi che iniziano con "azure".
> CLI2.0 è basata su Python e ha comandi che iniziano con "az". L'importazione di file di zona è supportata in entrambe le versioni, è consigliabile utilizzare i comandi CLI1.0 hello, come descritto in questa pagina.

## <a name="obtain-your-existing-dns-zone-file"></a>Recupero del file di zona DNS esistente

Prima di importare un file di zona DNS in DNS di Azure, è necessario tooobtain una copia del file di zona hello. Hello origine di questo file dipende da dove zona DNS hello è attualmente ospitato.

* Se la zona DNS è ospitata da un servizio (ad esempio un registrar, un provider di hosting DNS dedicato o provider di cloud alternativi), che il servizio deve fornire il file di zona DNS hello possibilità toodownload hello.
* Se la zona DNS è ospitata il servizio DNS di Windows, cartella di hello predefinita per i file di zona hello è **%systemroot%\system32\dns**. file di zona tooeach Hello percorso Mostra anche su hello **generale** scheda della console DNS hello.
* Se la zona DNS è ospitata usando l'associazione, percorso hello del file di zona hello per ogni zona è specificato nel file di configurazione di binding hello **named. conf**.

> [!NOTE]
> I file di zona scaricati da GoDaddy hanno un formato leggermente non standard. È necessario toocorrect questo prima di importare questi file di zona DNS di Azure.
>
> I nomi DNS in hello RDATA di ogni record DNS vengono specificati come nomi completi, ma che non dispongono di una terminazione "." Ciò significa che vengono interpretati da altri sistemi DNS come nomi relativi. È necessario tooedit hello zona file tooappend hello terminazione "." tootheir nomi prima di importarli in DNS di Azure.
>
> Ad esempio, è necessario modificato troppo record CNAME "www 3600 IN contoso.com CNAME" hello "www 3600 CNAME IN contoso.com."
> con un "." alla fine.

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importare un file di zona DNS in DNS di Azure

L'importazione di un file di zona crea una nuova zona in DNS di Azure se non ne esiste già una. Se esiste già una zona hello, hello set di record nel file di zona hello devono essere uniti con i set di record esistenti hello.

### <a name="merge-behavior"></a>Unione

* Per impostazione predefinita, i set di record nuovi ed esistenti vengono uniti. I record identici all'interno di un set di record unito vengono deduplicati.
* In alternativa, specificando hello `--force` opzione, hello sostituisce processo di importazione il set di record esistente con nuovi set di record. I set di record esistenti che non dispone di un record corrispondente impostato nel file di zona importati hello vengono rimossi.
* Durante l'unione di set di record, hello toolive TTL (time) preesistenti di set di record è utilizzato. Quando `--force` è utilizzato, hello durata (TTL) del set di record nuovo hello viene utilizzato.
* Avvio di parametri di autorità (SOA) (ad eccezione di `host`) vengono sempre ricavate dal file di zona importati hello, indipendentemente dal fatto che `--force` viene utilizzato. Analogamente, per impostare al vertice zona hello record hello del server, hello TTL viene sempre acquisito dal file di zona importati hello.
* Un record CNAME importato non sostituisce un CNAME esistente registrare con stesso nome a meno che non hello hello `--force` parametro specificato.
* Quando si verifica un conflitto tra un record CNAME e un altro record di hello stesso nome ma è diversa, digitare (indipendentemente dal fatto che è esistente o nuova), record esistente hello viene mantenuto. Si tratta indipendentemente dall'utilizzo di hello di `--force`.

### <a name="additional-information-about-importing"></a>Altre informazioni sull'importazione

Hello note seguenti forniscono altri dettagli tecnici sulla zona hello processo di importazione.

* Hello `$TTL` direttiva è facoltativa ed è supportata. Se non si `$TTL` direttiva viene specificata, vengono importati i record senza una durata (TTL) esplicita impostare tooa TTL predefinito di 3600 secondi. Quando due record in stesso set di record hello specificano TTLs diversi, valore inferiore hello viene utilizzato.
* Hello `$ORIGIN` direttiva è facoltativa ed è supportata. Se non si `$ORIGIN` è impostata, predefinito hello valore utilizzato è il nome zona hello come specificato nella riga di comando hello (più terminazione hello ".").
* Hello `$INCLUDE` e `$GENERATE` direttive non sono supportate.
* Sono supportati questi tipi di record: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.
* Hello record SOA viene creato automaticamente da DNS di Azure quando viene creata una zona. Quando si importa un file di zona, tutti i parametri SOA vengono estratti dal file di zona hello *tranne* hello `host` parametro. Questo parametro utilizza il valore di hello fornito dal servizio DNS di Azure. Questo avviene perché questo parametro deve fare riferimento a server dei nomi primario toohello fornite da DNS di Azure.
* record server dei nomi Hello impostato al vertice zona hello viene anche creato automaticamente da DNS di Azure quando si crea la zona hello. Solo hello durata (TTL) di questo set di record viene importato. Questi record contengono nomi di server di nome hello forniti da DNS di Azure. dati del record di Hello non viene sovrascritto da valori hello contenuti nel file di zona importati hello.
* Durante l'anteprima pubblica, DNS di Azure supporta solo i record TXT a stringa singola. Multistringa record TXT sono essere troncati e concatenati too255 caratteri.

### <a name="cli-format-and-values"></a>Valori e formato dell'interfaccia della riga di comando

formato Hello di hello Azure CLI comando tooimport una zona DNS è:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Valori:

* `<resource group>`è il nome di hello hello del gruppo di risorse per la zona hello in DNS di Azure.
* `<zone name>`è il nome di hello della zona di hello.
* `<zone file name>`è hello/nome del percorso toobe file di zona hello importati.

Se una zona con questo nome non esiste nel gruppo di risorse hello, viene creato automaticamente. Se hello zona esiste già, hello set di record importati vengono unite con i set di record esistenti. toooverwrite hello esistente set di record, utilizzare hello `--force` opzione.

formato di hello tooverify di un file di zona senza effettivamente l'importazione, utilizzare hello `--parse-only` opzione.

### <a name="step-1-import-a-zone-file"></a>Passaggio 1. Importare un file di zona

un file di zona per la zona hello tooimport **contoso.com**.

1. Accedi tooyour sottoscrizione di Azure mediante Azure CLI 1.0 hello.

    ```azurecli
    azure login
    ```

2. Selezionare la sottoscrizione di hello in cui si desidera toocreate la nuova zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS di Azure è un servizio di gestione risorse di sola Azure, pertanto hello CLI di Azure deve essere disattivati tooResource modalità di gestione.

    ```azurecli
    azure config mode arm
    ```

4. Prima di utilizzare il servizio di DNS di Azure hello, è necessario registrare il provider di risorse di sottoscrizione toouse hello Network. Questa operazione viene eseguita una sola volta per ogni sottoscrizione.

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Se si non è ancora disponibile, è necessario anche toocreate un gruppo di risorse di gestione risorse.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. zona hello tooimport **contoso.com** dal file hello **contoso.com.txt** in una nuova zona DNS in gruppo di risorse hello **myresourcegroup**, eseguire il comando hello `azure network dns zone import`.<BR>Questo comando consente di caricare il file di zona hello e analizzarlo. comando Hello esegue una serie di comandi nel hello Azure servizio toocreate hello zona e i set di tutti i record di hello nella zona hello. comando Hello segnala lo stato nella finestra di console hello, insieme a eventuali errori o avvisi. Poiché set di record vengono creati in serie, potrebbe richiedere alcuni minuti tooimport un file di zona di grandi dimensioni.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Passaggio 2. Verificare la zona hello

tooverify hello zona DNS dopo aver importato il file hello, è possibile utilizzare uno qualsiasi dei seguenti metodi hello:

* È possibile elencare i record di hello hello comando CLI di Azure seguente:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* È possibile elencare i record di hello tramite i cmdlet di PowerShell hello `Get-AzureRmDnsRecordSet`.
* È possibile utilizzare `nslookup` tooverify risoluzione dei nomi per i record di hello. Poiché la zona hello non delegata ancora, è necessario toospecify hello corretto Azure server dei nomi DNS in modo esplicito. Hello esempio seguente viene illustrato come nomi di server di nome hello tooretrieve assegnati toohello zona. IT illustra anche come tooquery hello "www" registrare tramite `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Passaggio 3. Aggiornare la delega DNS

Dopo aver verificato che la zona hello è stata importata correttamente, è necessario tooupdate hello DNS delega toopoint toohello server dei nomi DNS di Azure. Per ulteriori informazioni, vedere l'articolo hello [Aggiorna delega DNS hello](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Esportare un file di zona DNS da DNS di Azure

formato Hello di hello Azure CLI comando tooimport una zona DNS è:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Valori:

* `<resource group>`è il nome di hello hello del gruppo di risorse per la zona hello in DNS di Azure.
* `<zone name>`è il nome di hello della zona di hello.
* `<zone file name>`è hello/nome del percorso toobe file di zona hello esportata.

Come con l'importazione di zona hello, è innanzitutto necessario toosign in, scegliere la sottoscrizione e configurare la modalità di gestione risorse di hello Azure CLI toouse.

### <a name="tooexport-a-zone-file"></a>tooexport un file di zona

1. Accedi tooyour sottoscrizione di Azure tramite hello CLI di Azure.

    ```azurecli
    azure login
    ```

2. Selezionare la sottoscrizione di hello in cui si desidera toocreate la zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS di Azure è un servizio solo di Gestione risorse di Azure. Hello CLI di Azure deve essere disattivati tooResource modalità di gestione.

    ```azurecli
    azure config mode arm
    ```

4. zona DNS di Azure esistente di hello tooexport **contoso.com** nel gruppo di risorse **myresourcegroup** toohello file **contoso.com.txt** (in hello cartella corrente), eseguire `azure network dns zone export`. Questo comando chiama hello tooenumerate servizio DNS di Azure set di record nella zona hello ed esportare file di zona hello risultati tooa compatibile con associazione.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
