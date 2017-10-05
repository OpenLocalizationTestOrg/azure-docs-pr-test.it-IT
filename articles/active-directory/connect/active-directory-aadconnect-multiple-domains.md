---
title: Domini multipli di Azure AD Connect
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Supporto di più domini per la federazione con Azure AD
La documentazione seguente fornisce indicazioni su come usare più domini di primo livello e sottodomini durante la federazione con domini di Office 365 o Azure AD.

## <a name="multiple-top-level-domain-support"></a>Supporto di più domini di primo livello
Per la federazione di più domini di primo livello con Azure AD sono necessarie alcune operazioni di configurazione aggiuntive che non sono obbligatorie per la federazione con un dominio di primo livello.

Quando un dominio è federato con Azure AD, alcune proprietà vengono impostate nel dominio in Azure.  Una proprietà importante è IssuerUri.  Si tratta di un URI usato da Azure AD per identificare il dominio a cui è associato il token.  Non è necessario che l'URI venga risolto, ma deve essere un URI valido.  Per impostazione predefinita, Azure AD lo imposta sul valore dell'identificatore del servizio federativo nella configurazione locale di AD FS.

> [!NOTE]
> L'identificatore del servizio federativo è un URI che identifica in modo univoco un servizio federativo.  Il servizio federativo è un'istanza di AD FS che funge da servizio token di sicurezza. 
> 
> 

È possibile visualizzare IssuerUri usando il comando `Get-MsolDomainFederationSettings -DomainName <your domain>`di PowerShell.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Si verifica un problema quando si vogliono aggiungere più domini di primo livello.  Ad esempio, si supponga di avere configurato la federazione tra Azure AD e l'ambiente locale.  Per questo documento si usa bmcontoso.com.  Viene quindi aggiunto un secondo dominio di primo livello, bmfabrikam.com.

![Domini](./media/active-directory-multiple-domains/domains.png)

Quando si prova a convertire il dominio bmfabrikam.com in modo che sia federato, viene visualizzato un errore.  La causa dell'errore è un vincolo di Azure AD che non consente alla proprietà IssuerUri di avere lo stesso valore per più di un dominio.  

