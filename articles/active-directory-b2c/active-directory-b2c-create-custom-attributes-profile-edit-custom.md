---
title: 'Azure Active B2C di Directory: Aggiungere i propri criteri toocustom gli attributi e utilizzare in Modifica profilo | Documenti Microsoft'
description: "Una procedura dettagliata sull'uso di proprietà di estensione, gli attributi personalizzati e vengono inclusi nell'interfaccia utente di hello"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: Creazione e utilizzo di attributi personalizzati in criteri personalizzati di modifica del profilo

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

In questo articolo creare un attributo personalizzato nella directory di Azure Active Directory B2C e il nuovo attributo utilizzato come un'attestazione personalizzata in viaggio di hello profilo Modifica utente.

## <a name="prerequisites"></a>Prerequisiti

Hello completato i passaggi nell'articolo hello [Guida introduttiva a criteri personalizzati](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Utilizzare gli attributi personalizzati toocollect informazioni sui clienti in Azure Active Directory B2C usando i criteri personalizzati
La directory di Azure Active Directory (Azure AD) B2C viene fornita con un set predefinito di attributi: nome, cognome, città, codice postale, userPrincipalName e così via.  È spesso necessario toocreate attributi personalizzati.  ad esempio:
* Un'applicazione che riguardano il cliente deve toopersist un attributo, ad esempio "LoyaltyNumber".
* Un provider di identità ha un identificatore utente univoco che deve essere salvato, ad esempio "uniqueUserGUID".
* Stato hello toopersist dell'utente, ad esempio "migrationStatus". è necessario un proprio processo utente personalizzata

Con Azure Active Directory B2C, è possibile estendere il set di hello di attributi archiviati in ogni account utente. È anche possibile leggere e scrivere tali attributi tramite hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

Le proprietà di estensione estendono schema hello degli oggetti utente hello nella directory hello.  proprietà di estensione Hello termini, un attributo personalizzato e attestazioni personalizzate, vedere toohello stessa operazione nel contesto di hello di questo nome di articolo e hello varia a seconda del contesto di hello (applicazione, oggetto, criteri).

Le proprietà di estensione possono essere registrate solo su un oggetto applicazione anche se possono contenere dati per un utente. proprietà Hello è applicazione toohello associata. oggetto applicazione Hello deve essere concesso l'accesso in scrittura tooregister una proprietà di estensione. Proprietà di estensione 100 (tra tutti i tipi e tutte le applicazioni) possono essere scritti tooany singolo oggetto. Le proprietà di estensione vengono aggiunti toohello tipo di directory di destinazione e diventa immediatamente accessibile nel tenant di directory hello Azure Active Directory B2C.
Se un'applicazione hello viene eliminata, vengono rimosse anche le proprietà di estensione insieme a tutti i dati in essi contenuti per tutti gli utenti. Se una proprietà di estensione viene eliminata dall'applicazione hello, viene anche rimossa per hello hello valori eliminati e gli oggetti directory di destinazione.

Le proprietà di estensione esistono solo nel contesto di hello di un'applicazione registrata nel tenant di hello. id di oggetto Hello dell'applicazione deve essere incluso in hello TechnicalProfile che lo utilizzano.

>[!NOTE]
>directory di Azure Active Directory B2C Hello include in genere un'applicazione Web denominata `b2c-extensions-app`.  Questa applicazione viene utilizzata principalmente per le attestazioni personalizzate di hello create tramite il portale di Azure hello dai criteri predefiniti di hello b2c.  L'uso di estensioni di tooregister questa applicazione per i criteri personalizzati b2c è consigliato solo per gli utenti esperti.  Istruzioni per questo sono incluse nella sezione passaggi successivi in questo articolo hello.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Creazione di un nuovo toostore applicazione le proprietà di estensione hello

