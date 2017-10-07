---
title: "i dati personali aaaProtect con controlli di identità e accessi Azure | Documenti Microsoft"
description: "Tramite Azure toohelp di controlli di identità e accessi proteggere i dati personali"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory e Multi-Factor Authentication: proteggere i dati personali usando l'identità e i controlli di accesso

Questo articolo fornisce informazioni e procedure che è possibile utilizzare i dati personali a tooprotect usando i servizi e funzionalità di sicurezza di autenticazione di Azure Active Directory e a più fattori.

## <a name="scenario"></a>Scenario

Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico. toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito 

la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello. Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale, Include inoltre informazioni sulle risorse umane di tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni. riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.

Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio hello aziendali presenti in ogni HelloWorld hanno accesso alle risorse aziendali toosome.

## <a name="problem-statement"></a>Presentazione del problema

società Hello devono proteggere privacy hello dei dati personali dei dipendenti e clienti da utenti malintenzionati tentando di accedere toogain di identità toouse compromesso. È inoltre necessario verificare che toopersonal di accesso ai dati in base agli utenti legittimi sono limitati solo a quelli che ne hanno bisogno toodo i processi.

## <a name="company-goal"></a>Obiettivo dell'azienda

obiettivo della società Hello è tooensure che accedono ai dati toopersonal è rigorosamente controllate. È essenziale che le identità degli utenti con accesso ai dati toopersonal sia protetta da autenticazione avanzata. Un criterio di [privilegio minimo] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) deve essere applicata in modo che solo livello hello di accesso necessarie, non di più utenti autorizzati.

## <a name="solutions"></a>Soluzioni

Microsoft Azure offre gli strumenti di gestione delle identità e accessi toohelp società chi ha accesso tooresources che contengono dati personali.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gestisce le identità e controlla l'accesso tooAzure così come altri locali e altre risorse cloud, dati e applicazioni. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) aiuta gli amministratori di Azure toominimize hello numerose persone che hanno accesso toocertain informazioni quali dati personali. Consente loro toodiscover, limitare e monitorare le identità con privilegi e i relativi tooresources e tooassign temporaneo,-Time (JIT) diritti amministrativi tooeligible gli utenti di accesso. Consente anche di ottenere informazioni su coloro che hanno privilegi amministrativi di AAD.

le attività di Hello relativi all'utilizzo di AAD PIM includono:

- Abilitazione di Privileged Identity Management per la directory

- Utilizzando Gestione identità con privilegi amministratore dashboard toosee importanti informazioni a colpo d'occhio

- La gestione delle identità con privilegiata hello (amministratori) aggiungendo o rimuovendo ruolo tooeach amministratori permanenti o idonei

- Configurazione delle impostazioni di attivazione di hello ruolo

- Attivazione dei ruoli

- Verifica dell'attività dei ruoli

#### <a name="how-do-i-enable-aad-pim"></a>Come abilitare Azure Active Directory Privileged Identity Management

usare PIM per la directory, toostart hello seguenti:

1. Accedi toohello portale di Azure come amministratore globale della directory.

2. Se l'organizzazione dispone di più di una directory, selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure. Selezionare la directory di hello in cui si userà Azure AD Privileged Identity Management.

3. Selezionare **più servizi** e utilizzare hello **filtro** toosearch casella di testo per Azure AD Privileged Identity Management.

4. Controllare **Pin toodashboard** e quindi fare clic su **crea**. verrà visualizzata la finestra di Hello applicazione Privileged Identity Management.

Una volta configurato, Azure AD Privileged Identity Management vedrai il pannello di navigazione hello ogni volta che si apre un'applicazione hello.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Per altre informazioni e istruzioni su come iniziare a usare Azure Active Directory Privileged Identity Management, vedere [Iniziare ad usare Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started).

### <a name="azure-role-based-access-control"></a>Controllo degli accessi in base al ruolo di Azure

[Controllo di accesso basato sui ruoli Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) aiuta gli amministratori di Azure a gestire tooAzure di accedere alle risorse abilitazione hello concessione dell'accesso in base a hello assegnato il ruolo utente. È possibile separare i compiti all'interno di un team e concedere solo hello quantità di accesso toousers, gruppi e le applicazioni che devono tooperform i processi.

È possibile concedere accesso basato sui ruoli toousers utilizzando hello portale di Azure, gli strumenti da riga di comando di Azure o le API di gestione di Azure.

