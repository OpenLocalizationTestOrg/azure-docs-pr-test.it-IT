<span data-ttu-id="5cfe8-101">Creare le credenziali di distribuzione con hello [az webapp distribuzione utente set](/cli/azure/webapp/deployment/user#set) comando.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="5cfe8-102">Un utente di distribuzione è necessario per FTP e app web tooa locale distribuzione Git.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="5cfe8-103">nome utente hello e password sono a livello di account.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-103">hello user name and password are account level.</span></span> <span data-ttu-id="5cfe8-104">_Sono quindi diversi dalle credenziali della sottoscrizione di Azure._</span><span class="sxs-lookup"><span data-stu-id="5cfe8-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="5cfe8-105">In hello seguente comando, sostituire  *\<nome utente >* e  *\<password >* con un nuovo nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="5cfe8-106">nome utente Hello deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-106">hello user name must be unique.</span></span> <span data-ttu-id="5cfe8-107">Hello password deve essere composta da almeno otto caratteri, con due simboli di hello seguenti tre elementi: lettere, numeri e simboli.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="5cfe8-108">Se viene visualizzato un ` 'Conflict'. Details: 409` errore, nome utente hello di modifica.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="5cfe8-109">Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="5cfe8-110">L'utente di distribuzione viene creato una sola volta e può essere usato per tutte le distribuzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="5cfe8-111">Nome del record hello utente e password.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-111">Record hello user name and password.</span></span> <span data-ttu-id="5cfe8-112">È necessario toodeploy hello web app in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5cfe8-112">You need them toodeploy hello web app later.</span></span>
>
>