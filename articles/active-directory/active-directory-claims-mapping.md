---
title: Mapping delle attestazioni in Azure Active Directory (anteprima pubblica)| Microsoft Docs
description: Questa pagina descrive il mapping delle attestazioni di Azure Active Directory.
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Mapping delle attestazioni in Azure Active Directory (anteprima pubblica)

>[!NOTE]
>Questa funzionalità sostituisce e sostituisce hello [attestazioni personalizzazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offerti tramite il portale di hello oggi. Se si personalizzano le attestazioni usando il portale di hello inoltre toohello metodo grafico/PowerShell disponibili in questo documento su hello stessa applicazione, i token emessi per tale applicazione verrà ignorata configurazione hello hello portale.
Le configurazioni effettuate tramite metodi hello descritti in questo documento non si rifletteranno nel portale di hello.

Questa funzionalità viene usata per le attestazioni hello toocustomize amministratori tenant generate nei token per un'applicazione specifica al proprio tenant. È possibile usare i criteri di mapping delle attestazioni per:

- Selezionare le attestazioni che vengono incluse nei token.
- Creare tipi di attestazione non esistenti.
- Scegliere o modificare hello origine dei dati generati in attestazioni specifiche.

>[!NOTE]
>Questa funzionalità è attualmente disponibile in anteprima pubblica. Essere preparati toorevert o rimuovere tutte le modifiche. funzionalità di Hello è disponibile in alcuna sottoscrizione di Azure Active Directory (Azure AD) durante l'anteprima pubblica. Tuttavia, quando la funzionalità hello diventa disponibile in genere, alcuni aspetti della funzionalità hello potrebbero richiedere una sottoscrizione di Azure Active Directory premium.

## <a name="claims-mapping-policy-type"></a>Tipo di criteri di mapping di attestazioni
In Azure AD un oggetto **Criteri** rappresenta un set di regole imposto su singole applicazioni o su tutte le applicazioni in un'organizzazione. Ogni tipo di criteri presenta una struttura univoca, con un set di proprietà che vengono quindi applicati toowhich tooobjects che sono assegnati.

Le attestazioni di un mapping dei criteri è un tipo di **criteri** oggetto che modifica hello attestazioni generato nel token rilasciato per applicazioni specifiche.

## <a name="claim-sets"></a>Set di attestazioni
Alcuni set di attestazioni definiscono come e quando vengono utilizzate nei token.

### <a name="core-claim-set"></a>Set di attestazioni core
Presenti nel core hello attestazioni set sono presenti in ogni token, indipendentemente dal criterio. Queste attestazioni sono anche considerate limitate e non possono essere modificate.

### <a name="basic-claim-set"></a>Set di attestazioni di base
set di attestazioni di base Hello include le attestazioni di hello generati per impostazione predefinita per i token (nel set di attestazioni core toohello aggiunta). Queste attestazioni possono essere omessa o deve essere modificate mediante attestazioni hello mapping dei criteri.

### <a name="restricted-claim-set"></a>Set di attestazioni con restrizioni
Le attestazioni con restrizioni non possono essere modificate usando i criteri. Impossibile modificare l'origine dati Hello e non viene applicata alcuna trasformazione durante la generazione di queste attestazioni.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tabella 1: Set di attestazioni limitate al token JSON Web (JWT)
|Tipo di attestazione (nome)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|assertion|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|code|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|password|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|resource|
|role|
|roles|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|username|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tabella 2: Set di attestazioni limitate Security Assertion Markup Language (SAML)
|Tipo di attestazione (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Proprietà di criteri di mapping di attestazioni
Utilizzare la proprietà hello di mapping toocontrol criteri quali attestazioni vengono generate e in cui i dati hello ha origine da attestazioni. Se non è impostato alcun criterio, sistema hello rilascia token contenente set di attestazioni core hello hello base set di attestazioni e le attestazioni facoltative hello applicazione ha scelto tooreceive.

### <a name="include-basic-claim-set"></a>Includere set di attestazioni di base

**Stringa:** IncludeBasicClaimSet

**Tipo di dati:** booleano (True o False)

**Riepilogo:** questa proprietà determina se il set di attestazioni di base di hello è inclusa nei token interessati da questo criterio. 

- Se set tooTrue, tutte le attestazioni nel set di attestazioni di base di hello viene generati nei token interessati dai criteri hello. 
- Se set tooFalse, le attestazioni nel set di attestazioni di base di hello non è nei token hello, a meno che non vengono singolarmente aggiunti nella proprietà di schema hello attestazioni di hello stesso criterio.

>[!NOTE] 
>Presenti nel core hello attestazioni presenti in ogni token indipendentemente dalle quali questa proprietà è impostata su set. 

### <a name="claims-schema"></a>Schema di attestazioni

**Stringa:** ClaimsSchema

**Tipo di dati:** BLOB JSON con una o più voci dello schema di attestazioni

**Riepilogo:** questa proprietà definisce quali attestazioni sono presenti nei token hello interessati dai criteri di hello, set di attestazioni toohello base inoltre e set di attestazioni core hello.
Per ogni voce di schema di attestazioni definita in questa proprietà sono necessarie alcune informazioni. È necessario specificare la provenienza dei dati hello (**valore** o **coppia origine/ID**), e di attestazione dati hello viene generato come (**tipo di attestazione**).

### <a name="claim-schema-entry-elements"></a>Elementi di voci dello schema di attestazioni

**Valore:** elemento Value hello definisce un valore statico come toobe dati hello generato nell'attestazione hello.

**Coppia di origine con ID:** hello origine e gli elementi ID definiscono i cui dati hello in hello attestazione proviene da. 

elemento Source Hello deve essere impostata tooone seguenti hello: 


- "utente": dati di hello hello attestazione è una proprietà sull'oggetto utente hello. 
- "applicazione": dati di hello hello attestazione è una proprietà di entità servizio dell'applicazione (client) hello. 
- "resource": dati di hello hello attestazione è una proprietà dell'entità servizio di risorsa hello.
- "audience": dati hello nell'attestazione hello sono una proprietà dell'entità servizio hello di destinatari hello del token hello (entrambi hello client o la risorsa entità servizio).
- "company": dati hello in hello è una proprietà sull'oggetto aziendale del tenant di hello risorsa di attestazione.
- "trasformazione": richiedere dati hello in hello dalla trasformazione delle attestazioni (vedere la sezione hello "trasformazione delle attestazioni" più avanti in questo articolo). 

Se l'origine hello trasformazione, hello **TransformationID** elemento deve essere incluso in questa definizione di attestazione anche.

elemento ID Hello identifica la proprietà sull'origine hello fornisce il valore di hello per hello attestazione. Hello nella tabella seguente sono elencati i valori hello dell'ID valido per ogni valore di origine.

#### <a name="table-3-valid-id-values-per-source"></a>Tabella 3: Valori di ID validi per ogni Source
|Sorgente|ID|Descrizione|
|-----|-----|-----|
|Utente|surname|Cognome|
|Utente|givenname|Nome|
|Utente|displayname|Nome visualizzato|
|Utente|objectId|ObjectID|
|Utente|mail|Indirizzo di posta elettronica|
|Utente|userprincipalname|Nome dell'entità utente|
|Utente|department|department|
|Utente|onpremisessamaccountname|Nome account SAM locale|
|Utente|netbiosname|Nome NetBios|
|Utente|dnsdomainname|Nome di dominio DNS|
|Utente|onpremisesecurityidentifier|ID di sicurezza locale|
|Utente|companyname|Nome organizzazione|
|Utente|streetaddress|Indirizzo|
|Utente|postalcode|CAP|
|Utente|preferredlanguange|Lingua preferita|
|Utente|onpremisesuserprincipalname|UPN locale|
|Utente|mailNickname|Nome di posta elettronica alternativo|
|Utente|extensionattribute1|Attributo di estensione 1|
|Utente|extensionattribute2|Attributo di estensione 2|
|Utente|extensionattribute3|Attributo di estensione 3|
|Utente|extensionattribute4|Attributo di estensione 4|
|Utente|extensionattribute5|Attributo di estensione 5|
|Utente|extensionattribute6|Attributo di estensione 6|
|Utente|extensionattribute7|Attributo di estensione 7|
|Utente|extensionattribute8|Attributo di estensione 8|
|Utente|extensionattribute9|Attributo di estensione 9|
|Utente|extensionattribute10|Attributo di estensione 10|
|Utente|extensionattribute11|Attributo di estensione 11|
|Utente|extensionattribute12|Attributo di estensione 12|
|Utente|extensionattribute13|Attributo di estensione 13|
|Utente|extensionattribute14|Attributo di estensione 14|
|Utente|extensionattribute15|Attributo di estensione 15|
|Utente|othermail|Posta elettronica alternativa|
|Utente|country|Paese|
|Utente|city|city|
|Utente|state|Stato|
|Utente|jobtitle|Posizione|
|Utente|employeeid|ID dipendente|
|Utente|facsimiletelephonenumber|Numero di telefono fax|
|application, resource, audience|displayname|Nome visualizzato|
|application, resource, audience|objected|ObjectID|
|application, resource, audience|tags|Tag di entità servizio|
|Azienda|tenantcountry|Paese del tenant|

**TransformationID:** elemento TransformationID hello deve essere disponibile solo se hello elemento di origine è stato impostato troppo "trasformazione".

- Questo elemento deve corrispondere elemento ID hello della voce di trasformazione hello in hello **ClaimsTransformation** proprietà che definisce la modalità di generazione dati hello per questa attestazione.

**Tipo di attestazione:** hello **JwtClaimType** e **SamlClaimType** elementi che definiscono quali attestazioni questa voce di schema richiesta fa riferimento a.

- Hello JwtClaimType deve contenere il nome di hello di hello attestazione toobe generato in Jwt.
- Hello SamlClaimType deve contenere hello URI di hello attestazione toobe generato nei token SAML.

>[!NOTE]
>I nomi e gli URI di attestazioni in hello limitato set non può essere utilizzato per gli elementi di tipo di attestazione hello attestazione. Per ulteriori informazioni, vedere sezione "Restrizioni e le eccezioni" hello, più avanti in questo articolo.

### <a name="claims-transformation"></a>Trasformazione delle attestazioni

**Stringa:** ClaimsTransformation

**Tipo di dati:** BLOB JSON con una o più voci di trasformazione 

**Riepilogo:** utilizzare proprietà tooapply comuni trasformazioni toosource i dati, dati di output di hello toogenerate per le attestazioni specificate nelle attestazioni Schema hello.

**ID:** utilizzare hello ID elemento tooreference questa voce di trasformazione nella voce di Schema attestazioni TransformationID hello. Questo valore deve essere univoco per ogni voce di trasformazione all'interno di questo criterio.

**TransformationMethod:** elemento TransformationMethod hello identifica quale operazione viene eseguita toogenerate hello dati di attestazione hello.

Basato sul metodo hello scelto, è previsto un set di input e output. Questi vengono definiti utilizzando hello **InputClaims**, **parametri di input** e **OutputClaims** elementi.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tabella 4: Metodi di trasformazione e input/output previsti
|TransformationMethod|Input previsto|Output previsto|Descrizione|
|-----|-----|-----|-----|
|Join|string1, string2, separator|outputClaim|Esegue il join di stringhe di input dividendole con un separatore. Ad esempio: stringa1: "foo@bar.com", stringa2: "sandbox", separatore: "." comporta in outputClaim: "foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|Estrae parte locale di hello di un indirizzo di posta elettronica. Ad esempio: mail:"foo@bar.com" comporta in outputClaim:"foo". Se non @ segno è presente, stringa di input originale hello viene restituito come è.|

**InputClaims:** utilizzare un InputClaims elemento toopass hello dati una trasformazione di attestazioni schema voce tooa. Include due attributi: **ClaimTypeReferenceId** e **TransformationClaimType**.

- **ClaimTypeReferenceId** è unita in join con elemento ID della hello attestazione schema voce toofind hello appropriato attestazione di input. 
- **TransformationClaimType** è toogive utilizzati come input di toothis un nome univoco. Questo nome deve corrispondere a uno degli input hello previsto per il metodo di trasformazione hello.

**Parametri di input:** utilizzare un toopass di elemento di parametri di input una trasformazione tooa valore costante. Include due attributi: **Value** e **ID**.

- **Valore** hello effettivo valore costante toobe passato.
- **ID** è toogive utilizzati come input di toothis un nome univoco. Questo nome deve corrispondere a uno degli input hello previsto per il metodo di trasformazione hello.

**OutputClaims:** utilizzare un OutputClaims elemento toohold hello di dati generati da una trasformazione e ricollegarlo tooa attestazione voce di schema. Include due attributi: **ClaimTypeReferenceId** e **TransformationClaimType**.

- **ClaimTypeReferenceId** è unita in join con ID hello dell'attestazione di output appropriato di hello attestazione schema voce toofind hello.
- **TransformationClaimType** è toogive usato un output toothis nome univoco. Questo nome deve corrispondere a uno di output di hello previsto per il metodo di trasformazione hello.

### <a name="exceptions-and-restrictions"></a>Eccezioni e restrizioni

**Elemento NameID di SAML e UPN:** hello gli attributi da cui si hello NameID UPN valori di origine e hello attestazioni trasformazioni che sono consentite, sono limitati.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tabella 5: Attributi consentiti come origine dati per NameID di SAML
|Sorgente|ID|Descrizione|
|-----|-----|-----|
|Utente|mail|Indirizzo di posta elettronica|
|Utente|userprincipalname|Nome dell'entità utente|
|Utente|onpremisessamaccountname|Nome account SAM locale|
|Utente|employeeid|ID dipendente|
|Utente|extensionattribute1|Attributo di estensione 1|
|Utente|extensionattribute2|Attributo di estensione 2|
|Utente|extensionattribute3|Attributo di estensione 3|
|Utente|extensionattribute4|Attributo di estensione 4|
|Utente|extensionattribute5|Attributo di estensione 5|
|Utente|extensionattribute6|Attributo di estensione 6|
|Utente|extensionattribute7|Attributo di estensione 7|
|Utente|extensionattribute8|Attributo di estensione 8|
|Utente|extensionattribute9|Attributo di estensione 9|
|Utente|extensionattribute10|Attributo di estensione 10|
|Utente|extensionattribute11|Attributo di estensione 11|
|Utente|extensionattribute12|Attributo di estensione 12|
|Utente|extensionattribute13|Attributo di estensione 13|
|Utente|extensionattribute14|Attributo di estensione 14|
|Utente|extensionattribute15|Attributo di estensione 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tabella 6: Metodi di trasformazione consentiti per NameID di SAML
|TransformationMethod|Restrizioni|
| ----- | ----- |
|ExtractMailPrefix|Nessuna|
|Join|suffisso Hello da unire in join deve essere un dominio verificato del tenant di risorsa hello.|

### <a name="custom-signing-key"></a>Chiave di firma personalizzata
Una chiave di firma personalizzata deve essere assegnata toohello oggetto entità di servizio per un effetto tootake criteri di mapping di attestazioni. Tutti i token emessi che sono stati influenzati dal criterio hello vengono firmati con questa chiave. Le applicazioni devono essere configurati tooaccept token firmato con la chiave. In questo modo si garantisce che i token sono stati modificati dall'autore hello di hello riconoscimento criteri di mapping di attestazioni. Le applicazioni vengono protette dai criteri di mapping delle attestazioni creati da attori dannosi.

### <a name="cross-tenant-scenarios"></a>Scenari tra tenant
Le attestazioni di mapping dei criteri si applicano agli utenti di tooguest. Se un utente guest tenta tooaccess un'applicazione con attestazioni tooits assegnati criteri di mapping del servizio principale, hello predefinito token viene rilasciato (criteri hello non ha effetto).

## <a name="claims-mapping-policy-assignment"></a>Assegnazione di criteri di mapping delle attestazioni
Criteri di mapping possono essere assegnati solo oggetti principal tooservice di attestazioni.

### <a name="example-claims-mapping-policies"></a>Criteri di mapping delle attestazioni di esempio

In molti scenari di Azure AD è possibile personalizzare le attestazioni generate nei token per specifiche entità servizio. In questa sezione vengono illustrate le alcuni scenari comuni che possono aiutarti a comprendere come toouse hello dichiara il tipo di criteri di mapping.

#### <a name="prerequisites"></a>Prerequisiti
In hello seguono esempi, creare, aggiornare, collegare ed eliminare i criteri per le entità servizio. Nel caso di nuova tooAzure Active Directory, è consigliabile conoscere la modalità del tenant tooget un Azure AD prima di procedere con questi esempi. 

hello tooget avviato, alla procedura seguente:


1. Download più recenti hello [versione di anteprima pubblica di Azure AD PowerShell modulo](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Eseguire hello Connetti comando toosign tooyour account amministratore di Azure AD. Eseguire questo comando ogni volta che si avvia una nuova sessione.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee tutti i criteri che sono stati creati all'interno dell'organizzazione, hello esecuzione dopo il comando. È consigliabile eseguire questo comando dopo la maggior parte delle operazioni hello seguenti scenari, toocheck che i criteri vengono creati come previsto.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Esempio: Creare e assegnare un criterio tooomit hello attestazioni di base da entità servizio tooa i token emessi.
In questo esempio, creare un criterio che rimuove il set di attestazioni di base di hello toolinked i token emessi entità servizio.


1. Creare i criteri di mapping delle attestazioni. Questo criterio, le entità di servizio collegato toospecific, rimuove il set di attestazioni di base di hello dai token.
    1. criteri di hello toocreate, eseguiti questo comando: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee il nuovo criterio e criteri di hello tooget ObjectId, hello esecuzione seguente comando:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Assegnare l'entità di servizio tooyour criteri hello. È inoltre necessario tooget hello ObjectId dell'entità del servizio. 
    1.  toosee le entità servizio tutti dell'organizzazione, è possibile eseguire query Microsoft Graph. In alternativa, in Azure AD Graph Explorer, eseguire l'accesso tooyour account Azure AD.
    2.  Quando si dispone di hello ObjectId dell'hello di entità, eseguire servizio comando seguente:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Esempio: Creare e assegnare un criterio tooinclude hello EmployeeID e TenantCountry attestazioni nei token emessi tooa entità di servizio.
In questo esempio, si crea un criterio che aggiunge hello EmployeeID e TenantCountry tootokens emesso toolinked entità servizio. Hello EmployeeID viene generato come tipo di attestazione nome hello in entrambi i token SAML e Jwt. Hello TenantCountry viene generato come paese hello attestazione di tipo sia token SAML e Jwt. In questo esempio, si continuano tooinclude hello base le attestazioni nei token hello impostate.

1. Creare i criteri di mapping delle attestazioni. Questo criterio, le entità di servizio collegato toospecific, aggiunge hello EmployeeID e TenantCountry tootokens di attestazioni.
    1. criteri di hello toocreate, eseguiti questo comando:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee il nuovo criterio e criteri di hello tooget ObjectId, hello esecuzione seguente comando:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Assegnare l'entità di servizio tooyour criteri hello. È inoltre necessario tooget hello ObjectId dell'entità del servizio. 
    1.  toosee le entità servizio tutti dell'organizzazione, è possibile eseguire query Microsoft Graph. In alternativa, in Azure AD Graph Explorer, eseguire l'accesso tooyour account Azure AD.
    2.  Quando si dispone di hello ObjectId dell'hello di entità, eseguire servizio comando seguente:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Esempio: Creare e assegnare un criterio che utilizza una trasformazione di attestazioni nell'entità servizio tooa i token emessi.
In questo esempio, creare un criterio che genera un'attestazione personalizzata "JoinedData" tooJWTs emesso toolinked le entità di servizio. Questa attestazione contiene un valore creato dall'unione di dati hello archiviati nell'attributo extensionattribute1 hello oggetto user hello con ".sandbox". In questo esempio, Microsoft esclude le attestazioni di base hello impostate nei token hello.


1. Creare i criteri di mapping delle attestazioni. Questo criterio, le entità di servizio collegato toospecific, aggiunge hello EmployeeID e TenantCountry tootokens di attestazioni.
    1. criteri di hello toocreate, eseguiti questo comando: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee il nuovo criterio e criteri di hello tooget ObjectId, hello esecuzione seguente comando: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Assegnare l'entità di servizio tooyour criteri hello. È inoltre necessario tooget hello ObjectId dell'entità del servizio. 
    1.  toosee le entità servizio tutti dell'organizzazione, è possibile eseguire query Microsoft Graph. In alternativa, in Azure AD Graph Explorer, eseguire l'accesso tooyour account Azure AD.
    2.  Quando si dispone di hello ObjectId dell'hello di entità, eseguire servizio comando seguente: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
