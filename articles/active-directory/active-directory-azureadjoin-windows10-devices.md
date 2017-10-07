---
title: i dispositivi Windows 10 aaaUsing nell'area di lavoro | Documenti Microsoft
description: "Fornisce uno snapshot delle funzionalità per utenti e IT, contrasto hello modi un dispositivo può essere eseguito il provisioning e utilizzato in un'organizzazione con Windows 10."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Uso di dispositivi Windows 10 in azienda
Si applica a: PC Windows 10

Windows 10 offre tre modelli per le organizzazioni che consentono agli utenti tooaccess alle risorse di lavoro in modo sicuro e pratico.

* **Azure Active Directory Join** (aggiunta di Azure AD), per accedono alle risorse, ad esempio Office 365 principalmente nel cloud di hello i lavoratori. Aggiunta ad Azure AD è un'esperienza di provisioning aziendale self-service che costituisce una novità di Windows 10.
* **Aggiunta a un dominio**, per le organizzazioni che hanno investito in risorse e app locali. Aggiunta a un dominio offre un'esperienza migliorata in Windows 10, quando si è connessi AD tooAzure.
* **Un nuovo semplificata l'esperienza BYOD**per gli utenti che desiderano un lavoro tooadd account o dell'istituto di istruzione tooWindows e accedere facilmente alle risorse dispositivi personali.

Hello nella tabella seguente presenta uno snapshot delle funzionalità per utenti e amministratori IT, contrasto hello modi un dispositivo può essere eseguito il provisioning e utilizzato in un'organizzazione con Windows 10:

|  | Aggiunta a un dominio | Aggiunta ad Azure AD | Dispositivo personale |
| --- | --- | --- | --- |
| Accesso a un dispositivo Windows per gli account aziendali o dell'istituto di istruzione. |Sì |Sì |No |
| Utente single sign-on (SSO) tooOffice 365 e App di Azure AD. SSO è toosign possibilità hello in una sola volta tooaccess di risorse dell'organizzazione. |Sì |Sì |Sì |
| Utente SSO tooKerberos/NTLM app. |Sì |Limitato |Sì, tramite VPN |
| Autorizzazione avanzata e pratico accesso all'account aziendale o dell'istituto di istruzione con Microsoft Passport e Windows Hello. |Sì |Sì |Sì |
| Accedere all'archivio di Windows tooenterprise con un account aziendale o dell'istituto di istruzione (non un account Microsoft). |Sì |Sì |Sì |
| Roaming delle impostazioni utente tra dispositivi conforme ai criteri dell'organizzazione con account aziendali o dell'istituto di istruzione. |Sì |Sì |Sì |
| Hello possibilità toorestrict accesso tooorganizational App toodevices che sono conformi ai criteri aziendali di dispositivo. |Sì |Sì |Sì |
| Provisioning self-service per gli utenti di dispositivi per lavorare da qualsiasi luogo. |No |Sì |Sì |
| Dispositivi toomanage possibilità. |Sì, tramite Criteri di gruppo/SCCM |Sì |Sì |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Uso di dispositivi aziendali con Aggiunta ad Azure AD e aggiunta a un dominio in Windows 10
Windows 10 offre due modi per le risorse di lavoro di dispositivi di proprietà lavoro tooaccess:

* Aggiunta ad Azure AD
* Aggiunta a un dominio
  
  Sono entrambe valide opzioni, a seconda delle esigenze e dei requisiti dell'organizzazione. In alcuni casi, le organizzazioni possono sfruttare i vantaggi derivanti dall'abilitazione di entrambi i metodi di distribuzione.

## <a name="when-toouse-azure-active-directory-join"></a>Quando toouse Azure Active Directory Join
Aggiunta ad Azure AD è una nuova esperienza di provisioning aziendale self-service di Windows 10.  È destinato al thread che accedono alle risorse di lavoro, ad esempio Office 365 principalmente nel cloud di hello. È un modo semplice di tooconfigure Tablet, computer e telefoni per enterprise hello. Fa uso della gestione di dispositivi mobili, che garantisce controlli coerenti nelle piattaforme Windows.

**Usare Aggiunta ad Azure AD nei casi seguenti**:

* Si desidera tooenable hello provisioning self-service di dispositivi per visitare il thread di lavoro nell'hello.
* Si forniscono agli utenti dispositivi mobili aziendali, ad esempio tablet e telefoni.
* Si desidera toomanage un set di utenti in Azure Active Directory anziché in Active Directory, ad esempio gli studenti, collaboratori o stagionali.
* Si desidera tooprovide tooworkers funzionalità di unione nelle succursali remote con l'infrastruttura locale limitato.
* Non si ha un'istanza di Active Directory locale.

Alcune organizzazioni userà aggiunta ad Azure AD come hello modalità principale toodeploy lavoro dispositivi di proprietà, in particolare quando essi migrare la maggior parte o tutti i cloud toohello risorse. Le organizzazioni ibrida con Active Directory e Azure AD anche possono scegliere toodeploy un metodo o un altro in base a utente hello o un reparto.

