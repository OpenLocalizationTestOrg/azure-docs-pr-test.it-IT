---
title: utilizzando criteri di autorizzazione chiave contenuto aaaConfigure hello portale di Azure | Documenti Microsoft
description: Informazioni su come tooconfigure criteri di autorizzazione per una chiave simmetrica.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Configurare i criteri di autorizzazione della chiave simmetrica
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Panoramica
Servizi multimediali di Microsoft Azure consente toodeliver MPEG-DASH, Smooth Streaming e i flussi HTTP-Live-Streaming (HLS) protetti con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS consente inoltre di toodeliver DASH streams crittografato con DRM Widevine. PlayReady sia Widevine vengono crittografati in base hello specifica la crittografia comune (ISO/IEC 23001-7 CENC).

Servizi multimediali fornisce inoltre un **servizio di distribuzione chiave licenza** da cui i client possono ottenere chiavi AES o PlayReady/Widevine licenze tooplay hello contenuto crittografato.

Questo argomento viene illustrato come toouse hello criteri di autorizzazione chiave del contenuto hello tooconfigure portale Azure. è possibile utilizzare successivamente chiave Hello toodynamically crittografare il contenuto. Si noti che attualmente è possibile crittografare i seguenti formati di streaming hello: HLS, MPEG DASH e Smooth Streaming. Non è possibile crittografare i download progressivi.

Quando un lettore richiede un flusso che è impostato toobe crittografati in modo dinamico, servizi multimediali Usa hello configurato chiave toodynamically crittografare il contenuto utilizzando la crittografia AES o DRM. flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello. Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.

Se si prevede di più chiavi simmetriche toohave o toospecify un **servizio di distribuzione chiave licenza** URL diverso dal servizio di distribuzione delle chiavi di servizi multimediali, hello usare Media Services .NET SDK o le API REST.

[Configurare i criteri di autorizzazione della chiave simmetrica mediante Media Services .NET SDK](media-services-dotnet-configure-content-key-auth-policy.md)

[Configurare i criteri di autorizzazione della chiave simmetrica mediante l'API REST di Servizi multimediali](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Considerazioni applicabili:
* Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. toostart streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, l'endpoint di streaming è toobe in hello **esecuzione** stato. 
* L'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva. Per altre informazioni, vedere l'articolo relativo alla [codifica di un asset](media-services-encode-asset.md).
* Hello del servizio di distribuzione delle chiavi memorizza nella cache ContentKeyAuthorizationPolicy e gli oggetti correlati (opzioni di criteri e restrizioni) per 15 minuti.  Se si crea un oggetto ContentKeyAuthorizationPolicy e specifica toouse una restrizione "Token", quindi eseguirne il test e si aggiornano i criteri di hello troppo "aperto" restrizione, richiederà circa 15 minuti prima di hello criteri commutatori toohello "Aperto" versione di hello criterio.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Procedura: configurare i criteri di autorizzazione chiave hello
criteri di autorizzazione chiave hello tooconfigure, seleziona hello **protezione del contenuto** pagina.

Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi. possono avere criteri di autorizzazione chiave del contenuto Hello **aprire**, **token**, o **IP** restrizioni (**IP** può essere configurato con REST o .NET SDK).

### <a name="open-restriction"></a>Restrizione Open
Hello **aprire** restrizione implica sistema hello recapiterà tooanyone di chiave hello che effettua una richiesta di chiave. Questa restrizione può essere utile a scopo di test.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Restrizione Token
token hello toochoose con restrizioni dei criteri, premere hello **TOKEN** pulsante.

Hello **token** criterio con restrizioni deve essere accompagnato da un token emesso da un **servizio Token di sicurezza** (STS). Servizi multimediali supporta i token in hello **token Web semplici** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **Token Web JSON** formato (JWT). Per informazioni, vedere [Autenticazione dei token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Servizi multimediali non fornisce **servizi token di sicurezza**. È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure. Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con hello specificato chiave e rilasciare le attestazioni specificate nella configurazione della restrizione token hello. Hello servizio di distribuzione delle chiavi di servizi multimediali restituirà client toohello chiave di crittografia hello se hello token è valido e hello attestazioni nel token hello corrispondono a quelli configurati per la chiave simmetrica hello. Per ulteriori informazioni, vedere [i token ACS di usare Azure tooissue](http://mingfeiy.com/acs-with-key-services).

Quando si configura hello **TOKEN** criterio con restrizioni, è necessario impostare i valori per **chiave di verifica**, **dell'autorità di certificazione** e **destinatari**. chiave di verifica primaria Hello contiene hello chiave che hello token è stato firmato con, autorità emittente è hello servizio token di sicurezza che rilascia token hello. destinatari Hello (talvolta denominato ambito) descrive finalità hello del token hello o hello risorse hello token autorizza l'accesso. Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.

### <a name="playready"></a>PlayReady
Quando si protegge il contenuto con **PlayReady**, uno di hello utili toospecify nei criteri di autorizzazione è una stringa XML che definisce il modello di licenza PlayReady hello. Per impostazione predefinita, è hello seguenti criteri:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices><ContentKey i:type="ContentEncryptionKeyFromHeader" /><LicenseType>Nonpersistent</LicenseType><PlayRight><AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput></PlayRight></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>

È possibile fare clic su hello **importare criteri xml** pulsante e fornire un diverso XML conforme a XML Schema definito toohello [qui](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

