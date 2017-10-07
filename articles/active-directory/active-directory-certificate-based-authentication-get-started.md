---
title: aaaAzure l'autenticazione basata sui certificati di Active Directory - introduzione | Documenti Microsoft
description: Informazioni su come l'autenticazione basata su certificati tooconfigure nell'ambiente in uso
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Introduzione all'autenticazione basata su certificati di Azure Active Directory

Autenticazione basata su certificati consente toobe autenticato da Azure Active Directory con un certificato client in un dispositivo Windows, Android o iOS, quando ci si connette l'account di Exchange online a: 

- Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word   

- Client Exchange ActiveSync (EAS) 

Configurazione di questa funzionalità Elimina hello necessità tooenter un nome utente e la combinazione di password in determinate posta elettronica e le applicazioni di Microsoft Office sul tuo dispositivo mobile. 

In questo argomento:

- Fornisce hello tooconfigure i passaggi e utilizzare l'autenticazione basata su certificati per gli utenti del tenant Office 365 Enterprise, Business, Education e piani di governo degli Stati Uniti. Questa funzionalità è disponibile in anteprima nei piani Office 365 China, US Government Defense e US Government Federal. 

- Si presuppone che siano già configurati un'[infrastruttura a chiave pubblica (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [AD FS](connect/active-directory-aadconnectfed-whatis.md).    


## <a name="requirements"></a>Requisiti

l'autenticazione basata su certificato tooconfigure, hello devono verificarsi condizioni seguenti:  

- L'autenticazione basata sui certificati è supportata solo per ambienti federati per applicazioni browser o client nativi che usano l'autenticazione moderna (ADAL). Hello unica eccezione è Exchange Active Sync (EAS) per EXO che può essere utilizzato per gli account di entrambi, federati e gestiti. 

- autorità di certificazione radice Hello e qualsiasi autorità di certificazione intermedie devono essere configurati in Azure Active Directory.  

- Ogni autorità di certificazione deve avere un elenco di revoche di certificati (Certificate Revocation List o CRL) a cui si possa fare riferimento tramite un URL Internet.  

- È necessario che in Azure Active Directory sia configurata almeno un'autorità di certificazione. È possibile trovare passaggi correlati in hello [configurare le autorità di certificazione hello](#step-2-configure-the-certificate-authorities) sezione.  

- Per i client di Exchange ActiveSync, certificato client hello necessario hello instradabile elettronica utente indirizzo di Exchange online in entrambi hello nome dell'entità o valore del campo nome alternativo oggetto hello Nome RFC822 hello. Azure Active Directory esegue il mapping attributo hello RFC822 value toohello indirizzo Proxy nella directory hello.  

- Il dispositivo client deve avere accesso tooat almeno una autorità di certificazione che emette i certificati client.  

- Un certificato client per l'autenticazione del client deve essere stato rilasciato tooyour client.  




## <a name="step-1-select-your-device-platform"></a>Passaggio 1: Selezionare la piattaforma del dispositivo

Come primo passaggio, per la piattaforma del dispositivo hello che è rilevante, è necessario tooreview hello segue:

- supporto di applicazioni per dispositivi mobili Office Hello 
- Hello specifici requisiti di implementazione  

Hello correlate informazioni esistono per hello seguenti piattaforme per dispositivi:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Passaggio 2: Configurare le autorità di certificazione hello 

tooconfigure l'autorità di certificazione in Azure Active Directory, per ogni autorità di certificazione, caricare hello seguenti: 

* Hello parte pubblica del certificato hello, in *con estensione cer* formato 
* Hello per Internet URL in cui hello degli elenchi di revoche di certificati (CRL) si trovano

schema di Hello per un'autorità di certificazione è simile al seguente: 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Per la configurazione di hello, è possibile utilizzare hello [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Avviare Windows PowerShell con privilegi amministrativi. 
2. Installare il modulo hello Azure AD. È necessario tooinstall versione [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) o versione successiva.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Come primo passaggio di configurazione, è necessario tooestablish una connessione con il tenant. Non appena un tenant tooyour connessione esiste, è possibile esaminare, aggiungere, eliminare e modificare le autorità di certificazione attendibile hello definiti nella directory. 

### <a name="connect"></a>Connettere

