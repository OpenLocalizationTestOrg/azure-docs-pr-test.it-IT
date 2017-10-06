---
ms.assetid: 
title: ambienti di sicurezza separati insieme di credenziali chiave aaaAzure | Documenti Microsoft
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="8b999-102">Scenari di sicurezza di Azure Key Vault e confini geografici</span><span class="sxs-lookup"><span data-stu-id="8b999-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="8b999-103">Azure Key Vault è un servizio multi-tenant e usa un pool di moduli di protezione Hardware (HSM) in ogni posizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b999-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="8b999-104">Tutti i moduli di protezione hardware in Azure posizioni hello stessa area geografica condividono hello stesso limite di crittografia (ambiente di sicurezza Thales).</span><span class="sxs-lookup"><span data-stu-id="8b999-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="8b999-105">Stati Uniti orientali e condividere Stati Uniti occidentali, ad esempio, hello stesso ambiente di sicurezza perché appartengono località geografica toohello Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="8b999-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="8b999-106">Analogamente, tutte le posizioni di Azure nella condivisione Giappone hello world protezione stesso e tutte le posizioni di Azure in Australia, India e così via.</span><span class="sxs-lookup"><span data-stu-id="8b999-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="8b999-107">Comportamento di backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="8b999-107">Backup and restore behavior</span></span>

<span data-ttu-id="8b999-108">Un backup di una chiave da un insieme di credenziali chiave in una località di Azure può essere ripristinato tooa insieme di credenziali delle chiavi in un altro percorso di Azure, purché entrambe queste condizioni sono vere:</span><span class="sxs-lookup"><span data-stu-id="8b999-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="8b999-109">Entrambi hello Azure percorsi appartengono toohello stessa area geografica</span><span class="sxs-lookup"><span data-stu-id="8b999-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="8b999-110">Entrambi gli insiemi di credenziali chiave hello appartengono toohello stessa sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="8b999-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="8b999-111">Ad esempio, un backup eseguito da una specifica sottoscrizione di una chiave in un insieme di credenziali chiave India occidentale, può essere solo insieme di credenziali chiave tooanother ripristinato in hello stessa sottoscrizione e posizione geografica. India occidentale, India centrale o India meridionale.</span><span class="sxs-lookup"><span data-stu-id="8b999-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="8b999-112">Aree e prodotti</span><span class="sxs-lookup"><span data-stu-id="8b999-112">Regions and products</span></span>

- [<span data-ttu-id="8b999-113">Aree di Azure</span><span class="sxs-lookup"><span data-stu-id="8b999-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="8b999-114">Prodotti Microsoft in base all'area</span><span class="sxs-lookup"><span data-stu-id="8b999-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="8b999-115">Le aree sono mappate toosecurity mondi, visualizzati come intestazioni principale nelle tabelle di hello:</span><span class="sxs-lookup"><span data-stu-id="8b999-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="8b999-116">Prodotti hello dall'articolo area, ad esempio, hello **Americas** scheda contiene est US, Stati Uniti centrali, Stati Uniti OCCIDENTALI tutti i mapping toohello Americas area.</span><span class="sxs-lookup"><span data-stu-id="8b999-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="8b999-117">Un'eccezione è che il Dipartimento della difesa Stati Uniti orientali e il Dipartimento della difesa Stati Uniti centrali hanno i propri scenari di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8b999-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="8b999-118">Analogamente, sul hello **Europe** scheda, Europa settentrionale ed Europa occidentale eseguono entrambi il mapping area Europa toohello.</span><span class="sxs-lookup"><span data-stu-id="8b999-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="8b999-119">Hello stesso vale anche nel hello **Asia-Pacifico** scheda.</span><span class="sxs-lookup"><span data-stu-id="8b999-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



