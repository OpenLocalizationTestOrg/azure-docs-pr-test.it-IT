<span data-ttu-id="eb08e-101">tootag una risorsa durante la distribuzione, aggiungere hello `tags` risorsa toohello dell'elemento si sta distribuendo.</span><span class="sxs-lookup"><span data-stu-id="eb08e-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="eb08e-102">Fornire il nome di tag hello e valore.</span><span class="sxs-lookup"><span data-stu-id="eb08e-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="eb08e-103">Applicare un nome di tag toohello valore letterale</span><span class="sxs-lookup"><span data-stu-id="eb08e-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="eb08e-104">Hello esempio seguente viene illustrato un account di archiviazione con due tag (`Dept` e `Environment`) che vengono impostate tooliteral valori:</span><span class="sxs-lookup"><span data-stu-id="eb08e-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="eb08e-105">Applicare un elemento di tag object toohello</span><span class="sxs-lookup"><span data-stu-id="eb08e-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="eb08e-106">È possibile definire un parametro di oggetto che archivia diversi tag e applicare tale elemento tag toohello di oggetto.</span><span class="sxs-lookup"><span data-stu-id="eb08e-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="eb08e-107">Ogni proprietà nell'oggetto hello diventa un tag per la risorsa hello separato.</span><span class="sxs-lookup"><span data-stu-id="eb08e-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="eb08e-108">esempio Hello ha un parametro denominato `tagValues` vale a dire toohello applicato tag elemento.</span><span class="sxs-lookup"><span data-stu-id="eb08e-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="eb08e-109">Applicare un nome di tag toohello stringa JSON</span><span class="sxs-lookup"><span data-stu-id="eb08e-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="eb08e-110">toostore numero di valori in un singolo tag, applicare una stringa JSON che rappresenta i valori hello.</span><span class="sxs-lookup"><span data-stu-id="eb08e-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="eb08e-111">stringa JSON intera Hello viene archiviato come un tag che non può superare i 256 caratteri.</span><span class="sxs-lookup"><span data-stu-id="eb08e-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="eb08e-112">esempio Hello include un singolo tag denominato `CostCenter` che contiene più valori da una stringa JSON:</span><span class="sxs-lookup"><span data-stu-id="eb08e-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```