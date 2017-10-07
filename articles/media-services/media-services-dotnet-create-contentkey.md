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
# <a name="create-contentkeys-with-net"></a>Creare entità ContentKey mediante .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Servizi multimediali consente toocreate e recapitare gli asset crittografati. Oggetto **ContentKey** fornisce l'accesso sicuro tooyour **Asset**s. 

Quando si crea un nuovo asset (ad esempio, prima di [caricare file](media-services-dotnet-upload-files.md)), è possibile specificare le opzioni di crittografia seguenti hello: **StorageEncrypted**, **CommonEncryptionProtected**, o **EnvelopeEncryptionProtected**. 

Quando si consegna asset tooyour client, è possibile [configurare per toobe asset crittografati in modo dinamico](media-services-dotnet-configure-asset-delivery-policy.md) con uno dei seguenti due crittografie hello: **DynamicEnvelopeEncryption** o  **DynamicCommonEncryption**.

Gli asset crittografati sono associati toobe **ContentKey**s. Questo articolo viene descritto come toocreate una chiave simmetrica.

> [!NOTE]
> Quando si crea un nuovo **StorageEncrypted** utilizzando asset hello Media Services .NET SDK, hello **ContentKey** viene automaticamente creato e collegato con asset hello.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Uno dei valori hello che è necessario impostare quando creare un tipo di contenuto chiave è di tipo di chiave simmetrica hello. Scegliere uno dei seguenti valori hello. 

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

## <a id="envelope_contentkey"></a>Creare un'entità ContentKey di tipo envelope
Hello frammento di codice seguente crea una chiave simmetrica hello busta del tipo di crittografia. Quindi associa la chiave hello asset specificato hello.

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

chiamare

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Creare un'entità ContentKey di tipo common
Hello frammento di codice seguente crea una chiave simmetrica hello comuni del tipo di crittografia. Quindi associa la chiave hello asset specificato hello.

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
chiamare

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

