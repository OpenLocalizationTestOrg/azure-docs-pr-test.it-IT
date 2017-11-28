---
title: aaaCreate chiavi simmetriche con REST | Documenti Microsoft
description: Informazioni su come accedono a tooAssets chiavi simmetriche toocreate che forniscono protezione.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95e9322b-168e-4a9d-8d5d-d7c946103745
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: cb3b74bdb72c43ab5b375c0376b6704f4a93bb8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="416fb-103">Creazione di entità ContentKey mediante REST</span><span class="sxs-lookup"><span data-stu-id="416fb-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="416fb-104">REST</span><span class="sxs-lookup"><span data-stu-id="416fb-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="416fb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="416fb-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="416fb-106">Servizi multimediali consente toocreate nuovo e recapitare gli asset crittografati.</span><span class="sxs-lookup"><span data-stu-id="416fb-106">Media Services enables you toocreate new and deliver encrypted assets.</span></span> <span data-ttu-id="416fb-107">Oggetto **ContentKey** fornisce l'accesso sicuro tooyour **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="416fb-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="416fb-108">Quando si crea un nuovo asset (ad esempio, prima di [caricare file](media-services-rest-upload-files.md)), è possibile specificare le opzioni di crittografia seguenti hello: **StorageEncrypted**, **CommonEncryptionProtected**, o **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="416fb-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="416fb-109">Quando si consegna asset tooyour client, è possibile [configurare per toobe asset crittografati in modo dinamico](media-services-rest-configure-asset-delivery-policy.md) con uno dei seguenti due crittografie hello: **DynamicEnvelopeEncryption** o  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="416fb-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="416fb-110">Gli asset crittografati sono associati toobe **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="416fb-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="416fb-111">Questo articolo viene descritto come toocreate una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="416fb-111">This article describes how toocreate a content key.</span></span>

