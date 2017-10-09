## <a name="azure-dns"></a><span data-ttu-id="5caad-101">DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="5caad-101">Azure DNS</span></span>
<span data-ttu-id="5caad-102">DNS di Azure è un servizio di hosting per i domini DNS, che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5caad-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="5caad-103">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5caad-103">Property</span></span> | <span data-ttu-id="5caad-104">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5caad-104">Description</span></span> | <span data-ttu-id="5caad-105">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="5caad-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5caad-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="5caad-106">**DNSzones**</span></span> |<span data-ttu-id="5caad-107">Record DNS toohost delle informazioni di zona di dominio di un determinato dominio</span><span class="sxs-lookup"><span data-stu-id="5caad-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="5caad-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5caad-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="5caad-109">Set di record DNS</span><span class="sxs-lookup"><span data-stu-id="5caad-109">DNS record sets</span></span>
<span data-ttu-id="5caad-110">Le zone DNS dispongono di un oggetto figlio denominato set di record.</span><span class="sxs-lookup"><span data-stu-id="5caad-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="5caad-111">I set di record sono una raccolta di record host in base al tipo per una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5caad-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="5caad-112">I tipi record sono A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="5caad-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="5caad-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5caad-113">Property</span></span> | <span data-ttu-id="5caad-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5caad-114">Description</span></span> | <span data-ttu-id="5caad-115">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="5caad-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5caad-116">A</span><span class="sxs-lookup"><span data-stu-id="5caad-116">A</span></span> |<span data-ttu-id="5caad-117">Tipo di record IPv4</span><span class="sxs-lookup"><span data-stu-id="5caad-117">IPv4 record type</span></span> |<span data-ttu-id="5caad-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="5caad-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="5caad-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="5caad-119">AAAA</span></span> |<span data-ttu-id="5caad-120">Tipo di record IPv6</span><span class="sxs-lookup"><span data-stu-id="5caad-120">IPv6 record type</span></span> |<span data-ttu-id="5caad-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="5caad-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="5caad-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="5caad-122">CNAME</span></span> |<span data-ttu-id="5caad-123">tipo di record di nome canonical <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="5caad-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="5caad-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="5caad-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="5caad-125">MX</span><span class="sxs-lookup"><span data-stu-id="5caad-125">MX</span></span> |<span data-ttu-id="5caad-126">Tipo di record di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5caad-126">mail record type</span></span> |<span data-ttu-id="5caad-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="5caad-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="5caad-128">NS</span><span class="sxs-lookup"><span data-stu-id="5caad-128">NS</span></span> |<span data-ttu-id="5caad-129">tipo di record di nome del server</span><span class="sxs-lookup"><span data-stu-id="5caad-129">name server record type</span></span> |<span data-ttu-id="5caad-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="5caad-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="5caad-131">SOA</span><span class="sxs-lookup"><span data-stu-id="5caad-131">SOA</span></span> |<span data-ttu-id="5caad-132">Tipo di record di "Start of Authority" <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="5caad-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="5caad-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="5caad-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="5caad-134">SRV</span><span class="sxs-lookup"><span data-stu-id="5caad-134">SRV</span></span> |<span data-ttu-id="5caad-135">tipo di record di servizio</span><span class="sxs-lookup"><span data-stu-id="5caad-135">service record type</span></span> |<span data-ttu-id="5caad-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="5caad-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="5caad-137"><sup>1</sup> consente solo un valore per ogni set di record.</span><span class="sxs-lookup"><span data-stu-id="5caad-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="5caad-138"><sup>2</sup> consente solo un tipo di record SOA per ogni zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5caad-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="5caad-139">Esempio di zona DNS nel formato Json:</span><span class="sxs-lookup"><span data-stu-id="5caad-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
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

## <a name="additional-resources"></a><span data-ttu-id="5caad-140">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5caad-140">Additional resources</span></span>
<span data-ttu-id="5caad-141">Hello lettura [documentazione dell'API REST per le zone DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="5caad-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="5caad-142">Hello lettura [documentazione dell'API REST per i set di record DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="5caad-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

