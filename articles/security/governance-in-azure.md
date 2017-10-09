---
title: aaaGovernance in Azure | Documenti Microsoft
description: "Informazioni sui servizi di calcolo basate su cloud che includono un'ampia selezione di istanze di calcolo e i servizi che possono estendersi su e giù automaticamente toomeet hello esigenze dell'applicazione o dell'organizzazione."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Governance in Azure

Sappiamo che sicurezza processo cloud hello e come sia importante che trovare informazioni accurate e aggiornate sulla sicurezza di Azure. Uno dei toouse delle ragioni migliore Azure di hello per le applicazioni e servizi è tootake sfruttare la sua vasta gamma di funzionalità e strumenti di sicurezza. Questi strumenti e funzionalità rendono toocreate possibili soluzioni di protezione sulla piattaforma Azure sicura hello.

comprendere meglio matrice hello di controlli di Governance implementato in Microsoft Azure da parte del cliente sia hello e viene scritto prospettive di Microsoft operations, in questo articolo, "Governance in Azure", che fornisce un'analisi completa hello toohelp Funzionalità di governance è disponibile con Microsoft Azure.

## <a name="azure-platform"></a>Piattaforma Azure

Azure è una piattaforma del servizio cloud pubblico che supporta un'ampia gamma di sistemi operativi, linguaggi di programmazione, framework, strumenti, database e dispositivi. Può eseguire contenitori Linux con integrazione Dockers; creare app con JavaScript, Python, .NET, PHP, Java e Node.js; creare backend per dispositivi iOS, Android e Windows. Servizi cloud pubblico di Azure supportano hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si compila, o eseguire la migrazione di risorse IT a, un provider di servizi di cloud pubblico ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli di hello e servizi hello assicurano toomanage hello del basato su cloud Asset.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende possono soddisfare i requisiti di sicurezza. Inoltre, Azure offre numerose opzioni di protezione e hello possibilità toocontrol loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni dell'organizzazione.

Questo documento spiega come usare le funzionalità Governance di Azure per soddisfare questi requisiti.

## <a name="abstract"></a>Sunto

Governance di cloud di Microsoft Azure fornisce un controllo integrata e consulenza approccio per la revisione e segnalare le organizzazioni all'utilizzo di hello piattaforma Azure. Governance di cloud di Microsoft Azure fa riferimento processi decisionali toohello, criteri e i criteri coinvolti nella pianificazione hello, architettura, acquisizione, distribuzione, operazione e gestione di un Cloud computing.

toocreate un piano per la governance di cloud di Microsoft Azure, è necessario tootake approfondimenti hello persone, processi e le tecnologie attualmente in uso e quindi compilazione Framework che semplificano tooconsistently IT supportare le esigenze aziendali fornendo fine utenti con hello flessibilità toouse hello potenti funzionalità di Microsoft Azure.

Questo documento spiega come ottenere una governance di alto livello per le proprie risorse IT in Microsoft Azure. In questo documento consentono di comprendere le funzionalità di protezione e governance hello incorporate tooMicrosoft Azure.

di seguito Hello sono discussi di governance hello principale in questo white paper:

- Implementazione di criteri, processi e procedure in linea con gli obiettivi dell'organizzazione.

- Protezione e conformità continua con gli standard dell'organizzazione

- Invio di avvisi e monitoraggio

## <a name="implementation-of-policies-processes-and-procedures"></a>Implementazione di criteri, processi e procedure 

Gestione ha stabilito l'implementazione di toooversee ruoli e responsabilità di criteri di sicurezza informazioni hello e la continuità operativa in Azure. Gestione di Microsoft Azure è responsabile del controllo delle procedure di sicurezza e della continuità nell'ambito dei rispettivi team (compresi quelli di terze parti), ed è tenuta a contribuire alla conformità con i criteri, i processi e gli standard di sicurezza.

Di seguito sono fattori hello si è evoluti:

- Provisioning degli account

- Controlli delle sottoscrizioni

- Controlli degli accessi in base al ruolo

- Gestione delle risorse

- Rilevamento delle risorse

- Controllo delle risorse critiche

- L'accesso all'API tooBilling informazioni

- Controlli delle reti

## <a name="account-provisioning"></a>Provisioning degli account

Definizione account gerarchia è una struttura e il passaggio principale toouse all'interno di una società di servizi di Azure e struttura di governance hello core. In caso di clienti con contratto enterprise hello, i clienti possono suddividere ulteriormente ambiente hello in reparti, gli account e, infine, le sottoscrizioni.

