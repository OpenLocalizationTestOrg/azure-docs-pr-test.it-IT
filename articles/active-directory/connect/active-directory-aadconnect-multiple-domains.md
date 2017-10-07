---
title: "aaaAzure AD connettersi più domini"
description: "Questo documento descrive l'impostazione e la configurazione di più domini di primo livello con Office 365 e Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Supporto di più domini per la federazione con Azure AD
Hello documentazione riportata di seguito vengono fornite indicazioni su come toouse più domini di primo livello e i sottodomini quando la federazione con Office 365 o Azure AD domini.

## <a name="multiple-top-level-domain-support"></a>Supporto di più domini di primo livello
Per la federazione di più domini di primo livello con Azure AD sono necessarie alcune operazioni di configurazione aggiuntive che non sono obbligatorie per la federazione con un dominio di primo livello.

Quando un dominio è federato con Azure AD, vengono impostate diverse proprietà dominio hello in Azure.  Una proprietà importante è IssuerUri.  Si tratta di un URI che viene usato in Azure AD tooidentify dominio hello hello token è associato.  Hello URI non è necessario tooresolve tooanything ma deve essere un URI valido.  Per impostazione predefinita, Azure AD questo valore viene impostato toohello dell'identificatore del servizio federativo hello in locale ADFS configurazione.

> [!NOTE]
> Identificatore del servizio federativo Hello è un URI che identifica in modo univoco un servizio federativo.  servizio federativo Hello è un'istanza di AD FS che funziona come servizio token di sicurezza hello. 
> 
> 

È possibile visualizzare IssuerUri usando il comando di PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Si verifica un problema quando si desidera tooadd più di un dominio di primo livello.  Ad esempio, si supponga di avere configurato la federazione tra Azure AD e l'ambiente locale.  Per questo documento si usa bmcontoso.com.  Viene quindi aggiunto un secondo dominio di primo livello, bmfabrikam.com.

![Domini](./media/active-directory-multiple-domains/domains.png)

Quando si tenta di tooconvert nostri toobe dominio bmfabrikam.com federata, è visualizzato un errore.  Hello questo accade, Azure AD con un vincolo che non consente hello hello toohave di proprietà IssuerUri stesso valore per più di un dominio.  

