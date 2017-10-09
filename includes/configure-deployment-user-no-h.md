Creare le credenziali di distribuzione con hello [az webapp distribuzione utente set](/cli/azure/webapp/deployment/user#set) comando.

Un utente di distribuzione è necessario per FTP e app web tooa locale distribuzione Git. nome utente hello e password sono a livello di account. _Sono quindi diversi dalle credenziali della sottoscrizione di Azure._

In hello seguente comando, sostituire  *\<nome utente >* e  *\<password >* con un nuovo nome utente e una password. nome utente Hello deve essere univoco. Hello password deve essere composta da almeno otto caratteri, con due simboli di hello seguenti tre elementi: lettere, numeri e simboli. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Se viene visualizzato un ` 'Conflict'. Details: 409` errore, nome utente hello di modifica. Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.

L'utente di distribuzione viene creato una sola volta e può essere usato per tutte le distribuzioni di Azure.

> [!NOTE]
> Nome del record hello utente e password. È necessario toodeploy hello web app in un secondo momento.
>
>