---
title: aaaSecurity avvisi per tipo nel Centro protezione di Azure | Documenti Microsoft
description: In questo articolo vengono illustrati tipi diversi di hello degli avvisi di sicurezza disponibili nel Centro protezione di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Informazioni sugli avvisi di sicurezza nel Centro sicurezza di Azure
In questo articolo consente di tipi diversi di hello toounderstand di avvisi di sicurezza e informazioni dettagliate correlate che sono disponibili nel Centro protezione di Azure. Per ulteriori informazioni su come toomanage avvisi e gli eventi imprevisti, vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset dei rilevamenti avanzati, aggiornamento tooAzure Security Center Standard. È disponibile una versione di valutazione gratuita di 60 giorni. tooupgrade, selezionare **tariffario** in hello [criteri di sicurezza](security-center-policies.md). toolearn informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Quali tipi di avvisi sono disponibili?
Centro sicurezza di Azure Usa una serie di [funzionalità di rilevamento](security-center-detection-capabilities.md) tooalert clienti toopotential attacchi propri ambienti di destinazione. Questi avvisi contengono informazioni importanti sui hello cosa ha attivato hello avviso, le risorse di hello, destinate e origine dell'attacco hello hello. informazioni di Hello incluse in un avviso variano in base al tipo di hello di analitica utilizzato toodetect hello minaccia. Anche gli eventi imprevisti possono contenere ulteriori informazioni contestuali utili nel corso dell'analisi di una minaccia.  In questo articolo vengono fornite informazioni sui seguenti tipi di avviso hello:

* Analisi del comportamento delle macchine virtuali (VMBA)
* Analisi di rete
* Analisi delle risorse
* Informazioni contestuali

## <a name="virtual-machine-behavioral-analysis"></a>Analisi del comportamento delle macchine virtuali
Centro sicurezza di Azure è possibile utilizzare risorse tooidentify compromesso analitica comportamentali in base all'analisi dei registri eventi di macchina virtuale. ad esempio eventi di creazione di processi ed eventi di accesso. Inoltre, è la correlazione con altri toocheck segnali per il supporto di prova di una campagna generalizzata.

> [!NOTE]
> Per altre informazioni sulle funzionalità di rilevamento del Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Analisi degli arresti anomali
Analisi della memoria dump di arresto anomalo del sistema è toodetect un metodo usato malware più sofisticati che è in grado di tooevade sicurezza tradizionali soluzioni. Probabilità tooreduce hello è rilevato dal prodotti antivirus scrivendo mai toodisk o crittografando i componenti software scritti toodisk provare a varie forme di malware. In questo modo hello malware difficile toodetect utilizzando gli approcci tradizionali antimalware. Questo tipo di malware, tuttavia, è possibile rilevare tramite l'analisi della memoria, poiché malware necessario lasciare tracce in memoria in ordine toofunction.

Quando si blocca software, un dump di arresto anomalo del sistema acquisisce una parte della memoria in fase di arresto anomalo di hello di hello. arresto anomalo di Hello potrebbe dipendere da problemi di sistema, generali dell'applicazione o malware. Analizzando memoria hello nel dump di arresto anomalo di hello, Centro sicurezza PC può rilevare le tecniche utilizzate tooexploit vulnerabilità nel software, accedere a dati riservati e furtivamente rende persistenti all'interno di un computer compromesso. Questa operazione viene eseguita con prestazioni minimo impatto toohosts analysis hello viene eseguita da hello terminare il centro di sicurezza.

Hello seguente i campi è toohello arresto anomalo del sistema dump avviso esempi comuni riportate più avanti in questo articolo:

* File di dump: Nome del file di dump di arresto anomalo di hello.
* PROCESSNAME: Nome del processo di arresto anomalo hello.
* PROCESSVERSION: Versione di hello processo arrestato in modo anomalo.

