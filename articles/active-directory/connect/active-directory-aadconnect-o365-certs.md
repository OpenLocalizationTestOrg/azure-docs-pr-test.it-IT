---
title: rinnovo aaaCertificate per gli utenti di Office 365 e Azure AD | Documenti Microsoft
description: Questo articolo illustra gli utenti di 365 tooOffice come tooresolve problemi con messaggi di posta elettronica informarli riguardo rinnovare un certificato.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Rinnovare i certificati di federazione per Office 365 e Azure Active Directory
## <a name="overview"></a>Panoramica
Per la federazione tra Azure Active Directory (Azure AD) e Active Directory Federation Services (ADFS) ha esito positivo, i certificati di hello utilizzati da ADFS toosign sicurezza token tooAzure Active Directory devono corrispondere a quello configurato in Azure AD. Mancata corrispondenza può causare toobroken trust. Azure AD assicura che queste informazioni rimangano sincronizzate durante la distribuzione di AD FS e Proxy applicazione Web (per l'accesso Extranet).

In questo articolo fornisce informazioni aggiuntive toomanage il token di firma dei certificati e mantenerli sincronizzati con Azure AD, hello seguenti casi:

* Non si sta distribuendo hello Proxy applicazione Web e pertanto i metadati della federazione hello non sono disponibili in hello extranet.
* Non si utilizza configurazione predefinita di hello di ADFS per i certificati di firma di token.
* Si usa un provider di identità di terze parti.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Configurazione predefinita di AD FS per i certificati per la firma di token
la firma di token Hello e certificati di decrittografia token vengono in genere certificati autofirmati e sono ideali per un anno. Per impostazione predefinita, AD FS include un processo di rinnovo automatico denominato **AutoCertificateRollover**. Se si usa AD FS 2.0 o versione successiva, Office 365 e Azure AD aggiornano automaticamente il certificato prima della scadenza.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Notifica di rinnovo dal portale di Office 365 hello o un messaggio di posta elettronica
> [!NOTE]
> Se si ha ricevuto un messaggio di posta elettronica o una notifica tramite il portale in cui viene richiesto toorenew il certificato per Office, vedere [gestione modifiche tootoken i certificati di firma](#managecerts) toocheck se tootake è necessaria alcuna azione. Microsoft è a conoscenza di un problema di possibili che può portare toonotifications per il rinnovo del certificato viene inviato, anche quando è necessaria alcuna azione.
>
>

Azure AD tenta toomonitor hello i metadati della federazione e token di aggiornamento hello i certificati di firma, come indicato da questi metadati. 30 giorni prima della scadenza hello di certificati, la firma dei token hello Azure AD verifica se i nuovi certificati sono disponibili tramite il polling dei metadati di federazione hello.

* Se correttamente possa eseguire il polling dei metadati di federazione hello e recuperare nuovi certificati hello, alcuna notifica tramite posta elettronica o un avviso nel portale di Office 365 hello non è emesso toohello utente.
* Se non è possibile recuperare i certificati di firma di token a nuovo hello, sia perché i metadati della federazione hello non sono raggiungibili o non è abilitato il rollover automatico dei certificati, Azure AD rilascia un avviso nel portale di Office 365 hello e notifiche di posta elettronica.

![Notifica del portale di Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Se si utilizza ADFS, continuità aziendale tooensure, verificare che i server dispongano di hello dopo gli aggiornamenti in modo che non si verificano errori di autenticazione per i problemi noti. Si riducono in tal modo i problemi noti relativi al server proxy di AD FS per questo periodo di rinnovo e per quelli futuri:
>
> Server 2012 R2 - [Aggiornamento cumulativo per Windows Server: maggio 2014](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 and 2012 - [L'autenticazione tramite proxy ha esito negativo in Windows Server 2012 o Windows Server 2008 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Controllare se i certificati di hello toobe aggiornato<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Passaggio 1: Controllare lo stato AutoCertificateRollover hello
Nel server AD FS aprire Powershell. Verificare che il valore di AutoCertificateRollover hello è impostato tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Se si usa AD FS 2.0, eseguire prima Add-Pssnapin Microsoft.Adfs.Powershell.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Passaggio 2: Verificare che AD FS e Azure AD siano sincronizzati
Nel server AD FS, aprire il prompt di Azure AD PowerShell hello e connettersi tooAzure Active Directory.

> [!NOTE]
> È possibile scaricare Azure AD PowerShell [qui](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Verificare i certificati di hello configurate in ADFS e le proprietà di attendibilità di Azure AD per hello dominio specificavano.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Se le identificazioni personali hello in entrambi gli output di hello corrispondenza, i certificati siano sincronizzati con Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Passaggio 3: Verificare se il certificato è su tooexpire
Nell'output di Get-MsolFederationProperty o Get-AdfsCertificate hello verificare data hello in "Non dopo." Se data hello è inferiore a 30 giorni, è necessario eseguire l'operazione.

| AutoCertificateRollover | Certificati sincronizzati con Azure AD | I metadati della federazione sono accessibili pubblicamente | Validità | Azione |
|:---:|:---:|:---:|:---:|:---:|
| Sì |Sì |Sì |- |Non è richiesta alcuna azione. Vedere [Rinnovare automaticamente il certificato per la firma di token](#autorenew). |
| Sì |No |- |Meno di 15 giorni |Rinnovare immediatamente. Vedere [Rinnovare manualmente il certificato per la firma di token](#manualrenew). |
| No |- |- |Meno di 30 giorni |Rinnovare immediatamente. Vedere [Rinnovare manualmente il certificato per la firma di token](#manualrenew). |

\[-] Non è rilevante

## Rinnovare il token hello automaticamente il certificato di firma (scelta consigliata)<a name="autorenew"></a>
Non è necessario tooperform operazioni manuali se entrambe operazioni hello seguenti sono vere:

* È stato distribuito il Proxy applicazione Web, che consente di accedere ai metadati di federazione toohello da hello extranet.
* Si sta utilizzando una configurazione predefinita di hello ADFS (AutoCertificateRollover è abilitato).

Controllare hello seguente tooconfirm che hello certificato può essere aggiornato automaticamente.

**1. hello proprietà ADFS AutoCertificateRollover deve essere impostato tooTrue.** Indica che ADFS genererà automaticamente nuova firma di token e i certificati di decrittografia dei token, prima di quelli scadenza hello precedente.

**2. i metadati della federazione hello AD FS sono accessibili pubblicamente.** Verificare che i metadati di federazione siano accessibili pubblicamente passando toohello URL seguente da un computer hello internet pubblico (all'esterno delle rete aziendale hello):

https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml

dove `(your_FS_name) `viene sostituito con nome host del servizio federativo hello l'organizzazione utilizza, ad esempio fs.contoso.com.  Se si è in grado di tooverify di queste impostazioni correttamente, non è toodo qualsiasi altro elemento.  

Esempio: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Rinnovare il token hello manualmente il certificato di firma<a name="manualrenew"></a>
È possibile scegliere toorenew certificati di firma del token hello manualmente. Ad esempio, hello negli scenari seguenti potrebbero funzionare meglio per il rinnovo manuale:

* I certificati per la firma di token non sono certificati autofirmati. Hello più comune motivo è che l'organizzazione gestisce i certificati di ADFS registrati da un'autorità di certificazione dell'organizzazione.
* Sicurezza di rete non hello toobe metadati di federazione disponibili pubblicamente.

In questi scenari, ogni volta che si aggiorna il token hello firma dei certificati, è necessario aggiornare anche il dominio di Office 365 tramite comando PowerShell hello, Update-MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Passaggio 1: Verificare che in ADFS siamo disponibili nuovi certificati per la firma di token
**Configurazione non predefinita**

Se si utilizza una configurazione non predefinita di ADFS (in cui **AutoCertificateRollover** è troppo**False**), probabilmente si utilizza i certificati personalizzati (autofirmati). Per ulteriori informazioni sull'utilizzo dei certificati toorenew hello AD FS la firma di token, vedere [linee guida per i clienti che non usano ADFS i certificati autofirmati](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**I metadati della federazione non sono disponibili pubblicamente**

Hello d'altro canto, se **AutoCertificateRollover** è troppo**True**, ma i metadati di federazione non sono accessibili pubblicamente, assicurarsi innanzitutto che i nuovi certificati di firma di token sono stati generati da Active Directory ADFS. Verificare di che avere nuovo token di firma dei certificati da hello richiede alla procedura seguente:

1. Verificare che si è connessi nel server di toohello primaria AD FS.
2. Verificare i certificati di firma correnti hello in AD FS aprendo una finestra di comando di PowerShell ed eseguendo hello comando seguente:

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > Se si usa AD FS 2.0, è consigliabile eseguire prima Add-Pssnapin Microsoft.Adfs.Powershell.
   >
   >
3. Esaminare l'output del comando hello in tutti i certificati elencati. Se ADFS è stato generato un nuovo certificato, verrà visualizzato nell'output di hello due certificati: uno per i quali hello **IsPrimary** valore **True** hello e **NotAfter** Data all'interno di 5 giorni e quella per cui **IsPrimary** è **False** e **NotAfter** riguarda un anno in hello future.
4. Se solo un certificato e hello **NotAfter** data è entro 5 giorni, è necessario toogenerate un nuovo certificato.
5. toogenerate un nuovo certificato, eseguire hello comando al prompt dei comandi di PowerShell seguente: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Verificare l'aggiornamento hello eseguendo hello comando seguente nuovamente: c: PS\>Get-ADFSCertificate – CertificateType-la firma di token

Dovrebbero essere elencati due certificati, uno dei quali ha un **NotAfter** data di circa un anno nel futuro hello e quali hello **IsPrimary** valore **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Passaggio 2: Aggiornare nuovo token hello firma dei certificati per l'attendibilità hello Office 365
Aggiornamento di Office 365 con hello nuovi token firma i certificati toobe utilizzato per l'attendibilità di hello, come indicato di seguito.

1. Aprire hello modulo dei Microsoft Azure Active Directory per Windows PowerShell.
2. Eseguire $cred=Get-Credential. Quando questo cmdlet richiede le credenziali, digitare le credenziali dell'account amministratore servizio cloud.
3. Eseguire Connect-MsolService –Credential $cred. Questo cmdlet si connette il servizio di cloud toohello. Creazione di un contesto che consente la connessione del servizio cloud toohello è necessario prima di eseguire uno dei cmdlet di hello aggiuntivi installati dallo strumento hello.
4. Se si eseguono questi comandi in un computer che non è un server federativo primario hello ADFS, eseguire Set-MSOLAdfscontext-Computer <AD FS primary server>, dove <AD FS primary server> è nome FQDN interno hello del server di hello primario AD FS. Questo cmdlet crea un contesto che consente di connettersi tooAD ADFS.
5. Eseguire Update-MSOLFederatedDomain –DomainName <domain>. Questo cmdlet Aggiorna le impostazioni di hello da ADFS nel servizio cloud hello e configura hello relazione di trust tra due hello.

> [!NOTE]
> Se è necessario toosupport più domini di primo livello, ad esempio contoso.com e fabrikam.com, è necessario utilizzare hello **SupportMultipleDomain** con qualsiasi cmdlet. Per altre informazioni, vedere [Supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).
>
>

## Ripristinare il trust di Azure AD con AD Connect <a name="connectrenew"></a>
Se è configurata la farm di ADFS e trust di Azure AD mediante Azure AD Connect, è possibile utilizzare Azure AD Connect toodetect se è necessario tootake alcuna azione per il token di firma dei certificati. Se sono necessari i certificati di hello toorenew, è possibile utilizzare così toodo di Azure AD Connect.

Per ulteriori informazioni, vedere [ripristino trust hello](active-directory-aadconnect-federation-management.md).
