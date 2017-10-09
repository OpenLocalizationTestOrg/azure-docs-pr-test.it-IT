---
title: aaaAzure servizio metadati dell'istanza per le macchine virtuali Linux | Documenti Microsoft
description: Interfaccia REST tooget informazioni di Linux VM calcolo, rete e gli eventi di manutenzione programmata.
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a>Servizio metadati dell'istanza di Azure per macchine virtuali Linux


Hello Azure servizio metadati dell'istanza vengono fornite informazioni sull'esecuzione di istanze di macchine virtuali che possono essere utilizzati toomanage e configurare le macchine virtuali.
Le informazioni includono ad esempio SKU, configurazione di rete ed eventi di manutenzione previsti. Per altre informazioni sul tipo di informazioni disponibili, vedere le [categorie di metadati](#instance-metadata-data-categories).

Servizio metadati dell'istanza di Azure è un Endpoint REST accessibile tooall le macchine virtuali IaaS creati tramite hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). endpoint Hello è disponibile all'indirizzo IP non instradabile ben noto (`169.254.169.254`) che sono accessibili solo da hello macchina virtuale.

> [!IMPORTANT]
> Questo servizio è **disponibile a livello generale** nelle aree globali di Azure. È in anteprima pubblica per il cloud di Azure Germania, per la Cina e per enti pubblici. Riceve regolarmente gli aggiornamenti tooexpose nuove informazioni sulle istanze di macchine virtuali. Questa pagina riflette hello aggiornata [categorie di dati](#instance-metadata-data-categories) disponibili.

## <a name="service-availability"></a>Disponibilità del servizio
servizio di Hello è disponibile in tutte le aree di Azure globale disponibile a livello generale. servizio Hello è in anteprima pubblica in aree di hello per enti pubblici, Cina o Germania.

Regioni                                        | Disponibilità
-----------------------------------------------|-----------------------------------------------
[Tutte le aree globali di Azure con disponibilità a livello generale](https://azure.microsoft.com/regions/)     | Disponibile a livello generale 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | In anteprima 
[Azure per la Cina](https://www.azure.cn/)                                                           | In anteprima
[Azure Germania](https://azure.microsoft.com/overview/clouds/germany/)                    | In anteprima

Questa tabella viene aggiornata quando diventa disponibile il servizio hello in altri cloud di Azure.

tootry out hello servizio metadati dell'istanza, creare una macchina virtuale da [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) o hello [portale di Azure](http://portal.azure.com) in hello sopra le aree e seguire hello esempi seguenti.

## <a name="usage"></a>Utilizzo

### <a name="versioning"></a>Controllo delle versioni
Hello servizio metadati dell'istanza viene creata. Le versioni sono obbligatorie e la versione corrente di hello è `2017-04-02`.

> [!NOTE] 
> Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version. Questo formato non è più supportato e verrà rimossa in futuro hello.

Quando si aggiungono versioni più recenti, quelle precedenti sono comunque accessibili per la compatibilità, se gli script presentano dipendenze in formati di dati specifici. Si noti tuttavia che version(2017-03-01) anteprima corrente hello potrebbe non essere disponibile quando il servizio di hello è disponibile a livello generale.

### <a name="using-headers"></a>Uso delle intestazioni
Quando si eseguono query hello servizio metadati dell'istanza, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.

### <a name="retrieving-metadata"></a>Recupero dei metadati

I metadati dell'istanza sono disponibili per l'esecuzione di macchine virtuali create e gestite tramite [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Accedere a tutte le categorie di dati per un'istanza di macchina virtuale utilizzando hello seguito richiesta:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Tutte le query dei metadati dell'istanza fanno distinzione tra maiuscole e minuscole.

### <a name="data-output"></a>Output dei dati
Per impostazione predefinita, servizio metadati dell'istanza di hello restituisce i dati in formato JSON (`Content-Type: application/json`). Tuttavia, API diverse possono restituire dati in formati diversi se necessario.
Hello nella tabella seguente è un riferimento di altri formati di dati che potrebbero supportare le API.

API | Formato dati predefinito | Altri formati
--------|---------------------|--------------
/instance | json | text
/scheduledevents | json | Nessuno

tooaccess un formato di risposta non predefinito, specificare il formato richiesto di hello come parametro querystring nella richiesta di hello. ad esempio:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Sicurezza
endpoint di servizio metadati dell'istanza di Hello è accessibile solo dall'interno hello esegue l'istanza di macchina virtuale in un indirizzo IP non è instradabile. Inoltre, qualsiasi richiesta con un `X-Forwarded-For` intestazione viene rifiutata dal servizio hello.
È inoltre necessario richieste toocontain un `Metadata: true` tooensure intestazione che hello richiesta effettiva è stata direttamente previsto e che non fa parte di reindirizzamento non intenzionale. 

### <a name="error"></a>Errore
Se è presente un elemento di dati non trovato o una richiesta in formato non corretto, hello servizio metadati dell'istanza restituisce errori HTTP standard. ad esempio:

Codice di stato HTTP | Motivo
----------------|-------
200 - OK |
400 - Richiesta non valida | Intestazione `Metadata: true` mancante
404 - Non trovato | esistere Hello quando elemento richiesto 
405 - Metodo non consentito | Sono supportate solo le richieste `GET` e `POST`
429 - Numero eccessivo di richieste | l'API di Hello attualmente supporta un massimo di 5 query al secondo
500 - Errore del servizio     | Ripetere l'operazione in un secondo momento

### <a name="examples"></a>esempi

> [!NOTE] 
> Tutte le risposte delle API sono stringhe JSON. Tutte le risposte di esempio che seguono sono di tipo pretty-print per una migliore leggibilità.

#### <a name="retrieving-network-information"></a>Recupero delle informazioni di rete

**Richiesta**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Risposta**

> [!NOTE] 
> risposta Hello è una stringa JSON. Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Recupero dell'indirizzo IP pubblico

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Recupero di tutti i metadati per un'istanza

**Richiesta**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Risposta**

> [!NOTE] 
> risposta Hello è una stringa JSON. Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Recupero dei metadati in una macchina virtuale Windows

**Richiesta**

I metadati dell'istanza possono essere recuperati in Windows tramite l'utilità di PowerShell hello `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

O tramite hello `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Risposta**

> [!NOTE] 
> risposta Hello è una stringa JSON. Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Categorie di dati dei metadati dell'istanza
Hello seguenti categorie di dati sono disponibile tramite hello servizio metadati dell'istanza:

Dati | Descrizione
-----|------------
location | Hello area Azure VM è in esecuzione in
name | Nome della macchina virtuale hello 
offer | Offrono informazioni per l'immagine di macchina virtuale hello. Questo valore è presente solo per le immagini distribuite dalla raccolta di immagini di Azure.
publisher | Server di pubblicazione dell'immagine di macchina virtuale hello
sku | SKU specifico per l'immagine di macchina virtuale hello  
version | Versione dell'immagine di macchina virtuale hello 
osType | Linux o Windows 
platformUpdateDomain |  [Dominio di aggiornamento](manage-availability.md) hello macchina virtuale è in esecuzione in
platformFaultDomain | [Dominio di errore](manage-availability.md) hello macchina virtuale è in esecuzione in
vmId | [Identificatore univoco](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) per hello VM
vmSize | [Dimensioni macchina virtuale](sizes.md)
ipv4/privateIpAddress | Indirizzo IPv4 locale di hello VM 
ipv4/publicIpAddress | Indirizzo IPv4 pubblico di hello VM
subnet/address | Indirizzo di subnet di hello VM
subnet/prefix | Prefisso della subnet, ad esempio 24
ipv6/ipAddress | Indirizzo IPv6 locale di hello VM
macAddress | Indirizzo mac della macchina virtuale 
scheduledevents | Attualmente in anteprima pubblica. Vedere [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Scenari di utilizzo di esempio  

### <a name="tracking-vm-running-on-azure"></a>Rilevamento della macchina virtuale in esecuzione in Azure

Come provider di servizi, potrebbe essere necessario numero hello tootrack delle macchine virtuali in esecuzione il software o gli agenti necessari tootrack l'univocità di hello VM. toobe in grado di tooget un ID univoco per una macchina virtuale, utilizzare hello `vmId` campo servizio metadati dell'istanza.

**Richiesta**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Risposta**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Posizionamento di contenitori, dominio di aggiornamento/errore basato su partizioni dati 

Per alcuni scenari, il posizionamento di repliche dati diverse è di importanza primaria. Ad esempio, [posizionamento delle repliche HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) o la selezione host contenitore tramite un [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) richieda è hello tooknow `platformFaultDomain` e `platformUpdateDomain` hello macchina virtuale è in esecuzione in.
È possibile ottenere i dati direttamente tramite hello servizio metadati dell'istanza.

**Richiesta**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Risposta**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Ulteriori informazioni su hello VM durante il caso di supporto 

Come provider di servizi, si potrebbero ottenere una chiamata al supporto in cui si desidera tooknow ulteriori informazioni sulla macchina virtuale hello. Porre hello cliente tooshare hello calcolo metadati possono fornire informazioni di base per hello supporto professionale tooknow su tipo hello della macchina virtuale in Azure. 

**Richiesta**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Risposta**

> [!NOTE] 
> risposta Hello è una stringa JSON. Hello risposta di esempio seguente viene stampato per migliorare la leggibilità.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Esempi di chiamate del servizio di metadati utilizzando diversi linguaggi all'interno di hello VM 

Lingua | Esempio 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb
Go Lan   | https://github.com/Microsoft/azureimds/blob/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py
C++      | https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs
JavaScript | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh
    

## <a name="faq"></a>domande frequenti
1. Viene visualizzato l'errore hello `400 Bad Request, Required metadata header not specified`. Che cosa significa?
   * Servizio metadati dell'istanza di Hello richiede intestazione hello `Metadata: true` toobe passato nella richiesta di hello. Il passaggio di questa intestazione nella chiamata REST hello consente accesso toohello servizio metadati dell'istanza. 
2. Perché non riesco a ottenere le informazioni di calcolo per la macchina virtuale?
   * Hello servizio metadati dell'istanza supporta attualmente solo le istanze create con Azure Resource Manager. In hello future, si potrebbe aggiungere supporto per le macchine virtuali del servizio Cloud.
3. Ho creato la mia macchina virtuale tramite Azure Resource Manager tempo fa. Perché non riesco a vedere le informazioni sui metadati di calcolo?
   * Per tutte le macchine virtuali create dopo settembre 2016, aggiungere un [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart vedere calcolo metadati. Per macchine virtuali meno recenti (Create prima di settembre 2016), aggiungere o rimuovere estensioni o dati dischi toohello VM toorefresh metadati.
4. Perché viene visualizzato errore hello `500 Internal Server Error`?
   * Inviare di nuovo la richiesta basata sul sistema di backoff esponenziale. Se il problema di hello persiste, contattare il supporto tecnico di Azure.
5. Dove posso condividere domande o commenti aggiuntivi?
   * Inviare i propri commenti accedendo alla pagina http://feedback.azure.com.
7. Il servizio funziona per l'istanza del set di scalabilità di macchine virtuali?
   * Sì, il Servizio metadati è disponibile per le istanze del set di scalabilità. 
6. Come ottenere supporto per il servizio hello?
   * supporto tooget per il servizio di hello, creare un problema di supporto nel portale di Azure per la macchina virtuale in cui non si risposta dei metadati in grado di tooget dopo tentativi lunghi hello 

   ![Supporto per i metadati dell'istanza](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni su hello [agli eventi pianificati](scheduled-events.md) API **in anteprima pubblica** fornita da servizio metadati dell'istanza di hello.