![Errore della federazione](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parametro SupportMultipleDomain
tooworkaround, è necessario un IssuerUri diversi che possono essere eseguiti utilizzando hello tooadd `-SupportMultipleDomain` parametro.  Questo parametro viene utilizzato con hello seguente cmdlet:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Questo parametro consente AD Azure configurare hello IssuerUri in modo che è basato su nome hello del dominio di hello.  Questo valore sarà univoco nelle directory di Azure AD.  Utilizzando il parametro hello consente hello PowerShell comando toocomplete correttamente.

![Errore della federazione](./media/active-directory-multiple-domains/convert.png)

Esaminano impostazioni hello del nuovo dominio bmfabrikam.com si può vedere seguente hello:

![Errore della federazione](./media/active-directory-multiple-domains/settings.png)

Si noti che `-SupportMultipleDomain` invariato di hello altri endpoint che sono ancora configurate servizio federativo di toopoint tooour nella adfs.bmcontoso.com.

Un altro aspetto che `-SupportMultipleDomain` does che assicura che sistema di hello AD FS include il valore dell'autorità di certificazione corretta di hello nel token rilasciato per Azure AD. A tale scopo eseguire parte di utenti hello UPN di dominio hello e questa impostazione come dominio hello in hello IssuerUri, vale a dire https://{upn suffisso} / adfs/services/trust. 

In questo modo durante l'autenticazione tooAzure AD o Office 365, hello IssuerUri elemento token dell'utente hello è dominio hello toolocate usato in Azure AD.  Se non è possibile trovare una corrispondenza hello autenticazione avrà esito negativo. 

Ad esempio, se un utente UPN è bsimon@bmcontoso.com, elemento IssuerUri hello in problemi relativi AD ADFS token hello imposterà toohttp://bmcontoso.com/adfs/services/trust. La configurazione di Azure AD hello verrà trovata corrispondenza e l'autenticazione avrà esito positivo.

di seguito Hello è regola attestazione personalizzata hello che implementa questa logica:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> In ordine toouse hello - SupportMultipleDomain passare quando si tenta di nuovo tooadd o convertire già aggiunti domini, è necessario toohave toosupport la relazione di trust federativa del programma di installazione li originariamente.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Come tooupdate hello trust tra ADFS e Azure AD
Se hello federata trust tra ADFS e l'istanza di Azure AD non è stata configurata, potrebbe essere necessario toore-creare il trust.  Questo avviene perché, quando è originariamente il programma di installazione senza hello `-SupportMultipleDomain` parametro hello IssuerUri è impostato con il valore predefinito di hello.  In hello schermata seguente è possibile visualizzare hello IssuerUri impostata toohttps://adfs.bmcontoso.com/adfs/services/trust.

In questo momento, se è stato aggiunto correttamente un nuovo dominio nel portale di Azure AD hello e quindi tentare tooconvert utilizzando `Convert-MsolDomaintoFederated -DomainName <your domain>`, si ottiene hello errore seguente.

![Errore della federazione](./media/active-directory-multiple-domains/trust1.png)

Se si tenta di hello tooadd `-SupportMultipleDomain` commutatore verranno inviati hello errore seguente:

![Errore della federazione](./media/active-directory-multiple-domains/trust2.png)

Durante il tentativo semplicemente toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` su hello dominio originale inoltre genererà un errore.

![Errore della federazione](./media/active-directory-multiple-domains/trust3.png)

Attenersi alla procedura hello sotto tooadd un dominio di primo livello aggiuntivo.  Se si dispone già aggiunto un dominio e non è stata utilizzata hello `-SupportMultipleDomain` parametro start con passaggi hello per eliminare e aggiornare il dominio originale.  Se non è stato aggiunto un dominio di primo livello ancora è possibile iniziare con la procedura di hello per aggiungere un dominio con PowerShell di Azure AD Connect.

Utilizzare hello seguendo i passaggi tooremove hello Microsoft Online trust e aggiornare il dominio originale.

1. Nel server federativo di AD FS aprire **Gestione AD FS** 
2. A sinistra di hello, espandere **relazioni di Trust** e **Relying Party Trusts**
3. In hello destra, l'eliminazione di hello **piattaforma delle identità di Microsoft Office 365** voce.
   ![Rimozione di Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. In un computer dotato di [modulo di Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installato eseguire hello seguente: `$cred=Get-Credential`.  
5. Immettere hello username e password di un amministratore globale per il dominio di Azure AD hello che con federazione
6. In PowerShell immettere `Connect-MsolService -Credential $cred`
7. In PowerShell immettere `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Si tratta di dominio originale hello.  Quindi l'uso di hello precedente domini che sarebbe:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Utilizzare hello seguendo i passaggi tooadd hello nuovo dominio di primo livello con PowerShell

1. In un computer dotato di [modulo di Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installato eseguire hello seguente: `$cred=Get-Credential`.  
2. Immettere hello username e password di un amministratore globale per il dominio di Azure AD hello che con federazione
3. In PowerShell immettere `Connect-MsolService -Credential $cred`
4. In PowerShell immettere `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Utilizzare hello seguendo i passaggi tooadd hello nuovo dominio di primo livello con Azure AD Connect.

1. Avvio di Azure AD Connect, da desktop hello o menu start
2. Scegliere "Aggiunta di un altro dominio di Azure AD" ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add1.png)
3. Immettere le credenziali di Azure AD e Active Directory.
4. Selezionare il dominio di secondo hello desiderato tooconfigure per la federazione.
   ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add2.png)
5. Fare clic su Installa.

### <a name="verify-hello-new-top-level-domain"></a>Verificare il dominio di primo livello nuovo hello
Tramite il comando di PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`è possibile visualizzare hello aggiornato IssuerUri.  Hello schermata riportata di seguito viene illustrato l'aggiornamento delle impostazioni di federazione hello nel nostro http://bmcontoso.com/adfs/services/trust dominio originale

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

E hello IssuerUri nel nuovo dominio è stato impostato toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Supporto per sottodomini
Quando si aggiunge un sottodominio, a causa di hello modo Azure AD gestite domini, erediterà le impostazioni di hello del padre hello.  Ciò significa che hello IssuerUri deve padri hello toomatch.

Si supponga ad esempio che sia presente il dominio bmcontoso.com e che quindi si aggiunga corp.bmcontoso.com.  Ciò significa che hello IssuerUri per un utente da corp.bmcontoso.com necessario toobe **http://bmcontoso.com/adfs/services/trust.**  Tuttavia la regola standard hello implementato sopra per Azure AD, verrà generato un token con un emittente come **http://corp.bmcontoso.com/adfs/services/trust.** valore obbligatorio del dominio hello che non corrispondono e l'autenticazione avrà esito negativo.

### <a name="how-tooenable-support-for-sub-domains"></a>La modalità di supporto tooenable per i sottodomini
In ordine toowork attorno a questa hello ADFS trust della relying party per Microsoft Online deve toobe aggiornato.  toodo, è necessario configurare una regola attestazioni personalizzata in modo che rimuove tutti i sottodomini dal suffisso UPN dell'utente hello durante la costruzione di valore dell'autorità di certificazione personalizzato hello. 

Hello seguente attestazione eseguirà questo:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
ultimo numero di Hello nell'espressione regolare hello imposta hello il numero di domini padre è presente nel dominio radice. In bmcontoso.com sono necessari due domini padre. Se tre padre domini sono stati mantenuti toobe (ad esempio: corp.bmcontoso.com), quindi il numero di hello sarebbe stata tre. Eventualy un intervallo possono essere indicati, corrispondenza hello verrà sempre effettuato massimo hello toomatch dei domini. "{2,3}", verranno restituiti due domini toothree (ad esempio: bmfabrikam.com e corp.bmcontoso.com).

Questa procedura hello utilizzare tooadd un'attestazione personalizzata toosupport i sottodomini.

1. Aprire Gestione AD FS.
2. Fare clic con il pulsante destro trust relying Party Online Microsoft hello e scegliere regole attestazione di modifica
3. Selezionare una regola attestazioni terzo hello e sostituire ![richiesta di modifica](./media/active-directory-multiple-domains/sub1.png)
4. Sostituire attestazioni corrente hello:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Sostituzione dell'attestazione](./media/active-directory-multiple-domains/sub2.png)

5. Fare clic su Ok.  Fare clic su Applica.  Fare clic su Ok.  Chiudere Gestione ADFS.