<span data-ttu-id="416fb-112">Hello seguenti sono passaggi generali per la generazione di chiavi simmetriche che si assoceranno le risorse che si desidera toobe crittografati.</span><span class="sxs-lookup"><span data-stu-id="416fb-112">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="416fb-113">Generare in modo casuale una chiave AES a 16 byte (per la crittografia common e envelope) o a 32 byte (per la crittografia di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="416fb-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="416fb-114">Questo sarà una chiave simmetrica di hello dell'asset, ovvero tutti i file associati con asset sarà necessario toouse hello stessa chiave simmetrica durante la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="416fb-114">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="416fb-115">Chiamare hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) e [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget metodi hello corretto certificato x. 509 che deve essere utilizzato tooencrypt la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="416fb-115">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="416fb-116">Crittografare la chiave simmetrica con la chiave pubblica hello di hello certificato x. 509.</span><span class="sxs-lookup"><span data-stu-id="416fb-116">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="416fb-117">Quando si esegue la crittografia di hello, Media Services .NET SDK Usa RSA con OAEP.</span><span class="sxs-lookup"><span data-stu-id="416fb-117">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="416fb-118">È possibile vedere un esempio in hello [EncryptSymmetricKeyData funzione](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="416fb-118">You can see an example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="416fb-119">Creare un valore di checksum (basato su hello algoritmo di checksum chiave AES PlayReady) calcolato usando l'identificatore di chiave hello e chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="416fb-119">Create a checksum value (based on hello PlayReady AES key checksum algorithm) calculated using hello key identifier and content key.</span></span> <span data-ttu-id="416fb-120">Per ulteriori informazioni, vedere la sezione "Algoritmo di Checksum chiave AES PlayReady" del documento oggetto intestazione PlayReady hello hello trova [qui](http://www.microsoft.com/playready/documents/).</span><span class="sxs-lookup"><span data-stu-id="416fb-120">For more information, see hello “PlayReady AES Key Checksum Algorithm” section of hello PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="416fb-121">Hello seguito è riportato un esempio di .NET che consente di calcolare il checksum hello usando hello GUID parte dell'identificatore di chiave hello e hello deselezionare la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="416fb-121">hello following is a .NET example that calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

         public static string CalculateChecksum(byte[] contentKey, Guid keyId)
         {

            byte[] array = null;
            using (AesCryptoServiceProvider aesCryptoServiceProvider = new AesCryptoServiceProvider())
            {
                aesCryptoServiceProvider.Mode = CipherMode.ECB;
                aesCryptoServiceProvider.Key = contentKey;
                aesCryptoServiceProvider.Padding = PaddingMode.None;
                ICryptoTransform cryptoTransform = aesCryptoServiceProvider.CreateEncryptor();
                array = new byte[16];
                cryptoTransform.TransformBlock(keyId.ToByteArray(), 0, 16, array, 0);
            }
            byte[] array2 = new byte[8];
            Array.Copy(array, array2, 8);
            return Convert.ToBase64String(array2);
         }
5. <span data-ttu-id="416fb-122">Creare la chiave simmetrica hello con hello **proprietà EncryptedContentKey** (convertito stringa codificata in formato toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, e **Checksum** valori ricevuti nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="416fb-122">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="416fb-123">Associare hello **ContentKey** entità con la **Asset** entità tramite l'operazione di hello $links.</span><span class="sxs-lookup"><span data-stu-id="416fb-123">Associate hello **ContentKey** entity with your **Asset** entity through hello $links operation.</span></span>

<span data-ttu-id="416fb-124">Si noti che in questo argomento Mostra come toogenerate una chiave AES, crittografare la chiave hello e calcolo del checksum hello.</span><span class="sxs-lookup"><span data-stu-id="416fb-124">Note that this topic does not show how toogenerate an AES key, encrypt hello key, and calculate hello checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="416fb-125">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="416fb-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="416fb-126">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="416fb-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="416fb-127">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="416fb-127">Connect tooMedia Services</span></span>

<span data-ttu-id="416fb-128">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="416fb-128">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="416fb-129">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="416fb-129">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="416fb-130">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="416fb-130">You must make subsequent calls toohello new URI.</span></span>

## <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="416fb-131">Recuperare ProtectionKeyId hello</span><span class="sxs-lookup"><span data-stu-id="416fb-131">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="416fb-132">Hello di esempio seguente viene illustrato come tooretrieve hello ProtectionKeyId, un'identificazione personale del certificato, per il certificato di hello è necessario utilizzare per crittografare la chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="416fb-132">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="416fb-133">Eseguire questo passaggio toomake di avere già certificato appropriato hello nel computer.</span><span class="sxs-lookup"><span data-stu-id="416fb-133">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="416fb-134">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="416fb-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="416fb-135">Risposta:</span><span class="sxs-lookup"><span data-stu-id="416fb-135">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

## <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="416fb-136">Recuperare ProtectionKey di hello per hello ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="416fb-136">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="416fb-137">Hello esempio seguente viene illustrato come tooretrieve hello x. 509 usando ProtectionKeyId hello ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="416fb-137">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="416fb-138">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="416fb-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="416fb-139">Risposta:</span><span class="sxs-lookup"><span data-stu-id="416fb-139">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

## <a name="create-hello-contentkey"></a><span data-ttu-id="416fb-140">Creare hello ContentKey</span><span class="sxs-lookup"><span data-stu-id="416fb-140">Create hello ContentKey</span></span>
<span data-ttu-id="416fb-141">Dopo aver recuperato certificato x. 509 hello e utilizzato relativo tooencrypt chiave pubblica della chiave simmetrica, creare un **ContentKey** entità e set di conseguenza i valori delle relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="416fb-141">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="416fb-142">Uno dei valori hello che è necessario impostare quando creare hello contenuto chiave è di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="416fb-142">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="416fb-143">Scegliere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="416fb-143">Choose from one of hello following values.</span></span>

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


<span data-ttu-id="416fb-144">Hello seguente esempio viene illustrato come toocreate un **ContentKey** con un **ContentKeyType** impostato per la crittografia di archiviazione ("1") e hello **ProtectionKeyType** impostare troppo "0" tooindicate che hello Id chiave di protezione è l'identificazione personale del certificato x. 509 di hello.</span><span class="sxs-lookup"><span data-stu-id="416fb-144">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="416fb-145">Richiesta</span><span class="sxs-lookup"><span data-stu-id="416fb-145">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }


<span data-ttu-id="416fb-146">Risposta:</span><span class="sxs-lookup"><span data-stu-id="416fb-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="416fb-147">Associare hello ContentKey a un Asset</span><span class="sxs-lookup"><span data-stu-id="416fb-147">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="416fb-148">Dopo la creazione di hello ContentKey, associarlo all'Asset usando l'operazione di hello $links, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="416fb-148">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="416fb-149">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="416fb-149">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net


    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="416fb-150">Risposta:</span><span class="sxs-lookup"><span data-stu-id="416fb-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="416fb-151">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="416fb-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="416fb-152">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="416fb-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

