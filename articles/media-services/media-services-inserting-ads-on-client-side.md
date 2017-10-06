---
title: annunci aaaInserting sul lato client hello | Documenti Microsoft
description: Questo argomento viene illustrato come tooinsert annunci sul hello lato client.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Inserimento di annunci sul lato client hello
In questo argomento contiene informazioni su come tooinsert diversi tipi di annunci sul lato client hello.

Per informazioni sul supporto di sottotitoli codificati e annunci nei video in streaming live, vedere, [Sottotitoli codificati supportati e standard per l'inserimento di annunci](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Azure Media Player attualmente non supporta gli annunci.
> 
> 

## <a id="insert_ads_into_media"></a>Inserimento di annunci nei file multimediali
Servizi multimediali di Azure fornisce il supporto per l'inserimento di annunci tramite hello Windows Media Platform: Player Framework. Player Framework con supporto per gli annunci sono disponibili per i dispositivi Windows 8, Silverlight, Windows Phone 8 e iOS. Ogni player framework contiene un codice di esempio che illustra come tooimplement un'applicazione Windows Media player. Esistono tre diversi tipi di annunci, che è possibile inserire nell'elenco dei supporti:.

* **Lineare** – completo annunci frame Pausa video principale hello.
* **Non lineari** : annunci sovrapposti visualizzati durante la riproduzione di video principale hello, in genere un logo o altra immagine statica posizionate all'interno di Windows Media player hello.
* **Complementare** : annunci visualizzati all'esterno di Windows Media player hello.

Gli annunci possono essere inseriti in qualsiasi punto della sequenza temporale del video principale hello. È necessario indicare quando tooplay hello Active Directory e che il lettore hello tooplay annunci. Questa operazione viene eseguita mediante una serie di file standard basati su XML: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) e Digital Video Player Ad Interface Definition (VPAID). I file VAST specificano quali toodisplay annunci. File VMAP specificano quando tooplay vari annunci e contengono XML VAST. I file MAST rappresentano un altro toosequence annunci di modo che possono contenere XML VAST. I file VPAID definiscono un'interfaccia tra lettore video hello e ad hello o un server Active Directory.

Ogni Player Framework ha un funzionamento diverso, che verrà illustrato in un argomento specifico. Questo argomento viene descritto hello meccanismi di base usati tooinsert annunci. Le applicazioni di lettore video richiedere annunci da un ad server. server di annunci Hello può rispondere in diversi modi:

* Restituzione di un file VAST
* Restituzione di un file VMAP (con VAST incorporato)
* Restituzione di un file MAST (con VAST incorporato)
* Restituzione di un file VAST con annunci VPAID

### <a name="using-a-video-ad-service-template-vast-file"></a>Uso di un file VAST (Video Ad Service Template)
Un file VAST specifica gli annunci toodisplay. Hello XML riportato di seguito è riportato un esempio di un file VAST per un annuncio lineare:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

annuncio lineare Hello è descritta da hello <**lineare**> elemento. Specifica la durata di hello di annuncio hello, tenere traccia degli eventi, fare clic, fare clic su rilevamento e un numero di **MediaFile** elementi. Gli eventi di rilevamento vengono specificati all'interno di hello <**TrackingEvents**> elemento e consentono un tootrack server Active Directory diversi eventi che si verificano durante la visualizzazione ad hello. In questo caso hello iniziali, intermedi, completato ed espandere gli eventi vengono registrati. evento di avvio Hello si verifica quando l'annuncio hello venga visualizzato. Hello punto medio evento si verifica almeno 50% della sequenza temporale dell'annuncio hello è stata visualizzata. evento completa Hello si verifica quando l'annuncio hello è stato eseguito toohello fine. evento di espansione Hello si verifica quando l'utente hello espande schermata toofull di lettore video hello. I clickthrough sono specificati con un <**click-through**> elemento all'interno di un <**VideoClicks**> elemento e specifica un toodisplay di risorsa URI tooa quando hello utente fa clic sull'annuncio hello. Monitoraggio viene specificato un <**monitoraggio**> elemento, anche all'interno di hello <**VideoClicks**> elemento e di specificare una risorsa di rilevamento per hello player toorequest quando hello utente fa clic su in ad.hello hello <**MediaFile**> elementi specificano le informazioni su una determinata codifica di un annuncio. Se è presente più di un <**MediaFile**> elemento, il lettore di hello può scegliere hello migliore codifica per la piattaforma hello. 

