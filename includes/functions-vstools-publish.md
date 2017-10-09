1. In **Esplora**, fare clic sul progetto hello e selezionare **pubblica**. Selezionare **Crea nuovo** e quindi fare clic su **Pubblica**. 

    ![Pubblicare creando una nuova app per le funzioni](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Se Visual Studio tooyour account Azure non sono stati già connessi, fare clic su **aggiungere un account...** .  

3. In hello **Crea servizio App** finestra di dialogo, utilizzare hello **Hosting** impostazioni hello specificato nella tabella seguente: 

    ![Runtime locale di Azure](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Impostazione      | Valore consigliato  | Descrizione                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome app** | Nome globalmente univoco | Nome che identifica in modo univoco la nuova app per le funzioni. |
    | **Sottoscrizione** | Scegliere la sottoscrizione | Hello toouse di sottoscrizione di Azure. |
    | **[Gruppo di risorse](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nome della risorsa hello gruppo in cui toocreate l'app di funzione. |
    | **[Piano di servizio app](../articles/azure-functions/functions-scale.md)** | Piano a consumo | Verificare che hello toochoose **consumo** in **dimensioni** quando si crea un nuovo piano.  |
    | **[Account di archiviazione](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nome globalmente univoco | Usare un account di archiviazione esistente o crearne uno nuovo.   |

4. Fare clic su **crea** toocreate un'app di funzione in Azure con queste impostazioni. Dopo aver completato il provisioning di hello, prendere nota di hello **URL del sito** valore, ovvero indirizzo hello dell'app in funzione in Azure. 

    ![Runtime locale di Azure](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
