---
title: "Considerazioni di progettazione identità ibrida Active Directory aaaAzure - definire una strategia di adozione di identità ibrida | Documenti Microsoft"
description: "Con il controllo di accesso condizionale, Azure Active Directory verifica specifiche condizioni hello selezionate per l'autenticazione utente hello e prima di consentire l'accesso toohello applicazione. Quando queste condizioni sono soddisfatte, l'utente di hello è autenticato e accesso toohello applicazione consentita."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Definire una strategia di adozione della soluzione ibrida di gestione delle identità
In questa attività verranno definite strategia di adozione identità ibrida hello ai ibrida identità soluzione toomeet hello requisiti aziendali che sono stati descritti in:

* [Determinare le esigenze aziendali](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Determinare i requisiti di sincronizzazione della directory](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Determinare i requisiti di autenticazione a più fattori](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Definire la strategia in base alle esigenze aziendali
prima attività Hello indirizzi determinare le esigenze aziendali organizzazioni hello.  È necessario prestare particolare attenzione per non correre il rischio di ampliare eccessivamente l'ambito.  In inizio hello mantenerla semplice, ma è sempre necessario tooplan per una progettazione che verrà contenere e semplificarne la modifica in hello future.  Indipendentemente dal fatto che si tratti di una struttura semplice o uno estremamente complesso, Azure Active Directory è piattaforma di Microsoft Identity hello che supporta Office 365, Microsoft Online Services e applicazioni cloud.

## <a name="define-an-integration-strategy"></a>Definire una strategia di integrazione
Microsoft ha previsto tre principali scenari di integrazione, ovvero identità cloud, identità sincronizzate e identità federate.  È necessario valutare l'adozione di una di queste strategie di integrazione.  Hello strategia scelta può variare e includere le decisioni di hello nella scelta di uno, il tipo dell'esperienza utente di cui si desidera tooprovide, si dispone di alcuni dell'infrastruttura esistente di hello già sul posto e novità hello conveniente.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

gli scenari di Hello definiti nelle hello sopra figura sono:

* **Identità cloud**: si tratta di identità che esiste solo nel cloud di hello.  Nel caso di hello di Azure AD, sarebbe risiedono in particolare in directory di Azure AD.
* **Sincronizzato**: si tratta di identità che esistono in locale e nel cloud hello.  Grazie ad Azure AD Connect, questi utenti vengono creati o associati ad account Azure AD esistenti.  Hello hash della password dell'utente sincronizzati dal cloud di toohello ambiente locale hello in quello che viene definito un hash della password.  Durante la sincronizzazione con un'avvertenza hello è che se un utente è disabilitato in hello nell'ambiente locale, può richiedere ore too3 per tale tooshow stato account in Azure AD.  Ciò è dovuto toohello intervallo di tempo di sincronizzazione.
* **Federati**: queste identità esistono sia in locale e nel cloud hello.  Grazie ad Azure AD Connect, questi utenti vengono creati o associati ad account Azure AD esistenti.  

> [!NOTE]
> Per ulteriori informazioni sulle opzioni di sincronizzazione hello leggere [integrazione delle identità locali con Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Consente di determinare hello vantaggi e svantaggi di ognuna delle seguenti strategie hello Hello nella tabella seguente:

| Strategia | Vantaggi | Svantaggi: |
| --- | --- | --- |
| **Identità cloud** |Toomanage più semplice per l'organizzazione di piccole dimensioni. <br> Non è necessario disporre di hardware aggiuntive di tooinstall No in locale<br>Se l'utente hello lascia la società hello facilmente disabilitata |Gli utenti dovranno toosign-in quando si accede a carichi di lavoro nel cloud hello <br> Le password possono o non sia uguale hello per le identità cloud e locali |
| **Identità sincronizzate** |La password locale consente di eseguire l'autenticazione sia alla directory locale che alla directory cloud  <br>Toomanage più semplice per le organizzazioni di piccole, medie o grandi dimensioni <br>Gli utenti possono usufruire dell'accesso Single Sign-On per alcune risorse <br> Metodo preferito di Microsoft per la sincronizzazione <br> Toomanage semplice |Alcuni clienti potrebbero essere riluttanti toosynchronize le directory con hello cloud a causa di polizia specifico della società |
| **Federato** |Gli utenti possono usufruire dell'accesso Single Sign-On  <br>Se un utente viene terminato o si lascia, hello account può essere disabilitato immediatamente e revocato l'accesso,<br> Supporta scenari avanzati che non sono disponibili con le identità sincronizzate |I passaggi più toosetup e configurare <br> Manutenzioni superiori <br> Potrebbe essere necessario hardware aggiuntivo infrastruttura STS hello <br> Può richiedere server federativo di hello tooinstall hardware aggiuntivo. Se si utilizza ADFS, è necessario software aggiuntivo <br> È richiesta una configurazione estesa per SSO <br> Punto di errore critico di errore se il server federativo hello è attivo, gli utenti non saranno in grado di tooauthenticate |

### <a name="client-experience"></a>Esperienza client
strategia di Hello utilizzate determineranno l'esperienza di accesso utente hello.  Hello tabelle seguenti forniscono informazioni su quali utenti hello dovrebbero loro Accedi riscontrarsi toobe.  Si noti che non tutti i provider di identità federate supportano l'accesso Single Sign-On in tutti gli scenari.

**Applicazioni di rete privata e aggiunte a un dominio**:

|  | Identità sincronizzata | Identità federata |
| --- | --- | --- |
| Web browser |Autenticazione basata su form |l'accesso Single sign in, a volte necessari l'ID organizzazione toosupply |
| Outlook |Richiesta di credenziali |Richiesta di credenziali |
| Skype for Business (Lync) |Richiesta di credenziali |Single Sign-On per Lync, richiesta di credenziali per Exchange |
| OneDrive for Business |Richiesta di credenziali |Single Sign-On |
| Abbonamento a Office Pro Plus |Richiesta di credenziali |Single Sign-On |

**Risorse esterne o non attendibili**:

|  | Identità sincronizzata | Identità federata |
| --- | --- | --- |
| Web browser |Autenticazione basata su form |Autenticazione basata su form |
| Outlook, Skype for Business (Lync), OneDrive for Business, abbonamento a Office |Richiesta di credenziali |Richiesta di credenziali |
| Exchange ActiveSync |Richiesta di credenziali |Single Sign-On per Lync, richiesta di credenziali per Exchange |
| App per dispositivi mobili |Richiesta di credenziali |Richiesta di credenziali |

Se si è stabilito dall'attività 1 di disporre di un 3rd party toouse corso IdP o sono una tooprovide federazione con Azure AD, sono necessarie funzionalità toobe comunicata hello seguenti supportati:

* Può supportare qualsiasi provider SAML 2.0 che è conforme a hello profilo SP-Lite tooAzure autenticazione Active Directory e le applicazioni associate
* Supporta passivo l'autenticazione, che facilita l'autenticazione tooOWA, Simulato, e così via.
* I client di Exchange Online possono essere supportati tramite hello Enhanced Client profilo (ECP di SAML 2.0)

È anche importante conoscere quali funzionalità non saranno disponibili:

* Senza WS-Trust/Federation tutti gli altri client attivi verranno interrotti
  * Che indica che nessun client Lync, i client OneDrive, Office Subscription, Office Mobile precedente tooOffice 2016
* Transizione di autenticazione toopassive Office consentiranno toosupport pure SAML 2.0 IdPs, ma il supporto sarà comunque in modo da client a

> [!NOTE]
> Per hello hello articolo http://aka.ms/ssoproviders leggere l'elenco più aggiornato.
> 
> 

## <a name="define-synchronization-strategy"></a>Definire la strategia di sincronizzazione
In questa attività si definirà strumenti hello che verranno locale dati toohello nel cloud utilizzati toosynchronize hello organizzazione e quali topologia, è necessario utilizzare.  Poiché, la maggior parte delle organizzazioni di utilizzare Active Directory, informazioni sull'utilizzo di Azure AD Connect tooaddress hello domande viene fornite in modo dettagliato.  Per gli ambienti che non dispongono di Active Directory, informazioni sull'uso di FIM 2010 R2 oppure toohelp MIM 2016 pianificare questa strategia.  Tuttavia, nelle versioni future di Azure AD Connect supporterà directory LDAP, pertanto a seconda dell'indicatore cronologico, queste informazioni potrebbero essere in grado di tooassist.

### <a name="synchronization-tools"></a>Strumenti di sincronizzazione
Negli anni hello, diversi strumenti di sincronizzazione sono esisteva ed è utilizzata per vari scenari.  Attualmente Azure AD Connect è hello passare tootool ideale per tutti gli scenari supportati.  Anche AAD Sync e DirSync sono ancora in circolazione e potrebbero ancora essere presenti nell'ambiente in uso. 

> [!NOTE]
> Per hello informazioni più recenti relative hello supportata funzionalità di ogni strumento, vedere [confronto degli strumenti di integrazione Directory](active-directory-hybrid-identity-design-considerations-tools-comparison.md) articolo.  
> 
> 

### <a name="supported-topologies"></a>Topologie supportate
Quando si definisce una strategia di sincronizzazione, deve essere determinata topologia hello utilizzata. A seconda di hello informazioni che è state definite nel passaggio 2, è possibile determinare la topologia sono uno toouse appropriato hello. Hello singola foresta, singolo topologia di Active Directory di Azure è hello più comune ed è costituito da una singola foresta di Active Directory e una singola istanza di Azure AD.  Si sta toobe utilizzato nella maggior parte degli scenari di hello e topologia hello previsto quando si utilizza l'installazione di Express la connessione AD Azure, come illustrato nella figura che segue hello.

![](./media/hybrid-id-design-considerations/single-forest.png)Singola foresta Scenario è molto comune per toohave anche piccole e grandi organizzazioni più insiemi di strutture, come illustrato nella figura 5.

> [!NOTE]
> Per ulteriori informazioni su hello locale diversi e topologie di Azure Active Directory con sincronizzazione di Azure AD Connect leggere l'articolo hello [topologie per Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Scenario a più foreste

Se in questo caso hello hello quindi multi-forest-singola topologia di Active Directory di Azure è necessario considerare se hello gli elementi seguenti sono vere:

* Gli utenti dispongono solo 1 identità in tutte le foreste: hello sezione gli utenti che identifica univocamente questa procedura viene descritta più dettagliatamente.
* autenticazione dell'utente Hello toohello foresta in cui si trova la propria identità
* Il nome dell'entità utente e l'ancoraggio di origine (ID immutabile) provengono da questa foresta
* Tutte le foreste sono accessibili da Azure AD Connect – ciò significa non è necessario toobe di dominio e può essere inserito in una rete Perimetrale, se ciò facilita questo.
* Gli utenti hanno una sola cassetta postale
* insieme di strutture di Hello che ospita postale una cassetta ha hello migliore qualità dei dati per gli attributi visibili in hello Exchange elenco (globale)
* Se non vi è alcuna cassetta postale per utente hello e qualsiasi foresta può essere utilizzati toocontribute questi valori
* Se si dispone di una cassetta postale collegata, è anche un altro account in toosign un diverso insieme di strutture utilizzato in.

> [!NOTE]
> Gli oggetti che esistono in sia in locale e nel cloud hello "connessi" tramite un identificatore univoco. Nel contesto di hello della sincronizzazione della Directory, questo identificatore univoco è hello di cui viene fatto riferimento tooas SourceAnchor. Nel contesto di hello di Single Sign-On, si tratta di cui viene fatto riferimento tooas hello ImmutableId. [Concetti di progettazione per Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) per altre considerazioni relative hello uso di SourceAnchor.
> 
> 

Se hello precedente non sono true e si dispone di più di un account attivo o più cassette postali, Azure AD Connect verrà scegliere uno e ignorare hello altri.  Se sono stati collegati alle cassette postali ma nessun altro account, questi account non sarà esportato tooAzure Active Directory e che l'utente non sarà un membro di tutti i gruppi.  Questo comportamento è diverso da come si trovava hello precedenti con DirSync ed è il supporto intenzionale toobetter questi scenari a più foreste. Uno scenario con più foreste è illustrato nella figura hello riportato di seguito.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Topologia multipla di Azure AD a più foreste**

È consigliabile toohave che solo una singola directory di Azure AD per un'organizzazione, ma è supportata, che viene mantenuta una relazione 1:1 tra un server di sincronizzazione di Azure AD Connect e una directory di Azure AD.  Per ogni istanza di Azure AD, sarà necessaria un'installazione di Azure AD Connect.  Inoltre, Azure AD, per impostazione predefinita è isolato e gli utenti in un'istanza di Azure Active Directory non saranno in grado di toosee gli utenti in un'altra istanza.

È possibile e supportati tooconnect una istanza di directory di Azure AD toomultiple di Active Directory come illustrato nella figura che segue hello in locale:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Scenario di filtro a singola foresta**

In ordine toodo seguito hello deve essere vere:

* I server del servizio di sincronizzazione Azure AD Connect devono essere configurati per l'applicazione di filtri, in modo che ogni server includa un set di oggetti che si escludono a vicenda su cui operare,  L'operazione viene eseguita, ad esempio, da ambito di ogni server tooa dominio o l'unità Organizzativa.
* È possibile registrare solo un dominio DNS in una singola directory di Azure AD in modo hello UPN degli utenti hello in hello locale Active Directory è necessario utilizzare spazi dei nomi distinti
* Gli utenti in un'istanza di Azure Active Directory saranno solo gli utenti in grado di toosee dalla relativa istanza.  Questo non essere in grado di toosee utenti hello altre istanze
* Solo una delle directory hello Azure AD possa abilitare Exchange ibrido con hello AD locale
* Esclusione reciproca si applica anche toowrite-back.  Alcune funzionalità di writeback non sono quindi supportate con questa topologia, perché presuppongono una singola configurazione locale.  Sono inclusi:
  * Writeback dei gruppi con la configurazione predefinita
  * Writeback dei dispositivi

Tenere presente che segue hello non è supportata e non deve essere scelta come un'implementazione:

* Non è supportato toohave più server di sincronizzazione di Azure AD Connect connessione directory toohello stesso Azure Active Directory, anche se sono configurati toosynchronize si escludono a vicenda set dell'oggetto
* È supportato toosync hello directory toomultiple Azure AD dell'utente stesso. 
* È inoltre supportato toomake una modifica alla configurazione toomake gli utenti in uno tooappear di Azure AD come contatti in un'altra directory di Azure AD. 
* È inoltre tooconnect toomultiple Azure Active Directory di toomodify non supportato Azure AD Connect sincronizzazione.
* Come previsto da progettazione, le directory di Azure AD sono isolate. Configurazione di hello toochange non supportato di Azure AD Connect sincronizzare tooread i dati da un'altra directory di Azure AD in toobuild un tentativo di un elenco indirizzi globale comune e unificato tra le directory hello è. È inoltre gli utenti di tooexport non supportato come contatti tooanother AD usando la sincronizzazione di Azure AD Connect on-premise.

> [!NOTE]
> Se l'organizzazione limita computer della rete di connettersi a Internet toohello, questo articolo vengono elencati gli endpoint di hello (FQDN, IPv4 e gli intervalli di indirizzi IPv6) che è necessario includere nella consentono l'uscita elenchi e l'area siti attendibili di Internet Explorer di tooensure i computer client i computer possono utilizzare correttamente Office 365. Per altre informazioni, vedere [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Definire la strategia di autenticazione a più fattori
In questa attività che si definirà hello toouse strategia multi-factor authentication.  Azure Multi-Factor Authentication è disponibile in due diverse versioni.  Uno è basato su cloud e altri hello è locale con Azure MFA Server hello.  In base a hello valutazione che è sopra riportato è possibile determinare quale soluzione è hello quello corretto per la strategia.  Utilizzare la tabella hello sotto toodetermine opzione di progettazione più soddisfare il requisito di sicurezza della società:

Opzioni di progettazione per l'autenticazione a più fattori:

| Toosecure Asset | Autenticazione a più fattori nel cloud hello | MFA in locale |
| --- | --- | --- |
| App Microsoft |sì |sì |
| App SaaS nella raccolta di app hello |sì |sì |
| Le applicazioni IIS pubblicate tramite proxy app per Azure AD |sì |sì |
| Applicazioni di IIS non pubblicate tramite hello Proxy App di Azure AD |no |sì |
| Accesso remoto, ad esempio VPN, Gateway Desktop remoto |no |sì |

Anche se potrebbe scelto in una soluzione per la strategia, è comunque necessario valutazione di hello toouse dall'alto in cui si trovano gli utenti.  Ciò potrebbe causare toochange soluzione hello.  Utilizzare tabella hello seguente tooassist è determinare questo valore:

| Posizione degli utenti | Opzione di progettazione preferita |
| --- | --- |
| Azure Active Directory |Multi-FactorAuthentication nel cloud hello |
| Azure AD e AD locale usando la federazione con AD FS |Entrambi |
| Azure AD e Active Directory locale con Azure AD Connect, senza sincronizzazione delle password |Entrambi |
| Azure AD e Active Directory locale con Azure AD Connect, con sincronizzazione delle password |Entrambi |
| Active Directory locale |Server Multi-Factor Authentication |

> [!NOTE]
> È inoltre necessario assicurarsi che hello multi-factor authentication progettazione l'opzione selezionata supporta le funzionalità di hello necessari per la progettazione.  Per altre informazioni vedere [scegliere una soluzione di sicurezza di multi-factor hello è](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Provider di Multi-Factor Authentication
La modalità Multi-Factor Authentication è disponibile per impostazione predefinita per gli amministratori globali che dispongono di un tenant Azure Active Directory. Tuttavia, se si desidera tooextend multi-factor authentication tooall degli utenti e/o tooyour gli amministratori globali toobe tootake in grado di sfruttare funzionalità quali il portale di gestione di hello, messaggi di saluto personalizzati e i report, quindi è necessario acquistare e configurare Provider di multi-Factor Authentication.

> [!NOTE]
> È inoltre necessario assicurarsi che hello multi-factor authentication progettazione l'opzione selezionata supporta le funzionalità di hello necessari per la progettazione. 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Determinare i requisiti di protezione dati](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

