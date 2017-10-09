
### <a name="cacheskuname"></a>cacheSKUName
memorizzare nella Cache Redis di Azure nuovo piano tariffario di hello Hello.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

modello Hello definisce i valori hello sono consentiti per questo parametro (Standard o Basic) e assegna un valore predefinito (Basic) se viene specificato alcun valore. Basic fornisce un singolo nodo con più dimensioni disponibili too53 GB.
Fornisce due nodi primario/Replica con più dimensioni disponibili backup too53 GB e 99,9% contratto di servizio.

### <a name="cacheskufamily"></a>cacheSKUFamily
famiglia di Hello per sku hello.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
dimensione Hello della nuova istanza di Cache Redis di Azure hello. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


modello di Hello definisce i valori hello consentiti per questo parametro (0, 1, 2, 3, 4, 5 o 6) e assegna un valore predefinito (1) se viene specificato alcun valore. Tali numeri corrispondono dimensioni della cache toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

