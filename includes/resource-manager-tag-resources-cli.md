Utilizzare un gruppo di risorse tooa tag, tooadd **set di gruppi di azure**. Se il gruppo di risorse hello non dispone di tutti i tag esistenti, passare i tag di hello.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

I tag vengono aggiornati nel loro complesso. Se si desidera tooadd un gruppo di risorse tooa tag con i tag esistenti, è possibile passare tutti i tag di hello. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

I tag non vengono ereditati dalle risorse in un gruppo di risorse. utilizzare una risorsa, tooa tag tooadd **set di risorse di azure**. Passare il numero di versione API per il tipo di risorsa hello che si sta aggiungendo i tag hello hello. Se occorre una versione di hello API tooretrieve, utilizzare hello comando con il provider di risorse hello per il tipo di hello che si impostano seguente:

```azurecli
azure provider show -n Microsoft.Storage --json
```

Nei risultati di hello, cercare il tipo di risorsa hello desiderato.

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

A questo punto, specificare tale versione dell'API, il nome gruppo di risorse, il nome della risorsa, il tipo di risorsa e il valore del tag come parametri.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

I tag risultano direttamente sulle risorse e sui gruppi di risorse. i tag esistenti hello toosee, ottenere un gruppo di risorse e le risorse con **Mostra gruppo azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Che restituisce i metadati relativi a gruppo di risorse hello, incluso qualsiasi tooit tag applicati.

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

Per visualizzare i tag per una particolare risorsa hello utilizzare **Mostra risorse di azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve tutte le risorse di hello con un valore di tag, utilizzare:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve tutti i gruppi di risorse di hello con un valore di tag, utilizzare:

```azurecli
azure group list -t Dept=Finance
```

È possibile visualizzare i tag esistenti hello nella sottoscrizione con hello comando seguente:

```azurecli
azure tag list
```
