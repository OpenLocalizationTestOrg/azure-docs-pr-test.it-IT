---
title: aaaTroubleshoot protezione errori VMware/fisici tooAzure | Documenti Microsoft
description: Questo articolo vengono descritti gli errori di replica della macchina VMware di comuni hello e come tootroubleshoot li
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Risolvere i problemi di replica per macchine virtuali VMware/server fisici locali
Potrebbe essere visualizzato un messaggio di errore specifico durante la protezione delle macchine virtuali VMware o dei server fisici con Azure Site Recovery. Questo articolo presenta alcuni dei messaggi di errore più comuni rilevati, insieme a tooresolve passaggi di risoluzione dei problemi di hello li.


## <a name="initial-replication-is-stuck-at-0"></a>Replica iniziale bloccata allo 0%
La maggior parte degli errori di replica iniziale hello che si verificano al supporto tecnico è a causa di problemi di tooconnectivity tra server al processo server di origine o di processo server in Azure.
Per la maggior parte dei casi, è possibile self risolvere questi problemi seguendo i passaggi di hello elencati di seguito.

###<a name="check-hello-following-on-source-machine"></a>Verificare hello seguenti nel computer di origine
* Dalla riga di comando di computer Server di origine, è possibile usare Telnet tooping hello Server di elaborazione con la porta https (impostazione predefinita 9443) come illustrato di seguito toosee se sono presenti problemi di connettività di rete o porta del firewall problemi gravi.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Utilizzo di Telnet, non usare la connettività tootest PING.  Se Telnet non è installato, seguire l'elenco di passaggi hello [qui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Se non è possibile tooconnect, consente la porta in ingresso 9443 sul Server di elaborazione hello e controllare se hello problema ancora viene chiuso. Si sono verificati alcuni casi in cui il problema era dovuto al posizionamento del server di elaborazione dietro una rete perimetrale.

* Controllare lo stato di hello del servizio `InMage Scout VX Agent – Sentinel/OutpostStart` se non è in esecuzione e controllare se il problema di hello esiste ancora.   
 
###<a name="check-hello-following-on-process-server"></a>Verificare hello seguenti nel SERVER di elaborazione

* **Controllare se i server di elaborazione è attivamente push tooAzure dati** 

Computer Server di elaborazione, aprire hello Task Manager (premere Ctrl + Maiusc-Esc). Andare nella scheda prestazioni toohello e fare clic sul collegamento 'Monitoraggio risorse Open'. Da Gestione risorse, passare tooNetwork scheda. Controllare se cbengine.exe 'Processi con attività rete' sta inviando attivamente volumi elevati di dati (in Mbps).

![Abilitare la replica](./media/site-recovery-protection-common-errors/cbengine.png)

Se non seguire i passaggi di hello elencati di seguito:

* **Verificare se i server di elaborazione è in grado di tooconnect Blob di Azure**: selezionare e controllare cbengine.exe tooview hello 'Connessioni TCP' toosee se si verifica la connettività dal processo server tooAzure archiviazione blob URL.

![Abilitare la replica](./media/site-recovery-protection-common-errors/rmonitor.png)

In caso contrario, andare tooControl pannello > servizi, controllare se hello seguenti servizi siano in esecuzione:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Ri) Avviare il servizio che non è in esecuzione e verificare se il problema di hello esista ancora.

* **Verificare se i server di elaborazione è in grado di tooconnect indirizzo IP pubblico di tooAzure tramite la porta 443**

Aprire hello CBEngineCurr.errlog più recenti da `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e cercare: 443 e connessione tentativo non riuscito.

![Abilitare la replica](./media/site-recovery-protection-common-errors/logdetails1.png)

Se si verificano problemi, dalla riga di comando di Server di elaborazione, usare telnet tooping l'indirizzo IP pubblico di Azure (mascherato sopra immagine) trovato in hello CBEngineCurr.currLog tramite la porta 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Se si tooconnect non è possibile, controllare se il problema di accesso di hello è scadenza toofirewall o Proxy, come descritto nel passaggio successivo.


* **Controllare se firewall basato su indirizzi IP nel server di elaborazione non bloccano l'accesso**: se si utilizza un regole del firewall basato su indirizzi IP nel server di hello, quindi scaricare elenco completo di hello dei Data Center intervalli IP Microsoft Azure da [qui ](https://www.microsoft.com/download/details.aspx?id=41653) e li aggiunge tooyour firewall configurazione tooensure consentono la comunicazione tooAzure (e hello porta HTTPS (443)).  Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).

* **Controllare se il firewall basato su URL sul server di elaborazione non blocchi l'accesso**: se si utilizza una regola firewall URL basato su server hello, assicurarsi di hello URL seguenti viene aggiunti toofirewall configurazione. 
     
  `*.accesscontrol.windows.net:`, usato per il controllo di accesso e la gestione delle identità.

  `*.backup.windowsazure.com:`, usato per l'orchestrazione e il trasferimento dei dati di replica.

  `*.blob.core.windows.net:`Utilizzato per l'accesso toohello account di archiviazione che archivia i dati replicati

  `*.hypervrecoverymanager.windowsazure.com:`, usato per l'orchestrazione e le operazioni di gestione della replica.

  `time.nist.gov`e `time.windows.com`: utilizzato toocheck sincronizzazione dell'ora tra sistema e l'ora globale.

URL per il **cloud di Azure per enti pubblici**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Controllare che le impostazioni del proxy nel server di elaborazione non blocchino l'accesso**.  Se si utilizza un Server Proxy, verificare il nome di server proxy hello venga risolto dal server DNS hello.
toocheck di quanto specificato in fase di hello del programma di installazione di Server di configurazione. Passare tooregistry chiave

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Verificare che hello stesse impostazioni sono utilizzate da dati toosend agente di Azure Site Recovery.
Cercare Backup di Microsoft Azure 

![Abilitare la replica](./media/site-recovery-protection-common-errors/mab.png)

Aprire il servizio e fare clic su Azione > Modifica proprietà. Nella scheda Configurazione del Proxy, verrà visualizzato l'indirizzo proxy hello, che deve essere lo stesso come indicato dalle impostazioni del Registro di sistema hello. In caso contrario,. modificarlo toohello stesso indirizzo.

![Abilitare la replica](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Controllare se nel server di elaborazione non è vincolato limitazione della larghezza di banda**: aumentare la larghezza di banda hello e verificare se il problema di hello esista ancora.

##<a name="next-steps"></a>Passaggi successivi
Se è necessario ulteriore assistenza, quindi registrare la query troppo[forum ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). È disponibile una community attiva e uno dei nostri tecnici saranno in grado di tooassist è.
