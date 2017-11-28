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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="dbc14-103">Inserimento di annunci sul lato client hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="dbc14-104">In questo argomento contiene informazioni su come tooinsert diversi tipi di annunci sul lato client hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="dbc14-105">Per informazioni sul supporto di sottotitoli codificati e annunci nei video in streaming live, vedere, [Sottotitoli codificati supportati e standard per l'inserimento di annunci](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="dbc14-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="dbc14-106">Azure Media Player attualmente non supporta gli annunci.</span><span class="sxs-lookup"><span data-stu-id="dbc14-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="dbc14-107"><a id="insert_ads_into_media"></a>Inserimento di annunci nei file multimediali</span><span class="sxs-lookup"><span data-stu-id="dbc14-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="dbc14-108">Servizi multimediali di Azure fornisce il supporto per l'inserimento di annunci tramite hello Windows Media Platform: Player Framework.</span><span class="sxs-lookup"><span data-stu-id="dbc14-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="dbc14-109">Player Framework con supporto per gli annunci sono disponibili per i dispositivi Windows 8, Silverlight, Windows Phone 8 e iOS.</span><span class="sxs-lookup"><span data-stu-id="dbc14-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="dbc14-110">Ogni player framework contiene un codice di esempio che illustra come tooimplement un'applicazione Windows Media player. Esistono tre diversi tipi di annunci, che è possibile inserire nell'elenco dei supporti:.</span><span class="sxs-lookup"><span data-stu-id="dbc14-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="dbc14-111">**Lineare** – completo annunci frame Pausa video principale hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="dbc14-112">**Non lineari** : annunci sovrapposti visualizzati durante la riproduzione di video principale hello, in genere un logo o altra immagine statica posizionate all'interno di Windows Media player hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="dbc14-113">**Complementare** : annunci visualizzati all'esterno di Windows Media player hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="dbc14-114">Gli annunci possono essere inseriti in qualsiasi punto della sequenza temporale del video principale hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="dbc14-115">È necessario indicare quando tooplay hello Active Directory e che il lettore hello tooplay annunci.</span><span class="sxs-lookup"><span data-stu-id="dbc14-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="dbc14-116">Questa operazione viene eseguita mediante una serie di file standard basati su XML: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) e Digital Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="dbc14-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="dbc14-117">I file VAST specificano quali toodisplay annunci.</span><span class="sxs-lookup"><span data-stu-id="dbc14-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="dbc14-118">File VMAP specificano quando tooplay vari annunci e contengono XML VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="dbc14-119">I file MAST rappresentano un altro toosequence annunci di modo che possono contenere XML VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="dbc14-120">I file VPAID definiscono un'interfaccia tra lettore video hello e ad hello o un server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbc14-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="dbc14-121">Ogni Player Framework ha un funzionamento diverso, che verrà illustrato in un argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="dbc14-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="dbc14-122">Questo argomento viene descritto hello meccanismi di base usati tooinsert annunci. Le applicazioni di lettore video richiedere annunci da un ad server.</span><span class="sxs-lookup"><span data-stu-id="dbc14-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="dbc14-123">server di annunci Hello può rispondere in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="dbc14-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="dbc14-124">Restituzione di un file VAST</span><span class="sxs-lookup"><span data-stu-id="dbc14-124">Return a VAST file</span></span>
* <span data-ttu-id="dbc14-125">Restituzione di un file VMAP (con VAST incorporato)</span><span class="sxs-lookup"><span data-stu-id="dbc14-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="dbc14-126">Restituzione di un file MAST (con VAST incorporato)</span><span class="sxs-lookup"><span data-stu-id="dbc14-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="dbc14-127">Restituzione di un file VAST con annunci VPAID</span><span class="sxs-lookup"><span data-stu-id="dbc14-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="dbc14-128">Uso di un file VAST (Video Ad Service Template)</span><span class="sxs-lookup"><span data-stu-id="dbc14-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="dbc14-129">Un file VAST specifica gli annunci toodisplay.</span><span class="sxs-lookup"><span data-stu-id="dbc14-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="dbc14-130">Hello XML riportato di seguito è riportato un esempio di un file VAST per un annuncio lineare:</span><span class="sxs-lookup"><span data-stu-id="dbc14-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="dbc14-131">annuncio lineare Hello è descritta da hello <**lineare**> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="dbc14-132">Specifica la durata di hello di annuncio hello, tenere traccia degli eventi, fare clic, fare clic su rilevamento e un numero di **MediaFile** elementi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="dbc14-133">Gli eventi di rilevamento vengono specificati all'interno di hello <**TrackingEvents**> elemento e consentono un tootrack server Active Directory diversi eventi che si verificano durante la visualizzazione ad hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="dbc14-134">In questo caso hello iniziali, intermedi, completato ed espandere gli eventi vengono registrati.</span><span class="sxs-lookup"><span data-stu-id="dbc14-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="dbc14-135">evento di avvio Hello si verifica quando l'annuncio hello venga visualizzato.</span><span class="sxs-lookup"><span data-stu-id="dbc14-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="dbc14-136">Hello punto medio evento si verifica almeno 50% della sequenza temporale dell'annuncio hello è stata visualizzata.</span><span class="sxs-lookup"><span data-stu-id="dbc14-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="dbc14-137">evento completa Hello si verifica quando l'annuncio hello è stato eseguito toohello fine.</span><span class="sxs-lookup"><span data-stu-id="dbc14-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="dbc14-138">evento di espansione Hello si verifica quando l'utente hello espande schermata toofull di lettore video hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="dbc14-139">I clickthrough sono specificati con un <**click-through**> elemento all'interno di un <**VideoClicks**> elemento e specifica un toodisplay di risorsa URI tooa quando hello utente fa clic sull'annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="dbc14-140">Monitoraggio viene specificato un <**monitoraggio**> elemento, anche all'interno di hello <**VideoClicks**> elemento e di specificare una risorsa di rilevamento per hello player toorequest quando hello utente fa clic su in ad.hello hello <**MediaFile**> elementi specificano le informazioni su una determinata codifica di un annuncio.</span><span class="sxs-lookup"><span data-stu-id="dbc14-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="dbc14-141">Se è presente più di un <**MediaFile**> elemento, il lettore di hello può scegliere hello migliore codifica per la piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="dbc14-142">Gli annunci lineari possono essere visualizzati in un ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="dbc14-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="dbc14-143">toodo, aggiungere ulteriori <Ad> elementi toohello VAST file e specificare l'ordine di hello utilizzando l'attributo di sequenza hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="dbc14-144">Questa condizione è illustrata Hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dbc14-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="dbc14-145">Anche gli annunci non lineari vengono specificati in un elemento <Creative>.</span><span class="sxs-lookup"><span data-stu-id="dbc14-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="dbc14-146">Hello seguente esempio viene illustrato un <Creative> elemento che descrive un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="dbc14-147">Hello <**NonLinearAds**> elemento può contenere uno o più <**non lineari**> elementi, ognuno dei quali può descrivere un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="dbc14-148">Hello <**non lineari**> elemento specifica hello risorsa per l'annuncio non lineare hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="dbc14-149">Hello risorsa può essere una <**StaticResouce**>, <**IFrameResource**>, o una <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="dbc14-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="dbc14-150"> <**StaticResource**> descrive una risorsa non HTML e definisce un attributo creativeType che specifica la modalità di visualizzazione risorse hello:</span><span class="sxs-lookup"><span data-stu-id="dbc14-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="dbc14-151">Image/gif, image/jpeg, image/png: hello risorsa è visualizzata in un elemento HTML <**img**> tag.</span><span class="sxs-lookup"><span data-stu-id="dbc14-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="dbc14-152">Application/x-javascript: risorse hello viene visualizzato in un elemento HTML <**script**> tag.</span><span class="sxs-lookup"><span data-stu-id="dbc14-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="dbc14-153">Application/x-shockwave-flash: la risorsa hello viene visualizzato in un lettore Flash.</span><span class="sxs-lookup"><span data-stu-id="dbc14-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="dbc14-154">**IFrameResource** descrive una risorsa HTML che può essere visualizzata in un IFrame.</span><span class="sxs-lookup"><span data-stu-id="dbc14-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="dbc14-155">**HTMLResource** descrive una parte di codice HTML che può essere inserita in una pagina Web.</span><span class="sxs-lookup"><span data-stu-id="dbc14-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="dbc14-156">**TrackingEvents** specificare gli eventi di rilevamento e hello toorequest URI quando si verifica l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="dbc14-157">In hello in questo esempio vengono registrati eventi acceptInvitation e collapse.</span><span class="sxs-lookup"><span data-stu-id="dbc14-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="dbc14-158">Per ulteriori informazioni su hello **NonLinearAds** elemento e i relativi elementi figlio, vedere IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="dbc14-159">Si noti che hello **TrackingEvents** elemento si trova all'interno di hello **NonLinearAds** elemento anziché hello **non lineari** elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="dbc14-160">Gli annunci complementari vengono definiti entro un elemento <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="dbc14-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="dbc14-161">Hello <CompanionAds> elemento può contenere uno o più <Companion> elementi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="dbc14-162">Ogni <Companion> elemento descrive un annuncio complementare e può contenere un <StaticResource>, <IFrameResource>, o <HTMLResource> , specificata in hello stesso modo in un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="dbc14-163">Un file VAST può contenere più annunci complementari e hello lettore può scegliere hello toodisplay di Active Directory più appropriato.</span><span class="sxs-lookup"><span data-stu-id="dbc14-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="dbc14-164">Per altre informazioni su VAST, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="dbc14-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="dbc14-165">Uso di un file VMAP (Video Multiple Ad Playlist) digitale</span><span class="sxs-lookup"><span data-stu-id="dbc14-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="dbc14-166">Un file VMAP permette di toospecify quando si verificano interruzioni pubblicitarie, quanto tempo ogni interruzione è, quanti annunci possono essere visualizzati all'interno di un'interruzione e i tipi di annunci possono essere visualizzati durante un'interruzione.</span><span class="sxs-lookup"><span data-stu-id="dbc14-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="dbc14-167">Hello seguente in un esempio di file VMAP che definisce una singola interruzione pubblicitaria:</span><span class="sxs-lookup"><span data-stu-id="dbc14-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="dbc14-168">Un file VMAP inizia con un elemento <VMAP> che include uno o più elementi <AdBreak>, ognuno dei quali definisce un'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="dbc14-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="dbc14-169">Ogni interruzione pubblicitaria specifica un tipo di interruzione, un ID di interruzione e un offset temporale.</span><span class="sxs-lookup"><span data-stu-id="dbc14-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="dbc14-170">attributo di Hello breakType specifica il tipo di hello di Active Directory che può essere riprodotto durante l'interruzione di hello: lineare, non lineare o la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="dbc14-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="dbc14-171">Gli annunci di visualizzazione mappa annunci complementari tooVAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="dbc14-172">È possibile specificare più tipi di annuncio in un elenco separato da virgole (senza spazi).</span><span class="sxs-lookup"><span data-stu-id="dbc14-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="dbc14-173">Hello breakID è un identificatore facoltativo per annunci hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="dbc14-174">Hello timeOffset specifica quando deve essere visualizzato ad hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="dbc14-175">Può essere specificato in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="dbc14-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="dbc14-176">Tempo: con formato hh:mm:ss o hh:mm:ss.mmm, dove .mmm corrisponde a millisecondi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="dbc14-177">il valore di Hello di questo attributo specifica il tempo di hello dall'inizio di hello dell'inizio di toohello hello video della sequenza temporale di interruzione pubblicitaria hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="dbc14-178">Percentuale: con formato n % dove n è la percentuale hello di hello sequenza temporale video tooplay prima di riprodurre l'annuncio hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="dbc14-179">Inizio/fine: Specifica che un annuncio deve essere visualizzato prima o dopo la visualizzazione del video hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="dbc14-180">Posizione: specifica l'ordine di hello delle interruzioni pubblicitarie quando l'intervallo di hello delle interruzioni pubblicitarie hello è sconosciuto, come lo streaming live.</span><span class="sxs-lookup"><span data-stu-id="dbc14-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="dbc14-181">ordine di Hello di ogni interruzione è specificato nel formato hello #n dove n è un numero intero maggiore o uguale a 1.</span><span class="sxs-lookup"><span data-stu-id="dbc14-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="dbc14-182">1 indica l'annuncio hello deve essere riprodotto alla prima opportunità hello, 2 indica ad hello deve essere riprodotto alla seconda opportunità hello e così via.</span><span class="sxs-lookup"><span data-stu-id="dbc14-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="dbc14-183">All'interno di hello <**AdBreak**> non esiste l'elemento può essere una <**AdSource**> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="dbc14-184">Hello <**AdSource**> elemento contiene hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbc14-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="dbc14-185">ID: specifica un identificatore per l'origine dell'annuncio hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="dbc14-186">allowMultipleAds: valore booleano che specifica se è possono visualizzare più annunci durante l'interruzione pubblicitaria hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="dbc14-187">followRedirects: valore booleano facoltativo che specifica se il lettore di hello deve rispettare i reindirizzamenti in una risposta annuncio</span><span class="sxs-lookup"><span data-stu-id="dbc14-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="dbc14-188">Hello <**AdSource**> elemento fornisce player hello una risposta annuncio inline o una risposta annuncio tooan di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="dbc14-189">Può contenere uno dei seguenti elementi hello:</span><span class="sxs-lookup"><span data-stu-id="dbc14-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="dbc14-190"><VASTAdData>indica che una risposta annuncio VAST è incorporata nel file VMAP hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="dbc14-191"><AdTagURI>: un URI che fa riferimento a una risposta annuncio da un altro sistema.</span><span class="sxs-lookup"><span data-stu-id="dbc14-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="dbc14-192"><CustomAdData>: -una stringa arbitraria che rappresenta una risposta non VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="dbc14-193">In questo esempio una risposta annuncio inline è specificata con un elemento <VASTAdData> che contiene una risposta annuncio VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="dbc14-194">Per ulteriori informazioni su hello ad altri elementi, vedere [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="dbc14-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="dbc14-195">Hello <**AdBreak**> può anche contenere un elemento <**TrackingEvents**> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="dbc14-196">Hello <**TrackingEvents**> elemento consente di tootrack hello inizio o fine di un'interruzione pubblicitaria o se si è verificato un errore durante l'interruzione pubblicitaria hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="dbc14-197">Hello <**TrackingEvents**> elemento contiene uno o più <**rilevamento**> elementi, ognuno dei quali specifica un evento di rilevamento e un URI di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="dbc14-198">eventi di rilevamento possibili Hello sono:</span><span class="sxs-lookup"><span data-stu-id="dbc14-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="dbc14-199">breakStart: rileva inizio hello di un'interruzione pubblicitaria</span><span class="sxs-lookup"><span data-stu-id="dbc14-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="dbc14-200">breakEnd: rileva hello completamento di un'interruzione pubblicitaria</span><span class="sxs-lookup"><span data-stu-id="dbc14-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="dbc14-201">Error: rileva un errore che si è verificato durante l'interruzione pubblicitaria hello</span><span class="sxs-lookup"><span data-stu-id="dbc14-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="dbc14-202">Hello di esempio seguente viene illustrato un file VMAP che specifica gli eventi di rilevamento</span><span class="sxs-lookup"><span data-stu-id="dbc14-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="dbc14-203">Per ulteriori informazioni su hello <**TrackingEvents**> elemento e i relativi elementi figlio, vedere http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="dbc14-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="dbc14-204">Uso di un file MAST (Media Abstract Sequencing Template)</span><span class="sxs-lookup"><span data-stu-id="dbc14-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="dbc14-205">Un file MAST permette toospecify trigger che definiscono quando è visualizzato un annuncio.</span><span class="sxs-lookup"><span data-stu-id="dbc14-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="dbc14-206">di seguito Hello è un file MAST di esempio che contiene i trigger per un annuncio precedente, un annuncio midroll e postroll.</span><span class="sxs-lookup"><span data-stu-id="dbc14-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="dbc14-207">Un file MAST inizia con un elemento **MAST** che contiene un elemento **triggers**.</span><span class="sxs-lookup"><span data-stu-id="dbc14-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="dbc14-208">Hello <triggers> elemento contiene uno o più **trigger** gli elementi che definiscono quando deve essere riprodotto un annuncio.</span><span class="sxs-lookup"><span data-stu-id="dbc14-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="dbc14-209">Hello **trigger** elemento contiene un **startConditions** elemento che specificano quando un annuncio deve iniziare tooplay.</span><span class="sxs-lookup"><span data-stu-id="dbc14-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="dbc14-210">Hello **startConditions** elemento contiene uno o più <condition> elementi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="dbc14-211">Quando ogni <condition> valuta tootrue un trigger è avviato o revocato varia a seconda se hello <condition> è contenuto all'interno di un **startConditions** o **endConditions** elemento rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="dbc14-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="dbc14-212">Quando più <condition> gli elementi sono presenti, vengono considerate come OR implicito, qualsiasi condizione di valutazione tootrue genererà tooinitiate trigger hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="dbc14-213">Gli elementi <condition> possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="dbc14-213"><condition> elements can be nested.</span></span> <span data-ttu-id="dbc14-214">Quando figlio <condition> elementi sono stati definiti, vengono considerate come and implicito e tutte le condizioni devono restituire tootrue per tooinitiate trigger hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="dbc14-215">Hello <condition> elemento contiene hello gli attributi che definiscono la condizione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbc14-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="dbc14-216">**tipo** : Specifica il tipo di hello di condizione, eventi o proprietà</span><span class="sxs-lookup"><span data-stu-id="dbc14-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="dbc14-217">**nome** : hello nome di hello toobe proprietà o evento utilizzato durante la valutazione</span><span class="sxs-lookup"><span data-stu-id="dbc14-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="dbc14-218">**valore** : hello valore che verrà valutata rispetto a una proprietà</span><span class="sxs-lookup"><span data-stu-id="dbc14-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="dbc14-219">**operatore** : hello toouse operazione durante la valutazione: EQ (uguale), NEQ (diverso da), GTR (maggiore), GEQ (maggiore o uguale a), LT (minore di), LEQ (minore o uguale a), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="dbc14-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="dbc14-220">**endConditions** contengono anche elementi <condition>.</span><span class="sxs-lookup"><span data-stu-id="dbc14-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="dbc14-221">Quando si valuta una condizione di trigger hello tootrue è reset.hello <trigger> elemento contiene inoltre un <sources> elemento che contiene uno o più <source> elementi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="dbc14-222">Hello <source> gli elementi definiscono hello URI toohello ad risposta e il tipo di hello della risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="dbc14-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="dbc14-223">In questo esempio non viene specificato un URI risposta VAST tooa.</span><span class="sxs-lookup"><span data-stu-id="dbc14-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="dbc14-224">Uso di VPAID (Video Player-Ad Interface Definition)</span><span class="sxs-lookup"><span data-stu-id="dbc14-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="dbc14-225">VPAID è un'API per l'abilitazione di toocommunicate unità annuncio eseguibile con un lettore video.</span><span class="sxs-lookup"><span data-stu-id="dbc14-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="dbc14-226">Ciò offre esperienze altamente interattive per gli annunci.</span><span class="sxs-lookup"><span data-stu-id="dbc14-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="dbc14-227">Hello utente può interagire con annunci hello e ad hello può rispondere tooactions eseguita dal Visualizzatore hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="dbc14-228">Ad esempio un annuncio può mostrare pulsanti che consentono di hello utente tooview ulteriori informazioni o una versione più lunga dell'annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="dbc14-229">lettore video Hello deve supportare hello API VPAID e annuncio eseguibile hello deve implementare hello API.</span><span class="sxs-lookup"><span data-stu-id="dbc14-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="dbc14-230">Quando un lettore richiede un annuncio da un server di hello ad server può rispondere con una risposta VAST contenente un annuncio vpaid.</span><span class="sxs-lookup"><span data-stu-id="dbc14-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="dbc14-231">Un annuncio eseguibile è creato in codice che deve essere eseguito in un ambiente di runtime, ad esempio Adobe Flash™ o JavaScript eseguibile in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="dbc14-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="dbc14-232">Quando un ad server restituisce una risposta VAST contenente un annuncio vpaid, hello valore dell'attributo apiFramework hello in hello <MediaFile> elemento deve essere "VPAID".</span><span class="sxs-lookup"><span data-stu-id="dbc14-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="dbc14-233">Questo attributo specifica quell'annuncio hello contenuto un annuncio eseguibile vpaid.</span><span class="sxs-lookup"><span data-stu-id="dbc14-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="dbc14-234">Hello tipo attributo deve essere impostato il tipo MIME toohello di hello eseguibile, ad esempio "application/x-shockwave-flash" o "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="dbc14-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="dbc14-235">frammento XML seguente Hello Mostra hello <MediaFile> elemento da una risposta VAST contenente un annuncio eseguibile vpaid.</span><span class="sxs-lookup"><span data-stu-id="dbc14-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="dbc14-236">Un annuncio eseguibile può essere inizializzato utilizzando hello <AdParameters> elemento all'interno di hello <Linear> o <NonLinear> elementi in una risposta VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="dbc14-237">Per ulteriori informazioni su hello <AdParameters> elemento, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="dbc14-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="dbc14-238">Per ulteriori informazioni su hello API VPAID, vedere [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="dbc14-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="dbc14-239">Implementazione di un lettore Windows o Windows Phone 8 con supporto per gli annunci</span><span class="sxs-lookup"><span data-stu-id="dbc14-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="dbc14-240">Hello Microsoft Media Platform: Player Framework per Windows 8 e Windows Phone 8 contiene una raccolta di applicazioni di esempio che illustrano come un'applicazione di lettore video con tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="dbc14-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="dbc14-241">È possibile scaricare esempi di Windows Media Player Framework e hello hello da [Player Framework per Windows 8 e Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="dbc14-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="dbc14-242">Quando si apre hello playerframework soluzione verrà visualizzato un numero di cartelle nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="dbc14-243">cartella Advertising Hello contiene hello esempio codice pertinente toocreating un lettore video con supporto di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbc14-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="dbc14-244">Cartella di annunci hello interno è un numero di XAML/cs file ognuno dei quali Mostra come tooinsert annunci in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="dbc14-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="dbc14-245">Hello seguente elenco descrive ogni:</span><span class="sxs-lookup"><span data-stu-id="dbc14-245">hello following list describes each:</span></span>

