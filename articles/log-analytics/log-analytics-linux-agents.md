---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Connettere il tooLog computer Linux Analitica
Log Analytics consente di raccogliere dati dai computer Linux e di agire in base a essi. Aggiunta di dati raccolti da Linux tooOMS consente toomanage i sistemi Linux e le soluzioni contenitore come Docker, indipendentemente dalla posizione dei computer, praticamente ovunque. Origini dati possono risiedere nel data center locale come server fisici, computer virtuali in un servizio ospitato su cloud come Amazon Web Services (AWS) o Microsoft Azure, o anche hello portatile sulla propria scrivania. OMS raccoglie anche dati da computer Windows in modo analogo, quindi supporta un ambiente IT effettivamente ibrido.

È possibile visualizzare e gestire i dati da tutte queste origini dati con Log Analytics in OMS con un singolo portale di gestione. Questo riduce la necessità di hello toomonitor con diversi sistemi, rende facile tooconsume ed è possibile esportare i dati desiderati toowhatever analitica soluzione o sistema aziendale già disponibile.

Questo articolo è una Guida introduttiva che consente di raccogliere e gestire i dati per i computer Linux usando hello agente OMS per Linux. Maggiori informazioni tecniche, ad esempio informazioni su configurazione del server proxy, informazioni sulle metriche di CollectD e origini dati JSON personalizzati sono disponibili nella [panoramica sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) e nella [documentazione completa sull'agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) su GitHub.

Attualmente, è possibile raccogliere hello seguenti tipi di dati da computer Linux:

* Metriche delle prestazioni
* Eventi SysLog
* Avvisi da Nagios e Zabbix
* Metriche delle prestazioni, inventario e log del contenitore Docker

## <a name="supported-linux-versions"></a>Versioni di Linux supportate
Le versioni x86 e x64 sono supportate ufficialmente su diverse distribuzioni Linux. Tuttavia, hello agente OMS per Linux può essere eseguito anche in altre distribuzioni non elencate.

* Amazon Linux dalla 2012.09 alla 2015.09
* CentOS Linux 5, 6 e 7
* Oracle Linux 5, 6 e 7
* Red Hat Enterprise Linux Server 5, 6 e 7
* Debian GNU/Linux 6, 7 e 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 e 12

## <a name="oms-agent-for-linux"></a>Agente OMS per Linux
Hello agente Operations Management Suite per Linux è costituito da più pacchetti. versione file Hello contiene hello seguenti pacchetti, disponibili dal bundle della shell hello in esecuzione con `--extract`.

| **Pacchetto** | **Versione** | **Descrizione** |
| --- | --- | --- |
| omsagent |1.1.0 |Hello agente Operations Management Suite per Linux |
| omsconfig |1.1.1 |Agente di configurazione per l'agente OMS hello |
| omi |1.0.8.3 |Open Management Infrastructure (OMI): server CIM leggero |
| scx |1.6.2 |Provider OMI CIM per metriche delle prestazioni del sistema operativo |
| apache-cimprov |1.0.0 |Monitoraggio delle prestazioni del server HTTP Apache per OMI. Installato solo se viene rilevato il server HTTP Apache. |
| mysql-cimprov |1.0.0 |Monitoraggio delle prestazioni del server MySQL per OMI. Installato solo se viene rilevato il server MySQL/MariaDB. |
| docker-cimprov |0.1.0 |Provider Docker per OMI. Installato solo se viene rilevato Docker. |

### <a name="additional-installation-artifacts"></a>Elementi di installazione aggiuntivi
Dopo aver installato l'agente OMS hello per i pacchetti Linux, hello modifiche di configurazione aggiuntive a livello di sistema seguenti vengono applicate. Questi elementi vengono rimossi quando il pacchetto omsagent hello.

* Viene creato un utente senza privilegi denominato `omsagent` . Si tratta di hello account hello omsagent daemon eseguito come
* Viene creato un file "include" sudoers in /etc/sudoers.d/omsagent. questo autorizza omsagent toorestart hello syslog e i daemon omsagent. Se le direttive "include" sudo non sono supportate nella versione di hello installata di sudo, queste voci verranno scritte troppo/ecc/file.
* configurazione di syslog Hello è tooforward modificato un subset dell'agente toohello eventi. Per ulteriori informazioni, vedere hello **configurazione della raccolta dei dati** sezione riportata di seguito

### <a name="linux-data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati Linux
Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati.

| una sezione source | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minuto |
| Nagios |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |All'arrivo |
| syslog |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |dall'Archiviazione di Azure: 10 minuti; dall'agente: all'arrivo |
| Contatori delle prestazioni di Linux |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |Come pianificato, almeno 10 secondi. |
| Rilevamento modifiche |![Sì](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |Ogni ora |

### <a name="package-requirements"></a>Requisiti del pacchetto
| **Pacchetto obbligatorio** | **Descrizione** | **Versione minima** |
| --- | --- | --- |
| Glibc |Libreria GNU C |2.5-12 |
| Openssl |Librerie OpenSSL |0.9.8e o 1.0 |
| Curl |Client Web cURL |7.15.5 |
| Python-ctypes |Librerie di funzioni |N/D |
| PAM |Moduli di autenticazione modulare |n/d |

> [!NOTE]
> Rsyslog o syslog-ng sono necessari toocollect messaggi syslog. il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog. dati di syslog toocollect da questa versione di queste distribuzioni, hello rsyslog daemon deve essere installato e configurato tooreplace sysklog.
>
>

## <a name="quick-install"></a>Installazione rapida
Eseguire i seguenti comandi toodownload hello omsagent hello, la convalida di checksum hello, quindi installare e agente hello onboard. I comandi sono per la versione a 64 bit. Hello ID area di lavoro e chiave primaria sono disponibili nel portale OMS hello in **impostazioni** su hello **Connected Sources** scheda.

![Dettagli dell'area di lavoro](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Sono disponibili numerosi altri metodi di tooinstall hello agente e aggiornarlo. Altre informazioni su di essi in [hello tooinstall passaggi agente OMS per Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

È inoltre possibile visualizzare hello [Azure procedura dettagliata video](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Scegliere il metodo di raccolta di dati Linux
La modalità hello tipi di dati, che potrebbe ad esempio toocollect varia a seconda se si desidera portale di OMS hello toouse o se si desidera modificare i vari file di configurazione direttamente nei client Linux. Se si sceglie portale hello toouse, configurazione hello viene inviato automaticamente tooall i client Linux. Se servono configurazioni diverse per diversi client Linux, necessario file client tooedit singolarmente o utilizzare un'alternativa, come PowerShell DSC, Chef o Puppet.

È possibile specificare gli eventi syslog hello e contatori delle prestazioni che si desidera toocollect utilizzando file di configurazione nei computer Linux hello. *Se si sceglie la raccolta dei dati tooconfigure modificando i file di configurazione dell'agente, è necessario disabilitare la configurazione centralizzata di hello.*  Vengono fornite istruzioni sotto tooconfigure la raccolta dei dati dell'agente di hello i file di configurazione, nonché toodisable configurazione centrale per tutti gli agenti OMS per Linux o singoli computer.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Disabilitare la gestione OMS per un singolo computer Linux
Raccolta dei dati centralizzata per i dati di configurazione è disabilitata per un singolo computer Linux con hello script OMS_MetaConfigHelper.py. Ciò può risultare utile se un sottoinsieme di computer necessita di una configurazione specializzata.

toodisable configurazione centralizzata:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

toore-abilita la configurazione centralizzata:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Contatori delle prestazioni di Linux
Contatori delle prestazioni di Linux sono contatori di prestazioni simili tooWindows, entrambi hanno un funzionamento analogo. È possibile utilizzare hello seguendo procedure tooadd e configurarli. Dopo che sono state aggiunte tooOMS, raccolta dei dati per loro ogni 30 secondi.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd un contatore delle prestazioni di Linux in OMS
1. gli agenti OMS per Linux tramite il portale di OMS hello tooconfigure, è possibile aggiungere i contatori delle prestazioni di Linux nella pagina Impostazioni hello, fare clic su **dati**.  
2. In hello **impostazioni** pagina **dati** , fare clic su **i contatori delle prestazioni di Linux** e quindi selezionare o digitare hello nome del contatore hello desiderato tooadd.  
    ![dati](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Se non si conosce nome completo di hello del contatore di hello, è possibile iniziare a digitare un nome parziale e verrà visualizzato un elenco dei contatori disponibili. Quando si individua il contatore hello desidera tooadd, fare clic sul nome nell'elenco di hello hello e quindi fare clic su hello più hello tooadd icona contatore.
4. Dopo aver aggiunto il contatore hello, viene visualizzato nell'elenco di hello dei contatori evidenziato con una barra colorata.
5. Per impostazione predefinita, hello **Apply below macchine toomy configurazione** opzione è selezionata. Se si desidera toodisable l'invio di dati di configurazione, deselezionare la selezione di hello.
6. Al termine la modifica dei contatori delle prestazioni, nella parte inferiore di hello della pagina hello fare clic su **salvare** toofinalize le modifiche. le modifiche di configurazione Hello apportate vengono quindi inviate hello tooall gli agenti OMS per Linux registrati in OMS, in genere entro 5 minuti.

### <a name="configure-linux-performance-counters-in-oms"></a>Configurare i contatori delle prestazioni di Linux in OMS
Per i contatori delle prestazioni di Windows è possibile scegliere un'istanza specifica per ogni contatore delle prestazioni. Tuttavia, per i contatori delle prestazioni di Linux, qualsiasi istanza di un contatore prescelto si applica tooall i contatori figlio del contatore padre hello. Hello nella tabella seguente mostra le istanze comuni hello tooboth disponibili Linux e Windows contatori delle prestazioni.

| **Nome dell'istanza** | **Significato** |
| --- | --- |
| \_Totale |Totale di tutte le istanze di hello |
| \* |Tutte le istanze |
| (/&#124;/var) |Corrisponde alle istanze denominate / oppure /var |

Analogamente, hello intervallo di campionamento che si sceglie per un contatore padre si applica tooall i contatori figlio. In altre parole, tutti gli intervalli di campionamento contatore hello figlio e le istanze sono collegate tra loro.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Aggiungere e configurare le metriche delle prestazioni con Linux
Toocollect le metriche delle prestazioni sono controllate dalla configurazione hello in/ecc/rifiutare/microsoft/omsagent/&lt;id area di lavoro&gt;/conf/omsagent.conf. Vedere [metriche delle prestazioni disponibili](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) per le classi disponibili e le metriche per hello agente OMS per Linux.

Ogni oggetto, o categoria, delle prestazioni metriche toocollect deve essere definito nel file di configurazione hello come una singola `<source>` elemento. sintassi di Hello seguito è descritto hello.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Hello parametri configurabili di questo elemento sono:

* **Oggetto\_nome**: nome dell'oggetto per la raccolta di hello hello.
* **Istanza\_regex**: un *espressione regolare* toocollect quali istanze di definizione. valore di Hello: `.*` specifica tutte le istanze. le metriche del processore toocollect per solo hello \_istanza totale, è possibile specificare `_Total`. per dati metrici sui processi toocollect hello solo le istanze crond o sshd, è possibile specificare: `(crond|sshd)`.
* **Contatore\_nome\_regex**: un *espressione regolare* definizione toocollect quali contatori (per oggetto hello). specificare tutti i contatori per l'oggetto hello, toocollect: `.*`. toocollect solo i contatori di spazio di swapping per l'oggetto memoria hello, è possibile specificare:`.+Swap.+`
* **Intervallo:**: hello frequenza di raccolta contatori dell'oggetto cui hello.

configurazione predefinita di Hello per le metriche delle prestazioni è:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Abilitare i contatori delle prestazioni di MySQL usando comandi di Linux
Se il MySQL Server o MariaDB Server viene rilevato nel computer di hello durante l'installazione del bundle omsagent hello, viene installata automaticamente un provider per il MySQL Server di monitoraggio delle prestazioni. Questo provider si connette toohello locale MySQL/MariaDB server tooexpose le statistiche sulle prestazioni. È necessario tooconfigure le credenziali utente di MySQL in modo che hello provider possa accedere hello MySQL Server.

toodefine un predefinito account utente per il server MySQL hello in localhost, usare hello esempio di comando seguente.

> [!NOTE]
> file delle credenziali Hello deve essere leggibile per l'account omsagent hello. È consigliabile eseguire comandi di hello mycimprovauth come omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


In alternativa, è possibile specificare hello necessarie le credenziali di MySQL in un file, creando hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Per ulteriori informazioni sulla gestione delle credenziali di MySQL per il monitoraggio tramite file mysql-auth hello, vedere [le credenziali nel file di autenticazione hello il monitoraggio di MySQL gestire](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Vedere [Database le autorizzazioni necessarie per i contatori delle prestazioni di MySQL](#database-permissions-required-for-mysql-performance-counters) per informazioni dettagliate sulle autorizzazioni per gli oggetti necessari per hello MySQL utente toocollect dati sulle prestazioni di MySQL Server.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Abilitare i contatori delle prestazioni del server HTTP Apache usando comandi di Linux
Se nel computer di hello viene rilevato Apache HTTP Server durante l'installazione del bundle omsagent hello, viene installata automaticamente un provider di Apache HTTP Server per il monitoraggio delle prestazioni. Questo provider si basa su un "modulo" Apache che deve essere caricato in dati sulle prestazioni di ordine tooaccess Ciao Apache HTTP Server.

È possibile caricare il modulo di hello con hello comando seguente:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache modulo di monitoraggio, eseguire hello comando seguente:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>dati sulle prestazioni tooview con Log Analitica
1. Nel portale di Operations Management Suite hello, fare clic sul riquadro Log Search hello.
2. Nella barra di ricerca hello, digitare `* (Type=Perf)` tooview tutti i contatori delle prestazioni.

Poiché OMS raccoglie anche i dati del contatore delle prestazioni di Windows, è necessario limitare ambito hello dati tooLinux specifici di ricerca. In tal caso, hello esempio permetterebbe di visualizzare le prestazioni dei dati specifico tooan server Linux di esempio denominato Chorizo21.

```
Type=Perf Computer=chorizo*
```

![Server di esempio visualizzato nei risultati della ricerca](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Nei risultati di hello, è possibile fare clic su **metriche** contatori hello tooview che per la raccolta dei dati. I dati in tempo reale vengono mostrati come grafici per ogni contatore.

![Metriche](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog è un protocollo analogo tooWindows i registri eventi di registrazione di eventi, ovvero entrambi funzionano in modo analogo, quando sono visualizzati in OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd una nuova funzione syslog di Linux in OMS
1. In hello **impostazioni** pagina **dati** , fare clic su **Syslog** e toohello a sinistra dell'icona di addizione hello, digitare hello nome della funzione syslog hello che si desidera tooadd.
    ![Syslog per Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Se non si conosce nome completo di hello della funzione di hello, è possibile iniziare a digitare un nome parziale e verrà visualizzato un elenco delle funzioni syslog disponibili. Quando si trova funzione syslog di hello desidera tooadd, fare clic sul nome nell'elenco di hello hello e quindi fare clic su hello più hello tooadd icona funzione syslog.
3. Dopo averla aggiunta, viene visualizzato nell'elenco di hello di funzione hello evidenziata con una barra colorata. Successivamente, scegliere i livelli di gravità hello (categorie di informazioni funzione syslog) che si desidera toocollect.
4. Nella parte inferiore di hello di hello pagina fare clic su **salvare** toofinalize le modifiche. le modifiche di configurazione Hello apportate vengono quindi inviate hello tooall gli agenti OMS per Linux registrati in OMS, in genere entro 5 minuti.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Configurare le funzionalità SysLog per Linux in Linux
Gli eventi Syslog vengono inviati dal daemon syslog hello, ad esempio rsyslog o syslog-ng, porta locale tooa che l'agente di hello è in ascolto. Per impostazione predefinita, si tratta della porta 25224. Quando viene installato l'agente di hello, viene applicata una configurazione predefinita di syslog. disponibile in:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng: /etc/syslog-ng/syslog-ng.conf

configurazione di syslog agente di Hello predefinita OMS carica gli eventi syslog da tutte le funzioni con un livello di gravità avviso o superiore.

> [!NOTE]
> Se si modifica la configurazione di syslog hello, è necessario riavviare i daemon syslog hello hello modifiche tootake effetto.
>
>

Hello configurazione predefinita di syslog per hello agente OMS per Linux per OMS è:

#### <a name="rsyslog"></a>Rsyslog
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview tutti gli eventi Syslog con Log Analitica
1. Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.
2. In hello **Log Management** raggruppamento, scegliere una ricerca syslog predefinita e quindi selezionare uno toorun è.

Questo esempio mostra tutti gli eventi SysLog.

![Eventi SysLog visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-syslog.png)

È ora possibile esaminare i risultati della ricerca.

## <a name="linux-alerts"></a>Avvisi di Linux
Se si usa Nagios o Zabbix toomanage che i computer Linux, quindi OMS può ricevere avvisi di hello generati da questi strumenti. Tuttavia, non sono attualmente presenti metodo tooconfigure in ingresso avviso dati tramite il portale di OMS hello. Al contrario, sarà necessario tooedit l'invio degli avvisi tooOMS una configurazione file toostart.

### <a name="collect-alerts-from-nagios"></a>Raccogliere avvisi da Nagios
toocollect gli avvisi da un server Nagios, è necessario hello toomake dopo le modifiche di configurazione.

1. Concedere all'utente di hello **omsagent** file di log Nagios toohello accesso in lettura (ad esempio /var/log/nagios/nagios.log). Supponendo che i file nagios.log hello è di proprietà di gruppo hello **nagios** , è possibile aggiungere l'utente hello **omsagent** toohello **nagios** gruppo.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Modificare il file di confconfiguration hello (via/rifiutare/microsoft/omsagent / /&lt;id area di lavoro&gt;/conf/omsagent.conf). Verificare che siano presenti e non come commento hello seguenti voci:

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Riavviare i daemon omsagent hello:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Raccogliere avvisi da Zabbix
toocollect gli avvisi da un server Zabbix, la procedura è simile passaggi toothose precedenza per Nagios, ma sarà necessario toospecify un utente e password in *cancellare il testo*. Questo approccio non è ideale, ma verrà probabilmente modificato a breve. tooaddress questo problema, è consigliabile creare utente hello e concedere l'autorizzazione toomonitor solo.

Una sezione di esempio del file di configurazione omsagent. conf hello (via/rifiutare/microsoft/omsagent / /&lt;id area di lavoro&gt;/conf/omsagent.conf) per Zabbix sarebbe simile hello seguente:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Visualizzare avvisi nella ricerca di Log Analytics
Dopo aver configurato il tooOMS di avvisi toosend computer Linux, è possibile utilizzare alcuni semplici ricerca query tooview hello gli avvisi del registro. Hello esempio query di ricerca seguente restituisce tutti gli avvisi di hello registrato che sono stati generati. Ad esempio, se si verifica un problema di problema nell'infrastruttura IT, quindi i risultati per hello query potrebbero indicare problemi hello potrebbero origine di esempio seguente. Inoltre, è possibile isolare facilmente negli avvisi toohello da toohelp di sistema di origine "narrow" l'analisi. Hello vantaggio è che non è necessariamente i sistemi di gestione di toogo toovarious dall'inizio di hello, purché gli avvisi vengono inviati tooOMS, è possibile avviare non esiste.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios tutti gli avvisi con Log Analitica
1. Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.
2. Nella barra di query hello, digitare hello seguenti query di ricerca

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Avvisi Nagios visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Dopo aver visualizzato i risultati della ricerca hello, è possibile esaminare i dettagli aggiuntivi, ad esempio *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview tutti gli avvisi Zabbix con Log Analitica
1. Nel portale di Operations Management Suite hello, fare clic su hello **ricerca nei Log** riquadro.
2. Nella barra di query hello, digitare hello seguenti query di ricerca

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Avvisi Zabbix visualizzati in Ricerca log](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Dopo aver visualizzato i risultati della ricerca hello, è possibile esaminare i dettagli aggiuntivi, ad esempio *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Compatibilità con System Center Operations Manager
Hello agente OMS per Linux condivide i file binari dell'agente con l'agente di System Center Operations Manager hello. L'installazione di hello agente OMS per Linux in un sistema attualmente gestito da Operations Manager aggiornamenti hello pacchetti OMI e SCX nella versione più recente di hello computer tooa. Hello agente OMS per Linux e System Center 2012 R2 sono compatibili. Tuttavia, **System Center 2012 SP1 e versioni precedenti sono attualmente non supportati o compatibili con hello agente OMS per Linux.**

> [!NOTE]
> Se l'agente OMS per Linux hello è installato tooa computer che non è attualmente gestito da Operations Manager e in seguito si desidera computer hello toomanage con Operations Manager, è necessario modificare configurazione OMI hello prima di individuare computer hello. **Questo passaggio non è necessario se l'agente di Operations Manager hello viene installato prima di hello agente OMS per Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>tooenable hello agente OMS per Linux toocommunicate con Operations Manager
1. Modificare hello file /etc/opt/omi/conf/omiserver.conf
2. Verificare che hello riga che inizia con **httpsport =** definisca hello porta 1270. ad esempio `httpsport=1270`
3. Riavviare il server OMI hello:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Autorizzazioni del database necessarie per i contatori delle prestazioni di MySQL
toogrant autorizzazioni tooa utente monitoraggio di MySQL, hello utente che concede deve avere il privilegio 'GRANT option' hello nonché privilegio hello da concedere.

Affinché l'utente di MySQL hello utente hello dati sulle prestazioni di tooreturn avrà bisogno di accesso toohello seguente query:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Utente di MySQL toothese query hello richiede inoltre l'accesso SELECT toohello le tabelle predefinite seguenti:

* information_schema
* mysql

È possibile concedere questi privilegi eseguendo i comandi grant seguenti hello.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Gestire le credenziali nel file di autenticazione hello il monitoraggio di MySQL
Hello nelle sezioni seguenti gestire le credenziali di MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Configurare il provider OMI MySQL hello
il provider OMI MySQL Hello richiede un utente di MySQL preconfigurato e installate le librerie client di MySQL in ordine tooquery hello prestazioni o informazioni sull'integrità dall'istanza di MySQL hello.

### <a name="mysql-omi-authentication-file"></a>File di autenticazione OMI MySQL
Il provider OMI MySQL Usa un toodetermine di file di autenticazione quale istanza di MySQL hello indirizzo di binding e la porta è in attesa e quali credenziali toouse toogather metriche. Durante la hello installazione OMI MySQL provider analizzerà i file di configurazione my.cnf di MySQL (nei percorsi predefiniti) per indirizzo di binding e la porta e parzialmente hello set di file di autenticazione OMI MySQL.

toocomplete monitoraggio di un'istanza di server MySQL, aggiungere un file di autenticazione OMI MySQL pregenerato nella directory corretta di hello.

### <a name="authentication-file-format"></a>Formato del file di autenticazione
Hello file autenticazione OMI MySQL è un file di testo che contiene informazioni su:

* Porta
* Bind-address
* Nome utente MySQL
* Password con codifica Base64

Hello file autenticazione OMI MySQL concede solo privilegi di lettura/scrittura toohello Linux utente che ha generato.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Un file di autenticazione OMI MySQL predefinito contiene un'istanza predefinita e un numero di porta a seconda delle informazioni disponibili e analizzate dal file di configurazione di MySQL trovato hello.

istanza predefinita di Hello è un toomake indica la gestione di più istanze di MySQL in un singolo host Linux e corrisponde hello istanza con la porta 0. Tutte le istanze aggiunte ereditano le proprietà impostate dall'istanza predefinita di hello. Ad esempio, se viene aggiunto l'istanza di MySQL in ascolto sulla porta '3308', indirizzo di binding, username e password con codificata Base64 dell'istanza predefinita di hello verrà essere tootry utilizzato e monitorare hello istanza in ascolto sulla porta 3308. Se l'istanza hello sulla porta 3308 è associata tooanother indirizzo e utilizzi hello stesso nome utente di MySQL e una password solo hello respecification di hello è necessaria l'indirizzo di binding e hello altre proprietà verrà ereditata.

Esempi del file di autenticazione hello seguente hello.

Istanza predefinita e istanza con porta 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Istanza predefinita e istanza con porta 3308 e password con codifica Base 64 diversa:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Proprietà** | **Descrizione** |
| --- | --- |
| Porta |Porta rappresenta hello di porta corrente hello MySQL istanza è in attesa.  porta Hello 0 implica che proprietà hello seguenti vengono utilizzate per l'istanza predefinita. |
| Bind-address |Indirizzo di binding Hello è hello corrente MySQL indirizzo di binding |
| username |Questo nome utente hello dell'utente di MySQL hello a cui l'istanza di server MySQL hello toouse toomonitor. |
| Password con codifica Base64 |Si tratta hello password dell'utente di monitoraggio MySQL hello con codificata Base64. |
| AutoUpdate |Quando viene aggiornato il Provider OMI MySQL hello hello provider Ripeti analisi per le modifiche nel file my.cnf hello e sovrascrivere il file di autenticazione OMI MySQL hello. Impostare questo flag tootrue o false a seconda degli aggiornamenti necessari toohello OMI MySQL file di autenticazione. |

#### <a name="authentication-file-location"></a>Percorso del file di autenticazione
Hello File autenticazione OMI MySQL dovrebbe essere si trova nella seguente posizione hello e nome "mysql-auth":

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

file Hello (e directory auth/omsagent) devono essere di proprietà utente omsagent hello.

## <a name="agent-logs"></a>Log dell'agente
log di Hello per hello agente OMS per Linux sono disponibili in:

/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/

i registri di Hello per hello è agente OMS per Linux per il programma omsconfig (configurazione dell'agente) sono disponibili:

/var/opt/microsoft/omsconfig/log/

Log per i componenti OMI e SCX hello (che forniscono dati di metrica di prestazioni) sono disponibili in:

/var/opt/omi/log/ e /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Risoluzione dei problemi di hello agente OMS per Linux
Utilizzare hello seguente toodiagnose informazioni e risolvere i problemi comuni.

Se nessuna delle informazioni in questa sezione Risoluzione dei problemi di hello consente, consente inoltre hello seguenti risorse toohelp risolvere il problema.

* I clienti con supporto tecnico Premier possono registrare un caso di supporto tramite [Premier](https://premier.microsoft.com/)
* I clienti con contratti di supporto tecnico di Azure possono accedere casi di supporto in hello [portale di Azure](https://manage.windowsazure.com/?getsupport=true)
* Presentare un [problema GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Forum di commenti e suggerimenti per idee e di un report sui bug toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Percorsi log importanti
| File | Path |
| --- | --- |
| File di log dell'agente OMS per Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| File di log di configurazione dell'agente OMS |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>File di configurazione importanti
| Categoria | Percorso file |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf` o `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf` |
| Output e agente generale Performance, Nagios, Zabbix e OMS |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Configurazioni aggiuntive |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> La modifica dei file di configurazione per i contatori delle prestazioni e Syslog vengono sovrascritti se è abilitata la configurazione del portale di OMS. È possibile disattivare la configurazione in hello portale di OMS (per tutti i nodi) o per singoli nodi eseguendo hello:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Abilitazione della registrazione di debug
debug tooenable registrazione, è possibile utilizzare i plug-in output di hello OMS e un output dettagliato.

#### <a name="oms-output-plugin"></a>Plug-in di output di OMS
FluentD consente hello plug-in toospecify livelli di registrazione per i livelli di registrazione diversi per input e output. toospecify un livello di log diverso per l'output OMS, modificare la configurazione del agente generale hello in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.

Nella parte inferiore di hello hello del file di configurazione, modificare hello `log_level` proprietà `info` troppo`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

La registrazione di debug consente toosee in batch caricamenti toohello servizio OMS separandoli con un tipo, numero di elementi di dati e di tempo impiegato toosend.

*Esempio di log abilitato per il debug:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Output dettagliato
Anziché utilizzare i plug-in output di hello OMS, si possono inoltre restituire gli elementi di dati direttamente troppo`stdout`, che è visibile in hello agente OMS per Linux file di log.

Nel file di configurazione generale dell'agente OMS hello in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commento hello OMS plug-in di output aggiungendo un `#` davanti a ogni riga.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Di seguito hello plug-in di output, rimuovere il commento hello nella seguente sezione rimuovendo hello hello `#` simbolo all'inizio di hello di ogni riga.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>I messaggi Syslog inoltrati non vengono visualizzati nel registro hello
#### <a name="probable-causes"></a>Possibili cause
* Hello configurazione applicata toohello Linux server non consentono l'insieme di strutture di hello inviato e/o livelli di log
* Syslog non è vengono inoltrati correttamente toohello Linux server
* numero di Hello di messaggi inoltrati al secondo è troppo grande per la configurazione di base di hello agente OMS per Linux toohandle hello

#### <a name="resolutions"></a>Soluzioni
* Verificare che la configurazione nel portale di OMS hello hello per Syslog ha tutti i livelli di log corretto hello e le funzioni hello
  * **Portale OMS &gt; Impostazioni &gt; Dati &gt; Syslog**
* Verificare che syslog native messaggistica daemon (`rsyslog`, `syslog-ng`) è in grado di tooreceive messaggi hello inoltrato
* Controllare le impostazioni del firewall su hello Syslog server tooensure che i messaggi non vengano bloccati
* Simulare un tooOMS messaggio Syslog utilizzando hello `logger` comando - ad esempio:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Problemi di connessione tooOMS quando si utilizza un proxy
#### <a name="probable-causes"></a>Possibili cause
* proxy Hello specificato quando l'installazione e configurazione agente hello è corretto
* gli endpoint del servizio OMS Hello non sono whitelistested nel Data Center

#### <a name="resolutions"></a>Soluzioni
* Reinstallare hello agente OMS per Linux tramite comando con l'opzione hello seguente hello `-v` abilitato. In questo modo l'output dettagliato dell'agente di hello connessione tramite hello proxy toohello servizio OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Consultare la documentazione hello per proxy OMS [agente hello di configurazione per l'utilizzo con un server proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Verificare che hello seguendo gli endpoint del servizio OMS sono inclusi

| Risorsa agente | Porte |
| --- | --- |
| &#42;.ods.opinsights.azure.com |Porta 443 |
| &#42;.oms.opinsights.azure.com |Porta 443 |
| ods.systemcenteradvisor.com |Porta 443 |
| &#42;.blob.core.windows.net/ |Porta 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Viene visualizzato un messaggio di errore 403 durante il caricamento
#### <a name="probable-causes"></a>Possibili cause
* hello data e ora non sono corrette nel Linux Server
* Hello ID area di lavoro e la chiave dell'area di lavoro non sono corrette

#### <a name="resolution"></a>Risoluzione
* Verificare ora hello del server Linux con hello `date` comando. Se hello sono maggiori di dati o meno di 15 minuti da hello ora corrente, caricamento ha esito negativo. toocorrect, aggiornare data hello e/o fuso orario del server Linux.
* versione più recente di Hello di hello agente OMS per Linux che informa se l'errore di caricamento causa una differenza di tempo
* Eseguire il re-caricamento tramite hello ID area di lavoro corretto e la chiave dell'area di lavoro. Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Viene visualizzato un errore 500 o errore 404 nel file di log hello dopo il caricamento
Si tratta di un problema noto che si verifica durante il primo caricamento hello dei dati di Linux in un'area di lavoro OMS. Questo non influisce sui dati inviati o su altri problemi. È possibile ignorare gli errori di hello quando inizialmente onboarding.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios dati non viene visualizzato nel portale di OMS hello
#### <a name="probable-causes"></a>Possibili cause
* Hello omsagent utente non dispone delle autorizzazioni tooread da file di log Nagios hello
* sezioni di filtro e Hello Nagios origine sono ancora impostati come commenti file omsagent. conf hello

#### <a name="resolutions"></a>Soluzioni
* Aggiungere l'utente omsagent hello in ordine tooread dal file Nagios hello. Per maggiori informazioni, vedere [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Avvisi di Nagios).
* In hello agente OMS per il file di configurazione generale di Linux in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, assicurarsi che **entrambi** hello Nagios sezioni di origine e di filtro sono commenti rimossi, simile toohello esempio seguente.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>I dati di Linux non viene visualizzato nel portale di OMS hello
#### <a name="probable-causes"></a>Possibili cause
* Errore del servizio di OMS toohello Onboarding
* Connessione toohello servizio OMS è bloccato
* Hello agente OMS per Linux dati viene eseguito il backup

#### <a name="resolutions"></a>Soluzioni
* Verificare che toohello onboarding servizio OMS ha avuto esito positivo, verificando che hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` esiste.
* Eseguire il re-caricamento tramite hello omsadmin.sh della riga di comando. Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.
* Se si utilizza un proxy, utilizzare hello proxy sulla risoluzione dei problemi passaggi precedente
* In alcuni casi, quando l'agente OMS per Linux hello può comunicare con il servizio OMS, hello dati hello agente sono toohello backup buffer completo dimensioni pari a 50 MB. Riavviare hello agente OMS per Linux eseguendo hello `/opt/microsoft/omsagent/bin/service_control restart` comando.
  >[AZURE.NOTE] Il problema è risolto nell'agente versione 1.1.0-28 o versioni successive.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Configurazione del contatore delle prestazioni Syslog Linux non viene applicato nel portale OMS hello
#### <a name="probable-causes"></a>Possibili cause
* agente di configurazione Hello in hello agente OMS per Linux è recuperato dal portale OMS hello configurazione più recente di hello.
* Hello impostazioni modificate nel portale di hello non sono state applicate

#### <a name="resolutions"></a>Soluzioni
`omsconfig`è l'agente di configurazione hello in hello agente OMS per Linux che recupera le modifiche di configurazione del portale di OMS ogni 5 minuti. Questa configurazione viene quindi applicato toohello agente OMS per Linux i file di configurazione si trova in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* In alcuni casi, hello agente OMS per Linux agente di configurazione potrebbe non essere in grado di toocommunicate con il servizio di configurazione del portale hello risultante nella configurazione più recente non vengono applicati.
* Verificare che hello `omsconfig` agente viene installato con l'esempio hello:

  * `dpkg --list omsconfig` oppure `rpm -qi omsconfig`
  * Se non è installato, è possibile reinstallare hello versione hello agente OMS per Linux
* Verificare che hello `omsconfig` agente possa comunicare con il servizio OMS hello

  * Eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
    * Hello comando precedente restituisce hello configurazione che l'agente recupera dal portale di hello, incluse le impostazioni di registro di sistema, i contatori delle prestazioni di Linux e i log personalizzati
    * Se il comando hello precedente non riesce, eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Il comando forza hello omsconfig sono disponibili agenti toocommunicate con configurazione più recente di hello OMS servizio tooretrieve hello.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Dati di log personalizzato Linux non viene visualizzato nel portale di OMS hello
#### <a name="probable-causes"></a>Possibili cause
* Errore del servizio di caricamento tooOMS
* Hello **hello applica seguente toomy configurazione server Linux** impostazione non è stata selezionata.
* non sono selezionato omsconfig sono disponibili log personalizzato hello più recente dal portale hello
* Hello `omsagent` utilizzo è log personalizzato di hello tooaccess Impossibile a causa di problemi relativi alle autorizzazioni tooa o `omsagent` non è stato trovato. In questo caso, si noterà hello seguente output:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Si tratta di un problema noto con hello Race Condition che è stato risolto in hello agente OMS per Linux versione 1.1.0-217

#### <a name="resolutions"></a>Soluzioni
* Verificare di aver correttamente caricato, determinando se hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file esista.
  * Se necessario, caricare nuovamente tramite riga di comando omsadmin.sh hello. Vedere [Onboarding tramite riga di comando hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) per ulteriori informazioni.
* In hello portale di OMS, in **impostazioni** su hello **dati** scheda, verificare che hello **hello applica seguente toomy configurazione server Linux** impostazione è selezionata  
  ![applicazione della configurazione](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Verificare che hello `omsconfig` agente possa comunicare con il servizio OMS hello

  * Eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
  * Hello comando precedente restituisce hello configurazione che l'agente recupera dal hello portale, incluse le impostazioni di registro di sistema, i contatori delle prestazioni di Linux e i log personalizzati
  * Se il comando hello precedente non riesce, eseguire hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Questo comando forza hello omsconfig sono disponibili agenti toocommunicate con il servizio OMS e recuperare la configurazione più recente di hello.

Anziché hello agente OMS per l'utente di Linux in esecuzione come utente con privilegi `root`, hello agente OMS per Linux viene eseguito come hello `omsagent` utente. Nella maggior parte dei casi, è necessario l'autorizzazione esplicita concessi all'utente di toohello in ordine tooread determinati file.

autorizzazione toogrant troppo`omsagent` utente, eseguire hello seguenti comandi:

1. Aggiungere hello `omsagent` gruppo specifico di utenti tooa con`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. File necessario concedere l'accesso in lettura universale toohello con`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Si verifica un problema noto con hello Race Condition che è stato risolto in hello agente OMS per Linux versione 1.1.0-217. Dopo aver aggiornato toohello più recenti dell'agente, eseguire hello comando tooget hello più recente del plug-in output di hello seguenti:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Limitazioni note
Esaminare hello seguenti sezioni toolearn sulle limitazioni attuali di hello agente OMS per Linux.

### <a name="azure-diagnostics"></a>Diagnostica Azure
Per le macchine virtuali Linux in esecuzione in Azure, ulteriori passaggi potrebbero essere necessario tooallow la raccolta dei dati da diagnostica di Azure e Operations Management Suite. **La versione 2.2** di hello estensione diagnostica per Linux è necessaria per la compatibilità con hello agente OMS per Linux.

Per ulteriori informazioni sull'installazione e configurazione di hello estensione diagnostica per Linux, vedere [utilizzare hello Azure CLI comando tooenable estensione diagnostica per Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Aggiornamento hello estensione di diagnostica per Linux da too2.2 2.0 di ASM CLI di Azure:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Questi esempi di comando fanno riferimento a un file denominato PrivateConfig.json. formato di Hello del file dovrebbe essere simile a hello seguente esempio.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog non è supportato.
Rsyslog o syslog-ng sono necessari toocollect messaggi syslog. il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog. dati di syslog toocollect da questa versione di queste distribuzioni, hello rsyslog daemon deve essere installato e configurato tooreplace sysklog. Per ulteriori informazioni sulla sostituzione di sysklog con rsyslog, vedere [installare il RPM rsyslog creato di recente hello](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.
* Acquisire familiarità con [log ricerche](log-analytics-log-searches.md) tooview dettagliate informazioni raccolte da soluzioni.
* Utilizzare [dashboard](log-analytics-dashboards.md) toosave e la visualizzazione ricerca personalizzati.
