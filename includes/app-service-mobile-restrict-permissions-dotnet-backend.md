
Per impostazione predefinita, le API in un back-end dell'app per dispositivi mobili possono essere richiamate in modo anonimo. Successivamente, è necessario toorestrict i client tooonly autenticato di accesso.  

* **Node.js nuovamente end (tramite il portale di Azure hello)** :  

    Nelle impostazioni dell'app per dispositivi mobili fare clic su **Tabelle semplici** e selezionare la tabella. Fare clic su **Modifica autorizzazioni**, selezionare **Authenticated access only** (Solo accesso con autenticazione) per tutte le autorizzazioni e quindi fare clic su **Salva**.
* **Back-end. NET (C#)**:  

    Nel progetto server hello, passare troppo**controller** > **TodoItemController.cs**. Aggiungere hello `[Authorize]` attributo toohello **TodoItemController** classe, come indicato di seguito. toorestrict accesso solo toospecific i metodi, è inoltre possibile applicare questi metodi solo toothose attributo anziché la classe hello. Ripubblicare progetto server hello.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Back-end Node.js (tramite codice Node.js)** :  

    autenticazione toorequire per l'accesso di tabella, aggiungere hello lo script server Node.js toohello di riga seguente:

        table.access = 'authenticated';

    Per ulteriori informazioni, vedere [procedura: richiedere l'autenticazione per accesso tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). progetto di codice toodownload hello Guida introduttiva del sito, vedere toolearn [come: Download hello Node.js back-end delle Guide rapide progetto di codice usando Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
