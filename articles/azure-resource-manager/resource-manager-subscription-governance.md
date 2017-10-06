---
title: aaaBest procedure consigliate per le aziende spostamento tooAzure | Documenti Microsoft
description: Viene descritto lo scaffolding utilizzano aziende tooensure un ambiente sicuro e gestibile.
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Scaffold Azure enterprise: governance prescrittiva per le sottoscrizioni
Le aziende siano adottando sempre più cloud pubblico di hello per la flessibilità e la flessibilità. Si utilizzano i ricavi toogenerate punti di forza del cloud hello o ottimizzare le risorse per le aziende hello. Microsoft Azure offre una vasta gamma di servizi di aziende possono assemblare come blocchi predefiniti tooaddress un'ampia gamma di applicazioni e i carichi di lavoro. 

La conoscenza ma, in cui toobegin è spesso difficile. Dopo avere deciso toouse Azure, alcune domande in genere verificano:

* "Come si soddisfano i requisiti legali soddisfare i requisiti legali per la sovranità dei dati in determinati paesi?"
* "Come è possibile garantire che un utente non apporti inavvertitamente modifiche a un sistema critico?"
* "Come è possibile determinare cosa è supportato da ogni risorsa, in modo da poterlo giustificare e fatturare con precisione?"

potenziali Hello di una sottoscrizione vuota con guide alcuna clausola guard sono lunga e complessa. Questo spazio vuoto può compromettere il tooAzure di spostamento.

Questo articolo fornisce un punto di partenza per le esigenze di hello tooaddress tecnici per la governance e il saldo con hello necessario per la flessibilità. Introdotto il concetto di hello dello scaffolding un'organizzazione che consente alle organizzazioni di implementazione e gestire le sottoscrizioni di Azure. 

## <a name="need-for-governance"></a>Esigenza di governance
Quando si spostano tooAzure, è necessario risolvere argomento hello di governance anticipata tooensure hello utilizzo corretto di cloud hello all'interno dell'organizzazione hello. Sfortunatamente, ora hello e della burocrazia creazione di un sistema di controllo completo significa alcuni gruppi aziendali passare direttamente toovendors senza coinvolgere IT aziendale. Questo approccio è possibile lasciare hello enterprise aprire toovulnerabilities se le risorse di hello non sono gestite correttamente. caratteristiche di Hello di un cloud pubblico di hello - agilità, la flessibilità e prezzi in base al consumo, sono importanti toobusiness gruppi che devono tooquickly hello esigenze dei clienti (interni ed esterni). Ma, IT aziendale deve tooensure sistemi e i dati sono protetti in modo efficace.

In uno scenario reale scaffolding è base hello toocreate utilizzato della struttura di hello. lo scaffolding Hello descrive la struttura generale di hello e fornisce punti di ancoraggio per più permanente toobe sistemi montato. Lo scaffolding di un'organizzazione è hello stesso: un set di controlli flessibili e funzionalità di Azure che forniscono struttura toohello ambiente e punti di ancoraggio per i servizi basati su cloud pubblico hello. Fornisce i generatori di hello (IT e i gruppi di business) un toocreate foundation e associare nuovi servizi.

lo scaffolding di Hello è basato su procedure consigliate che è stato raccolto dal molti appuntamenti con i client di diverse dimensioni. Tali client compresi tra lo sviluppo di soluzioni in aziende di hello cloud tooFortune 500 e fornitori di software indipendenti che sono la migrazione e lo sviluppo di soluzioni cloud hello organizzazioni di piccole dimensioni. lo scaffolding enterprise Hello è toosupport flessibile toobe "apposito" tradizionale carichi di lavoro sia i carichi di lavoro agile; ad esempio, gli sviluppatori che creano applicazioni software-as-a-service (SaaS) in base alle funzionalità di Azure.