### <a name="shellcode-discovered"></a>Individuato attacco shellcode
ShellCode è payload hello che viene eseguito dopo una vulnerabilità del software di attacchi malware. Questo avviso indica che l'analisi di dump di arresto anomalo del sistema ha rilevato codice eseguibile che presenta un comportamento comunemente adottato dai payload dannosi. Sebbene anche il software non dannoso possa mostrare comportamenti simili, questo non fa generalmente parte delle normali procedure di sviluppo software.

esempio di avviso Shellcode Hello fornisce hello campo aggiuntivo seguente:

* : Hello indirizzo in memoria di shellcode hello.

Esempio di questo tipo di avviso:

![Avviso per shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Individuato hijack del modulo
Windows Usa le librerie a collegamento dinamico (DLL) tooallow software tooutilize comuni Windows funzionalità del sistema. Hijack DLL si verifica quando malware hello DLL carico ordine tooload dannoso i payload in memoria, in cui è possibile eseguire codice arbitrario. Questo avviso indica che analysis dump di arresto anomalo del sistema hello ha rilevato un modulo denominato in modo analogo che viene caricato da due percorsi diversi. Uno dei percorsi di hello caricato proviene da un percorso binario di sistema Windows comune.

In alcuni casi, gli sviluppatori di software lecito modificano l'ordine di caricamento DLL di hello per motivi non intenzionale, ad esempio la strumentazione, mediante l'estensione del sistema operativo Windows hello o estendere un'applicazione Windows. Centro sicurezza di Azure controlla se un modulo caricato conforme profilo sospette tooa toohelp distinguere tra le modifiche dannoso e potenzialmente grave toohello ordine di caricamento DLL. risultato Hello di questo controllo è indicato dal campo di "Firma" hello di avviso hello e verrà riflessi in base alla gravità hello di avviso hello, descrizione dell'avviso e procedura per la risoluzione degli avvisi. Se il modulo di hello è legittimo o dannoso, tooresearch analizzare hello nella copia del disco di hello Hijack modulo. Ad esempio, si può verificare una firma digitale del file hello o eseguire una scansione antivirus.

I campi comuni toohello descritti nella sezione precedente "Shellcode individuati" hello, questo avviso fornisce inoltre hello seguenti campi:

* FIRMA: Indica se il profilo di comportamenti sospetti tooa è conforme alle hello Hijack modulo.
* HIJACKEDMODULE: nome hello di hello soggetta a Hijack del modulo di sistema Windows.
* HIJACKEDMODULEPATH: percorso hello di hello soggetta a Hijack del modulo di sistema Windows.
* HIJACKINGMODULEPATH: percorso hello del modulo Hijack hello.

Esempio di questo tipo di avviso:

![Avviso di hijack del modulo](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Rilevato modulo Windows mascherato
Malware può utilizzare nomi comuni dei file binari di sistema di Windows (ad esempio, SVCHOST. Con estensione EXE) o moduli (ad esempio, NTDLL. DLL) troppo*di blend in* e nascondere la natura hello del software dannoso di hello agli amministratori di sistema. Questo avviso indica che l'analisi di dump di arresto anomalo del sistema hello rileva che tale file di dump di arresto anomalo del sistema hello contiene i moduli che utilizzano i nomi dei moduli di sistema di Windows, ma non soddisfano altri criteri che sono tipici della creazione di moduli di Windows. Analisi hello nella copia del disco del modulo di simulazione hello può fornire ulteriori informazioni sulla natura legittimo o malintenzionati di hello di questo modulo. L'analisi può includere:

* Verificare che il file hello in questione viene fornito come parte di un pacchetto software lecito.
* Verificare la firma digitale del file hello.
* Eseguire una scansione antivirus nel file hello.

I campi comuni toohello descritti in precedenza nella sezione "Shellcode individuati" hello, questo avviso fornisce inoltre hello campi aggiuntivi seguenti:

* Dettagli: Descrive se i metadati del modulo hello sono valido e se il modulo hello è stato caricato da un percorso di sistema.
* NOME: il nome di hello del modulo di Windows hello simulazione.
* PERCORSO: hello percorso toohello simulazione modulo di Windows.

Questo avviso anche estrae e consente di visualizzare alcuni campi di intestazione PE del modulo di hello, ad esempio "CHECKSUM" e "TIMESTAMP". Questi campi vengono visualizzati solo se i campi di hello sono presenti nel modulo hello. Vedere hello [specifica Microsoft PE e COFF](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) per informazioni dettagliate su questi campi.

Esempio di questo tipo di avviso:

![Avviso di modulo Windows mascherato](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Individuato file binario di sistema modificato
Malware può modificare i file binari del sistema principale in dati di access toocovertly ordine o furtivamente persistenti in un sistema compromesso. Questo avviso indica che analysis dump di arresto anomalo del sistema hello ha rilevato che i file binari di core del sistema operativo Windows sono stati modificati in memoria o su disco.

Gli sviluppatori di software legittimo modificano occasionalmente i moduli del sistema in memoria per motivi non dannosi, ad esempio per il pacchetto Detours o per la compatibilità delle applicazioni. Centro sicurezza di Azure controlla se modulo modificato hello conforme tooa sospette profilo toohelp distinguere tra i moduli dannosi e potenzialmente legittimi. risultato Hello di questo controllo è indicato in base alla gravità hello di avviso hello, descrizione dell'avviso e procedura per la risoluzione degli avvisi.

I campi comuni toohello descritti in precedenza nella sezione "Shellcode individuati" hello, questo avviso fornisce inoltre hello campi aggiuntivi seguenti:

* MODULENAME: Nome di hello modificato sistema binario.
* MODULEVERSION: Versione di hello modificato sistema binario.

Esempio di questo tipo di avviso:

![Avviso di file binario di sistema](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Processo sospetto eseguito
Centro sicurezza PC identifica un processo sospetto che viene eseguito nella macchina virtuale di destinazione hello e quindi attiva un avviso. rilevamento di Hello non cerca di nome specifico hello, ma cerca i parametri del file eseguibile hello. Pertanto, anche se l'utente malintenzionato hello Rinomina hello eseguibile, Centro sicurezza PC ancora possibile rilevare processo sospette hello.

Esempio di questo tipo di avviso:

![Avviso di processo sospetto](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Tentativi ripetuti di query sugli account di dominio
Centro sicurezza PC in grado di rilevare più tenta tooquery account di dominio Active Directory, di cui è in genere eseguite dagli utenti malintenzionati durante l'esplorazione di rete. Gli utenti malintenzionati possono sfruttare gli utenti di hello questa tecnica tooquery hello dominio tooidentify, identificare gli account amministratore di dominio di hello, identificare i computer hello sono controller di dominio, nonché di identificano hello potenziali dominio relazione di trust con altri domini.

Esempio di questo tipo di avviso:

![Avviso di tentativi di query multipli su account di dominio](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Sono stati enumerati i membri del gruppo Administrators locale

Centro sicurezza PC verrà tootrigger un avviso quando l'evento di sicurezza di hello 4798, in Windows Server 2016 e Windows 10, viene attivato. L'evento si verifica quando i gruppi Administrators locali vengono enumerati, attività in genere eseguita dagli utenti malintenzionati durante la ricognizione della rete. Gli utenti malintenzionati possono sfruttare questa identità di hello tooquery tecnica di utenti con privilegi amministrativi.

Esempio di questo tipo di avviso:

![Amministratore locale](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Combinazione anomala di lettere maiuscole e minuscole

Centro sicurezza PC attiverà un avviso quando rileva utilizzo hello di una combinazione di caratteri maiuscoli e minuscoli dalla riga di comando hello. Alcuni utenti non autorizzati possono utilizzare toohide questa tecnica dalla distinzione maiuscole/minuscole o hash basato su regole macchina.

Esempio di questo tipo di avviso:

![Combinazione anomala](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Sospetto attacco con Golden Ticket Kerberos

Un compromesso [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) chiave può essere utilizzata da un toocreate malintenzionato Kerberos "Golden ticket," consentendo hello autore dell'attacco tooimpersonate tutti gli utenti desiderano. Centro sicurezza PC verrà tootrigger un avviso quando viene rilevato questo tipo di attività.

> [!NOTE] 
> Per altre informazioni sui Golden Ticket Kerberos, vedere [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx) (Guida alla prevenzione del furto di credenziali in Windows 10).

Esempio di questo tipo di avviso:

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Creato account sospetto

Centro sicurezza attiverà un avviso quando viene creato un account molto somigliante a un account predefinito esistente con privilegi amministrativi. Questa tecnica può essere utilizzata da utenti malintenzionati toocreate malintenzionati account tooavoid essere rilevata dalla verifica risorse umane.
 
Esempio di questo tipo di avviso:

![Account sospetto](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Creata regola del firewall sospetta

Gli utenti malintenzionati tentino toocircumvent host sicurezza creando toocommunicate di applicazioni dannose tooallow regole firewall personalizzate con comando e il controllo o attacchi toolaunch tramite rete hello tramite hello compromesso host. Il Centro sicurezza attiverà un avviso quando rileva che è stata creata una nuova regola del firewall da un file eseguibile in una posizione sospetta.
 
Esempio di questo tipo di avviso:

![Regola del firewall](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Combinazione sospetta di HTA e PowerShell

Il Centro sicurezza attiverà un avviso quando rileva che un host HTA (HTML Application Host) di Microsoft sta avviando comandi di PowerShell. Questa è una tecnica utilizzata da utenti malintenzionati toolaunch dannoso gli script di PowerShell.
 
Esempio di questo tipo di avviso:

![HTA e PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Analisi di rete
Il sistema di rilevamento delle minacce di rete del Centro sicurezza funziona mediante la raccolta automatica di informazioni sulla sicurezza dal traffico IPFIX (Internet Protocol Flow Information Export) di Azure. Viene avviata l'analisi di queste informazioni, correlazione spesso informazioni provenienti da più origini, tooidentify minacce.

### <a name="suspicious-outgoing-traffic-detected"></a>Rilevamento di traffico in uscita sospetto
Dispositivi di rete possono essere individuati e profilati in quantità hello esattamente come altri tipi di sistemi. L'attacco ha in genere inizio con la scansione o la scansione sistematica delle porte. Nell'esempio riportato di seguito hello, sono sospetti Secure Shell (SSH) il traffico proveniente da una macchina virtuale. In questo scenario è possibile che si verifichi un attacco di forza bruta SSH o un attacco di scansione sistematica delle porte contro una risorsa esterna.

![Avviso per traffico in uscita sospetto](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Questo avviso offre informazioni che è possibile utilizzare risorse hello tooidentify che è stato utilizzato tooinitiate questo tipo di attacco. Questo avviso include anche informazioni tooidentify hello compromesso macchina, ora del rilevamento hello, oltre a protocollo hello e porta usata. Questo pannello offre inoltre un elenco dei passaggi di monitoraggio e aggiornamento che può essere utilizzato toomitigate questo problema.

### <a name="network-communication-with-a-malicious-machine"></a>Comunicazione di rete con un computer dannoso
Sfruttando i feed di intelligence per le minacce di Microsoft, il Centro sicurezza di Azure può rilevare i computer compromessi che comunicano con indirizzi IP dannosi. In molti casi, l'indirizzo dannoso hello è un centro di comando e controllo. In questo caso, il Centro sicurezza PC ha rilevato che la comunicazione hello è stata eseguita con malware cavallo caricatore (noto anche come [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![Avviso di comunicazione di rete](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Questo avviso vengono fornite informazioni che consentono di risorsa di hello tooidentify che era tooinitiate utilizzato questo tipo di attacco, hello attaccata di risorse, hello vittima IP, IP autore dell'attacco hello e ora del rilevamento hello.

> [!NOTE]
> Gli indirizzi IP attivi sono stati rimossi dallo screenshot per motivi di privacy.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Rilevato possibile attacco Denial of Service in uscita
Il traffico di rete anomala che ha origine da una macchina virtuale può provocare tootrigger Centro sicurezza PC un tipo di tipo denial of service potenziale di attacco.

Esempio di questo tipo di avviso:

![DoS in uscita](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Analisi delle risorse
Analisi delle risorse Centro sicurezza PC è incentrata sulla piattaforma come servizi un servizio (PaaS), ad esempio l'integrazione di hello con hello [rilevamento minacce del Database di SQL Azure](../sql-database/sql-database-threat-detection.md) funzionalità. In base ai risultati dell'analisi hello da queste aree, centro di sicurezza attiva un avviso di risorse.

### <a name="potential-sql-injection"></a>Potenziale attacco SQL injection
Attacchi SQL injection è un attacco in cui malware viene inserito in stringhe successivamente passate tooan istanza di SQL Server per l'analisi e l'esecuzione. È consigliabile verificare la presenza di vulnerabilità a questo tipo di attacco in qualsiasi procedura che crea istruzioni SQL, perché SQL Server esegue tutte le query sintatticamente valide che riceve. Rilevamento minacce SQL Usa machine learning, analisi comportamentale e anomalie rilevamento toodetermine sospette gli eventi che potrebbero essere eseguita nei database di SQL Azure. ad esempio:

* Tentativo di accesso al database da parte di un ex dipendente
* Attacchi SQL injection
* Database di produzione tooa insoliti di accesso da un utente a casa

![Avviso di potenziale SQL injection](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

informazioni Hello in questo avviso possono essere utilizzato tooidentify hello attaccata di risorse, ora del rilevamento hello e stato hello attacco hello. Fornisce inoltre un collegamento toofurther operazioni di analisi.

### <a name="vulnerability-toosql-injection"></a>La vulnerabilità tooSQL attacco intrusivo nel codice
Questo avviso viene generato in caso di rilevamento di un errore dell'applicazione in un database. Questo avviso può indicare che attacchi injection di tooSQL una possibile vulnerabilità.

![Avviso di potenziale SQL injection](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Accesso da posizione insolita
Questo avviso viene generato quando un evento di accesso da un indirizzo IP è stato rilevato nel server hello, che non è stata individuata in hello ultimo periodo.

![Avviso di accesso insolito](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Informazioni contestuali
Durante un'analisi più approfondita, gli analisti necessario un contesto aggiuntivo tooreach un esito sulla natura hello di minaccia hello e come toomitigate è.  Ad esempio, è stata rilevata un'anomalie di rete, ma senza conoscenza cos'altro sta accadendo in rete hello o con risorse di destinazione toohello considerare è ogni disco rigido toounderstand tootake quali azioni accanto. tooaid con quella, problemi di sicurezza possono includere elementi, gli eventi correlati e informazioni che possono aiutare si hello. Hello disponibilità di informazioni aggiuntive variano in base hello tipo di minaccia rilevata e hello configurazione dell'ambiente e non sarà disponibile per tutti gli eventi di sicurezza.

Se sono disponibili informazioni aggiuntive, verrà visualizzato in hello incidente sotto l'elenco di hello degli avvisi. Potrebbero essere riportate informazioni come:

- Eventi di cancellazione di log
- Dispositivi Plug and Play collegati da dispositivi sconosciuti
- Avvisi non operativi 

![Avviso di accesso insolito](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Vedere anche
In questo articolo è stato sui diversi tipi di hello di avvisi di sicurezza del Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure](security-center-incident.md)
* [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md)
* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md)
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md): domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.
