---
title: Panoramica del modello di licenza PlayReady di servizi aaaMedia
description: In questo argomento fornisce una panoramica di un modello di licenza PlayReady licenze PlayReady tooconfigure utilizzato.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="fcba8-103">Panoramica del modello di licenza PlayReady di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="fcba8-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="fcba8-104">Servizi multimediali di Azure offre un servizio per la distribuzione di licenze Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="fcba8-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="fcba8-105">Quando il lettore dell'utente finale hello (ad esempio Silverlight) Cerca tooplay del PlayReady contenuto protetto, una richiesta viene inviato toohello licenza recapito servizio tooobtain una licenza.</span><span class="sxs-lookup"><span data-stu-id="fcba8-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="fcba8-106">Se il servizio licenze hello Approva richiesta di hello, che possono essere emessi licenza hello client toohello inviato e può essere utilizzato toodecrypt e play hello contenuto specificato.</span><span class="sxs-lookup"><span data-stu-id="fcba8-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="fcba8-107">Servizi multimediali fornisce anche API che permettono di configurare le licenze PlayReady.</span><span class="sxs-lookup"><span data-stu-id="fcba8-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="fcba8-108">Le licenze contengono i diritti di hello e le restrizioni che si desidera per hello tooenforce di runtime di PlayReady DRM quando un utente tenta tooplayback contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="fcba8-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="fcba8-109">Di seguito sono disponibili alcuni esempi di limitazioni che possono essere specificate per le licenze PlayReady:</span><span class="sxs-lookup"><span data-stu-id="fcba8-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="fcba8-110">Hello DateTime da cui hello licenza è valida.</span><span class="sxs-lookup"><span data-stu-id="fcba8-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="fcba8-111">valore di data/ora scadenza licenza hello Hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="fcba8-112">Per toobe di licenza hello salvato nell'archivio permanente in client hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="fcba8-113">Le licenze persistenti vengono tooallow in genere utilizzata la riproduzione offline del contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="fcba8-114">livello di protezione minimo Hello che un lettore deve offrire tooplay il contenuto.</span><span class="sxs-lookup"><span data-stu-id="fcba8-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="fcba8-115">livello di protezione per i controlli di output di hello del contenuto audio/video di output di Hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="fcba8-116">Per ulteriori informazioni, vedere controlli Output di hello sezione (3.5) hello in [regole di conformità di PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="fcba8-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="fcba8-117">Attualmente, è possibile configurare solo hello PlayRight della licenza PlayReady hello (questo diritto è richiesto).</span><span class="sxs-lookup"><span data-stu-id="fcba8-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="fcba8-118">Hello PlayRight fornisce ai client hello contenuto hello tooplayback possibilità di hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="fcba8-119">Hello PlayRight consente inoltre di configurare restrizioni specifiche tooplayback.</span><span class="sxs-lookup"><span data-stu-id="fcba8-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="fcba8-120">Per altre informazioni, vedere [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="fcba8-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="fcba8-121">licenze PlayReady tooconfigure tramite servizi multimediali, è necessario configurare il modello di licenza PlayReady di servizi multimediali di hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="fcba8-122">modello di Hello è definito in XML.</span><span class="sxs-lookup"><span data-stu-id="fcba8-122">hello template is defined in XML.</span></span>

<span data-ttu-id="fcba8-123">Hello esempio seguente mostra hello modello più semplice (e più comune) che consente di configurare una licenza di streaming di base.</span><span class="sxs-lookup"><span data-stu-id="fcba8-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="fcba8-124">Con questa licenza i client sarebbero in grado di tooplayback del PlayReady contenuto protetto.</span><span class="sxs-lookup"><span data-stu-id="fcba8-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="fcba8-125">Hello XML conforme toohello modello XML schema di licenza PlayReady definito nel modello di licenza PlayReady hello sezione dello schema XML.</span><span class="sxs-lookup"><span data-stu-id="fcba8-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="fcba8-126">Servizi multimediali definisce inoltre un set di classi .NET che potrebbero essere utilizzati tooserialized e tooand deserializzato da hello XML.</span><span class="sxs-lookup"><span data-stu-id="fcba8-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="fcba8-127">Per una descrizione delle classi principali, vedere [Classi .NET di Servizi multimediali](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="fcba8-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="fcba8-128">che vengono utilizzati tooconfigure modelli di licenza.</span><span class="sxs-lookup"><span data-stu-id="fcba8-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="fcba8-129">Per un esempio end-to-end che utilizza .NET classi modello di licenza PlayReady hello tooconfigure, vedere [utilizzando la crittografia dinamica PlayReady e del servizio di recapito licenze](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="fcba8-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="fcba8-130"><a id="classes"></a>Modelli di licenza tooconfigure utilizzate le classi .NET di servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="fcba8-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="fcba8-131">di seguito Hello sono classi .NET principali hello sono modelli di licenza PlayReady di servizi multimediali tooconfigure utilizzato.</span><span class="sxs-lookup"><span data-stu-id="fcba8-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="fcba8-132">Queste classi vengono mappate toohello tipi definiti in [schema XML del modello di licenza PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="fcba8-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="fcba8-133">Hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) classe è utilizzata tooserialize e deserializzare tooand dal modello di licenza di servizi multimediali di hello XML.</span><span class="sxs-lookup"><span data-stu-id="fcba8-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="fcba8-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="fcba8-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="fcba8-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -questa classe rappresenta il modello di hello per risposta hello inviati toohello back-end utente.</span><span class="sxs-lookup"><span data-stu-id="fcba8-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="fcba8-136">Contiene un campo di una stringa di dati personalizzati tra server licenze hello e un'applicazione hello (potrebbe essere utile per la logica app personalizzata), nonché un elenco di uno o più modelli di licenza.</span><span class="sxs-lookup"><span data-stu-id="fcba8-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="fcba8-137">Questa è hello "principale" classe nella gerarchia del modello hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="fcba8-138">Vale a dire che il modello di risposta hello include un elenco di modelli di licenza e i modelli di licenza hello includono (direttamente o indirettamente) tutte hello altre classi che costituiscono hello modello dati toobe serializzato.</span><span class="sxs-lookup"><span data-stu-id="fcba8-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="fcba8-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="fcba8-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="fcba8-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -classe hello rappresenta un modello di licenza per la creazione di toobe di licenze PlayReady restituiti agli utenti finali toohello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="fcba8-141">Contiene dati hello nella chiave simmetrica di hello nella licenza hello e qualsiasi toobe diritti o restrizioni applicata da hello runtime di PlayReady DRM quando si utilizza la chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="fcba8-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="fcba8-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="fcba8-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="fcba8-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -questa classe rappresenta hello PlayRight di una licenza PlayReady.</span><span class="sxs-lookup"><span data-stu-id="fcba8-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="fcba8-144">Garantisce hello utente hello possibilità tooplayback hello contenuto soggetto toohello zero o più restrizioni configurato nella licenza hello e su hello elemento PlayRight stesso (criterio specifico di riproduzione).</span><span class="sxs-lookup"><span data-stu-id="fcba8-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="fcba8-145">La maggior parte dei criteri di hello in hello PlayRight ha toodo con restrizioni di output che controllano i tipi di output che può essere riprodotto contenuto hello hello ed eventuali restrizioni che devono essere inserite sul posto, quando si usa un determinato output.</span><span class="sxs-lookup"><span data-stu-id="fcba8-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="fcba8-146">Ad esempio, se hello quindi hello DigitalVideoOnlyContentRestriction è abilitato, il runtime DRM consentirà solo toobe video di hello su output digitali (gli output video analogici non consentiti contenuto hello toopass).</span><span class="sxs-lookup"><span data-stu-id="fcba8-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcba8-147">Questi tipi di restrizioni possono essere molto potenti ma possono inoltre influire hello consumer.</span><span class="sxs-lookup"><span data-stu-id="fcba8-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="fcba8-148">Se hello protezioni dell'output sono configurate troppo restrittiva, è possibile che il contenuto di hello potrebbe risultare non riproducibile in alcuni client.</span><span class="sxs-lookup"><span data-stu-id="fcba8-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="fcba8-149">Per ulteriori informazioni, vedere hello [regole di conformità di PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="fcba8-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="fcba8-150">Per un esempio dei livelli di protezione supportati da Silverlight, vedere [Supporto Silverlight per la protezione dell'output](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="fcba8-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="fcba8-151"><a id="schema"></a>Schema XML del modello di licenza PlayReady</span><span class="sxs-lookup"><span data-stu-id="fcba8-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="fcba8-152">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="fcba8-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fcba8-153">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="fcba8-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

