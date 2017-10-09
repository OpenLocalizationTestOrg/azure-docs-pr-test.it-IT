## <a name="load-balancer"></a><span data-ttu-id="8c52e-101">Bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="8c52e-101">Load Balancer</span></span>
<span data-ttu-id="8c52e-102">Quando si desidera tooscale le applicazioni, viene utilizzato un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="8c52e-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="8c52e-103">Gli scenari di distribuzione più comuni riguardano applicazioni in esecuzione in più istanze della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c52e-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="8c52e-104">le istanze VM Hello sono applicazioni da un bilanciamento del carico che consente di toohello il traffico di rete toodistribute diverse istanze.</span><span class="sxs-lookup"><span data-stu-id="8c52e-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![Scheda di interfaccia di rete in una macchina virtuale singola](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="8c52e-106">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8c52e-106">Property</span></span> | <span data-ttu-id="8c52e-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8c52e-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c52e-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="8c52e-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="8c52e-109">un bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP).</span><span class="sxs-lookup"><span data-stu-id="8c52e-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="8c52e-110">Questi indirizzi IP fungono in ingresso per il traffico hello e possono essere IP pubblico o privato IP</span><span class="sxs-lookup"><span data-stu-id="8c52e-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="8c52e-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="8c52e-111">*backendAddressPools*</span></span> |<span data-ttu-id="8c52e-112">Questi sono gli indirizzi IP associati verrà distribuita le schede NIC VM toowhich carico hello</span><span class="sxs-lookup"><span data-stu-id="8c52e-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="8c52e-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="8c52e-113">*loadBalancingRules*</span></span> |<span data-ttu-id="8c52e-114">una proprietà della regola esegue il mapping di un indirizzo IP specificato front-end e porta set tooa combinazione di indirizzi IP back-end e combinazione di porta.</span><span class="sxs-lookup"><span data-stu-id="8c52e-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="8c52e-115">Con una singola definizione di una risorsa di bilanciamento del carico è possibile definire più regole di bilanciamento carico, ciascuna delle quali riflette una combinazione di IP e porte front-end e di IP e porte back-end associata alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8c52e-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="8c52e-116">regola di Hello è una porta in macchine virtuali nel pool back-end hello hello front-end pool toomany</span><span class="sxs-lookup"><span data-stu-id="8c52e-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="8c52e-117">*Probe*</span><span class="sxs-lookup"><span data-stu-id="8c52e-117">*Probes*</span></span> |<span data-ttu-id="8c52e-118">probe consentono di tenere traccia di tookeep integrità hello di istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c52e-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="8c52e-119">Se un probe di integrità non riesce, istanza di macchina virtuale hello verrà eseguita dalla rotazione automaticamente</span><span class="sxs-lookup"><span data-stu-id="8c52e-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="8c52e-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="8c52e-120">*inboundNatRules*</span></span> |<span data-ttu-id="8c52e-121">Le regole NAT definizione hello che passano attraverso IP front-end hello traffico in entrata e distribuite tooa macchina virtuale specifica istanza di toohello back-end IP.</span><span class="sxs-lookup"><span data-stu-id="8c52e-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="8c52e-122">La regola NAT è una porta nella macchina virtuale nel pool back-end hello hello front-end pool tooone</span><span class="sxs-lookup"><span data-stu-id="8c52e-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="8c52e-123">Esempio di modello di bilanciamento del carico in formato Json:</span><span class="sxs-lookup"><span data-stu-id="8c52e-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
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
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="8c52e-124">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8c52e-124">Additional resources</span></span>
<span data-ttu-id="8c52e-125">Leggere [API REST di bilanciamento del carico](https://msdn.microsoft.com/library/azure/mt163651.aspx) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="8c52e-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