Distretti scolastici e università, ad esempio, possono gestire il personale di Active Directory e gli studenti in Azure AD. Alcune società potrebbe essere necessario toomanage filiali o i reparti vendite in Azure AD. In un'organizzazione ibrida è possibile usare entrambi i metodi, Aggiunta ad Azure AD e aggiunta a un dominio. Aggiunta ad Azure AD può essere un join di toodomain complemento ideale per la distribuzione di dispositivi in un ambiente di lavoro.

**Se hello più normale accesso tooenterprise alle risorse tramite cloud hello, l'organizzazione potrebbe sfruttare i vantaggi aggiuntivi se**:

* È possibile rimuovere le dipendenze dall'infrastruttura di identità locale.
* È possibile semplificare il modello di distribuzione dei dispositivi evitando le soluzioni di creazione dell'immagine consentendo la configurazione self-service.
* È possibile utilizzare tutti i dispositivi toomanage di gestione di dispositivi mobili su varie piattaforme.

Per ulteriori informazioni sull'aggiunta di Azure AD, vedere [estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Quando aggiunta a un dominio toouse (o continuare a utilizzarlo)
Per hello ultimi 15 anni, molte organizzazioni sono utilizzati dispositivi lavoro tooconnect join di un dominio. Consente agli utenti toosign nei dispositivi tootheir con Active Directory di lavoro o scuola account. Aggiunta a un dominio consente inoltre di toocentrally IT e gestire completamente questi dispositivi. Le organizzazioni si basano su metodi tooprovision periferiche e spesso utilizzano toomanage System Center Configuration Manager (SCCM) o criteri di gruppo (GP) li.

**L'organizzazione dovrebbe usare o continuare a usare l'aggiunta a un dominio nei casi seguenti**:

* Sono Win32 App distribuito toothese dispositivi che utilizzano l'autenticazione NTLM o Kerberos.
* È necessario che i dispositivi toomanage criteri di gruppo o SCCM/DCM.
* Si desidera toocontinue toouse imaging soluzioni tooconfigure dispositivi per i dipendenti.

**Aggiunta a un dominio Windows 10 offre inoltre i vantaggi seguenti hello quando connesso AD tooAzure**:

* Autenticazione avanzata associata a dispositivo e pratico accesso all'account aziendale o dell'istituto di istruzione con Microsoft Passport e Windows Hello.
* Accedere a toohello enterprise, Windows Store per i dispositivi che utilizzano lavoro o scuola account (necessari account di Microsoft).
* Roaming delle impostazioni utente tra dispositivi conforme ai criteri dell'organizzazione usando account aziendali o dell'istituto di istruzione, non è necessario un account Microsoft.
* Hello possibilità toorestrict accesso tooorganizational App toodevices che sono conformi ai criteri aziendali di dispositivo.

Per ulteriori informazioni sull'aggiunta di Azure AD, vedere [estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Abilitare l'aggiunta di dispositivi personali per il lavoro o lo studio
toosupport BYOD in enterprise hello, Windows 10 offre hello utente hello possibilità tooadd un lavoro o computer tootheir di scuola account, tablet o telefono. Dopo aver hello utente aggiunge un lavoro o account, dispositivo hello è registrato con Azure AD e facoltativamente registrati nel sistema di gestione di dispositivi mobili hello hello organizzazione è stata configurata. directory Hello risulteranno questi dispositivi vs 'Registrato'. come aggiunti ad Azure AD. Gli amministratori IT possono applicare criteri diversi in base a queste informazioni, offrendo un approccio più semplice per un dispositivo personale rispetto a un dispositivo aziendale, se necessario.

Gli utenti possono aggiungere un lavoro o dell'istituto di istruzione in modo molto dispositivo personale tootheir di account. È possibile farlo quando si accede a un'applicazione di lavoro per hello prima volta, o possono farlo manualmente tramite il menu di impostazioni hello. Questo account fornirà le risorse tooorganizational SSO.

Per ulteriori informazioni sull'aggiunta di Azure AD, vedere [connessione tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienze](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Abilitare l'aggiunta a un dominio o Aggiunta ad Azure AD
Tutti i metodi descritti in precedenza (Aggiungi aggiunta al dominio e aggiunta ad Azure AD di lavoro o scuola account) dispone di punti di ingresso nell'esperienza utente hello Windows 10. Tuttavia, una funzionalità di hello tooenable amministratore IT nell'infrastruttura hello tutti richiedono prima di eseguire analisi hello.

## <a name="requirements-for-deploying-azure-ad-join"></a>Requisiti per la distribuzione di Aggiunta ad Azure AD
toodeploy aggiunta ad Azure AD per qualsiasi set di utenti, è necessario hello seguenti:

* Una sottoscrizione di Azure AD.
* Una sottoscrizione di Azure AD Premium, ad esempio la registrazione per la gestione di dispositivi mobili automatica, se sono necessarie altre funzionalità.
* Gestione dei dispositivi mobili, ad esempio, una sottoscrizione di Microsoft Intune, gestione dei dispositivi mobili per Office 365 o uno qualsiasi dei fornitori di gestione con i dispositivi mobili partner hello che si integrano con Azure AD. (Vedere hello [sezione Domande frequenti](#frequently-asked-questions) verso la fine hello di questo articolo per altre informazioni).

Se le funzionalità ibride, è consigliabile distribuire Azure AD Connect tooextend hello locale directory tooAzure Active Directory.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Requisiti per l'uso dell'aggiunta a un dominio con Azure AD
Aggiunta a un dominio continua toowork perché sono sempre associati. Tuttavia, i vantaggi di Azure AD hello tooget sarà necessario hello seguenti:

* Una sottoscrizione di Azure AD.
* Una distribuzione di Azure AD Connect tooextend hello locale tooAzure di directory Active Directory.
* Un criterio che consenta di tooAzure di accesso condizionale toohave dispositivi appartenenti a un dominio Active Directory.
* Un criterio che consente l'accesso ai dispositivi troppo "dominio" Se si desidera toobe toorestrict in grado di accedere per alcuni dispositivi.
* System Center Configuration Manager versione 1509 per Technical Preview, tooenable regole per la richiesta di dispositivi conformi. (Vedere la documentazione di TechNet hello e post di blog).

Per ulteriori informazioni sull'aggiunta a un dominio Windows 10, vedere [connessione tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienze](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Requisiti per l'uso di BYOD con l'opzione Aggiungi un account aziendale o dell'istituto di istruzione
tooenable "bring your own device" (BYOD) con gli account aziendali o dell'istituto di istruzione, sono necessari i seguenti elementi di hello:

* Una sottoscrizione di Azure AD.
* Una sottoscrizione di Azure AD Premium, ad esempio la registrazione per la gestione di dispositivi mobili automatica, se sono necessarie altre funzionalità.

## <a name="requirements-for-using-microsoft-passport"></a>Requisiti per l'uso di Microsoft Passport
tooenable Microsoft Passport, sarà necessario seguente hello:

* Un'infrastruttura a chiave pubblica (PKI) per il supporto dell'autenticazione basata su certificati che usa Microsoft Passport.
* Una sottoscrizione di Intune per il supporto dell'autenticazione basata su certificati che usa Microsoft Passport per l'aggiunta ad Azure AD e gli account aziendali o dell'istituto di istruzione.
* System Center Configuration Manager versione 1509 per Technical Preview (vedere la documentazione di TechNet hello e post di blog) per il supporto dell'autenticazione basata su certificati che utilizza Microsoft Passport per l'aggiunta al dominio.
* Criteri per l'abilitazione di Microsoft Passport organizzazione hello.

Come un'alternativa toousing un'infrastruttura PKI, è possibile abilitare Microsoft Passport basato su chiave eseguendo hello seguenti:

* Distribuzione di controller di dominio di Windows Server 2016 "Production Preview 1". Non è necessario alcun livello di funzionalità del dominio o della foresta. Saranno sufficienti vari controller di dominio per la ridondanza per ogni sito Active Directory.
* Impostare criteri tooenable Microsoft Passport hello organizzazione.

Per altre informazioni su Microsoft Passport e Windows Hello in Windows 10, vedere <link-to-MS-Passport-and-Windows-Hello-document>.

## <a name="frequently-asked-questions"></a>Domande frequenti
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Quali prodotti partner di gestione di dispositivi mobili si integrano con Azure AD?
Hello seguenti prodotti fornitore integrano con Azure AD per la registrazione unificata e l'accesso condizionale in Windows 10:

* AirWatch di VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* Gestione di dispositivi mobili locale SOTI
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Come funziona Aggiunta all'area di lavoro in Windows 10?
Area di lavoro è stato utilizzato in Windows 8.1 tooenable BYOD. In Windows 10 BYOD viene abilitato tramite l'opzione Aggiungi un account aziendale o dell'istituto di istruzione, come illustrato in precedenza. Per le organizzazioni che non si integrano la gestione dei dispositivi mobili con Azure AD, gli utenti possono registrare dispositivi hello in Gestione manualmente tramite **impostazioni** > **account**  >  **Accesso società**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Gli utenti connettersi all'account di dominio tootheir account Microsoft in Windows 10?
Non in Windows 10. In Windows 8.1, gli utenti dei dispositivi appartenenti a un dominio potrebbero "connettersi" loro tooenable account di dominio di Microsoft account (ad esempio, Hotmail, Live, Outlook, Xbox, e così via) tootheir alcune esperienze quali SSO tooLive servizi, utilizzo di Windows Store hello e mobili impostazioni utente tra i dispositivi. In Windows 10, hello account Microsoft "connect" funzionalità è stata ritirata. utente Hello è possibile aggiungere uno o più account Microsoft come account aggiuntivi tooenable SSO tooconsumer servizi, ad esempio hello Windows Store. Questa operazione viene eseguita in **Impostazioni** > **Account** > **Il tuo account**.

Gli utenti che eseguono l'aggiornamento da dispositivi appartenenti a un dominio di Windows 8.1 e che ha eseguito la connessione all'account Microsoft, verrà automaticamente all'account Microsoft collegati aggiunti toohello elenco di account aggiuntivi che utilizzano.

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

