---
title: aaaApplications e browser che utilizzano regole di accesso condizionale in Azure Active Directory | Documenti Microsoft
description: Controllo di accesso condizionale, Azure Active Directory controlla per condizioni specifiche durante l'autenticazione utente hello e tooallow accesso all'applicazione.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Applicazioni e browser che usano regole di accesso condizionale in Azure Active Directory

Le regole di accesso condizionale sono supportate in applicazioni connesse di Azure AD (Azure Active Directory), applicazioni SaaS (Software as a Service) federate preintegrate, applicazioni che usano l'accesso SSO (Single Sign-On) basato su password, applicazioni line-of-business e applicazioni che usano il proxy dell'applicazione di Azure AD. Per un elenco dettagliato delle applicazioni per cui è possibile abilitare l'accesso condizionale, vedere [Servizi abilitati con l'accesso condizionale](active-directory-conditional-access-technical-reference.md). L'accesso condizionale è ideale sia per le applicazioni desktop che per i dispositivi mobili che usano un'autenticazione moderna. In questo articolo viene illustrato il funzionamento dell'accesso condizionale nelle app desktop e in quelle per dispositivi mobili.

È possibile usare le pagine di accesso di Azure AD nelle applicazioni che usano l'autenticazione moderna. In una pagina di accesso all'utente viene richiesto di effettuare un'autenticazione a più fattori. Un messaggio viene visualizzato se l'accesso dell'utente hello è bloccato. In modo che vengono valutati i criteri di accesso condizionale basato su dispositivo, è necessario per hello dispositivo tooauthenticate con Azure AD, l'autenticazione moderna.

È importante tooknow quali applicazioni possono utilizzare regole di accesso condizionale e hello passaggi che potrebbe essere necessario tootake toosecure altri punti di ingresso dell'applicazione.

## <a name="applications-that-use-modern-authentication"></a>Applicazioni che usano l'autenticazione moderna
> [!NOTE]
> Se in Azure AD è presente un criterio di accesso condizionale equivalente a un analogo criterio di Office 365, configurare entrambi i criteri di accesso condizionale. Questa restrizione è applicabile, ad esempio, i criteri di accesso tooconditional per Exchange Online o SharePoint Online.
>
>

Hello applicazioni seguenti supportano l'accesso condizionale per Office 365 e altre applicazioni di servizio connesso AD Azure:


| Servizio di destinazione| Piattaforma| Applicazione |
| --- | --- | --- |
| Qualsiasi servizio app Mie app| Android e iOS| MFA e criteri relativi alle applicazioni. I criteri basati su dispositivo non sono supportati.|
| Servizio app Azure Remote| Windows 10, Windows 8.1, Windows 7, iOS, Android e Mac OS X| App Azure Remote|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS e Android| Dynamics CRM|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, iOS/Android e MAC OSX| Microsoft Team Services consente di controllare tutti i servizi che supportano i team Microsoft e tutte le app client: Windows Desktop, MAC OS X, iOS, Android, WP e web client|
| Office 365 Exchange Online| Windows 10| App Mail/Calendar/People, Outlook 2016, Outlook 2013 (con l'autenticazione moderna), Skype for Business (con l'autenticazione moderna)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (con l'autenticazione moderna), Skype for Business (con l'autenticazione moderna)|
| Office 365 Exchange Online| iOS| App Outlook Mobile|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office per macOS)|
| Office 365 SharePoint Online| Windows 10| Applicazioni di Office 2016, Office Universal App, Office 2013 (con l'autenticazione moderna), il client di sincronizzazione OneDrive (vedere [note](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), pianificato per hello future supporto di gruppi di Office, SharePoint app supportano pianificati per hello future|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| App di Office 2016, Office 2013 (con autenticazione moderna), client sincronizzazione OneDrive (vedere le [note](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| App Office per dispositivi mobili|
| Office 365 SharePoint Online| Mac OS X| Office 2016 per macOS (solo Word, Excel, PowerPoint e OneNote). OneDrive per il supporto di Business pianificata hello future|
| Office 365 Yammer| Windows 10, iOS, Android| App Office Yammer|
| Servizio PowerBI| Windows 10, Windows 8.1, Windows 7 e iOS| App PowerBI. Hello app di Power BI per Android non supporta attualmente l'accesso condizionale basato su dispositivi.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS e Android| App Visual Studio Team Services|








## <a name="applications-that-do-not-use-modern-authentication"></a>Applicazioni che non utilizzano l'autenticazione moderna
Attualmente, è necessario utilizzare altri tooapps accesso tooblock di metodi che non utilizzano l'autenticazione moderna. Le regole per le app che non usano l'autenticazione moderna non vengono applicate in base all'accesso condizionale. Questo vale soprattutto per l'accesso a Exchange e SharePoint. La maggior parte delle versioni meno recenti delle app usa protocolli di controllo dell'accesso non moderni.

### <a name="control-access-in-office-365-sharepoint-online"></a>Controllo dell'accesso in Office 365 SharePoint Online
È possibile disabilitare un protocolli legacy per l'accesso a SharePoint tramite il cmdlet Set-SPOTenant hello. Utilizzare questo client di Office tooprevent cmdlet che utilizzano i protocolli di autenticazione non moderni di accedere alle risorse di SharePoint Online.

**Comando di esempio**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Controllo dell'accesso in Office 365 Exchange Online
Exchange offre due categorie principali di protocolli. Esaminare le opzioni seguenti hello e quindi selezionare i criteri di hello adatto alla propria organizzazione.

* **Exchange ActiveSync**. Per impostazione predefinita, i criteri di accesso condizionale per l'autenticazione a più fattori e i criteri di posizione non vengono applicati per Exchange ActiveSync. È necessario servizi toothese di accesso tooprotect configurando direttamente i criteri di Exchange ActiveSync o mediante il blocco di Exchange ActiveSync, utilizzando le regole di Active Directory Federation Services (ADFS).
* <seg>
  **Protocolli legacy**.</seg> È possibile bloccare protocolli legacy con AD FS. In questo modo si impedisce ai client di Office tooolder accesso, ad esempio Office 2013 senza abilitata l'autenticazione moderna e versioni precedenti di Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>Protocollo ADFS tooblock legacy
È possibile utilizzare hello seguente esempio rilascio regole tooblock protocollo legacy di accesso di autorizzazione a livello di hello AD FS. Scegliere una delle due configurazioni più comuni.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Opzione 1: Consentono di Exchange ActiveSync e le applicazioni legacy, ma solo su intranet hello
Tramite l'applicazione hello seguenti tre regole toohello ADFS relying party attendibile per la piattaforma di identità di Microsoft Office 365, il traffico di Exchange ActiveSync, e browser e il traffico di autenticazione moderna, hanno accesso. Le applicazioni legacy sono bloccate da hello extranet.

##### <a name="rule-1"></a>Regola 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Regola 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Regola 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Opzione 2: consentire l'accesso a Exchange ActiveSync e bloccare le applicazioni legacy
Tramite l'applicazione hello seguenti tre regole toohello ADFS relying party attendibile per la piattaforma di identità di Microsoft Office 365, il traffico di Exchange ActiveSync, e browser e il traffico di autenticazione moderna, hanno accesso. Le app legacy vengono bloccate da qualunque percorso.

##### <a name="rule-1"></a>Regola 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Regola 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Regola 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Browser supportati per criteri basati su dispositivo 

È possibile ottenere solo per i criteri di dispositivo in base che consentono di controllare l'accesso per la conformità del dispositivo e aggiunta al dominio, quando è in grado di identificare e autenticare il dispositivo hello Azure AD. Durante la maggior parte dei controlli, ad esempio percorso e il lavoro di autenticazione a più fattori per la maggior parte dei dispositivi e browser, i criteri per i dispositivi richiedono versione hello del sistema operativo e i browser elencati di seguito. Accesso è bloccato per gli utenti del browser non supportato o sistemi operativi hello se un criterio del dispositivo è in uso. 

| OS                     | Browser                 | Supporto     |
| :--                    | :--                      | :-:         |
| Windows 10                 | Internet Explorer, Edge                 | ![Controllo][1] |
| Windows 10                 | Chrome                   | Preview     |
| Windows 8/8.1            | IE, Chrome               | ![Controllo][1] |
| Windows 7                  | IE, Chrome               | ![Controllo][1] |
| iOS                    | Safari                   | ![Controllo][1] |
| Android                | Chrome                   | ![Controllo][1] |
| Windows Phone          | Internet Explorer, Edge                 | ![Controllo][1] |
| Windows Server 2016    | Internet Explorer, Edge                 | ![Controllo][1] |
| Windows Server 2016    | Chrome                   | Presto disponibile |
| Windows Server 2012 R2 | IE, Chrome               | ![Controllo][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![Controllo][1] |
| Mac OS                 | Safari                   | ![Controllo][1] |
| Mac OS                 | Chrome                   | Presto disponibile |

> [!NOTE]
> Per il supporto di Chrome, è necessario utilizzare Windows 10 creatori di aggiornamento e l'estensione di hello installazione trovato [qui](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Passaggi successivi

Per maggiori dettagli, vedere [Accesso condizionale in Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


