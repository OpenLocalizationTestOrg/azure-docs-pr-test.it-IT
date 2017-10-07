---
title: dispositivi Windows 10 e Windows Server 2016 unita in join ibrido aaaTroubleshooting Azure Active Directory | Documenti Microsoft
description: "Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory 

In questo argomento è applicabile toohello client seguenti:

-   Windows 10
-   Windows Server 2016

Per altri client Windows, vedere [Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).

In questo argomento si presuppone che sia [Configurazione ibrida di Azure Active Directory i dispositivi appartenenti](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport seguenti scenari:

- Accesso condizionale basato su dispositivo

- [Roaming aziendale delle impostazioni](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)


Questo documento fornisce istruzioni sulla risoluzione dei problemi in modo tooresolve potenziali problemi. 


Per Windows 10 e Windows Server 2016, ibrida di Azure Active Directory join supporta hello Windows 10 aggiornamento di novembre 2015 e versioni successive. È consigliabile utilizzare dall'aggiornamento Aniversary hello.

## <a name="step-1-retrieve-hello-join-status"></a>Passaggio 1: Recuperare lo stato di join hello 

**stato di join tooretrieve hello:**

1. Hello Apri prompt dei comandi come amministratore

2. Digitare **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Nessun DeviceId: identificazione personale 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected del Provider di crittografia della piattaforma Microsoft: Sì KeySignTest:: deve eseguire con privilegi elevati tootest.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>Passaggio 2: Valutare lo stato di join hello 

Esaminare i seguenti campi hello e assicurarsi che dispongano di valori previsti hello:

### <a name="azureadjoined--yes"></a>AzureAdJoined: YES  

Questo campo indica se il dispositivo hello viene unito con Azure AD. Se il valore di hello è **n**, hello tooAzure join Active Directory non è ancora completato. 

**Possibili cause:**

- Autenticazione del computer hello per un join non riuscita.

- È un proxy HTTP nell'organizzazione hello che non può essere individuati dal computer hello

- computer Hello non riesce a raggiungere tooauthenticate AD Azure o Azure DRS per la registrazione

- Hello computer potrebbero non essere nella rete interna dell'organizzazione hello o VPN con tooan diretto visibilità diretta del controller di dominio Active Directory locale.

- Se il computer di hello dispone di un TPM, può essere in uno stato non valido.

- Potrebbe esserci un errore di configurazione in servizi di hello evidenziato nel documento hello che sarà necessario tooverify nuovamente. Esempi comuni:

    - Il server federativo non dispone di endpoint WS-Trust abilitati

    - Il server federativo non consente l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.

    - È presente alcun oggetto punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello

---

### <a name="domainjoined--yes"></a>DomainJoined: YES  

Questo campo indica se si aggiunge il dispositivo hello tooan Active Directory locale o non. Se il valore di hello è **n**, dispositivo hello non è possibile eseguire un join di Azure AD ibrido.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: NO  

Questo campo indica se il dispositivo di hello è registrato con Azure AD come un dispositivo personale (contrassegnata come *all'area di lavoro*). Questo valore deve essere **NO** per un computer aggiunto al dominio che è anche aggiunto all'identità ibrida di Azure AD. Se il valore di hello è **Sì**, completamento toohello precedente di join di Azure AD ibrido hello è stato aggiunto un account aziendale o dell'istituto di istruzione. In questo caso, l'account di hello viene ignorato quando si utilizza una versione di hello dall'aggiornamento Aniversary di Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: YES e AzureADPrt: YES
  
Questi campi indicano se utente hello è autenticata correttamente tooAzure AD durante l'accesso toohello dispositivo. Se i valori hello sono **n**, potrebbe essere dovuto:

- Chiave di archiviazione non valida (STK) nel TPM associato hello dispositivo durante la registrazione (controllo hello KeySignTest durante l'esecuzione con privilegi elevati).

- ID di accesso alternativo

- Proxy HTTP non trovato

## <a name="next-steps"></a>Passaggi successivi

Per domande, vedere hello [domande frequenti sulla gestione dei dispositivi](device-management-faq.md) 
