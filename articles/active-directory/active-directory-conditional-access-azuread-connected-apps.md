---
title: Accesso condizionale per le app SaaS aaaAzure | Documenti Microsoft
description: "Accesso condizionale di Azure AD consente l'accesso di tooblock possibilità di hello e si tooconfigure autenticazione a più fattori per ogni applicazione regole di accesso per gli utenti non connessi a una rete attendibile. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Introduzione all'accesso condizionale di Azure Active Directory
L'accesso condizionale di Azure Active Directory per app [SaaS](https://azure.microsoft.com/overview/what-is-saas/) e app connesse ad Azure AD consente di configurare l'accesso condizionale in base a un gruppo, una posizione e alla sensibilità dell'applicazione. 

Con l'accesso condizionale basato sulla sensibilità dell'applicazione è possibile configurare regole di accesso Multi-Factor Authentication (MFA) per ogni applicazione. Autenticazione a più fattori per ogni applicazione fornisce l'accesso tooblock di hello possibilità per gli utenti che non si trovano in una rete attendibile. È possibile applicare agli utenti tooall regole di autenticazione a più fattori che sono stati assegnati toohello applicazione o solo per gli utenti all'interno di specificati gruppi di sicurezza.  Gli utenti possono essere esclusi dal requisito di autenticazione a più fattori hello se accedono a un'applicazione hello da un indirizzo IP all'interno rete dell'organizzazione hello.

Queste funzionalità saranno disponibili toocustomers che hanno acquistato una licenza di Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Prerequisiti dello scenario
* Licenza di Azure Active Directory Premium
* Tenant di Azure Active Directory federato o gestito
* I tenant federati richiedono l'abilitazione dell'autenticazione Multi-Factor Authentication.

## <a name="configure-per-application-access-rules"></a>Configurare le regole di accesso per ogni applicazione
In questa sezione viene descritto come accedere a tooconfigure per ogni applicazione regole.

1. Accedi toohello portale di Azure classico utilizzando un account che è un amministratore globale per Azure AD.
2. Nel riquadro sinistro di hello selezionare **Active Directory**.
3. Nella scheda Directory hello, selezionare la directory.
4. Seleziona hello **applicazioni** scheda.
5. Sarà impostata per un'applicazione hello SELECT che hello regola.
6. Seleziona hello **configura** scheda.
7. Scorrere verso il basso sezione regole di accesso toohello. Selezionare una regola di accesso desiderato hello.
8. Specificare gli utenti di hello hello regola verrà applicata a.
9. Abilitare i criteri di hello selezionando **attivata toobe**.

## <a name="understanding-access-rules"></a>Informazioni sulle regole di accesso
Questa sezione viene fornita una descrizione dettagliata delle regole di accesso hello è supportato in hello accesso condizionale alle applicazioni di Azure.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Specifica gli utenti di hello hello regole si applicano all'accesso
Per impostazione predefinita i criteri di hello verranno applicati agli utenti di tooall che dispone di accesso toohello applicazione. Tuttavia, è inoltre possibile limitare hello toousers di criteri che sono membri di hello specificati gruppi di sicurezza. Hello **Aggiungi gruppo** pulsante è tooselect utilizzati uno o più gruppi dalla finestra di dialogo Selezione gruppo hello che hello regola di accesso verranno applicate a. Questa finestra di dialogo può anche essere gruppi utilizzati tooremove selezionato. Quando le regole di hello sono tooGroups tooapply selezionata, le regole di accesso hello verranno applicate solo agli utenti che appartengono tooone di hello specificato gruppi di sicurezza.

Gruppi di sicurezza possono anche essere esclusa in modo esplicito dal criterio hello selezionando hello **tranne** opzione e specificare uno o più gruppi. Gli utenti che sono membri di un gruppo di hello **tranne** elenco non è il requisito di autenticazione a più fattori di soggetto toohello, anche se sono membri di un gruppo si applica tale regola di accesso hello.
regola di accesso Hello illustrato di seguito richiederà tutti gli utenti a hello Gestioni gruppo toouse multi-factor authentication quando si accede a un'applicazione hello.

![Impostazione delle regole di accesso condizionale con MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Regole di accesso condizionale con MFA
Se un utente è stato configurato con funzionalità di autenticazione a più fattori per utente hello, questa impostazione per utente hello combinerà con regole di autenticazione a più fattori hello dell'applicazione hello. Ciò significa che un utente che è stato configurato per l'autenticazione a più fattori per utente sarà richiesto tooperform autenticazione a più fattori anche se è stato escluso dalle regole di autenticazione a più fattori applicazione hello. Altre informazioni sull'autenticazione a più fattori e le impostazioni per utente.

### <a name="access-rule-options"></a>Opzioni delle regole di accesso
è supportato Hello le opzioni seguenti:

* **Richiedere l'autenticazione a più fattori**: gli utenti di hello si applicano le regole di accesso hello toowhom, saranno necessari toocomplete autenticazione a più fattori prima che l'accesso a un'applicazione hello che hello criteri si applica a.
* **Richiedere l'autenticazione a più fattori quando non al lavoro**: un utente che proviene da un indirizzo IP attendibile non sarà necessario tooperform autenticazione a più fattori. Hello attendibili gli intervalli di indirizzi IP possono essere configurati nella pagina Impostazioni di autenticazione a più fattori hello.
* **Blocca l'accesso quando non al lavoro**: un utente che non accede da un indirizzo IP attendibile verrà bloccato. Hello attendibili gli intervalli di indirizzi IP possono essere configurati nella pagina Impostazioni di autenticazione a più fattori hello.

### <a name="setting-rule-status"></a>Impostazione dello stato delle regole
Lo stato regola di accesso consente di abilitare le regole di hello o disattivare. Quando hello le regole di accesso sono disattivate, il requisito di autenticazione a più fattori di hello non viene applicato.

### <a name="access-rule-evaluation"></a>Valutazione delle regole di accesso
Quando un utente accede a un'applicazione federata che utilizza OAuth 2.0, OpenID Connect, SAML o WS-Federation, vengono valutate le regole di accesso. Inoltre, le regole di accesso vengono valutate quando hello OAuth 2.0 e OpenID Connect utilizza un tooacquire token di aggiornamento un token di accesso. Se la valutazione dei criteri non riesce quando viene utilizzato un token di aggiornamento, hello errore **invalid_grant** verrà restituito, questo indica l'utente di hello deve toore-autenticare client toohello.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Configurare l'autenticazione a più fattori tooprovide federation services
Per i tenant federati, autenticazione a più fattori può essere eseguita da Azure Active Directory o da hello server ADFS locale.

Per impostazione predefinita, MFA viene eseguita in una pagina ospitata da Azure Active Directory. tooconfigure autenticazione a più fattori in locale, hello **-SupportsMFA** deve essere impostata troppo**true** in Azure Active Directory, mediante il modulo di hello Azure AD per Windows PowerShell.

Hello esempio seguente viene illustrato come tooenable locale autenticazione a più fattori tramite hello [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) nel tenant contoso.com hello:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

In aggiunta toosetting questo flag, hello tenant federato AD FS istanza deve essere configurato tooperform multi-factor authentication. Seguire le istruzioni di hello per [la distribuzione di Azure multi-Factor Authentication locale](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Articoli correlati
* [Protezione dell'accesso tooOffice 365 e altre App connessa tooAzure Active Directory](active-directory-conditional-access.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

