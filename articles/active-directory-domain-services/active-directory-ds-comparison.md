---
title: 'Servizi di dominio AD Azure: I controller di dominio servizi di dominio Active Directory di Azure confrontare tooDIY | Documenti Microsoft'
description: Confronto tra i controller di dominio di Azure Active Directory Domain Services tooDIY
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Come toodecide se servizi di dominio Active Directory di Azure è adatta per il caso di utilizzo
Con servizi di dominio Active Directory di Azure è possibile distribuire i carichi di lavoro nei servizi infrastruttura di Azure, senza dovere tooworry sulla gestione dell'infrastruttura di identità in Azure. Questo servizio gestito è diverso da una tipica distribuzione di Windows Server Active Directory che viene distribuita e amministrata in modo autonomo. servizio di Hello è toodeploy semplice e offre il monitoraggio dello stato automatizzato e monitoraggio e aggiornamento. Ci stiamo in continua evoluzione tooadd assistenza hello per scenari di distribuzione comuni.

toodecide se toouse di servizi di dominio di Active Directory di Azure, è consigliabile hello seguente documentazione:

* Vedere l'elenco di hello di [funzionalità offerte dai servizi di dominio Active Directory di Azure](active-directory-ds-features.md).
* Esaminare comuni [scenari di distribuzione per Servizi di dominio Azure Active Directory](active-directory-ds-scenarios.md).
* Infine, [confrontare l'opzione di servizi di dominio Active Directory di Azure AD fai da te tooa](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Confrontare dominio tooDIY Active Directory di servizi di dominio Active Directory di Azure in Azure
Hello nella tabella seguente contribuisce di stabilire tra l'utilizzo di servizi di dominio Active Directory di Azure e gestire la propria infrastruttura di Active Directory in Azure.

| **Funzionalità** | **Servizi di dominio Azure Active Directory** | **AD "fai da te" in VM di Azure** |
| --- |:---:|:---:|
| [**Servizi gestiti**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**&amp;#x2715;** |
| [**Distribuzioni sicure**](active-directory-ds-comparison.md#secure-deployments) |**&amp;#x2713;** |L'amministratore deve distribuzione hello toosecure. |
| [**Server DNS**](active-directory-ds-comparison.md#dns-server) |**&#x2713;** (servizio gestito) |**&#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&#x2715;** |**&amp;#x2713;** |
| [**Aggiunta a un dominio**](active-directory-ds-comparison.md#domain-join) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Autenticazione di dominio tramite NTLM e Kerberos**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Delega vincolata Kerberos**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|basata sulle risorse|basata sulle risorse e basata su account|
| [**Struttura personalizzata per le unità organizzative**](active-directory-ds-comparison.md#custom-ou-structure) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Estensioni dello schema**](active-directory-ds-comparison.md#schema-extensions) |**&#x2715;** |**&amp;#x2713;** |
| [**Relazioni di trust di dominio/foresta di AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&#x2715;** |**&amp;#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**LDAP sicuro (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&amp;#x2713;** |**&#x2713;** |
| [**Distribuzione in diverse aree geografiche**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&amp;#x2715;** |**&amp;#x2713;** |

#### <a name="managed-service"></a>Servizi gestiti
Servizi di dominio Azure AD è gestito da Microsoft. Non si dispone di tooworry sull'applicazione di patch, aggiornamenti, il monitoraggio, backup e garantire la disponibilità del dominio. Queste attività di gestione sono disponibili come servizio di Microsoft Azure per i domini gestiti.

#### <a name="secure-deployments"></a>Distribuzioni sicure
dominio gestito Hello è bloccato in modo sicuro in base alle raccomandazione di sicurezza di Microsoft per le distribuzioni di Active Directory. Questi suggerimenti derivano dalla decenni del team del prodotto AD hello dell'esperienza di progettazione e il supporto di distribuzioni di Active Directory. Per le distribuzioni fai da te, è necessario distribuzione specifica tootake passaggi toolock giù/proteggere la distribuzione.

#### <a name="dns-server"></a>Server DNS
Un dominio gestito da Servizi di dominio Azure AD include servizi DNS gestiti. I membri del gruppo 'Administrators di controller di dominio di AAD' hello possono gestire DNS nel dominio hello gestito. Membri di questo gruppo hanno tutti i privilegi di amministrazione DNS per il dominio gestito hello. Gestione di DNS può essere eseguita mediante hello 'Console di amministrazione DNS' incluso nel pacchetto di strumenti di amministrazione remota Server (RSAT) hello.
[Altre informazioni](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Privilegi amministrativi per il dominio o per l'organizzazione
Questi privilegi elevati non sono disponibili in un dominio gestito di Servizi di dominio Azure AD. Le applicazioni che richiedono questi privilegi elevati non possono essere distribuite nei domini gestiti di AAD-DS. Un subset ridotto di privilegi amministrativi è toomembers disponibile del gruppo di amministrazione delegata hello chiamato 'amministratori dei controller di dominio AAD '. Questi privilegi includono privilegi tooconfigure DNS, configurare criteri di gruppo, ottengono i privilegi di amministratore sul computer di dominio e così via.

#### <a name="domain-join"></a>Aggiunta a un dominio
È possibile aggiungere macchine virtuali toohello gestiti toohow simile a dominio dominio di computer tooan Active Directory.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Autenticazione di dominio tramite NTLM e Kerberos
Con i servizi di dominio Active Directory di Azure, è possibile utilizzare tooauthenticate le credenziali aziendali con il dominio gestito hello. Le credenziali vengono mantenute sincronizzate con il tenant di Azure AD. Per i tenant sincronizzati, Azure AD Connect garantisce che le modifiche apportate toocredentials locale sincronizzati tooAzure AD. Potrebbe essere necessario tooset di un dominio di Active Directory con l'installazione di un dominio fai da te, relazione di trust con locale AD tooauthenticate gli utenti con le proprie credenziali aziendali. In alternativa, potrebbe essere necessario tooset backup tooensure di replica di Active Directory che le password degli utenti sincronizzati macchine virtuali controller di dominio di Azure tooyour.

#### <a name="kerberos-constrained-delegation"></a>Delega vincolata Kerberos
Non si dispone dei privilegi di "Domain Admin" in un dominio gestito Active Directory Domain Services. Pertanto non è possibile configurare la delega vincolata Kerberos basata su account (tradizionale). Tuttavia, è possibile configurare più sicuro hello basata sulle risorse per la delega vincolata.
[Altre informazioni](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Struttura personalizzata per le unità organizzative
I membri del gruppo 'Administrators di controller di dominio di AAD' hello è possono creare unità organizzative personalizzate hello gestito dominio. Gli utenti che creare unità organizzative personalizzate vengono concessi privilegi amministrativi completi su hello unità Organizzativa.
[Altre informazioni](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Estensioni dello schema
È possibile estendere allo schema di base hello di un dominio gestito di servizi di dominio Active Directory di Azure. Pertanto, le applicazioni basate su schema tooAD delle estensioni (ad esempio, nuovi attributi nell'oggetto utente hello) non possono essere elevate e spostata domini tooAAD di dominio Active Directory.

#### <a name="ad-domain-or-forest-trusts"></a>Relazioni di trust di dominio o foresta di AD
Domini gestiti non possono essere configurato tooset relazioni di trust (in ingresso/in uscita) con altri domini. Pertanto, gli scenari di distribuzione della foresta di risorse non possono usare Azure AD Domain Services. Analogamente, le distribuzioni in cui si preferisce non toosynchronize password tooAzure AD non è possibile utilizzare servizi di dominio Active Directory di Azure.

#### <a name="ldap-read"></a>Lettura LDAP
Hello gestiti dominio supporta LDAP letture i carichi di lavoro. È quindi possibile distribuire le applicazioni che eseguono operazioni con dominio gestito hello di lettura LDAP.

#### <a name="secure-ldap"></a>LDAP sicuro
È possibile configurare servizi di dominio Active Directory di Azure tooprovide sicura LDAP accesso tooyour gestiti hello di dominio, inclusi su internet.
[Altre informazioni](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Scrittura LDAP
dominio gestito Hello è di sola lettura per gli oggetti utente. Pertanto, le applicazioni che eseguono operazioni di scrittura LDAP per gli attributi dell'oggetto utente hello non funzionano in un dominio gestito. Inoltre, le password degli utenti non possono essere modificate in dominio gestito hello. Un altro esempio sarebbe la modifica di appartenenza a gruppi o gli attributi di gruppo all'interno di dominio gestiti hello, che non è consentito. Tuttavia, qualsiasi modifica toouser attributi o le password apportate in Azure Active Directory (tramite PowerShell/portale) locale o Active Directory vengono sincronizzati toohello AAD di dominio Active Directory gestito dominio.

#### <a name="group-policy"></a>Criteri di gruppo
Non vi è un incorporato oggetto Criteri di gruppo ogni per i contenitori di "AADDC utenti" e "Computer AADDC" hello. È possibile personalizzare questi criteri di gruppo tooconfigure oggetti Criteri di gruppo predefiniti. I membri del gruppo 'Administrators di controller di dominio di AAD' hello possono anche creare oggetti Criteri di gruppo personalizzate e le collegano le unità organizzative tooexisting (incluse le unità organizzative personalizzate).
[Altre informazioni](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Distribuzioni geograficamente sparse
I domini gestiti di Servizi di dominio Azure AD sono disponibili in una singola rete virtuale in Azure. Per gli scenari che richiedono toobe controller dominio disponibile in più aree di Azure tra HelloWorld, l'impostazione di controller di dominio in macchine virtuali IaaS di Azure potrebbe essere alternativa migliore hello.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Opzioni di distribuzione AD "fai da te"
È possibile casi d'uso di distribuzione in cui è necessario alcune delle funzionalità di hello offerte da un'installazione di Windows Server Active Directory. In questi casi, considerare una delle seguenti opzioni (DIY) fai da te hello:

* **Dominio cloud autonomo:** è possibile configurare un "dominio cloud" autonomo usando macchine virtuali Azure che sono state configurate come controller di dominio. Questa infrastruttura non si integra con l'ambiente Active Directory locale. Questa opzione richiederebbe un set diverso di 'cloud credenziali' toologin o gestire le macchine virtuali nel cloud hello.
* **Distribuzione di foresta di risorse:** è possibile impostare un dominio nella topologia della foresta risorse hello, utilizzando macchine virtuali di Azure configurate come controller di dominio. Quindi si può impostare una relazione di trust di Active Directory con l'ambiente Active Directory locale. È possibile foresta delle risorse toothis computer (macchine virtuali di Azure) aggiunta al dominio nel cloud hello. Autenticazione utente avviene su sia una directory di on-premise tooyour connessione VPN/ExpressRoute.
* **Estendere la tooAzure di dominio locale:** è possibile connettere una rete locale tooyour di rete virtuale di Azure tramite una connessione VPN/ExpressRoute. Questa impostazione consente di macchine virtuali di Azure toobe tooyour collegati AD locale. In alternativa è toopromote il controller di dominio di replica del dominio locale in Azure come macchina virtuale. È possibile quindi configurarlo tooreplicate su una directory di on-premise tooyour connessione VPN/ExpressRoute. Questa modalità di distribuzione si estende in modo efficace il tooAzure di dominio locale.

> [!NOTE]
> Un'opzione fai da te potrebbe essere più adatta per determinate situazioni di distribuzione. Prendere in considerazione [condividere commenti](active-directory-ds-contact-us.md) toohelp ci comprendere quali funzionalità facilitare si è scelto di servizi di dominio Active Directory di Azure in futuro hello. Questi commenti e suggerimenti utili per sviluppare seme di toobetter servizio hello che esigenze di implementazione e casi d'uso.
>
>

Microsoft ha pubblicato [linee guida per la distribuzione di Windows Server Active Directory in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp rendere più semplice eseguire installazioni.

## <a name="related-content"></a>Contenuti correlati
* [Funzionalità - Servizi di dominio Azure AD](active-directory-ds-features.md)
* [Scenari di distribuzione - Servizi di dominio Azure AD](active-directory-ds-scenarios.md)
* [Linee guida per la distribuzione di Active Directory di Windows Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
