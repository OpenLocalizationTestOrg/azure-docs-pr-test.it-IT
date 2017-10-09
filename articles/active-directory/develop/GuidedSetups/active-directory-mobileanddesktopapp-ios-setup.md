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
## <a name="setting-up-your-ios-application"></a>Configurazione dell'applicazione iOS

In questa sezione vengono fornite istruzioni dettagliate su come un nuovo toodemonstrate progetto toocreate come toointegrate un'applicazione iOS (Swift) con *Accedi con Microsoft* in modo per eseguire una query Web API che richiedono un token.

> Se si preferisce toodownload progetto XCode questo esempio invece, [Scaricare un progetto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) e ignorare toohello [passaggio di configurazione](#create-an-application-express) tooconfigure nell'esempio di codice hello prima dell'esecuzione.


## <a name="install-carthage-toodownload-and-build-msal"></a>Installare toodownload Carthage e compilare MSAL
Gestione di pacchetti Carthage viene utilizzato durante il periodo di anteprima hello di MSAL: si integra con XCode mantenendo il possibilità hello per libreria di Microsoft toomake modifiche toohello.

- Scaricare e installare una versione più recente di hello di Carthage [qui](https://github.com/Carthage/Carthage/releases "Carthage URL di download")

## <a name="creating-your-application"></a>Creazione dell'applicazione

1.  Aprire Xcode e selezionare `Create a new Xcode project`
2.  Selezionare `iOS` > `Single view Application` e fare clic su *Next* (Avanti)
3.  Assegnare un nome prodotto e fare clic su *Next* (Avanti)
4.  Selezionare una cartella toocreate l'app e fare clic su *crea*

## <a name="build-hello-msal-framework"></a>Compilare hello MSAL Framework

Attenersi alle istruzioni hello seguenti toopull e quindi compilare più recente delle librerie MSAL utilizzando Carthage hello:

1.  Aprire terminal bash hello e passare cartella radice dell'applicazione toohello
2.  Hello seguente copiare e incollare nel hello bash terminal toocreate un file 'Cartfile':

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Copiare e incollare hello riportato di seguito. Questo comando recupera le dipendenze in una cartella Carthage/estrazioni, quindi crea hello MSAL libreria:
</li>
</ol>

```bash
carthage update
```

> processo di Hello precedente è toodownload utilizzato e compilazione hello libreria di autenticazione di Microsoft (MSAL). MSAL gestisce l'acquisizione, la memorizzazione nella cache e l'aggiornamento utente token utilizzati tooaccess API protette da Azure Active Directory v2 hello.

## <a name="add-hello-msal-framework-tooyour-application"></a>Aggiungere un'applicazione hello MSAL framework tooyour
1.  In Xcode aprire hello `General` scheda
2.  Passare toohello `Linked Frameworks and Libraries` sezione e fare clic su`+`
3.  Selezionare `Add other…`.
4.  Selezionare: `Carthage` > `Build` > `iOS` > `MSAL.framework` e fare clic su *Open* (Apri). Dovrebbe essere `MSAL.framework` toohello elenco aggiunto.
5.  Andare troppo`Build Phases` scheda e fare clic su `+` icona, scegliere`New Run Script Phase`
6.  Aggiungere hello seguente contenuto toohello *script area*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Aggiungere il seguente troppo di hello<code>Input Files</code> facendo <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Creazione dell'interfaccia utente dell'applicazione
Nell'ambito del modello di progetto viene automaticamente creato un file Main.storyboard. Istruzioni di hello sotto toocreate hello app dell'interfaccia utente:

1.  CTRL + clic `Main.storyboard` toobring alto dal menu di scelta rapida hello e quindi fare clic su:`Open As` > `Source Code`
2.  Sostituire hello `<scenes>` nodo con codice hello riportato di seguito:

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