lo scaffolding enterprise Hello è previsto toobe hello foundation di ogni nuova sottoscrizione in Azure. Consente agli amministratori tooensure i carichi di lavoro soddisfa hello minimi requisiti di governance di un'organizzazione senza impedire rapidamente i propri obiettivi di business e gli sviluppatori.

> [!IMPORTANT]
> Governance è fondamentale toohello esito positivo di Azure. Le destinazioni di questo articolo hello implementazione tecnica dello scaffolding di un'organizzazione ma interessa solo processo più ampio hello e le relazioni tra i componenti di hello. Governance criteri propaga dall'alto hello verso il basso e viene determinata dal quale hello business desidera tooachieve. Naturalmente, la creazione di hello di un modello di governance per Azure include rappresentanti dal reparto IT, ma ancora più importante verificare che disponga di rappresentazione complessa da leader del gruppo di business e sicurezza e gestione dei rischi. Fine hello, lo scaffolding di un'organizzazione consiste nel ridurre business rischio toofacilitate mission e degli obiettivi dell'organizzazione.
> 
> 

Hello seguente immagine vengono descritti i componenti hello di scaffold hello. foundation Hello si basa su un piano a tinta unita per reparti, gli account e sottoscrizioni. pilastri Hello è costituita da criteri di gestione delle risorse e standard di denominazione sicuro. il resto di Hello del scaffold hello proviene da componenti di base di funzionalità di Azure e le funzionalità che consentono un ambiente sicuro e gestibile.

