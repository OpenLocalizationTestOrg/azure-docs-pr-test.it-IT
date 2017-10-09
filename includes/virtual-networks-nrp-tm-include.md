## <a name="traffic-manager-profile"></a><span data-ttu-id="1cbb6-101">Profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="1cbb6-101">Traffic Manager Profile</span></span>
<span data-ttu-id="1cbb6-102">Gestione traffico e la relativa risorsa endpoint figlio abilitare tooendpoints di routing DNS in Azure e all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="1cbb6-103">Questa distribuzione del traffico è regolata dai metodi dei criteri di routing.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="1cbb6-104">Gestione traffico consente inoltre di monitorata toobe di integrità di endpoint e traffico deviato in modo appropriato in base hello integrità di un endpoint.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="1cbb6-105">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1cbb6-105">Property</span></span> | <span data-ttu-id="1cbb6-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1cbb6-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1cbb6-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="1cbb6-108">i valori possibili sono *Prestazioni*, *Valore ponderato* e *Priorità*</span><span class="sxs-lookup"><span data-stu-id="1cbb6-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="1cbb6-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-109">**dnsConfig**</span></span> |<span data-ttu-id="1cbb6-110">Nome di dominio completo per il profilo di hello</span><span class="sxs-lookup"><span data-stu-id="1cbb6-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="1cbb6-111">**Protocollo**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-111">**Protocol**</span></span> |<span data-ttu-id="1cbb6-112">protocollo di monitoraggio, i valori possibili sono *HTTP* e *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="1cbb6-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="1cbb6-113">**Porta**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-113">**Port**</span></span> |<span data-ttu-id="1cbb6-114">porta di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="1cbb6-114">monitoring port</span></span> |
| <span data-ttu-id="1cbb6-115">**Percorso**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-115">**Path**</span></span> |<span data-ttu-id="1cbb6-116">percorso di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="1cbb6-116">monitoring path</span></span> |
| <span data-ttu-id="1cbb6-117">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-117">**Endpoints**</span></span> |<span data-ttu-id="1cbb6-118">contenitore per le risorse endpoint</span><span class="sxs-lookup"><span data-stu-id="1cbb6-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="1cbb6-119">Endpoint</span><span class="sxs-lookup"><span data-stu-id="1cbb6-119">Endpoint</span></span>
<span data-ttu-id="1cbb6-120">Un endpoint è una risorsa figlio di un profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="1cbb6-121">Rappresenta un servizio o il traffico web endpoint toowhich utente viene distribuito in base ai criteri configurato hello in hello risorsa per il profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="1cbb6-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1cbb6-122">Property</span></span> | <span data-ttu-id="1cbb6-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1cbb6-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1cbb6-124">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-124">**Type**</span></span> |<span data-ttu-id="1cbb6-125">Hello tipo dell'endpoint di hello, i valori possibili sono *punto finale di Azure*, *Endpoint esterno*, e *Endpoint annidati*</span><span class="sxs-lookup"><span data-stu-id="1cbb6-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="1cbb6-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-126">**targetResourceId**</span></span> |<span data-ttu-id="1cbb6-127">indirizzo IP pubblico di un endpoint di servizio o Web.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="1cbb6-128">Può trattarsi di un endpoint di Azure o esterno.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="1cbb6-129">**Peso**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-129">**Weight**</span></span> |<span data-ttu-id="1cbb6-130">peso dell'endpoint usato nella gestione del traffico.</span><span class="sxs-lookup"><span data-stu-id="1cbb6-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="1cbb6-131">**Priorità**</span><span class="sxs-lookup"><span data-stu-id="1cbb6-131">**Priority**</span></span> |<span data-ttu-id="1cbb6-132">priorità dell'endpoint hello toodefine usato un'azione di failover</span><span class="sxs-lookup"><span data-stu-id="1cbb6-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="1cbb6-133">Esempio di Gestione traffico in formato Json:</span><span class="sxs-lookup"><span data-stu-id="1cbb6-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="1cbb6-134">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1cbb6-134">Additional resources</span></span>
<span data-ttu-id="1cbb6-135">Per ulteriori informazioni, leggere la [documentazione dell'API REST per Gestione traffico](https://msdn.microsoft.com/library/azure/mt163664.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1cbb6-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

