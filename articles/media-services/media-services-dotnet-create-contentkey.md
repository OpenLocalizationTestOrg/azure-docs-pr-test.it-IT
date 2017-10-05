---
title: "Creare entità ContentKey mediante .NET"
description: Informazioni su come creare chiavi simmetriche che forniscono l'accesso sicuro agli asset.
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
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="31280-103">Creare entità ContentKey mediante .NET</span><span class="sxs-lookup"><span data-stu-id="31280-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31280-104">REST</span><span class="sxs-lookup"><span data-stu-id="31280-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="31280-105">.NET</span><span class="sxs-lookup"><span data-stu-id="31280-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="31280-106">Servizi multimediali consente di creare asset crittografati e distribuirli.</span><span class="sxs-lookup"><span data-stu-id="31280-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="31280-107">Un'entità **ContentKey** consente l'accesso sicuro alle entità **Asset**.</span><span class="sxs-lookup"><span data-stu-id="31280-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="31280-108">Quando si crea un nuovo asset, ad esempio prima di [caricare file](media-services-dotnet-upload-files.md), è possibile specificare le seguenti opzioni di crittografia: **StorageEncrypted**, **CommonEncryptionProtected** o **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="31280-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="31280-109">Quando si distribuiscono asset ai client, è possibile [configurarli per la crittografia dinamica](media-services-dotnet-configure-asset-delivery-policy.md) con una delle due seguenti opzioni: **DynamicEnvelopeEncryption** o **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="31280-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="31280-110">Gli asset crittografati devono essere associati alle entità **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="31280-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="31280-111">Questo articolo descrive come creare una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="31280-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="31280-112">Quando si crea un nuovo asset **StorageEncrypted** mediante Media Services .NET SDK, l'entità **ContentKey** viene creata automaticamente e collegata all'asset.</span><span class="sxs-lookup"><span data-stu-id="31280-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="31280-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="31280-113">ContentKeyType</span></span>
<span data-ttu-id="31280-114">Uno dei valori che è necessario impostare quando si crea una chiave simmetrica è quello relativo al tipo.</span><span class="sxs-lookup"><span data-stu-id="31280-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="31280-115">È possibile scegliere uno dei seguenti valori.</span><span class="sxs-lookup"><span data-stu-id="31280-115">Choose from one of the following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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

## <span data-ttu-id="31280-116"><a id="envelope_contentkey"></a>Creare un'entità ContentKey di tipo envelope</span><span class="sxs-lookup"><span data-stu-id="31280-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="31280-117">Il seguente frammento di codice crea una chiave simmetrica con tipo di crittografia envelope.</span><span class="sxs-lookup"><span data-stu-id="31280-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="31280-118">Associa quindi la chiave all'asset specificato.</span><span class="sxs-lookup"><span data-stu-id="31280-118">It then associates the key with the specified asset.</span></span>

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

<span data-ttu-id="31280-119">chiamare</span><span class="sxs-lookup"><span data-stu-id="31280-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="31280-120"><a id="common_contentkey"></a>Creare un'entità ContentKey di tipo common</span><span class="sxs-lookup"><span data-stu-id="31280-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="31280-121">Il seguente frammento di codice crea una chiave simmetrica con tipo di crittografia common.</span><span class="sxs-lookup"><span data-stu-id="31280-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="31280-122">Associa quindi la chiave all'asset specificato.</span><span class="sxs-lookup"><span data-stu-id="31280-122">It then associates the key with the specified asset.</span></span>

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

        // Associate the key with the asset.
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
<span data-ttu-id="31280-123">chiamare</span><span class="sxs-lookup"><span data-stu-id="31280-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="31280-124">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="31280-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="31280-125">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="31280-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

