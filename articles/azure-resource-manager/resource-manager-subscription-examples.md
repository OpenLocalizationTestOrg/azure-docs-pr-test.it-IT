---
title: aaaScenarios ed esempi per la governance sottoscrizione | Documenti Microsoft
description: Vengono forniti esempi di come tooimplement governance di sottoscrizione di Azure per scenari comuni.
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Esempi di implementazione di scaffold enterprise di Azure
In questo argomento vengono forniti esempi di come un'organizzazione può implementare indicazioni hello per un [lo scaffolding di Azure enterprise](resource-manager-subscription-governance.md). Usa una società fittizia denominata Contoso tooillustrate procedure consigliate per gli scenari comuni.

## <a name="background"></a>Background
Contoso è una società in tutto il mondo che fornisce soluzioni di catena di fornitura per i clienti in tutti i dati da un modello nel pacchetto di modello tooa "Software come servizio" distribuito in locale.  Lo sviluppo software tutto il mondo hello con centri di sviluppo significativo India hello Uniti e Canada.

parte di ISV Hello della società hello è suddivisa in diverse unità aziendali indipendenti che gestiscono i prodotti in un'azienda significativa. Ogni business unit ha i suoi sviluppatori, responsabili di prodotto e architetti.

Hello servizi tecnologia Enterprise (ETS) business unit fornisce le funzionalità IT centralizzata e gestisce centri dati in cui le unità aziendali ospitano le proprie applicazioni. Con la gestione di centri dati hello, hello organizzazione ETS fornisce e gestisce i servizi di rete/telefonia e collaborazione centralizzata (ad esempio posta elettronica e i siti Web). Gestisce inoltre i carichi di lavoro rivolti ai clienti per business unit più piccole che non dispongono di personale operativo.

Hello seguenti utenti tipo viene utilizzato in questo argomento:

* Dave è amministratore di Azure ETS hello.
* Alice è direttore di sviluppo Contoso business unit di hello supply chain.

Contoso deve app toobuild un line-of-business e un'app che riguardano il cliente. Si è deciso toorun hello App in Azure. Dave legge hello [governance sottoscrizione rigorosa](resource-manager-subscription-governance.md) argomento ed è ora pronto tooimplement indicazioni hello.

## <a name="scenario-1-line-of-business-application"></a>Scenario 1: applicazione line-of-business
Contoso è la creazione di un toobe di sistema (BitBucket) Gestione codice di origine utilizzato dagli sviluppatori tra HelloWorld.  un'applicazione Hello Usa infrastruttura come servizio (IaaS) per l'hosting e costituito da server web e un server di database. Gli sviluppatori di accedere ai server nei propri ambienti di sviluppo, ma non necessario accedono toohello server in Azure. ETS Contoso desidera tooallow proprietario dell'applicazione hello e un'applicazione hello toomanage team. un'applicazione Hello disponibile solo durante la rete aziendale di Contoso. Dave tooset sottoscrizione hello è necessario per questa applicazione. sottoscrizione Hello ospiterà anche altri software relative agli sviluppatori in futuro hello.  

