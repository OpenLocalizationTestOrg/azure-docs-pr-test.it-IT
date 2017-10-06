---
title: risoluzione dei problemi Site Recovery aaaAzure per errori e problemi di replica di Azure in Azure | Documenti Microsoft
description: Risoluzione dei problemi e degli errori che si verificano quando si esegue la replica di macchine virtuali di Azure per il ripristino di emergenza
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Risolvere i problemi di replica delle VM da Azure ad Azure

In questo articolo vengono descritti i problemi comuni di hello in Azure Site Recovery quando la replica e il ripristino delle macchine virtuali di Azure dall'area di un'area tooanother e viene spiegato come tootroubleshoot li. Per ulteriori informazioni sulle configurazioni supportate, vedere hello [matrice del supporto per la replica delle macchine virtuali di Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problemi di quota delle risorse di Azure (codice errore 150097)
La sottoscrizione deve essere abilitato toocreate macchine virtuali di Azure nell'area di destinazione hello che è possibile pianificare toouse come l'area di ripristino di emergenza. Inoltre, la sottoscrizione deve dispone di sufficienti toocreate quota abilitato le macchine virtuali di dimensioni specifiche. Per impostazione predefinita, i prelievi di Site Recovery hello stesse dimensioni per la destinazione di hello VM come hello macchina virtuale di origine. Se la dimensione corrispondente hello non è disponibile, le dimensioni consentite più vicina hello viene selezionata automaticamente. Se non ci sono dimensioni corrispondenti che supportano la configurazione della VM di origine, viene visualizzato il messaggio di errore seguente:

**Codice errore** | **Possibili cause** | **Consiglio**
--- | --- | ---
150097<br></br>**Messaggio**: Impossibile abilitare la replica per la macchina virtuale hello VmName. | -La sottoscrizione che potrebbe non essere ID abilitato toocreate tutte le macchine virtuali nel percorso di area di destinazione hello.</br></br>-L'ID sottoscrizione potrebbe non essere abilitata o non dispone di sufficienti quota toocreate specifiche dimensioni di macchina virtuale nel percorso di area di destinazione hello.</br></br>-Una dimensione di macchina virtuale di destinazione appropriate corrispondente origine hello conteggio VM NIC (2) per l'ID sottoscrizione hello non vengono trovata nel percorso di area di destinazione hello.| Contatto [supporto per la fatturazione Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable la creazione di VM per hello necessari dimensioni di macchina virtuale nel percorso di destinazione hello per la sottoscrizione. Dopo averlo abilitato, operazione non riuscita del tentativo hello.

### <a name="fix-hello-problem"></a>Risolvere il problema di hello
È possibile contattare [supporto per la fatturazione Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable il toocreate sottoscrizione macchine virtuali di dimensioni necessarie nel percorso di destinazione hello.

Se il percorso di destinazione hello dispone di un vincolo di capacità, disabilitare la replica e abilitarla tooa altro percorso in cui la sottoscrizione è sufficiente toocreate quota sulle macchine virtuali di dimensioni hello necessario.

## <a name="trusted-root-certificates-error-code-151066"></a>Certificati radice trusted (codice errore 151066)

Se tutti i certificati radice attendibili più recenti hello non sono presenti sulla hello macchina virtuale, il processo "abilitare la replica" potrebbe non riuscire. Senza certificati hello, hello autenticazione e autorizzazione dei servizio Site Recovery chiamate da hello VM esito negativo. viene visualizzato il messaggio di errore Hello per il processo di ripristino del sito "abilitare la replica" hello non riuscita:

**Codice errore** | **Causa possibile** | **Raccomandazioni**
--- | --- | ---
151066<br></br>**Messaggio**: La configurazione di Site Recovery non è riuscita. | Hello richiesti i certificati radice attendibili utilizzati per l'autorizzazione e autenticazione non sono presenti nel computer di hello. | -Per una macchina virtuale in esecuzione del sistema operativo di Windows hello, verificare che hello attendibili i certificati radice siano presenti nel computer di hello. Per informazioni, vedere [Configurare radici attendibili e certificati non consentiti](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Per una macchina virtuale in esecuzione hello del sistema operativo Linux, seguire indicazioni hello per i certificati radice attendibili pubblicata dal server di distribuzione versione sistema operativo Linux hello.

### <a name="fix-hello-problem"></a>Risolvere il problema di hello
**Windows**

Installare gli aggiornamenti di Windows più recenti di hello in hello macchina virtuale in modo che tutti i certificati radice attendibile hello siano presenti nel computer di hello. Se si è in un ambiente disconnesso, seguire hello processo standard di Windows update nei certificati hello tooget dell'organizzazione. Se i certificati non sono presenti sulla macchina virtuale hello hello necessario hello chiamate toohello servizio Site Recovery esito negativo per motivi di sicurezza.

Seguire tipico gestione degli aggiornamenti Windows hello o un processo di gestione di aggiornamento di certificato in tooget l'organizzazione tutti i certificati radice più recenti di hello e revoca dei certificati hello aggiornato elenco hello macchine virtuali.

tooverify che hello problema viene risolto, visitare toologin.microsoftonline.com da un browser nella macchina virtuale.

**Linux**

Seguire indicazioni hello fornite dal hello più recente elenco certificati revocati in hello VM Linux distributore tooget hello più recenti certificati radice attendibili.

Poiché SuSE Linux vengono utilizzati collegamenti simbolici toomaintain un elenco di certificati, seguire questi passaggi:

1.  Accedere come utente ROOT.

2.  Eseguire questo comando:

      ``# cd /etc/ssl/certs``

3.  toosee certificato CA radice di Symantec hello è presente o meno, eseguire questo comando:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Se non vengono trovati file hello, eseguire questi comandi:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  un collegamento simbolico con b204d74a.0 toocreate -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, eseguire questo comando:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Controllare toosee se questo comando è hello output seguente. In caso contrario, si dispone di toocreate un collegamento simbolico:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Se 653b494a.0 collegamento simbolico non è presente, è possibile utilizzare questo collegamento simbolico di toocreate di comando:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Connettività in uscita per gli intervalli IP o gli URL di Site Recovery (codice errore 151037 o 151072)

Per il ripristino del sito replica toowork, URL o l'indirizzo IP compreso toospecific di connettività in uscita viene richiesto dall'hello macchina virtuale. Se la macchina virtuale si trova dietro un firewall o utilizza la sicurezza gruppo () regole toocontrol in uscita connettività di rete, è possibile visualizzare uno di questi messaggi di errore:

**Codici di errore** | **Possibili cause** | **Raccomandazioni**
--- | --- | ---
151037<br></br>**Messaggio**: non è stato possibile tooregister macchina virtuale di Azure con il ripristino del sito. | -Si utilizza l'accesso in uscita toocontrol NSG in hello VM e hello richieste IP intervalli non abilitata per l'accesso in uscita.</br></br>-Si usano gli strumenti di terze parti e hello necessari intervalli IP/URL non consentito.</br>| -Se si utilizza la connettività di rete in uscita firewall proxy toocontrol in hello VM, verificare che hello gli URL dei prerequisiti o gli intervalli IP di Data Center sono inclusi. Per informazioni, vedere le [indicazioni per i proxy firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Se si utilizza la connettività di rete in uscita toocontrol di regole di gruppo in hello macchina virtuale, verificare che gli intervalli IP di hello prerequisiti datacenter sono inclusi. Per altre informazioni, vedere le [indicazioni per i gruppi di sicurezza di rete](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Messaggio**: La configurazione di Site Recovery non è riuscita. | Connessione non può essere stabilita tooSite gli endpoint del servizio di ripristino. | -Se si utilizza la connettività di rete in uscita firewall proxy toocontrol in hello VM, verificare che hello gli URL dei prerequisiti o gli intervalli IP di Data Center sono inclusi. Per informazioni, vedere le [indicazioni per i proxy firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Se si utilizza la connettività di rete in uscita toocontrol di regole di gruppo in hello macchina virtuale, verificare che gli intervalli IP di hello prerequisiti datacenter sono inclusi. Per altre informazioni, vedere le [indicazioni per i gruppi di sicurezza di rete](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Risolvere il problema di hello
toowhitelist [hello necessari URL](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) o hello [gli intervalli IP necessari](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), seguire i passaggi hello hello [rete fornite nel documento](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Disco non trovato nella macchina hello (codice di errore 150039)

Un nuovo disco collegato toohello che macchina virtuale deve essere inizializzato.

**Codice errore** | **Possibili cause** | **Raccomandazioni**
--- | --- | ---
150039<br></br>**Messaggio**: il disco di dati di Azure (DiskName) (DiskURI) con il numero di unità logica (LUN) (LUNValue) non è stato mappato tooa disco corrispondente segnalata all'interno di macchina virtuale che dispone di hello hello stesso valore LUN. | -Un nuovo disco dati è stato collegato toohello VM ma non è stata inizializzata.</br></br>-il disco dati hello all'interno di hello VM non è correttamente reporting valore LUN hello in cui hello disco era collegato toohello VM.| Verificare che i dischi dati hello vengono inizializzati e quindi ripetere l'operazione di hello.</br></br>Per Windows: [Connettere e inizializzare un nuovo disco](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Per Linux: [Inizializzare un nuovo disco dati in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Risolvere il problema di hello
Assicurarsi che siano stati inizializzati i dischi dati hello e quindi ripetere l'operazione di hello:

- Per Windows: [Connettere e inizializzare un nuovo disco](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Per Linux: [Inizializzare un nuovo disco dati in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Se hello problema persiste, contattare il supporto tecnico.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Non è possibile toosee hello macchina virtuale di Azure per la selezione nella "abilitare la replica"

La VM di Azure potrebbe non venire visualizzata tra le opzioni nel [passaggio 2 della procedura di abilitazione della replica](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Questo problema potrebbe essere a causa di configurazione di Site Recovery toostale a sinistra nella macchina virtuale di Azure hello. configurazione non aggiornata Hello potrebbe rimanere in una macchina virtuale di Azure in hello seguenti casi:

- È abilitata la replica per hello macchina virtuale di Azure tramite il ripristino del sito e quindi eliminato insieme di credenziali di Site Recovery hello senza in modo esplicito la disabilitazione della replica su hello macchina virtuale.
- È abilitata la replica per hello macchina virtuale di Azure tramite il ripristino del sito e quindi eliminato il gruppo di risorse hello contenente l'insieme di credenziali di Site Recovery hello senza in modo esplicito la disabilitazione della replica su hello macchina virtuale.

### <a name="fix-hello-problem"></a>Risolvere il problema di hello

È possibile utilizzare [rimuovere uno script di configurazione di ripristino automatico di sistema non aggiornato](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) e rimuovere la configurazione di Site Recovery non aggiornati di hello in hello macchina virtuale di Azure. Dovrebbe essere hello macchina virtuale in [abilitare la replica: passaggio 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) dopo la rimozione di configurazione non aggiornata hello.


## <a name="next-steps"></a>Passaggi successivi
[Replicare le macchine virtuali di Azure](site-recovery-replicate-azure-to-azure.md)
