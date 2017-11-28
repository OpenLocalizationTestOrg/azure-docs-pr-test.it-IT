---
title: aaaCreate ContentKeys con .NET
description: Informazioni su come accedono a tooAssets chiavi simmetriche toocreate che forniscono protezione.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="f4330-103">Creare entità ContentKey mediante .NET</span><span class="sxs-lookup"><span data-stu-id="f4330-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4330-104">REST</span><span class="sxs-lookup"><span data-stu-id="f4330-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="f4330-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f4330-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="f4330-106">Servizi multimediali consente toocreate e recapitare gli asset crittografati.</span><span class="sxs-lookup"><span data-stu-id="f4330-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="f4330-107">Oggetto **ContentKey** fornisce l'accesso sicuro tooyour **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="f4330-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="f4330-108">Quando si crea un nuovo asset (ad esempio, prima di [caricare file](media-services-dotnet-upload-files.md)), è possibile specificare le opzioni di crittografia seguenti hello: **StorageEncrypted**, **CommonEncryptionProtected**, o **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="f4330-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="f4330-109">Quando si consegna asset tooyour client, è possibile [configurare per toobe asset crittografati in modo dinamico](media-services-dotnet-configure-asset-delivery-policy.md) con uno dei seguenti due crittografie hello: **DynamicEnvelopeEncryption** o  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="f4330-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="f4330-110">Gli asset crittografati sono associati toobe **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="f4330-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="f4330-111">Questo articolo viene descritto come toocreate una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="f4330-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="f4330-112">Quando si crea un nuovo **StorageEncrypted** utilizzando asset hello Media Services .NET SDK, hello **ContentKey** viene automaticamente creato e collegato con asset hello.</span><span class="sxs-lookup"><span data-stu-id="f4330-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="f4330-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="f4330-113">ContentKeyType</span></span>
<span data-ttu-id="f4330-114">Uno dei valori hello che è necessario impostare quando creare un tipo di contenuto chiave è di tipo di chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="f4330-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="f4330-115">Scegliere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="f4330-115">Choose from one of hello following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <span data-ttu-id="f4330-116"><a id="envelope_contentkey"></a>Creare un'entità ContentKey di tipo envelope</span><span class="sxs-lookup"><span data-stu-id="f4330-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="f4330-117">Hello frammento di codice seguente crea una chiave simmetrica hello busta del tipo di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f4330-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="f4330-118">Quindi associa la chiave hello asset specificato hello.</span><span class="sxs-lookup"><span data-stu-id="f4330-118">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="f4330-119">chiamare</span><span class="sxs-lookup"><span data-stu-id="f4330-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="f4330-120"><a id="common_contentkey"></a>Creare un'entità ContentKey di tipo common</span><span class="sxs-lookup"><span data-stu-id="f4330-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="f4330-121">Hello frammento di codice seguente crea una chiave simmetrica hello comuni del tipo di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f4330-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="f4330-122">Quindi associa la chiave hello asset specificato hello.</span><span class="sxs-lookup"><span data-stu-id="f4330-122">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="f4330-123">chiamare</span><span class="sxs-lookup"><span data-stu-id="f4330-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="f4330-124">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f4330-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4330-125">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f4330-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

