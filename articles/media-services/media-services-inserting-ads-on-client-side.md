---
title: Inserimento di annunci sul lato client | Microsoft Docs
description: Questo argomento illustra come inserire annunci sul lato client.
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="1b7bf-103">Inserimento di annunci sul lato client</span><span class="sxs-lookup"><span data-stu-id="1b7bf-103">Inserting ads on the client side</span></span>
<span data-ttu-id="1b7bf-104">Questo argomento contiene informazioni su come inserire diversi tipi di annunci sul lato client.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="1b7bf-105">Per informazioni sul supporto di sottotitoli codificati e annunci nei video in streaming live, vedere, [Sottotitoli codificati supportati e standard per l'inserimento di annunci](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="1b7bf-106">Azure Media Player attualmente non supporta gli annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="1b7bf-107"><a id="insert_ads_into_media"></a>Inserimento di annunci nei file multimediali</span><span class="sxs-lookup"><span data-stu-id="1b7bf-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="1b7bf-108">Servizi multimediali di Azure offre il supporto per l'inserimento di annunci tramite la piattaforma Windows Media Platform, ovvero i player framework.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="1b7bf-109">Player Framework con supporto per gli annunci sono disponibili per i dispositivi Windows 8, Silverlight, Windows Phone 8 e iOS.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="1b7bf-110">Ogni player framework contiene codice di esempio che illustra come implementare un'applicazione di tipo lettore. È possibile inserire tre tipi diversi di annunci nei file multimediali.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="1b7bf-111">**Lineari** : annunci con frequenza massima che interrompono il video principale.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="1b7bf-112">**Non lineari** : annunci sovrapposti visualizzati durante la riproduzione del video principale, in genere un logo o un'altra immagine statica all'interno del lettore.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="1b7bf-113">**Complementari** : annunci visualizzati all'esterno del lettore.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="1b7bf-114">Gli annunci possono essere inseriti in qualsiasi punto della sequenza temporale del video principale.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="1b7bf-115">È necessario indicare al lettore quando riprodurre l'annuncio e quali annunci riprodurre.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="1b7bf-116">Questa operazione viene eseguita mediante una serie di file standard basati su XML: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) e Digital Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="1b7bf-117">I file VAST indicano quali annunci visualizzare,</span><span class="sxs-lookup"><span data-stu-id="1b7bf-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="1b7bf-118">mentre i file VMAP specificano quando riprodurre i vari annunci e contengono XML VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="1b7bf-119">I file MAST rappresentano invece un altro modo di riprodurre in sequenza annunci contenenti XML VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="1b7bf-120">I file VPAID, infine, definiscono un'interfaccia tra il lettore video e l'annuncio o il server di annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="1b7bf-121">Ogni Player Framework ha un funzionamento diverso, che verrà illustrato in un argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="1b7bf-122">Questo argomento illustra i meccanismi di base usati per inserire gli annunci. Le applicazioni di tipo lettore video richiedono gli annunci da un server di annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="1b7bf-123">Il server di annunci può rispondere in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="1b7bf-124">Restituzione di un file VAST</span><span class="sxs-lookup"><span data-stu-id="1b7bf-124">Return a VAST file</span></span>
* <span data-ttu-id="1b7bf-125">Restituzione di un file VMAP (con VAST incorporato)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="1b7bf-126">Restituzione di un file MAST (con VAST incorporato)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="1b7bf-127">Restituzione di un file VAST con annunci VPAID</span><span class="sxs-lookup"><span data-stu-id="1b7bf-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="1b7bf-128">Uso di un file VAST (Video Ad Service Template)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="1b7bf-129">Un file VAST specifica gli annunci da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="1b7bf-130">Il codice XML seguente è un esempio di un file VAST per un annuncio lineare:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="1b7bf-131">L'annuncio lineare viene descritto dall'elemento <**Linear**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="1b7bf-132">Specifica la durata dell'annuncio, gli eventi di rilevamento, il clickthrough, il monitoraggio dei clic e alcuni elementi **MediaFile**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="1b7bf-133">Gli eventi di rilevamento vengono specificati entro l'elemento <**TrackingEvents**> e permette a un server di annunci di rilevare diversi elementi che si verificano durante la visualizzazione dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="1b7bf-134">In questo caso vengono rilevati gli eventi iniziali, intermedi, di completamento e di espansione.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="1b7bf-135">L'evento iniziale si verifica quando l'annuncio viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="1b7bf-136">L'evento intermedio si verifica quando è stato visualizzato almeno il 50% della sequenza temporale dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="1b7bf-137">L'evento di completamento si verifica quando l'esecuzione dell'annuncio è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="1b7bf-138">L'evento di espansione di verifica quando l'utente espande il lettore video visualizzandolo a schermo intero.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="1b7bf-139">I clickthrough vengono specificati con un elemento <**ClickThrough**> entro un elemento <**VideoClicks**> e specifica un URI per una risorsa da visualizzare quando l'utente fa clic sull'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="1b7bf-140">Il monitoraggio dei clic viene specificato in un elemento <**ClickTracking**>, incluso in un elemento <**VideoClicks**> e specifica una risorsa di rilevamento che il lettore può richiedere quando l'utente fa clic sull'annuncio. Gli elementi <**MediaFile**> specificano informazioni su una codifica specifica di un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="1b7bf-141">Quando sono presenti più elementi <**MediaFile**>, il lettore video può scegliere la codifica migliore per la piattaforma.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="1b7bf-142">Gli annunci lineari possono essere visualizzati in un ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="1b7bf-143">A tale scopo, aggiungere altri elementi <Ad> al file VAST e specificare l'ordine usando l'attributo di sequenza.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="1b7bf-144">L'esempio seguente illustra questi concetti.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="1b7bf-145">Anche gli annunci non lineari vengono specificati in un elemento <Creative>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="1b7bf-146">L'esempio seguente illustra un elemento <Creative> che descrive un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="1b7bf-147">L'elemento <**NonLinearAds**> può contenere uno o più elementi <**NonLinear**>, ognuno dei quali può descrivere un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="1b7bf-148">L'elemento <**NonLinear**> specifica la risorsa per l'annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="1b7bf-149">La risorsa può essere di tipo <**StaticResouce**>, <**IFrameResource**> o <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="1b7bf-150"> <**StaticResource**> descrive una risorsa non HTML e definisce un attributo creativeType che specifica la modalità di visualizzazione della risorsa:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="1b7bf-151">Image/gif, image/jpeg, image/png: la risorsa viene visualizzata in un tag HTML <**img**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="1b7bf-152">Application/x-javascript: la risorsa viene visualizzata in un tag HTML <**script**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="1b7bf-153">Application/x-shockwave-flash: la risorsa viene visualizzata in un lettore Flash.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="1b7bf-154">**IFrameResource** descrive una risorsa HTML che può essere visualizzata in un IFrame.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="1b7bf-155">**HTMLResource** descrive una parte di codice HTML che può essere inserita in una pagina Web.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="1b7bf-156">**TrackingEvents** specifica gli eventi di rilevamento e l'URI da richiedere quando si verifica un evento.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="1b7bf-157">In questo esempio vengono rilevati gli eventi acceptInvitation e collapse.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="1b7bf-158">Per altre informazioni sull'elemento **NonLinearAds** e i rispettivi figli, vedere IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="1b7bf-159">Si noti che l'elemento **TrackingEvents** si trova entro l'elemento **NonLinearAds** invece dell'elemento **NonLinear**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="1b7bf-160">Gli annunci complementari vengono definiti entro un elemento <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="1b7bf-161">L'elemento <CompanionAds> può contenere uno o più elementi <Companion>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="1b7bf-162">Ogni elemento <Companion> descrive un annuncio complementare e può contenere una risorsa di tipo <StaticResource>, <IFrameResource>, o <HTMLResource>, specificata in modo analogo a un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="1b7bf-163">Un file VAST può contenere più annunci complementari e il lettore può scegliere quello più adatto da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="1b7bf-164">Per altre informazioni su VAST, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="1b7bf-165">Uso di un file VMAP (Video Multiple Ad Playlist) digitale</span><span class="sxs-lookup"><span data-stu-id="1b7bf-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="1b7bf-166">Un file VMAP permette di specificare quando si verificano le interruzioni pubblicitarie, la durata di ogni interruzione, quanti annunci possono essere visualizzati in ogni interruzione e il tipo di annunci da visualizzare in un'interruzione.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="1b7bf-167">L'esempio seguente illustra un file VMAP che definisce una singola interruzione pubblicitaria:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="1b7bf-168">Un file VMAP inizia con un elemento <VMAP> che include uno o più elementi <AdBreak>, ognuno dei quali definisce un'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="1b7bf-169">Ogni interruzione pubblicitaria specifica un tipo di interruzione, un ID di interruzione e un offset temporale.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="1b7bf-170">L'attributo breakType specifica il tipo di annuncio che può essere riprodotto durante l'interruzione: lineare, non lineare o di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="1b7bf-171">Gli annunci di visualizzazione sono mappati agli annunci complementari VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="1b7bf-172">È possibile specificare più tipi di annuncio in un elenco separato da virgole (senza spazi).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="1b7bf-173">breakID è un identificatore facoltativo per l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="1b7bf-174">timeOffset specifica quando deve essere visualizzato l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="1b7bf-175">Può essere specificato in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="1b7bf-176">Tempo: con formato hh:mm:ss o hh:mm:ss.mmm, dove .mmm corrisponde a millisecondi.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="1b7bf-177">Il valore di questo attributo specifica il tempo dall'inizio della sequenza temporale del video all'inizio dell'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="1b7bf-178">Percentuale: con formato n% dove n indica la percentuale della sequenza temporale del video da riprodurre prima della visualizzazione dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="1b7bf-179">Inizio/Fine: specifica che un annuncio deve essere visualizzato prima o dopo la visualizzazione del video.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="1b7bf-180">Posizione: specifica l'ordine delle interruzioni pubblicitarie quando la tempistica delle interruzioni pubblicitarie è sconosciuta ad esempio nello streaming live.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="1b7bf-181">L'ordine di ogni interruzione è specificato con il formato #n dove n è un valore Integer pari a 1 o superiore.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="1b7bf-182">1 indica che l'annuncio deve essere riprodotto alla prima opportunità, 2 indica che l'annuncio deve essere riprodotto alla seconda opportunità e così via.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="1b7bf-183">Nell'elemento <**AdBreak**> può essere presente un elemento <**AdSource**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="1b7bf-184">L'elemento <**AdSource**> contiene gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="1b7bf-185">ID: specifica un identificatore per l'origine dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="1b7bf-186">allowMultipleAds: valore booleano che specifica se è possibile visualizzare più annunci durante l'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="1b7bf-187">followRedirects: valore booleano facoltativo che specifica se il lettore deve rispettare i reindirizzamenti in una risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="1b7bf-188">L'elemento <**AdSource**> fornisce al lettore una risposta inline all'annuncio o un riferimento a una risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="1b7bf-189">Può contenere uno degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="1b7bf-190"><VASTAdData> indica che una risposta annuncio VAST è incorporata nel file VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="1b7bf-191"><AdTagURI>: un URI che fa riferimento a una risposta annuncio da un altro sistema.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="1b7bf-192"><CustomAdData>: -una stringa arbitraria che rappresenta una risposta non VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="1b7bf-193">In questo esempio una risposta annuncio inline è specificata con un elemento <VASTAdData> che contiene una risposta annuncio VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="1b7bf-194">Per altre informazioni sugli altri elementi, vedere [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="1b7bf-195">L'elemento <**AdBreak**> può contenere anche un elemento <**TrackingEvents**>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="1b7bf-196">L'elemento <**TrackingEvents**> permette di rilevare l'inizio o la fine di un'interruzione pubblicitaria o eventuali errori verificatisi durante l'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="1b7bf-197">L'elemento <**TrackingEvents**> contiene uno o più elementi <**Tracking**>, ognuno dei quali specifica un evento di rilevamento e un URI di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="1b7bf-198">Di seguito sono elencati gli eventi di rilevamento possibili:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="1b7bf-199">breakStart: rileva l'inizio di un'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="1b7bf-200">breakEnd: rileva il completamento di un'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="1b7bf-201">error: rileva un errore verificatosi durante l'interruzione pubblicitaria.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="1b7bf-202">L'esempio seguente mostra un file VMAP che specifica gli eventi di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="1b7bf-203">Per altre informazioni sull'elemento <**TrackingEvents**> e i rispettivi elementi figlio, vedere http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="1b7bf-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="1b7bf-204">Uso di un file MAST (Media Abstract Sequencing Template)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="1b7bf-205">Un file MAST permette di specificare i trigger che definiscono il momento in cui è visualizzato un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="1b7bf-206">Di seguito è riportato un file MAST di esempio che contiene trigger per un annuncio di tipo preroll, midroll e postroll.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="1b7bf-207">Un file MAST inizia con un elemento **MAST** che contiene un elemento **triggers**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="1b7bf-208">L'elemento <triggers> contiene uno o più elementi **trigger** che definiscono quando deve essere riprodotto un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="1b7bf-209">L'elemento **trigger** contiene un elemento **startConditions** che specifica quando deve iniziare la riproduzione di un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="1b7bf-210">L'elemento **startConditions** contiene uno o più elementi <condition>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="1b7bf-211">Quando ogni elemento <condition> restituisce true, sarà avviato o revocato un trigger, rispettivamente in base alla presenza di <condition> in un elemento **startConditions** o **endConditions**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="1b7bf-212">Se sono presenti più elementi <condition>, saranno considerati come OR implicito e qualsiasi condizione che restituisce true provocherà l'avvio del trigger.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="1b7bf-213">Gli elementi <condition> possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-213"><condition> elements can be nested.</span></span> <span data-ttu-id="1b7bf-214">Quando gli elementi <condition> figlio sono preimpostati, sono considerati come AND implicito e per l'avvio del trigger tutte le condizioni devono restituire true.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="1b7bf-215">L'elemento <condition> contiene gli attributi seguenti che definiscono la condizione:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="1b7bf-216">**type** - specifica il tipo di condizione, di evento o di proprietà.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="1b7bf-217">**name** - nome della proprietà o dell'evento da usare durante la valutazione.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="1b7bf-218">**value** – valore in base al quale sarà valutata una proprietà.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="1b7bf-219">**operator** : operazione da usare durante la valutazione: EQ (uguale), NEQ (diverso da), GTR (maggiore), GEQ (maggiore o uguale), LT (minore), LEQ (minore o uguale), MOD (modulo).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="1b7bf-220">**endConditions** contengono anche elementi <condition>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="1b7bf-221">Quando una condizione restituisce true, il trigger viene reimpostato. L'elemento <trigger> contiene anche un elemento <sources> che include uno o più elementi <source>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="1b7bf-222">Gli elementi <source> definiscono l'URI per la risposta annuncio e il tipo della risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="1b7bf-223">In questo esempio si assegna un URI a una risposta VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="1b7bf-224">Uso di VPAID (Video Player-Ad Interface Definition)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="1b7bf-225">VPAID è un'API che permette alle unità di annuncio eseguibili di comunicare con un lettore video.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="1b7bf-226">Ciò offre esperienze altamente interattive per gli annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="1b7bf-227">L'utente può interagire con l'annuncio e l'annuncio può rispondere alle azioni eseguite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="1b7bf-228">Ad esempio, un annuncio può mostrare pulsanti che permettono all'utente di visualizzare altre informazioni o una versione più lunga dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="1b7bf-229">Il lettore video deve supportare l'API VPAID e l'annuncio eseguibile la deve implementare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="1b7bf-230">Quando un lettore richiede un annuncio da un ad server, è possibile che il server risponda con una risposta VAST contenente un annuncio VPAID.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="1b7bf-231">Un annuncio eseguibile è creato in codice che deve essere eseguito in un ambiente di runtime, ad esempio Adobe Flash™ o JavaScript eseguibile in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="1b7bf-232">Quando un ad server restituisce una risposta VAST contenente un annuncio VPAID, il valore dell'attributo apiFramework nell'elemento <MediaFile> deve essere "VPAID".</span><span class="sxs-lookup"><span data-stu-id="1b7bf-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="1b7bf-233">Questo attributo specifica che l'annuncio incluso è un annuncio eseguibile VPAID.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="1b7bf-234">L'attributo type deve essere impostato sul tipo MIME dell'eseguibile, ad esempio "application/x-shockwave-flash" o "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="1b7bf-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="1b7bf-235">Il frammento di codice XML seguente mostra l'elemento <MediaFile> da una risposta VAST contenente un annuncio eseguibile VPAID.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="1b7bf-236">Un annuncio eseguibile può essere inizializzato mediante l'elemento <AdParameters> negli elementi <Linear> o <NonLinear> in una risposta VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="1b7bf-237">Per altre informazioni sull'elemento <AdParameters>, vedere [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="1b7bf-238">Per altre informazioni sull'API VPAID, vedere [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="1b7bf-239">Implementazione di un lettore Windows o Windows Phone 8 con supporto per gli annunci</span><span class="sxs-lookup"><span data-stu-id="1b7bf-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="1b7bf-240">Microsoft Media Platform: Player Framework per Windows 8 e Windows Phone 8 contiene una raccolta di applicazioni di esempio che illustrano come implementare un'applicazione per la lettura di video tramite il framework.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="1b7bf-241">È possibile scaricare Player Framework e i relativi esempi dalla pagina relativa a [Player Framework per Windows 8 e Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="1b7bf-242">Quando si apre la soluzione Microsoft.PlayerFramework.Xaml.Samples, verrà visualizzato un numero di cartelle all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="1b7bf-243">La cartella Advertising contiene il codice di esempio necessario per la creazione di un lettore video con supporto per gli annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="1b7bf-244">All'interno della cartella Advertising è presente un numero di file XAML/cs, ognuno dei quali mostra come inserire gli annunci in una specifica modalità.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="1b7bf-245">L'elenco seguente descrive i singoli file:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-245">The following list describes each:</span></span>

* <span data-ttu-id="1b7bf-246">AdPodPage.xaml - Mostra come visualizzare un podcast annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="1b7bf-247">AdSchedulingPage.xaml - Mostra come pianificare annunci.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="1b7bf-248">FreeWheelPage.xaml - Mostra come usare il plug-in FreeWheel per pianificare annunci</span><span class="sxs-lookup"><span data-stu-id="1b7bf-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="1b7bf-249">MastPage.xaml - Mostra come pianificare annunci con un file MAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="1b7bf-250">ProgrammaticAdPage.xaml - Mostra come pianificare la visualizzazione di annunci in un video a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="1b7bf-251">ScheduleClipPage.xaml - Mostra come pianificare un annuncio senza usare un file VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="1b7bf-252">VastLinearCompanionPage.xaml - Mostra come inserire annunci lineari e annunci complementari.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="1b7bf-253">VastNonLinearPage.xaml - Mostra come inserire un annuncio non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="1b7bf-254">VmapPage.xaml - Mostra come specificare annunci con un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="1b7bf-255">Ognuno di questi esempi usa la classe MediaPlayer definita da Player Framework.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="1b7bf-256">Nella maggior parte degli esempi vengono usati plug-in che aggiungono supporto per vari formati di risposta annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="1b7bf-257">L'esempio ProgrammaticAdPage interagisce a livello di codice con un'istanza MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="1b7bf-258">Esempio AdPodPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-258">AdPodPage Sample</span></span>
<span data-ttu-id="1b7bf-259">Questo esempio usa AdSchedulerPlugin per definire quando visualizzare un annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="1b7bf-260">In questo esempio viene pianificata la riproduzione di un annuncio midroll dopo 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="1b7bf-261">Il podcast annuncio (ossia un gruppo di annunci visualizzati in ordine) è specificato in un file VAST restituito da un ad server.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="1b7bf-262">L'URI per il file VAST è specificato nell'elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="1b7bf-263">Per altre informazioni su AdSchedulerPlugin, vedere la pagina relativa all' [inserimento di annunci in Player Framework su Windows 8 e Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="1b7bf-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-264">AdSchedulingPage</span></span>
<span data-ttu-id="1b7bf-265">Questo esempio usa AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="1b7bf-266">Vengono pianificati tre annunci, un annuncio preroll, un annuncio midroll e un annuncio postroll.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="1b7bf-267">L'URI per il VAST per ciascuno di essi è specificato in un elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="1b7bf-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-268">FreeWheelPage</span></span>
<span data-ttu-id="1b7bf-269">Questo esempio usa FreeWheelPlugin, che specifica un attributo Source che a sua volta specifica un URI che punta a un file SmartXML in cui è specificato il contenuto dell'annuncio, oltre alle informazioni di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="1b7bf-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-270">MastPage</span></span>
<span data-ttu-id="1b7bf-271">Questo esempio usa MastSchedulerPlugin, che consente di usare un file MAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="1b7bf-272">L'attributo Source specifica il percorso del file MAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="1b7bf-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="1b7bf-274">Questo esempio interagisce a livello di codice con MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="1b7bf-275">Il file ProgrammaticAdPage.xaml crea un'istanza di MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="1b7bf-276">Il file ProgrammaticAdPage.xaml.cs crea un oggetto AdHandlerPlugin, aggiunge un elemento TimelineMarker per specificare quando un annuncio deve essere visualizzato, quindi aggiunge un gestore per l'evento MarkerReached che carica un oggetto RemoteAdSource specificando un URI a un file VAST, quindi riproduce l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="1b7bf-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-277">ScheduleClipPage</span></span>
<span data-ttu-id="1b7bf-278">Questo esempio usa AdSchedulerPlugin per pianificare un annuncio midroll specificando un file con estensione wmv contenente l'annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="1b7bf-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="1b7bf-280">L'esempio illustra come usare AdSchedulerPlugin per pianificare un annuncio lineare midroll con un annuncio complementare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="1b7bf-281">L'elemento <RemoteAdSource> specifica il percorso del file VAST.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="1b7bf-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="1b7bf-283">Questo esempio usa l'elemento AdSchedulerPlugin per pianificare un annuncio lineare e uno non lineare.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="1b7bf-284">Il percorso del file VAST è specificato nell'elemento <RemoteAdSource>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="1b7bf-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="1b7bf-285">VMAPPage</span></span>
<span data-ttu-id="1b7bf-286">Questo esempio usa l'elemento VmapSchedulerPlugin per pianificare annunci usando un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="1b7bf-287">L'URI al file VMAP è specificato nell'attributo Source dell'elemento <VmapSchedulerPlugin>.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="1b7bf-288">Implementazione di un lettore video iOS con supporto per gli annunci</span><span class="sxs-lookup"><span data-stu-id="1b7bf-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="1b7bf-289">Microsoft Media Platform: Player Framework per iOS contiene una raccolta di applicazioni di esempio che illustrano come implementare un'applicazione per la lettura di video tramite il framework.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="1b7bf-290">È possibile scaricare Player Framework e i relativi esempi dalla pagina relativa a [Media Player Framework di Azure](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="1b7bf-291">La pagina di GitHub include un collegamento a una pagina Wiki che contiene informazioni aggiuntive su player framework e un'introduzione all'esempio del lettore, ovvero la pagina [Wiki su Media Player di Azure](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="1b7bf-292">Pianificazione di annunci con VMAP</span><span class="sxs-lookup"><span data-stu-id="1b7bf-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="1b7bf-293">L'esempio seguente illustra come pianificare gli annunci usando un file VMAP.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="1b7bf-294">Pianificazione di annunci con VAST</span><span class="sxs-lookup"><span data-stu-id="1b7bf-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="1b7bf-295">L'esempio seguente illustra come pianificare un annuncio VAST ad associazione tardiva.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="1b7bf-296">L'esempio seguente illustra come pianificare un annuncio VAST ad associazione anticipata.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="1b7bf-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="1b7bf-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="1b7bf-298">L'esempio seguente illustra come inserire un annuncio usando Rough Cut Editing (RCE)</span><span class="sxs-lookup"><span data-stu-id="1b7bf-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="1b7bf-299">L'esempio seguente illustra come pianificare un podcast annuncio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="1b7bf-300">L'esempio seguente illustra come pianificare un annuncio midroll temporaneo.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="1b7bf-301">Un annuncio temporaneo viene riprodotto solo una volta, indipendentemente da qualsiasi ricerca eseguita dal visualizzatore.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="1b7bf-302">L'esempio seguente illustra come pianificare un annuncio midroll permanente.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="1b7bf-303">Un annuncio permanente verrà visualizzato ogni volta che viene raggiunto il punto specificato nella sequenza temporale del video.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="1b7bf-304">L'esempio seguente illustra come pianificare un annuncio postroll.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="1b7bf-305">L'esempio seguente illustra come pianificare un annuncio preroll.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="1b7bf-306">L'esempio seguente illustra come pianificare un annuncio midroll sovrapposto.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="1b7bf-307">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1b7bf-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1b7bf-308">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1b7bf-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1b7bf-309">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1b7bf-309">See Also</span></span>
[<span data-ttu-id="1b7bf-310">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="1b7bf-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

