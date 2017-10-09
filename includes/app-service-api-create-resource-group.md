<span data-ttu-id="e5235-101">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e5235-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="e5235-102">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.</span><span class="sxs-lookup"><span data-stu-id="e5235-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e5235-103">toosee hello posizioni disponibili, eseguire hello `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="e5235-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="e5235-104">In genere si creano risorse in un'area nelle vicinanze.</span><span class="sxs-lookup"><span data-stu-id="e5235-104">You generally create resources in a region near you.</span></span>
