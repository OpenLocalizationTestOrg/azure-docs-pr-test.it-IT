## <a name="application-gateway"></a><span data-ttu-id="cef9f-101">Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="cef9f-101">Application Gateway</span></span>
<span data-ttu-id="cef9f-102">Il servizio Gateway applicazione fornisce una soluzione di bilanciamento del carico HTTP gestita da Azure basata sul bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="cef9f-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="cef9f-103">Il bilanciamento del carico applicazioni consente di usare le regole di routing per il traffico di rete basato su HTTP.</span><span class="sxs-lookup"><span data-stu-id="cef9f-103">Application load balancing allows the use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="cef9f-104">Proprietà</span><span class="sxs-lookup"><span data-stu-id="cef9f-104">Property</span></span> | <span data-ttu-id="cef9f-105">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cef9f-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cef9f-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="cef9f-106">**backendAddressPools**</span></span> |<span data-ttu-id="cef9f-107">L’elenco di indirizzi IP dei server di back-end.</span><span class="sxs-lookup"><span data-stu-id="cef9f-107">The list of IP addresses of the back end servers.</span></span> <span data-ttu-id="cef9f-108">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici o indirizzi IP privati.</span><span class="sxs-lookup"><span data-stu-id="cef9f-108">The IP addresses listed should either belong to the virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="cef9f-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="cef9f-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="cef9f-110">Ogni pool ha impostazioni quali porta, protocollo e affinità basate sui cookie.</span><span class="sxs-lookup"><span data-stu-id="cef9f-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="cef9f-111">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="cef9f-111">These settings are tied to a pool and are applied to all servers within the pool</span></span> |
| <span data-ttu-id="cef9f-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="cef9f-112">**frontendPorts**</span></span> |<span data-ttu-id="cef9f-113">Questa porta è la porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="cef9f-113">This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="cef9f-114">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="cef9f-114">Traffic hits this port, and then gets redirected to one of the back end servers</span></span> |
| <span data-ttu-id="cef9f-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="cef9f-115">**httpListeners**</span></span> |<span data-ttu-id="cef9f-116">Il listener ha una porta front-end, un protocollo (Http o Https, con applicazione della distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="cef9f-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="cef9f-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="cef9f-117">**requestRoutingRules**</span></span> |<span data-ttu-id="cef9f-118">La regola associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico.</span><span class="sxs-lookup"><span data-stu-id="cef9f-118">The rule binds the listener and the back end server pool and defines which back end server pool the traffic should be directed.</span></span> <span data-ttu-id="cef9f-119">Attualmente è supportato solo come Round-robin</span><span class="sxs-lookup"><span data-stu-id="cef9f-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="cef9f-120">Esempio di un modello Json del gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="cef9f-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location to deploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for the Virtual Network"
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


### <a name="additional-resources"></a><span data-ttu-id="cef9f-121">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cef9f-121">Additional resources</span></span>
<span data-ttu-id="cef9f-122">Leggere [ API REST del gateway applicazione](https://msdn.microsoft.com/library/azure/mt299388.aspx) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="cef9f-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

