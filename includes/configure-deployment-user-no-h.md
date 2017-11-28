<span data-ttu-id="9807d-101">Creare credenziali di distribuzione con il comando [az webapp deployment user set](/cli/azure/webapp/deployment/user#set).</span><span class="sxs-lookup"><span data-stu-id="9807d-101">Create deployment credentials with the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="9807d-102">Un utente della distribuzione è necessario per la distribuzione con FTP e l'istanza Git locale in un'app Web.</span><span class="sxs-lookup"><span data-stu-id="9807d-102">A deployment user is required for FTP and local Git deployment to a web app.</span></span> <span data-ttu-id="9807d-103">Nome utente e password sono a livello di account.</span><span class="sxs-lookup"><span data-stu-id="9807d-103">The user name and password are account level.</span></span> <span data-ttu-id="9807d-104">_Sono quindi diversi dalle credenziali della sottoscrizione di Azure._</span><span class="sxs-lookup"><span data-stu-id="9807d-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="9807d-105">Nel comando seguente sostituire *\<user-name>* e *\<password>* con un nuovo nome utente e una nuova password.</span><span class="sxs-lookup"><span data-stu-id="9807d-105">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="9807d-106">Il nome utente deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="9807d-106">The user name must be unique.</span></span> <span data-ttu-id="9807d-107">La password deve essere composta da almeno otto caratteri, con due dei tre elementi seguenti: lettere, numeri e simboli.</span><span class="sxs-lookup"><span data-stu-id="9807d-107">The password must be at least eight characters long, with two of the following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="9807d-108">Se viene visualizzato un errore ` 'Conflict'. Details: 409`, modificare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="9807d-108">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="9807d-109">Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.</span><span class="sxs-lookup"><span data-stu-id="9807d-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="9807d-110">L'utente di distribuzione viene creato una sola volta e può essere usato per tutte le distribuzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9807d-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="9807d-111">Registrare il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="9807d-111">Record the user name and password.</span></span> <span data-ttu-id="9807d-112">Saranno necessari per distribuire l'app Web in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9807d-112">You need them to deploy the web app later.</span></span>
>
>