![Provisioning degli account](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Se non si dispone di un contratto enterprise agreement, è consigliabile utilizzare [tag Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) gerarchia toodefine livello di sottoscrizione. Una sottoscrizione di Azure è l'unità di base hello in cui sono contenute tutte le risorse. Definisce anche diversi limiti all'interno di Azure, ad esempio il numero di memorie centrali, risorse e così via. Le sottoscrizioni possono contenere [gruppi di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), che a loro volta contengono risorse. I principi di [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) si applicano solo a questi tre livelli.

Ogni organizzazione è diverso e gerarchia hello con il tag di Azure in caso di non aziendali consente notevole flessibilità nell'organizzazione all'interno della società hello Azure. Prima di distribuire risorse in Microsoft Azure, dovrebbero essere gerarchia del modello e comprendere hello impatto sulla fatturazione, l'accesso alle risorse e complessità.

## <a name="subscription-controls"></a>Controlli delle sottoscrizioni

La sottoscrizione permette di controllare come l'uso delle risorse viene riportato e fatturato. È possibile impostare sottoscrizioni in modo che fatturazione e pagamento siano separati. Come spiegato in precedenza, un account Azure può avere più sottoscrizioni. Le sottoscrizioni possono essere utilizzati toodetermine hello Azure dell'utilizzo di più reparti di una società.

Ad esempio, nel caso in cui l'azienda abbia reparti IT, risorse umane e marketing e questi reparti abbiano più progetti in corso. In base all'utilizzo di hello delle risorse di Azure come macchine virtuali per ogni reparto, può essere fatturati di conseguenza. Da questo possiamo controllare finanze hello di ogni reparto.

Le sottoscrizioni di Azure definiscono tre parametri:

- Un ID sottoscrittore univoco

- Una sede di fatturazione

- Set di risorse disponibili

Per un singolo utente, che include un ID di account Microsoft, dei servizi una carta di credito numero e hello suite completa di Azure - anche se Microsoft impone limiti di utilizzo, in base al tipo di sottoscrizione hello.

Le gerarchie di registrazione di Azure definiscono come sono strutturati i servizi nell'ambito di un contratto Enterprise. Hello Enterprise Portal consente ai clienti toodivide. accedere alle risorse di tooAzure associata a un contratto Enterprise Agreement in base alle esigenze dell'organizzazione di gerarchie flessibili tooan personalizzabile. modello di gerarchia Hello deve corrispondere gestione e la struttura geografico dell'organizzazione in modo che hello associata fatturazione e l'accesso alle risorse può tenere conto in modo accurato per.

modelli di alto livello Hello tre sono unità funzionali, business e reparti geografici, usando un costrutto amministrativo per account raggruppamenti. All'interno di ciascun reparto, è possibile assegnare agli account sottoscrizioni, che creano silos per la fatturazioni e molti limiti chiave in Azure (ad esempio, numero di macchine virtuali, account di archiviazione, ecc.).

![Controlli delle sottoscrizioni](./media/governance-in-azure/security-governance-in-azure-fig2.png)


Per le organizzazioni con un contratto Enterprise, le sottoscrizioni di Azure seguono una gerarchia a quattro livelli:

- Amministratore della registrazione Enterprise

- Amministratore del reparto

- Proprietario dell'account

- Amministratore del servizio

Questa gerarchia determina seguente hello:

- Rapporto di fatturazione

- Amministrazione account

- Ruolo tooartifacts di controllo di accesso basato su (RBAC)

- Confini/Limiti

- Confini

  - Uso e fatturazione (scheda tariffa in base al numero di offerte)

  - Limiti

  - Rete virtuale

- Collegato too1 AAD (1 AAD essere associata a più sottoscrizioni)

- Account di registrazione associato tooan enterprise

## <a name="role-based-access-controls"></a>Controlli degli accessi in base al ruolo

Quando Azure è stato inizialmente rilasciato, accesso ai controlli tooa sottoscrizione erano di base: amministratore o coamministratore. Accedere a sottoscrizione tooa in hello Classic implicita accesso tooall hello risorse del modello nel portale di hello. La mancanza di un controllo accurato led toohello aumentare del numero di sottoscrizioni tooprovide un livello di controllo di accesso ragionevole per una registrazione di Azure.

![Controlli degli accessi in base al ruolo](./media/governance-in-azure/security-governance-in-azure-fig3.png)

La proliferazione di sottoscrizioni non è più necessaria. Controllo di accesso basato sui ruoli, è possibile assegnare gli utenti toostandard ruoli (ad esempio common "lettura" e i tipi di ruoli "writer"). È inoltre possibile definire ruoli personalizzati.

[Controllo degli accessi in base al ruolo di Azure (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) consente una gestione specifica degli accessi per Azure. Usa tale controllo, è possibile concedere solo quantità di hello di accesso che gli utenti devono tooperform i processi. Le aziende sicurezza è consigliabile concentrarsi sul dando dipendenti hello conoscere esattamente le autorizzazioni che necessarie. Numero eccessivo di autorizzazioni espongono tooattackers un account. Un numero di autorizzazioni insufficiente impedisce ai dipendenti di svolgere il proprio lavoro in modo efficiente. Il Controllo degli accessi in base al ruolo di Azure (RBAC) aiuta a risolvere questo problema offrendo la gestione specifica degli accessi per Azure. RBAC consente compiti toosegregate entro il periodo di hello team e concedere solo di accesso toousers necessarie tooperform i processi. Invece di concedere a tutti autorizzazioni senza restrizioni per la sottoscrizione o le risorse di Azure, è possibile consentire solo determinate azioni.

Ad esempio, un dipendente di usare RBAC toolet gestire macchine virtuali in una sottoscrizione, mentre un altro può gestire SQL database all'interno di hello stessa sottoscrizione.

Azure RBAC presenta tre ruoli di base che si applicano a tipi di risorse tooall:

- **Proprietario** dispone di accesso completo tooall risorse hello toodelegate destra accesso tooothers inclusi.

- **Collaboratore** possono creare e gestire tutti i tipi di risorse di Azure, ma non è possibile concedere l'accesso tooothers.

- **Lettore** può visualizzare le risorse di Azure esistenti.

rest Hello dei ruoli RBAC hello in Azure consente la gestione delle risorse di Azure specifiche. Ad esempio, hello ruolo Collaboratore di macchina virtuale consente toocreate utente hello e gestire macchine virtuali. Non viene loro rete virtuale di accesso toohello o subnet hello hello macchina virtuale si connette a.

[Ruoli predefiniti RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) elenchi hello ruoli disponibili in Azure. Specifica le operazioni di hello e che ogni ruolo incorporato e concede toousers ambito.

Concedere l'accesso tramite l'assegnazione di hello appropriato RBAC ruolo toousers, gruppi e applicazioni in un determinato ambito. ambito Hello un'assegnazione di ruolo può essere una sottoscrizione, un gruppo di risorse o una singola risorsa. Un ruolo assegnato a un ambito padre concede l'accesso anche elementi figlio toohello in esso contenuti.

Ad esempio, un utente con gruppo di risorse tooa di accesso è possibile gestire tutte le risorse di hello che contiene, ad esempio siti Web, macchine virtuali e subnet.

RBAC Azure solo hello di supporta le operazioni di gestione risorse di Azure in hello portale di Azure e le API di gestione risorse di Azure. Non tutte le operazioni a livello di dati svolte sulle risorse di Azure possono essere autorizzate tramite RBAC. Ad esempio, è possibile autorizzare un utente toomanage gli account di archiviazione, ma non toohello BLOB o tabelle all'interno di un Account di archiviazione non possono. Analogamente, un database SQL può essere gestito, ma non hello tabelle all'interno di esso.

Per altri dettagli sulla gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).

È anche possibile [creare un ruolo personalizzato](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) nel controllo di accesso gestire (RBAC) se nessuno dei ruoli predefiniti hello soddisfa l'accesso a specifiche esigenze. È possibile creare ruoli personalizzati utilizzando [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure interfaccia della riga di comando (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli), hello e [API REST](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Proprio come i ruoli predefiniti, è possono assegnare ruoli personalizzati toousers, gruppi e le applicazioni di sottoscrizione, gruppo di risorse e gli ambiti di risorsa.

All'interno di ogni sottoscrizione, è possibile concedere le assegnazioni di ruolo too2000.

## <a name="resource-management"></a>Resource management

Solo il modello di distribuzione classica hello originariamente fornito da Azure. In questo modello, ogni risorsa esistente in modo indipendente; si è verificato in alcun modo toogroup risorse correlate. In alternativa, è necessario toomanually verificare quali risorse composta da una soluzione o applicazione e ricordare toomanage multipla in un approccio coordinato.

toodeploy una soluzione, è necessario tooeither creare ogni risorsa singolarmente tramite portale classico hello o creare uno script che tutte le risorse di hello nell'ordine corretto hello distribuito. toodelete una soluzione, è necessario toodelete ogni risorsa singolarmente. Non era semplice applicare e aggiornare i criteri di controllo di accesso per le risorse correlate. Infine, è Impossibile applicare tag tooresources toolabel con condizioni che consentono di monitorare le risorse e gestire la fatturazione.

In 2014, Azure ha introdotto Gestione risorse, aggiunto il concetto di hello di un gruppo di risorse. Un gruppo di risorse è un contenitore di risorse che condividono un ciclo di vita comune. modello di distribuzione di gestione risorse di Hello offre diversi vantaggi:

- È possibile distribuire, gestire e monitorare tutti i servizi di hello per la soluzione in un gruppo, piuttosto che gestisce i servizi singolarmente.

- È possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente.

- È possibile applicare tooall controllo di accesso alle risorse nel gruppo di risorse, e tali criteri vengono applicati automaticamente quando nuove risorse vengono aggiunti toohello gruppo di risorse.

- È possibile applicare tag tooresources toologically organizzare tutte le risorse di hello nella sottoscrizione.

- È possibile utilizzare l'infrastruttura di hello toodefine JavaScript Object Notation (JSON) per la soluzione. file JSON Hello è noto come un modello di gestione risorse.

- È possibile definire le dipendenze di hello tra risorse e pertanto vengono distribuiti in ordine corretto hello.

![Gestione delle risorse](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Gestione risorse consente tooput risorse in gruppi significativi per l'affinità di gestione, fatturazione o naturale. Come accennato in precedenza, Azure offre due modelli di distribuzione. In precedenza hello [modello classico](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), unità di gestione di base hello stato sottoscrizione hello. È difficile toobreak verso il basso le risorse all'interno di una sottoscrizione, che ha portato toohello creazione di un numero elevato di sottoscrizioni. Con il modello di gestione risorse hello, abbiamo visto introduzione hello di gruppi di risorse.

Un gruppo di risorse è un contenitore con risorse correlate per una soluzione Azure. [gruppo di risorse Hello](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) può includere tutte le risorse di hello per soluzione hello o solo le risorse che si desidera toomanage come gruppo. Si decide come risorse tooallocate tooresource gruppi basati su cosa hello più utile per l'organizzazione.

Per altri suggerimenti sui modelli, vedere [Procedure consigliate per la creazione di modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

Gestione risorse di Azure consente di analizzare dipendenze tooensure risorse vengono create nell'ordine corretto hello. Se una risorsa si basa sul valore di un'altra risorsa, ad esempio una macchina virtuale che richiede un account di archiviazione per i dischi, impostare una dipendenza.

>[!Note]
>Per altre informazioni, vedere [Definizione delle dipendenze nei modelli di Gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

È inoltre possibile utilizzare il modello di hello per infrastruttura toohello degli aggiornamenti. Ad esempio, è possibile aggiungere una soluzione di tooyour risorsa e aggiungere le regole di configurazione per le risorse di hello che sono già state distribuite. Se il modello di hello specifica la creazione di una risorsa ma che esiste già una risorsa, Gestione risorse di Azure esegue un aggiornamento anziché creare un nuovo asset. Azure Resource Manager aggiornamenti hello esistente asset toohello stesso stato perché sarebbe come nuovo.

Gestione risorse fornisce le estensioni per gli scenari, quando è necessario operazioni aggiuntive, ad esempio l'installazione di software che non è incluso nel programma di installazione hello.

## <a name="resource-tracking"></a>Rilevamento delle risorse

Gli utenti dell'organizzazione aggiungono la sottoscrizione alle risorse toohello, diventa sempre più importante tooassociate delle risorse con reparto appropriato hello, customer e ambiente. È possibile collegare metadati tooresources tramite tag. Utilizzare [tag](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide informazioni sulle risorse hello o il proprietario di hello. Tag consentono di toonot solo aggregazione e le risorse di gruppo in diversi modi, ma utilizzano tali dati per scopi di hello di chargeback.

Usare i tag quando si dispone di una raccolta di gruppi di risorse e risorse complessa ed è necessario toovisualize tali risorse in modo hello più hello tooyou senso la maggior parte delle. Ad esempio possibile contrassegnare le risorse che svolgono un ruolo simile all'interno dell'organizzazione o appartengono toohello stesso reparto.

Senza tag, gli utenti dell'organizzazione è possibile creare più risorse che possono essere toolater difficile identificano e gestire. Ad esempio, si consiglia toodelete tutte le risorse di hello per un progetto. Se tali risorse non vengono contrassegnate per il progetto di hello, è necessario trovarli manualmente. Assegnazione di tag può essere un aspetto importante è tooreduce costi non necessari nella sottoscrizione.

Le risorse non è necessario tooreside in hello stessa risorsa gruppo tooshare un tag. È possibile creare la propria tooensure tassonomia di tag in tutti gli utenti nell'organizzazione di utilizzano comuni tag anziché utenti inavvertitamente l'applicazione di tag leggermente diverso (ad esempio "dept" anziché "department").

Criteri di risorse consentono di toocreate regole standard per l'organizzazione. È possibile creare criteri che garantiscono le risorse sono contrassegnate con i valori appropriati di hello.

> [!Note]
> Per altre informazioni, vedere [Applicare criteri delle risorse per i tag](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

È inoltre possibile visualizzare le risorse contrassegnate tramite hello portale di Azure.

Hello [report utilizzo](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) per la sottoscrizione include nomi di tag e valori, che consente di toobreak i costi da tag.

> [!Note]
> Per ulteriori informazioni sui tag, vedere [tramite tag tooorganize le risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

Hello limitazioni seguenti si applica tootags:

- Ogni risorsa o gruppo di risorse può avere un massimo di 15 coppie chiave-valore di tag. Questa limitazione si applica solo alla risorsa o gruppo di risorse toohello tootags applicati direttamente. Un gruppo di risorse può contenere più risorse ognuna con 15 coppie chiave-valore di tag.

- nome del tag Hello è limitato too512 caratteri.

- valore del tag Hello è limitato too256 caratteri.

- Gruppo di risorse toohello tag applicati non vengono ereditati dalle risorse hello in tale gruppo di risorse.

Se si dispone di più di 15 valori che è necessario tooassociate con una risorsa, utilizzare una stringa JSON per il valore di tag hello. stringa JSON Hello può contenere molti valori che sono applicati tooa singolo tag chiave.

### <a name="tags-and-billing"></a>Tag e fatturazione

Tag abilitare si toogroup i dati di fatturazione. Ad esempio, se si eseguono più macchine virtuali per le organizzazioni diverse, è possibile utilizzare hello tag toogroup utilizzo dal centro di costo. È anche possibile usare tag toocategorize costi dall'ambiente di runtime; ad esempio, hello fatturazione dell'utilizzo per le macchine virtuali in esecuzione nell'ambiente di produzione.

È possibile recuperare informazioni sui tag tramite hello [utilizzo delle risorse di Azure e RateCard APIs](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) o hello utilizzo con valori delimitati da virgole (CSV) file. Si scarica il file di utilizzo hello da hello [portale degli account Azure](https://account.windowsazure.com/) o [portale EA](https://ea.azure.com/).

>[!Note]
> Per ulteriori informazioni sulla toobilling accesso a livello di codice, vedere [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). Per le operazioni API REST, vedere [Riferimento API REST alla fatturazione di Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Quando si scarica utilizzo hello CSV per i servizi che supportano i tag con fatturazione, vengono visualizzati i tag di hello nella colonna tag hello.

## <a name="critical-resource-controls"></a>Controlli delle risorse critiche

L'organizzazione aggiunge sottoscrizione toohello dei servizi principali, diventa sempre più importante tooensure che tali servizi sono disponibili tooavoid interruzioni delle attività aziendali. [Blocchi di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) consentono operazioni toorestrict sulle risorse di alto valore in cui vengano modificati o eliminati hanno un impatto significativo sulle applicazioni o l'infrastruttura cloud. È possibile applicare blocchi tooa sottoscrizione, gruppo di risorse o la risorsa. In genere, vengono applicati blocchi toofoundational risorse quali le reti virtuali, i gateway e gli account di archiviazione.

I blocchi di risorse attualmente supportano due valori: CanNotDelete e ReadOnly. CanNotDelete significa che gli utenti (con i diritti appropriati hello) possono quindi leggerà o modifica una risorsa ma non è possibile eliminarlo. ReadOnly significa che gli utenti autorizzati non possono eliminare o modificare una risorsa.

Blocchi di gestione risorse di si applicano solo toooperations che si verificano nel piano di gestione di hello, che include le operazioni inviate troppo<https://management.azure.com>. non si limitano i blocchi di hello come risorse di eseguono le proprie funzioni. Vengono limitate le modifiche alle risorse, ma non le operazioni delle risorse. Ad esempio, un blocco di sola lettura su un Database SQL impedisce l'eliminazione o Modifica database hello, ma non impedisce la creazione, aggiornamento o eliminazione di dati nel database di hello.

L'applicazione **ReadOnly** può generare risultati toounexpected perché alcune operazioni che sembrano leggere operazioni sono necessarie ulteriori azioni. Ad esempio, inserire un **ReadOnly** blocco su un account di archiviazione impedisce l'elenco di chiavi hello tutti gli utenti. elenco di Hello operazione delle chiavi viene gestita tramite una richiesta POST hello ha restituito le chiavi sono disponibili per le operazioni di scrittura.

![Controllo delle risorse critiche](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Per un altro esempio, l'inserimento di un blocco di sola lettura in una risorsa di servizio App impedisce Esplora Server Visual Studio di visualizzare i file per la risorsa hello perché tale interazione richiede l'accesso in scrittura.

A differenza di controllo di accesso basato sui ruoli, si utilizza Gestione blocchi tooapply una restrizione in tutti gli utenti e ruoli. toolearn sull'impostazione delle autorizzazioni per utenti e ruoli, vedere [Azure Role-based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Quando si applica un blocco a un ambito padre, tutte le risorse in tale ambito ereditano hello stesso blocco. Anche le risorse in seguito si aggiungono ereditano blocco hello dall'elemento padre di hello. blocco di più restrittivo Hello nell'ereditarietà hello ha la precedenza.

i blocchi di gestione toocreate o delete, è necessario disporre di accesso tooMicrosoft.Authorization/ _o Microsoft.Authorization/locks/_ azioni. Di hello ruoli predefiniti, solo **proprietario** e **amministratore di accesso utente** vengono concesse tali azioni.

## <a name="api-access-toobilling-information"></a>Informazioni di toobilling accesso API

Utilizzare i dati di utilizzo e risorse toopull le API di fatturazione di Azure in strumenti di analisi di dati preferito. Hello dell'utilizzo delle risorse di Azure e RateCard APIs consente di prevedere con precisione e gestire i costi. Hello API vengono implementati come parte della famiglia di hello di API esposte dal hello Gestione risorse di Azure e Provider di risorse.

### <a name="azure-resource-usage-api-preview"></a>API di uso delle risorse di Azure (anteprima)

Hello utilizzare Azure [API di utilizzo delle risorse](https://msdn.microsoft.com/library/azure/mt219003) tooget i dati a consumo Azure stimato. Hello API include:

- **Role-based Access Control di Azure** -configurare l'accesso criteri su hello [portale di Azure](https://portal.azure.com/) o tramite [cmdlet di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) toospecify possono accedere gli utenti o applicazioni dati sull'utilizzo della sottoscrizione toohello. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere hello chiamante tooeither hello fatturazione lettura, lettura, proprietario o collaboratore ruolo tooget accesso toohello dati di utilizzo per una sottoscrizione di Azure specifico.

- **Aggregazioni orarie o giornaliere** : i chiamanti possono specificare se desiderano i dati di utilizzo di Azure in intervalli orari o giornalieri. valore predefinito di Hello è giornaliero.

- **I metadati dell'istanza (inclusi i tag delle risorse)** -ottenere i dettagli a livello di istanza come uri di risorsa completo hello (/Subscriptions/<ID {id sottoscrizione} /...), hello informazioni sul gruppo di risorse e i tag delle risorse. Questi metadati consentono in modo deterministico e allocare tag hello, per casi di utilizzo come Ricarica tra utilizzo a livello di codice.

- **I metadati di Resource** -Dettagli risorsa, ad esempio nome misuratore hello, misuratore categoria, sottocategoria misuratore, unità e area assegnare chiamante hello una migliore comprensione di ciò che è stato elaborato. Diverse anche collaborazioni terminologia dei metadati di risorsa tooalign hello portale di Azure, Azure-utilizzo CSV, EA CSV, di fatturazione e altre esperienze pubblico, toolet correlare dati esperienze.

- **Utilizzo per tutti i tipi di offerte** : i dati di utilizzo sono accessibili per tutti i tipi di offerta, tra cui il pagamento in base al consumo, MSDN, l’impegno monetario, il credito monetari ed EA.

**API RateCard delle risorse di Azure (anteprima)**

Utilizzare hello API RateCard risorse di Azure tooget hello elenco disponibile delle risorse di Azure e stimato informazioni sui prezzi per ognuno. Hello API include:

- **Controllo di accesso basato sui ruoli Azure** : configurazione dei criteri di accesso nel portale di Azure hello o tramite Azure PowerShell cmdlet toospecify che gli utenti o applicazioni possono ottenere accesso toohello RateCard dati. Per l’autenticazione, i chiamanti devono utilizzare i token standard di Azure Active Directory. Aggiungere hello chiamante tooeither hello lettore, il proprietario o collaboratore ruolo tooget accesso toohello dati di utilizzo per una sottoscrizione di Azure specifico.

- **Supporto delle offerte con pagamento in base al consumo, MSDN, impegno monetario e credito monetario (EA non supportato)** : questa API fornisce informazioni sulle tariffe a livello di offerta di Azure. il chiamante Hello di questa API deve passare tariffe e i dettagli delle risorse hello offerta informazioni tooget. Siamo tariffe EA tooprovide attualmente non è possibile perché EA offre sono personalizzate le tariffe per la registrazione. Ecco alcuni degli scenari di hello che sono possibili con combinazione hello di hello utilizzo e hello RateCard APIs:

- **Spesa di Azure durante il mese di hello** -combinazione hello uso di hello informazioni sull'utilizzo e RateCard APIs tooget una visione migliore in cloud di spesa mese hello. È possibile analizzare hello oraria e giornaliera bucket di utilizzo e il relativo costo stimato.

- **Consente di impostare avvisi** : utilizzare hello utilizzo e hello RateCard APIs tooget stimato il consumo di cloud e le spese e consente di impostare avvisi basato su risorse o valuta.

- **Stimare i costi** – Get del consumo stimato e del cloud spesa e applicare di machine learning toopredict algoritmi quali costi hello sarebbe alla fine hello hello del ciclo di fatturazione.

- **Pre-utilizzo di analisi dei costi** : utilizzare hello API RateCard toopredict quanto fattura sarebbe per l'utilizzo previsto quando si sposta tooAzure i carichi di lavoro. Nel caso di carichi di lavoro esistenti in altri cloud o un cloud privato, è anche possibile mappare l'utilizzo con hello Azure tariffe tooget dedicare una stima più accurata di Azure. In questo modo stima hello toopivot possibilità offerte speciali e di confronto tra tipi di offerta diversa hello oltre a pagamento a consumo, come un impegno monetario e credito monetario. Hello API fornisce inoltre hello possibilità toosee costo differenze per regione e consente toodo un toohelp analisi di simulazione costo di prendere decisioni di distribuzione.

- **L'analisi di simulazione** -è possibile determinare se è più conveniente toorun carichi di lavoro in un'altra area o in un'altra configurazione di hello risorse di Azure. Risorse di Azure i costi possono differire in base hello regione di Azure in uso.

- È inoltre possibile determinare se un altro tipo di offerta di Azure offre una tariffa migliore per una risorsa di Azure.

## <a name="networking-controls"></a>Controlli della rete

Accesso tooresources può essere esterno o interno (all'interno di hello rete aziendale) (tramite hello internet). È facile per gli utenti dell'organizzazione tooinadvertently put risorse in posizione errata hello e potenzialmente aprirli toomalicious accesso. Come in locale i dispositivi, le aziende devono aggiungere tooensure controlli appropriati che gli utenti di Azure prendere decisioni circostanziate hello.

![Controlli delle reti](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Per la governance delle sottoscrizioni, vengono identificate le risorse principali che garantiscono il controllo di base degli accessi. risorse principali Hello è costituito da:

### <a name="network-connectivity"></a>Connettività di rete

[Reti virtuali](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) sono oggetti contenitori per le subnet. Sebbene non sia strettamente necessario, viene spesso utilizzato durante la connessione alle risorse aziendali toointernal applicazioni. Hello consente di servizio di rete virtuale di Azure è toosecurely tooeach altre risorse di Azure di connettersi con le reti virtuali (Vnet).

Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato. È inoltre possibile connettere una rete locale tooyour di reti virtuali.

Di seguito sono descritte le funzionalità delle reti virtuali di Azure:

- **Isolamento**: le reti virtuali sono isolate le une dalle altre. È possibile creare reti virtuali separate per lo sviluppo, test e produzione che hello utilizzare blocchi di indirizzi CIDR stesso. È altrimenti possibile creare più reti virtuali che usano blocchi di indirizzi CIDR diversi e connettere tra loro le reti. Una rete virtuale può essere segmentata in più subnet. Azure fornisce la risoluzione dei nomi interna per le macchine virtuali e istanze del ruolo di servizi Cloud connesso tooa rete virtuale. È possibile configurare facoltativamente toouse una rete virtuale dei propri server DNS, anziché utilizzare la risoluzione dei nomi interno di Azure.

- **Connettività Internet**: accederanno a tutte le macchine virtuali (VM) di Azure e servizi Cloud le istanze del ruolo sono connesso tooa rete virtuale toohello Internet, per impostazione predefinita. È inoltre possibile abilitare le risorse toospecific di accesso in ingresso, in base alle esigenze.

- **Connettività a risorse di Azure**: le risorse di Azure, ad esempio servizi Cloud e macchine virtuali possono essere connesso toohello stessa rete virtuale. le risorse di Hello possono connettersi tooeach altri indirizzi IP privati, anche se sono presenti in subnet diverse. Azure offre predefinito routing tra subnet, le reti virtuali e reti locali, in modo da non avere tooconfigure e gestire le route.

- **Connettività tra reti virtuali**: le reti virtuali possono essere connesso tooeach altri, l'abilitazione di risorse connessa tooany toocommunicate di rete virtuale con qualsiasi risorsa di qualsiasi altra rete virtuale.

- **Connettività locale**: le reti virtuali possono essere reti locali tooon connessi tramite connessioni di rete privata tra la rete e Azure o tramite una connessione VPN site-to-site over hello Internet.

- **Filtraggio del traffico**: il traffico di rete delle istanze dei ruoli VM e Servizi cloud può essere filtrato in ingresso e in uscita in base all'indirizzo IP e la porta di origine, l'indirizzo IP e la porta di destinazione, e il protocollo.

- **Routing**: è possibile anche ignorare il routing predefinito di Azure configurando route personalizzate oppure usando le route BGP attraverso un gateway di rete.

## <a name="network-access-controls"></a>Controlli di accesso alla rete

[Gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) sono ad esempio un firewall e specificare le regole per come una risorsa può "parlare" rete hello. Offre un controllo granulare come o hello stesso una subnet o macchina virtuale, è possibile connettersi toohello Internet o altre subnet nella rete virtuale.

Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooresources il traffico di rete connessa tooAzure reti virtuali (VNet). NSGs può essere associato toosubnets, singole macchine virtuali (classico), o interfacce di rete (NIC) collegati tooVMs Gestione risorse ().

Quando un gruppo è subnet tooa associato, hello regole tooall risorse toohello connesso subnet. Il traffico può essere limitato ulteriormente associando anche un gruppo tooa macchina virtuale o scheda di rete.

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Sicurezza e conformità continua con gli standard aziendali

Ogni azienda ha esigenze diverse e ciascuna di loro può ottenere vantaggi diversi dalle soluzioni cloud. Tuttavia, di tutti i tipi sono dotate di hello stessi problemi di base sullo spostamento toohello cloud. Desiderano tooretain il controllo dei dati e tale toobe dati mantenuti protetta e privata, pur mantenendo la conformità e trasparenza desiderato.

Ciò che i clienti chiedono ai provider di servizi cloud è:

- **Proteggere i dati** mentre riconoscimento di tali cloud hello può fornire maggiore sicurezza dei dati e controllo amministrativo, dei responsabili IT sono ancora in questione che la migrazione cloud toohello rimarranno toohackers più vulnerabile rispetto correnti soluzioni interne.

- **Mantenere riservati i dati**: i servizi cloud pongono straordinarie sfide in termini di privacy alle aziende. Come società cercare toohello cloud toosave sui costi di infrastruttura e migliorare la flessibilità, sono anche preoccuparsi perdere il controllo in cui sono archiviati i dati, che accede a tale colonna e come Ottiene usato.

- **Fornire qui controllo** anche come sfruttano hello cloud toodeploy altre soluzioni innovative, le aziende sono molto importante perdere il controllo dei dati. diffusione di informazioni recenti Hello delle agenzie governative degli accesso ai dati dei clienti, tramite mezzi sia validi e molto legali, apportare alcune CIO tenere conto di archiviare i dati nel cloud hello.

- **Promuovere la trasparenza** mentre sicurezza, privacy e controllo sono responsabili delle decisioni importanti toobusiness, desidera inoltre il possibilità hello tooindependently verificare come i dati vengano archiviati, a cui si accede e protette.

- **Mantenere la conformità** anche l'uso di tecnologie cloud della società, hello complessità e dell'ambito di standard e normative continuare tooevolve. Le aziende devono tooknow che siano soddisfatti i relativi standard di conformità e conformità evolveranno come normative cambiano nel tempo.

## <a name="security-configuration-monitoring-and-alerting"></a>Configurazione della sicurezza, monitoraggio e invio di avvisi

I sottoscrittori di Azure possono gestire i propri ambienti cloud da più dispositivi, tra cui workstation di gestione, PC per sviluppatori e dispositivi di utenti finali con privilegi elevati con autorizzazioni specifiche per le attività. In alcuni casi, le funzioni amministrative vengono eseguite tramite le console basata sul web, ad esempio hello portale di Azure. In altri casi, potrebbe essere tooAzure connessioni dirette da sistemi locali su reti Private virtuali (VPN), servizi Terminal, protocolli di applicazioni client o (a livello di codice) hello Azure Service Management API (SMAPI). Gli endpoint client possono essere inoltre aggiunti a un dominio o isolati e non gestiti, ad esempio tablet o smartphone.

Anche se più funzioni di accesso e la gestione forniscono un'ampia gamma di opzioni, questo variabilità può aggiungere distribuzione cloud tooa di rischio. Può essere difficile toomanage, tenere traccia e controllare le azioni amministrative. Questo variabilità anche può comportare rischi di protezione tramite gli endpoint di accesso non regolamentate tooclient che vengono utilizzati per la gestione dei servizi cloud. L'uso di workstation generiche o personali per lo sviluppo e la gestione dell'infrastruttura genera vettori di minaccia imprevedibili, come l'esplorazione del Web (ad esempio attacchi di tipo watering hole) o la posta elettronica (ad esempio "ingegneria sociale" e phishing).

Il monitoraggio, registrazione e controllo fornire una base per il rilevamento e la comprensione delle attività amministrative, ma potrebbe non essere sempre possibile tooaudit tutte le azioni di completamento dettaglio scadenza toohello quantità di dati generati. Controllo efficacia hello dei criteri di gestione di hello è tuttavia consigliabile.

Governance sicurezza di Azure da oggetti Criteri di gruppo di dominio Active Directory AD toocontrol Windows degli amministratori di hello tutte le interfacce, ad esempio la condivisione file. Includere le workstation di gestione nei processi di controllo, monitoraggio e registrazione. Tenere traccia di tutti gli accessi e gli utilizzi di amministratori e sviluppatori.

### <a name="azure-security-center"></a>Centro sicurezza di Azure

Hello [Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) fornisce una visualizzazione dello stato di sicurezza hello delle risorse nelle sottoscrizioni hello centrale e vengono fornite indicazioni che consentono di evitare che le risorse di compromesse. È possibile abilitare i criteri più granulari (ad esempio, l'applicazione criteri toospecific gruppi di risorse che consentono di hello enterprise tootailor loro rischio toohello situazione che sono addressing).

![Centro sicurezza di Azure](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Il Centro sicurezza offre un monitoraggio di sicurezza integrato e gestione dei criteri per le sottoscrizioni di Azure, aiuta a rilevare le minacce che potrebbero altrimenti passare inosservate ed è compatibile con un ampio ecosistema di soluzioni di sicurezza. Dopo aver abilitato [criteri di sicurezza](https://docs.microsoft.com/azure/security-center/security-center-policies) per le risorse di una sottoscrizione, il Centro sicurezza PC analizza le risorse tooidentify potenziali vulnerabilità della sicurezza hello. Le informazioni sulla configurazione di rete sono disponibili immediatamente.

Centro sicurezza di Azure rappresenta una combinazione tra l'analisi delle procedure consigliate e la gestione dei criteri di sicurezza per tutte le risorse incluse nella sottoscrizione di Azure. Questo strumento potente e facile toouse consente ai team di sicurezza e rischi ufficiali tooprevent, rilevare e rispondere toosecurity minacce come automaticamente raccoglie e analizza i dati di sicurezza di risorse di Azure, rete hello e soluzioni partner come firewall e antimalware.

Inoltre, Centro sicurezza di Azure si applica analitica avanzate, tra cui machine learning e analisi del comportamento, sfruttando al contempo informazioni sulle minacce globale da Microsoft hello di prodotti e servizi, hello Microsoft Digital Crimes Unit (DCU), Microsoft Security Response Center (MSRC) e un feed esterno. [Governance sicurezza](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) possono essere applicate genericamente a livello di sottoscrizione hello o circoscritti toospecific, tooindividual requisiti granulare applicati alle risorse tramite una definizione di criteri.

Infine, Centro sicurezza di Azure analizza l'integrità di protezione delle risorse in base a tali criteri e Usa questo dashboard dettagliati tooprovide e gli avvisi per eventi, ad esempio il rilevamento di malware o connessione IP dannosi tentativi.

>[!Note]
> Per ulteriori informazioni su come indicazioni tooapply, leggere [implementazione delle indicazioni di sicurezza nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Centro sicurezza PC raccoglie i dati da tooassess le macchine virtuali lo stato di protezione, fornire consigli sulla sicurezza e ricevere un avviso toothreats. La prima volta che si accede al Centro sicurezza, la raccolta dati viene abilitata in tutte le macchine virtuali della sottoscrizione. È consigliabile la raccolta dei dati, ma è possibile rifiutare esplicitamente da [la disabilitazione della raccolta dati](https://docs.microsoft.com/azure/security-center/security-center-faq) in hello criterio Centro sicurezza PC.

Infine, Centro sicurezza di Azure è una piattaforma aperta che consente di partner Microsoft e software di toocreate fornitori di software indipendenti che si collega tooenhance Centro sicurezza di Azure le relative funzionalità.

Centro sicurezza di Azure monitora hello seguendo le risorse di Azure:

- Macchine virtuali (VM) (compresi servizi cloud)

- Reti virtuali di Azure

- Servizio di SQL Azure

- Soluzioni dei partner integrate nella sottoscrizione di Azure come un web application firewall nelle macchine virtuali e nell'[ambiente del servizio app](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

sviluppo del software OMS Hello e protezione delle informazioni del team del servizio e [programma governance](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) supporta i requisiti di business ed è conforme toolaws e alle normative, come descritto in [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) e [Microsoft Trust Center conformità](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Vengono anche fornite informazioni su come OMS stabilisce i requisiti di sicurezza, identifica i controlli di sicurezza, e gestisce e monitora i rischi. Ogni anno viene effettuata una revisione di criteri, standard, procedure e linee guida.

Ciascun membro del team di sviluppo di OMS riceve una formazione formale sulla sicurezza delle applicazioni. Internamente, viene usato un sistema di controllo della versione per lo sviluppo di software, che Ogni progetto software è protetta dal sistema di controllo della versione di hello.

Microsoft si avvale di un team per la sicurezza e conformità che supervisiona e valuta tutti i servizi in Microsoft. Ai responsabili della sicurezza delle informazioni costituiscono team hello e non sono associati con hello engineering reparti che lo sviluppo di OMS. ai responsabili della sicurezza Hello hanno i propri catena di gestione ed eseguire valutazioni indipendenti di prodotti e di sicurezza tooensure services e di conformità.

Operations Management Suite (noto anche come OMS) è una raccolta di servizi di gestione che sono stati progettati in cloud hello dall'inizio hello. Anziché distribuire e gestire le risorse localmente, i componenti OMS sono ospitati integralmente in Azure. La configurazione è minima ed è possibile essere operativi in davvero pochi minuti.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Il fatto che i servizi OMS vengono eseguiti nel cloud hello non significa che non è possibile gestire efficacemente l'ambiente locale.

Inserire un agente su tutte le finestre o computer Linux nel proprio data center e invierà tooLog dati Analitica in cui possono essere analizzato insieme a tutti gli altri dati raccolti dal cloud o in servizi locali. Utilizzare Backup di Azure e Azure Site Recovery cloud hello tooleverage per backup e disponibilità elevata di risorse locali.

I runbook nel cloud hello in genere non è possibile accedere alle risorse di on-premise, ma è possibile installare un agente in uno o più computer troppo che ospiterà i runbook nel data center. Quando si avvia un runbook, è sufficiente specificare se si desidera che toorun nel cloud hello o in un thread di lavoro locale.

funzionalità di base Hello di OMS viene fornita da un set di servizi in esecuzione in Azure. Ogni servizio fornisce una funzione di gestione specifico, ed è possibile combinare gli scenari di gestione diverso di servizi tooachieve.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Operation Manager di Azure estende le sue funzionalità offrendo soluzioni di gestione. Le [soluzioni di gestione](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) sono set pre-confezionati di logica che implementano uno scenario di gestione usando uno o più servizi OMS.

![Operation Manager di Azure](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Diverse soluzioni sono disponibili da Microsoft e dai partner che è possibile aggiungere facilmente tooyour valore hello tooincrease di sottoscrizione di Azure dell'investimento in OMS.

Come partner, è possibile creare la propria toosupport soluzioni le applicazioni e servizi e fornire loro toousers tramite hello Azure Marketplace o modelli di avvio rapido.

## <a name="performance-alerting-and-monitoring"></a>Invio di avvisi e monitoraggio delle prestazioni

### <a name="alerting"></a>Creazione di avvisi

Gli avvisi sono un metodo per monitorare le metriche, gli eventi e i log delle risorse di Azure e ricevere una notifica quando una condizione specificata viene soddisfatta.

**Avvisi nei diversi servizi di Azure**

Gli avvisi sono disponibili in diversi servizi, tra cui:

- Application Insights: abilita i test Web e gli avvisi sulle metriche.

>[!Note]
> Vedere [Impostare gli avvisi in Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) e [Monitorare la disponibilità e la velocità di risposta dei siti Web](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Log Analitica (Operations Management Suite): Abilita il routing hello di attività e i log di diagnostica tooLog Analitica. Operations Management Suite consente gli avvisi relativi alla metrica, ai log e altri tipi di avviso.

>[!Note]
> Per altre informazioni, vedere Avvisi in [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Monitoraggio di Azure: permette di generare avvisi sia in base a valori metrici che in base agli eventi del registro attività. È possibile utilizzare hello [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/dn931943.aspx) toomanage avvisi.

>[!Note]
> Per ulteriori informazioni, vedere [utilizzando hello portale di Azure, PowerShell o gli avvisi di hello interfaccia della riga di comando toocreate](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>Monitoraggio

I problemi di prestazioni nell'app cloud possono avere un impatto sull'azienda. Con più componenti interconnessi e versioni frequenti, possono verificarsi in qualsiasi momento riduzioni delle prestazioni. Se si sta sviluppando un'app, gli utenti scopriranno problemi che non vengono generalmente rilevati durante i test. Si deve sapere immediatamente su questi problemi e di strumenti per la diagnosi e risoluzione dei problemi di hello. Microsoft Azure offre diversi strumenti per identificare i problemi.

**Come monitorare le app cloud di Azure**

Per il monitoraggio delle applicazioni e dei servizi di Azure sono disponibili diversi strumenti, le cui funzionalità in parte si sovrappongono. Si tratta in parte per motivi cronologici e in parte dovuto toohello sfocatura tra lo sviluppo e l'operazione di un'applicazione.

Di seguito sono strumenti principali hello:

- **Monitoraggio di Azure** è lo strumento di base per il monitoraggio dei servizi eseguiti in Azure. Fornisce dati a livello di infrastruttura sulla velocità effettiva di hello di un servizio e hello circostanti ambiente. Se si gestiscono le App in Azure, decidere se tooscale verso l'alto o verso il basso le risorse, quindi il monitoraggio di Azure offre è utilizzare toostart.

- **Application Insights** può essere usato per lo sviluppo e come soluzione di monitoraggio di produzione. Installa un pacchetto nell'app, consentendo di vedere ciò che accade dall'interno. I dati includono i tempi di risposta delle dipendenze, le tracce delle eccezioni, gli snapshot per il debug e i profili di esecuzione. Fornisce potenti strumenti avanzati per l'analisi di tutti questi dati di telemetria entrambi toohelp si esegue il debug di un'app e toohelp comprendere cosa gli utenti con esso. È possibile indicare se un picco in tempi di risposta è in scadenza toosomething in un'app o un problema resourcing esterno. Se si utilizza Visual Studio e app hello causa l'errore, è possibile eseguire toohello destra problema righe di codice in modo è possibile correggere l'errore.

- **Log Analitica** per gli utenti che necessitano di tootune prestazioni e piano di manutenzione, alle applicazioni in esecuzione nell'ambiente di produzione. È basato su Azure Raccoglie e aggrega i dati da molte origini, anche se con un ritardo di 10 minuti too15. Offre una soluzione di gestione IT olistica per l'infrastruttura Azure, locale e basata sul cloud di terze parti (ad esempio, Amazon Web Services). Fornisce strumenti più completi i dati di tooanalyze in altre origini, consente di query complesse in tutti i log e può inviare un avviso in modo proattivo condizioni specifiche. È anche possibile raccogliere dati personalizzati nel repository centrale per l'esecuzione di query e la visualizzazione.

- **System Center Operations Manager (SCOM)** è destinato alla gestione e al monitoraggio di installazioni cloud di grandi dimensioni. Può essere già noto come strumento di gestione per cloud locali basati su Windows Sever e Hyper-V, ma può anche essere integrato con app Azure e gestirle. Tra l'altro, può installare Application Insights in app attive esistenti. L'eventuale inattività di un'app viene segnalata in pochi secondi.


## <a name="next-steps"></a>Passaggi successivi

- [Procedure consigliate per la creazione di modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Esempi di implementazione della governance delle sottoscrizioni di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/).
