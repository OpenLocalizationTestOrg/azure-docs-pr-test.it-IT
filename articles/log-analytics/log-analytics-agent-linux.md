---
title: aaaConnect il tooOperations computer Linux Management Suite (OMS) | Documenti Microsoft
description: In questo articolo viene descritto come i computer Linux tooconnect ospitato in Azure, altri cloud o locale tooOMS utilizzando hello agente OMS per Linux.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Connettere il tooOperations computer Linux Management Suite (OMS) 

Con Microsoft Operations Management Suite (OMS), è possibile raccogliere i dati generati dai computer Linux e da soluzioni contenitore come Docker, che si trovano nel data center locale, come macchine virtuali o server fisici in locale, macchine virtuali in un servizio ospitato nel cloud come Amazon Web Services (AWS) o Microsoft Azure, nonché usare tali dati. È inoltre possibile utilizzare soluzioni di gestione disponibili in OMS, ad esempio rilevamento delle modifiche, le modifiche di configurazione, tooidentify e tooproactively gli aggiornamenti software di gestione degli aggiornamenti toomanage gestire hello del ciclo di vita delle macchine virtuali Linux. 

Hello agente OMS per Linux comunica in uscita con il servizio OMS hello sulla porta TCP 443 e se hello connessione toocommunicate di server proxy o firewall tooa su Internet, hello esaminare [agente hello di configurazione per l'utilizzo con un proxy HTTP Server o Gateway OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand modifiche della configurazione sarà necessario toobe applicato.  Se si sta monitorando computer hello con System Center 2016 - Operations Manager o Operations Manager 2012 R2, può essere multihomed con hello OMS servizio toocollect dati e il servizio di inoltro toohello e ancora essere monitorato da Operations Manager.  I computer Linux monitorati da un gruppo di gestione di Operations Manager integrato con OMS non viene visualizzato di configurazione per le origini dati e inoltra raccolti dati tramite il gruppo di gestione di hello.  agente OMS Hello non può essere configurato tooreport toomore rispetto a un'area di lavoro.  

Se i criteri di sicurezza IT non consentono i computer su toohello di tooconnect la rete Internet, agente hello può essere informazioni di configurazione tooreceive OMS Gateway configurato tooconnect toohello e inviare i dati raccolti a seconda della soluzione hello che è abilitata. Per ulteriori informazioni e procedure su come tooconfigure toocommunicate l'agente Linux di OMS tramite un servizio OMS toohello Gateway OMS, vedere [connettersi tooOMS computer tramite Gateway OMS hello](log-analytics-oms-gateway.md).  

Hello diagramma seguente illustra la connessione hello tra i computer gestiti tramite agenti Linux hello e OMS, incluse le porte e direzione hello.

![Diagramma della comunicazione degli agenti diretti con OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Requisiti di sistema
Prima di iniziare, esaminare hello seguenti siano soddisfatti i prerequisiti di hello tooverify di dettagli.

### <a name="supported-linux-operating-systems"></a>Sistemi operativi Linux supportati
Hello seguendo le distribuzioni di Linux è ufficialmente supportato.  Tuttavia, hello agente OMS per Linux può essere eseguito anche in altre distribuzioni non elencate.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 e 7 (x86/x64)
* Oracle Linux 5, 6 e 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)
* Debian GNU/Linux 6, 7 e 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 e 12 (x86/x64)

### <a name="network"></a>Rete
informazioni di Hello seguito proxy hello elenco e le informazioni di configurazione di firewall necessarie per hello toocommunicate agente Linux a OMS. Il traffico è in uscita dal servizio OMS toohello rete. 

|Risorsa agente| Porte |  
|------|---------|  
|*.ods.opinsights.azure.com | Porta 443|   
|*.oms.opinsights.azure.com | Porta 443|   
|*.blob.core.windows.net/ | Porta 443|   
|*.azure-automation.net | Porta 443|  

### <a name="package-requirements"></a>Requisiti dei pacchetti

 **Pacchetto obbligatorio**   | **Descrizione**   | **Versione minima**
--------------------- | --------------------- | -------------------
Glibc | Libreria GNU C   | 2.5-12 
Openssl | Librerie OpenSSL | 0.9.8e o 1.0
Curl | Client Web cURL | 7.15.5
Python-ctypes | | 
PAM | Moduli di autenticazione modulare | 

> [!NOTE]
>  Rsyslog o syslog-ng sono necessari toocollect messaggi syslog. il daemon Hello predefinito syslog nella versione 5 di Red Hat Enterprise Linux CentOS e Oracle Linux (sysklog) non è supportato per la raccolta di eventi syslog. dati di syslog toocollect da questa versione di queste distribuzioni, hello rsyslog daemon deve essere installato e configurato sysklog tooreplace, 

agente Hello include più pacchetti. versione file Hello contiene hello seguenti pacchetti, disponibili dal bundle della shell hello in esecuzione con `--extract`:

**Pacchetto** | **Versione** | **Descrizione**
----------- | ----------- | --------------
omsagent | 1.4.0 | Hello agente Operations Management Suite per Linux
omsconfig | 1.1.1 | Agente di configurazione per l'agente OMS hello
omi | 1.2.0 | Open Management Infrastructure (OMI) - server CIM leggero
scx | 1.6.3 | Provider OMI CIM per metriche delle prestazioni del sistema operativo
apache-cimprov | 1.0.1 | Monitoraggio delle prestazioni del server HTTP Apache per OMI. Installato se viene rilevato il server HTTP Apache.
mysql-cimprov | 1.0.1 | Monitoraggio delle prestazioni del server MySQL per OMI. Installato se viene rilevato il server MySQL/MariaDB.
docker-cimprov | 1.0.0 | Provider Docker per OMI. Installato se viene rilevato Docker.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibilità con System Center Operations Manager
Hello agente OMS per Linux condivide i file binari dell'agente con l'agente di System Center Operations Manager hello. Se si installa hello agente OMS per Linux in un sistema attualmente gestito da Operations Manager, hello pacchetti OMI e SCX nella versione più recente di hello computer tooa. In questa versione, hello OMS e System Center 2016 - agenti di Operations Manager/Operations Manager 2012 R2 per Linux sono compatibili. 

> [!NOTE]
> System Center 2012 SP1 e versioni precedenti sono attualmente non supportati o compatibili con hello agente OMS per Linux.<br>
> Hello agente OMS per Linux viene installato tooa computer che non è attualmente monitorati da Operations Manager, se si desidera quindi computer hello toomonitor con Operations Manager, è necessario modificare hello [configurazione OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) precedente computer hello toodiscovering. **Questo passaggio è *non* necessario se l'agente di Operations Manager hello viene installato prima di hello agente OMS per Linux.**

### <a name="system-configuration-changes"></a>Modifiche alla configurazione di sistema
Dopo aver installato hello agente OMS per i pacchetti Linux, hello modifiche di configurazione aggiuntive a livello di sistema seguenti vengono applicate. Questi elementi vengono rimossi quando il pacchetto omsagent hello.

* Viene creato un utente senza privilegi denominato `omsagent` . Si tratta di hello account hello omsagent daemon eseguito come.
* Viene creato un file "include" suoders in /etc/sudoers.d/omsagent. Questo autorizza omsagent toorestart hello syslog e i daemon omsagent. Se le direttive "include" sudo non sono supportate nella versione di hello installata di sudo, queste voci vengono scritte troppo/ecc/file.
* configurazione di syslog Hello è tooforward modificato un subset dell'agente toohello eventi. Per ulteriori informazioni, vedere hello **configurazione della raccolta dei dati** sezione riportata di seguito

### <a name="upgrade-from-a-previous-release"></a>Eseguire l'aggiornamento da una versione precedente
L'aggiornamento da versioni precedenti alla 1.0.0-47 è supportato in questa versione. Installazione di hello con hello `--upgrade` comando consente di aggiornare tutti i componenti della versione più recente di hello agente toohello.

## <a name="installing-hello-agent"></a>Installazione agente hello

In questa sezione viene descritto come pacchetti di hello tooinstall agente OMS per Linux tramite un bunndle, che contiene Debian e RPM per ognuno dei componenti di agente hello.  Può essere installato direttamente o l'estrazione di singoli pacchetti di tooretrieve hello.  

È necessario l'ID area di lavoro OMS e la chiave, che è possibile trovare passando toohello [portale classico OMS](https://mms.microsoft.com).  In hello **Panoramica** pagina hello menu superiore selezionare **impostazioni**, quindi passare troppo**server con connessione Sources\Linux**.  Vedrai hello valore toohello a destra di **ID area di lavoro** e **chiave primaria**.  Copiare e incollare entrambi i valori nell'editor predefinito.    

1. Hello download più recenti [agente OMS per Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) o [agente OMS per Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) da GitHub.  
2. Trasferimento hello bundle appropriata (x86 o x64) tooyour computer Linux tramite scp o sftp.
3. Installazione hello bundle utilizzando hello `--install` o `--upgrade` argomento. 

    > [!NOTE]
    > Se sono installati pacchetti esistenti, ad esempio quando l'agente System Center Operations Manager hello per Linux è già installata, utilizzare hello `--upgrade` argomento. tooconnect tooOperations Management Suite durante l'installazione, fornire hello `-w <WorkspaceID>` e `-s <Shared Key>` parametri.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall e caricare direttamente
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>pacchetto dell'agente hello tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall e tooa onboard dell'area di lavoro in Microsoft Cloud per enti pubblici
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configurazione agente hello per l'utilizzo con un server proxy HTTP o il Gateway di OMS
Hello agente OMS per Linux supporta la comunicazione tramite un server proxy HTTP o HTTPS o il servizio OMS toohello di Gateway di OMS.  Sono supportate sia l'autenticazione anonima che quella di base (nome utente/password).  

### <a name="proxy-configuration"></a>Configurazione proxy
valore di configurazione proxy Hello è hello la seguente sintassi:

`[protocol://][user:password@]proxyhost[:port]`

Proprietà|Descrizione
-|-
Protocol|http o https
user|Nome utente facoltativo per l'autenticazione proxy
password|Password facoltativa per l'autenticazione proxy
proxyhost|FQDN o indirizzo del server proxy hello/OMS Gateway
port|Numero di porta facoltativi per hello proxy server/OMS Gateway

Ad esempio: `http://user01:password@proxy01.contoso.com:8080`

server proxy Hello può essere specificato durante l'installazione o modificando i file di configurazione proxy.conf hello dopo l'installazione.   

### <a name="specify-proxy-configuration-during-installation"></a>Specificare la configurazione proxy durante l'installazione
Hello `-p` o `--proxy` argomento per il pacchetto di installazione omsagent hello specifica hello proxy configurazione toouse. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Definire la configurazione del proxy hello in un file
configurazione del proxy Hello può essere impostata nel file hello `/etc/opt/microsoft/omsagent/proxy.conf` e `/etc/opt/microsoft/omsagent/conf/proxy.conf `. file Hello possono essere creati o modificati direttamente, ma le relative autorizzazioni devono essere utente omiuser di hello toogrant aggiornato autorizzazione in lettura file hello. ad esempio:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Rimozione della configurazione proxy hello
tooremove una configurazione del proxy definito in precedenza e ripristinare la connettività toodirect, rimuovere hello proxy.conf file:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Onboarding con Operations Management Suite
Se un ID area di lavoro e una chiave non sono state specificate durante l'installazione del bundle hello, hello agente deve essere registrato successivamente con Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Caricamento tramite riga di comando hello
Eseguire il comando di omsadmin.sh hello fornendo l'id area di lavoro hello e la chiave per l'area di lavoro. Questo comando deve essere eseguito come comando radice (con elevazione sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Onboarding usando un file
1.  Creare file hello `/etc/omsagent-onboard.conf`. file Hello deve essere leggibile e scrivibile per la radice.
`sudo vi /etc/omsagent-onboard.conf`
2.  Inserire hello righe nel file hello con l'ID area di lavoro e chiave condivisa seguenti:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Eseguire hello tooOMS tooOnboard comando seguente:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Hello file viene eliminato nell'onboarding.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Abilitare hello agente OMS per Linux tooreport tooSystem Center Operations Manager
Eseguire i seguenti passaggi tooconfigure hello agente OMS per gruppo di gestione di System Center Operations Manager di Linux tooreport tooa hello.  

1. Modificare il file hello`/etc/opt/omi/conf/omiserver.conf`
2. Verificare che hello riga che inizia con **httpsport =** definisca hello porta 1270. Ad esempio: `httpsport=1270`
3. Riavviare il server OMI hello:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Log dell'agente
Hello registri per hello agente OMS per Linux è reperibile in: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello registri per il programma omsconfig (configurazione dell'agente) sono disponibili hello è reperibile in: `/var/opt/microsoft/omsconfig/log/` registri per i componenti OMI e SCX hello (che forniscono dati di metrica di prestazioni) sono reperibile in:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Configurazione di rotazione del log
configurazione di rotazione log Hello per omsagent è reperibile in:`/etc/logrotate.d/omsagent-<workspace id>`

le impostazioni predefinite di Hello sono: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Disinstallazione di hello agente OMS per Linux
Hello pacchetti dell'agente possono essere disinstallati dal file con estensione sh bundle hello in esecuzione con hello `--purge` argomento, che rimuove completamente agente hello e la relativa configurazione dal computer hello.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problema: Tooconnect Impossibile tramite proxy tooOMS

#### <a name="probable-causes"></a>Possibili cause
* proxy Hello specificato durante il caricamento non è corretto
* gli endpoint del servizio OMS Hello non sono whitelistested nel Data Center 

#### <a name="resolutions"></a>Soluzioni
1. Reonboard toohello servizio OMS con hello agente OMS per Linux tramite comando con l'opzione hello seguente hello `-v` abilitato. In questo modo l'output dettagliato dell'agente di hello connessione tramite hello proxy toohello servizio OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Nella sezione hello [agente di hello di configurazione per l'utilizzo con un proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify sia stata configurata correttamente hello toocommunicate agente tramite un server proxy.    
* Verificare che hello in seguito gli endpoint del servizio OMS sono inclusi:

    |Risorsa agente| Porte |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Porta 443|   
    |*.oms.opinsights.azure.com | Porta 443|   
    |ods.systemcenteradvisor.com | Porta 443|   
    |*.blob.core.windows.net/ | Porta 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problema: Viene visualizzato un errore 403 durante il tentativo di tooonboard

#### <a name="probable-causes"></a>Possibili cause
* Data e ora nel server Linux non sono corrette 
* L'ID e la chiave dell'area di lavoro usati non sono corretti

#### <a name="resolution"></a>Risoluzione

1. Controllo hello con data di comando hello sul server Linux. Se il tempo di hello è + /-15 minuti dall'ora corrente, caricamento ha esito negativo. toocorrect questo aggiornamento hello data e/o un fuso orario del server Linux. 
2. Verificare di che aver installato hello versione hello agente OMS per Linux.  la versione più recente di Hello viene segnalata la se a causa di un errore di caricamento hello sfasamento dell'ora.
3. Reonboard con corretto ID area di lavoro e la chiave dell'area di lavoro attenendosi alle istruzioni di installazione hello in precedenza in questo argomento.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problema: Viene visualizzato un errore 404 e 500 nel file di log hello subito dopo il caricamento
Si tratta di un problema noto che si verifica durante il primo caricamento dei dati di Linux in un'area di lavoro di OMS. Questo non influisce sui dati inviati o sull'esperienza d'uso del servizio.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problema: Non vengono visualizzati tutti i dati nel portale OMS hello

#### <a name="probable-causes"></a>Possibili cause

- Errore del servizio di OMS toohello Onboarding
- Connessione toohello servizio OMS è bloccato
- Viene eseguito il backup dei dati dell'agente OMS per Linux

#### <a name="resolutions"></a>Soluzioni
1. Controllare se hello onboarding servizio OMS è stata eseguita correttamente controllando se hello seguente file esiste già:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard utilizzando hello `omsadmin.sh` le istruzioni della riga di comando
3. Se si utilizza un proxy, fare riferimento passaggi per la risoluzione proxy toohello specificati in precedenza.
4. In alcuni casi, quando l'agente OMS per Linux hello può comunicare con il servizio OMS, hello dati sull'agente hello sono di dimensioni del buffer completo toohello in coda, che è 50 MB. eseguendo hello comando seguente, è necessario riavviare l'agente OMS per Linux Hello: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Il problema è stato risolto nell'agente versione 1.1.0-28 e versioni successive.
> 