---
title: Classificazione per Azure aaaData | Documenti Microsoft
description: In questo articolo fornisce un'introduzione toohello nozioni fondamentali sulla classificazione dei dati ed evidenzia il relativo valore, in particolare nel contesto di hello del cloud computing e l'utilizzo di Microsoft Azure
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Classificazione dei dati per Azure
In questo articolo fornisce un'introduzione toohello nozioni fondamentali sulla classificazione dei dati ed evidenzia il relativo valore, in particolare nel contesto di hello del cloud computing e l'utilizzo di Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Concetti fondamentali della classificazione dei dati per Azure
Per ottimizzare la classificazione dei dati in un'organizzazione, è necessario conoscere a fondo le esigenze dell'organizzazione e sapere con esattezza dove si trovano gli asset di dati.  

Gli stati di base dei dati sono tre: 

* Inattivi 
* In corso 
* In transito 

Tutti i tre stati richiedono soluzioni tecniche univoche per la classificazione dei dati, ma hello applicati principi della classificazione dei dati deve essere hello uguale per ogni. I dati che viene classificati come riservati devono toostay riservati quando al resto, nel processo e in transito. 

I dati possono anche essere strutturati o non strutturati. Il processo di classificazione tipico per hello strutturato dati trovati nel database e fogli di calcolo sono toomanage lunga e complessa minore rispetto a quelle per i dati non strutturati, ad esempio documenti, codice sorgente e posta elettronica. 

> [!TIP]
> Per altre informazioni sulle funzionalità di Azure e sulle procedure consigliate per la crittografia dei dati, vedere [Procedure consigliate per la crittografia dei dati in Azure](azure-security-data-encryption-best-practices.md)
> 
> 

In generale, le organizzazioni avranno più dati non strutturati che strutturati. Indipendentemente dal fatto che i dati siano strutturati o, è importante per si toomanage dati maiuscole/minuscole. Se implementata correttamente, la classificazione dei dati consente di garantire che i dati sensibili o riservati risorse vengono gestite con maggiore supervisione di asset di dati che sono considerati toodistribute pubblico o disponibile. 

### <a name="controlling-access-toodata"></a>Controllo dell'accesso toodata
L'autenticazione e l'autorizzazione vengono spesso confuse e i rispettivi ruoli fraintesi. In realtà sono molto diversi, come illustrato nella seguente illustrazione hello.  

