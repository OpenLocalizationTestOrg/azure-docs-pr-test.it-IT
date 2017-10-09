[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister l'API web, utilizzare le impostazioni di hello specificate nella tabella hello.

![Impostazioni di registrazione di esempio per una nuova API Web](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Impostazione      | Valore di esempio  | Descrizione                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | API Contoso B2C | Immettere un **nome** per un'applicazione hello che descrive il tooconsumers API. | 
| **Includi app Web/API Web** | Sì | Selezionare **Sì** per un'API Web. |
| **Consenti il flusso implicito** | Sì | Selezionare **Sì** se l'applicazione usa l'[accesso con OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL di risposta** | `https://localhost:44316/` | Gli URL di risposta sono gli endpoint a cui Azure AD B2C restituisce eventuali token richiesti dall'applicazione. Immettere [un ](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **URL di risposta** appropriato. In questo esempio l'API Web è locale ed è in ascolto sulla porta 44316. |
| **URI ID app** | api | URI ID App Hello è l'identificatore hello utilizzato per l'API web. Hello identificatore completo, incluso il dominio hello URI viene generato automaticamente. |

Fare clic su **crea** tooregister l'applicazione.

L'applicazione appena registrato viene visualizzato nell'elenco delle applicazioni per il tenant B2C hello hello. Selezionare l'API web elenco hello. verrà visualizzato il riquadro di proprietà Hello dell'API.

![Proprietà dell'API Web](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Prendere nota di hello univoco globale **ID Client applicazione**. ID di hello viene usato nel codice dell'applicazione.
