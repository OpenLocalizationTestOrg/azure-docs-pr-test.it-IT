---
title: criteri di protezione del contenuto aaaConfiguring usando hello portale di Azure | Documenti Microsoft
description: In questo articolo viene illustrato come toouse hello tooconfigure portale Azure i criteri di protezione del contenuto. Hello articolo inoltre illustrato come tooenable crittografia dinamica per le risorse.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Configurazione dei criteri di protezione del contenuto tramite hello portale di Azure
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Panoramica
Microsoft Azure Media Services (AMS) consente di toosecure gli elementi multimediali dal tempo hello che lascia computer tramite l'archiviazione, elaborazione e il recapito. Servizi multimediali consente toodeliver il contenuto è crittografato in modo dinamico con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit), common encryption (CENC) con PlayReady e/o DRM Widevine e FairPlay di Apple. 

AMS fornisce un servizio per la distribuzione di licenze DRM e i client tooauthorized chiavi non crittografata AES. Hello portale di Azure consente toocreate uno **criteri di autorizzazione chiave licenza** per tutti i tipi di crittografia.

In questo articolo viene illustrato come tooconfigure contenuto criteri di protezione con hello portale di Azure. Hello articolo inoltre illustrato come asset di tooyour tooapply crittografia dinamica.


> [!NOTE]
> Se si usa criteri di protezione di Azure toocreate portale classico di hello, criteri hello potrebbero emergere hello [portale di Azure](https://portal.azure.com/). Tuttavia, tutti hello precedente criteri ancora esiste. È possibile esaminarli utilizzando hello Azure Media Services .NET SDK o hello [Esplora servizi di supporto di Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) strumento (criteri hello toosee, pulsante destro del mouse su asset hello -> visualizzazione di informazioni (F4) -> fare clic su chiavi simmetriche -> scheda Fare clic sulla chiave hello). 
> 
> Se si desidera tooencrypt all'asset usando i nuovi criteri, configurarli con hello portale di Azure, fare clic su Salva e riapplicare la crittografia dinamica. 
> 
> 

## <a name="start-configuring-content-protection"></a>Avviare la configurazione della protezione del contenuto
portale toostart hello toouse la configurazione di protezione del contenuto, account globali tooyour AMS, hello seguenti:

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. Selezionare **Impostazioni** > **Protezione del contenuto**.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>criterio di autorizzazione per chiavi e licenze
AMS supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi o licenze. criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client affinché hello chiave licenza toobe toohello delived client. Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: **aprire** o **token** restrizione.

Hello portale di Azure consente toocreate uno **criteri di autorizzazione chiave licenza** per tutti i tipi di crittografia.

### <a name="open"></a>Apri
Restrizione Open significa che il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave. Questo tipo di limitazione può risultare utile ai fini dei test. 

### <a name="token"></a>token
criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza). Servizi multimediali supporta i token in formato JSON Web Token (JWT) e i token SWT (Simple Web token) hello. Servizi multimediali non fornisce servizi token di sicurezza. È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure. Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con hello specificato chiave e rilasciare le attestazioni specificate nella configurazione della restrizione token hello. attestazioni di servizi multimediali Hello servizio di distribuzione chiavi restituirà hello richiesto hello e chiave (o licenza) client toohello se hello token è valido in hello token corrispondono a quelle configurate per la chiave di hello (o licenza).

Quando si configurano i criteri con restrizione token hello, è necessario specificare la chiave di verifica primaria hello, autorità emittente e parametri pubblico. chiave di verifica primaria Hello contiene hello chiave che hello token è stato firmato con, autorità emittente è hello servizio token di sicurezza che rilascia token hello. destinatari Hello (talvolta denominato ambito) descrive finalità hello del token hello o hello risorse hello token autorizza l'accesso. Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Modello dei diritti PlayReady
Per informazioni dettagliate sul modello di diritti di hello PlayReady, vedere [Panoramica del modello di licenza PlayReady servizi multimediali](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Non persistente
Se si configura una licenza come non persistenti, è solo conservato in memoria mentre player hello utilizza licenza hello.  

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Persistente
Se si configura la licenza hello come permanente, esso viene salvato nell'archivio permanente in client hello.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Modello dei diritti Widevine
Per informazioni dettagliate sul modello di hello Widevine diritti, vedere [Cenni preliminari sui modelli di licenza Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Basic
Quando si seleziona **base**, hello modello verrà creato con tutti i valori predefiniti.

### <a name="advanced"></a>Avanzate
Per informazioni dettagliate sull'opzione avanzata delle configurazioni Widevine, vedere [questo](media-services-widevine-license-template-overview.md) argomento.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Configurazione di FairPlay
crittografia FairPlay tooenable, è necessario tooprovide hello App certificato e chiave privata dell'applicazione (chiedere) tramite l'opzione di configurazione FairPlay hello. Per informazioni dettagliate sulla configurazione e i requisiti di FairPlay, vedere [questo](media-services-protect-hls-with-fairplay.md) articolo.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Applicare asset tooyour crittografia dinamica
Il vantaggio di tootake di crittografia dinamica, è necessario tooencode il file di origine in un set di file MP4 a velocità in bit adattiva.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Selezionare una risorsa che si desidera tooencrypt
Selezionare tutte le attività, toosee **impostazioni** > **asset**.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Crittografare con AES o DRM
Quando si seleziona **Crittografa** per un asset, sono disponibili due opzioni: **AES** o **DRM**. 

#### <a name="aes"></a>AES
La crittografia con chiave non crittografata AES sarà abilitata su tutti i protocolli di streaming: Smooth Streaming, HLS e MPEG-DASH.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Quando si seleziona una scheda DRM hello, viene visualizzata con diverse opzioni di criteri di protezione del contenuto (che è necessario aver configurato a questo punto) + un set di protocolli di flusso.

* **PlayReady e Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine.
* **PlayReady e Widevine con MPEG-DASH + FairPlay con HLS** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine. Verranno anche crittografati i flussi HLS con FairPlay.
* **PlayReady solo con Smooth Streaming, HLS e MPEG-DASH** : i flussi Smooth Streaming, HLS e MPEG-DASH verranno crittografati dinamicamente con la soluzione DRM PlayReady.
* **Solo Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con la soluzione DRM Widevine.
* **Solo FairPlay con HLS** : il flusso HLS verrà crittografato dinamicamente con FairPlay.

crittografia FairPlay tooenable, è necessario tooprovide hello App certificato e chiave privata dell'applicazione (chiedere) tramite l'opzione di configurazione FairPlay del pannello delle impostazioni di protezione del contenuto hello hello.

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Una volta apportate selezione della crittografia hello, premere **applica**.

>[!NOTE] 
>Se si intende tooplay un AES crittografata HLS in Safari, vedere [questo blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