![Errore della federazione](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parametro SupportMultipleDomain
Per risolvere il problema, è necessario aggiungere una proprietà IssuerUri diversa, usando il parametro `-SupportMultipleDomain` .  Questo parametro viene usato con i cmdlet seguenti:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Questo parametro consente ad Azure AD di configurare IssuerUri in modo che sia basata sul nome del dominio.  Questo valore sarà univoco nelle directory di Azure AD.  L'uso del parametro consente il completamento corretto del comando di PowerShell.

![Errore della federazione](./media/active-directory-multiple-domains/convert.png)

Se si esaminano le impostazioni del nuovo dominio bmfabrikam.com, si può notare quanto segue:

![Errore della federazione](./media/active-directory-multiple-domains/settings.png)

Si noti che `-SupportMultipleDomain` non modifica gli altri endpoint, che sono ancora configurati in modo da fare riferimento al servizio federativo su adfs.bmcontoso.com.

`-SupportMultipleDomain` consente anche di assicurare che il sistema AD FS includa il valore Issuer appropriato nei token emessi per Azure AD, selezionando la porzione relativa al dominio del valore UPN degli utenti e impostandola come dominio in IssuerUri, ovvero https://{upn suffix}/adfs/services/trust. 

In questo modo durante l'autenticazione in Azure AD oppure Office 365 l'elemento IssuerUri nel token dell'utente viene usato per individuare il dominio in Azure AD.  Se non viene rilevata una corrispondenza, l'autenticazione non riuscirà. 

Ad esempio, se un utente UPN è bsimon@bmcontoso.com, l'elemento IssuerUri i problemi di token AD FS verrà impostato su http://bmcontoso.com/adfs/services/trust. Se questo corrisponde alla configurazione di Azure AD, l'autenticazione avrà esito positivo.

Di seguito è riportata la regola attestazioni personalizzata che implementa questa logica:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> Per usare l'opzione -SupportMultipleDomain quando si prova ad aggiungere o convertire domini già aggiunti, è necessario che il trust federativo sia stato configurato per supportarli in origine.  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a>Come aggiornare il trust tra AD FS e Azure AD
Se il trust federativo non è stato configurato tra AD FS e l'istanza di Azure AD, potrebbe essere necessario crearlo di nuovo,  perché, quando viene configurato in origine senza il parametro `-SupportMultipleDomain`, il valore IssuerUri viene impostato con il valore predefinito.  Nella schermata seguente è possibile vedere che IssuerUri è impostato su https://adfs.bmcontoso.com/adfs/services/trust.

Se un nuovo dominio è stato aggiunto correttamente al portale di Azure AD e si prova a convertirlo usando `Convert-MsolDomaintoFederated -DomainName <your domain>`, verrà visualizzato l'errore seguente.

![Errore della federazione](./media/active-directory-multiple-domains/trust1.png)

Se si prova ad aggiungere l'opzione `-SupportMultipleDomain` , verrà visualizzato l'errore seguente:

![Errore della federazione](./media/active-directory-multiple-domains/trust2.png)

Se si prova semplicemente a eseguire `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` nel dominio originale, verrà visualizzato un errore.

![Errore della federazione](./media/active-directory-multiple-domains/trust3.png)

Usare la procedura seguente per aggiungere un dominio di primo livello aggiuntivo.  Se è già stato aggiunto un dominio e non è stato usato il parametro `-SupportMultipleDomain` , iniziare dalla procedura per la rimozione e l'aggiornamento del dominio originale.  Se il dominio di primo livello non è stato ancora aggiunto, è possibile iniziare dalla procedura per l'aggiunta di un dominio usando comandi PowerShell di Azure AD Connect.

Usare la procedura seguente per rimuovere il trust di Microsoft Online e aggiornare il dominio originale.

1. Nel server federativo di AD FS aprire **Gestione AD FS** 
2. Sulla sinistra espandere **Relazioni di attendibilità** e **Attendibilità componente**
3. Sulla destra eliminare la voce **Piattaforma delle identità di Microsoft Office 365** .
   ![Rimozione di Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. Nel computer in cui è installato il [Modulo di Microsoft Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) eseguire il comando seguente: `$cred=Get-Credential`.  
5. Immettere il nome utente e la password di un amministratore globale di Azure AD con cui si esegue la federazione.
6. In PowerShell immettere `Connect-MsolService -Credential $cred`
7. In PowerShell immettere `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Questa impostazione è relativa al dominio originale.  Usando i domini precedenti, si ottiene quindi: `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Usare la procedura seguente per aggiungere il nuovo dominio di primo livello tramite PowerShell

1. Nel computer in cui è installato il [Modulo di Microsoft Azure Active Directory per Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) eseguire il comando seguente: `$cred=Get-Credential`.  
2. Immettere il nome utente e la password di un amministratore globale di Azure AD con cui si esegue la federazione.
3. In PowerShell immettere `Connect-MsolService -Credential $cred`
4. In PowerShell immettere `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Usare la procedura seguente per aggiungere il nuovo dominio di primo livello tramite Azure AD Connect.

1. Avviare Azure AD Connect dal desktop o dal menu Start.
2. Scegliere "Aggiunta di un altro dominio di Azure AD" ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add1.png)
3. Immettere le credenziali di Azure AD e Active Directory.
4. Selezionare il secondo dominio da configurare per la federazione.
   ![Aggiunta di un altro dominio di Azure AD](./media/active-directory-multiple-domains/add2.png)
5. Fare clic su Installa.

### <a name="verify-the-new-top-level-domain"></a>Verificare il nuovo dominio di primo livello
Usando il comando `Get-MsolDomainFederationSettings -DomainName <your domain>`di PowerShell, è possibile visualizzare la proprietà IssuerUri aggiornata.  La schermata seguente mostra le impostazioni di federazione aggiornate sul dominio originale http://bmcontoso.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

E IssuerUri sul nuovo dominio è stato impostato su https://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Supporto per sottodomini
A causa della modalità di gestione dei domini in Azure AD, eventuali sottodomini aggiunti erediteranno le impostazioni del dominio padre.  La proprietà IssuerUri deve quindi corrispondere a quella degli elementi padre.

Si supponga ad esempio che sia presente il dominio bmcontoso.com e che quindi si aggiunga corp.bmcontoso.com.  Ciò significa che IssuerUri per un utente di corp.bmcontoso.com dovrà essere **http://bmcontoso.com/adfs/services/trust.**  Tuttavia la regola standard implementata sopra per Azure AD genererà un token con un emittente come **http://corp.bmcontoso.com/adfs/services/trust.** che non corrisponderà al valore di dominio obbligatorio e l'autenticazione avrà esito negativo.

### <a name="how-to-enable-support-for-sub-domains"></a>Come abilitare il supporto per sottodomini
Per risolvere questo problema, è necessario che il trust della relying party di AD FS per Microsoft Online venga aggiornato.  Per eseguire questa operazione, è necessario configurare una regola attestazioni personalizzata, in modo che vengano rimossi tutti i sottodomini dal suffisso UPN di un utente durante la creazione del valore Issuer personalizzato. 

L'attestazione seguente consente di eseguire questa operazione:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
L'ultimo numero dell'espressione regolare imposta il numero di domini padre presente nel dominio radice. In bmcontoso.com sono necessari due domini padre. Se fossero necessari tre domini padre (ad esempio: corp.bmcontoso.com), il numero sarebbe tre. È possibile indicare un intervallo, la corrispondenza sarà sempre in base al massimo dei domini. "{2,3}" corrisponde a due o tre domini (ad esempio: bmfabrikam.com e corp.bmcontoso.com).

Usare la procedura seguente per aggiungere un'attestazione personalizzata per il supporto dei sottodomini.

1. Aprire Gestione AD FS.
2. Fare clic con il pulsante destro del mouse sul trust della relying party di Microsoft Online RP quindi scegliere Modifica regole attestazione.
3. Selezionare la terza regola attestazioni e sostituire ![Modifica dell'attestazione](./media/active-directory-multiple-domains/sub1.png)
4. Sostituire l'attestazione corrente:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Sostituzione dell'attestazione](./media/active-directory-multiple-domains/sub2.png)

5. Fare clic su Ok.  Fare clic su Applica.  Fare clic su Ok.  Chiudere Gestione ADFS.

