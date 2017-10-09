<span data-ttu-id="88f49-101">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="88f49-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="88f49-102">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.</span><span class="sxs-lookup"><span data-stu-id="88f49-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="88f49-103">È in genere creare la risorsa hello e gruppo di risorse in un'area più vicino.</span><span class="sxs-lookup"><span data-stu-id="88f49-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="88f49-104">percorsi toosee tutte supportate per le app Web di Azure, eseguire hello `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="88f49-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
