---
title: le licenze di servizi multimediali tooAzure aaaUsing castLabs toodeliver Widevine | Documenti Microsoft
description: In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs. la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e viene recapitata licenze Widevine dal server licenze castLabs.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>Utilizzando castLabs toodeliver Widevine licenze tooAzure servizi multimediali
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Panoramica
In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs. la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e licenze Widevine viene recapitata da **castLabs** server licenze.

streaming di contenuto protetto tooplayback CENC (PlayReady e/o Widevine), è possibile usare [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Per informazioni dettagliate vedere la [documentazione dell’AMP](http://amp.azure.net/libs/amp/latest/docs/)

Hello seguente diagramma viene illustrata un'architettura di integrazione di servizi multimediali di Azure e castLabs ad alto livello.

![integrazione](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Configurazione di sistema tipica
* I contenuti multimediali vengono archiviati in Servizi multimediali di Azure.
* Gli ID delle chiavi simmetriche vengono archiviati sia in castLabs sia in Servizi multimediali di Azure.
* castLabs e Servizi multimediali di Azure dispongono entrambi di un sistema di autenticazione dei token integrato. Hello le sezioni seguenti illustrano i token di autenticazione. 
* Quando un client richiede video hello toostream, il contenuto di hello è crittografato in modo dinamico con **crittografia comune** (CENC) e compresso in modo dinamico dal sistema AMS tooSmooth Streaming e trattino. Viene inoltre fornita la crittografia dei flussi elementari M2TS PlayReady per il protocollo di streaming HLS.
* La licenza per PlayReady viene recuperata dal server licenze di Servizi multimediali di Azure, mentre la licenza per Widevine viene recuperata dal server licenze castLabs. 
* Media Player automaticamente decide quali toofetch di licenza in base alle funzionalità di piattaforma client hello. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Generazione di token di autenticazione per ottenere una licenza
CastLabs e AMS supportano entrambi JWT (JSON Web Token) formato di token utilizzato tooauthorize una licenza. 

### <a name="jwt-token-in-ams"></a>Token JWT in Servizi multimediali di Azure
Hello nella tabella seguente descrive i token JWT in AMS. 

| Issuer | Stringa dell'autorità di certificazione da hello scelto servizio Token (sicurezza) |
| --- | --- |
| Audience |Stringa di destinatari da hello utilizzata servizio token di sicurezza |
| Claims |Set di attestazioni |
| NotBefore |Inizio validità del token hello |
| Expires |Fine validità del token hello |
| SigningCredentials |chiave Hello condiviso tra i Server licenze PlayReady, castLabs Server licenze e servizio token di sicurezza, potrebbe trattarsi di una chiave simmetrica o asimmetrica. |

### <a name="jwt-token-in-castlabs"></a>Token JWT in castLabs
Hello nella tabella seguente descrive i token JWT in castLabs. 

| Nome | Descrizione |
| --- | --- |
| optData |Stringa JSON contenente informazioni relative all'utente. |
| crt |Oggetto JSON stringa contenente informazioni sull'asset hello, i relativi diritti di licenza info e la riproduzione. |
| iat |Hello data/ora corrente nel periodo. |
| jti |Identificatore univoco su questo token (ogni token sono utilizzabili solo una volta nel sistema castLabs hello). |

## <a name="sample-solution-set-up"></a>Configurazione della soluzione di esempio
Hello [soluzione di esempio](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) è costituito da due progetti:

* Un'applicazione console che può essere presenti restrizioni DRM tooset utilizzata su una risorsa già acquisita, per PlayReady e Widevine.
* Un'applicazione Web incaricata della distribuzione dei token, che possono essere considerati come una versione molto semplificata di un servizio token di sicurezza.

applicazione console hello toouse:

1. Modificare le credenziali toosetup AMS di hello app. config, castLabs credenziali, configurazione di servizio token di sicurezza e una chiave condivisa.
2. Caricare un asset in Servizi multimediali di Azure.
3. Get hello UUID da hello caricato Asset e modificare 32 riga nel file Program.cs hello:
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Usare un AssetId per la denominazione asset hello nel sistema castLabs hello (44 riga nel file Program.cs hello).
   
   È necessario impostare AssetId per **castLabs**; è necessario toobe una stringa alfanumerica univoca.
5. Eseguire il programma hello.

hello toouse applicazione Web (STS):

1. Merchant castlabs di modifica hello Web. config toosetup ID, la configurazione di STS hello e chiave condivisa hello.
2. Distribuire tooAzure siti Web.
3. Passare sito Web toohello.

## <a name="playing-back-a-video"></a>Riproduzione di un video
tooplayback un video crittografata con la crittografia comune (PlayReady e/o Widevine), è possibile usare hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Quando si esegue l'applicazione console hello, vengono restituite hello ID chiave contenuto e hello manifesto URL.

1. Aprire una nuova scheda e avviare il servizio token di sicurezza: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Andare troppo[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Incollare in hello URL di streaming.
4. Fare clic su hello **opzioni avanzate** casella di controllo.
5. In hello **protezione** elenco a discesa selezionare PlayReady e/o Widevine.
6. Incollare il token hello recuperato dal servizio token di sicurezza nella casella di testo hello Token. 
   
   server licenze di Hello castLab non è necessario hello "portatore =" prefisso token hello. Pertanto, rimuovere prima di inviare il token hello.
7. Aggiornare Windows Media player hello.
8. Hello video deve essere in esecuzione.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

