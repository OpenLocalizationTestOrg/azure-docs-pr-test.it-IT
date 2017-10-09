Le organizzazioni usano più applicazioni [Software as a Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) per la produttività in quanto la tecnologia e gli strumenti cloud stanno diventando sempre più disponibili. Man mano che aumenta il numero di hello di App SaaS, diventa difficile per gli account toomanage gli amministratori di hello e diritti di accesso e per le password diversi hello tooremember gli utenti. Gestire singolarmente queste applicazioni richiede un impegno aggiuntivo ed è meno sicuro.

* Dipendenti con tookeep tenere traccia del numero di password tendono toouse meno sicure tooremember metodi li, annotare le password o utilizzando hello stesse password tra numero di account.
* Quando arriva un nuovo dipendente o un dipendente esistente lascia l'organizzazione, è necessario eseguire il provisioning o deprovisioning di tutti i relativi account singolarmente.
* Inoltre, i dipendenti possono iniziare a utilizzare App SaaS per il proprio lavoro senza passare attraverso IT, vale a dire che creano i propri account nei sistemi in cui gli amministratori IT di hello non sono state approvate e non sono di monitoraggio.  

Una soluzione per tutti questi problemi è l'accesso Single Sign-On (SSO). È hello più App toomanage modo più semplice e offrono agli utenti un'esperienza coerenza sign-on. Azure Active Directory (Azure AD) offre una soluzione SSO efficace e ha molte applicazioni preintegrate disponibili, con le esercitazioni per gli amministratori tooquickly consente di impostare una nuova app e avviare provisioning utenti.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Come vengono integrate le app in Azure Active Directory?
Azure AD consente toointegrate le App e il provisioning degli account. Questa operazione può essere eseguita tramite due approcci.

* Se app hello è pre-integrato nell'app hello raccolta, è possibile scorrere tale portale tooset di App e configurare le impostazioni di hello tooallow SSO. Per qualsiasi raccolta app, è possibile iniziare da seguire hello semplici istruzioni presentate nella raccolta di app hello e hello tooenable portale Azure accesso single sign-on.
* Se l'applicazione hello non è presente nella raccolta di hello, ancora impostare la maggior parte delle applicazioni in Azure AD come un'app personalizzata. Questa operazione richiede leggermente più tecniche tooconfigure competenze. È possibile aggiungere qualunque applicazione che supporta SAML 2.0 come applicazione federata o qualunque applicazione che dispone di una pagina di accesso basata su HTML come applicazione Single Sign-On con password.

Hello caso in cui gli utenti hanno creato i propri account per le app SaaS che non sono gestite dal reparto IT, hello [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) strumento offre una soluzione. Questo strumento consente di monitorare hello web traffico tooidentify quali App vengono utilizzate in tutta l'organizzazione hello e hello numero di utenti che utilizzano ognuno di essi. IT possono utilizzare questo toolearn informazioni degli utenti a cui hello App Preferiti e decidere quali toointegrate in Azure AD per SSO.  

Quando si integra un'app in Azure AD, è possibile eseguire il mapping stabilita identità tootheir rispettivi AD Azure le identità delle applicazioni degli utenti hello.  

