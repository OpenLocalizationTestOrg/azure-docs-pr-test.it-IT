---
title: prestazioni aaaImprove compressione dei file nella rete CDN di Azure | Documenti Microsoft
description: "Informazioni su come file tooimprove trasferire velocità e aumentare le prestazioni di caricamento pagina per la compressione dei file nella rete CDN di Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure
La compressione è la velocità di trasferimento file un metodo semplice ed efficace tooimprove e aumento delle prestazioni di caricamento pagina grazie alla riduzione delle dimensioni del file prima di esso viene inviato dal server hello. Riduce i costi della larghezza di banda e offre un'esperienza più reattiva per gli utenti.

Esistono due modi tooenable compressione:

* È possibile abilitare la compressione sul server di origine, nel qual caso hello CDN passaggi hello file compressi e recapitare tooclients file compressi che ne fanno richiesta.
* È possibile abilitare la compressione direttamente su un server di edge CDN, in cui hello case CDN comprime, hello file ed esse forniscono agli utenti di tooend, anche se essi non vengono compressi dal server di origine hello.

> [!IMPORTANT]
> Modifiche alla configurazione di rete CDN vengono alcuni toopropagate ora tramite rete hello.  La propagazione dei profili della <b>Rete CDN di Azure fornita da Akamai</b> in genere dura meno di un minuto.  La propagazione dei profili della <b>Rete CDN di Azure fornita da Verizon</b> , in genere le modifiche vengono applicate entro 90 minuti.  Se si tratta di hello prima di che aver configurato la compressione per l'endpoint CDN, è necessario considerare in attesa che le impostazioni di compressione hello siano propagate POP toohello prima della risoluzione dei problemi di toobe 1-2 ore
> 
> 

## <a name="enabling-compression"></a>Abilitare la compressione
> [!NOTE]
> forniscono Hello livelli Standard e Premium CDN hello stessa funzionalità di compressione, ma hello interfaccia utente diversa.  Per ulteriori informazioni sulle differenze di hello tra i livelli Standard e Premium CDN, vedere [Panoramica della rete CDN di Azure](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Livello Standard
> [!NOTE]
> Questa sezione si applica troppo**Azure CDN Standard da Verizon** e **Azure CDN Standard da Akamai** profili.
> 
> 

1. Dalla pagina del profilo CDN hello, fare clic su endpoint rete CDN hello desiderato toomanage.
   
    ![Endpoint della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    verrà visualizzata la pagina endpoint rete CDN di Hello.
2. Fare clic su hello **configura** pulsante.
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    verrà visualizzata la pagina di configurazione della rete CDN Hello.
3. Attivare **compressione**.
   
    ![Opzioni di compressione della rete CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. Utilizzare i tipi predefiniti hello o modificare l'elenco di hello mediante la rimozione o aggiunta di tipi di file.
   
   > [!TIP]
   > Mentre è possibile, si consiglia di formati di toocompressed compressione tooapply, ad esempio ZIP, MP3, MP4, JPG e così via.
   > 
   > 
5. Dopo aver apportato le modifiche, fare clic su hello **salvare** pulsante.

### <a name="premium-tier"></a>Livello Premium
> [!NOTE]
> Questa sezione si applica troppo**Premium rete CDN di Azure da Verizon** profili.
> 
> 

1. Dalla pagina del profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.  Fare clic su **Compressione**.

    ![Selezione della compressione file](./media/cdn-file-compression/cdn-compress-select.png)
   
    Vengono visualizzate le opzioni di compressione.
   
    ![Compressione dei file](./media/cdn-file-compression/cdn-compress-files.png)
3. Abilitare la compressione facendo hello **è abilitata la compressione** pulsante di opzione.  Immettere i tipi MIME hello desiderato toocompress come un elenco delimitato da virgole (senza spazi) in hello **tipi di File** casella di testo.
   
   > [!TIP]
   > Mentre è possibile, si consiglia di formati di toocompressed compressione tooapply, ad esempio ZIP, MP3, MP4, JPG e così via. 
   > 
   > 
4. Dopo aver apportato le modifiche, fare clic su hello **aggiornamento** pulsante.

## <a name="compression-rules"></a>Regole di compressione
Le tabelle seguenti descrivono il comportamento della compressione della rete CDN di Azure per ogni scenario.

> [!IMPORTANT]
> Per la **Rete CDN di Azure fornita da Verizon** (Standard e Premium) vengono compressi soltanto i file idonei.  toobe idonee per la compressione, un file necessario:
> 
> * Maggiore di 128 byte.
> * Minore di 1 MB.
> 
> Per la **Rete CDN di Azure fornita da Akamai**, tutti i file sono idonei per la compressione.
> 
> Per tutti i prodotti della rete CDN di Azure, il file deve essere un file di tipo MIME [configurato per la compressione](#enabling-compression).
> 
> I profili della **rete CDN di Azure fornita da Verizon** (Standard e Premium) supportano la codifica **gzip** (zip GNU), **deflate**, **bzip2** o **br** (Brotli). Per la codifica Brotli, la compressione di hello viene eseguita solo nel bordo hello. Hello client/browser deve inviare una richiesta hello per la codifica Brotli e asset compresso hello deve sono stati compressi sul lato di origine hello prima. 
>
>I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.
> 
> **Rete CDN di Azure da Akamai** endpoint sempre richiesta **gzip** con codifica di file di origine di hello, indipendentemente dalla richiesta di hello del client. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Compressione disabilitata o file non idoneo per la compressione
| Formato richiesto del client tramite l'intestazione Accept-Encoding | Formato del file memorizzato nella cache | Client toohello di risposta della rete CDN | Note |
| --- | --- | --- | --- |
| Compresso |Compresso |Compresso | |
| Compresso |Non compresso |Non compresso | |
| Compresso |Non memorizzato nella cache |Compressa o non compressa |A seconda della risposta dell'origine |
| Non compresso |Compresso |Non compresso | |
| Non compresso |Non compresso |Non compresso | |
| Non compresso |Non memorizzato nella cache |Non compresso | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Compressione abilitata e file idoneo per la compressione
| Formato richiesto del client tramite l'intestazione Accept-Encoding | Formato del file memorizzato nella cache | Client toohello di risposta della rete CDN | Note |
| --- | --- | --- | --- |
| Compresso |Compresso |Compresso |Transcodifica della rete CDN tra formati supportati |
| Compresso |Non compresso |Compresso |Compressione da parte della rete CDN |
| Compresso |Non memorizzato nella cache |Compresso |La rete CDN esegue la compressione se l'origine restituisce Non compresso.  **Rete CDN di Azure da Verizon** passa hello file non compresso della prima richiesta hello e quindi comprime e memorizza nella cache di hello file per le richieste successive.  I file con l'intestazione `Cache-Control: no-cache` non verranno mai compressi. |
| Non compresso |Compresso |Non compresso |Decompressione da parte della rete CDN |
| Non compresso |Non compresso |Non compresso | |
| Non compresso |Non memorizzato nella cache |Non compresso | |

## <a name="media-services-cdn-compression"></a>Compressione della rete CDN dei servizi multimediali
Per gli endpoint di streaming abilitata la rete CDN di servizi multimediali, la compressione è abilitata per impostazione predefinita per i seguenti tipi di contenuto hello: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, applicazione/f4m + xml. È possibile abilitare/disabilitare la compressione per hello indicato tipi utilizzando hello portale di Azure.  

## <a name="see-also"></a>Vedere anche
* [Risoluzione dei problemi della compressione dei file CDN](cdn-troubleshoot-compression.md)    