![Accesso e controllo dei dati](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Autenticazione
L'autenticazione in genere include almeno due parti: un ID utente o nome utente, tooidentify un utente e un token, ad esempio una password, tooconfirm che hello credenziali nome utente è valido. il processo di Hello non fornisce hello utente autenticato con accesso tooany elementi o servizi. Consente di verificare che l'utente hello è l'identità che sono.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) offre servizi di identità basati su cloud che consentono di tooauthenticate e autorizzano gli utenti. 
> 
> 

### <a name="authorization"></a>Authorization
L'autorizzazione è il processo di hello di fornire un tooaccess possibilità di hello utente autenticato, un'applicazione, i set di dati, i file di dati o un altro oggetto. L'assegnazione di utenti autenticati hello diritti toouse, modificare o eliminare gli elementi che possono accedere richiede classificazione toodata attenzione. 

Autorizzazione ha esito positivo richiede l'implementazione di un meccanismo toovalidate dei singoli utenti tooaccess file e le informazioni in base a una combinazione di ruolo, i criteri di sicurezza e considerazioni sui criteri di rischio. Ad esempio, dati da applicazioni di specifiche line-of-business (LOB) potrebbero non essere necessario toobe accessibile da tutti i dipendenti e solo un piccolo subset di dipendenti probabilmente avrà bisogno di accesso toohuman i file di risorse (h). Ma per le organizzazioni toocontrol chi può accedere a dati, nonché come e quando, un sistema efficace per autenticare gli utenti deve essere presenti. 

> [!TIP]
> in Microsoft Azure, assicurarsi che tooleverage gestire accesso controllo (RBAC) toogrant solo hello quantità di accesso che gli utenti devono tooperform i processi. Lettura [utilizzare accesso toomanage assegnazioni di ruolo tooyour risorse di Azure Active Directory](../active-directory/role-based-access-control-configure.md) per ulteriori informazioni. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Ruoli e responsabilità nel cloud computing
Anche se i provider di cloud consente di gestire i rischi, i clienti devono tooensure tale gestione classificazione dei dati e imposizione è implementato correttamente tooprovide hello livello appropriato di servizi di gestione dati.  

Classificazione dei dati responsabilità variano in base quale modello di servizio cloud è presente, come illustrato nella seguente illustrazione hello. tre modelli di servizio cloud primario Hello sono infrastruttura come servizio (IaaS), piattaforma come servizio (PaaS) e software come servizio (SaaS). Implementazione di meccanismi di classificazione dei dati verrà inoltre variano in base l'affidabilità hello e le aspettative del provider di cloud hello. 

![Ruoli](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Anche se si è responsabili per classificare i dati, i provider di cloud devono fare impegni scritti su come verranno sicura e mantenere la privacy hello hello dati del cliente archiviati all'interno di cloud.  

* **I provider IaaS** requisiti sono limitati tooensuring che hello ambiente virtuale in grado di gestire funzionalità di classificazione dei dati e i requisiti di conformità. I provider IaaS presentano un ruolo più piccolo nella classificazione dei dati perché è necessario solo tooensure che i dati dei clienti soddisfi i requisiti di conformità. Tuttavia, i provider ancora necessario assicurarsi che gli ambienti virtuali in valuta i requisiti di classificazione dei dati in aggiunta toosecuring centri dati.
* **Provider PaaS** responsabilità possono essere combinate, perché piattaforma hello può essere utilizzata per la protezione tooprovide approccio a più livelli per uno strumento di classificazione. Provider PaaS potrebbe essere responsabile per l'autenticazione e probabilmente alcune regole di autorizzazione e deve fornire protezione e del livello di applicazione tootheir funzionalità classificazione dei dati. Molto come i provider IaaS, PaaS provider necessario tooensure propria piattaforma conforme con gli eventuali requisiti di classificazione dati rilevanti.
* **I provider SaaS** viene spesso considerata come parte di una catena di autorizzazione e sarà necessario tooensure che hello dati archiviati in un'applicazione SaaS hello possono essere controllate dal tipo di classificazione. Applicazioni SaaS possono essere utilizzate per le applicazioni LOB e per loro natura necessario tooprovide hello significa tooauthenticate e autorizzare i dati archiviati e utilizzati. 

## <a name="classification-process"></a>Processo di classificazione
Molte organizzazioni di comprendere hello necessario per la classificazione dei dati e trovano ad affrontare un problema di base tooimplement: dove toobegin?

Un modo efficace e semplice la classificazione dei dati tooimplement è toouse hello piano, controllo, ACT modello da [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). figura seguente Hello grafici attività hello di classificazione dei dati toosuccessfully necessario implementare questo modello.  

1. **PLAN**. Identificare gli asset di dati, un programma di classificazione hello dati responsabile toodeploy e sviluppare i profili di protezione. 
2. **DO**. Dopo aver concordati criteri di classificazione dei dati, distribuire l'applicazione hello e implementare le tecnologie di imposizione in base alle esigenze per i dati riservati.  
3. **CHECK**. Controllare e convalidare i criteri di classificazione di hello tooensure che strumenti hello e metodi utilizzati in modo efficace sono l'indirizzamento di report. 
4. **ACT**. Esaminare lo stato di hello di accesso ai dati e file e i dati che richiedono revisione utilizzando una riclassificazione e modifiche tooadopt metodologia di revisione e tooaddress nuovi rischi.  

![Plan, Do, Check, Act](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Selezionare un modello di terminologia adatto alle proprie esigenze
Esistono diversi tipi di processi per classificare i dati, inclusi i processi manuali, i processi in base alla posizione classificare i dati in base alla posizione di un utente o del sistema, basate su applicazioni processi come la classificazione specifico del database e automatizzati processi utilizzati da varie tecnologie, alcuni dei quali sono descritti nella sezione "Protezione dei dati riservati" hello più avanti in questo articolo.  

Questo articolo presenta due modelli di terminologia generalizzati basati su modelli di uso comune e riconosciuti nel settore. Questi modelli di terminologia, che fornisce tre livelli di sensibilità di classificazione, vengono visualizzati in hello nella tabella seguente.  

> [!NOTE]
> Quando la classificazione di un file o una risorsa che combina dati che verrebbero classificati in genere diversi livelli di livello più elevato di hello di classificazione presenta devono stabilire hello classificazione generale. Ad esempio, un file contenente dati sensibili e con restrizioni deve essere classificato come con restrizioni.  
> 
> 

| **Riservatezza** | **Modello di terminologia 1** | **Modello di terminologia 2** |
| --- | --- | --- |
| Alto |Riservate |Con restrizioni |
| Media |Solo per uso interno |Sensibili |
| Basso |Pubblico |Senza restrizioni |

#### <a name="confidential-restricted"></a>Riservate (con restrizioni)
Le informazioni sono classificate come riservati o con restrizioni includono dati che possono essere tooone irreversibile o di più utenti singoli e/o organizzazioni se perso o compromesso. Tali informazioni spesso viene forniti con cadenza "necessità tooknow" e potrebbero includere: 

* Dati personali, incluse le informazioni personali, ad esempio codici fiscali o numeri di carta di identità, numeri di passaporto, numeri di carta di credito, numeri di patente, cartelle cliniche e numeri ID polizza assicurativa sanitaria.  
* Record finanziari, inclusi i numeri di conto finanziario, ad esempio numeri di conto corrente o di investimento. 
* Materiale aziendale, ad esempio documenti o dati che costituiscono una proprietà intellettuale univoca o specifica.  
* Dati legali, incluso il potenziale materiale coperto da segreto professionale. 
* Dati di autenticazione, incluse le chiavi di crittografia private, le coppie nome utente e password o altre sequenze di identificazione, ad esempio file di chiave biometrica privata. 

I dati classificati come riservati hanno spesso requisiti normativi e di conformità per la gestione dei dati. 

#### <a name="for-internal-use-only-sensitive"></a>Solo per uso interno (sensibili)
Le informazioni classificate con sensibilità media includono file e dati che non hanno gravi conseguenze per una persona e/o un'organizzazione, se vengono persi o eliminati definitivamente. Tali informazioni possono includere: 

* Messaggio di posta elettronica, la maggior parte delle quali può essere eliminata o distribuita senza causare una situazione di crisi (escluse le cassette postali o posta elettronica da utenti che sono identificati nella classificazione riservate hello).  
* Documenti e file che non includono dati riservati.

In genere, questa classificazione include tutto ciò che non è riservato. Questa classificazione può includere la maggior parte dei dati aziendali, perché la maggior parte dei file gestiti o usati quotidianamente possono essere classificati come sensibili. Con l'eccezione di hello dei dati sono reso pubblico o riservate, tutti i dati all'interno di un'organizzazione aziendale possono essere classificati come sensibile per impostazione predefinita. 

#### <a name="public-unrestricted"></a>Pubbliche (senza restrizioni)
Informazioni che viene classificate come public includono file di dati e che non sono critiche toobusiness esigenze o operazioni. Questa classificazione è inoltre possibile includere dati che sono stato intenzionalmente rilasciata toohello pubblico per l'uso, ad esempio marketing materiale o premere annunci. Questa classificazione può includere anche altri dati, ad esempio messaggi di posta elettronica indesiderata archiviati da un servizio di posta elettronica. 

### <a name="define-data-ownership"></a>Definire la proprietà dei dati
È importante tooestablish una deselezionare privative catena di proprietà per tutti gli asset di dati. Hello nella tabella seguente identifica i ruoli di proprietà dei dati diverse in attività di classificazione dei dati e i relativi diritti rispettivi.  

| **Ruolo** | **Creare** | **Modifica/Eliminazione** | **Delega** | **Lettura** | **Archiviazione/Ripristino** |
| --- | --- | --- | --- | --- | --- |
| Proprietario |X |X |X |X |X |
| Responsabile | | |X | | |
| Amministratore | | | | |X |
| Utente\* | |X | |X | |

**Un responsabile può concedere agli utenti diritti aggiuntivi, ad esempio di modifica ed eliminazione* 

> [!NOTE]
> Questa tabella è solo un esempio rappresentativo e non include un elenco completo di ruoli e diritti. 
> 
> 

Hello **proprietario dell'asset dati** hello creatore originale dei dati di hello, che possono delegare la proprietà e l'assegnazione di un responsabile. Quando viene creato un file, il proprietario di hello deve essere in grado di tooassign una classificazione, che significa che hanno un toounderstand responsabilità requisiti toobe classificati come riservati in base ai criteri dell'organizzazione. Tutti i dati del proprietario di un asset di dati possono essere classificati automaticamente come solo per uso interno (sensibili) a meno che non sia responsabile della proprietà o della creazione di tipi di dati riservati (con restrizioni). Spesso, il ruolo del proprietario hello verrà modificato dopo hello dati riservati. Proprietario hello potrebbe essere ad esempio, creare un database di classificazione delle informazioni e lasciare il responsabile di dati toohello diritti.  

> [!NOTE]
> i proprietari di asset di dati spesso usano una combinazione di servizi, dispositivi e supporti, alcuni dei quali sono personali e alcuni dei quali appartengono toohello organizzazione. Criteri organizzativi chiari consentono di assicurarsi che l'utilizzo di dispositivi, ad esempio portatili e Smart Device, segua le linee guida relative alla classificazione dei dati.  
> 
> 

Hello **responsabile asset di dati** assegnato dal proprietario dell'asset hello (o un loro delegato) toomanage hello asset secondo tooagreements con proprietario dell'asset hello o in base ai requisiti di criteri applicabili. In teoria, il ruolo di responsabile hello può essere implementato in un sistema automatico. Un responsabile dell'asset assicura che i controlli di accesso necessari vengono forniti e responsabile della gestione e protezione delle risorse di delega tootheir attenzione. responsabilità di Hello del responsabile di asset hello potrebbe includere:  

* Protezione di asset hello in conformità con la direzione del proprietario dell'asset hello o conformi proprietario dell'asset hello 
* Verifica della conformità con i criteri di classificazione 
* Informare i proprietari della risorsa di qualsiasi modifica tooagreed-su controlli e/o protezione procedure toothose precedente le modifiche apportate hanno effetto 
* Proprietario dell'asset toohello Reporting sulla rimozione di tooor modifiche delle responsabilità del responsabile dell'asset di hello 
* Un **amministratore** ha il compito di verificare che venga mantenuta l'integrità, ma non è né un utente, né il responsabile né il proprietario di un asset di dati. Infatti, molti ruoli di amministratore di forniscono servizi di gestione di dati contenitore senza la necessità di accedere ai dati toohello. il ruolo di amministratore di Hello include backup e ripristino dei dati di hello, gestione dei record di risorse hello, e scegliendo l'acquisizione e operativo hello dispositivi e archiviazione tale asset hello casa. 
* utente di asset Hello include chiunque disponga dei privilegi di accesso toodata o un file. Assegnazione di accesso viene spesso delegata dal responsabile di hello proprietario toohello asset.  

### <a name="implementation"></a>Implementazione
Considerazioni sulla gestione di si applicano le metodologie di classificazione tooall. Queste considerazioni necessitano tooinclude dettagli sull'utente, quali, in cui, quando e perché un asset di dati potrebbe essere utilizzato, accedere, modificato o eliminato. Gestione asset tutti deve essere effettuata con una conoscenza di come un'organizzazione viste relativi rischi, ma una metodologia semplice può essere applicata come definito nel processo di classificazione dei dati hello. Considerazioni aggiuntive per la classificazione dei dati includono hello introduzione di nuove applicazioni e strumenti, la gestione delle modifiche dopo aver implementato un metodo di classificazione.  

### <a name="reclassification"></a>Riclassificazione
Riclassificazione o modifica dello stato di classificazione hello di un asset di dati deve toobe eseguita quando un utente o il sistema determina l'importanza dell'asset di dati che hello o il profilo di rischio è stato modificato. Ciò è importante per assicurare che lo stato di classificazione hello continua toobe corrente e valido. La maggior parte del contenuto non classificato manualmente può essere classificata automaticamente o in base all'utilizzo da un responsabile o da un proprietario dei dati. 

### <a name="manual-data-reclassification"></a>Riclassificazione manuale dei dati
In teoria, questo sforzo assicurarsi che i dettagli di hello di una modifica sono acquisiti e controllati. motivo più probabile Hello riclassificazione manuale sarebbe per motivi di riservatezza, o per i record mantenuti in formato carta o dati di tooreview un requisito che è stato originariamente classificazioni non corrette. Perché questo white paper considera la classificazione dei dati e lo spostamento dati nel cloud toohello, impegno manuale riclassificazione richiedono attenzione nel caso per caso e una verifica della gestione dei rischi sarebbe ideale tooaddress i requisiti di classificazione. Tale tentativo verrebbe in genere, considerare i criteri dell'organizzazione hello sulle operazioni necessarie toobe classificati, hello lo stato di classificazione predefinito (tutti i dati e file riservati, ma non riservato) e accettare le eccezioni per i dati ad alto rischio. 

### <a name="automatic-data-reclassification"></a>Riclassificazione automatica dei dati
Riclassificazione automatica dei dati utilizza hello stesso generale della regola di classificazione manuale. eccezione di Hello è soluzioni automatiche garantisce che le regole vengono seguite e applicate in base alle esigenze. La classificazione dei dati può essere eseguita nell'ambito di un criterio di applicazione della classificazione dei dati, che può essere applicato quando i dati sono archiviati, sono in uso e in transito usando la tecnologia di autorizzazione.

* In base all'applicazione. Per impostazione predefinita, l'uso di determinate applicazioni imposta un livello di classificazione. Ad esempio, i dati del software CRM (Customer Relationship Management), delle risorse umane e degli strumenti di gestione dei record sanitari sono riservati per impostazione predefinita. 
* In base alla posizione. La posizione dei dati consente di identificare la riservatezza dei dati. Ad esempio, i dati archiviati da un HR o di reparto finanziario sono probabilmente toobe riservato in natura.  

### <a name="data-retention-recovery-and-disposal"></a>Conservazione, ripristino ed eliminazione dei dati
Il ripristino e l'eliminazione dei dati, come la riclassificazione, sono aspetti essenziali della gestione degli asset di dati. deve essere definiti da un criterio di conservazione dati Hello principi per il ripristino dei dati e l'eliminazione e applicati in hello stesso modo riclassificazione dati; tale tentativo verrebbe eseguita da ruoli di amministratore e responsabile hello come attività di collaborazione.  

Errore toohave criteri di conservazione dati potrebbe essere toocomply errore o di perdita di dati con requisiti legali e normativi l'individuazione. La maggior parte delle organizzazioni che non dispone di un criterio di conservazione di dati definito chiaramente tendono toouse un criterio di conservazione predefinito "mantenere tutti gli elementi". Tuttavia, tale criterio di conservazione presenta rischi aggiuntivi negli scenari di servizi cloud. 

Criteri di conservazione dati per il provider di servizi cloud, ad esempio, possono essere considerato come hello "durata" di sottoscrizione hello (fino a quando il servizio di hello è a pagamento per, conservazione dei dati di hello). È possibile che un contratto di questo tipo non risponda ai criteri di conservazione aziendali o normativi. La definizione di un criterio per i dati riservati può assicurare che i dati vengano archiviati e rimossi in base alle procedure consigliate. Inoltre, un criterio di archiviazione è possibile crearle tooformalize una comprensione dei dati deve essere eliminata e quando. 

Criteri di conservazione dei dati devono prendere in considerazione hello necessario ai requisiti normativi e i requisiti di conformità, nonché i requisiti di conservazione legali aziendali. I dati classificati possono far sorgere dubbi sulla durata della conservazione e sulle eccezioni per i dati archiviati con un provider. È più probabile che tali dubbi riguardino i dati non classificati correttamente. 

> [!TIP]
> altre informazioni sui criteri di conservazione dei dati di Azure e più leggendo hello [contratto di sottoscrizione Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Protezione dei dati riservati
Dopo che i dati riservati, ricerca e l'implementazione di dati riservati di modi tooprotect diventa parte integrante di qualsiasi strategia di distribuzione di protezione dati. Protezione dei dati riservati richiede di archiviazione e trasmettere le architetture tradizionali nonché come cloud hello dati toohow ulteriore attenzione. 

In questa sezione vengono fornite informazioni alcune tecnologie in grado di automatizzare attività di imposizione toohelp proteggere i dati che sono stati classificati come riservati. 

Come hello illustrata nella figura seguente, queste tecnologie possono essere distribuite come soluzioni basate su cloud o locali, o in una modalità ibrida, con alcune delle loro distribuiti in locale e parte nel cloud hello. (Alcune tecnologie, ad esempio la crittografia e rights management, estendono anche dispositivi toouser.)  

![Tecnologie](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Software di Rights Management
Una soluzione per evitare la perdita di dati è il software di Rights Management. A differenza degli approcci che tentano di flusso di hello toointerrupt di informazioni in uscita punti in un'organizzazione, viene utilizzato software di gestione dei diritti a livelli all'interno di tecnologie di archiviazione di dati. I documenti vengono crittografati e il controllo su chi può decrittografarli usa controlli di accesso definiti in una soluzione per il controllo dell'autenticazione, ad esempio un servizio directory.  

> [!TIP]
> è possibile utilizzare Azure Rights Management (Azure RMS) come dati tooprotect soluzione hello informazioni protezione in scenari diversi. Per altre informazioni su questa soluzione di Azure, vedere [Informazioni su Azure Rights Management](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms).
> 
> 

Alcuni dei vantaggi di hello del software di gestione dei diritti: 

* Informazioni sensibili protette. Gli utenti possono proteggere i dati direttamente usando le applicazioni abilitate per Rights Management. Non sono necessari passaggi aggiuntivi: la creazione di documenti, l'invio di posta elettronica e la pubblicazione di dati offrono un'esperienza di protezione dei dati personali coerente. 
* La protezione viene trasferita con dati hello. I clienti rimangono nel controllo di chi ha accesso ai dati tootheir cloud hello, infrastruttura IT o il desktop dell'utente hello. Le organizzazioni possono scegliere tooencrypt i propri dati e limitare l'accesso in base a tootheir requisiti aziendali. 
* Criteri di protezione delle informazioni predefiniti. Gli amministratori e gli utenti possono usare criteri standard per diversi scenari aziendali comuni, ad esempio "Informazioni aziendali riservate - Sola lettura" e "Non inoltrare". Un'ampia gamma di diritti di utilizzo sono supportati, ad esempio lettura, copia e stampa, salvare, modifica e di inoltro tooallow flessibilità nella definizione dei diritti di utilizzo personalizzato. 

> [!TIP]
> È possibile proteggere i dati in Archiviazione di Azure usando la funzionalità [Crittografia del servizio di archiviazione di Azure](../storage/storage-service-encryption.md) per i dati inattivi. È inoltre possibile utilizzare [crittografia del disco Azure](azure-security-disk-encryption.md) toohelp proteggere i dati contenuti nei dischi virtuali utilizzati per macchine virtuali di Azure.
> 
> 

### <a name="encryption-gateways"></a>Gateway di crittografia
Gateway di crittografia operano nei propri servizi di crittografia tooprovide livelli reindirizzando tutti i dati basati su toocloud di accesso. Questo approccio non va confuso con quello di una rete privata virtuale (VPN). Gateway di crittografia sono tooprovide progettato un trasparente soluzioni basate su toocloud dei livelli.   

Gateway di crittografia può fornire un mezzo toomanage e protezione dei dati è state classificate come riservati mediante la crittografia dati hello in transito nonché i dati inattivi.  

Gateway di crittografia vengono inseriti nel flusso di dati hello tra i dispositivi utente e applicazione data center di servizi di crittografia/decrittografia di tooprovide. Queste soluzioni, come le VPN, sono prevalentemente soluzioni locali. Sono progettati tooprovide con il controllo sulle chiavi di crittografia, che consente di riducono il rischio di hello di inserimento dati hello e gestione delle chiavi con un provider di terze parti. Tali soluzioni sono progettate, come crittografia, toowork in modo trasparente e senza problemi tra utenti e servizio hello. 

> [!TIP]
> è possibile utilizzare le reti locali tooextend ExpressRoute di Azure nel cloud di Microsoft hello su una connessione privata dedicata. Per altre informazioni su questa funzionalità, vedere [Panoramica tecnica relativa a ExpressRoute](../expressroute/expressroute-introduction.md). Un'altra opzione per la connettività cross-premise tra la rete locale e [Azure è una VPN da sito a sito](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Prevenzione della perdita dei dati
Perdita di dati (talvolta definito tooas perdita di dati) è un fattore importante e prevenire la perdita di dati esterni tramite Insider intenzionali che accidentali hello è fondamentale per molte organizzazioni.  

Le tecnologie di prevenzione della perdita dei dati (DLP) consentono di assicurarsi che soluzioni come i servizi di posta elettronica non trasmettano i dati classificati come riservati. Le organizzazioni possono usufruire delle funzionalità DLP di prodotti esistenti toohelp evitare perdite di dati. Tali funzionalità utilizzano i criteri che possono essere facilmente creati da zero o un modello fornito dal provider di software hello.  

Tecnologie DLP è possono eseguire analisi approfondita del contenuto tramite corrispondenze di parole chiave, corrispondenze del dizionario, la valutazione dell'espressione regolare e altro contenuto toodetect esame del contenuto che viola i criteri dell'organizzazione DLP. Ad esempio, DLP possono aiutare a evitare la perdita di hello di hello seguenti tipi di dati: 

* Codici fiscali o numeri di carta di identità 
* Informazioni bancarie 
* Numeri di carta di credito  
* Indirizzi IP 

Alcune tecnologie DLP forniscono anche la configurazione DLP hello possibilità toooverride hello (ad esempio, se un'organizzazione deve elaboratore retribuzioni tooa di tootransmit Social Security number information). Inoltre, è possibile tooconfigure DLP in modo che gli utenti vengono informati prima di tentare anche informazioni riservate toosend che non dovrebbero essere trasmessi. 

> [!TIP]
> è possibile utilizzare Office 365 DLP funzionalità tooprotect i documenti. Per altre informazioni, vedere il blog sui [controlli di conformità di Office 365 per la prevenzione della perdita dei dati](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/).
> 
> 

## <a name="see-also"></a>Vedere anche
* [Procedure consigliate per la crittografia in Azure](azure-security-data-encryption-best-practices.md)
* [Procedure consigliate per la sicurezza con il controllo di accesso e la gestione delle identità di Azure](azure-security-identity-management-best-practices.md)
* [Blog del team di sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

