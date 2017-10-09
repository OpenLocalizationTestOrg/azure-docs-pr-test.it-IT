<span data-ttu-id="3a8cc-101">Utilizzare un gruppo di risorse tooa tag, tooadd **set di gruppi di azure**.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="3a8cc-102">Se il gruppo di risorse hello non dispone di tutti i tag esistenti, passare i tag di hello.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="3a8cc-103">I tag vengono aggiornati nel loro complesso.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-103">Tags are updated as a whole.</span></span> <span data-ttu-id="3a8cc-104">Se si desidera tooadd un gruppo di risorse tooa tag con i tag esistenti, è possibile passare tutti i tag di hello.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="3a8cc-105">I tag non vengono ereditati dalle risorse in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="3a8cc-106">utilizzare una risorsa, tooa tag tooadd **set di risorse di azure**.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="3a8cc-107">Passare il numero di versione API per il tipo di risorsa hello che si sta aggiungendo i tag hello hello.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="3a8cc-108">Se occorre una versione di hello API tooretrieve, utilizzare hello comando con il provider di risorse hello per il tipo di hello che si impostano seguente:</span><span class="sxs-lookup"><span data-stu-id="3a8cc-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="3a8cc-109">Nei risultati di hello, cercare il tipo di risorsa hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="3a8cc-110">A questo punto, specificare tale versione dell'API, il nome gruppo di risorse, il nome della risorsa, il tipo di risorsa e il valore del tag come parametri.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="3a8cc-111">I tag risultano direttamente sulle risorse e sui gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="3a8cc-112">i tag esistenti hello toosee, ottenere un gruppo di risorse e le risorse con **Mostra gruppo azure**.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="3a8cc-113">Che restituisce i metadati relativi a gruppo di risorse hello, incluso qualsiasi tooit tag applicati.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="3a8cc-114">Per visualizzare i tag per una particolare risorsa hello utilizzare **Mostra risorse di azure**.</span><span class="sxs-lookup"><span data-stu-id="3a8cc-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="3a8cc-115">tooretrieve tutte le risorse di hello con un valore di tag, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="3a8cc-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="3a8cc-116">tooretrieve tutti i gruppi di risorse di hello con un valore di tag, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="3a8cc-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="3a8cc-117">È possibile visualizzare i tag esistenti hello nella sottoscrizione con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3a8cc-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