1. Aprire una sessione di esplorazione e passare toohello [Azure Portal](https://portal.azure.com) e accedere con credenziali amministrative di hello Directory B2C da tooconfigure.
1. Fare clic su **Azure Active Directory** nel menu di navigazione sinistro hello. Potrebbe essere necessario per la selezione di più servizi toofind >.
1. Selezionare **Registrazioni per l'app** e fare clic su **Registrazione nuova applicazione**
1. Fornire seguente hello consigliato voci:
  * Specificare un nome per un'applicazione web hello: **WebApp-GraphAPI-DirectoryExtensions**
  * Tipo di applicazione: app Web/API
  * URL di accesso: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Selezionare **Crea. Operazione completata viene visualizzato in hello **notifiche**
1. Selezionare un'applicazione web hello appena creato: **WebApp-GraphAPI-DirectoryExtensions**
1. Selezionare Impostazioni: **Autorizzazioni necessarie**
1. Selezionare l'API **Windows Active Directory**
1. Inserire un segno di spunta in Autorizzazioni per l'applicazione: **Legge e scrive i dati della directory**, quindi **Salva**
1. Selezionare **Concedere le autorizzazioni** e quindi fare clic su **Sì** per confermare.
1. Copiare negli Appunti tooyour e salvare hello seguenti identificatori dagli WebApp-GraphAPI-DirectoryExtensions > Impostazioni > Proprietà >
*  **ID applicazione**. Esempio: `103ee0e6-f92d-4183-b576-8c3739027780`
* **ID oggetto**. Esempio: `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modifica di hello di tooadd ApplicationObjectId i criteri personalizzati

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>Hello <TechnicalProfile Id="AAD-Common"> è tooas cui "comuni" perché gli elementi sono inclusi in e riutilizzati in hello tutti TechnicalProfiles di Azure Active Directory utilizzando l'elemento hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Quando hello TechnicalProfile scrive per la proprietà di estensione di hello prima ora toohello appena creato, è possibile che si verifichi un errore occasionale.  proprietà di estensione Hello creato hello prima volta che viene utilizzato.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Utilizzando una nuova proprietà di estensione hello / attributo personalizzato in un proprio processo utente


1. Aprire hello Relying Party(RP) file che descrive i criteri di modifica viaggio utente.  Se si sta avviando, potrebbe essere consigliabile toodownload la versione di hello RP PolicyEdit già configurata file direttamente dalla sezione criteri personalizzati di B2C Azure nel portale di Azure hello hello.  In alternativa, aprire il file XML dalla cartella di archiviazione.
2. Aggiungere un'attestazione personalizzata `loyaltyId`.  Includendo hello personalizzato con una richiesta di rimborso in hello `<RelyingParty>` elemento, è passato come un toohello parametro UserJourney TechnicalProfiles e incluse nel token hello per un'applicazione hello.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. Aggiungere un file di criteri di attestazione definizione toohello estensione `TrustFrameworkExtensions.xml` all'interno di hello `<ClaimsSchema>` elemento, come illustrato.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Aggiungere hello stessa attestazione file di definizione dei criteri di Base toohello `TrustFrameworkBase.xml`.  
>Aggiunta di un `ClaimType` definizione base hello sia nel hello estensioni file in genere non è necessario, tuttavia, poiché i passaggi successivi hello aggiungerà hello extension_loyaltyId tooTechnicalProfiles nel file di Base hello, convalida criteri hello rifiuterà il caricamento di hello hello file di base senza di esso.
>Potrebbe essere utile tootrace esecuzione di hello del viaggio utente hello denominato "ProfileEdit" nel file TrustFrameworkBase.xml hello.  Ricerca di viaggio utente hello di hello stesso nome nell'editor e osservare che il passaggio 5 di orchestrazione richiama hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".  Ricerca e controllare questo toofamiliarize TechnicalProfile con flusso hello.
5. Aggiungere loyaltyId come attestazioni di input e output di hello TechnicalProfile "SelfAsserted ProfileUpdate"
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Aggiunge l'attestazione "UserWriteProfileUsingObjectId-AAD" TechnicalProfile toopersist hello valore attestazione hello nella proprietà di estensione hello, per l'utente corrente di hello nella directory hello.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. Aggiunge l'attestazione nel valore di hello tooread TechnicalProfile "UserReadUsingObjectId-AAD" dell'attributo di estensione hello ogni volta che un utente accede. Hello TechnicalProfiles finora sono state modificate nel flusso di hello del solo gli account locali.  Volendo nuovo attributo hello nel flusso di hello di un account o federata sociale, un set diverso di TechnicalProfiles deve toobe modificato. Vedere i passaggi successivi.

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>elemento IncludeTechnicalProfile Hello aggiunge tutti gli elementi di hello di Azure ad comune toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Criterio personalizzato di test hello tramite "Esegui"
1. Aprire hello **Pannello di Azure Active Directory B2C** e passare troppo**identità esperienza Framework > criteri personalizzati**.
1. Selezionare i criteri personalizzati hello caricato, quindi scegliere hello **Esegui ora** pulsante.
1. È necessario essere in grado di toosign utilizzando un indirizzo di posta elettronica.

token id Hello inviato nuovamente tooyour applicazione include una nuova proprietà di estensione hello come un'attestazione personalizzata preceduta da extension_loyaltyId. Vedere l'esempio.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Passaggi successivi

Aggiungere hello nuova attestazione toohello flussi per gli account di accesso account social modificando hello TechnicalProfiles elencati. Questi due TechnicalProfiles utilizzate dal toowrite gli account di accesso account sociale o federata e leggere i dati utente hello utilizzando alternativeSecurityId hello come indicatore di posizione dell'oggetto utente hello hello.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Utilizzando hello stessi attributi di estensione tra i criteri predefiniti e personalizzati.
Quando si aggiungono gli attributi dell'estensione (noto anche come attributi personalizzati) tramite l'uso del portale hello, tali attributi vengono registrati utilizzando hello * * b2c-estensioni-app presente in ogni tenant b2c.  toouse questi attributi di estensione per il criterio personalizzato:
1. All'interno di tenant b2c in portal.azure.com, passare troppo**Azure Active Directory** e selezionare **registrazioni di App**
2. Trovare **b2c-extensions-app** e selezionarlo
3. In hello record 'Essentials' **ID applicazione** e hello **ID di oggetto**
4. Includerli nei metadati del profilo tecnico AAD-Common come indicato di seguito:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

la coerenza tookeep con esperienza del portale hello, creare questi attributi utilizzando l'interfaccia utente del portale hello *prima* utilizzarle nei criteri personalizzati.  Quando si crea un attributo "ActivationStatus" nel portale di hello, è necessario consultare tooit come indicato di seguito:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>riferimento

* A **profilo tecnico (TP)** è un tipo di elemento che può essere considerato come un *funzione* che definisce il nome di un endpoint, i metadati, il protocollo e dettagli hello exchange di attestazioni che hello identità Esperienza Framework deve eseguire.  Quando questo *funzione* viene chiamato in un passaggio di orchestrazione o da un altro TechnicalProfile, hello InputClaims e OutputClaims vengono forniti come parametri per il chiamante di hello.


* Per una gestione completa sulle proprietà di estensione, vedere l'articolo hello [le estensioni dello SCHEMA di DIRECTORY | CONCETTI RELATIVI ALL'API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Gli attributi di estensione nell'API Graph sono denominati in base alla convenzione hello `extension_ApplicationObjectID_attributename`. Criteri personalizzati fanno riferimento gli attributi tooextensions come extension_attributename, pertanto l'omissione di hello ApplicationObjectId in hello XML
