---
title: Calcolo aaaAzure - estensione diagnostica per Linux | Documenti Microsoft
description: "La modalità tooconfigure hello metriche toocollect Azure Linux diagnostica estensione (LAD) e registrare eventi da macchine virtuali Linux in esecuzione in Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Utilizzare i registri e le metriche toomonitor estensione diagnostica per Linux

Questo documento descrive versione 3.0 e successive di hello estensione diagnostica per Linux.

> [!IMPORTANT]
> Per informazioni sulla versione 2.3 e precedenti, vedere [questo documento](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Introduzione

Estensione diagnostica per Linux Hello consente un utente monitoraggio hello integrità di una VM Linux in esecuzione in Microsoft Azure. Dispone di hello seguenti funzionalità:

* Raccoglie le metriche delle prestazioni del sistema da hello VM e li archivia in una tabella specifica in un account di archiviazione designate.
* Recupera la registrazione degli eventi dal Registro di sistema e li archivia in una tabella specifica in hello designato account di archiviazione.
* Consente la metrica utenti toocustomize hello dati venga raccolti e caricata.
* Abilita funzioni syslog hello toocustomize di utenti e i livelli di gravità degli eventi che vengono raccolti e caricati.
* Consente agli utenti tooupload log specificato file tooa designato archiviazione tabella.
* Supporta l'invio delle metriche e log eventi tooarbitrary EventHub gli endpoint e i BLOB in formato JSON in hello definito account di archiviazione.

Questa estensione funziona con entrambi i modelli di distribuzione di Azure.

## <a name="installing-hello-extension-in-your-vm"></a>L'installazione dell'estensione hello nella macchina virtuale

È possibile abilitare questa estensione tramite il cmdlet di Azure PowerShell hello, script CLI di Azure o i modelli di distribuzione di Azure. Per altre informazioni, vedere [Funzionalità delle estensioni](./extensions-features.md).

Hello portale di Azure non può essere tooenable utilizzati oppure configurare LAD 3.0. ma esso stesso installa e configura la versione 2.3. Avvisi e i grafici del portale di azure funzionano con i dati di entrambe le versioni dell'estensione hello.

Le istruzioni di installazione e la [configurazione di esempio scaricabile](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurano LAD 3.0 per:

* acquisire e archiviare hello stesse metriche come sono stati forniti da 2.3 LAD;
* acquisire un set di metriche di sistema di file, nuovo tooLAD 3.0; utile
* acquisire l'insieme di syslog predefinito hello abilitata da 2.3 LAD;
* abilitare hello esperienza del portale di Azure per la creazione di grafici e avvisi sulle metriche di macchina virtuale.

configurazione scaricabile Hello è solo un esempio; modificarlo toosuit le proprie esigenze.

### <a name="prerequisites"></a>Prerequisiti

* **Agente Linux di Azure 2.2.0 o versione successiva**. La maggior parte delle immagini della raccolta Linux di macchine virtuali di Azure include la versione 2.2.7 o successive. Eseguire `/usr/sbin/waagent -version` tooconfirm hello versione hello macchina virtuale. Se hello macchina virtuale è in esecuzione una versione precedente dell'agente guest hello, seguire [queste istruzioni](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate è.
* **Interfaccia della riga di comando di Azure**. [Impostare hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente nel computer.
* Hello wget comando, se si dispone già: eseguire `sudo apt-get install wget`.
* Una sottoscrizione di Azure esistente e una risorsa di archiviazione esistente all'interno dell'account dati hello toostore.

### <a name="sample-installation"></a>Installazione di esempio

Compilare i parametri corretti hello in hello prime tre righe, quindi eseguire lo script come radice:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

Hello URL per la configurazione di esempio hello e il relativo contenuto è toochange soggetto. Scaricare una copia del file JSON di impostazioni del portale hello e personalizzarlo per le proprie esigenze. Qualsiasi modello o automazione creato dall'utente deve usare la propria copia, invece di scaricare l'URL ogni volta.

### <a name="updating-hello-extension-settings"></a>L'aggiornamento delle impostazioni di estensione hello

Dopo aver modificato il protetti o le impostazioni pubbliche, distribuire le VM toohello eseguendo hello stesso comando. Se qualsiasi elemento modificata nelle impostazioni di hello, impostazioni hello aggiornato vengono inviate toohello estensione. LAD ricaricamenti configurazione hello e riavviato.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migrazione da versioni precedenti di estensione hello

Hello la versione più recente dell'estensione hello è **3.0**. **Le versioni precedenti (2.x) sono deprecate e la loro pubblicazione potrebbe essere annullata a partire dal 31 luglio 2018**.

> [!IMPORTANT]
> Questa estensione è stata introdotta configurazione toohello modifiche di rilievo dell'estensione hello. Una di queste modifiche è stata effettuata sicurezza hello tooimprove di estensione hello. di conseguenza, la compatibilità con 2. x potrebbe non essere mantenuta. Inoltre, hello estensione server di pubblicazione per questa estensione è diverso dal server di pubblicazione hello per le versioni 2. x hello.
>
> toomigrate da 2. x toothis nuova versione dell'estensione di hello, è necessario disinstallare l'estensione precedente di hello (nel nome di server di pubblicazione hello precedente), quindi installare la versione 3 di estensione hello.

Consigli:

* Installare l'estensione di hello con l'aggiornamento di versione secondaria automatico abilitato.
  * Nel modello di distribuzione classica le macchine virtuali, specificare '3.*' come versione di hello se si sta installando l'estensione hello tramite Azure XPLAT CLI o Powershell.
  * Distribuzione di gestione risorse di Azure le macchine virtuali del modello, includere ' "autoUpgradeMinorVersion": true' nel modello di distribuzione VM hello.
* Usare un account di archiviazione nuovo o diverso per LAD 3.0. Esistono diverse piccole incompatibilità tra LAD 2.3 e LAD 3.0 che creano problemi nella condivisione di un account:
  * LAD 3.0 inserisce gli eventi SysLog in una tabella con un nome diverso.
  * le stringhe per counterSpecifier Hello `builtin` metriche differiscono LAD 3.0.

## <a name="protected-settings"></a>Impostazioni protette

Questo set di informazioni per la configurazione contiene informazioni riservate che devono essere protette dalla visualizzazione pubblica, ad esempio, le credenziali di archiviazione. Queste impostazioni sono trasmessi tooand archiviati dall'estensione hello in forma crittografata.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nome | Valore
---- | -----
storageAccountName | nome Hello hello dell'account di archiviazione in cui i dati vengono scritti dall'estensione hello.
storageAccountEndPoint | endpoint (facoltativo) hello identificazione cloud hello in cui hello esiste l'account di archiviazione. Se questa impostazione è assente, LAD predefinito toohello cloud pubblico di Azure, `https://core.windows.net`. toouse un account di archiviazione in Azure in Germania, Azure per enti pubblici o Azure China, imposta questo valore di conseguenza.
storageAccountSasToken | Un [token SAS Account](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) per i servizi Blob e tabella (`ss='bt'`), applicabile toocontainers e oggetti (`srt='co'`), che aggiungono, creare, elencare, aggiornare e le autorizzazioni di scrittura (`sp='acluw'`). Eseguire *non* includono hello iniziali punto interrogativo (?).
mdsdHttpProxy | (facoltativo) HTTP proxy informazioni necessarie tooenable hello estensione tooconnect toohello specificato l'account di archiviazione e l'endpoint.
sinksConfig | (facoltativo) I dettagli di metriche toowhich destinazioni alternative e gli eventi possono essere recapitati. dettagli specifici di Hello di ogni sink dati supportata dall'estensione hello vengono trattati nelle sezioni hello che seguono.

È possibile creare facilmente token SAS hello necessarie tramite hello portale di Azure.

1. Selezionare toowhich account di archiviazione generico hello desiderato hello estensione toowrite
1. Selezionare "Firma di accesso condiviso" da parte di impostazioni hello del menu a sinistra di hello
1. Assicurarsi di sezioni di hello appropriate come descritte in precedenza
1. Fare clic su hello "Generare SAS".

![immagine](./media/diagnostic-extension/make_sas.png)

Hello di copia generato SAS nel campo storageAccountSasToken hello; rimuovere hello iniziali punto interrogativo ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Questa sezione facoltativa definisce le destinazioni aggiuntive estensione hello toowhich invia informazioni hello che raccoglie. Matrice di Hello "sink" contiene un oggetto per ogni sink dati aggiuntivi. attributo "tipo" determina Hello hello altri attributi nell'oggetto hello.

Elemento | Valore
------- | -----
name | Sink di toothis toorefer altrove nella configurazione dell'estensione hello è utilizzata una stringa.
type | tipo di Hello del sink da definire. Determina hello altri valori (se presente) in istanze di questo tipo.

La versione 3.0 di hello estensione diagnostica per Linux supporta due tipi di sink: EventHub e JsonBlob.

#### <a name="hello-eventhub-sink"></a>sink di EventHub Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

voce "sasURL" Hello contiene hello URL completo, incluso il token di firma di accesso condiviso, per hello dati toowhich Hub eventi deve essere pubblicata. LAD richiede una firma di accesso condiviso denominazione di un criterio che consente l'attestazione di trasmissione hello. Esempio:

* Creare uno spazio dei nomi dell'hub eventi denominato `contosohub`
* Creare un Hub eventi nello spazio dei nomi hello chiamato`syslogmsgs`
* Creare un criterio di accesso condiviso in Hub eventi denominato hello `writer` che abilita hello attestazione di trasmissione

Se è stata creata una firma di accesso condiviso valida fino a mezzanotte UTC del 1 ° gennaio 2018, potrebbe essere il valore di sasURL hello:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Per altre informazioni sulla generazione di token SAS per gli hub eventi, vedere [questa pagina Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>sink JsonBlob Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Dati indirizzati tooa JsonBlob sink vengono archiviati in BLOB in archiviazione di Azure. Ogni istanza di LAD crea un BLOB all'ora per ogni nome di sink. Ciascun BLOB contiene sempre una matrice JSON sintatticamente valida dell'oggetto. Le nuove voci vengono aggiunti in modo atomico toohello matrice. BLOB vengono archiviati in un contenitore con stesso nome come sink hello hello. Hello regole di archiviazione di Azure per i nomi dei contenitori blob applicare toohello nomi di sink JsonBlob: tra 3 e 63 caratteri ASCII alfanumerici minuscoli o trattini.

## <a name="public-settings"></a>Impostazioni pubbliche

Questa struttura contiene diversi blocchi di impostazioni che controllano i dati raccolti dall'estensione hello hello. Tutte le impostazioni sono facoltative. Se si specifica `ladCfg`, è necessario specificare anche `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Elemento | Valore
------- | -----
StorageAccount | nome Hello hello dell'account di archiviazione in cui i dati vengono scritti dall'estensione hello. Deve essere hello stesso nome specificato nella hello [protetto impostazioni](#protected-settings).
mdsdHttpProxy | (facoltativo) Stessa descrizione disponibile hello [protetto impostazioni](#protected-settings). valore pubblica Hello viene sottoposto a override dal valore private hello, se impostata. Inserire le impostazioni proxy che contengono un segreto, ad esempio una password, in hello [protetto impostazioni](#protected-settings).

gli elementi rimanenti Hello sono descritti in dettaglio nelle sezioni che seguono hello.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Sink di questa raccolta di hello controlli struttura facoltativo di metriche e i registri per toohello di recapito dei dati di servizio e tooother le metriche di Azure. È necessario specificare `performanceCounters` o `syslogEvents` oppure entrambi. È necessario specificare hello `metrics` struttura.

Elemento | Valore
------- | -----
eventVolume | (facoltativo) Controlli hello numero di partizioni create all'interno di tabella di archiviazione hello. Può essere uno tra `"Large"`, `"Medium"` o `"Small"`. Se non specificato, il valore di predefinito hello è `"Medium"`.
sampleRateInSeconds | intervallo predefinito di hello (facoltativo) tra raccolta della metrica (non aggregata) non elaborata. frequenza di campionamento Hello più piccola supportata è 15 secondi. Se non specificato, il valore di predefinito hello è `15`.

#### <a name="metrics"></a>Metriche

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Elemento | Valore
------- | -----
resourceId | ID di risorsa di gestione risorse di Azure di Hello di hello macchina virtuale o di scalabilità della macchina virtuale hello impostare hello toowhich che VM appartiene. Questa impostazione deve essere specificato anche se qualsiasi sink JsonBlob viene utilizzata nella configurazione di hello.
scheduledTransferPeriod | frequenza di Hello in cui le metriche di aggregazione sono toobe calcolata e trasferiti tooAzure metriche, espresso come un intervallo di tempo è 8601. periodo di trasferimento più piccolo Hello è 60 secondi, ovvero PT1M. È necessario specificare almeno un scheduledTransferPeriod.

Esempi di hello metriche specificate nella sezione performanceCounters hello vengono raccolti ogni 15 secondi o frequenza di campionamento hello definito in modo esplicito per il contatore hello. Se più frequenze scheduledTransferPeriod visualizzato (come esempio hello), ogni aggregazione viene calcolato in modo indipendente.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Questa sezione facoltativa controlla raccolta hello della metrica. Gli esempi non elaborati vengono aggregati per ogni [scheduledTransferPeriod](#metrics) tooproduce questi valori:

* mean
* minimum
* maximum
* ultimo valore raccolto
* numero di campioni non elaborati usato aggregazione hello toocompute

Elemento | Valore
------- | -----
sinks | (facoltativo) Un elenco delimitato da virgole di nomi di sink toowhich che LAD invia i risultati di metrica aggregati. Tutte le metriche aggregate sono pubblicati tooeach elencati sink. Vedere [sinksConfig](#sinksconfig). Esempio: `"EHsink1, myjsonsink"`.
type | Identifica hello provider effettivo della metrica hello.
class | Insieme a "counter", identifica metrica specifica di hello nello spazio dei nomi del provider di hello.
counter | Insieme a "class", identifica metrica specifica di hello nello spazio dei nomi del provider di hello.
counterSpecifier | Identifica una metrica specifica di hello nello spazio dei nomi Azure metriche hello.
condition | (facoltativo) Consente di selezionare un'istanza specifica di metrica di hello toowhich oggetto hello applica o seleziona hello aggregazione in tutte le istanze di tale oggetto. Per ulteriori informazioni, vedere hello [ `builtin` le definizioni delle metriche](#metrics-supported-by-builtin).
sampleRate | È l'intervallo 8601 che imposta la frequenza di hello in cui vengono raccolti degli esempi non elaborati per la metrica. Se non è impostata, l'intervallo di raccolta hello è impostata dal valore hello di [sampleRateInSeconds](#ladcfg). frequenza di campionamento supportata più breve Hello è 15 secondi (PT15S).
unit | Deve essere una delle seguenti stringhe: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond". Definisce l'unità di hello metrica hello. Consumer di dati raccolti hello prevedere hello raccolti dati valori toomatch questa unità. LAD ignora questo campo.
displayName | Hello etichetta (in lingua hello specificata dalle impostazioni locali associato di hello impostazione) toobe collegato toothis dati di metrica di Azure. LAD ignora questo campo.

counterSpecifier Hello è un identificatore arbitrario. I consumer di dati di metrica, ad esempio hello grafici portale Azure e avviso di funzionalità, utilizzano counterSpecifier come hello "key" che identifica una metrica o un'istanza di una metrica. Per le metriche `builtin`, è consigliabile usare i valori di counterSpecifier che iniziano con `/builtin/`. Se si raccolgono un'istanza di una metrica specifica, è consigliabile che allegare identificatore hello del valore di counterSpecifier toohello istanza hello. Di seguito sono riportati alcuni esempi:

* `/builtin/Processor/PercentIdleTime` - Tempo di inattività medio calcolato per tutti i core
* `/builtin/Disk/FreeSpace(/mnt)`-Spazio per hello /mnt filesystem
* `/builtin/Disk/FreeSpace` - Spazio libero medio calcolato per tutti i file system montati

LAD né hello portale di Azure prevede hello counterSpecifier valore toomatch qualsiasi criterio di ricerca. È consigliabile essere coerenti durante la creazione dei valori di counterSpecifier.

Quando si specifica `performanceCounters`, LAD scrive sempre tabella tooa dati nell'archiviazione di Azure. È possibile avere hello stesso dati scritti tooJSON BLOB e/o hub eventi, ma non è possibile disabilitare l'archiviazione tabella tooa di dati. Tutte le istanze di hello estensione diagnostica configurato toouse hello stesso account di archiviazione con nome e l'endpoint aggiungere toohello i registri e le metriche stessa tabella. Se la scrittura di un numero eccessivo di macchine virtuali toohello stessa partizione della tabella, Azure può limitare scrive toothat partizione. Hello eventVolume impostazione cause voci toobe distribuite su 1 (piccola), 10 (Media) o 100 partizioni diverse (grande). In genere, "Medium" è sufficiente tooensure traffico non è limitato. funzionalità di Azure metriche Hello di hello portale di Azure utilizza i dati di hello grafici tooproduce tabella o tootrigger avvisi. nome della tabella Hello è la concatenazione di hello di queste stringhe:

* `WADMetrics`
* Hello "scheduledTransferPeriod" per hello aggregati i valori archiviati nella tabella hello
* `P10DV2S`
* Una data nel formato hello "Aaaammgg", che modifica ogni 10 giorni

Gli esempi includono `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Questa sezione facoltativa controlla raccolta hello di eventi dal Registro di sistema. Se la sezione hello viene omesso, è possibile che gli eventi syslog non vengono acquisiti affatto.

raccolta syslogEventConfiguration Hello ha una voce per ogni funzione syslog di interesse. Se minSeverity è "NONE" per una particolare caratteristica o se tale funzionalità è presente nell'elemento hello, non viene acquisito nessun evento da tale struttura.

Elemento | Valore
------- | -----
sinks | Un elenco delimitato da virgole di nomi di sink toowhich singolo registro eventi vengono pubblicati. Tutti gli eventi di registro corrispondenti restrizioni hello in syslogEventConfiguration sono pubblicati tooeach elencati sink. Esempio: "EHforsyslog"
facilityName | Un nome dell'impianto SysLog, ad esempio "LOG\_USER" o "LOG\_LOCAL0". Sezione "funzionalità" hello di hello [pagina man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) per l'elenco completo di hello.
minSeverity | Un livello di gravità SysLog, ad esempio "LOG\_ERR" o "LOG\_INFO". Sezione "livello" hello di hello [pagina man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) per l'elenco completo di hello. estensione Hello acquisisce gli eventi inviati toohello funzionalità in o sopra hello specificato livello.

Quando si specifica `syslogEvents`, LAD scrive sempre tabella tooa dati nell'archiviazione di Azure. È possibile avere hello stesso dati scritti tooJSON BLOB e/o hub eventi, ma non è possibile disabilitare l'archiviazione tabella tooa di dati. Hello partizionamento per questa tabella è hello uguali a quelli descritti per `performanceCounters`. nome della tabella Hello è la concatenazione di hello di queste stringhe:

* `LinuxSyslog`
* Una data nel formato hello "Aaaammgg", che modifica ogni 10 giorni

Gli esempi includono `LinuxSyslog20170410` e `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Questa sezione facoltativa consente di controllare l'esecuzione delle query arbitrarie [OMI](https://github.com/Microsoft/omi).

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Elemento | Valore
------- | -----
namespace | (facoltativo) hello OMI dello spazio dei nomi all'interno delle quali hello query deve essere eseguita. Se non viene specificato, hello predefinita è "root/scx", implementata da hello [provider multipiattaforma di System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Hello OMI query toobe eseguita.
tabella | tabella di archiviazione di Azure, hello (facoltativo) hello designato account di archiviazione (vedere [protetto impostazioni](#protected-settings)).
frequency | numero di hello (facoltativo) di secondi tra l'esecuzione di query hello. Il valore predefinito è 300, ovvero 5 minuti; il valore minimo è 15 secondi.
sinks | (facoltativo) Pubblicare un elenco delimitato da virgole di nomi di risultati di metrica del sink aggiuntive toowhich campione non elaborato. Nessuna aggregazione di questi esempi non elaborati viene calcolata per estensione hello o per le metriche di Azure.

È necessario specificare "table" o "sink" o entrambi.

### <a name="filelogs"></a>fileLogs

Hello controlli acquisizione di file di log. LAD acquisisce di nuove righe di testo quando vengono scritti i file toohello e li scrive tootable righe e/o qualsiasi sink specificato (JsonBlob o EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Elemento | Valore
------- | -----
file | percorso completo di Hello di hello log file toobe controllata e acquisiti. Hello pathname deve essere un singolo file, il nome Impossibile denominare una directory o i caratteri jolly.
tabella | tabella di archiviazione di Azure hello (facoltativo), nel servizio di archiviazione hello designato account (come specificato nella configurazione hello protetto), in cui le nuove righe da hello "tail" del file hello vengono scritte.
sinks | (facoltativo) Un elenco delimitato da virgole di nomi delle righe di log aggiuntivi sink toowhich inviato.

È necessario specificare "table" o "sink" o entrambi.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Metriche supportate dal provider builtin hello

provider di metrica builtin Hello è un'origine di metriche più interessanti tooa ampio gruppo di utenti. Queste metriche sono suddivise in cinque grandi categorie:

* Processore
* Memoria
* Rete
* File system
* Disco

### <a name="builtin-metrics-for-hello-processor-class"></a>metriche Builtin per hello classe del processore

classe del processore delle metriche Hello fornisce informazioni sull'utilizzo del processore in hello VM. Quando si aggregano le percentuali, il risultato di hello è Media hello per tutte le CPU. In una macchina virtuale di core due, se un core è stato occupato al 100% e altri hello è inattiva, al 100% hello segnalati che percentidletime sarà 50. Se il 50% di disponibilità per ogni core hello stesso periodo, hello segnalati risultato sarebbe inoltre 50. In una macchina virtuale, a quattro core con uno dei core occupato al 100% e hello altri inattivo, hello segnalato che percentidletime sarebbe 75.

counter | Significato
------- | -------
PercentIdleTime | Percentuale di tempo durante la finestra di aggregazione hello processori erano in esecuzione il ciclo inattivo di hello kernel
PercentProcessorTime | Percentuale di tempo di esecuzione di un thread non inattivo
PercentIOWaitTime | Percentuale di tempo di attesa per toocomplete di operazioni dei / o
PercentInterruptTime | Percentuale di tempo per l'esecuzione di DPC, ovvero chiamate di procedura differite, e interruzioni di hardware o software
PercentUserTime | Tempo di inattività durante la finestra di aggregazione hello, hello percentuale di tempo impiegato per l'utente più con priorità normale
PercentNiceTime | Tempo di inattività, hello percentuale impiegato per una priorità (nice)
PercentPrivilegedTime | Tempo di inattività, hello percentuale impiegato in modalità privilegiata (kernel)

Hello primi quattro contatori devono sommare too100%. Hello ultima tre contatori anche somma too100%. essi suddividere somma hello PercentProcessorTime PercentIOWaitTime e PercentInterruptTime.

impostare una singola misura aggregata su tutti i processori, tooobtain `"condition": "IsAggregate=TRUE"`. tooobtain una metrica per un processore specifico, ad esempio hello secondo processore di un tipo di quattro core VM, impostare `"condition": "Name=\\"1\\""`. I numeri dei processori logici sono nell'intervallo di hello `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>metriche Builtin per hello classe memoria

classe di memoria delle metriche Hello fornisce informazioni sull'utilizzo della memoria, spostamento e lo scambio.

counter | Significato
------- | -------
AvailableMemory | Memoria fisica disponibile in MiB
PercentAvailableMemory | Percentuale della memoria totale che indica la memoria fisica disponibile
UsedMemory | Memoria fisica in uso (MiB)
PercentUsedMemory | Percentuale della memoria totale che indica la memoria fisica in uso
PagesPerSec | Paging totale (lettura/scrittura)
PagesReadPerSec | Pagine lette dall'archivio di backup, ad esempio file di scambio, file di programma, file mappato e così via.
PagesWrittenPerSec | Pagine scritte toobacking archiviano (file di scambio, il file mappato e così via)
AvailableSwap | Spazio di swapping inutilizzato (MiB)
PercentAvailableSwap | Percentuale dello swapping totale che indica lo spazio di swapping inutilizzato
UsedSwap | Spazio di swapping in uso (MiB)
PercentUsedSwap | Percentuale dello swapping totale che indica lo spazio di swapping in uso

Questa classe di metriche presenta una singola istanza. attributo "condizione" Hello non è disponibili impostazioni utili e deve essere omessa.

### <a name="builtin-metrics-for-hello-network-class"></a>metriche Builtin per hello classe rete

Hello classe delle metriche di rete fornisce informazioni sulle attività di rete su un interfacce di rete singoli dall'avvio. LAD non espone le metriche relative alla larghezza di banda, che possono essere recuperate dalle metriche dell'host.

counter | Significato
------- | -------
BytesTransmitted | Byte totali inviati sin dall'avvio
BytesReceived | Byte totali ricevuti sin dall'avvio
BytesTotal | Byte totali inviati o ricevuti sin dall'avvio
PacketsTransmitted | Pacchetti totali inviati sin dall'avvio
PacketsReceived | Pacchetti totali ricevuti sin dall'avvio
TotalRxErrors | Numero di errori di ricezione sin dall'avvio
TotalTxErrors | Numero di errori di trasmissione sin dall'avvio
TotalCollisions | Numero di conflitti segnalati dalle porte di rete hello dall'avvio

 Anche se questa classe presenta un'istanza, LAD non supporta l'acquisizione delle metriche di rete aggregate per tutti i dispositivi di rete. impostare le metriche di hello tooobtain per un'interfaccia specifica, ad esempio eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>metriche Builtin per hello classe Filesystem

Hello classe Filesystem delle metriche vengono fornite informazioni sull'utilizzo del file System. Valori assoluti e percentuale vengono segnalati come sono visualizzati tooan utente ordinario (non radice).

counter | Significato
------- | -------
FreeSpace | Spazio disponibile su disco in byte
UsedSpace | Spazio su disco usato in byte
PercentFreeSpace | Percentuale di spazio libero
PercentUsedSpace | Percentuale di spazio usato
PercentFreeInodes | Percentuale di inode non usati
PercentUsedInodes | Percentuale di inode allocati, ovvero in uso, sommati tra tutti i file System
BytesReadPerSecond | Byte letti per secondo
BytesWrittenPerSecond | Byte scritti per secondo
Byte al secondo | Byte letti o scritti per secondo
ReadsPerSecond | Operazioni di lettura per secondo
WritesPerSecond | Operazioni di scrittura per secondo
TransfersPerSecond | Operazioni di lettura o scrittura per secondo

È possibile ottenere i valori aggregati in tutti i file System impostando `"condition": "IsAggregate=True"`. È possibile ottenere i valori per un determinato file system montato, ad esempio "/mnt", può essere ottenuto impostando `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>metriche Builtin per hello classe dei dischi

Hello classe dei dischi delle metriche vengono fornite informazioni sull'utilizzo di dispositivo disco. Queste statistiche si applicano toohello intera unità. Se sono presenti più file System in un dispositivo, hello contatori per il dispositivo sono, in modo efficiente, tutti gli aggregati.

counter | Significato
------- | -------
ReadsPerSecond | Operazioni di lettura per secondo
WritesPerSecond | Operazioni di scrittura per secondo
TransfersPerSecond | Operazioni totali per secondo
AverageReadTime | Media di secondi per operazione di lettura
AverageWriteTime | Media di secondi per operazione di scrittura
AverageTransferTime | Media di secondi per operazione
AverageDiskQueueLength | Media delle operazioni del disco in coda
ReadBytesPerSecond | Numero di byte letti al secondo
WriteBytesPerSecond | Numero di byte scritti al secondo
Byte al secondo | Numero di byte letti o scritti al secondo

È possibile ottenere i valori aggregati per tutti i dischi impostando `"condition": "IsAggregate=True"`. tooget informazioni per un dispositivo specifico (ad esempio dev/sdf1), impostare `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Installazione e configurazione di LAD 3.0 tramite l'interfaccia della riga di comando

Presupponendo che le impostazioni protette nel file hello Privateconfig e le informazioni di configurazione pubblico sono nella PublicConfig.json, eseguire questo comando:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

comando Hello presuppone che si utilizza la modalità di gestione delle risorse Azure hello (arm) di hello CLI di Azure. tooconfigure LAD per distribuzione classica del modello di macchine virtuali (ASM), passare troppo "asm" modalità (`azure config mode asm`) e omettere nome gruppo di risorse hello nel comando hello. Per ulteriori informazioni, vedere hello [documentazione CLI multipiattaforma](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Una configurazione di LAD 3.0 di esempio

In base che precede le definizioni, una configurazione di estensione di esempio LAD 3.0 con alcune spiegazioni hello. tooapply questo esempio tooyour case, è necessario usare il proprio nome di account di archiviazione, tenere conto di token di firma di accesso condiviso e i token SAS EventHubs.

### <a name="privateconfigjson"></a>PrivateConfig.json

Queste impostazioni private consentono di configurare:

* un account di archiviazione
* un token SAS dell'account corrispondente
* diversi sink, ad esempio JsonBlob o EventHubs con i token SAS

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Con queste impostazioni pubbliche il LAD:

* Caricare le metriche percentuale tempo processore e spazio su disco utilizzato toohello `WADMetrics*` tabella
* Caricare i messaggi syslog funzionalità "user" e alla gravità "info" toohello `LinuxSyslog*` tabella
* Caricare raw OMI query risultati (PercentProcessorTime e PercentIdleTime) toohello denominato `LinuxCPU` tabella
* Caricare le righe aggiunte nel file `/var/log/myladtestlog` toohello `MyLadTestLog` tabella

In ogni caso, i dati vengono anche caricati:

* Archiviazione Blob di Azure (nome del contenitore è definito in sink JsonBlob hello)
* Endpoint EventHubs (come specificato nel sink EventHubs hello)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Hello `resourceId` hello configurazione deve corrispondere che di scalabilità di macchine virtuali di macchina virtuale o hello hello impostata.

* Le metriche di piattaforma Azure per grafici e di avviso SA resourceId hello di hello macchina virtuale che si sta lavorando. È previsto che i dati di hello toofind per la macchina virtuale usando una chiave di ricerca di hello resourceId hello.
* Se si usano Azure scalabilità automatica, resourceId hello nella configurazione della scalabilità automatica hello devono corrispondere resourceId hello utilizzato da LAD.
* resourceId Hello viene compilata in nomi di hello di JsonBlobs scritti da LAD.

## <a name="view-your-data"></a>Visualizzare i dati

Utilizzare i dati sulle prestazioni tooview portale Azure hello o impostare gli avvisi:

![immagine](./media/diagnostic-extension/graph_metrics.png)

Hello `performanceCounters` dati vengono sempre archiviati in una tabella di archiviazione di Azure. Le API di Archiviazione di Azure sono disponibili per più linguaggi e piattaforme.

Dati inviati tooJsonBlob sink vengono archiviati nel BLOB nell'account di archiviazione hello denominato in hello [protetto impostazioni](#protected-settings). È possibile utilizzare i dati di blob hello tramite le API di archiviazione Blob di Azure.

Inoltre, è possibile utilizzare questi dati di hello tooaccess degli strumenti dell'interfaccia utente in archiviazione di Azure:

* Esplora server di Visual Studio.
* [Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Microsoft Azure Storage Explorer").

Questo snapshot di una sessione di Microsoft Azure Storage Explorer Mostra hello generate tabelle di archiviazione di Azure e i contenitori da un'estensione LAD 3.0 configurata correttamente in una macchina virtuale di test. immagine di Hello non corrisponde esattamente alla hello [configurazione di esempio 3.0 LAD](#an-example-lad-30-configuration).

![immagine](./media/diagnostic-extension/stg_explorer.png)

Vedere hello rilevante [EventHubs documentazione](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn come tooconsume messaggi pubblicati tooan EventHubs endpoint.

## <a name="next-steps"></a>Passaggi successivi

* Creare metrici avvisi in [Monitor Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) per le metriche di hello è raccogliere.
* Creare [grafici di monitoraggio](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) per le metriche.
* Informazioni su come troppo[creare un set di scalabilità della macchina virtuale](/azure/virtual-machines/linux/tutorial-create-vmss) tramite la scalabilità automatica toocontrol metriche.
