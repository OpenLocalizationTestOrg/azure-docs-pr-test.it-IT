---
title: appartenenti aaaTroubleshooting hello-registrazione automatica del dominio di Azure AD per Windows 10 e Windows Server 2016 | Documenti Microsoft
description: Risoluzione dei problemi di registrazione automatica hello del dominio di Azure AD aggiunto a un computer Windows 10 e Windows Server 2016.
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Risoluzione dei problemi di registrazione automatica del dominio aggiunti a un computer tooAzure AD – Windows 10 e Windows Server 2016

In questo argomento è applicabile toohello client seguenti:

-   Windows 10
-   Windows Server 2016

Per altri client di Windows, vedere [risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

Questo argomento si presuppone di aver configurato la registrazione automatica dei dispositivi appartenenti a un dominio come descritto in descritto in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-device-registration-get-started.md) hello toosupport seguenti scenari:

- [Accesso condizionale basato su dispositivo](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Roaming aziendale delle impostazioni](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)


Questo documento fornisce istruzioni sulla risoluzione dei problemi in modo tooresolve potenziali problemi. 

Hello registrazione è supportata in Windows hello aggiornamento 10 novembre 2015 e versioni successive.  
È consigliabile utilizzare hello dall'aggiornamento Aniversary per l'abilitazione di scenari di hello precedenti.

## <a name="step-1-retrieve-hello-registration-status"></a>Passaggio 1: Recuperare lo stato della registrazione hello 

**stato della registrazione tooretrieve hello:**

1. Aprire il prompt dei comandi di hello come amministratore.

2. Digitare **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Nessun DeviceId: identificazione personale 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected del Provider di crittografia della piattaforma Microsoft: Sì KeySignTest:: deve eseguire con privilegi elevati tootest.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>Passaggio 2: Valutare lo stato della registrazione hello 

Esaminare i seguenti campi hello e assicurarsi che dispongano di valori previsti hello:

### <a name="azureadjoined--yes"></a>AzureAdJoined: YES  

Questo campo viene visualizzato se il dispositivo di hello è registrato con Azure AD. Se il valore di hello Mostra come 'NO', non è stata completata la registrazione. 

**Possibili cause:**

- Autenticazione del computer hello per la registrazione non riuscita.

- È un proxy HTTP nell'organizzazione hello che non può essere individuati dal computer hello

- non riesce a raggiungere il computer Hello Azure Active Directory per l'autenticazione o Azure DRS per la registrazione

- Hello computer potrebbero non essere nella rete interna dell'organizzazione hello o VPN con tooan diretto visibilità diretta del controller di dominio Active Directory locale.

- Se il computer di hello dispone di un TPM, potrebbe essere in uno stato non valido.

- Potrebbe esserci un errore di configurazione in servizi di evidenziato nel documento hello che sarà necessario tooverify nuovamente. Esempi comuni:

    - Il server federativo non dispone di endpoint WS-Trust abilitati

    - Il server federativo potrebbe non consentire l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.

    - È presente alcun oggetto punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello

---

### <a name="domainjoined--yes"></a>DomainJoined: YES  

Questo campo Mostra se dispositivo hello è unita in join tooan Active Directory locale o meno. Se il valore di hello Mostra come **n**, dispositivo hello non vengono registrati automaticamente con Azure AD. Verificare innanzitutto che toohello di join hello dispositivo in Active Directory locale prima che la registrazione con Azure AD. Se si sta cercando di unione hello computer tooAzure AD direttamente, visitare tooLearn sulle funzionalità di Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: NO  

Questo campo viene visualizzato se il dispositivo di hello è registrato con Azure AD, ma come un dispositivo personale (contrassegnati come 'All'area di lavoro'). Se questo valore deve essere 'NO' per un computer aggiunto a un dominio registrato con Azure AD, tuttavia se viene visualizzato Sì significa che un account aziendale o dell'istituto di istruzione è stata aggiunta toohello precedente computer con la registrazione. In questo caso account hello verrà ignorato se si utilizza una versione di hello dall'aggiornamento Aniversary di Windows 10 (1607 quando in esecuzione comando WinVer hello in hello finestra 'Esegui' o una finestra del prompt dei comandi).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: YES e AzureADPrt: YES
  
Questi campi mostrano che l'utente hello ha autenticato tooAzure Active Directory all'accesso toohello dispositivo. Se vengono visualizzate 'NO' hello Ecco le possibili cause:

- Chiave di archiviazione non valida (STK) nel TPM associato hello dispositivo durante la registrazione (controllo hello KeySignTest durante l'esecuzione con privilegi elevati).

- ID di accesso alternativo

- Proxy HTTP non trovato

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere hello [domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md) 
