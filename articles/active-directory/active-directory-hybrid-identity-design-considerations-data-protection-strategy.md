---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - definire la strategia di protezione dati | Documenti Microsoft"
description: "Strategia di protezione dei dati hello definirai ai ibrida identità soluzione toomeet hello requisiti aziendali definiti."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Definire una strategia di protezione dei dati per la soluzione ibrida di gestione delle identità
In questa attività verranno definite strategia di protezione dei dati hello ai ibrida identità soluzione toomeet hello requisiti aziendali definiti in:

* [Determinare i requisiti di protezione dati](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Determinare i requisiti di gestione del contenuto](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Determinare i requisiti di controllo di accesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Determinare i requisiti di risposta agli eventi imprevisti](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Definire le opzioni di protezione dati
Come descritto in [Determinare i requisiti di sincronizzazione della directory](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), è possibile sincronizzare Microsoft Azure AD con Servizi di dominio Active Directory locale. Questa integrazione consente alle organizzazioni tooleverage AD Azure tooverify credenziali quando tentano tooaccess alle risorse aziendali. Questa operazione può essere eseguita per entrambi gli scenari: dati rest locale e nel cloud hello.  Accesso toodata in Azure AD richiede l'autenticazione utente tramite un servizio token di sicurezza (STS).

Una volta autenticato, nome dell'entità hello utente (UPN) viene letto dal token di autenticazione hello e hello replicati partizione e contenitore corrispondente viene determinato toohello del dominio dell'utente. Informazioni sull'esistenza, lo stato abilitato e ruolo dell'utente hello viene usate da hello autorizzazione sistema toodetermine se tenant di destinazione toohello hello richiesta di accesso è autorizzato per questo utente in questa sessione. Determinate azioni autorizzate (in particolare, creare l'utente, la reimpostazione della password) creare un audit trail che può essere utilizzato da un tenant rispetto della conformità toomanage amministratore o indagini.

Lo spostamento dei dati dal Data Center locale nell'archiviazione di Azure tramite una connessione Internet potrebbe non essere sempre fattibile scadenza toodata volume, la disponibilità di larghezza di banda o altre considerazioni. Hello [servizio di importazione/esportazione di archiviazione di Azure](../storage/common/storage-import-export-service.md) fornisce un'opzione basata su hardware per l'inserimento e recupero di grandi volumi di dati nell'archiviazione blob. Consente di toosend [crittografata con BitLocker](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) unità disco rigido direttamente le unità tooreturn tooan Data Center di Azure in cui gli operatori di cloud caricherà l'account di archiviazione tooyour contenuto hello, o è possibile scaricare tooyour i dati di Azure tooyou. Solo i dischi crittografati vengono accettati per il processo (tramite una chiave di BitLocker generata dal servizio hello stesso durante l'installazione di processo hello). la chiave di BitLocker Hello viene fornita tooAzure separatamente, in modo da fornire fuori banda chiave condivisione.

Poiché i dati in transito possono avvenire in diversi scenari, è anche tooknow rilevanti che usa Microsoft Azure [la rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/) il traffico tenant tooisolate da un altro, avvalendosi di misure, ad esempio livello host e guest firewall, il filtro dei pacchetti IP, il blocco delle porte e gli endpoint HTTPS. Tuttavia, la maggior parte delle comunicazioni interne di Azure, incluse quelle da infrastruttura a infrastruttura e da infrastruttura a cliente (locale), sono crittografate. Un altro scenario importante è comunicazioni hello in Data Center di Azure; Microsoft gestisce tooassure reti che nessuna macchina virtuale può rappresentare o intercettare su indirizzo IP hello di un altro. TLS/SSL viene utilizzato per accedere al database SQL o archiviazione di Azure o durante la connessione a servizi tooCloud. In questo caso, l'amministratore hello cliente è responsabile per ottenere un certificato TLS/SSL e la distribuzione di un'infrastruttura tootheir tenant. Il traffico di dati, lo spostamento tra le macchine virtuali nella stessa distribuzione hello o tra tenant in un'unica distribuzione tramite la rete virtuale di Microsoft Azure possono essere protetti tramite protocolli di comunicazione crittografata, ad esempio HTTPS, SSL/TLS o altri.

A seconda delle risposte alle domande hello [determinare i requisiti di protezione dati](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), dovrebbe essere in grado di toodetermine come si desidera tooprotect i dati e come soluzione con identità ibrida hello fornirà assistenza su tale. tabella Hello Mostra opzioni hello è supportate da Azure che sono disponibili per ogni scenario di protezione dati.

| Opzioni di protezione dati | Inattivi nel cloud hello | Inattivi in locale | In transito |
| --- | --- | --- | --- |
| Crittografia unità BitLocker |X |X | |
| Database di SQL Server tooencrypt |X |X | |
| Crittografia da VM a VM | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Lettura [conformità per funzionalità](https://azure.microsoft.com/support/trust-center/services/) in [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow informazioni su certificazioni hello non conforme a ogni servizio di Azure.
> Poiché le opzioni di hello per la protezione dei dati utilizzano un approccio a più livelli, il confronto tra tali opzioni non sono applicabili per questa attività. Verificare che, sfruttate tutte le opzioni disponibili per ogni stato che saranno dati hello.
>
>

## <a name="define-content-management-options"></a>Definire le opzioni di gestione del contenuto
Uno dei vantaggi dell'utilizzo di Azure AD toomanage un'infrastruttura di identità ibrida è che il processo di hello è completamente trasparente dal punto di vista dell'utente finale di hello. utente Hello tenterà tooaccess una risorsa condivisa, hello risorsa richiede l'autenticazione utente hello avrà toosend un tooAzure di richiesta di autenticazione AD in ordine tooobtain hello token e accedere alle risorse di hello. Questo processo viene eseguito in background, senza alcuna interazione dell'utente. È inoltre possibile toogrant autorizzazione tooa [gruppo](active-directory-manage-groups.md#getting-started-with-access-management) degli utenti in ordine tooallow li tooperform determinate azioni comuni.

Le organizzazioni che si preoccupano circa la privacy dei dati, richiedono in genere la classificazione dei dati per la soluzione da adottare. Se l'infrastruttura locale corrente sta già utilizzando la classificazione dei dati, è possibile tooleverage Azure AD come repository principale di hello dell'identità dell'utente. Uno strumento comune usato in locale per la classificazione dati è [Data Classification Toolkit](https://msdn.microsoft.com/library/Hh204743.aspx) per Windows Server 2012 R2. Questo strumento può aiutare tooidentify, classificare e proteggere i dati nei file server nel cloud privato. È inoltre possibile tooleverage hello [classificazione automatica dei File](https://technet.microsoft.com/library/hh831672.aspx) in Windows Server 2012 tooaccomplish questo.

Se l'organizzazione non dispone di classificazione dei dati sul posto ma deve tooprotect i file riservati senza l'aggiunta di nuovi server on-premise, possono utilizzare Microsoft [servizio Azure Rights Management](https://technet.microsoft.com/library/JJ585026.aspx).  Azure RMS Usa la crittografia, identità e autorizzazione toohelp criteri protetto i file e un messaggio di posta elettronica e funziona su più dispositivi, telefoni, Tablet e PC. Poiché Azure RMS è un servizio cloud, non è necessario poter condividere contenuti protetti con essi, tooexplicitly configurare relazioni di trust con altre organizzazioni. Se queste organizzazioni dispongono già di una directory di Office 365 o di Azure AD, la collaborazione tra organizzazioni è supportata automaticamente. È inoltre possibile sincronizzare solo hello gli attributi di directory che Azure RMS deve toosupport un'identità comune per gli account di Active Directory locale, tramite Azure Active Directory Synchronization Services (AAD Sync) o Azure AD Connect.

Una parte fondamentale della gestione dei contenuti è toounderstand chi sta accedendo ai quali risorse, una funzionalità di registrazione dettagliata è pertanto importante per la soluzione di gestione delle identità hello. Azure AD fornisce la registrazione delle informazioni seguenti per un periodo di oltre 30 giorni:

* Le modifiche nell'appartenenza al ruolo (ad esempio: utente aggiunto il ruolo di amministratore tooGlobal)
* Aggiornamenti delle credenziali, ad esempio modifiche delle password
* Gestione dei domini, ad esempio verifica di un dominio personalizzato, rimozione di un dominio
* Aggiunta o rimozione di applicazioni
* Gestione di utenti, ad esempio aggiunta, rimozione o aggiornamento di un utente
* Aggiunta o rimozione di licenze

> [!NOTE]
> Lettura [Microsoft Azure Security and Audit Log Management](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow ulteriori informazioni sulle funzionalità di registrazione in Azure.
> A seconda delle risposte alle domande hello [determinare i requisiti di gestione dei contenuti](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), dovrebbe essere in grado di toodetermine come si desidera hello toobe contenuto gestito nella soluzione delle identità ibrida. Tutte le opzioni esposte nella tabella 6 sono in grado di integrarsi con Azure AD, ma è importante toodefine che è più adatta alle proprie esigenze di business.
>
>

| Opzioni di gestione del contenuto | Vantaggi | Svantaggi: |
| --- | --- | --- |
| Centralizzata locale (server Active Directory Rights Management) |Controllo completo sull'infrastruttura di server hello responsabile per la classificazione dei dati hello <br> Funzionalità predefinita in Windows Server, senza necessità di licenza o sottoscrizione supplementare <br> Può essere integrato con Azure AD in uno scenario ibrido <br> Supporta la funzionalità Information Rights Management (IRM) nei servizi Microsoft Online come Exchange Online e SharePoint Online, nonché Office 365 <br> Supporta i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e file server che eseguono Windows Server e Infrastruttura di classificazione file. |Manutenzione più elevata (continuare con gli aggiornamenti, la configurazione e potenzialità di aggiornamento), dall'IT proprietario hello Server <br> Richiede un'infrastruttura di server locale<br> Non usa le funzionalità di Azure in modo nativo |
| Centralizzata nel cloud hello (Azure RMS) |Più facile confrontate toomanage toohello soluzione locale <br> Può essere integrato con Servizi di dominio Active Directory in uno scenario ibrido <br>  Completamente integrato con Azure Active Directory <br> Non richiede un server locale nel servizio di hello toodeploy ordine <br> Supporta i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e file server che eseguono Windows Server e Infrastruttura di classificazione file <br> Il reparto IT ha il controllo completo sulla chiave del tenant grazie alla funzionalità BYOK (Bring Your Own Key). |L'organizzazione deve avere una sottoscrizione cloud che supporta RMS  <br> L'organizzazione deve avere un'autenticazione utente toosupport di Azure Active directory per RMS |
| Ibrida (soluzione Azure RMS integrata con un server Active Directory Rights Management locale) |Questo scenario si accumula vantaggi hello di entrambi, centralizzata in locale e nel cloud hello. |L'organizzazione deve avere una sottoscrizione cloud che supporta RMS  <br> L'organizzazione deve avere un'autenticazione utente toosupport di Azure Active directory per RMS, <br> Richiede una connessione tra il servizio cloud di Azure e l'infrastruttura locale |

## <a name="define-access-control-options"></a>Definire le opzioni di controllo di accesso
Sfruttando l'autenticazione di hello, autorizzazione e controllo dell'accesso funzionalità disponibili in Azure AD si sarà in grado di tooenable il toouse aziendale un repository centrale di identità, consentendo agli utenti e partner toouse single sign-on (SSO) come illustrato nell'hello Nella figura seguente:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Gestione centralizzata e integrazione completa con altre directory

Azure Active Directory fornisce toothousands single sign-on di applicazioni SaaS e applicazioni web locali. Leggere hello [elenco di compatibilità di federazione di Azure Active Directory: provider di identità di terze parti che possono essere utilizzati tooimplement accesso single sign-on](https://msdn.microsoft.com/library/azure/jj679342.aspx) articolo per informazioni dettagliate su hello SSO terze parti che sono stati testati da Microsoft. Questa funzionalità consente l'organizzazione tooimplement un'ampia gamma di scenari B2B mantenendo controllo di gestione delle identità e accesso hello. Tuttavia, durante il processo di progettazione di hello B2B è importante toounderstand hello autenticazione che verrà utilizzato dal partner hello e verificare se questo metodo è supportato da Azure. Attualmente, i metodi supportati da Azure AD sono i seguenti:

* SAML (Security Assertion Markup Language)
* OAuth
* Kerberos
* Tokens
* Certificati

> [!NOTE]
> lettura [protocolli di autenticazione di Azure Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow informazioni più dettagliate su ogni protocollo e le relative funzionalità in Azure.
>
>

Con il supporto di hello Azure AD, aziendale dispositivi mobili le applicazioni possono utilizzare hello stesso facile servizi mobili autenticazione esperienza tooallow dipendenti toosign nelle proprie applicazioni per dispositivi mobili con le proprie credenziali aziendali di Active Directory. Con questa funzionalità, Azure AD è supportato come provider di identità nei servizi mobili insieme con hello altri provider di identità è già supportato (che includono Accounts Microsoft, Facebook ID, ID di Google e Twitter ID). Se hello App utilizza hello credenziali dell'utente che si trova nel dominio di Active Directory dell'azienda hello in locale, l'accesso da partner e gli utenti provenienti dal cloud hello hello dovrebbe essere trasparente. È possibile gestire dell'utente applicazioni web too(cloud-based) controllo di accesso condizionale, API web, Microsoft servizi cloud, 3rd applicazioni SaaS di terze parti e applicazioni native client (per dispositivi mobili) e vantaggi hello di sicurezza, il controllo, creazione di report in uno sul posto. Tuttavia, è consigliabile toovalidate questo ambiente non di produzione o con una quantità limitata di utenti.

> [!TIP]
> è importante toomention che Azure AD non dispone di criteri di gruppo di dominio Active Directory è. In Criteri di tooenforce ordine per i dispositivi è necessario, ad esempio una soluzione di gestione di dispositivi mobili [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Una volta hello viene autenticato mediante Azure AD, è importante avrà il livello hello tooevaluate di accesso utente hello. Hello livello di accesso utente hello avrà su una risorsa può variare, mentre Azure AD è possibile aggiungere un ulteriore livello di sicurezza per il controllo toosome di accedere alle risorse, è necessario inoltre tenere presente che risorsa hello stessa può anche avere un proprio elenco di controllo di accesso separatamente, ad esempio hello il controllo di accesso per i file si trova in un File Server. Figura Hello riportata di seguito vengono riepilogati i livelli di controllo di accesso che è possibile includere in uno scenario ibrido hello:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Ogni interazione nel diagramma hello è stato illustrato in figura X rappresenta uno scenario di controllo di accesso che può essere gestito da Azure AD. Di seguito è mostrata una descrizione di ogni scenario:

1. Tooapplications accesso condizionale che sono ospitati in locale: È possibile utilizzare i dispositivi registrati con criteri di accesso per le applicazioni che vengono configurate toouse AD FS con Windows Server 2012 R2. Per altre informazioni su come configurare l'accesso condizionale in locale, vedere [Configurazione dell'accesso condizionale in locale usando il servizio Registrazione del dispositivo di Azure Active Directory](active-directory-conditional-access.md).

2. Controllo di accesso toohello portale di Azure: Azure consente inoltre di portale toohello di controllo di accesso tramite il controllo di accesso basato sui ruoli (RBAC)). Questo metodo consente una quantità di hello società toorestrict hello di operazioni che un utente può eseguire nel portale di Azure hello. Utilizzando portale toohello di RBAC toocontrol accesso, gli amministratori IT possibile delegare l'accesso tramite hello approcci di gestione di accesso seguenti:

* Assegnazione di ruolo in base al gruppo: È possibile assegnare l'accesso tooAzure AD gruppi che possono essere sincronizzati da Active Directory locale. In questo modo tooleverage hello investimenti effettuati in strumenti e processi per la gestione dei gruppi dell'organizzazione. È inoltre possibile utilizzare funzionalità di gestione gruppi delegata hello di Azure AD Premium.
* Usare compilate con i ruoli in Azure: È possibile utilizzare tre ruoli: tooensure proprietario, collaboratore e lettore, che gli utenti e gruppi dispongono di autorizzazioni toodo attività hello solo devono toodo i processi.
* Accesso granulare tooresources: È possibile assegnare ruoli toousers e gruppi per una determinata sottoscrizione, gruppo di risorse o una singola risorsa di Azure, ad esempio un sito Web o di un database. In questo modo, è possibile garantire che gli utenti accedere alle risorse di hello tooall che devono e non tooresources di accesso che non richiedono toomanage.

> [!NOTE]
> Se si creano applicazioni e il controllo di accesso di toocustomize hello per le, è anche possibile toouse ruoli applicazione AD Azure per l'autorizzazione. Esaminare questo [esempio WebApp-RoleClaims-DotNet](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) sulla toobuild toouse l'app questa funzionalità.
>
>

3. Accesso condizionale per applicazioni di Office 365 con Microsoft Intune: gli amministratori IT possono effettuare il provisioning di accesso condizionale dispositivo criteri toosecure alle risorse aziendali, mentre in hello la stessa ora che consente agli information worker in hello tooaccess dispositivi conformi servizi. Per altre informazioni, vedere [Criteri di accesso condizionale dei dispositivi per i servizi di Office 365](active-directory-conditional-access-device-policies.md).

4. Accesso condizionale per le app Saas: [questa funzionalità](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) consente l'accesso tooblock hello possibilità per gli utenti e le regole di accesso di tooconfigure per ogni applicazione multi-factor authentication non su una rete attendibile. È possibile applicare agli utenti tooall regole di autenticazione a più fattori hello che sono stati assegnati toohello applicazione o solo per gli utenti all'interno di specificati gruppi di sicurezza. Gli utenti possono essere esclusi dal requisito di autenticazione a più fattori hello se accedono a un'applicazione hello da un indirizzo IP interno che in hello rete dell'organizzazione.

Poiché le opzioni di hello per il controllo di accesso utilizzano un approccio a più livelli, il confronto tra tali opzioni non sono applicabili per questa attività. Verificare che tutte le opzioni disponibili per ogni scenario in cui è necessario accedere alle risorse di tooyour toocontrol, sfruttate.

## <a name="define-incident-response-options"></a>Definire le opzioni di risposta agli eventi imprevisti
Azure AD può fornire supporto IT tooidentity potenziali rischi di protezione nell'ambiente di hello dal monitoraggio dell'attività dell'utente, del reparto IT può sfruttano l'accesso AD Azure e report sull'utilizzo delle funzionalità toogain visibilità hello integrità e la sicurezza della directory dell'organizzazione. Con queste informazioni, un amministratore IT possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.  [Sottoscrizione di Azure AD Premium](active-directory-get-started-premium.md) dispone di un set di report di sicurezza che possono attivare IT tooobtain queste informazioni. [report di Azure AD](active-directory-view-access-usage-reports.md) sono classificati nel modo seguente:

* **Report anomalie**: includono eventi che è stato rilevato toobe anomali di accesso. L'obiettivo è toomake si è consapevoli di tale attività e consentono di toobe in grado di toomake aggettivo indicano se un evento è sospetto.
* **Report applicazioni integrate**: fornisce informazioni dettagliate sul modo in cui vengono usate le applicazioni cloud nell'organizzazione. Azure Active Directory offre l'integrazione con migliaia di applicazioni cloud.
* **Segnalazioni di errore**: indicano errori che possono verificarsi durante il provisioning di applicazioni tooexternal account.
* **Report specifici dell'utente**: visualizzano i dati del dispositivo/dell'attività di accesso per un utente specifico.
* **Log attività**: include un record di tutti gli eventi controllati entro hello ultime 24 ore, ultimi 7 giorni o ultimi 30 giorni, nonché le modifiche delle attività di gruppo e attività di registrazione e di reimpostazione della password.

> [!TIP]
> Un altro report che contribuisce anche di hello team di risposta a eventi imprevisti che lavora su un case è hello [utente con credenziali perse](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) report.  Questo report evidenzia eventuali corrispondenze tra l'elenco delle credenziali perse e il tenant in uso.
>
>

Altri importanti report predefiniti disponibili in Azure AD che possono risultare utili per fornire le risposte durante l'analisi degli eventi imprevisti sono:

* **Attività di reimpostazione password**: fornire salve approfondite come attivamente la reimpostazione della password è in uso nell'organizzazione hello.
* **Attività di registrazione per la reimpostazione delle password**: fornisce informazioni dettagliate sugli utenti che hanno registrato i propri metodi per la reimpostazione delle password e sui metodi selezionati.
* **Attività del gruppo**: fornisce una cronologia dei gruppo toohello modifiche (ad esempio: gli utenti aggiunti o rimossi) che sono state avviate in hello Pannello di accesso.

Toohello principali funzionalità di creazione report disponibili in Azure AD Premium può essere sfruttata anche durante un processo di analisi di risposta a eventi imprevisti, reparto IT può inoltre sfruttare informazioni tooobtain Report di controllo, ad esempio:

* Le modifiche nell'appartenenza al ruolo (ad esempio: utente aggiunto il ruolo di amministratore tooGlobal)
* Aggiornamenti delle credenziali, ad esempio modifiche delle password
* Gestione dei domini, ad esempio verifica di un dominio personalizzato, rimozione di un dominio
* Aggiunta o rimozione di applicazioni
* Gestione di utenti, ad esempio aggiunta, rimozione o aggiornamento di un utente
* Aggiunta o rimozione di licenze

Poiché un approccio a più livelli non utilizzano opzioni hello per la risposta agli eventi imprevisti, confronto tra tali opzioni non sono applicabili per questa attività. Verificare che, sfruttate tutte le opzioni disponibili per ogni scenario che richiede la funzionalità di creazione report toouse AD Azure come parte del processo di risposta agli eventi imprevisti della società.

## <a name="next-steps"></a>Passaggi successivi
[Determinare le attività per la soluzione ibrida di gestione delle identità](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)
