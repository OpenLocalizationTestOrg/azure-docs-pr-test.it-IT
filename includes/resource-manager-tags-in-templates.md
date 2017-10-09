tootag una risorsa durante la distribuzione, aggiungere hello `tags` risorsa toohello dell'elemento si sta distribuendo. Fornire il nome di tag hello e valore.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Applicare un nome di tag toohello valore letterale
Hello esempio seguente viene illustrato un account di archiviazione con due tag (`Dept` e `Environment`) che vengono impostate tooliteral valori:

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

### <a name="apply-an-object-toohello-tag-element"></a>Applicare un elemento di tag object toohello
È possibile definire un parametro di oggetto che archivia diversi tag e applicare tale elemento tag toohello di oggetto. Ogni proprietà nell'oggetto hello diventa un tag per la risorsa hello separato. esempio Hello ha un parametro denominato `tagValues` vale a dire toohello applicato tag elemento.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>Applicare un nome di tag toohello stringa JSON

toostore numero di valori in un singolo tag, applicare una stringa JSON che rappresenta i valori hello. stringa JSON intera Hello viene archiviato come un tag che non può superare i 256 caratteri. esempio Hello include un singolo tag denominato `CostCenter` che contiene più valori da una stringa JSON:  

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