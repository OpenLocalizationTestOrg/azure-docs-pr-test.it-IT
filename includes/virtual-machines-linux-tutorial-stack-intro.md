## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Creare una macchina virtuale

Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando. 

esempio Hello crea una macchina virtuale denominata *myVM* e crea le chiavi SSH se sono già presenti in un percorso chiave predefinito. toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente. Prendere nota di hello `publicIpAddress`. Questo indirizzo è utilizzato tooaccess hello macchina virtuale.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Aprire la porta 80 per il traffico Web 

Per impostazione predefinita, nelle VM Linux distribuite in Azure sono consentite solo le connessioni SSH. Poiché questa macchina virtuale è in corso toobe un server web, è necessario tooopen la porta 80 da hello internet. Hello utilizzare [az vm aprire porte](/cli/azure/vm#open-port) comando tooopen hello desiderato porta.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Usare SSH per connettersi alla macchina virtuale


Se non si conosce hello indirizzo IP pubblico della macchina virtuale, esegue hello [elenco public-ip di rete az](/cli/azure/network/public-ip#list) comando:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello. Sostituire hello corretto indirizzo IP pubblico della macchina virtuale. In questo esempio, è l'indirizzo IP hello *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

