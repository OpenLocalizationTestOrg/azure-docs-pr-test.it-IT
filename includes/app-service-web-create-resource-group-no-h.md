Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

È in genere creare la risorsa hello e gruppo di risorse in un'area più vicino. percorsi toosee tutte supportate per le app Web di Azure, eseguire hello `az appservice list-locations` comando. 