Gli annunci lineari possono essere visualizzati in un ordine specifico. toodo, aggiungere ulteriori <Ad> elementi toohello VAST file e specificare l'ordine di hello utilizzando l'attributo di sequenza hello. Questa condizione è illustrata Hello di esempio seguente:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Anche gli annunci non lineari vengono specificati in un elemento <Creative>. Hello seguente esempio viene illustrato un <Creative> elemento che descrive un annuncio non lineare.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Hello <**NonLinearAds**> elemento può contenere uno o più <**non lineari**> elementi, ognuno dei quali può descrivere un annuncio non lineare. Hello <**non lineari**> elemento specifica hello risorsa per l'annuncio non lineare hello. Hello risorsa può essere una <**StaticResouce**>, <**IFrameResource**>, o una <**HTMLResouce**>. <**StaticResource**> descrive una risorsa non HTML e definisce un attributo creativeType che specifica la modalità di visualizzazione risorse hello:

Image/gif, image/jpeg, image/png: hello risorsa è visualizzata in un elemento HTML <**img**> tag.

Application/x-javascript: risorse hello viene visualizzato in un elemento HTML <**script**> tag.

Application/x-shockwave-flash: la risorsa hello viene visualizzato in un lettore Flash.

**IFrameResource** descrive una risorsa HTML che può essere visualizzata in un IFrame. **HTMLResource** descrive una parte di codice HTML che può essere inserita in una pagina Web. **TrackingEvents** specificare gli eventi di rilevamento e hello toorequest URI quando si verifica l'evento hello. In hello in questo esempio vengono registrati eventi acceptInvitation e collapse. Per ulteriori informazioni su hello **NonLinearAds** elemento e i relativi elementi figlio, vedere IAB.NET/VAST. Si noti che hello **TrackingEvents** elemento si trova all'interno di hello **NonLinearAds** elemento anziché hello **non lineari** elemento.

Gli annunci complementari vengono definiti entro un elemento <CompanionAds>. Hello <CompanionAds> elemento può contenere uno o più <Companion> elementi. Ogni <Companion> elemento descrive un annuncio complementare e può contenere un <StaticResource>, <IFrameResource>, o <HTMLResource> , specificata in hello stesso modo in un annuncio non lineare. Un file VAST può contenere più annunci complementari e hello lettore può scegliere hello toodisplay di Active Directory più appropriato. Per altre informazioni su VAST, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Uso di un file VMAP (Video Multiple Ad Playlist) digitale
Un file VMAP permette di toospecify quando si verificano interruzioni pubblicitarie, quanto tempo ogni interruzione è, quanti annunci possono essere visualizzati all'interno di un'interruzione e i tipi di annunci possono essere visualizzati durante un'interruzione. Hello seguente in un esempio di file VMAP che definisce una singola interruzione pubblicitaria:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Un file VMAP inizia con un elemento <VMAP> che include uno o più elementi <AdBreak>, ognuno dei quali definisce un'interruzione pubblicitaria. Ogni interruzione pubblicitaria specifica un tipo di interruzione, un ID di interruzione e un offset temporale. attributo di Hello breakType specifica il tipo di hello di Active Directory che può essere riprodotto durante l'interruzione di hello: lineare, non lineare o la visualizzazione. Gli annunci di visualizzazione mappa annunci complementari tooVAST. È possibile specificare più tipi di annuncio in un elenco separato da virgole (senza spazi). Hello breakID è un identificatore facoltativo per annunci hello. Hello timeOffset specifica quando deve essere visualizzato ad hello. Può essere specificato in uno dei seguenti modi hello:

1. Tempo: con formato hh:mm:ss o hh:mm:ss.mmm, dove .mmm corrisponde a millisecondi. il valore di Hello di questo attributo specifica il tempo di hello dall'inizio di hello dell'inizio di toohello hello video della sequenza temporale di interruzione pubblicitaria hello.
2. Percentuale: con formato n % dove n è la percentuale hello di hello sequenza temporale video tooplay prima di riprodurre l'annuncio hello
3. Inizio/fine: Specifica che un annuncio deve essere visualizzato prima o dopo la visualizzazione del video hello
4. Posizione: specifica l'ordine di hello delle interruzioni pubblicitarie quando l'intervallo di hello delle interruzioni pubblicitarie hello è sconosciuto, come lo streaming live. ordine di Hello di ogni interruzione è specificato nel formato hello #n dove n è un numero intero maggiore o uguale a 1. 1 indica l'annuncio hello deve essere riprodotto alla prima opportunità hello, 2 indica ad hello deve essere riprodotto alla seconda opportunità hello e così via.

