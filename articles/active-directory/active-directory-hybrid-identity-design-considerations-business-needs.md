---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di identità | Documenti Microsoft"
description: "Identificare hello esigenze aziendali che potrebbero causare requisiti hello toodefine per la progettazione di identità ibrida hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Determinare i requisiti per la soluzione ibrida di gestione delle identità
Hello primo passaggio nella progettazione di una soluzione con identità ibrida consiste requisiti hello toodetermine per organizzazione hello che sarà l'utilizzo di questa soluzione.  Gestione identità ibride viene avviato come un ruolo di supporto (supporta tutte le altre soluzioni di cloud mediante l'autenticazione) e passa le funzionalità nuove e interessanti tooprovide che sbloccare nuovi carichi di lavoro per gli utenti.  Questi carichi di lavoro o i servizi che si desidera tooadopt per gli utenti stabiliscono requisiti hello per la progettazione di identità ibrida hello.  Tali servizi e i carichi di lavoro necessario gestione identità ibride tooleverage sia in locale e nel cloud hello.  

È necessario toogo gli aspetti chiave di hello business toounderstand che cos'è un requisito ora e le società hello piani per hello future. Se non si dispone di visibilità hello della strategia a lungo termine hello per la progettazione di identità ibride, probabilità sono che la soluzione non sarà scalabile con esigenze aziendali di hello aumenta e modifica.   T ha diagramma seguente viene illustrato un esempio di un ibrido identità architettura hello carichi di lavoro sono viene sbloccato per gli utenti. Questo è solo un esempio di tutte le possibilità nuovo hello che può essere sbloccato e può essere recapitato con una strategia di identità ibrida a tinta unita. 

Alcuni componenti che fanno parte dell'architettura di identità ibrida hello![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Determinare le esigenze aziendali
Ogni società dispone di requisiti diversi, anche se queste aziende fanno parte di hello stesso settore, i requisiti aziendali reali hello potrebbero variare. È possibile sfruttare le procedure consigliate del settore hello, ma in definitiva è hello esigenze aziendali che potrebbero causare requisiti hello toodefine per la progettazione di identità ibrida hello. 

Assicurarsi che segue hello tooanswer domande tooidentify l'azienda deve:

* La società esegue la ricerca toocut costi operativi IT?
* La società esegue la ricerca toosecure risorse di cloud (app SaaS, infrastruttura)?
* La vostra società ricerca toomodernize il reparto IT?
  * Sono gli utenti più complessi e di applicazioni mobili IT toocreate eccezioni nel tipo diverso di tooallow di rete Perimetrale di risorse di traffico tooaccess diverse?
  * La società dispone di applicazioni legacy che necessari toobe pubblicati utente toothese ma che non sono facilmente toorewrite?
  * Azienda necessario tooaccomplish tutte queste attività e gestirlo in un controllo a hello contemporaneamente?
* La società ricerca identità degli utenti toosecure e ridurre i rischi riportando nuovi strumenti che consentono di sfruttare competenze hello di Azure sicurezza esperienza locale Microsoft?
* È l'azienda sta tentando di eliminare hello tooget temuto account "esterni" in locale e spostarli toohello cloud in cui non sono più una minaccia inattiva all'interno dell'ambiente locale?

## <a name="analyze-on-premises-identity-infrastructure"></a>Analizzare l'infrastruttura di gestione delle identità locale
Dopo aver creato un'idea relative ai requisiti di business della società, è necessario tooevaluate l'infrastruttura di identità locale. Questa valutazione è importante per la definizione di hello requisiti tecnici toointegrate identità soluzione toohello cloud identity management sistema corrente. Verificare che hello tooanswer seguenti domande:

* Qual è la soluzione di autenticazione e autorizzazione locale usata dall'azienda? 
* Al momento l'azienda usa servizi di sincronizzazione locali?
* L'azienda usa provider di identità di terze parti (IdP)?

È inoltre necessario toobe compatibile con i servizi cloud hello che l'azienda potrebbe avere. Esegue una valutazione toounderstand hello corrente integrazione SaaS, i modelli di soluzioni IaaS o PaaS nell'ambiente in uso è molto importante. Verificare che hello tooanswer seguente domande durante la valutazione:

* L'azienda usa un qualsiasi tipo d'integrazione con un provider di servizi cloud?
* In caso affermativo, quali sono i servizi in uso?
* Questa integrazione è già presente nell'ambiente di produzione o si tratta di un progetto pilota?

