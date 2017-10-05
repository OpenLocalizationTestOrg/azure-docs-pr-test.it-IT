---
ms.assetid: 
title: Scenari di sicurezza di Azure Key Vault | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="463ca-102">Scenari di sicurezza di Azure Key Vault e confini geografici</span><span class="sxs-lookup"><span data-stu-id="463ca-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="463ca-103">Azure Key Vault è un servizio multi-tenant e usa un pool di moduli di protezione Hardware (HSM) in ogni posizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="463ca-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="463ca-104">Tutti i moduli di protezione hardware nelle posizioni di Azure nella stessa area geografica condividono lo stesso limite di crittografia (ambiente di sicurezza Thales).</span><span class="sxs-lookup"><span data-stu-id="463ca-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="463ca-105">Ad esempio, gli Stati Uniti orientali e gli Stati Uniti occidentali condividono lo stesso scenario di sicurezza perché appartengono alla posizione geografica degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="463ca-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="463ca-106">Analogamente, tutte le posizioni di Azure in Giappone condividono lo stesso scenario di sicurezza e tutte le posizioni di Azure in Australia, in India e così via.</span><span class="sxs-lookup"><span data-stu-id="463ca-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="463ca-107">Comportamento di backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="463ca-107">Backup and restore behavior</span></span>

<span data-ttu-id="463ca-108">Un backup di una chiave presa da un insieme di credenziali della chiave in una posizione di Azure può essere ripristinato in un insieme di credenziali della chiave in un altra posizione di Azure, purché si verifichino entrambe le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="463ca-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="463ca-109">Entrambe le posizioni di Azure appartengono alla stessa posizione geografica</span><span class="sxs-lookup"><span data-stu-id="463ca-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="463ca-110">Entrambi gli insiemi di credenziali della chiave appartengono alla stessa sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="463ca-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="463ca-111">Ad esempio, un backup preso da una sottoscrizione data di una chiave in un insieme di credenziali della chiave in India occidentale, può essere ripristinato solo per un altro insieme di credenziali della chiave nella stessa sottoscrizione e località geografica: India occidentale, India centrale o India meridionale.</span><span class="sxs-lookup"><span data-stu-id="463ca-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="463ca-112">Aree e prodotti</span><span class="sxs-lookup"><span data-stu-id="463ca-112">Regions and products</span></span>

- [<span data-ttu-id="463ca-113">Aree di Azure</span><span class="sxs-lookup"><span data-stu-id="463ca-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="463ca-114">Prodotti Microsoft in base all'area</span><span class="sxs-lookup"><span data-stu-id="463ca-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="463ca-115">Le aree vengono mappate in scenari di sicurezza, visualizzati come intestazioni principali nelle tabelle:</span><span class="sxs-lookup"><span data-stu-id="463ca-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="463ca-116">Nei prodotti dell'articolo in base all'area, ad esempio, la scheda **Americhe** contiene Stati Uniti orientali, Stati Uniti centrali, Stati Uniti occidentali, tutti con il mapping eseguito per l'area delle Americhe.</span><span class="sxs-lookup"><span data-stu-id="463ca-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="463ca-117">Un'eccezione è che il Dipartimento della difesa Stati Uniti orientali e il Dipartimento della difesa Stati Uniti centrali hanno i propri scenari di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="463ca-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="463ca-118">Analogamente, nella scheda **Europa** l'Europa settentrionale e l'Europa occidentale eseguono entrambi il mapping nell'area Europa.</span><span class="sxs-lookup"><span data-stu-id="463ca-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="463ca-119">Lo stesso vale anche per la scheda **Asia Pacifico**.</span><span class="sxs-lookup"><span data-stu-id="463ca-119">The same is also true on the **Asia Pacific** tab.</span></span>



