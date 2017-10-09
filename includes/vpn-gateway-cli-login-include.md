<span data-ttu-id="b1bb0-101">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="b1bb0-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="b1bb0-102">Per altre informazioni sulla registrazione, vedere [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b1bb0-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="b1bb0-103">Se si dispone di più di una sottoscrizione di Azure, è possibile elencare le sottoscrizioni di hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="b1bb0-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="b1bb0-104">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="b1bb0-104">Specify hello subscription that you want toouse.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```