![componenti dello scaffold](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure è cresciuto rapidamente rispetto alla sua introduzione, nel 2008. Questa crescita necessario engineering Microsoft i team toorethink l'approccio adottato per la gestione e distribuzione di servizi. modello di gestione risorse di Azure Hello è stata introdotta in 2014 e sostituisce il modello di distribuzione classica hello. Gestione risorse consente alle organizzazioni toomore facilmente distribuire, organizzare e controllare le risorse di Azure. Resource Manager include la parallelizzazione quando si creano risorse per una distribuzione più veloce di soluzioni complesse e interdipendenti. Include inoltre il controllo di accesso granulare e hello possibilità tootag risorse con i metadati. Microsoft consiglia di creare tutte le risorse tramite il modello di gestione risorse hello. lo scaffolding enterprise Hello è progettato in modo esplicito per il modello di gestione risorse hello.
> 
> 

## <a name="define-your-hierarchy"></a>Definire la gerarchia
foundation Hello di scaffold hello è hello Azure Enterprise registrazione (e hello Enterprise Portal). iscrizione enterprise Hello definisce la forma hello e utilizzare i servizi di Azure all'interno di una società ed è una struttura di governance hello core. Nel contratto enterprise agreement hello, i clienti sono in grado di toofurther suddividere ambiente hello in reparti, gli account e, infine, le sottoscrizioni. Una sottoscrizione di Azure è l'unità di base hello in cui sono contenute tutte le risorse. Definisce anche diversi limiti all'interno di Azure, ad esempio il numero di memorie centrali, risorse e così via.

![gerarchia](./media/resource-manager-subscription-governance/agreement.png)

Ogni organizzazione è diverso e gerarchia hello nell'immagine precedente hello consente notevole flessibilità nell'organizzazione all'interno della società hello Azure. Prima di implementare indicazioni hello contenute nel presente documento, la gerarchia del modello e si hello impatto sulla fatturazione, l'accesso alle risorse e complessità.

sono tre modelli comuni di Hello per le registrazioni di Azure:

* Hello **funzionale** modello
  
    ![functional](./media/resource-manager-subscription-governance/functional.png)
* Hello **unità aziendale** modello 
  
    ![business](./media/resource-manager-subscription-governance/business.png)
* Hello **geografica** modello
  
    ![geografico](./media/resource-manager-subscription-governance/geographic.png)

Si applica lo scaffolding di hello in hello sottoscrizione tooextend livello hello requisiti di governance di enterprise hello nella sottoscrizione hello.

## <a name="naming-standards"></a>Standard di denominazione
Hello elemento scaffold hello è standard di denominazione. Standard di denominazione ben progettato consentono tooidentify risorse nel portale di hello in una fattura e script. È molto probabile che si disponga già di standard di denominazione per l'infrastruttura locale. Quando si aggiunge l'ambiente Azure tooyour, è necessario estendere quelli tooyour standard di denominazione delle risorse di Azure. Standard di denominazione per facilitare la gestione più efficiente dell'ambiente hello in tutti i livelli.

> [!TIP]
> Per le convenzioni di denominazione:
> * Rivedere e adottare ove possibile hello [indicazioni Patterns and Practices](../guidance/guidance-naming-conventions.md). Queste linee guida consentono di stabilire uno standard di denominazione significativo.
> * Usare il sistema camelCasing per i nomi delle risorse (ad esempio myResourceGroup e vnetNetworkName). Nota: Vi sono alcune risorse, quali gli account di archiviazione, in cui hello è solo toouse lettere minuscole (e non altri caratteri speciali).
> * È consigliabile utilizzare tooenforce (descritti nella sezione successiva hello) di criteri di gestione risorse di Azure standard di denominazione.
> 
> Hello suggerimenti precedenti consentono di implementare una convenzione di denominazione coerente.

## <a name="policies-and-auditing"></a>Criteri e controllo
elemento secondo Hello scaffold hello comporta la creazione di [criteri di gestione risorse di Azure](resource-manager-policy.md) e [controllo log attività hello](resource-group-audit.md). I criteri di gestione risorse forniscono rischio toomanage possibilità di hello in Azure. È possibile definire criteri in grado di garantire la sovranità dei dati attraverso la limitazione, l'applicazione o il controllo di determinate azioni. 

* Per impostazione predefinita, i criteri sono un sistema **allow**. Per controllare le azioni di definizione e assegnazione di criteri tooresources che nega o controllare le azioni sulle risorse.
* I criteri sono descritti dalle relative definizioni in un linguaggio di definizione dei criteri (condizioni if-then).
* I criteri vengono creati attraverso file con formattazione JSON (Javascript Object Notation). Dopo aver definito un criterio, assegnarla tooa particolare ambito: sottoscrizione, gruppo di risorse o la risorsa.

I criteri hanno più azioni che consentono l'uso di tooyour un approccio con granularità fine. azioni Hello sono:

* **Negare**: richiesta di blocchi di risorse hello
* **Controllo**: consente di richiesta di hello ma aggiunge un log attività toohello di riga (che può essere utilizzato tooprovide avvisi o i runbook tootrigger)
* **Aggiungere**: aggiunge informazioni toohello risorsa specificata. Ad esempio, se non è presente un tag "CostCenter" in una risorsa, aggiungere il tag con un valore predefinito.

### <a name="common-uses-of-resource-manager-policies"></a>Uso comune dei criteri di Resource Manager
Criteri di gestione risorse di Azure sono uno strumento potente in hello Azure toolkit. Consentono di tooavoid costi imprevisti, tooidentify un centro di costo per le risorse tramite l'assegnazione di tag e tooensure che siano soddisfatti i requisiti di conformità. Quando i criteri vengono combinati con la funzionalità di controllo predefinito di hello, è possibile personalizzare le soluzioni complesse e flessibile. I criteri di consentono alle aziende tooprovide controlli per i carichi di lavoro "IT tradizionale" e "Agile" i carichi di lavoro; ad esempio, lo sviluppo di applicazioni dei clienti. modelli più comuni di Hello che vediamo per i criteri sono:

* **Sovranità/dati di conformità geografica** -Azure fornisce aree tra HelloWorld. Le aziende desiderano spesso toocontrol in cui le risorse vengono create (se sovranità dati tooensure o semplicemente tooensure risorse vengono create utenti finali toohello Chiudi delle risorse di hello).
* **Gestione dei costi**: una sottoscrizione Azure può contenere risorse di diversi tipi e scalabilità. Le aziende desiderano spesso tooensure standard di evitare l'utilizzo di risorse inutilmente grandi, che possono richiedere centinaia di dollari al mese o più di sottoscrizioni.
* **Predefinito governance tramite tag richiesti** -tag la richiesta è una delle funzionalità più comuni e altamente desiderato di hello. Usando i criteri di gestione risorse di Azure le aziende sono in grado di tooensure che una risorsa è contrassegnata in modo appropriato. Hello più tag sono: tipo di reparto, proprietario della risorsa e ambiente (ad esempio - produzione, test e sviluppo)

**esempi**

Sottoscrizione di tipo "IT tradizionale" per le applicazioni line of business

* Applicare tag relativi a reparto e proprietario in tutte le risorse
* Limitare la creazione di risorse toohello area Nord America
* Limitare le possibilità di hello toocreate macchine virtuali serie G e cluster HDInsight

Ambiente di tipo "Agile" per una business unit che crea applicazioni cloud

* requisiti di sovranità toomeet dati, consentire la creazione di hello di risorse solo in un'area specifica.
* Applicare i tag di ambiente in tutte le risorse. Se viene creata una risorsa senza un tag, aggiungere hello **ambiente: sconosciuto** tag risorsa toohello.
* Controllare quando vengono create risorse al di fuori dell'America del Nord ma non impedirle.
* Controllare quando vengono create risorse dal costo elevato.

> [!TIP]
> utilizzo più comune di criteri di gestione delle risorse tra le organizzazioni Hello è toocontrol *in* risorse possono essere create e *cosa* tipi di risorse possono essere creati. Inoltre ai controlli tooproviding *in* e *cosa*, molte organizzazioni utilizzano criteri tooensure risorse hanno hello metadati appropriati toobill nuovamente per l'utilizzo. Si consiglia di applicare i criteri a livello di sottoscrizione hello per:
> 
> * Conformità dei dati/sovranità dei dati
> * Gestione dei costi
> * Tag obbligatori (in base alle esigenze aziendali, ad esempio BillTo, proprietario dell'applicazione)
> 
> È possibile applicare altri criteri a livelli inferiori di ambito.
> 
> 

### <a name="audit---what-happened"></a>Controllo: cos'è successo?
tooview relativa modalità di funzionamento dell'ambiente, è necessario tooaudit attività dell'utente. La maggior parte dei tipi di risorse all'interno di Azure crea log di diagnostica che è possibile analizzare tramite uno strumento di log o in Azure Operations Management Suite. È possibile raccogliere i registri delle attività tra più sottoscrizioni tooprovide, un reparto o la vista dell'organizzazione. I record di controllo sono un importante strumento di diagnostica e gli eventi di tootrigger un meccanismo fondamentale nell'ambiente Azure hello.

Log attività da distribuzioni di gestione risorse consentono di hello toodetermine **operazioni** che ha avuto luogo e gli autori. I log attività possono essere raccolti e aggregati tramite  strumenti quali Log Analytics.

## <a name="resource-tags"></a>Tag delle risorse
Gli utenti dell'organizzazione aggiungono la sottoscrizione alle risorse toohello, diventa sempre più importante tooassociate delle risorse con reparto appropriato hello, customer e ambiente. È possibile collegare metadati tooresources tramite [tag](resource-group-using-tags.md). Utilizzare tag tooprovide informazioni sulle risorse hello o il proprietario di hello. Tag consentono di toonot solo aggregazione e le risorse di gruppo in vari modi, ma utilizzano tali dati per scopi di hello di chargeback. È possibile contrassegnare le risorse con le coppie chiave-valore too15. 

I tag delle risorse sono flessibili e devono essere collegato toomost risorse. Esempi di tag di risorse comuni sono:

* BillTo
* Reparto (o Business unit)
* Ambiente (Produzione, Fase, Sviluppo)
* Livello (Livello Web, Livello di applicazione)
* Proprietario dell'applicazione
* ProjectName

![tags](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Per altri esempi di tag, vedere [Recommended Naming Conventions for Azure Resources](../guidance/guidance-naming-conventions.md) (Convenzioni di denominazione consigliate per le risorse di Azure).

> [!TIP]
> Si consiglia di creare un criterio che ordini l'assegnazione di tag per:
> 
> * Gruppi di risorse
> * Archiviazione
> * Macchine virtuali
> * Ambienti di servizi delle applicazioni/server Web
> 
> Questa strategia tag identifica i metadati sono necessari per business hello, finanza, sicurezza, gestione dei rischi e la gestione dell'ambiente di hello tra le sottoscrizioni. 

## <a name="resource-group"></a>Gruppo di risorse
Gestione risorse consente tooput risorse in gruppi significativi per l'affinità di gestione, fatturazione o naturale. Come accennato in precedenza, Azure offre due modelli di distribuzione. Hello precedente modello classico, unità di gestione di base hello è stato sottoscrizione hello. È difficile toobreak verso il basso le risorse all'interno di una sottoscrizione, che ha portato toohello creazione di un numero elevato di sottoscrizioni. Con il modello di gestione risorse hello, abbiamo visto introduzione hello di gruppi di risorse. I gruppi di risorse sono contenitori di risorse che hanno un ciclo di vita comune o condividono un attributo, ad esempio "tutti i server SQL" o "Applicazione A".

Gruppi di risorse non possono essere contenuti all'interno di altro e le risorse possono appartenere solo tooone gruppo di risorse. Determinate azioni possono essere applicate a tutte le risorse di un gruppo di risorse. Ad esempio, l'eliminazione di un gruppo di risorse rimuove tutte le risorse nel gruppo di risorse hello. In genere, inserire un'intera applicazione o sistema correlate nel hello stesso gruppo di risorse. Ad esempio, un'applicazione a tre livelli denominata applicazione Web di Contoso conterrebbe sul server web hello, server applicazioni e SQL server in hello stesso gruppo di risorse.

> [!TIP]
> Modalità di organizzazione dei gruppi di risorse possono variare rispetto a "tradizionale" carichi di lavoro troppo "Agile" carichi di lavoro:
> 
> * "Tradizionale IT" carichi di lavoro in genere sono raggruppate per gli elementi all'interno di hello stesso ciclo di vita, ad esempio un'applicazione. Il raggruppamento in base all'applicazione consente la gestione di singole applicazioni.
> * "Agile IT" carichi di lavoro tendono toofocus sulle applicazioni cloud orientati ai clienti esterni. gruppi di risorse Hello devono riflettere i livelli di hello di distribuzione (ad esempio livello Web, il livello di App) e la gestione.
> 
> Conoscere il carico di lavoro aiuta a sviluppare una strategia di gruppo di risorse.

## <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo
Probabile che sono chiedersi "che devono avere accesso tooresources?" e come è possibile controllare tale accesso. È fondamentale che consente o impedisce l'accesso toohello portale di Azure e il controllo di accesso tooresources nel portale di hello. 

Quando Azure è stato inizialmente rilasciato, accesso ai controlli tooa sottoscrizione erano di base: amministratore o coamministratore. Accedere a sottoscrizione tooa in hello Classic implicita accesso tooall hello risorse del modello nel portale di hello. La mancanza di un controllo accurato led toohello aumentare del numero di sottoscrizioni tooprovide un livello di controllo di accesso ragionevole per una registrazione di Azure.

La proliferazione di sottoscrizioni non è più necessaria. Controllo di accesso basato sui ruoli, è possibile assegnare gli utenti toostandard ruoli (ad esempio common "lettura" e i tipi di ruoli "writer"). È inoltre possibile definire ruoli personalizzati.

> [!TIP]
> controllo di accesso basato sui ruoli tooimplement:
> * Connetti l'identità aziendale archivio (in genere Active Directory) tooAzure Active Directory tramite hello strumento AD Connect.
> * Controllo hello amministratore/coamministratore di una sottoscrizione tramite un'identità gestita. **Non** assegnare proprietario della sottoscrizione nuovo amministratore/coamministratore tooa. Utilizzare invece RBAC ruoli tooprovide **proprietario** diritti tooa gruppo o un utente.
> * Aggiungere il gruppo di tooa gli utenti di Azure (ad esempio X i proprietari delle applicazioni) in Active Directory. Utilizzare hello gruppo sincronizzato tooprovide gruppo membri hello diritti appropriati toomanage hello gruppo di risorse contenente l'applicazione hello.
> * Seguire il principio di hello di concessione hello **privilegio minimo** toodo obbligatorio hello previsto di lavoro. ad esempio:
>   * Gruppo di distribuzione: Un gruppo che è solo le risorse in grado di toodeploy.
>   * Gestione delle macchine virtuali: Un gruppo di macchine virtuali in grado di toorestart (per le operazioni)
> 
> Questi suggerimenti aiutano a gestire l'accesso utente nella sottoscrizione.

## <a name="azure-resource-locks"></a>Blocchi per le risorse di Azure
L'organizzazione aggiunge sottoscrizione toohello dei servizi principali, diventa sempre più importante tooensure che tali servizi sono disponibili tooavoid interruzioni delle attività aziendali. [Blocchi di risorse](resource-group-lock-resources.md) consentono operazioni toorestrict sulle risorse di alto valore in cui vengano modificati o eliminati hanno un impatto significativo sulle applicazioni o l'infrastruttura cloud. È possibile applicare blocchi tooa sottoscrizione, gruppo di risorse o la risorsa. In genere, vengono applicati blocchi toofoundational risorse quali le reti virtuali, i gateway e gli account di archiviazione. 

I blocchi di risorse attualmente supportano due valori: CanNotDelete e ReadOnly. CanNotDelete significa che gli utenti (con i diritti appropriati hello) possono quindi leggerà o modifica una risorsa ma non è possibile eliminarlo. ReadOnly significa che gli utenti autorizzati non possono eliminare o modificare una risorsa.

i blocchi di gestione toocreate o delete, è necessario avere accesso troppo`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` azioni.
Ruoli predefiniti, hello solo proprietario e amministratore di accesso utente vengono concesse tali azioni.

> [!TIP]
> Le opzioni di rete di base devono essere protette con blocchi. L'eliminazione accidentale di un gateway VPN da sito a sito sarebbe tooan disastroso sottoscrizione di Azure. Azure non consente toodelete una rete virtuale è in uso, ma l'applicazione più restrizioni è una misura utile. 
> 
> * Rete virtuale: CanNotDelete
> * Gruppo di sicurezza di rete: CanNotDelete
> * Criteri: CanNotDelete
> 
> I criteri sono anche manutenzione toohello fondamentale di controlli appropriati. Si consiglia di applicare un **CanNotDelete** bloccare toopolices che sono in uso.

## <a name="core-networking-resources"></a>Risorse di rete di base
Accesso tooresources può essere esterno o interno (all'interno di hello rete aziendale) (tramite hello internet). È facile per gli utenti dell'organizzazione tooinadvertently put risorse in posizione errata hello e potenzialmente aprirli toomalicious accesso. Come con i dispositivi in locale, le aziende devono aggiungere tooensure controlli appropriati che gli utenti di Azure prendere decisioni circostanziate hello. Per la governance delle sottoscrizioni, vengono identificate le risorse principali che garantiscono il controllo di base degli accessi. risorse principali Hello è costituito da:

* **Reti virtuali**, cioè oggetti contenitore per le subnet. Sebbene non sia strettamente necessario, viene spesso utilizzato durante la connessione alle risorse aziendali toointernal applicazioni.
* **Gruppi di sicurezza di rete** sono simili tooa firewall e fornire regole per come una risorsa può "parlare" rete hello. Offre un controllo granulare come o hello stesso una subnet o macchina virtuale, è possibile connettersi toohello Internet o altre subnet nella rete virtuale.

![rete di base](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Per le reti:
> * Creare reti virtuali dedicate tooexternal orientati ai carichi di lavoro e i carichi di lavoro interna. Questo approccio riduce il possibilità di hello inavvertitamente inserire macchine virtuali che sono destinate per carichi di lavoro interni in uno spazio con connessione esterno.
> * Configurare l'accesso toolimit gruppi sicurezza di rete. Come minimo, bloccare toohello accesso internet da reti virtuali interne e blocco accesso toohello rete aziendale da reti virtuali esterne.
> 
> Questi suggerimenti aiutano a implementare risorse di rete sicure.

### <a name="automation"></a>Automazione
La gestione singola delle risorse è sia dispendiosa in termini di tempo che potenzialmente soggetta a errori per certe operazioni. Azure offre varie funzionalità di automazione tra cui Automazione di Azure, App per la logica e Funzioni di Azure. [Automazione di Azure](../automation/automation-intro.md) consente agli amministratori toocreate e definiscono le attività comuni di runbook toohandle nella gestione delle risorse. I runbook vengono creati attraverso un edito di codice PowerShell o un editor grafico. È possibile creare flussi di lavoro complessi in più fasi. Automazione di Azure è spesso toohandle usate attività comuni, ad esempio in corso l'arresto delle risorse inutilizzate o la creazione di risorse in trigger specifico di risposta tooa senza intervento umano.

> [!TIP]
> Per l'automazione:
> * Creare un account di automazione di Azure ed esaminare hello i runbook disponibili (riga di comando sia grafica) disponibili in hello [raccolta Runbook](../automation/automation-runbook-gallery.md).
> * Importare e personalizzare i runbook chiave per l'uso personale.
> 
> Uno scenario comune è hello possibilità tooStart/arresto le macchine virtuali in base a una pianificazione. Sono disponibili i runbook di esempio disponibili in hello raccolta che consentono di gestire questo scenario e illustrano come tooexpand è.
> 
> 

## <a name="azure-security-center"></a>Centro sicurezza di Azure
Ad esempio una di adozione di hello principale blocchi toocloud è stata problemi hello tramite la sicurezza. Responsabili IT e i reparti di sicurezza necessitano tooensure che le risorse in Azure sono sicure. 

Hello [Centro sicurezza di Azure](../security-center/security-center-intro.md) fornisce una visualizzazione dello stato di sicurezza hello delle risorse nelle sottoscrizioni hello centrale e vengono fornite indicazioni che consentono di evitare che le risorse di compromesse. È possibile abilitare i criteri più granulari (ad esempio, l'applicazione criteri toospecific gruppi di risorse che consentono di hello enterprise tootailor loro rischio toohello situazione che sono addressing). Infine, Centro sicurezza di Azure è una piattaforma aperta che consente di partner Microsoft e software di toocreate fornitori di software indipendenti che si collega tooenhance Centro sicurezza di Azure le relative funzionalità. 

> [!TIP]
> Il Centro sicurezza di Azure è abilitato per impostazione predefinita in ogni sottoscrizione. Tuttavia, è necessario abilitare la raccolta di dati da macchine virtuali tooallow Centro sicurezza di Azure tooinstall l'agente e avviare la raccolta di dati.
> 
> ![Raccolta dei dati](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Ora che si è appreso su governance di sottoscrizione, è ora toosee questi consigli in pratica. Vedere [Examples of implementing Azure subscription governance](resource-manager-subscription-examples.md) (Esempi di implementazione della governance delle sottoscrizioni di Azure).

