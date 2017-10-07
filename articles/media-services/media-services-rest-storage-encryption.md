---
title: aaaEncrypting i contenuti con crittografia di archiviazione tramite l'API REST AMS
description: Informazioni su come tooencrypt i contenuti con crittografia di archiviazione usando le API REST AMS.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>Crittografare il contenuto con la crittografia di archiviazione

Si consiglia di tooencrypt il contenuto localmente con AES-256 bit crittografia e quindi caricarla tooAzure archiviazione in cui verrà archiviata in forma crittografata.

In questo articolo viene fornita una panoramica di crittografia di archiviazione AMS e illustra la modalità di archiviazione hello tooupload crittografia contenuto:

* Creare una chiave simmetrica.
* Creare un asset. Impostare hello AssetCreationOption tooStorageEncryption durante la creazione di hello Asset.
  
     Gli asset crittografati sono toobe associata a chiavi simmetriche.
* Asset toohello chiave contenuto hello di collegamento.  
* Impostare i parametri per le entità AssetFile hello relative a crittografia di hello.

## <a name="considerations"></a>Considerazioni 

Se si desidera toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello. Prima dell'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificati criteri di distribuzione. Per altre informazioni, vedere l'articolo [Procedura: Configurare i criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).

Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>Connessione dei servizi tooMedia

Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.

