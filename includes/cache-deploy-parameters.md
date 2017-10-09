
### <a name="cacheskuname"></a><span data-ttu-id="7803a-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="7803a-101">cacheSKUName</span></span>
<span data-ttu-id="7803a-102">memorizzare nella Cache Redis di Azure nuovo piano tariffario di hello Hello.</span><span class="sxs-lookup"><span data-stu-id="7803a-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

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

<span data-ttu-id="7803a-103">modello Hello definisce i valori hello sono consentiti per questo parametro (Standard o Basic) e assegna un valore predefinito (Basic) se viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="7803a-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="7803a-104">Basic fornisce un singolo nodo con più dimensioni disponibili too53 GB.</span><span class="sxs-lookup"><span data-stu-id="7803a-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="7803a-105">Fornisce due nodi primario/Replica con più dimensioni disponibili backup too53 GB e 99,9% contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="7803a-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="7803a-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="7803a-106">cacheSKUFamily</span></span>
<span data-ttu-id="7803a-107">famiglia di Hello per sku hello.</span><span class="sxs-lookup"><span data-stu-id="7803a-107">hello family for hello sku.</span></span>

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


### <a name="cacheskucapacity"></a><span data-ttu-id="7803a-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="7803a-108">cacheSKUCapacity</span></span>
<span data-ttu-id="7803a-109">dimensione Hello della nuova istanza di Cache Redis di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7803a-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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


<span data-ttu-id="7803a-110">modello di Hello definisce i valori hello consentiti per questo parametro (0, 1, 2, 3, 4, 5 o 6) e assegna un valore predefinito (1) se viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="7803a-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="7803a-111">Tali numeri corrispondono dimensioni della cache toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="7803a-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

