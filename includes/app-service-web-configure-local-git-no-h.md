<span data-ttu-id="d600d-101">Configurare l'app web toohello locale distribuzione Git con hello [az webapp distribuzione origine configurazione-locale-git](/cli/azure/webapp/deployment/source#config-local-git) comando.</span><span class="sxs-lookup"><span data-stu-id="d600d-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="d600d-102">Servizio App supporta diversi modi toodeploy tooa contenuto web app, ad esempio FTP, Git locale, GitHub, Visual Studio Team Services e Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="d600d-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="d600d-103">Per questa guida introduttiva si distribuirà un'istanza Git locale.</span><span class="sxs-lookup"><span data-stu-id="d600d-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="d600d-104">Pertanto, che si distribuisce con un toopush di comando Git da un repository tooa repository locale in Azure.</span><span class="sxs-lookup"><span data-stu-id="d600d-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="d600d-105">In hello seguente comando, sostituire  *\<nome_app >* con il nome dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="d600d-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="d600d-106">output di Hello è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d600d-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="d600d-107">Hello `<username>` è hello [utente distribuzione](#configure-a-deployment-user) creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="d600d-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="d600d-108">Copiare l'URI visualizzato; hello si utilizzerà nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="d600d-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
