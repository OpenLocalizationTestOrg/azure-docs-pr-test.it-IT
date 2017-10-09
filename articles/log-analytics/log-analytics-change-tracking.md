---
title: modifiche di aaaTrack con Analitica di Log di Azure | Documenti Microsoft
description: Hello soluzione Change Tracking in Analitica Log consente di identificare modifiche al software e il servizio Windows che si verificano nell'ambiente in uso.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Tenere traccia delle modifiche del software nel proprio ambiente con hello soluzione Change Tracking

![Simbolo di Rilevamento modifiche](./media/log-analytics-change-tracking/change-tracking-symbol.png)

In questo articolo consente di utilizzare hello soluzione Change Tracking in Log Analitica tooeasily identificare le modifiche nell'ambiente in uso. soluzione Hello tiene traccia delle modifiche tooWindows e software Linux, i file di Windows e le chiavi del Registro di sistema, servizi di Windows e daemon Linux. Rilevando le modifiche alla configurazione è possibile localizzare eventuali problemi operativi.

Installare hello soluzione tooupdate hello tipo di agente che è stato installato. Le modifiche tooinstalled software, servizi di Windows e Linux daemon nei server monitorato hello vengono letti. Quindi, dati hello viene inviati servizio Analitica Log toohello nel cloud hello per l'elaborazione. Logica è applicato toohello ha ricevuto dati e dati hello vengono registrati nel servizio cloud di hello. Utilizzando le informazioni di hello nel dashboard Change Tracking hello, è possibile visualizzare facilmente modifiche di hello che sono state apportate all'infrastruttura del server.

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