All'interno di hello <**AdBreak**> non esiste l'elemento può essere una <**AdSource**> elemento. Hello <**AdSource**> elemento contiene hello gli attributi seguenti:

1. ID: specifica un identificatore per l'origine dell'annuncio hello
2. allowMultipleAds: valore booleano che specifica se è possono visualizzare più annunci durante l'interruzione pubblicitaria hello
3. followRedirects: valore booleano facoltativo che specifica se il lettore di hello deve rispettare i reindirizzamenti in una risposta annuncio

Hello <**AdSource**> elemento fornisce player hello una risposta annuncio inline o una risposta annuncio tooan di riferimento. Può contenere uno dei seguenti elementi hello:

* <VASTAdData>indica che una risposta annuncio VAST è incorporata nel file VMAP hello
* <AdTagURI>: un URI che fa riferimento a una risposta annuncio da un altro sistema.
* <CustomAdData>: -una stringa arbitraria che rappresenta una risposta non VAST.

In questo esempio una risposta annuncio inline è specificata con un elemento <VASTAdData> che contiene una risposta annuncio VAST. Per ulteriori informazioni su hello ad altri elementi, vedere [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Hello <**AdBreak**> può anche contenere un elemento <**TrackingEvents**> elemento. Hello <**TrackingEvents**> elemento consente di tootrack hello inizio o fine di un'interruzione pubblicitaria o se si è verificato un errore durante l'interruzione pubblicitaria hello. Hello <**TrackingEvents**> elemento contiene uno o più <**rilevamento**> elementi, ognuno dei quali specifica un evento di rilevamento e un URI di rilevamento. eventi di rilevamento possibili Hello sono:

1. breakStart: rileva inizio hello di un'interruzione pubblicitaria
2. breakEnd: rileva hello completamento di un'interruzione pubblicitaria
3. Error: rileva un errore che si è verificato durante l'interruzione pubblicitaria hello

Hello di esempio seguente viene illustrato un file VMAP che specifica gli eventi di rilevamento

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Per ulteriori informazioni su hello <**TrackingEvents**> elemento e i relativi elementi figlio, vedere http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Uso di un file MAST (Media Abstract Sequencing Template)
Un file MAST permette toospecify trigger che definiscono quando è visualizzato un annuncio. di seguito Hello è un file MAST di esempio che contiene i trigger per un annuncio precedente, un annuncio midroll e postroll.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



Un file MAST inizia con un elemento **MAST** che contiene un elemento **triggers**. Hello <triggers> elemento contiene uno o più **trigger** gli elementi che definiscono quando deve essere riprodotto un annuncio. 

Hello **trigger** elemento contiene un **startConditions** elemento che specificano quando un annuncio deve iniziare tooplay. Hello **startConditions** elemento contiene uno o più <condition> elementi. Quando ogni <condition> valuta tootrue un trigger è avviato o revocato varia a seconda se hello <condition> è contenuto all'interno di un **startConditions** o **endConditions** elemento rispettivamente. Quando più <condition> gli elementi sono presenti, vengono considerate come OR implicito, qualsiasi condizione di valutazione tootrue genererà tooinitiate trigger hello. Gli elementi <condition> possono essere annidati. Quando figlio <condition> elementi sono stati definiti, vengono considerate come and implicito e tutte le condizioni devono restituire tootrue per tooinitiate trigger hello. Hello <condition> elemento contiene hello gli attributi che definiscono la condizione hello seguenti: 

1. **tipo** : Specifica il tipo di hello di condizione, eventi o proprietà
2. **nome** : hello nome di hello toobe proprietà o evento utilizzato durante la valutazione
3. **valore** : hello valore che verrà valutata rispetto a una proprietà
4. **operatore** : hello toouse operazione durante la valutazione: EQ (uguale), NEQ (diverso da), GTR (maggiore), GEQ (maggiore o uguale a), LT (minore di), LEQ (minore o uguale a), MOD (modulo)

**endConditions** contengono anche elementi <condition>. Quando si valuta una condizione di trigger hello tootrue è reset.hello <trigger> elemento contiene inoltre un <sources> elemento che contiene uno o più <source> elementi. Hello <source> gli elementi definiscono hello URI toohello ad risposta e il tipo di hello della risposta annuncio. In questo esempio non viene specificato un URI risposta VAST tooa. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Uso di VPAID (Video Player-Ad Interface Definition)
VPAID è un'API per l'abilitazione di toocommunicate unità annuncio eseguibile con un lettore video. Ciò offre esperienze altamente interattive per gli annunci. Hello utente può interagire con annunci hello e ad hello può rispondere tooactions eseguita dal Visualizzatore hello. Ad esempio un annuncio può mostrare pulsanti che consentono di hello utente tooview ulteriori informazioni o una versione più lunga dell'annuncio hello. lettore video Hello deve supportare hello API VPAID e annuncio eseguibile hello deve implementare hello API. Quando un lettore richiede un annuncio da un server di hello ad server può rispondere con una risposta VAST contenente un annuncio vpaid.

Un annuncio eseguibile è creato in codice che deve essere eseguito in un ambiente di runtime, ad esempio Adobe Flash™ o JavaScript eseguibile in un Web browser. Quando un ad server restituisce una risposta VAST contenente un annuncio vpaid, hello valore dell'attributo apiFramework hello in hello <MediaFile> elemento deve essere "VPAID". Questo attributo specifica quell'annuncio hello contenuto un annuncio eseguibile vpaid. Hello tipo attributo deve essere impostato il tipo MIME toohello di hello eseguibile, ad esempio "application/x-shockwave-flash" o "application/x-javascript". frammento XML seguente Hello Mostra hello <MediaFile> elemento da una risposta VAST contenente un annuncio eseguibile vpaid. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Un annuncio eseguibile può essere inizializzato utilizzando hello <AdParameters> elemento all'interno di hello <Linear> o <NonLinear> elementi in una risposta VAST. Per ulteriori informazioni su hello <AdParameters> elemento, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Per ulteriori informazioni su hello API VPAID, vedere [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Implementazione di un lettore Windows o Windows Phone 8 con supporto per gli annunci
Hello Microsoft Media Platform: Player Framework per Windows 8 e Windows Phone 8 contiene una raccolta di applicazioni di esempio che illustrano come un'applicazione di lettore video con tooimplement hello framework. È possibile scaricare esempi di Windows Media Player Framework e hello hello da [Player Framework per Windows 8 e Windows Phone 8](https://playerframework.codeplex.com).

Quando si apre hello playerframework soluzione verrà visualizzato un numero di cartelle nel progetto hello. cartella Advertising Hello contiene hello esempio codice pertinente toocreating un lettore video con supporto di Active Directory. Cartella di annunci hello interno è un numero di XAML/cs file ognuno dei quali Mostra come tooinsert annunci in modo diverso. Hello seguente elenco descrive ogni:

* AdPodPage.xaml viene illustrato come toodisplay Active Directory contenitore.
* Mostra AdSchedulingPage.xaml come tooschedule annunci.
* FreeWheelPage.xaml viene illustrato come toouse hello annunci tooschedule di plug-in FreeWheel.
* Mostra MastPage.xaml come tooschedule annunci con un file MAST.
* Programmaticadpage viene illustrato come pianificare annunci di tooprogrammatically in un video.
* Mostra ScheduleClipPage.xaml come tooschedule un annuncio senza un file VAST.
* Mostra VastLinearCompanionPage.xaml come tooinsert lineari e annunci complementari.
* Mostra VastNonLinearPage.xaml come tooinsert un annuncio non lineare.
* Mostra VmapPage.xaml come toospecify annunci con un file VMAP.

Ognuno di questi esempi Usa classe MediaPlayer hello definite da hello player framework. Nella maggior parte degli esempi vengono usati plug-in che aggiungono supporto per vari formati di risposta annuncio. Hello-esempio ProgrammaticAdPage interagisce a livello di codice con un'istanza di MediaPlayer.

### <a name="adpodpage-sample"></a>Esempio AdPodPage
In questo esempio utilizza hello AdSchedulerPlugin toodefine quando toodisplay Active Directory. In questo esempio un annuncio midroll è pianificato toobe riprodotto dopo 5 secondi. podcast annuncio Hello (un gruppo di annunci toodisplay in ordine) viene specificato in un file VAST restituito da un ad server. file VAST toohello di Hello URI specificato nel hello <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Per ulteriori informazioni su hello AdSchedulerPlugin, vedere [pubblicità hello Player Framework su Windows 8 e Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
In questo esempio Usa anche hello AdSchedulerPlugin. Vengono pianificati tre annunci, un annuncio preroll, un annuncio midroll e un annuncio postroll. Hello URI toohello VAST per ogni annuncio è specificato un <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
Questo esempio utilizza hello FreeWheelPlugin che specifica un attributo di origine che specifica un URI file SmartXML tooa punti che specifica il contenuto di Active Directory, nonché informazioni sulla pianificazione di Active Directory.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Questo esempio utilizza hello MastSchedulerPlugin che consente a un file MAST toouse. attributo di origine Hello specifica il percorso di hello del file MAST hello.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
In questo esempio interagisce a livello di codice con hello Media Player. file Programmaticadpage Hello crea un'istanza di MediaPlayer hello:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

file ProgrammaticAdPage.xaml.cs Hello crea un AdHandlerPlugin, aggiunge un toospecify TimelineMarker quando un annuncio deve essere visualizzato e quindi aggiunge un gestore per l'evento MarkerReached hello che carica un RemoteAdSource specificando un file VAST tooa URI e quindi viene riprodotto annuncio Hello.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
Questo esempio utilizza hello AdSchedulerPlugin tooschedule un annuncio midroll specificando un file con estensione wmv contenente ad hello.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
In questo esempio viene illustrato come toouse hello AdSchedulerPlugin tooschedule un annuncio lineare midroll con un annuncio complementare. Hello <RemoteAdSource> elemento specifica il percorso di hello del file VAST hello.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Questo esempio utilizza hello AdSchedulerPlugin tooschedule lineare e un annuncio non lineare. Hello percorso del file VAST è specificato con hello <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
In questo esempio utilizza hello VmapSchedulerPlugin tooschedule gli annunci tramite un file VMAP. file VMAP toohello di Hello URI specificato nell'attributo di origine hello di hello <VmapSchedulerPlugin> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Implementazione di un lettore video iOS con supporto per gli annunci
Hello Microsoft Media Platform: Player Framework per iOS contiene una raccolta di applicazioni di esempio che illustrano come un'applicazione di lettore video con tooimplement hello framework. È possibile scaricare esempi di Windows Media Player Framework e hello hello da [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). pagina di github Hello è tooa un collegamento Wiki che contiene informazioni aggiuntive sulla hello player framework e un esempio di lettore toohello Introduzione: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Pianificazione di annunci con VMAP
Hello seguente esempio viene illustrato come gli annunci di tooschedule tramite un file VMAP.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>Pianificazione di annunci con VAST
Hello esempio riportato di seguito viene illustrato come tooschedule un annuncio VAST di associazione tardiva.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   Hello esempio riportato di seguito viene illustrato come tooschedule un annuncio VAST di associazione anticipata.
Esempio 4: pianificazione un hello VAST //Download annuncio VAST anticipata di associazione file se (! [ framework.adResolver downloadManifest: & manifesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[logFrameworkError self];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

Hello esempio riportato di seguito viene illustrato come tooinsert Active Directory utilizzando approssimativa Taglia modifica (ZARE)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Hello esempio seguente viene illustrato come tooschedule Active Directory contenitore.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello seguente esempio viene illustrato come tooschedule un annuncio midroll non permanenti. Un annuncio non nota adesiva viene riprodotto solo una volta indipendentemente dalle eventuali hello ricerca esegue il visualizzatore.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello seguente esempio viene illustrato come tooschedule un annuncio midroll permanente. Verrà visualizzata una nota adesiva ad ogni volta hello specificato viene raggiunto il punto nella sequenza temporale video hello.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


Hello esempio riportato di seguito viene illustrato come tooschedule postroll.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello esempio riportato di seguito viene illustrato come un annuncio preroll tooschedule.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello seguente esempio mostra come tooschedule un midroll sovrapposizione Active Directory.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Sviluppo di applicazioni di lettore video](media-services-develop-video-players.md)