una connessione con il tenant, usare hello tooestablish [Connetti AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Recupero 

le autorità di certificazione attendibile hello tooretrieve definiti nella directory, utilizzare hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Add

toocreate un'autorità di certificazione, usare hello [New AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet e set hello **crlDistributionPoint** tooa corretto valore dell'attributo: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Rimuovere

tooremove un'autorità di certificazione, usare hello [Remove AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modificare

toomodify un'autorità di certificazione, usare hello [Set AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Passaggio 3: Configurare la revoca

un certificato client, Azure Active Directory toorevoke Recupera certificato hello elenco di revoche di certificati (CRL) dagli URL hello caricato come parte di informazioni autorità di certificazione e lo memorizza nella cache. Hello all'ultima pubblicazione timestamp (**data di validità** proprietà) in hello CRL viene utilizzato tooensure hello CRL è ancora valido. Hello CRL è toocertificates accesso toorevoke periodicamente con cui viene fatto riferimento che fanno parte dell'elenco di hello.

Se una revoca più immediata è necessaria (ad esempio, se un utente perde un dispositivo), il token di autorizzazione hello dell'utente hello può essere invalidato. tooinvalidate hello autorizzazione token, impostare hello **StsRefreshTokenValidFrom** campo per l'utente con Windows PowerShell. È necessario aggiornare hello **StsRefreshTokenValidFrom** campo per ogni utente che si desidera accedere toorevoke per.

tooensure che revoca hello persiste, è necessario impostare hello **data di validità** di hello CRL tooa data hello valore impostato da **StsRefreshTokenValidFrom** e verificare che certificato hello in questione sia Hello CRL.

Hello seguendo i passaggi struttura hello processo per aggiornare e invalidare il token di autorizzazione hello dall'impostazione hello **StsRefreshTokenValidFrom** campo. 

**revoca tooconfigure:** 

1. Connettersi con il servizio di MSOL toohello credenziali di amministratore: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Recuperare hello corrente StsRefreshTokensValidFrom valore per un utente: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Configurare un nuovo valore StsRefreshTokensValidFrom per timestamp corrente di hello utente toohello uguale: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

deve essere futura hello data Hello che è impostata. Se data hello non hello future, hello **StsRefreshTokensValidFrom** non è impostata. Se la data hello è nel futuro, hello **StsRefreshTokensValidFrom** è impostata l'ora corrente (non hello date indicata dal comando Set-MsolUser) toohello. 


## <a name="step-4-test-your-configuration"></a>Passaggio 4: Testare la configurazione

### <a name="testing-your-certificate"></a>Test del certificato

Come un primo test della configurazione, è consigliabile toosign in troppo[Outlook Web Access](https://outlook.office365.com) o [SharePoint Online](https://microsoft.sharepoint.com) utilizzando il **browser sul dispositivo**.

Se l'accesso ha esito positivo significa che:

- certificato utente Hello è stato sottoposto a provisioning tooyour test dispositivo
- AD FS è configurato correttamente  


### <a name="testing-office-mobile-applications"></a>Test delle applicazioni Office per dispositivi mobili

**autenticazione basata su certificati tootest sull'applicazione di Office per dispositivi mobili:** 

1. Nel dispositivo di test installare un'applicazione Office per dispositivi mobili (ad esempio OneDrive).
3. Avvia un'applicazione hello. 
4. Immettere il nome utente e quindi selezionare il certificato di utente hello desiderato toouse. 

È necessario aver eseguito l'accesso. 

### <a name="testing-exchange-activesync-client-applications"></a>Test delle applicazioni client Exchange ActiveSync

tooaccess Exchange ActiveSync (EAS) tramite l'autenticazione basata su certificato, un profilo EAS contenente hello client certificato deve essere disponibile toohello applicazione. 

Hello profilo EAS deve contenere hello le seguenti informazioni:

- Hello toobe certificato utente utilizzato per l'autenticazione 

- endpoint EAS Hello (ad esempio, outlook.office365.com)

Un profilo EAS può essere configurato e sul dispositivo hello tramite l'utilizzo di gestione dei dispositivi mobili (MDM), ad esempio Intune o inserendo manualmente il certificato di hello in hello profilo EAS sul dispositivo hello hello.  

### <a name="testing-eas-client-applications-on-android"></a>Test delle applicazioni client EAS in Android

**autenticazione del certificato tootest:**  

1. Configurare un profilo EAS in un'applicazione hello che soddisfi i requisiti di hello precedenti.  
2. Aprire un'applicazione hello e verificare che la sincronizzazione della posta. 

