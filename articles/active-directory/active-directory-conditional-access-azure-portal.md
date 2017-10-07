---
title: aaaAzure Active Directory l'accesso condizionale | Documenti Microsoft
description: Utilizzare il controllo di accesso condizionale in Azure Active Directory toocheck per condizioni specifiche per l'autenticazione per accesso tooapplications.
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Accesso condizionale in Azure Active Directory

In un ambiente mobile-first, prima di cloud, Azure Active Directory consente di single sign-on toodevices, applicazioni e servizi da qualsiasi posizione. Proliferazione hello di dispositivi (BYOD inclusi), di operare off reti aziendali e App SaaS di terze parti 3rd, i professionisti IT devono affrontare due obiettivi opposti:

- Consentire toobe gli utenti finali di hello produttivi ovunque e
- Proteggere le risorse aziendali hello in qualsiasi momento

produttività tooimprove, Azure Active Directory fornisce agli utenti con un'ampia gamma di opzioni tooaccess risorse aziendali. Con la gestione di accesso dell'applicazione, Azure Active Directory consente solo tooensure *hello chi deve esserne informato* possono accedere alle applicazioni. Cosa accade se si desidera toohave maggiore controllo sulla modalità chi deve esserne informato hello accedono a risorse in determinate condizioni? Cosa accade se si dispone anche di condizioni in cui si desidera tooblock accesso toocertain App anche per hello *destro persone*? Ad esempio, potrebbe essere OK automaticamente se chi deve esserne informato hello accede determinate applicazioni da una rete attendibile. Tuttavia, potrebbe non desiderati tooaccess queste applicazioni da una rete che non attendibile. Per risolvere questi dubbi, è possibile usare l'accesso condizionale.

Accesso condizionale è una funzionalità di Azure Active Directory che consente di controlli tooenforce tooapps accesso hello nell'ambiente in base a condizioni specifiche. Con i controlli, è possibile collegare sia accesso toohello altri requisiti o si blocca. implementazione di Hello dell'accesso condizionale è basata sui criteri. Un approccio basato su criteri semplifica l'esperienza di configurazione in quanto segue modo hello che è valutare i requisiti di accesso.  

In genere, è necessario definire i requisiti di accesso utilizzando le istruzioni che dipendono dal modello di hello:

![Controllo](./media/active-directory-conditional-access-azure-portal/10.png)

Quando si sostituisce hello due occorrenze "*questo*" con le informazioni del mondo reale, è necessario un esempio di un'istruzione di criteri che probabilmente ha un aspetto familiare tooyou:

*Quando terzisti Cerca tooaccess nostri delle App cloud le reti non attendibili, bloccare l'accesso.*

istruzione dei criteri Hello precedente evidenzia power hello di accesso condizionale. Sebbene sia possibile attivare terzisti toobasically accedere App cloud (**che**), con accesso condizionale, è inoltre possibile definire le condizioni in cui hello è possibile accedere (**come**).

Nel contesto di hello di accesso condizionale di Azure Active Directory,

- "**Quando accade questo**" è l'**istruzione della condizione**
- "**Fare questo**" sono i **controlli**

![Controllo](./media/active-directory-conditional-access-azure-portal/11.png)

combinazione di Hello di un'istruzione con i controlli di condizione rappresenta un criterio di accesso condizionale.

