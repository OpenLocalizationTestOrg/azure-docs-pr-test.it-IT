<span data-ttu-id="fcfc6-101">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="fcfc6-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="fcfc6-102">Per altre informazioni sulla registrazione, vedere [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fcfc6-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="fcfc6-103">Se si hanno più sottoscrizioni Azure, elencare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="fcfc6-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="fcfc6-104">Specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="fcfc6-104">Specify the subscription that you want to use.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```