Per ulteriori informazioni sui concetti di base sui ruoli di Azure, vedere [introduzione Role-Based Access Control in hello portale di Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Come gestire il controllo degli accessi in base al ruolo con PowerShell

È possibile utilizzare i cmdlet di PowerShell toomanage RBAC di Azure, tra cui hello seguenti attività di gestione:

- Elenco dei ruoli

- Assegnazioni di accesso

- Concedere l'accesso

- Rimuovere un accesso

- Creare un ruolo personalizzato

- Ottenere le azioni per un provider di risorse

- Modificare un ruolo personalizzato

- Eliminare un ruolo personalizzato

- Elencare ruoli personalizzati

Per istruzioni su come toomanage RBAC Azure con PowerShell, vedere [basata sui ruoli di gestione accesso con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) è una soluzione di verifica in due fasi che consente di salvaguardare accesso toodata e applicazioni, rispettando la richiesta dell'utente per un semplice processo. Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.

toodeploy autenticazione a più fattori in hello cloud di Azure, è necessario toofirst attivarla e quindi attivare la verifica in due passaggi per gli utenti.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Come abilitare toouse Azure MFA?

Se gli utenti hanno le licenze che includono Azure multi-Factor Authentication, non è necessario che è necessario tooturn toodo su Azure MFA. In caso contrario, è necessario un provider multi-Factor Authentication toocreate nella directory. toodo, seguire questi passaggi:

1. Selezionare **Active Directory** in hello portale di Azure classico (connesso come amministratore).

2. Selezionare **Provider di Multi-Factor Authentication**.

3. Selezionare **Nuovo** e quindi **Provider di Multi-Factor Authentication** in **Servizi app**.

4. Selezionare **Creazione rapida**.

5. Compilare il campo di nome hello e selezionare un modello di utilizzo (per l'autenticazione o per utente abilitato).

6. Designare una directory a cui hello è associato il Provider di autenticazione a più fattori.

7. Fare clic su hello **crea** pulsante.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Per altre istruzioni su come toomanage Provider multi-Factor Authentication, vedere [Introduzione a un Provider di Azure multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Come attivare la verifica in due passaggi per gli utenti

È possibile applicare la verifica in due passaggi per accessi tutti o solo quando si verificano condizioni specifiche, è possibile creare verifica in due passaggi toorequire criteri di accesso condizionale.

L'abilitazione di autenticazione a più fattori di Azure, modificare stati utente è l'approccio tradizionale hello per la richiesta di verifica in due passaggi. Tutti gli utenti di hello che abiliti hello verifica in due passaggi di stesso requisito tooperform ogni volta che effettuano l'accesso. L'abilitazione di un utente sostituisce eventuali criteri di accesso condizionale in vigore per l'utente.

L'abilitazione di Azure MFA con criteri di accesso condizionale è un approccio più flessibile per richiedere la verifica in due passaggi. È possibile creare criteri di accesso condizionale che si applicano toogroups, nonché a singoli utenti. È possibile, ad esempio, assegnare ai gruppi ad alto rischio più restrizioni rispetto ai gruppi a basso rischio oppure richiedere la verifica in due passaggi solo per le app cloud ad alto rischio e non per quelle a basso rischio. L'accesso condizionale è tuttavia una funzionalità a pagamento di Azure Active Directory.

hello tooenable MFA modificando lo stato utente seguenti:

1. Accedi toohello portale di Azure come amministratore.
2. Andare troppo**Azure Active Directory \> utenti e gruppi \> tutti gli utenti**.
3. Selezionare **Multi-Factor Authentication**.
4. Trova hello utente che si desidera tooenable per Azure MFA. Potrebbe essere necessario toochange hello visualizzazione nella parte superiore di hello.
5. Controllare nome hello casella Avanti toohello dell'utente.
6. Sulla destra, nella casella rapide hello, scegliere **abilitare**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Confermare la selezione nella finestra popup di hello visualizzata.  Gli utenti per cui è stata abilitata l'autenticazione a più fattori verranno chiesto hello tooregister successivo che accesso.

tooenable Azure MFA con un criterio di accesso condizionale, hello seguenti:

1. Accedi toohello portale di Azure come amministratore.

2. Andare troppo**Azure Active Directory \> accesso condizionale**.

3. Selezionare **Nuovi criteri**.

4. In **Assegnazioni** selezionare **Utenti e gruppi**. Hello utilizzare **Include** e **escludere** schede toospecify quali utenti e gruppi verranno gestiti da criteri hello.

5. In **Assegnazioni** selezionare **App cloud**. Scegliere troppo**includono tutte le app cloud**.
6.  In **Controlli di accesso** selezionare **Concedi**. Selezionare **Richiedi autenticazione a più fattori**.
7.  Attivare **abilitare i criteri di** troppo**su** e quindi selezionare **salvare**.

Per informazioni su come tooset le impostazioni di autenticazione a più fattori di Azure tooconfigure di avvisi di illecito, creare un bypass monouso, utilizzare i messaggi vocali personalizzati, configurare la memorizzazione nella cache, specificare indirizzi IP attendibili, creare password dell'app, abilitare la memorizzazione di autenticazione a più fattori per i dispositivi che gli utenti attendibili, selezionare metodi di verifica, vedere [configurare impostazioni di Azure multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Passaggi successivi

- [Protezione dell'accesso con privilegi in Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Domande frequenti su Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Risoluzione dei problemi del controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