![Controllo](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Controlli

In un criterio di accesso condizionale i controlli definiscono che cosa deve accadere dopo che un'istruzione della condizione è stata soddisfatta.  
Con i controlli, è possibile bloccare o consentire l'accesso con requisiti aggiuntivi.
Quando si configura un criterio che consente l'accesso, è necessario tooselect almeno un requisito.   

### <a name="grant-controls"></a>Controlli di concessione
implementazione corrente di Hello di Azure Active Directory consente hello tooconfigure requisiti di controllo delle autorizzazioni seguenti:

![Controllo](./media/active-directory-conditional-access-azure-portal/05.png)

- **Autenticazione a più fattori**: è possibile richiedere l'autenticazione avanzata tramite l'autenticazione a più fattori. I provider possono usare Azure Multi-Factor Authentication o un provider di autenticazione a più fattori locale, in combinazione con Active Directory Federation Services (AD FS). Tramite multi-factor authentication consente di proteggere le risorse da cui si accede da un utente non autorizzato potrebbe avere avuto accesso toohello le credenziali di un utente valido.

- **Un dispositivo conforme** -è possibile impostare i criteri di accesso condizionale a livello di dispositivo hello. È possibile impostare un criterio tooonly attiva i computer che sono conformi o i dispositivi mobili che sono registrati in un tooaccess di gestione di dispositivi mobili alle risorse dell'organizzazione. Ad esempio, possibile usare Intune toocheck conformità del dispositivo e quindi segnalarlo tooAzure Active Directory per l'applicazione quando l'utente hello tenta tooaccess un'applicazione. Per istruzioni dettagliate sul funzionamento toouse Intune tooprotect App e dati, vedere [proteggere App e dati con Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). È inoltre possibile utilizzare la protezione dei dati tooenforce Intune per dispositivi smarriti o rubati. Per altre informazioni, vedere [Proteggere i dati con la cancellazione completa o selettiva tramite Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Dispositivi aggiunti a un dominio** : È possibile richiedere dispositivo hello utilizzati tooyour appartenenti a un dominio Active Directory toobe di tooconnect tooAzure locale Active Directory (AD). Questi criteri si applicano tooWindows desktop, portatili e Tablet enterprise. 

Se si dispone di più controlli selezionati, è possibile inoltre configurare se tutti gli elementi sono richiesti quando viene elaborato il criterio.

![Controllo](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Controlli di sessione
I controlli di sessione consentono di limitare l'esperienza in un'app cloud. i controlli di sessione Hello vengono applicati da applicazioni basate su cloud e si basano su informazioni aggiuntive fornite dall'app di Azure AD toohello sulla sessione hello.

![Controllo](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Usa restrizioni imposte dalle app
È possibile utilizzare questo controllo toorequire AD Azure toopass hello dispositivo informazioni toohello app cloud. In questo modo app cloud hello sapere se l'utente hello proviene da un dispositivo conforme o di un dispositivo aggiunto a un dominio. Questo controllo è attualmente supportata solo con SharePoint come app cloud hello. SharePoint utilizza hello dispositivo informazioni tooprovide gli utenti un'esperienza completa o limitata a seconda dello stato del dispositivo hello.
passare toolearn ulteriori informazioni sulla modalità di accesso con SharePoint, limitato toorequire [qui](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Istruzione della condizione

la sezione precedente di Hello ha introdotto toosupported opzioni tooblock o limitare l'accesso alle risorse tooyour in forma di controlli. In un criterio di accesso condizionale, è definire i criteri di hello necessari toobe soddisfatti per toobe i controlli applicati in forma di un'istruzione di condizione.  

È possibile includere hello seguendo le assegnazioni nell'istruzione della condizione:

![Controllo](./media/active-directory-conditional-access-azure-portal/07.png)


- **Chi** -In molti casi, si desidera il set specifico di tooa toobe applicare controlli di utenti. In un'istruzione di condizione, è possibile definire questo set selezionando gli utenti di hello e il criterio si applica ai gruppi. Se necessario, è anche possibile escludere in modo esplicito un set di utenti dal criterio esentandoli.  
Selezionando gli utenti e gruppi, definire ambito hello di utenti a che i criteri si applicano.    

    ![Controllo](./media/active-directory-conditional-access-azure-portal/08.png)



- **Che cosa**: di solito nel proprio ambiente vengono eseguite alcune app che, dal punto di vista della protezione, richiedono più attenzione di altre, Questo interessa, ad esempio, le app che hanno accesso ai dati toosensitive.
Se si seleziona App cloud, è definire l'ambito di hello delle applicazioni cloud, a che il criterio si applica. Se necessario, è anche possibile escludere in modo esplicito un set di app dal criterio.

    ![Controllo](./media/active-directory-conditional-access-azure-portal/09.png)


- **Come** - come accesso tooyour App viene eseguita in condizioni è possibile controllare, è possibile che non sia necessario per l'imposizione di controlli aggiuntivi in modalità App cloud accessibili dagli utenti. Tuttavia, operazioni potrebbero essere diverse se viene eseguita App cloud tooyour di accesso, ad esempio, le reti non attendibili o i dispositivi non conformi. In un'istruzione di condizione, è possibile definire determinate condizioni di accesso che dispongono di requisiti aggiuntivi per la modalità di accesso tooyour app.

    ![Condizioni](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Condizioni

Nell'implementazione corrente di hello di Azure Active Directory, è possibile definire le condizioni per hello seguenti aree:

- Rischio di accesso
- Piattaforme del dispositivo
- Località
- App client

![Condizioni](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Rischio di accesso

Il rischio di accesso è un oggetto che viene utilizzato per la probabilità di Azure Active Directory tootrack hello che un tentativo di accesso non è stato eseguito dal legittimo proprietario di hello di un account utente. In questo oggetto, probabilità hello (alta, Media o bassa) vengono memorizzate in forma di un attributo denominato [livello di rischio Accedi](active-directory-reporting-risk-events.md#risk-level). L'oggetto viene generato durante l'accesso di un utente se vengono rilevati rischi di accesso da Azure Active Directory. Per informazioni dettagliate, vedere [Accessi a rischio](active-directory-identityprotection.md#risky-sign-ins).  
È possibile utilizzare un livello di rischio Accedi hello calcolato come condizione nei criteri di accesso condizionale. 

![Condizioni](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Piattaforme del dispositivo

piattaforma del dispositivo Hello è caratterizzata dal sistema operativo hello in cui è in esecuzione nel dispositivo:

- Android
- iOS
- Windows Phone
- Windows
- macOS (anteprima). 

![Condizioni](./media/active-directory-conditional-access-azure-portal/02.png)

È possibile definire piattaforme per dispositivi hello inclusi nonché piattaforme per dispositivi che sono esentate dai criteri.  
piattaforme per dispositivi toouse criteri hello, prima modifica hello configurare gli elementi Toggle troppo**Sì**, quindi selezionare tutti o dispositivo singole piattaforme hello criterio si applica a. Se si selezionano le piattaforme per singoli dispositivi, criteri hello influisce solo su queste piattaforme. In questo caso, le piattaforme supportate tooother accessi non sono interessate dal criterio hello.


### <a name="locations"></a>Località

Hello posizione viene identificata dall'indirizzo IP di hello del client hello utilizzati tooconnect tooAzure Active Directory. Questa condizione richiede toobe familiarità con **denominato percorsi** e **autenticazione a più fattori di indirizzi IP attendibili**.  

**Posizioni denominate** è una funzionalità di Azure Active Directory che consente di intervalli di indirizzi IP attendibili toolabel le organizzazioni. Nell'ambiente in uso, è possibile utilizzare posizioni denominate contesto hello di rilevamento hello di [gli eventi di rischio](active-directory-reporting-risk-events.md) nonché l'accesso condizionale. Per altre informazioni sulla configurazione delle località denominate in Azure Active Directory, vedere [Località denominate in Azure Active Directory](active-directory-named-locations.md).

numero di Hello delle posizioni che è possibile configurare è limitato dalle dimensioni hello dell'oggetto correlato hello in Azure AD. È possibile configurare:
 
 - Una posizione denominata con degli intervalli IP too500
 - Un massimo di 60 alle posizioni (anteprima) con un intervallo IP assegnati tooeach di essi 


**Autenticazione a più fattori di indirizzi IP attendibili** è una funzionalità di autenticazione a più fattori che consente di intervalli di indirizzi IP attendibili toodefine che rappresenta la intranet locale dell'organizzazione. Quando si configurano un condizioni di percorso, gli indirizzi IP attendibili permette toodistinguish tra le connessioni effettuate da tutti gli altri percorsi e di rete dell'organizzazione. Per altre informazioni, vedere [Indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



È possibile includere tutte le località o tutti gli IP attendibili ed escludere tutti gli IP attendibili.

![Condizioni](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>App client

app client Hello può essere in un'app di Windows hello livello generico (browser web, app per dispositivi mobili, desktop client) è stato utilizzato tooconnect tooAzure Active Directory o in particolare è possibile selezionare Exchange Active Sync.  
Autenticazione legacy si riferisce tooclients utilizzando l'autenticazione di base, ad esempio client meno recenti di Office che non utilizzano l'autenticazione moderna. L'accesso condizionale non è attualmente supportato con l'autenticazione legacy.

![Condizioni](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Scenari comuni

### <a name="requiring-multi-factor-authentication-for-apps"></a>Richiesta dell'autenticazione a più fattori per le app

Molti ambienti dispongono di applicazioni che richiedono un livello di protezione maggiore rispetto a hello ad altri utenti.
Questo accade, ad esempio, hello per le applicazioni che dispongono di accesso toosensitive dati.
Se si desidera tooadd un ulteriore livello di protezione toothese App, è possibile configurare un criterio di accesso condizionale che richiede l'autenticazione a più fattori quando gli utenti accedono a tali app.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Richiesta dell'autenticazione a più fattori per l'accesso da reti non considerate attendibili

Questo scenario consente simile toohello precedente perché aggiunge un requisito per l'autenticazione a più fattori.
Tuttavia, la differenza principale hello è condizione hello per questo requisito.  
Durante lo stato attivo hello dello scenario precedente hello per le app con accesso ai dati toosensitve, hello di questo scenario è attiva percorsi attendibili.  
In altre parole, è possibile avere un requisito per l'autenticazione a più fattori se un'app è accessibile a un utente da una rete non considerata attendibile.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Solo i dispositivi attendibili possono accedere ai servizi di Office 365

Se si usa Intune nel proprio ambiente, è possibile avviare immediatamente usando l'interfaccia di criteri di accesso condizionale hello nella console di Azure hello.

Molti clienti di Intune usano tooensure di accesso condizionale che solo i dispositivi attendibili possono accedere ai servizi di Office 365. Ciò significa che i dispositivi mobili registrati con Intune e che soddisfano i requisiti di conformità e che i PC Windows sono dominio locale tooan unita in join. Dei miglioramenti principali è che non sia tooset hello stesso criterio per ognuno dei servizi di Office 365 hello.  Quando si crea un nuovo criterio, è possibile configurare hello Cloud App tooinclude ogni delle app di Office 365 hello che si desidera tooprotect con accesso condizionale.

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooknow tooconfigure criteri di accesso condizionale, vedere [iniziare con l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Se si è pronti tooconfigure criteri di accesso condizionale per l'ambiente, vedere hello [procedure consigliate per l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-best-practices.md). 
