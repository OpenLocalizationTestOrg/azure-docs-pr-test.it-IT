## <a name="azure-dns"></a><span data-ttu-id="092cb-101">DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="092cb-101">Azure DNS</span></span>
<span data-ttu-id="092cb-102">DNS di Azure è un servizio di hosting per i domini DNS, che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="092cb-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="092cb-103">Proprietà</span><span class="sxs-lookup"><span data-stu-id="092cb-103">Property</span></span> | <span data-ttu-id="092cb-104">Descrizione</span><span class="sxs-lookup"><span data-stu-id="092cb-104">Description</span></span> | <span data-ttu-id="092cb-105">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="092cb-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="092cb-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="092cb-106">**DNSzones**</span></span> |<span data-ttu-id="092cb-107">Informazioni sulla zona del dominio per ospitare i record DNS di un particolare dominio.</span><span class="sxs-lookup"><span data-stu-id="092cb-107">Domain zone information to host DNS records of a particular domain</span></span> |<span data-ttu-id="092cb-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="092cb-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="092cb-109">Set di record DNS</span><span class="sxs-lookup"><span data-stu-id="092cb-109">DNS record sets</span></span>
<span data-ttu-id="092cb-110">Le zone DNS dispongono di un oggetto figlio denominato set di record.</span><span class="sxs-lookup"><span data-stu-id="092cb-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="092cb-111">I set di record sono una raccolta di record host in base al tipo per una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="092cb-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="092cb-112">I tipi record sono A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="092cb-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="092cb-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="092cb-113">Property</span></span> | <span data-ttu-id="092cb-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="092cb-114">Description</span></span> | <span data-ttu-id="092cb-115">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="092cb-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="092cb-116">A</span><span class="sxs-lookup"><span data-stu-id="092cb-116">A</span></span> |<span data-ttu-id="092cb-117">Tipo di record IPv4</span><span class="sxs-lookup"><span data-stu-id="092cb-117">IPv4 record type</span></span> |<span data-ttu-id="092cb-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="092cb-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="092cb-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="092cb-119">AAAA</span></span> |<span data-ttu-id="092cb-120">Tipo di record IPv6</span><span class="sxs-lookup"><span data-stu-id="092cb-120">IPv6 record type</span></span> |<span data-ttu-id="092cb-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="092cb-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="092cb-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="092cb-122">CNAME</span></span> |<span data-ttu-id="092cb-123">tipo di record di nome canonical <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="092cb-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="092cb-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="092cb-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="092cb-125">MX</span><span class="sxs-lookup"><span data-stu-id="092cb-125">MX</span></span> |<span data-ttu-id="092cb-126">Tipo di record di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="092cb-126">mail record type</span></span> |<span data-ttu-id="092cb-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="092cb-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="092cb-128">NS</span><span class="sxs-lookup"><span data-stu-id="092cb-128">NS</span></span> |<span data-ttu-id="092cb-129">tipo di record di nome del server</span><span class="sxs-lookup"><span data-stu-id="092cb-129">name server record type</span></span> |<span data-ttu-id="092cb-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="092cb-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="092cb-131">SOA</span><span class="sxs-lookup"><span data-stu-id="092cb-131">SOA</span></span> |<span data-ttu-id="092cb-132">Tipo di record di "Start of Authority" <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="092cb-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="092cb-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="092cb-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="092cb-134">SRV</span><span class="sxs-lookup"><span data-stu-id="092cb-134">SRV</span></span> |<span data-ttu-id="092cb-135">tipo di record di servizio</span><span class="sxs-lookup"><span data-stu-id="092cb-135">service record type</span></span> |<span data-ttu-id="092cb-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="092cb-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="092cb-137"><sup>1</sup> consente solo un valore per ogni set di record.</span><span class="sxs-lookup"><span data-stu-id="092cb-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="092cb-138"><sup>2</sup> consente solo un tipo di record SOA per ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="092cb-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="092cb-139">Esempio di zona DNS nel formato Json:</span><span class="sxs-lookup"><span data-stu-id="092cb-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "The name of the DNS zone to be created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "The name of the DNS record to be created.  The name is relative to the zone, not the FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="092cb-140">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="092cb-140">Additional resources</span></span>
<span data-ttu-id="092cb-141">Per ulteriori informazioni, leggere la [documentazione dell'API REST per le zone DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) .</span><span class="sxs-lookup"><span data-stu-id="092cb-141">Read the [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="092cb-142">Leggere la [documentazione dell'API REST per i set di record DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="092cb-142">Read the [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