## <a name="storage-encryption-overview"></a>Panoramica della crittografia di archiviazione.
si applica la crittografia di archiviazione Hello AMS **AES CTR** intero file di modalità crittografia toohello.  La modalità CTR-AES è una crittografia a blocchi in grado di crittografare dati di lunghezza arbitraria senza bisogno di spaziatura interna. Eseguita mediante la crittografia di un blocco di contatore con l'algoritmo AES hello e quindi l'output di hello XOR ing di AES con tooencrypt dati hello o decrittografare.  blocco di contatore Hello utilizzato viene creato copiando il valore di hello di hello vettore di inizializzazione toobytes 0 too7 del valore del contatore hello e too15 di 8 byte del valore del contatore hello impostati toozero. Del blocco del contatore di 16 byte hello, too15 di 8 byte (ad esempio hello il byte meno significativi) vengono utilizzato come un intero senza segno a 64 bit semplice che viene incrementato di uno per ogni blocco successivo di elaborazione dati ed è mantenuta in ordine di byte di rete. Si noti che se questo numero intero raggiunga il valore massimo a hello (0xFFFFFFFFFFFFFFFF) quindi incrementarlo Reimposta hello blocco contatore toozero (8 byte too15) senza influire su altri hello 64 bit del contatore hello (vale a dire too7 byte 0).   In ordine toomaintain hello sicurezza della crittografia modalità hello AES CTR hello valore vettore di inizializzazione per un determinato identificatore di chiave per ogni chiave simmetrica deve essere univoco per ogni file e i file devono essere minore di 2 ^ 64 blocchi in lunghezza.  Si tratta di tooensure che un valore del contatore non viene mai riutilizzato con una chiave specificata. Per ulteriori informazioni sulla modalità di hello CTR, vedere [pagina wiki](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (articolo wiki hello utilizza il termine hello "Nonce" anziché "Vettore di inizializzazione").

Utilizzare **crittografia di archiviazione** tooencrypt il contenuto non crittografato localmente con AES-256 bit crittografia e quindi caricarla tooAzure archiviazione dove viene archiviato in forma crittografata. Gli asset protetti con crittografia di archiviazione vengono decrittografati automaticamente e inseriti in un file crittografato sistema precedente tooencoding e, facoltativamente, crittografare nuovamente toouploading precedente come nuovo asset di output. Hello primario per la crittografia di archiviazione viene usata quando si desidera toosecure file multimediali di input di alta qualità applicando una crittografia avanzata rest su disco.

In ordine toodeliver asset crittografato di archiviazione, è necessario configurare i criteri di distribuzione dell'asset hello in modo da servizi multimediali come toodeliver il contenuto. Prima che l'asset può essere trasmesso, hello streaming flussi e crittografia di archiviazione hello viene rimosso il server dei contenuti usando hello specificato criterio di recapito (ad esempio, AES, crittografia comune o Nessuna crittografia).

## <a name="create-contentkeys-used-for-encryption"></a>Creare chiavi simmetriche per la crittografia
Gli asset crittografati sono toobe associato alla chiave di crittografia di archiviazione. È necessario creare hello contenuto toobe chiave utilizzata per la crittografia prima di creare file di asset di hello. Questa sezione viene descritto come toocreate una chiave simmetrica.

Hello seguenti sono passaggi generali per la generazione di chiavi simmetriche che si assoceranno le risorse che si desidera toobe crittografati. 

1. Per la crittografia di archiviazione, generare in modo casuale una chiave AES a 32 byte. 
   
    Questo sarà una chiave simmetrica di hello dell'asset, ovvero tutti i file associati con asset sarà necessario toouse hello stessa chiave simmetrica durante la decrittografia. 
2. Chiamare hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) e [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget metodi hello corretto certificato x. 509 che deve essere utilizzato tooencrypt la chiave simmetrica.
3. Crittografare la chiave simmetrica con la chiave pubblica hello di hello certificato x. 509. 
   
   Quando si esegue la crittografia di hello, Media Services .NET SDK Usa RSA con OAEP.  È possibile visualizzare un esempio di .NET in hello [EncryptSymmetricKeyData funzione](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Creare un valore di checksum calcolato usando l'identificatore di chiave hello e chiave simmetrica. Hello .NET esempio seguente calcola il checksum di hello usando hello GUID parte dell'identificatore di chiave hello e hello deselezionare la chiave simmetrica.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Creare la chiave simmetrica hello con hello **proprietà EncryptedContentKey** (convertito stringa codificata in formato toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, e **Checksum** valori ricevuti nei passaggi precedenti.

    Per la crittografia di archiviazione, hello proprietà seguenti devono essere incluse nel corpo della richiesta hello.

    Proprietà del corpo della richiesta    | Descrizione
    ---|---
    ID | Hello ContentKey Id che viene generato effettuata utilizzando hello seguente formato, "NB:<NEW GUID>".
    ContentKeyType | Questo è il tipo di chiave simmetrica di hello come numero intero per questa chiave simmetrica. Passato valore hello 1 per la crittografia di archiviazione.
    EncryptedContentKey | Viene creato un nuovo valore di chiave simmetrica che corrisponde a un valore a 256 bit (32 byte). crittografia della chiave Hello mediante hello certificato crittografia di archiviazione x. 509 che viene recuperato da servizi multimediali di Microsoft Azure tramite l'esecuzione di una richiesta HTTP GET per hello GetProtectionKeyId e GetProtectionKey metodi. Ad esempio, vedere hello seguente di codice .NET: hello **EncryptSymmetricKeyData** metodo definito [qui](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Questo è hello id chiave di protezione per hello certificato crittografia di archiviazione x. 509 che è stato utilizzato tooencrypt la chiave simmetrica.
    ProtectionKeyType | Questo è il tipo di crittografia per la chiave di protezione hello che è stato utilizzato tooencrypt chiave simmetrica di hello hello. Per l'esempio questo valore è StorageEncryption(1).
    Checksum |checksum calcolato di Hello MD5 per la chiave simmetrica hello. Viene calcolato crittografando l'Id contenuto hello con chiave simmetrica hello. codice di esempio Hello viene illustrato come toocalculate hello checksum.


### <a name="retrieve-hello-protectionkeyid"></a>Recuperare ProtectionKeyId hello
Hello di esempio seguente viene illustrato come tooretrieve hello ProtectionKeyId, un'identificazione personale del certificato, per il certificato di hello è necessario utilizzare per crittografare la chiave simmetrica. Eseguire questo passaggio toomake di avere già certificato appropriato hello nel computer.

Richiesta:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Risposta:

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Recuperare ProtectionKey di hello per hello ProtectionKeyId
Hello esempio seguente viene illustrato come tooretrieve hello x. 509 usando ProtectionKeyId hello ottenuto nel passaggio precedente hello.

Richiesta:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Risposta:

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

### <a name="create-hello-content-key"></a>Creare una chiave simmetrica hello
Dopo aver recuperato certificato x. 509 hello e utilizzato relativo tooencrypt chiave pubblica della chiave simmetrica, creare un **ContentKey** entità e set di conseguenza i valori delle relative proprietà.

Uno dei valori hello che è necessario impostare quando creare hello contenuto chiave è di tipo hello. In caso di crittografia di archiviazione hello, hello è '1'. 

Hello seguente esempio viene illustrato come toocreate un **ContentKey** con un **ContentKeyType** impostato per la crittografia di archiviazione ("1") e hello **ProtectionKeyType** impostare troppo "0" tooindicate che hello Id chiave di protezione è l'identificazione personale del certificato x. 509 di hello.  

Richiesta

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

Risposta:

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

## <a name="create-an-asset"></a>Creare un asset
Hello seguente esempio viene illustrato come toocreate un asset.

**Richiesta HTTP**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

**Risposta HTTP**

Se ha esito positivo, viene restituito l'esempio hello:

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a>Associare hello ContentKey a un Asset
Dopo la creazione di hello ContentKey, associarlo all'Asset usando l'operazione di hello $links, come illustrato nell'esempio seguente hello:

Richiesta:

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

Risposta:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Creare un'entità AssetFile
Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entità rappresenta un file video o audio che viene archiviato in un contenitore blob. Un file di asset è sempre associato a un asset e un asset può contenere uno o più file. attività di Media Services Encoder Hello non riesce se un oggetto di file di asset non è associato a un file digitale in un contenitore blob.

Si noti che hello **AssetFile** istanza e hello effettivo file multimediale sono due oggetti distinti. istanza di AssetFile Hello contiene i metadati relativi a file di supporto hello, mentre i file di supporto hello contiene hello effettivo contenuto multimediale.

Dopo aver caricato il file multimediale digitale in un contenitore blob, si utilizzerà hello **MERGE** hello tooupdate HTTP richiesta AssetFile con le informazioni nel file multimediale (non illustrato in questo argomento). 

**Richiesta HTTP**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

**Risposta HTTP**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
