[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister l'applicazione per dispositivi mobili o nativo, utilizza le impostazioni di hello specificate nella tabella hello.

![Impostazioni di registrazione di esempio per una nuova applicazione per dispositivi mobili o nativa](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Impostazione      | Valore di esempio  | Descrizione                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | App Contoso B2C | Immettere un **nome** per un'applicazione hello che descrive il tooconsumers dell'applicazione. |
| **Client nativo** | Sì | Selezionare **Sì** per un'applicazione per dispositivi mobili o nativa. |
| **URI di reindirizzamento personalizzato** | `com.onmicrosoft.contoso.appname://redirect/path` | Immettere un URI di reindirizzamento con uno schema personalizzato. Assicurarsi di scegliere un [URI di reindirizzamento valido](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) e di non includere caratteri speciali come i caratteri di sottolineatura. |

Fare clic su **crea** tooregister l'applicazione.

L'applicazione appena registrato viene visualizzato nell'elenco delle applicazioni per il tenant B2C hello hello. Selezionare l'app mobile o nativo dall'elenco di hello. riquadro delle proprietà dell'applicazione Hello viene visualizzato.

![Proprietà dell'applicazione](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Prendere nota di hello univoco globale **ID Client applicazione**. ID di hello viene usato nel codice dell'applicazione.

Se l'applicazione nativa chiama un'API Web protetta da Azure AD B2C, seguire questa procedura:
   1. Creare un segreto dell'applicazione da passare toohello **chiavi** blade e facendo clic su hello **Genera chiave** pulsante. Prendere nota di hello **chiave App** valore. Valore di hello è utilizzato come segreto dell'applicazione hello nel codice dell'applicazione.
   2. Fare clic su **Accesso all'API**, quindi su **Aggiungi** e selezionare l'API Web e gli ambiti (autorizzazioni).

> [!NOTE]
> Un **segreto dell'applicazione** è una credenziale di sicurezza importante e deve essere protetto in modo appropriato.
> 
