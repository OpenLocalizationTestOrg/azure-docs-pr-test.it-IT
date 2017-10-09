---
title: iOS v2 aaaAzure AD Getting Started - il programma di installazione | Documenti Microsoft
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="83795-103">Configurazione dell'applicazione iOS</span><span class="sxs-lookup"><span data-stu-id="83795-103">Setting up your iOS application</span></span>

<span data-ttu-id="83795-104">In questa sezione vengono fornite istruzioni dettagliate su come un nuovo toodemonstrate progetto toocreate come toointegrate un'applicazione iOS (Swift) con *Accedi con Microsoft* in modo per eseguire una query Web API che richiedono un token.</span><span class="sxs-lookup"><span data-stu-id="83795-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="83795-105">Se si preferisce toodownload progetto XCode questo esempio invece,</span><span class="sxs-lookup"><span data-stu-id="83795-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="83795-106">[Scaricare un progetto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83795-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="83795-107">Installare toodownload Carthage e compilare MSAL</span><span class="sxs-lookup"><span data-stu-id="83795-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="83795-108">Gestione di pacchetti Carthage viene utilizzato durante il periodo di anteprima hello di MSAL: si integra con XCode mantenendo il possibilità hello per libreria di Microsoft toomake modifiche toohello.</span><span class="sxs-lookup"><span data-stu-id="83795-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="83795-109">Scaricare e installare una versione più recente di hello di Carthage [qui](https://github.com/Carthage/Carthage/releases "Carthage URL di download")</span><span class="sxs-lookup"><span data-stu-id="83795-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="83795-110">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="83795-110">Creating your application</span></span>

1.  <span data-ttu-id="83795-111">Aprire Xcode e selezionare `Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="83795-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="83795-112">Selezionare `iOS` > `Single view Application` e fare clic su *Next* (Avanti)</span><span class="sxs-lookup"><span data-stu-id="83795-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="83795-113">Assegnare un nome prodotto e fare clic su *Next* (Avanti)</span><span class="sxs-lookup"><span data-stu-id="83795-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="83795-114">Selezionare una cartella toocreate l'app e fare clic su *crea*</span><span class="sxs-lookup"><span data-stu-id="83795-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="83795-115">Compilare hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="83795-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="83795-116">Attenersi alle istruzioni hello seguenti toopull e quindi compilare più recente delle librerie MSAL utilizzando Carthage hello:</span><span class="sxs-lookup"><span data-stu-id="83795-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="83795-117">Aprire terminal bash hello e passare cartella radice dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="83795-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="83795-118">Hello seguente copiare e incollare nel hello bash terminal toocreate un file 'Cartfile':</span><span class="sxs-lookup"><span data-stu-id="83795-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="83795-119">Copiare e incollare hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="83795-119">Copy and paste hello below.</span></span> <span data-ttu-id="83795-120">Questo comando recupera le dipendenze in una cartella Carthage/estrazioni, quindi crea hello MSAL libreria:</span><span class="sxs-lookup"><span data-stu-id="83795-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="83795-121">processo di Hello precedente è toodownload utilizzato e compilazione hello libreria di autenticazione di Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="83795-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="83795-122">MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente token utilizzati tooaccess API protette da Azure Active Directory v2 hello.</span><span class="sxs-lookup"><span data-stu-id="83795-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="83795-123">Aggiungere un'applicazione hello MSAL framework tooyour</span><span class="sxs-lookup"><span data-stu-id="83795-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="83795-124">In Xcode aprire hello `General` scheda</span><span class="sxs-lookup"><span data-stu-id="83795-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="83795-125">Passare toohello `Linked Frameworks and Libraries` sezione e fare clic su`+`</span><span class="sxs-lookup"><span data-stu-id="83795-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="83795-126">Selezionare `Add other…`.</span><span class="sxs-lookup"><span data-stu-id="83795-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="83795-127">Selezionare: `Carthage` > `Build` > `iOS` > `MSAL.framework` e fare clic su *Open* (Apri).</span><span class="sxs-lookup"><span data-stu-id="83795-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="83795-128">Dovrebbe essere `MSAL.framework` toohello elenco aggiunto.</span><span class="sxs-lookup"><span data-stu-id="83795-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="83795-129">Andare troppo`Build Phases` scheda e fare clic su `+` icona, scegliere`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="83795-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="83795-130">Aggiungere hello seguente contenuto toohello *script area*:</span><span class="sxs-lookup"><span data-stu-id="83795-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="83795-131">Aggiungere il seguente troppo di hello<code>Input Files</code> facendo <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="83795-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="83795-132">Creazione dell'interfaccia utente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="83795-132">Creating your application’s UI</span></span>
<span data-ttu-id="83795-133">Nell'ambito del modello di progetto viene automaticamente creato un file Main.storyboard.</span><span class="sxs-lookup"><span data-stu-id="83795-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="83795-134">Istruzioni di hello sotto toocreate hello app dell'interfaccia utente:</span><span class="sxs-lookup"><span data-stu-id="83795-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="83795-135">CTRL + clic `Main.storyboard` toobring alto dal menu di scelta rapida hello e quindi fare clic su:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="83795-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="83795-136">Sostituire hello `<scenes>` nodo con codice hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="83795-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