* È necessario disporre di un [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), o [Linux](log-analytics-linux-agents.md) agente in ogni computer in cui si desidera toomonitor modifiche.
* Aggiungere hello Change Tracking soluzione tooyour area di lavoro OMS da hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). In alternativa, è possibile aggiungere soluzioni hello utilizzando informazioni hello [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Non è necessaria una configurazione aggiuntiva.

### <a name="configure-linux-files-tootrack"></a>Configurare tootrack file Linux
Utilizzare hello seguendo i passaggi tooconfigure file tootrack nei computer Linux.

1. Nel portale OMS hello, fare clic su **impostazioni** (simbolo a forma di ingranaggio hello).
2. In hello **impostazioni** pagina, fare clic su **dati**, quindi fare clic su **rilevamento File Linux**.
3. In Linux File di rilevamento delle modifiche, digitare l'intero percorso hello, incluso il nome di file hello del file hello che si desidera tootrack e quindi fare clic su hello **Aggiungi** simbolo. Ad esempio: "/etc/*.conf"
4. Fare clic su **Salva**.  

> [!NOTE]
> Il rilevamento dei file di Linux contiene funzionalità aggiuntive, tra cui il rilevamento di directory, la ricorsione tramite directory e il rilevamento di caratteri jolly.

### <a name="configure-windows-files-tootrack"></a>Configurare Windows file tootrack
Utilizzare i seguenti passaggi tooconfigure file tootrack nei computer Windows hello.

1. Nel portale OMS hello, fare clic su **impostazioni** (simbolo a forma di ingranaggio hello).
2. In hello **impostazioni** pagina, fare clic su **dati**, quindi fare clic su **rilevamento File Windows**.
3. In Windows File di rilevamento delle modifiche, digitare l'intero percorso hello, incluso il nome di file hello del file hello che si desidera tootrack e quindi fare clic su hello **Aggiungi** simbolo. Ad esempio: C:\Programmi (x86)\Internet Explorer\iexplore.exe o C:\Windows\System32\drivers\etc\hosts.
4. Fare clic su **Save**.  
   ![Rilevamento modifiche file di Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Configurare tootrack chiavi del Registro di sistema di Windows
Utilizzare hello seguente tootrack chiavi del Registro di sistema di passaggi tooconfigure nei computer Windows.

1. Nel portale OMS hello, fare clic su **impostazioni** (simbolo a forma di ingranaggio hello).
2. In hello **impostazioni** pagina, fare clic su **dati**, quindi fare clic su **rilevamento del Registro di sistema Windows**.
3. Change Tracking del Registro di sistema Windows, digitare hello intera chiave che si desidera tootrack e quindi fare clic su hello **Aggiungi** simbolo.
4. Fare clic su **Salva**.  
   ![Rilevamento modifiche del Registro di sistema Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Spiegazione delle proprietà di raccolta di file di Linux
1. **Tipo**
   * **File** (Indicare i metadati di file: dimensioni, data di modifica, hash, ecc.)
   * **Directoy** (Indicare i metadati di directory: dimensioni, data di modifica, ecc.)
2. **Collegamenti** (collegamento simbolico Linux gestione fa riferimento a tooother file o directory)
   * **Ignora** (collegamenti simbolici ignora durante recurions toonot includono hello file/directory a cui fa riferimento)
   * **Seguire** (collegamenti simbolici hello seguire durante la ricorsione tooalso includono hello file/directory a cui fa riferimento)
   * **Gestire** (seguire i collegamenti simbolici hello e alter trattamento hello del contenuto restituito)

   > [!NOTE]   
   > non è consigliabile Hello opzione i collegamenti di "Gestisci". Il recupero del contenuto del file non è supportato.

3. **Recurse** (Recurse i livelli di cartelle e tenere traccia di tutti i file di istruzione di percorso hello riunione)
4. **Sudo** (Consentire di accedere a file o directory che richiedono il privilegio sudo)

### <a name="limitations"></a>Limitazioni
Hello soluzione Change Tracking non supporta attualmente hello seguenti elementi:

* Cartelle (directory) per Rilevamento file di Windows
* Ricorsione per Rilevamento file di Windows
* Caratteri jolly per Rilevamento file di Windows
* Variabili di percorso
* File system di rete
* File Content

Altre limitazioni:

* Hello **dimensioni massime File** colonna e i valori vengono utilizzati nell'implementazione corrente di hello.
* Se si raccolgono i file più di 2500 in ciclo hello di 30 minuti, potrebbero verificarsi una riduzione delle prestazioni di soluzione.
* Quando il traffico di rete è elevato, i record delle modifiche potrebbero richiedere tooa numero massimo di sei ore toodisplay.
* Se si modifica la configurazione hello mentre si arresta un computer, computer hello può inserire le modifiche ai file che faceva parte toohello di configurazione precedente.

## <a name="change-tracking-data-collection-details"></a>Informazioni dettagliate sulla raccolta dei dati di Change Tracking
Rilevamento delle modifiche raccoglie l'inventario software e i metadati del servizio Windows tramite agenti hello che è stata abilitata.

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per il rilevamento delle modifiche.

| Piattaforma | Agente diretto | Agente di Operations Manager | Agente Linux | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows e Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minuti too50 minuti, in base al tipo di modifica hello. Vedere hello per ulteriori informazioni nella tabella seguente. |


Hello nella tabella seguente mostra la frequenza di raccolta dati hello per tipi di hello di modifiche.

| **tipo di modifica** | **frequency** | **L'****agente** **invia le differenze quando vengono rilevate?**  |
| --- | --- | --- |
| Registro di sistema di Windows | 50 minuti | No |
| File Windows | 30 minuti | Sì. Se non si verifica alcun cambiamento in 24 ore, viene inviato uno snapshot. |
| File Linux | 15 minuti | Sì. Se non si verifica alcun cambiamento in 24 ore, viene inviato uno snapshot. |
| Servizi Windows | 30 minuti | Sì, ogni 30 minuti quando vengono rilevate modifiche. Ogni 24 ore viene inviato uno snapshot, indipendentemente dalle modifiche. In tal caso, snapshot hello viene inviato anche se sono state apportate modifiche. |
| Daemon Linux | 5 minuti | Sì. Se non si verifica alcun cambiamento in 24 ore, viene inviato uno snapshot. |
| Software Windows | 30 minuti | Sì, ogni 30 minuti quando vengono rilevate modifiche. Ogni 24 ore viene inviato uno snapshot, indipendentemente dalle modifiche. In tal caso, snapshot hello viene inviato anche se sono state apportate modifiche. |
| Software Linux | 5 minuti | Sì. Se non si verifica alcun cambiamento in 24 ore, viene inviato uno snapshot. |

### <a name="registry-key-change-tracking"></a>Rilevamento delle modifiche della chiave del Registro di Sistema

Log Analitica esegue del Registro di sistema di Windows il monitoraggio e rilevamento con hello soluzione Change Tracking. scopo di Hello del monitoraggio delle modifiche tooregistry chiavi è toopinpoint punti di estendibilità in cui è possibile attivare il codice di terze parti e malware. esempio Hello Elenca Mostra hello predefinita del Registro di sistema le chiavi vengono rilevati dalla soluzione hello e ogni motivo per cui viene rilevato.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Monitora gli script eseguiti all'avvio.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Monitora gli script eseguiti all'arresto del sistema.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Consente di monitorare le chiavi che vengono caricate prima hello utente esegue l'accesso in tootheir account di Windows. Hello chiave viene usata per i programmi a 32 bit in esecuzione nel computer a 64 bit.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - Controlla le modifiche apportate tooapplication impostazioni.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Monitora le voci di avvio automatico che si collegano direttamente in Esplora risorse e che in genere funzionano in-process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Monitora le voci di avvio automatico che si collegano direttamente in Esplora risorse e che in genere funzionano in-process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Monitora le voci di avvio automatico che si collegano direttamente in Esplora risorse e che in genere funzionano in-process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitora la registrazione del gestore della sovrapposizione delle icone.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitora la registrazione del gestore della sovrapposizione delle icone per i programmi a 32 bit in esecuzione su computer a 64 bit.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Monitora i nuovi plug-in dell'oggetto browser helper per Internet Explorer. Tooaccess usato hello modello DOM (Document Object) di spostamento di pagina e toocontrol corrente hello.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Monitora i nuovi plug-in dell'oggetto browser helper per Internet Explorer. Tooaccess usato hello modello DOM (Document Object) di hello pagina e toocontrol spostamento corrente per programmi a 32 bit in esecuzione nel computer a 64 bit.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Monitora le nuove estensioni di Internet Explorer, come i menu degli strumenti personalizzati e i pulsanti della barra degli strumenti personalizzata.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Monitora le nuove estensioni di Internet Explorer, come i menu degli strumenti personalizzati e i pulsanti della barra degli strumenti personalizzata per i programmi a 32 bit in esecuzione su computer a 64 bit.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Consente di monitorare i driver a 32 bit hello associato wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc. Sezione toohello [drivers] analoga hello del sistema. File INI.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Driver a 32 bit hello monitoraggi associati wavemapper, wave1 e wave2, msacm.imaadpcm, .msadpcm, .msgsm610 e vidc per programmi a 32 bit in esecuzione nel computer a 64 bit. Sezione toohello [drivers] analoga hello del sistema. File INI.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitoraggi hello elenco noto o di uso comune delle DLL di sistema; Questo sistema impedisce a persone di sfruttamento autorizzazioni directory dell'applicazione debole di eliminazione nelle versioni di Trojan horse di DLL di sistema.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Elenco di monitoraggi hello pacchetti tooreceive in grado di notifiche di eventi da Winlogon, modello di supporto di accesso interattivo hello per sistema operativo di Windows hello.


## <a name="use-change-tracking"></a>Uso di Change Tracking
Dopo l'installazione della soluzione hello, è possibile visualizzare il riepilogo di hello delle modifiche per i server monitorati tramite hello **Change Tracking** riquadro hello **Panoramica** pagina in OMS.

![immagine del riquadro Change Tracking](./media/log-analytics-change-tracking/change-tracking-tile.png)

È possibile visualizzare le modifiche tooyour infrastruttura e quindi analizzare i dettagli per hello seguenti categorie:

* Modifiche per tipo di configurazione per i servizi software e di Windows.
* Modifiche software tooapplications e gli aggiornamenti per singoli server.
* Numero totale di modifiche software per ogni applicazione.
* Pacchetti Linux
* Modifiche dei servizi di Windows per singoli server.
* Modifiche a daemon Linux

![image of Change Tracking dashboard](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![image of Change Tracking dashboard](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview modifiche di qualsiasi tipo
1. In hello **Panoramica** pagina, fare clic su hello **Change Tracking** riquadro.
2. In hello **Change Tracking** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli dei tipi hello modifiche e quindi fare clic su uno tooview informazioni dettagliate su di esso in hello **ricerca nei log** pagina.
3. In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca. È inoltre possibile filtrare dai risultati di hello toonarrow facet.

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview dettagliate dati di rilevamento delle modifiche.
