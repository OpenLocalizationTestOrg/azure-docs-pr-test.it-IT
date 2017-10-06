---
title: sicurezza dei dati Analitica aaaLog | Documenti Microsoft
description: Informazioni su come Log Analytics garantisce la privacy degli utenti e ne protegge i dati.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Sicurezza dei dati di Log Analytics
Microsoft è impegnata tooprotecting la privacy degli utenti e dei dati, offrendo al contempo software e servizi che aiutino a gestire hello infrastruttura IT dell'organizzazione. Sappiamo bene che quando si affidano i dati tooothers, necessarie per garantirne la sicurezza. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio.

La sicurezza e la protezione dei dati sono altamente prioritarie per Microsoft. Contattaci con eventuali domande, suggerimenti o problema riguardo a qualsiasi di hello le seguenti informazioni, compresi i criteri di sicurezza in [opzioni di supporto tecnico di Azure](http://azure.microsoft.com/support/options/).

Questo articolo illustra come i dati vengono raccolti, elaborati e protetti da Analitica di Log in hello Operations Management Suite (OMS). Si usa servizio web di agenti tooconnect toohello, utilizzare i dati operativi di System Center Operations Manager toocollect o recuperare dati da diagnostica di Azure per l'utilizzo da Analitica Log. Hello dati raccolti vengono inviati tramite Internet hello tramite l'autenticazione basata su certificato & 3 SSL toohello servizio Analitica di Log, che è ospitato in Microsoft Azure. Dati sono compressi dall'agente hello prima che venga inviato.

servizio Registro Analitica Hello gestisce in modo sicuro i dati basati su cloud tramite hello dei seguenti metodi:

* separazione dei dati
* conservazione dei dati
* sicurezza fisica
* gestione di eventi imprevisti
* conformità
* certificazioni degli standard di sicurezza

## <a name="data-segregation"></a>Separazione dei dati
I dati dei clienti vengono mantenuti separati logicamente in ogni componente hello servizio OMS. Tutti i dati vengono contrassegnati in base all'organizzazione. Tale contrassegno persiste per tutto hello del ciclo di vita dei dati e viene applicato a ogni livello del servizio hello. Ogni cliente ha un blob di Azure dedicato che ospita i dati a lungo termine hello

## <a name="data-retention"></a>Conservazione dei dati
Dati di ricerca log indicizzati vengono archiviati e conservati secondo tooyour prezzi piano. Per altre informazioni, vedere [Prezzi di Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft consente di eliminare i dati dei clienti di 30 giorni dopo la chiusura dell'area di lavoro OMS hello. Inoltre, Microsoft eliminerà hello Account di archiviazione di Azure in cui risiedono i dati di hello. L'eliminazione dei dati del cliente non comporta la distruzione delle unità fisiche.

Hello nella tabella seguente sono elencate alcune delle soluzioni disponibili di hello in OMS ed esempi hello tipi di dati che raccolti.

| **Soluzione** | **Tipi di dati** |
| --- | --- |
| Configuration Assessment |Dati di configurazione, metadati e dati di stato |
| Capacity Planning |Dati e metadati sulle prestazioni |
| Antimalware |Dati e metadati di configurazione |
| System Update Assessment |Metadati e dati di stato |
| Log Management |Log eventi definiti dall'utente, log eventi di Windows e/o log di IIS |
| Change Tracking |Inventario software e metadati dei servizi di Windows |
| SQL and Active Directory Assessment |Dati WMI, dati del Registro di sistema, dati sulle prestazioni e risultati delle visualizzazioni a gestione dinamica di SQL Server |

Hello nella tabella seguente vengono illustrati esempi di tipi di dati:

| **Tipo di dati** | **Fields** |
| --- | --- |
| Avviso |Alert Name, Alert Description, BaseManagedEntityId, Problem ID, IsMonitorAlert, RuleId, ResolutionState, Priority, Severity, Category, Owner, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configurazione |CustomerID, AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Evento |EventId, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, Number, Category, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Nota:** quando si scrive gli eventi con campi personalizzati nel registro eventi di Windows toohello, OMS li raccoglie. |
| Metadata |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Address, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Prestazioni |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Stato |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Sicurezza fisica
Hello Log Analitica nel servizio OMS è gestito da personale Microsoft e tutte le attività vengono registrate e possono essere controllate. servizio Hello viene eseguito interamente in Azure e soddisfa hello i criteri di progettazione comuni di Azure. È possibile visualizzare i dettagli sulla hello sicurezza fisica delle risorse di Azure a pagina 18 della hello [Cenni preliminari sulla sicurezza di Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Aree toosecure diritti di accesso fisico vengono modificate entro un giorno lavorativo per chi non ha la responsabilità per il servizio OMS hello, tra cui trasferimento e la chiusura. Per ulteriori informazioni hello globale dell'infrastruttura fisica usato [Datacenters Microsoft](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Gestione di eventi imprevisti
OMS dispone di un processo di gestione degli eventi imprevisti a cui aderiscono tutti i servizi di Microsoft. toosummarize, è:

* Utilizzare un modello di responsabilità condivisa in cui una parte di responsabilità di sicurezza appartiene tooMicrosoft e una parte appartiene toohello cliente
* Gestire gli eventi imprevisti correlati alla sicurezza di Azure
  * Avviare un'indagine quando viene rilevato un evento imprevisto
  * Valutare l'impatto di hello e la gravità dell'evento imprevisto da un membro del team di risposta agli eventi imprevisti nella chiamata. In base all'evidenza, valutazione hello può o non può generare un'ulteriore escalation toohello risposta team addetto alla sicurezza.
  * Diagnosi di un evento imprevisto da protezione risposta esperti tooconduct hello legali o tecnici analisi, identificare le strategie di contenimento, riduzione dei rischi e soluzione alternativa. Se il team addetto alla sicurezza hello ritiene che i dati dei clienti potrebbero non essere più esposto tooan illecito o non autorizzati di esecuzione parallela singoli del processo di notifica dell'evento imprevisto cliente hello inizia in parallelo.  
  * Stabilizzare e il ripristino da evento imprevisto di hello. il team di risposta agli eventi imprevisti Hello crea un problema di ripristino piano toomitigate hello. I passaggi per il contenimento della crisi, ad esempio la messa in quarantena dei sistemi coinvolti, possono verificarsi immediatamente e in parallelo con la diagnosi. Le misure di attenuazione più lungo termine può essere pianificati che si verificano dopo che è trascorso rischio immediato hello.  
  * Chiudere l'incidente hello e condurre una finale. team di risposta agli eventi imprevisti Hello Crea evento imprevisto, un finale che descrive i dettagli di hello di hello con hello intenzione toorevise criteri, procedure e processi tooprevent una ricorrenza dell'evento hello.
* Inviare ai clienti una notifica sugli eventi imprevisti relativi alla sicurezza
  * Determinare l'ambito hello di clienti interessati e tooprovide qualsiasi persona che ha un impatto più dettagliato di un avviso come possibili
  * Creare tooprovide una notifica ai clienti con informazioni sufficientemente dettagliate in modo che possano eseguire un'analisi più approfondita i loro e soddisfare gli impegni che sono destinate agli utenti finali tootheir durante non eccessivamente ritardando il processo di notifica hello.
  * Verificare e dichiarare l'evento imprevisto di hello, in base alle esigenze.
  * Informare i clienti con una notifica sull'evento imprevisto senza ritardi ingiustificati e nel rispetto dei termini legali o contrattuali. Le notifiche di eventi di sicurezza vengono recapitate tooone o più degli amministratori di un cliente con qualsiasi mezzo seleziona Microsoft, tra cui tramite posta elettronica.
* Svolgere la formazione e verificare la preparazione del team
  * Il personale di Microsoft sono sicurezza toocomplete richiesto e sensibilizzazione, che consente loro tooidentify e report sospetta la presenza di problemi di sicurezza.  
  * Gli operatori lavorando hello servizio Microsoft Azure hanno obblighi training aggiunta che racchiudono i sistemi toosensitive accesso ospita dati sui clienti.
  * Il personale di risposta di sicurezza Microsoft riceve una formazione specializzata per i ruoli ricoperti

In caso di perdita di dati di un cliente, viene inviata una notifica a tale cliente nell'arco di un giorno. Tuttavia, in OMS non si è mai verificata alcuna perdita di dati. Inoltre, vengono conservate le copie dei dati creati e distribuiti geograficamente.

Per ulteriori informazioni su come Microsoft risponde a eventi imprevisti toosecurity, vedere [risposta di sicurezza di Microsoft Azure nel Cloud hello](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Conformità
Hello sicurezza delle informazioni OMS software development e il servizio del team e il programma di governance supporta i requisiti di business e rispetti toolaws e alle normative, come descritto in [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) e [Microsoft Trust Center conformità](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Qui viene anche descritto il modo in cui OMS stabilisce i requisiti di sicurezza, identifica i controlli di sicurezza, gestisce e controlla i rischi. Ogni anno viene effettuata una revisione di criteri, standard, procedure e linee guida.

Ciascun membro del team di sviluppo di OMS riceve una formazione formale sulla sicurezza delle applicazioni. Internamente, viene usato un sistema di controllo della versione per lo sviluppo di software, che Ogni progetto software è protetta dal sistema di controllo della versione di hello.

Microsoft si avvale di un team per la sicurezza e conformità che supervisiona e valuta tutti i servizi in Microsoft. Ai responsabili della sicurezza delle informazioni costituiscono team hello e non sono associati con hello engineering reparti che lo sviluppo di OMS. ai responsabili della sicurezza Hello hanno i propri catena di gestione ed eseguire valutazioni indipendenti di prodotti e di sicurezza tooensure services e di conformità.

Il consiglio di amministrazione di Microsoft viene tenuto aggiornato tramite un report annuale su tutti i programmi per la sicurezza delle informazioni messi in atto da Microsoft.

Hello software development e il servizio team di OMS è attivamente impegnata con i team legale di Microsoft e di conformità di hello e altri tooacquire partner di settore certificazioni diversi.

## <a name="certifications-and-attestations"></a>Certificazioni e attestazioni
Hello di OMS Log Analitica soddisfa i requisiti seguenti:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Pagamento (PCI conforme) con Smart Card Industry Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) da hello Consiglio standard di sicurezza PCI.
* [Service Organization Controls (SOC) 1 di tipo 1 e SOC 2 di tipo 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2)
* [HIPAA e HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) per le società che hanno un contratto di società in affari HIPAA
* Criteri di progettazione comuni di Windows
* Microsoft Trustworthy Computing
* Come servizio di Azure, i componenti hello OMS Usa rispettare i requisiti di conformità tooAzure. Altre informazioni disponibili in [Centro protezione Microsoft - Conformità](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> In alcune certificazioni e attestazioni Log Analytics viene indicato con il nome precedente, *Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Flusso di dati sulla sicurezza del cloud computing
Hello diagramma seguente mostra un'architettura di sicurezza cloud come flusso hello delle informazioni dall'azienda e viene protetto come Sposta servizio Analitica Log toohello, visualizzato infine nel portale OMS hello. Diagramma di hello riporta anche informazioni aggiuntive su ogni passaggio.

![Immagine relativa alla sicurezza e alla raccolta dati di OMS](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Iscriversi a Log Analytics e raccogliere dati
Per tooLog Analitica del dati di toosend l'organizzazione, configurare gli agenti di Windows, gli agenti in esecuzione su macchine virtuali di Azure o gli agenti OMS per Linux. Se si usano agenti Operations Manager, quindi utilizzare una procedura guidata configurazione in hello Operations console tooconfigure li. Gli utenti (che potrebbero essere singoli utenti o un gruppo di persone) creare uno o più account OMS (aree di lavoro OMS) e registrare gli agenti utilizzando uno dei seguenti account hello:

* [ID aziendale](../active-directory/sign-up-organization.md)
* [Account Microsoft - Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Un'area di lavoro di OMS viene usata per raccogliere, aggregare, analizzare e presentare i dati. Ogni area di lavoro è univoco e un'area di lavoro viene utilizzato principalmente come mezzo toopartition dati. Ad esempio, è consigliabile toohave gestiti i dati di produzione con uno area di lavoro OMS e i dati di test gestiti con un'altra area di lavoro. Aree di lavoro consentono inoltre di accedere ai toohello dati un amministratore controllo utente. A ogni area di lavoro possono essere associati più account utente, ognuno dei quali può accedere a più aree di lavoro di OMS. Creare le aree di lavoro in base all'area data center. Ogni area di lavoro viene replicata tooother Data Center nell'area di hello, principalmente per la disponibilità del servizio OMS.

Per Operations Manager, al termine della procedura guidata configurazione hello, ogni gruppo di gestione di Operations Manager stabilisce una connessione con il servizio Registro Analitica hello. È quindi possibile utilizzare hello computer guidata toochoose i computer nel gruppo di gestione di hello autorizzati servizio toohello di toosend dati. Per altri tipi di agente, ciascuna collega in modo sicuro servizio OMS toohello.

Tutte le comunicazioni tra sistemi connessi e hello servizio Analitica di Log vengono crittografate.  Hello TLS (HTTPS) viene utilizzato per la crittografia.  processo SDL Microsoft Hello è seguito tooensure Analitica Log sia aggiornato con miglioramenti più recenti di hello in protocolli di crittografia.

Ogni tipo di agente raccoglie dati per Log Analytics. tipo di Hello di dati raccolti è dipende dai tipi hello di soluzioni usati. È possibile visualizzare un riepilogo di una raccolta di dati a [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md). Inoltre, per la maggior parte delle soluzioni sono disponibili altre informazioni dettagliate sulla raccolta. Una soluzione è costituita da un bundle di visualizzazioni, query di ricerca, regole di raccolta dati e logica di elaborazione predefinite. Solo gli amministratori possono utilizzare Log Analitica tooimport una soluzione. Dopo l'importazione, la soluzione hello è spostato toohello i server di gestione Operations Manager (se usati) e quindi tooany agenti che si sono scelto. Hello agenti raccoglieranno quindi i dati di hello.

## <a name="2-send-data-from-agents"></a>2. Invio dei dati dagli agenti
Vengono registrati tutti i tipi di agenti con una chiave di registrazione e viene stabilita una connessione sicura tra agente hello e il servizio Registro Analitica hello tramite l'autenticazione basata sui certificati e SSL con la porta 443. OMS Usa toogenerate un archivio segreto e gestire le chiavi. Le chiavi private vengono ruotate ogni 90 giorni e vengono archiviate in Azure e sono gestite dal hello Azure operazioni che seguono strict normative e procedure di conformità.

Con Operations Manager, si registra un'area di lavoro con il servizio Registro Analitica hello e viene stabilita una connessione HTTPS sicura tra server di gestione di Operations Manager hello.

Per gli agenti di Windows in esecuzione in macchine virtuali di Azure, una chiave di archiviazione di sola lettura è tooread utilizzati gli eventi di diagnostica in tabelle di Azure.

Se tutti gli agenti sono il servizio toohello toocommunicate Impossibile per qualsiasi motivo, hello dati raccolti vengono archiviati in locale in una cache temporanea e il server di gestione di hello proverà dati hello tooresend ogni 8 minuti per 2 ore. dati memorizzati nella cache dell'agente di Hello sono protetto da archivio credenziali del sistema operativo hello. Se il servizio hello: Impossibile elaborare dati hello dopo due ore, gli agenti di hello verranno inseriti nella coda dati hello. Se la coda hello è pieno, OMS avvia l'eliminazione di tipi di dati, a partire da dati sulle prestazioni. limite della coda agente Hello è una chiave del Registro di sistema, pertanto è possibile modificare, se necessario. I dati raccolti vengono compressi e inviati toohello servizio ignorando i database locali, in modo non aggiunge alcun toothem di carico. Dopo la raccolta di hello invio dei dati, viene rimosso dalla cache di hello.

Come descritto in precedenza, i dati dagli agenti vengono inviati tramite SSL tooMicrosoft Data Center di Azure. Facoltativamente, è possibile utilizzare ExpressRoute tooprovide aggiuntiva di sicurezza per i dati di hello. ExpressRoute è un modo toodirectly connettersi tooAzure da una rete WAN esistente, ad esempio un multi-protocollo di etichetta commutazione VPN (MPLS), fornito da un provider di servizi di rete. Per altre informazioni, vedere [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. il servizio Registro Analitica hello riceve ed elabora i dati
servizio Registro Analitica Hello assicura che i dati in arrivo provengano da un'origine attendibile convalida i certificati e l'integrità dei dati di hello con l'autenticazione di Azure. Hello dati non elaborati vengono quindi archiviati come blob in [archiviazione di Microsoft Azure](../storage/common/storage-introduction.md) e non è crittografato. Tuttavia, ogni blob di archiviazione di Azure offre un set di set univoco di chiavi, che è accessibile toothat solo utente. tipo di Hello di dati archiviati dipende dai tipi di hello di soluzioni che sono stati importati e usati toocollect dati. Quindi, hello servizio Analitica Log elabora dati non elaborati di hello per il blob di archiviazione di Azure hello.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Utilizzare i dati di Log Analitica tooaccess hello
È possibile accedere tooLog Analitica nel portale OMS hello tramite account aziendale hello o account Microsoft che è configurato in precedenza. Tutto il traffico tra il portale di OMS hello e Analitica di Log in OMS viene inviato tramite un canale HTTPS sicuro. Quando si usa il portale di OMS hello, viene generato un ID di sessione nel client utente hello (browser web) e dati viene archiviati in una cache locale finché non hello sessione viene terminata. Quando termina, cache di hello viene eliminata. I cookie sul lato client, che non contengono informazioni personali, non vengono rimossi automaticamente. I cookie di sessione sono protetti e contrassegnati HTTPOnly. Dopo un periodo di inattività predeterminato, hello OMS portale sessione terminata.

Tramite il portale di OMS hello, è possibile esportare i file di dati tooa CSV e sarà possibile accedere tramite le API di ricerca di dati. Esportazione CSV è limitato too50, 000 righe per i dati di API e di esportazione è too5 con restrizioni, 000 righe per ogni ricerca.

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione a Log Analitica](log-analytics-get-started.md) toolearn informazioni sul Log Analitica e get attivo e in esecuzione in minuti.
