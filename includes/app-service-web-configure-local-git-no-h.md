Configurare l'app web toohello locale distribuzione Git con hello [az webapp distribuzione origine configurazione-locale-git](/cli/azure/webapp/deployment/source#config-local-git) comando.

Servizio App supporta diversi modi toodeploy tooa contenuto web app, ad esempio FTP, Git locale, GitHub, Visual Studio Team Services e Bitbucket. Per questa guida introduttiva si distribuirà un'istanza Git locale. Pertanto, che si distribuisce con un toopush di comando Git da un repository tooa repository locale in Azure. 

In hello seguente comando, sostituire  *\<nome_app >* con il nome dell'applicazione web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

output di Hello è hello seguente formato:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Hello `<username>` è hello [utente distribuzione](#configure-a-deployment-user) creato nel passaggio precedente.

Copiare l'URI visualizzato; hello si utilizzerà nel passaggio successivo hello.
