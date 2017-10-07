---
title: 'Azure Active Directory Domain Services: sincronizzazione nei domini gestiti | Documentazione Microsoft'
description: Informazioni sulla sincronizzazione in un dominio gestito di Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Sincronizzazione in un dominio gestito di Azure Active Directory Domain Services
Hello diagramma seguente illustra come funziona la sincronizzazione in servizi di dominio Active Directory di Azure domini gestiti.

![Topologia della sincronizzazione in Azure Active Directory Domain Services](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Sincronizzazione dal tenant tooyour Azure Active directory locale
Sincronizzazione di Azure AD Connect sia gli account utente utilizzato toosynchronize, appartenenza al gruppo e tenant di tooyour AD Azure gli hash delle credenziali. Gli attributi dell'utente account, ad esempio hello UPN e locale vengono sincronizzate sicurezza (SID). Se si utilizzano servizi di dominio Active Directory di Azure, gli hash delle credenziali legacy richiesto per l'autenticazione NTLM e Kerberos sono tenant di Azure AD sincronizzati tooyour.

Se si configura il writeback, modifiche che si verificano nella directory di Azure AD vengono sincronizzate tooyour indietro Active Directory locale. Ad esempio, se si modifica la password con le funzionalità di modifica della password self-service di Azure AD, la password modificata hello viene aggiornata in locale il dominio di Active Directory.

> [!NOTE]
> Utilizzare sempre la versione più recente di hello di Azure AD Connect tooensure si dispone di correzioni per tutti i bug noti.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>La sincronizzazione dal tooyour tenant di Azure AD gestite dominio
Account utente, appartenenza al gruppo e gli hash delle credenziali sono sincronizzati dal tooyour tenant di Azure AD dominio gestito di servizi di dominio Azure Active Directory. Questo processo di sincronizzazione è automatico, Non è necessario tooconfigure, monitorare e gestire il processo di sincronizzazione. Una volta completata la sincronizzazione iniziale monouso hello della directory, viene in genere richiede circa 20 minuti per le modifiche apportate in Azure AD toobe riflesse nel dominio gestito. Questo intervallo di sincronizzazione applica toopassword modifiche o modifiche tooattributes apportate in Azure AD.

il processo di sincronizzazione Hello è anche un-bidirezionali/unidirezionale in natura. Il dominio gestito è in gran parte di sola lettura, ad eccezione delle eventuali unità organizzative personalizzate create. Pertanto, è possibile apportare modifiche toouser attributi, le password degli utenti o appartenenza al gruppo nel dominio gestito hello. Di conseguenza, vi è alcuna sincronizzazione inversa delle modifiche dal tooyour di indietro dominio gestito tenant di Azure AD.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Sincronizzazione da un ambiente locale a più foreste
Molte organizzazioni hanno un'infrastruttura di identità locale piuttosto complessa composta da più foreste account. Azure AD Connect supporta la sincronizzazione di utenti, gruppi e gli hash delle credenziali dal tenant di Azure AD tooyour ambienti a più foreste.

Il tenant di Azure AD è invece uno spazio dei nomi piatto molto più semplice. tooenable utenti tooreliably accedere ad applicazioni protette da Azure AD, risolvere i conflitti di nome UPN tra gli account utente in foreste diverse. Orsi di dominio gestiti i servizi di dominio Active Directory di Azure chiudere tenant di Azure AD tooyour somiglianza. Nel dominio gestito viene perciò visualizzata una struttura di unità organizzative piatta. Tutti gli utenti e gruppi vengono archiviati all'interno del contenitore "AADDC utenti" hello, indipendentemente dal dominio locale hello o della foresta da cui essi sono state sincronizzate in. Anche se in locale è stata configurata una struttura gerarchica di unità organizzative, il dominio gestito presenta comunque una semplice struttura di unità organizzative piatta.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Esclusioni - ciò che non sincronizzato dominio gestito tooyour
Hello attributi o oggetti seguenti non sono sincronizzati tooyour tenant di Azure AD o dominio gestito tooyour:

* **Gli attributi esclusi:** è possibile scegliere alcuni attributi tooexclude la sincronizzazione di tenant di Azure AD tooyour dal dominio locale con Azure AD Connect. Gli attributi esclusi non sono disponibili nel dominio gestito.
* **Criteri di gruppo:** criteri di gruppo configurati nel dominio locale non sono sincronizzati tooyour di dominio gestiti.
* **Condivisione SYSVOL:** in modo analogo, contenuto hello di hello condivisione SYSVOL nel dominio locale non è sincronizzati tooyour di dominio gestiti.
* **Gli oggetti computer:** oggetti Computer per il dominio locale di tooyour aggiunti a un computer non sono sincronizzati tooyour di dominio gestiti. Questi computer non ha una relazione di trust con il dominio gestito e appartengono tooyour solo dominio locale. Nel dominio gestito, trovare gli oggetti computer solo per i computer è aggiunto al dominio in modo esplicito toohello gestito dominio.
* **Gli attributi di SidHistory per utenti e gruppi:** utente primario hello e il gruppo primario SID dal dominio locale sono dominio gestito tooyour sincronizzato. Tuttavia, gli attributi di SidHistory esistenti per utenti e gruppi non sono sincronizzati dal dominio gestito tooyour dominio locale.
* **Le strutture di unità Organizzativa dell'organizzazione:** unità organizzative definiti nel dominio locale non sincronizzare tooyour di dominio gestiti. Nel dominio gestito sono presenti due unità organizzative incorporate. Per impostazione predefinita, il dominio gestito presenta una struttura di unità organizzative piatta. È tuttavia possibile troppo[creare un'unità Organizzativa nel dominio gestito](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Come attributi specifici vengono sincronizzati tooyour di dominio gestiti
Hello nella tabella seguente sono elencati alcuni attributi comuni e viene descritto il modo in cui dominio gestito tooyour sincronizzato.

| Attributo nel dominio gestito | Origine | Note |
|:--- |:--- |:--- |
| UPN |Attributo UPN dell'utente nel tenant di Azure AD |l'attributo UPN Hello dal tenant di Azure AD viene sincronizzato come dominio tooyour gestiti. Pertanto, toosign modo più affidabile di hello nel dominio gestito tooyour Usa l'UPN. |
| SAMAccountName |Attributo mailNickname dell'utente nel tenant di Azure AD o generato automaticamente |attributo SAMAccountName Hello è originato dall'attributo mailNickname hello nel tenant di Azure AD. Se più account utente dispone di hello stesso attributo mailNickname, hello SAMAccountName viene generato automaticamente. Se hello mailNickname o prefisso UPN dell'utente è più di 20 caratteri, hello SAMAccountName è generato automaticamente toosatisfy hello 20 limite di caratteri per gli attributi SAMAccountName. |
| Password |Password utente del tenant di Azure AD |Gli hash delle credenziali necessari per l'autenticazione NTLM o Kerberos, anche detti credenziali supplementari, vengono sincronizzati dal tenant di Azure AD. Se il tenant di Azure AD è un tenant sincronizzato, tali credenziali vengono originate dal dominio locale. |
| SID utente/gruppo primario |Generato automaticamente |SID primario di Hello per gli account utente o gruppo è stato generato automaticamente nel dominio gestito. Questo attributo non corrisponde hello utente/SID gruppo primario dell'oggetto hello in locale di dominio Active Directory. Questa mancata corrispondenza infatti hello gestito dominio dispone di un altro spazio dei nomi SID di dominio locale. |
| Cronologia SID per utenti e gruppi |SID utente/gruppo primario locale |attributo SidHistory Hello per utenti e gruppi nel dominio gestito è impostata l'utente primario del toomatch hello corrispondente o SID di gruppo nel dominio locale. Questa funzionalità consente di verificare accuratezza di spostamento e di locale applicazioni toohello dominio gestiti più semplice, poiché non è necessario risorse toore ACL. |

> [!NOTE]
> **Accedi toohello dominio gestito nel formato UPN hello:** attributo SAMAccountName hello potrebbe essere generato automaticamente da alcuni account utente nel dominio gestito. Se più utenti hanno hello stesso attributo mailNickname o gli utenti sono eccessivamente lungo i prefissi UPN, hello SAMAccountName per questi utenti può essere generato automaticamente. Pertanto, hello SAMAccountName formato (ad esempio, ' CONTOSO100\joeuser') non è sempre un modo affidabile toosign toohello dominio. L'attributo SAMAccountName autogenerato dell'utente potrebbe infatti essere diverso dal relativo prefisso UPN. Utilizzare il formato UPN hello (ad esempio, 'joeuser@contoso100.com') toosign in toohello gestiti in modo affidabile di dominio.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Mapping degli attributi per gli account utente
Hello nella tabella seguente illustra gli attributi specifici come per gli oggetti utente nel tenant di Azure AD sono attributi sincronizzati toocorresponding nel dominio gestito.

| Attributo utente nel tenant di Azure AD | Attributo utente nel dominio gestito |
|:--- |:--- |
| accountEnabled |userAccountControl (attiva o disattiva hello ACCOUNT_DISABLED bit) |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |title |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (a volte può essere generato automaticamente) |
| mobile |mobile |
| objectId |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (attiva o disattiva hello DONT_EXPIRE_PASSWORD bit) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Mapping degli attributi per i gruppi
Hello nella tabella seguente illustra gli attributi specifici come per gli oggetti gruppo nel tenant di Azure AD sono attributi sincronizzati toocorresponding nel dominio gestito.

| Attributo di gruppo nel tenant di Azure AD | Attributo di gruppo nel dominio gestito |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (a volte può essere generato automaticamente) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectId |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Gli oggetti che non sono sincronizzati tooyour tenant di Azure AD dal dominio gestito
Come descritto nella sezione precedente di questo articolo, non vi è alcuna sincronizzazione da tooyour di indietro il dominio gestito tenant di Azure AD. È possibile scegliere troppo[creare un'unità organizzativa personalizzato (OU)](active-directory-ds-admin-guide-create-ou.md) nel dominio gestito. All'interno delle queste unità organizzative personalizzate è possibile creare anche altre unità organizzative, utenti, gruppi o account di servizio. Nessuno degli oggetti hello creati all'interno di unità organizzative personalizzate vengono sincronizzate tooyour indietro tenant di Azure AD. ma sono disponibili per l'uso unicamente all'interno del dominio gestito. Di conseguenza, questi oggetti non sono visibili tramite cmdlet di Azure AD PowerShell, API Graph di Azure AD o interfaccia utente di gestione di hello Azure AD.

## <a name="related-content"></a>Contenuti correlati
* [Funzionalità - Servizi di dominio Azure AD](active-directory-ds-features.md)
* [Scenari di distribuzione - Servizi di dominio Azure AD](active-directory-ds-scenarios.md)
* [Considerazioni sulla rete per Azure AD Domain Services](active-directory-ds-networking.md)
* [Introduzione ad Azure AD Domain Services](active-directory-ds-getting-started.md)