### <a name="naming-standards--resource-groups"></a>Standard di denominazione e gruppi di risorse
Davide crea una sottoscrizione toosupport gli strumenti di sviluppo che sono comuni a tutte le unità aziendali hello. (Per un'applicazione hello e reti hello) deve toocreate nomi significativi per la sottoscrizione di hello e gruppi di risorse. Crea hello seguenti gruppi di risorse e di sottoscrizione:

| Elemento | Nome | Descrizione |
| --- | --- | --- |
| Subscription |Produzione di strumenti per gli sviluppatori Contoso ETS |Supporta gli strumenti di sviluppo più diffusi |
| Gruppo di risorse |rgBitBucket |Contiene i server web dell'applicazione di hello e server di database |
| Gruppo di risorse |rgCoreNetworks |Contiene le reti virtuali hello e connessione gateway da sito a sito |

### <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo
Dopo aver creato la sottoscrizione, Davide desidera tooensure che hello team appropriato e i proprietari delle applicazioni possono accedere alle risorse. Dave riconosce che ogni team ha requisiti diversi. Giorgio Usa gruppi hello che sono stati sincronizzati dal tooAzure di Active Directory (AD) locale Contoso Active Directory e fornisce un livello ottimale di hello dei team toohello di accesso.

Dave assegna hello seguenti ruoli per la sottoscrizione di hello:

| Ruolo | Troppo assegnato| Descrizione |
| --- | --- | --- |
| [Proprietario](../active-directory/role-based-access-built-in-roles.md#owner) |ID gestito da Active Directory di Contoso |Questo ID è controllato con accesso Just in Time (JIT) tramite lo strumento di gestione delle identità di Contoso e assicura il totale controllo degli accessi dei proprietari delle sottoscrizioni. |
| [Gestore della sicurezza SQL](../active-directory/role-based-access-built-in-roles.md#security-manager) |Reparto di gestione dei rischi e della sicurezza |Questo ruolo consente agli utenti toolook in hello Centro sicurezza di Azure e lo stato di hello delle risorse di hello. |
| [Collaboratore di rete](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Team di rete |Questo ruolo consente hello sito tooSite VPN di Contoso rete team toomanage e hello reti virtuali. |
| *Ruolo personalizzato* |Proprietario dell'applicazione |Davide crea un ruolo che concede hello possibilità toomodify risorse nel gruppo di risorse hello. Per altre informazioni, vedere [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Criteri
Dave è hello seguenti requisiti per la gestione delle risorse nella sottoscrizione hello:

* Poiché gli strumenti di sviluppo hello supportano gli sviluppatori tra HelloWorld, Davide non desidera che gli utenti tooblock la creazione di risorse in qualsiasi area. Tuttavia, deve tooknow in cui le risorse vengono create.
* È preoccupato per i costi. Di conseguenza, desidera che i proprietari delle applicazioni tooprevent dalla creazione di macchine virtuali inutilmente costose.  
* Poiché questa applicazione gestisce gli sviluppatori in numero di unità di business, desidera tootag ogni risorsa con proprietario di unità e applicazione di business hello. Tramite questi tag, ETS di fatturare team appropriato hello.

Crea seguente hello [criteri di gestione risorse](resource-manager-policy.md):

| Campo | Effetto | Descrizione |
| --- | --- | --- |
| location |audit |Creazione di hello delle risorse di hello in qualsiasi area di controllo |
| type |deny |Nega la creazione di macchine virtuali serie G |
| tags |deny |Richiede il tag del proprietario dell'applicazione |
| tags |deny |Richiede il tag del centro di costo |
| tags |append |Aggiungere il nome di tag **Business Unit** e valore del tag **ETS** tooall risorse |

### <a name="resource-tags"></a>Tag delle risorse
Dave riconosce che deve toohave informazioni specifiche nel centro di costo di hello bill tooidentify hello per l'implementazione di hello BitBucket. Inoltre, Dave vuole tooknow che tutti hello risorse ETS proprietario.

Aggiunge il seguente hello [tag](resource-group-using-tags.md) toohello risorse e gruppi di risorse.

| Nome del tag | Valore del tag |
| --- | --- |
| ApplicationOwner |nome Hello di persona hello che gestisce l'applicazione. |
| CostCenter |centro di costo Hello del gruppo di hello che paga per hello consumo di Azure. |
| BusinessUnit |**ETS** (hello business unit associata sottoscrizione hello) |

### <a name="core-network"></a>Rete core
Hello ETS Contoso informazioni revisioni del team di gestione di protezione e al rischio di Dave proposto pianificare toomove hello applicazione tooAzure. Desiderano tooensure che non è un'applicazione hello esposti toohello internet.  Dave dispone anche di App per sviluppatori in futuro hello sarà spostato tooAzure. Queste app richiedono interfacce pubbliche.  toomeet questi requisiti, Davide sono disponibili due reti virtuali interne ed esterne e una rete gruppo toorestrict l'accesso.

Crea hello seguenti risorse:

| Tipo di risorsa | Nome | Descrizione |
| --- | --- | --- |
| Rete virtuale |vnInternal |Utilizzato con BitBucket applicazione hello e sia connesso tramite una rete aziendale del tooContoso ExpressRoute.  Una subnet (sbBitBucket) fornisce un'applicazione hello con uno spazio di indirizzi IP specifico. |
| Rete virtuale |vnExternal |È disponibile per le applicazioni future che richiedono endpoint pubblici. |
| Gruppo di sicurezza di rete |nsgBitBucket |Assicura che hello è ridotto al minimo la superficie di attacco di questo carico di lavoro consentendo le connessioni solo sulla porta 443 per la subnet hello in un'applicazione hello risiede (sbBitBucket). |

### <a name="resource-locks"></a>Blocchi risorse
Dave riconosce che deve essere protetto connettività hello dalla rete virtuale interna toohello Contoso rete aziendale da qualsiasi e script o l'eliminazione accidentale.

Crea seguente hello [blocco di risorsa](resource-group-lock-resources.md):

| Tipo di blocco | Risorsa | Descrizione |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Impedisce agli utenti di rete virtuale di eliminazione hello o subnet, ma non impedisce l'aggiunta di hello di nuove subnet. |

### <a name="azure-automation"></a>Automazione di Azure
Dave non ha nulla tooautomate per questa applicazione. Anche se ha creato un account di Automazione di Azure, inizialmente non lo userà.

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Gestione dei servizi IT di Contoso deve tooquickly identificare e gestire i rischi. Desidera inoltre toounderstand esistano problemi.  

toofulfill questi requisiti, hello Abilita Dave [Centro sicurezza di Azure](../security-center/security-center-intro.md)e fornisce sicurezza responsabile toohello accesso.

## <a name="scenario-2-customer-facing-app"></a>Scenario 2: app destinata ai clienti
leadership business Hello nella business unit di hello supply chain ha identificato vari engagement di tooincrease opportunità con i clienti di Contoso utilizzando una carta fedeltà. Il team di Alice deve creare l'applicazione e decide che Azure aumenta le possibilità toomeet hello esigenza aziendale. Alice funziona con Dave da due sottoscrizioni tooconfigure ETS per lo sviluppo e il funzionamento di questa applicazione.

### <a name="azure-subscriptions"></a>Sottoscrizioni Azure
Dave accede toohello Azure Enterprise Portal e visualizzerà che tale reparto catena di fornitura hello esiste già.  Tuttavia, quando questo progetto è hello primo progetto di sviluppo per il team di catena di fornitura hello in Azure, Dave riconosce hello necessario per un nuovo account per il team di sviluppo di Alice.  Crea account "R & D" hello, in cui il team e assegna accesso tooAlice. Alice accede tramite il portale di Azure hello e crea due sottoscrizioni: i server di sviluppo hello uno toohold e uno toohold hello produzione.  Lei conforme agli standard di denominazione di hello stabilita in precedenza durante la creazione di hello seguenti sottoscrizioni:

| Uso della sottoscrizione | Nome |
| --- | --- |
| Sviluppo. |SupplyChain ResearchDevelopment LoyaltyCard Development |
| Produzione |SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>Criteri
Dave e Alice discutere applicazione hello e identificare che questa applicazione viene utilizzata solo i clienti nell'area Nord America hello.  Alice e il suo team pianificare l'ambiente del servizio dell'applicazione di Azure toouse e un'applicazione hello toocreate SQL Azure. Si potrebbe essere necessario toocreate le macchine virtuali durante lo sviluppo.  Alice vuole tooensure con risorse hello necessari tooexplore ed esaminare i problemi senza recuperando ETS proprio gli sviluppatori.

Per hello **sottoscrizione sviluppo**, creano hello seguenti criteri:

| Campo | Effetto | Descrizione |
| --- | --- | --- |
| location |audit |Creazione di hello delle risorse di hello in qualsiasi area di controllo. |

Non limitano il tipo di hello dello sku di che un utente può creare in fase di sviluppo e non richiedono tag per tutti i gruppi di risorse o le risorse.

Per hello **sottoscrizione di produzione**, creano hello seguenti criteri:

| Campo | Effetto | Descrizione |
| --- | --- | --- |
| location |deny |Negare creazione hello delle risorse di fuori di Stati Uniti hello data center. |
| tags |deny |Richiede il tag del proprietario dell'applicazione |
| tags |deny |Richiede il tag del reparto. |
| tags |append |Aggiungi gruppo di risorse tooeach tag che indica l'ambiente di produzione. |

Non limitano il tipo di hello dello sku di che un utente può creare nell'ambiente di produzione.

### <a name="resource-tags"></a>Tag delle risorse
Dave riconosce che deve toohave informazioni specifiche tooidentify hello business corretto gruppi per la fatturazione e la proprietà. Definisce i tag delle risorse per i gruppi di risorse e le risorse.

| Nome del tag | Valore del tag |
| --- | --- |
| ApplicationOwner |nome Hello di persona hello che gestisce l'applicazione. |
| department |centro di costo Hello del gruppo di hello che paga per hello consumo di Azure. |
| EnvironmentType |**Produzione** (anche se la sottoscrizione hello include **produzione** in nome hello, incluso il tag consente facile identificazione quando si esaminano le risorse nel portale di hello o nella fattura hello.) |

### <a name="core-networks"></a>Reti core
Hello ETS Contoso informazioni revisioni del team di gestione di protezione e al rischio di Dave proposto pianificare toomove hello applicazione tooAzure. Desiderano tooensure che hello applicazione carta fedeltà correttamente isolate e protette in una rete Perimetrale.  toofulfill questo requisito, Dave e Alice creare una rete virtuale esterna e un hello di tooisolate gruppo di sicurezza rete applicazione carta fedeltà dalla rete aziendale di Contoso hello.  

Per hello **sottoscrizione sviluppo**, creano:

| Tipo di risorsa | Nome | Descrizione |
| --- | --- | --- |
| Rete virtuale |vnInternal |Serve l'ambiente di sviluppo di carta fedeltà Contoso hello ed è connesso tramite la rete aziendale del tooContoso ExpressRoute. |

Per hello **sottoscrizione di produzione**, creano:

| Tipo di risorsa | Nome | Descrizione |
| --- | --- | --- |
| Rete virtuale |vnExternal |Ospita un'applicazione hello carta fedeltà e non è connesso direttamente tooContoso's ExpressRoute. Push del codice tramite il sistema di codice sorgente direttamente i servizi PaaS toohello. |
| Gruppo di sicurezza di rete |nsgBitBucket |Assicura che hello è ridotto al minimo la superficie di attacco di questo carico di lavoro, consentendo solo la comunicazione in entrata sulla porta TCP 443.  Contoso sta indagando anche attraverso un firewall applicazione Web per protezione aggiuntiva. |

### <a name="resource-locks"></a>Blocchi risorse
Dave, Alice conferisce e decide di blocchi di risorse tooadd su alcune delle risorse chiave hello hello ambiente tooprevent accidentali durante un push volontariamente codice.

Creano hello blocco seguente:

| Tipo di blocco | Risorsa | Descrizione |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |tooprevent agli utenti di eliminare la rete virtuale hello o subnet. blocco Hello non impedire l'aggiunta di hello di nuove subnet. |

### <a name="azure-automation"></a>Automazione di Azure
Alice e il team di sviluppo hanno ambiente hello toomanage di runbook completo per questa applicazione. i runbook Hello consentono di hello aggiunta o l'eliminazione di nodi per un'applicazione hello e altre attività DevOps.

toouse questi runbook, abilitare [automazione](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Gestione dei servizi IT di Contoso deve tooquickly identificare e gestire i rischi. Desidera inoltre toounderstand esistano problemi.  

toofulfill questi requisiti, Davide consente Centro sicurezza di Azure. Verificare che esegue il monitoraggio risorse hello hello Centro sicurezza di Azure e fornisce l'accesso ai team di sicurezza e DevOps toohello.

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla creazione di modelli di gestione delle risorse, vedere [procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).

