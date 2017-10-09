Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee hello posizioni disponibili, eseguire hello `az appservice list-locations` comando. In genere si creano risorse in un'area nelle vicinanze.