* <span data-ttu-id="dbc14-246">AdPodPage.xaml viene illustrato come toodisplay Active Directory contenitore.</span><span class="sxs-lookup"><span data-stu-id="dbc14-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="dbc14-247">Mostra AdSchedulingPage.xaml come tooschedule annunci.</span><span class="sxs-lookup"><span data-stu-id="dbc14-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="dbc14-248">FreeWheelPage.xaml viene illustrato come toouse hello annunci tooschedule di plug-in FreeWheel.</span><span class="sxs-lookup"><span data-stu-id="dbc14-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="dbc14-249">Mostra MastPage.xaml come tooschedule annunci con un file MAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="dbc14-250">Programmaticadpage viene illustrato come pianificare annunci di tooprogrammatically in un video.</span><span class="sxs-lookup"><span data-stu-id="dbc14-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="dbc14-251">Mostra ScheduleClipPage.xaml come tooschedule un annuncio senza un file VAST.</span><span class="sxs-lookup"><span data-stu-id="dbc14-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="dbc14-252">Mostra VastLinearCompanionPage.xaml come tooinsert lineari e annunci complementari.</span><span class="sxs-lookup"><span data-stu-id="dbc14-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="dbc14-253">Mostra VastNonLinearPage.xaml come tooinsert un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="dbc14-254">Mostra VmapPage.xaml come toospecify annunci con un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="dbc14-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="dbc14-255">Ognuno di questi esempi Usa classe MediaPlayer hello definite da hello player framework.</span><span class="sxs-lookup"><span data-stu-id="dbc14-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="dbc14-256">Nella maggior parte degli esempi vengono usati plug-in che aggiungono supporto per vari formati di risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="dbc14-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="dbc14-257">Hello-esempio ProgrammaticAdPage interagisce a livello di codice con un'istanza di MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="dbc14-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="dbc14-258">Esempio AdPodPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-258">AdPodPage Sample</span></span>
<span data-ttu-id="dbc14-259">In questo esempio utilizza hello AdSchedulerPlugin toodefine quando toodisplay Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbc14-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="dbc14-260">In questo esempio un annuncio midroll è pianificato toobe riprodotto dopo 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="dbc14-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="dbc14-261">podcast annuncio Hello (un gruppo di annunci toodisplay in ordine) viene specificato in un file VAST restituito da un ad server.</span><span class="sxs-lookup"><span data-stu-id="dbc14-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="dbc14-262">file VAST toohello di Hello URI specificato nel hello <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="dbc14-263">Per ulteriori informazioni su hello AdSchedulerPlugin, vedere [pubblicità hello Player Framework su Windows 8 e Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="dbc14-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="dbc14-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-264">AdSchedulingPage</span></span>
<span data-ttu-id="dbc14-265">In questo esempio Usa anche hello AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="dbc14-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="dbc14-266">Vengono pianificati tre annunci, un annuncio preroll, un annuncio midroll e un annuncio postroll.</span><span class="sxs-lookup"><span data-stu-id="dbc14-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="dbc14-267">Hello URI toohello VAST per ogni annuncio è specificato un <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="dbc14-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-268">FreeWheelPage</span></span>
<span data-ttu-id="dbc14-269">Questo esempio utilizza hello FreeWheelPlugin che specifica un attributo di origine che specifica un URI file SmartXML tooa punti che specifica il contenuto di Active Directory, nonché informazioni sulla pianificazione di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbc14-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="dbc14-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-270">MastPage</span></span>
<span data-ttu-id="dbc14-271">Questo esempio utilizza hello MastSchedulerPlugin che consente a un file MAST toouse.</span><span class="sxs-lookup"><span data-stu-id="dbc14-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="dbc14-272">attributo di origine Hello specifica il percorso di hello del file MAST hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="dbc14-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="dbc14-274">In questo esempio interagisce a livello di codice con hello Media Player.</span><span class="sxs-lookup"><span data-stu-id="dbc14-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="dbc14-275">file Programmaticadpage Hello crea un'istanza di MediaPlayer hello:</span><span class="sxs-lookup"><span data-stu-id="dbc14-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="dbc14-276">file ProgrammaticAdPage.xaml.cs Hello crea un AdHandlerPlugin, aggiunge un toospecify TimelineMarker quando un annuncio deve essere visualizzato e quindi aggiunge un gestore per l'evento MarkerReached hello che carica un RemoteAdSource specificando un file VAST tooa URI e quindi viene riprodotto annuncio Hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="dbc14-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-277">ScheduleClipPage</span></span>
<span data-ttu-id="dbc14-278">Questo esempio utilizza hello AdSchedulerPlugin tooschedule un annuncio midroll specificando un file con estensione wmv contenente ad hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="dbc14-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="dbc14-280">In questo esempio viene illustrato come toouse hello AdSchedulerPlugin tooschedule un annuncio lineare midroll con un annuncio complementare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="dbc14-281">Hello <RemoteAdSource> elemento specifica il percorso di hello del file VAST hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="dbc14-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="dbc14-283">Questo esempio utilizza hello AdSchedulerPlugin tooschedule lineare e un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="dbc14-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="dbc14-284">Hello percorso del file VAST è specificato con hello <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="dbc14-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="dbc14-285">VMAPPage</span></span>
<span data-ttu-id="dbc14-286">In questo esempio utilizza hello VmapSchedulerPlugin tooschedule gli annunci tramite un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="dbc14-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="dbc14-287">file VMAP toohello di Hello URI specificato nell'attributo di origine hello di hello <VmapSchedulerPlugin> elemento.</span><span class="sxs-lookup"><span data-stu-id="dbc14-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="dbc14-288">Implementazione di un lettore video iOS con supporto per gli annunci</span><span class="sxs-lookup"><span data-stu-id="dbc14-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="dbc14-289">Hello Microsoft Media Platform: Player Framework per iOS contiene una raccolta di applicazioni di esempio che illustrano come un'applicazione di lettore video con tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="dbc14-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="dbc14-290">È possibile scaricare esempi di Windows Media Player Framework e hello hello da [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="dbc14-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="dbc14-291">pagina di github Hello è tooa un collegamento Wiki che contiene informazioni aggiuntive sulla hello player framework e un esempio di lettore toohello Introduzione: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="dbc14-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="dbc14-292">Pianificazione di annunci con VMAP</span><span class="sxs-lookup"><span data-stu-id="dbc14-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="dbc14-293">Hello seguente esempio viene illustrato come gli annunci di tooschedule tramite un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="dbc14-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="dbc14-294">Pianificazione di annunci con VAST</span><span class="sxs-lookup"><span data-stu-id="dbc14-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="dbc14-295">Hello esempio riportato di seguito viene illustrato come tooschedule un annuncio VAST di associazione tardiva.</span><span class="sxs-lookup"><span data-stu-id="dbc14-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="dbc14-296">Hello esempio riportato di seguito viene illustrato come tooschedule un annuncio VAST di associazione anticipata.</span><span class="sxs-lookup"><span data-stu-id="dbc14-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="dbc14-297">Esempio 4: pianificazione un hello VAST //Download annuncio VAST anticipata di associazione file se (! [ framework.adResolver downloadManifest: & manifesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[logFrameworkError self];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="dbc14-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="dbc14-298">Hello esempio riportato di seguito viene illustrato come tooinsert Active Directory utilizzando approssimativa Taglia modifica (ZARE)</span><span class="sxs-lookup"><span data-stu-id="dbc14-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="dbc14-299">Hello esempio seguente viene illustrato come tooschedule Active Directory contenitore.</span><span class="sxs-lookup"><span data-stu-id="dbc14-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="dbc14-300">Hello seguente esempio viene illustrato come tooschedule un annuncio midroll non permanenti.</span><span class="sxs-lookup"><span data-stu-id="dbc14-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="dbc14-301">Un annuncio non nota adesiva viene riprodotto solo una volta indipendentemente dalle eventuali hello ricerca esegue il visualizzatore.</span><span class="sxs-lookup"><span data-stu-id="dbc14-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="dbc14-302">Hello seguente esempio viene illustrato come tooschedule un annuncio midroll permanente.</span><span class="sxs-lookup"><span data-stu-id="dbc14-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="dbc14-303">Verrà visualizzata una nota adesiva ad ogni volta hello specificato viene raggiunto il punto nella sequenza temporale video hello.</span><span class="sxs-lookup"><span data-stu-id="dbc14-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="dbc14-304">Hello esempio riportato di seguito viene illustrato come tooschedule postroll.</span><span class="sxs-lookup"><span data-stu-id="dbc14-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="dbc14-305">Hello esempio riportato di seguito viene illustrato come un annuncio preroll tooschedule.</span><span class="sxs-lookup"><span data-stu-id="dbc14-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="dbc14-306">Hello seguente esempio mostra come tooschedule un midroll sovrapposizione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbc14-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="dbc14-307">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="dbc14-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dbc14-308">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="dbc14-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="dbc14-309">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dbc14-309">See Also</span></span>
[<span data-ttu-id="dbc14-310">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="dbc14-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