> [!NOTE]
> Se si dispone di un mapping accurato di tutte le App e servizi cloud, è possibile utilizzare lo strumento di Cloud App Discovery hello. Questo strumento fornisce al reparto IT la visibilità necessaria su tutte le app cloud, aziendali e non, usate nell'organizzazione. Che rende più semplice che mai toodiscover shadow IT dell'organizzazione, inclusi i dettagli su modelli di utilizzo e agli utenti l'accesso delle applicazioni cloud. vedere tooget avviato [individuazione app Cloud](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Valutare i requisiti di integrazione della soluzione di gestione delle identità
Successivamente, sarà necessario requisiti di integrazione delle identità di tooevaluate hello. Questa valutazione è requisiti tecnici di hello toodefine importanti per la modalità in cui verranno autenticati gli utenti, come la presenza dell'organizzazione hello apparirà nel cloud hello, come organizzazione hello consentirà autorizzazione e quale esperienza utente hello è toobe continua. Verificare che hello tooanswer seguenti domande:

* L'organizzazione prevede di usare la federazione, l'autenticazione standard o entrambe?
* La federazione è un requisito?  A causa delle operazioni seguenti hello:
  * Accesso Single Sign-On basato su Kerberos
  * L'azienda dispone di applicazioni locali (sviluppate internamente o da terze parti) che usano il formato SAML o funzionalità federative simili.
  * Multi-Factor Authentication tramite smart card. RSA SecurID e così via.
  * Regole di accesso client che consentono di risolvere domande hello riportate di seguito:
    1. È possibile bloccare tutti l'accesso esterno tooOffice 365 basate sull'indirizzo IP di hello del client hello?
    2. È possibile bloccare tutti l'accesso esterno tooOffice 365, ad eccezione di Exchange ActiveSync?
    3. È possibile bloccare tutti l'accesso esterno tooOffice 365, ad eccezione delle applicazioni basate su browser (OWA, Simulato)
    4. È possibile bloccare tutti l'accesso esterno tooOffice 365 per i membri di gruppi di Active Directory designati
* Preoccupazioni relative a sicurezza e controllo
* Si dispone già di un investimento esistente in una soluzione di autenticazione federata
* Specifica il nome dell'organizzazione verrà utilizzati per il dominio nel cloud hello?
* Organizzazione di hello dispone di un dominio personalizzato?
  1. Questo dominio è pubblico e facile da verificare tramite DNS?
  2. In caso contrario, quindi si dispone di un dominio pubblico che può essere utilizzato tooregister un UPN alternativo in Active Directory?
* Sono identificatori utente hello coerenti per la rappresentazione di cloud? 
* Organizzazione di hello dispone di applicazioni che richiedono l'integrazione con servizi cloud?
* Organizzazione di hello dispone di più domini e verrà tutte utilizzano l'autenticazione standard o federata?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Valutare le applicazioni in esecuzione nell'ambiente
Dopo avere un'idea riguardanti locale e dell'infrastruttura cloud, è necessario applicazioni hello tooevaluate eseguite in questi ambienti. Questa valutazione è importante toodefine hello toointegrate requisiti tecnici di sistema di gestione identità queste applicazioni toohello cloud. Verificare che hello tooanswer seguenti domande:

* Dove risiederanno le applicazioni?
* Gli utenti accederanno alle applicazioni locali?  Nel cloud hello? A entrambe?
* Sono presenti i piani di carichi di lavoro tootake hello esistente dell'applicazione e spostarli toohello cloud?
* Esistono piani toodevelop nuove applicazioni che risiedono in locale o in hello cloud che utilizzeranno l'autenticazione cloud?

## <a name="evaluate-user-requirements"></a>Valutare i requisiti degli utenti
È anche i requisiti dell'utente tooevaluate hello. Questa valutazione è passaggi hello toodefine importanti che è necessaria per caricamento e l'assistenza degli utenti, di transizione toohello cloud. Verificare che hello tooanswer seguenti domande:

* Gli utenti accederanno alle applicazioni in locale?
* Gli utenti accederanno applicazioni nel cloud hello?
* Come eseguire gli utenti in genere accesso tootheir ambiente locale?
* Come gli utenti accesso toohello verrà cloud?

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Determinare i requisiti di risposta agli eventi imprevisti](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) esaminerà le opzioni di hello disponibili e i vantaggi o svantaggi di ogni opzione.  Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Determinare i requisiti di sincronizzazione della directory](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

