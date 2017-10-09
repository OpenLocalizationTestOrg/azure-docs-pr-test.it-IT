## <a name="application-gateway"></a><span data-ttu-id="d3b49-101">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="d3b49-101">Application Gateway</span></span>
<span data-ttu-id="d3b49-102">Il servizio Gateway applicazione fornisce una soluzione di bilanciamento del carico HTTP gestita da Azure basata sul bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="d3b49-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="d3b49-103">Bilanciamento del carico di applicazioni consente l'utilizzo di hello regole di routing del traffico di rete basato su HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3b49-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="d3b49-104">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d3b49-104">Property</span></span> | <span data-ttu-id="d3b49-105">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d3b49-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3b49-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="d3b49-106">**backendAddressPools**</span></span> |<span data-ttu-id="d3b49-107">elenco di Hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="d3b49-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="d3b49-108">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale, o devono essere un indirizzo IP/VIP pubblico o privato IP</span><span class="sxs-lookup"><span data-stu-id="d3b49-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="d3b49-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="d3b49-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="d3b49-110">Ogni pool ha impostazioni quali porta, protocollo e affinità basate sui cookie.</span><span class="sxs-lookup"><span data-stu-id="d3b49-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="d3b49-111">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool</span><span class="sxs-lookup"><span data-stu-id="d3b49-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="d3b49-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="d3b49-112">**frontendPorts**</span></span> |<span data-ttu-id="d3b49-113">Questa porta è aperta nel gateway applicazione hello la porta pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="d3b49-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="d3b49-114">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello</span><span class="sxs-lookup"><span data-stu-id="d3b49-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="d3b49-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="d3b49-115">**httpListeners**</span></span> |<span data-ttu-id="d3b49-116">Listener dispone di una porta di front-end, un protocollo (Http o Https, si tratta tra maiuscole e minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload)</span><span class="sxs-lookup"><span data-stu-id="d3b49-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="d3b49-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="d3b49-117">**requestRoutingRules**</span></span> |<span data-ttu-id="d3b49-118">regola di Hello associa hello pool server back-end del listener e hello e definisce da indirizzare il traffico di hello pool server back-end.</span><span class="sxs-lookup"><span data-stu-id="d3b49-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="d3b49-119">Attualmente è supportato solo come Round-robin</span><span class="sxs-lookup"><span data-stu-id="d3b49-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="d3b49-120">Esempio di un modello Json del gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="d3b49-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="d3b49-121">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d3b49-121">Additional resources</span></span>
<span data-ttu-id="d3b49-122">Leggere [ API REST del gateway applicazione](https://msdn.microsoft.com/library/azure/mt299388.aspx) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="d3b49-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

