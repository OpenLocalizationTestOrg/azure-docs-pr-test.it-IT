---
title: 'Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni | Documentazione Microsoft'
description: Riferimento delle espressioni di provisioning dichiarativo nel servizio di sincronizzazione Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="5e95f-103">Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni</span><span class="sxs-lookup"><span data-stu-id="5e95f-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="5e95f-104">In Azure AD Connect, le funzioni sono toomanipulate utilizzato un valore di attributo durante la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="5e95f-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="5e95f-105">Sintassi delle funzioni hello Hello viene espresso nel formato hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5e95f-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="5e95f-106">Se una funzione è in overload e accetta più sintassi, verranno elencate tutte quelle valide.</span><span class="sxs-lookup"><span data-stu-id="5e95f-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="5e95f-107">le funzioni Hello sono fortemente tipizzate e verificano che il tipo di hello passato nel tipo hello documentato corrispondenze.</span><span class="sxs-lookup"><span data-stu-id="5e95f-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="5e95f-108">Se il tipo di hello non corrisponde, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="5e95f-109">tipi di Hello sono espressi con hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="5e95f-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="5e95f-110">**bin** : binario</span><span class="sxs-lookup"><span data-stu-id="5e95f-110">**bin** – Binary</span></span>
* <span data-ttu-id="5e95f-111">**bool** : booleano</span><span class="sxs-lookup"><span data-stu-id="5e95f-111">**bool** – Boolean</span></span>
* <span data-ttu-id="5e95f-112">**dt** : data/ora UTC</span><span class="sxs-lookup"><span data-stu-id="5e95f-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="5e95f-113">**enum** : enumerazione di costanti note</span><span class="sxs-lookup"><span data-stu-id="5e95f-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="5e95f-114">**EXP** : espressione, è previsto tooevaluate tooa booleano</span><span class="sxs-lookup"><span data-stu-id="5e95f-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="5e95f-115">**mvbin** : binario multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="5e95f-116">**mvstr** : stringa multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="5e95f-117">**mvref** : riferimento multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="5e95f-118">**num** : numerico</span><span class="sxs-lookup"><span data-stu-id="5e95f-118">**num** – Numeric</span></span>
* <span data-ttu-id="5e95f-119">**ref** : riferimento</span><span class="sxs-lookup"><span data-stu-id="5e95f-119">**ref** – Reference</span></span>
* <span data-ttu-id="5e95f-120">**str** : stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-120">**str** – String</span></span>
* <span data-ttu-id="5e95f-121">**var** : variante di (quasi) tutti gli altri tipi</span><span class="sxs-lookup"><span data-stu-id="5e95f-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="5e95f-122">**void** : non restituisce un valore</span><span class="sxs-lookup"><span data-stu-id="5e95f-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="5e95f-123">funzioni con i tipi di hello Hello **mvbin**, **mvstr**, e **mvref** può funzionare solo su attributi multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="5e95f-124">Le funzioni con **bin**, **str** e **ref** operano con gli attributi a valore singolo e multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="5e95f-125">Riferimento alle funzioni</span><span class="sxs-lookup"><span data-stu-id="5e95f-125">Functions Reference</span></span>
| <span data-ttu-id="5e95f-126">Elenco di funzioni</span><span class="sxs-lookup"><span data-stu-id="5e95f-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5e95f-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="5e95f-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="5e95f-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="5e95f-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="5e95f-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="5e95f-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="5e95f-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="5e95f-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="5e95f-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="5e95f-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="5e95f-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="5e95f-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="5e95f-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="5e95f-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="5e95f-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="5e95f-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5e95f-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="5e95f-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="5e95f-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="5e95f-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="5e95f-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="5e95f-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="5e95f-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="5e95f-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="5e95f-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="5e95f-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="5e95f-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="5e95f-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="5e95f-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="5e95f-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="5e95f-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="5e95f-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="5e95f-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="5e95f-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="5e95f-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="5e95f-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="5e95f-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="5e95f-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="5e95f-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="5e95f-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="5e95f-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="5e95f-150">**Conversione**</span><span class="sxs-lookup"><span data-stu-id="5e95f-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="5e95f-151">CBool</span><span class="sxs-lookup"><span data-stu-id="5e95f-151">CBool</span></span>](#cbool) |[<span data-ttu-id="5e95f-152">CDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-152">CDate</span></span>](#cdate) |[<span data-ttu-id="5e95f-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="5e95f-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="5e95f-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="5e95f-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="5e95f-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="5e95f-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5e95f-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="5e95f-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5e95f-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="5e95f-158">CNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="5e95f-159">CRef</span><span class="sxs-lookup"><span data-stu-id="5e95f-159">CRef</span></span>](#cref) |[<span data-ttu-id="5e95f-160">CStr</span><span class="sxs-lookup"><span data-stu-id="5e95f-160">CStr</span></span>](#cstr) |[<span data-ttu-id="5e95f-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="5e95f-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="5e95f-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="5e95f-163">**Data/Ora**</span><span class="sxs-lookup"><span data-stu-id="5e95f-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="5e95f-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="5e95f-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="5e95f-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="5e95f-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="5e95f-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="5e95f-167">Now</span><span class="sxs-lookup"><span data-stu-id="5e95f-167">Now</span></span>](#now) | |
| [<span data-ttu-id="5e95f-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="5e95f-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="5e95f-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="5e95f-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="5e95f-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="5e95f-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="5e95f-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="5e95f-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="5e95f-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="5e95f-173">**Versione di valutazione**</span><span class="sxs-lookup"><span data-stu-id="5e95f-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="5e95f-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="5e95f-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="5e95f-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="5e95f-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="5e95f-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="5e95f-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="5e95f-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="5e95f-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="5e95f-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="5e95f-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="5e95f-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="5e95f-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="5e95f-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="5e95f-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="5e95f-182">IsString</span><span class="sxs-lookup"><span data-stu-id="5e95f-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="5e95f-183">**Matematiche**</span><span class="sxs-lookup"><span data-stu-id="5e95f-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="5e95f-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="5e95f-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="5e95f-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="5e95f-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="5e95f-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="5e95f-187">**A più valori**</span><span class="sxs-lookup"><span data-stu-id="5e95f-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="5e95f-188">Contiene</span><span class="sxs-lookup"><span data-stu-id="5e95f-188">Contains</span></span>](#contains) |[<span data-ttu-id="5e95f-189">Numero</span><span class="sxs-lookup"><span data-stu-id="5e95f-189">Count</span></span>](#count) |[<span data-ttu-id="5e95f-190">Elemento</span><span class="sxs-lookup"><span data-stu-id="5e95f-190">Item</span></span>](#item) |[<span data-ttu-id="5e95f-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="5e95f-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="5e95f-192">Join</span><span class="sxs-lookup"><span data-stu-id="5e95f-192">Join</span></span>](#join) |[<span data-ttu-id="5e95f-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="5e95f-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="5e95f-194">Split</span><span class="sxs-lookup"><span data-stu-id="5e95f-194">Split</span></span>](#split) | | |
| <span data-ttu-id="5e95f-195">**Flusso del programma**</span><span class="sxs-lookup"><span data-stu-id="5e95f-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="5e95f-196">Errore</span><span class="sxs-lookup"><span data-stu-id="5e95f-196">Error</span></span>](#error) |[<span data-ttu-id="5e95f-197">IIF</span><span class="sxs-lookup"><span data-stu-id="5e95f-197">IIF</span></span>](#iif) |[<span data-ttu-id="5e95f-198">Selezionare</span><span class="sxs-lookup"><span data-stu-id="5e95f-198">Select</span></span>](#select) |[<span data-ttu-id="5e95f-199">Switch</span><span class="sxs-lookup"><span data-stu-id="5e95f-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="5e95f-200">Dove</span><span class="sxs-lookup"><span data-stu-id="5e95f-200">Where</span></span>](#where) |[<span data-ttu-id="5e95f-201">With</span><span class="sxs-lookup"><span data-stu-id="5e95f-201">With</span></span>](#with) | | | |
| <span data-ttu-id="5e95f-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="5e95f-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="5e95f-203">GUID</span><span class="sxs-lookup"><span data-stu-id="5e95f-203">GUID</span></span>](#guid) |[<span data-ttu-id="5e95f-204">InStr</span><span class="sxs-lookup"><span data-stu-id="5e95f-204">InStr</span></span>](#instr) |[<span data-ttu-id="5e95f-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="5e95f-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="5e95f-206">LCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="5e95f-207">Left</span><span class="sxs-lookup"><span data-stu-id="5e95f-207">Left</span></span>](#left) |[<span data-ttu-id="5e95f-208">Len</span><span class="sxs-lookup"><span data-stu-id="5e95f-208">Len</span></span>](#len) |[<span data-ttu-id="5e95f-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="5e95f-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="5e95f-210">Mid</span><span class="sxs-lookup"><span data-stu-id="5e95f-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="5e95f-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="5e95f-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="5e95f-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="5e95f-212">PadRight</span></span>](#padright) |[<span data-ttu-id="5e95f-213">PCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-213">PCase</span></span>](#pcase) |[<span data-ttu-id="5e95f-214">Replace</span><span class="sxs-lookup"><span data-stu-id="5e95f-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="5e95f-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="5e95f-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="5e95f-216">Right</span><span class="sxs-lookup"><span data-stu-id="5e95f-216">Right</span></span>](#right) |[<span data-ttu-id="5e95f-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="5e95f-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="5e95f-218">Trim</span><span class="sxs-lookup"><span data-stu-id="5e95f-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="5e95f-219">UCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-219">UCase</span></span>](#ucase) |[<span data-ttu-id="5e95f-220">Word</span><span class="sxs-lookup"><span data-stu-id="5e95f-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="5e95f-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="5e95f-221">BitAnd</span></span>
<span data-ttu-id="5e95f-222">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-222">**Description:**</span></span>  
<span data-ttu-id="5e95f-223">Hello funzione BitAnd imposta i bit specificati su un valore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="5e95f-224">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="5e95f-225">value1, value2: valori numerici da unire con AND</span><span class="sxs-lookup"><span data-stu-id="5e95f-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="5e95f-226">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-226">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-227">Questa funzione converte una rappresentazione binaria di toohello entrambi i parametri e imposta un bit:</span><span class="sxs-lookup"><span data-stu-id="5e95f-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="5e95f-228">0 - se uno o entrambi i bit corrispondenti di hello *mask* e *flag* sono pari a 0</span><span class="sxs-lookup"><span data-stu-id="5e95f-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="5e95f-229">1 - se nessuno dei bit corrispondenti hello è 1.</span><span class="sxs-lookup"><span data-stu-id="5e95f-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="5e95f-230">In altre parole, restituisce 0 in tutti i casi tranne quando hello bit corrispondenti di entrambi i parametri hanno valore 1.</span><span class="sxs-lookup"><span data-stu-id="5e95f-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="5e95f-231">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="5e95f-232">Restituisce 7 esadecimale "F" e "F7" restituiscono il valore toothis.</span><span class="sxs-lookup"><span data-stu-id="5e95f-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="5e95f-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="5e95f-233">BitOr</span></span>
<span data-ttu-id="5e95f-234">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-234">**Description:**</span></span>  
<span data-ttu-id="5e95f-235">Hello funzione BitOr imposta i bit specificati su un valore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="5e95f-236">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="5e95f-237">value1, value2: valori numerici da unire con OR</span><span class="sxs-lookup"><span data-stu-id="5e95f-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="5e95f-238">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-238">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-239">Questa funzione converte una rappresentazione binaria di toohello entrambi i parametri e imposta un too1 bit se uno o entrambi i bit corrispondenti di hello nella maschera e nel flag sono 1 e too0 se entrambi i bit corrispondenti hello è 0.</span><span class="sxs-lookup"><span data-stu-id="5e95f-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="5e95f-240">In altre parole, restituisce 1 in tutti i casi tranne dove hello bit corrispondenti di entrambi i parametri hanno valore 0.</span><span class="sxs-lookup"><span data-stu-id="5e95f-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="5e95f-241">CBool</span><span class="sxs-lookup"><span data-stu-id="5e95f-241">CBool</span></span>
<span data-ttu-id="5e95f-242">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-242">**Description:**</span></span>  
<span data-ttu-id="5e95f-243">Hello funzione CBool restituisce che un valore booleano basato su espressione valutata hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="5e95f-244">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="5e95f-245">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-245">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-246">Se l'espressione hello restituisce tooa valore diverso da zero, CBool restituisce True, altrimenti restituisce False.</span><span class="sxs-lookup"><span data-stu-id="5e95f-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="5e95f-247">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="5e95f-248">Restituisce True se entrambi attributi hanno hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="5e95f-249">CDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-249">CDate</span></span>
<span data-ttu-id="5e95f-250">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-250">**Description:**</span></span>  
<span data-ttu-id="5e95f-251">Hello funzione CDate restituisce un valore DateTime UTC da una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="5e95f-252">DateTime non è un attributo nativo in Sync, ma viene usato da alcune funzioni.</span><span class="sxs-lookup"><span data-stu-id="5e95f-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="5e95f-253">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="5e95f-254">Value: una stringa con una data, un'ora e facoltativamente un fuso orario</span><span class="sxs-lookup"><span data-stu-id="5e95f-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="5e95f-255">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-255">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-256">Hello restituito è sempre di stringa in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="5e95f-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="5e95f-257">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="5e95f-258">Restituisce un valore DateTime in base a ora di inizio del dipendente hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="5e95f-259">Restituisce un valore di data/ora che rappresenta "2013-01-11 12:00 AM"</span><span class="sxs-lookup"><span data-stu-id="5e95f-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="5e95f-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="5e95f-260">CertExtensionOids</span></span>
<span data-ttu-id="5e95f-261">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-261">**Description:**</span></span>  
<span data-ttu-id="5e95f-262">Restituisce hello Oid valori di tutte le estensioni critiche hello di un oggetto del certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="5e95f-263">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-264">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-265">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="5e95f-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="5e95f-266">CertFormat</span></span>
<span data-ttu-id="5e95f-267">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-267">**Description:**</span></span>  
<span data-ttu-id="5e95f-268">Restituisce hello nome del formato di hello del certificato x. 509v3.</span><span class="sxs-lookup"><span data-stu-id="5e95f-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="5e95f-269">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-270">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-271">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="5e95f-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="5e95f-272">CertFriendlyName</span></span>
<span data-ttu-id="5e95f-273">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-273">**Description:**</span></span>  
<span data-ttu-id="5e95f-274">Restituisce l'alias di un certificato associato hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="5e95f-275">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-276">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-277">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="5e95f-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="5e95f-278">CertHashString</span></span>
<span data-ttu-id="5e95f-279">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-279">**Description:**</span></span>  
<span data-ttu-id="5e95f-280">Restituisce hello valore hash SHA1 per il certificato x. 509v3 hello sotto forma di stringa esadecimale.</span><span class="sxs-lookup"><span data-stu-id="5e95f-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="5e95f-281">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-282">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-283">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="5e95f-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="5e95f-284">CertIssuer</span></span>
<span data-ttu-id="5e95f-285">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-285">**Description:**</span></span>  
<span data-ttu-id="5e95f-286">Restituisce hello nome dell'autorità di certificazione hello che ha emesso il certificato di x. 509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="5e95f-287">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-288">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-289">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="5e95f-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="5e95f-290">CertIssuerDN</span></span>
<span data-ttu-id="5e95f-291">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-291">**Description:**</span></span>  
<span data-ttu-id="5e95f-292">Restituisce hello nome distinto dell'autorità di certificazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="5e95f-293">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-294">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-295">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="5e95f-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-296">CertIssuerOid</span></span>
<span data-ttu-id="5e95f-297">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-297">**Description:**</span></span>  
<span data-ttu-id="5e95f-298">Restituisce hello Oid dell'autorità di certificazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="5e95f-299">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-300">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-301">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="5e95f-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5e95f-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="5e95f-303">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-303">**Description:**</span></span>  
<span data-ttu-id="5e95f-304">Restituisce le informazioni dell'algoritmo delle chiavi di hello per il certificato x. 509v3 sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="5e95f-305">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-306">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-307">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="5e95f-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="5e95f-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="5e95f-309">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-309">**Description:**</span></span>  
<span data-ttu-id="5e95f-310">Restituisce i parametri dell'algoritmo delle chiavi di hello certificato x. 509v3 hello sotto forma di stringa esadecimale.</span><span class="sxs-lookup"><span data-stu-id="5e95f-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="5e95f-311">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-312">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-313">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="5e95f-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="5e95f-314">CertNameInfo</span></span>
<span data-ttu-id="5e95f-315">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-315">**Description:**</span></span>  
<span data-ttu-id="5e95f-316">Restituisce autorità emittente e oggetto hello nomi da un certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="5e95f-317">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="5e95f-318">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-319">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="5e95f-320">X509NameType: hello X509NameType valore per il soggetto hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="5e95f-321">includesIssuerName: nome dell'autorità emittente di hello tooinclude true; in caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="5e95f-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="5e95f-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="5e95f-322">CertNotAfter</span></span>
<span data-ttu-id="5e95f-323">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-323">**Description:**</span></span>  
<span data-ttu-id="5e95f-324">Restituisce la data hello nell'ora locale dopo il quale un certificato non è più valido.</span><span class="sxs-lookup"><span data-stu-id="5e95f-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="5e95f-325">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-326">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-327">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="5e95f-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="5e95f-328">CertNotBefore</span></span>
<span data-ttu-id="5e95f-329">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-329">**Description:**</span></span>  
<span data-ttu-id="5e95f-330">Restituisce la data hello nell'ora locale in cui un certificato diventa valido.</span><span class="sxs-lookup"><span data-stu-id="5e95f-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="5e95f-331">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-332">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-333">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="5e95f-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-334">CertPublicKeyOid</span></span>
<span data-ttu-id="5e95f-335">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-335">**Description:**</span></span>  
<span data-ttu-id="5e95f-336">Restituisce hello Oid della chiave pubblica di hello certificato x. 509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="5e95f-337">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-338">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-339">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="5e95f-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="5e95f-341">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-341">**Description:**</span></span>  
<span data-ttu-id="5e95f-342">Restituisce hello Oid dei parametri di chiave pubblica hello certificato x. 509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="5e95f-343">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-344">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-345">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="5e95f-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="5e95f-346">CertSerialNumber</span></span>
<span data-ttu-id="5e95f-347">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-347">**Description:**</span></span>  
<span data-ttu-id="5e95f-348">Restituisce il numero di serie hello del certificato x. 509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="5e95f-349">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-350">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-351">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="5e95f-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="5e95f-353">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-353">**Description:**</span></span>  
<span data-ttu-id="5e95f-354">Restituisce hello Oid dell'algoritmo hello utilizzato firma hello toocreate di un certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="5e95f-355">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-356">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-357">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="5e95f-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="5e95f-358">CertSubject</span></span>
<span data-ttu-id="5e95f-359">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-359">**Description:**</span></span>  
<span data-ttu-id="5e95f-360">Ottiene hello nome distinto del soggetto da un certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="5e95f-361">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-362">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-363">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="5e95f-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="5e95f-364">CertSubjectNameDN</span></span>
<span data-ttu-id="5e95f-365">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-365">**Description:**</span></span>  
<span data-ttu-id="5e95f-366">Restituisce hello nome distinto del soggetto da un certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="5e95f-367">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-368">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-369">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="5e95f-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="5e95f-370">CertSubjectNameOid</span></span>
<span data-ttu-id="5e95f-371">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-371">**Description:**</span></span>  
<span data-ttu-id="5e95f-372">Restituisce hello Oid del nome soggetto hello da un certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="5e95f-373">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-374">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-375">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="5e95f-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="5e95f-376">CertThumbprint</span></span>
<span data-ttu-id="5e95f-377">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-377">**Description:**</span></span>  
<span data-ttu-id="5e95f-378">Restituisce hello identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="5e95f-379">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-380">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-381">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="5e95f-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="5e95f-382">CertVersion</span></span>
<span data-ttu-id="5e95f-383">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-383">**Description:**</span></span>  
<span data-ttu-id="5e95f-384">Restituisce hello versione del formato di un certificato x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="5e95f-385">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-386">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-387">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="5e95f-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-388">CGuid</span></span>
<span data-ttu-id="5e95f-389">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-389">**Description:**</span></span>  
<span data-ttu-id="5e95f-390">Hello funzione CGuid Converte la rappresentazione di stringa hello della rappresentazione binaria di tooits GUID.</span><span class="sxs-lookup"><span data-stu-id="5e95f-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="5e95f-391">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="5e95f-392">Stringa formattata con questo schema: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="5e95f-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="5e95f-393">Contiene</span><span class="sxs-lookup"><span data-stu-id="5e95f-393">Contains</span></span>
<span data-ttu-id="5e95f-394">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-394">**Description:**</span></span>  
<span data-ttu-id="5e95f-395">funzione Contains Hello trova una stringa all'interno di un attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="5e95f-396">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-396">**Syntax:**</span></span>  
<span data-ttu-id="5e95f-397">`num Contains (mvstring attribute, str search)` - distinzione maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="5e95f-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="5e95f-398">`num Contains (mvref attribute, str search)` - distinzione maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="5e95f-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="5e95f-399">attributo: hello toosearch di un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="5e95f-400">ricerca: stringa toofind nell'attributo hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="5e95f-401">Casetype: CaseInsensitive o CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="5e95f-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="5e95f-402">Restituisce l'indice nell'attributo multivalore hello in cui trovare la stringa hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="5e95f-403">Se la stringa hello non viene trovata, viene restituito 0.</span><span class="sxs-lookup"><span data-stu-id="5e95f-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="5e95f-404">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-404">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-405">Per gli attributi di stringa multivalore, ricerca hello trova le sottostringhe nei valori hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="5e95f-406">Per gli attributi di riferimento, hello stringa cercata deve corrispondere esattamente toobe valore hello considerata una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="5e95f-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="5e95f-407">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="5e95f-408">Se l'attributo proxyAddresses hello dispone di un indirizzo di posta elettronica primario (indicato da lettere maiuscole "SMTP:"), quindi restituire l'attributo proxyAddress hello, in caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="5e95f-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="5e95f-409">ConvertFromBase64</span></span>
<span data-ttu-id="5e95f-410">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-410">**Description:**</span></span>  
<span data-ttu-id="5e95f-411">Hello ConvertFromBase64 funzione converte hello specificato stringa regolare tooa di valore con codificata base64.</span><span class="sxs-lookup"><span data-stu-id="5e95f-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="5e95f-412">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-412">**Syntax:**</span></span>  
<span data-ttu-id="5e95f-413">`str ConvertFromBase64(str source)`: presuppone l'uso di Unicode per la codifica</span><span class="sxs-lookup"><span data-stu-id="5e95f-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="5e95f-414">source: stringa con codifica Base 64</span><span class="sxs-lookup"><span data-stu-id="5e95f-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="5e95f-415">Encoding: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="5e95f-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="5e95f-416">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="5e95f-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="5e95f-417">Entrambi gli esempi restituiscono "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="5e95f-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="5e95f-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5e95f-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="5e95f-419">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-419">**Description:**</span></span>  
<span data-ttu-id="5e95f-420">Hello ConvertFromUTF8Hex funzione converte hello specificato stringa tooa di valore con codifica Hex UTF8.</span><span class="sxs-lookup"><span data-stu-id="5e95f-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="5e95f-421">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="5e95f-422">source: stringa con codifica a 2 byte UTF8</span><span class="sxs-lookup"><span data-stu-id="5e95f-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="5e95f-423">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-423">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-424">Hello differenza tra questa funzione e ConvertFromBase64([],UTF8) tale risultato hello è descrittivo per l'attributo DN hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="5e95f-425">Questo formato viene utilizzato da Azure Active Directory come DN.</span><span class="sxs-lookup"><span data-stu-id="5e95f-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="5e95f-426">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="5e95f-427">Restituisce "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="5e95f-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="5e95f-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="5e95f-428">ConvertToBase64</span></span>
<span data-ttu-id="5e95f-429">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-429">**Description:**</span></span>  
<span data-ttu-id="5e95f-430">Hello funzione ConvertToBase64 converte una stringa base 64 Unicode di tooa stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="5e95f-431">Converte il valore di hello di una matrice di interi tooits equivalente rappresentazione di stringa codificata con cifre base 64.</span><span class="sxs-lookup"><span data-stu-id="5e95f-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="5e95f-432">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="5e95f-433">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="5e95f-434">Restituisce "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="5e95f-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="5e95f-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5e95f-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="5e95f-436">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-436">**Description:**</span></span>  
<span data-ttu-id="5e95f-437">Hello funzione ConvertToUTF8Hex converte tooa una stringa valore Hex UTF8.</span><span class="sxs-lookup"><span data-stu-id="5e95f-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="5e95f-438">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="5e95f-439">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-439">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-440">formato di output di Hello di questa funzione viene usato da Azure Active Directory come formato di attributo DN.</span><span class="sxs-lookup"><span data-stu-id="5e95f-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="5e95f-441">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="5e95f-442">Restituisce 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="5e95f-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="5e95f-443">Numero</span><span class="sxs-lookup"><span data-stu-id="5e95f-443">Count</span></span>
<span data-ttu-id="5e95f-444">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-444">**Description:**</span></span>  
<span data-ttu-id="5e95f-445">Hello funzione Count restituisce il numero di hello di elementi in un attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="5e95f-446">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="5e95f-447">CNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-447">CNum</span></span>
<span data-ttu-id="5e95f-448">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-448">**Description:**</span></span>  
<span data-ttu-id="5e95f-449">Hello funzione CNum accetta una stringa e restituisce un tipo di dati numerici.</span><span class="sxs-lookup"><span data-stu-id="5e95f-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="5e95f-450">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="5e95f-451">CRef</span><span class="sxs-lookup"><span data-stu-id="5e95f-451">CRef</span></span>
<span data-ttu-id="5e95f-452">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-452">**Description:**</span></span>  
<span data-ttu-id="5e95f-453">Converte un attributo di riferimento di stringa tooa</span><span class="sxs-lookup"><span data-stu-id="5e95f-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="5e95f-454">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="5e95f-455">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="5e95f-456">CStr</span><span class="sxs-lookup"><span data-stu-id="5e95f-456">CStr</span></span>
<span data-ttu-id="5e95f-457">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-457">**Description:**</span></span>  
<span data-ttu-id="5e95f-458">Hello dalla funzione CStr converte il tipo di dati stringa tooa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="5e95f-459">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="5e95f-460">value: può essere un valore numerico, un attributo di riferimento o un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="5e95f-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="5e95f-461">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="5e95f-462">Può restituire "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="5e95f-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="5e95f-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="5e95f-463">DateAdd</span></span>
<span data-ttu-id="5e95f-464">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-464">**Description:**</span></span>  
<span data-ttu-id="5e95f-465">Restituisce un valore Date contenente un toowhich data che è stato aggiunto un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="5e95f-466">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="5e95f-467">intervallo: espressione stringa che rappresenta l'intervallo di hello dell'ora in cui si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="5e95f-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="5e95f-468">la stringa Hello deve avere uno dei seguenti valori hello:</span><span class="sxs-lookup"><span data-stu-id="5e95f-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="5e95f-469">yyyy Year</span><span class="sxs-lookup"><span data-stu-id="5e95f-469">yyyy Year</span></span>
  * <span data-ttu-id="5e95f-470">q Quarter</span><span class="sxs-lookup"><span data-stu-id="5e95f-470">q Quarter</span></span>
  * <span data-ttu-id="5e95f-471">m Month</span><span class="sxs-lookup"><span data-stu-id="5e95f-471">m Month</span></span>
  * <span data-ttu-id="5e95f-472">y Day of year</span><span class="sxs-lookup"><span data-stu-id="5e95f-472">y Day of year</span></span>
  * <span data-ttu-id="5e95f-473">d Day</span><span class="sxs-lookup"><span data-stu-id="5e95f-473">d Day</span></span>
  * <span data-ttu-id="5e95f-474">w Weekday</span><span class="sxs-lookup"><span data-stu-id="5e95f-474">w Weekday</span></span>
  * <span data-ttu-id="5e95f-475">ww Week</span><span class="sxs-lookup"><span data-stu-id="5e95f-475">ww Week</span></span>
  * <span data-ttu-id="5e95f-476">h Hour</span><span class="sxs-lookup"><span data-stu-id="5e95f-476">h Hour</span></span>
  * <span data-ttu-id="5e95f-477">n Minute</span><span class="sxs-lookup"><span data-stu-id="5e95f-477">n Minute</span></span>
  * <span data-ttu-id="5e95f-478">s Second</span><span class="sxs-lookup"><span data-stu-id="5e95f-478">s Second</span></span>
* <span data-ttu-id="5e95f-479">valore: hello numero di unità si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="5e95f-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="5e95f-480">Può essere positivo (tooget date nel futuro hello) o negativo (tooget date in hello precedente).</span><span class="sxs-lookup"><span data-stu-id="5e95f-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="5e95f-481">Data: DateTime che rappresenta data toowhich hello intervallo viene aggiunto.</span><span class="sxs-lookup"><span data-stu-id="5e95f-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="5e95f-482">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="5e95f-483">Aggiunge 3 mesi e restituisce un valore di data/ora che rappresenta "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="5e95f-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="5e95f-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-484">DateFromNum</span></span>
<span data-ttu-id="5e95f-485">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-485">**Description:**</span></span>  
<span data-ttu-id="5e95f-486">Hello funzione DateFromNum converte un valore in tooa di formato data AD tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="5e95f-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="5e95f-487">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="5e95f-488">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="5e95f-489">Restituisce un valore di data/ora che rappresenta 2012-01-01 23:00:00</span><span class="sxs-lookup"><span data-stu-id="5e95f-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="5e95f-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="5e95f-490">DNComponent</span></span>
<span data-ttu-id="5e95f-491">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-491">**Description:**</span></span>  
<span data-ttu-id="5e95f-492">Hello funzione DNComponent restituisce il valore di hello di un componente DN specificato da sinistra.</span><span class="sxs-lookup"><span data-stu-id="5e95f-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="5e95f-493">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="5e95f-494">DN: hello riferimento attributo toointerpret</span><span class="sxs-lookup"><span data-stu-id="5e95f-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="5e95f-495">ComponentNumber: componente di hello hello DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="5e95f-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="5e95f-496">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="5e95f-497">Se dn è "cn=Joe,ou=…," verrà restituito Joe</span><span class="sxs-lookup"><span data-stu-id="5e95f-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="5e95f-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="5e95f-498">DNComponentRev</span></span>
<span data-ttu-id="5e95f-499">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-499">**Description:**</span></span>  
<span data-ttu-id="5e95f-500">Hello funzione DNComponentRev restituisce il valore di hello di un componente DN specificato da destra (fine hello).</span><span class="sxs-lookup"><span data-stu-id="5e95f-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="5e95f-501">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="5e95f-502">DN: hello riferimento attributo toointerpret</span><span class="sxs-lookup"><span data-stu-id="5e95f-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="5e95f-503">ComponentNumber - componente hello tooreturn hello DN</span><span class="sxs-lookup"><span data-stu-id="5e95f-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="5e95f-504">Options: DC - Ignora tutti i componenti con "dc="</span><span class="sxs-lookup"><span data-stu-id="5e95f-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="5e95f-505">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-505">**Example:**</span></span>  
<span data-ttu-id="5e95f-506">Se dn è "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com", allora</span><span class="sxs-lookup"><span data-stu-id="5e95f-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="5e95f-507">restituiscono entrambi US.</span><span class="sxs-lookup"><span data-stu-id="5e95f-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="5e95f-508">Errore</span><span class="sxs-lookup"><span data-stu-id="5e95f-508">Error</span></span>
<span data-ttu-id="5e95f-509">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-509">**Description:**</span></span>  
<span data-ttu-id="5e95f-510">funzione di errore Hello è tooreturn usato un errore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="5e95f-511">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="5e95f-512">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="5e95f-513">Se hello attributo accountName non è presente, verrà generato un errore nell'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="5e95f-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="5e95f-514">EscapeDNComponent</span></span>
<span data-ttu-id="5e95f-515">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-515">**Description:**</span></span>  
<span data-ttu-id="5e95f-516">Hello funzione EscapeDNComponent accetta un componente di un DN e utilizza caratteri di escape in modo può essere rappresentato in LDAP.</span><span class="sxs-lookup"><span data-stu-id="5e95f-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="5e95f-517">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="5e95f-518">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="5e95f-519">Assicura che l'oggetto di hello può essere creato in una directory LDAP, anche se l'attributo displayName hello contiene caratteri che devono essere sottoposti a escape in LDAP.</span><span class="sxs-lookup"><span data-stu-id="5e95f-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="5e95f-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="5e95f-520">FormatDateTime</span></span>
<span data-ttu-id="5e95f-521">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-521">**Description:**</span></span>  
<span data-ttu-id="5e95f-522">Funzione FormatDateTime Hello è tooformat utilizzata una stringa tooa DateTime con un formato specificato</span><span class="sxs-lookup"><span data-stu-id="5e95f-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="5e95f-523">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="5e95f-524">valore: un valore in formato DateTime hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="5e95f-525">formato: una stringa che rappresenta hello formato tooconvert per.</span><span class="sxs-lookup"><span data-stu-id="5e95f-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="5e95f-526">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-526">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-527">Hello i valori possibili per il formato di hello è disponibili qui: [formati di data/ora definiti dall'utente (funzione Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="5e95f-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="5e95f-528">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="5e95f-529">Il risultato è "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="5e95f-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="5e95f-530">Può restituire "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="5e95f-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="5e95f-531">GUID</span><span class="sxs-lookup"><span data-stu-id="5e95f-531">GUID</span></span>
<span data-ttu-id="5e95f-532">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-532">**Description:**</span></span>  
<span data-ttu-id="5e95f-533">funzione Hello GUID genera un nuovo GUID casuale</span><span class="sxs-lookup"><span data-stu-id="5e95f-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="5e95f-534">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="5e95f-535">IIF</span><span class="sxs-lookup"><span data-stu-id="5e95f-535">IIF</span></span>
<span data-ttu-id="5e95f-536">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-536">**Description:**</span></span>  
<span data-ttu-id="5e95f-537">Hello funzione IIF restituisce un set di valori possibili in base a una condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="5e95f-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="5e95f-538">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="5e95f-539">condizione: qualsiasi valore o espressione che può essere valutata tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="5e95f-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="5e95f-540">valueIfTrue: se hello Condition tootrue, hello restituito di valore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="5e95f-541">valueIfFalse: se hello Condition toofalse, hello restituito di valore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="5e95f-542">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="5e95f-543">Se l'utente di hello è un interno, restituisce hello alias di un utente con"t" aggiunto toohello inizio, else restituisce hello alias utente è.</span><span class="sxs-lookup"><span data-stu-id="5e95f-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="5e95f-544">InStr</span><span class="sxs-lookup"><span data-stu-id="5e95f-544">InStr</span></span>
<span data-ttu-id="5e95f-545">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-545">**Description:**</span></span>  
<span data-ttu-id="5e95f-546">Hello funzione InStr trova hello prima occorrenza di una sottostringa in una stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="5e95f-547">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="5e95f-548">StringCheck: toobe la ricerca di stringhe</span><span class="sxs-lookup"><span data-stu-id="5e95f-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="5e95f-549">StringMatch: stringa toobe trovato</span><span class="sxs-lookup"><span data-stu-id="5e95f-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="5e95f-550">Start: avvio posizione toofind hello sottostringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="5e95f-551">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="5e95f-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="5e95f-552">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-552">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-553">Posizione di hello restituisce in cui è stata trovata la sottostringa hello o 0 se non trovato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="5e95f-554">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="5e95f-555">/ / Restituisce too5</span><span class="sxs-lookup"><span data-stu-id="5e95f-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="5e95f-556">Valuta too7</span><span class="sxs-lookup"><span data-stu-id="5e95f-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="5e95f-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="5e95f-557">InStrRev</span></span>
<span data-ttu-id="5e95f-558">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-558">**Description:**</span></span>  
<span data-ttu-id="5e95f-559">Hello funzione InStrRev trova hello l'ultima occorrenza di una sottostringa in una stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="5e95f-560">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="5e95f-561">StringCheck: toobe la ricerca di stringhe</span><span class="sxs-lookup"><span data-stu-id="5e95f-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="5e95f-562">StringMatch: stringa toobe trovato</span><span class="sxs-lookup"><span data-stu-id="5e95f-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="5e95f-563">Start: avvio posizione toofind hello sottostringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="5e95f-564">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="5e95f-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="5e95f-565">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-565">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-566">Posizione di hello restituisce in cui è stata trovata la sottostringa hello o 0 se non trovato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="5e95f-567">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="5e95f-568">Restituisce 7</span><span class="sxs-lookup"><span data-stu-id="5e95f-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="5e95f-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="5e95f-569">IsBitSet</span></span>
<span data-ttu-id="5e95f-570">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-570">**Description:**</span></span>  
<span data-ttu-id="5e95f-571">funzione Hello IsBitSet verifica se un bit è impostato o non</span><span class="sxs-lookup"><span data-stu-id="5e95f-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="5e95f-572">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="5e95f-573">valore: un valore numerico valutato. flag: un valore numerico che è hello bit toobe valutata</span><span class="sxs-lookup"><span data-stu-id="5e95f-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="5e95f-574">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="5e95f-575">Restituisce True perché bit "4" è impostato il valore esadecimale di hello "F"</span><span class="sxs-lookup"><span data-stu-id="5e95f-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="5e95f-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-576">IsDate</span></span>
<span data-ttu-id="5e95f-577">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-577">**Description:**</span></span>  
<span data-ttu-id="5e95f-578">Se può essere espressione hello valuta come tipo DateTime, hello funzione IsDate restituisce tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5e95f-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="5e95f-579">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="5e95f-580">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-580">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-581">Utilizzare toodetermine se CDate () può avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="5e95f-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="5e95f-582">IsCert</span></span>
<span data-ttu-id="5e95f-583">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-583">**Description:**</span></span>  
<span data-ttu-id="5e95f-584">Restituisce true se i dati non elaborati hello possono essere serializzati in oggetto certificato X509Certificate2 .NET.</span><span class="sxs-lookup"><span data-stu-id="5e95f-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="5e95f-585">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5e95f-586">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5e95f-587">Matrice di byte Hello può essere binaria (DER) con codificata o dati con codifica base 64 x. 509.</span><span class="sxs-lookup"><span data-stu-id="5e95f-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="5e95f-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="5e95f-588">IsEmpty</span></span>
<span data-ttu-id="5e95f-589">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-589">**Description:**</span></span>  
<span data-ttu-id="5e95f-590">Se l'attributo hello è presente in hello CS o MV, ma restituisce una stringa vuota tooan, funzione IsEmpty hello valuta tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5e95f-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="5e95f-591">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="5e95f-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-592">IsGuid</span></span>
<span data-ttu-id="5e95f-593">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-593">**Description:**</span></span>  
<span data-ttu-id="5e95f-594">Se la stringa hello può essere convertito tooa GUID, funzione isguid restituisce hello valutata tootrue.</span><span class="sxs-lookup"><span data-stu-id="5e95f-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="5e95f-595">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="5e95f-596">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-596">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-597">Un GUID viene definito come stringa in base a uno degli schemi seguenti: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="5e95f-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="5e95f-598">Utilizzare toodetermine se cguid () può avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="5e95f-599">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="5e95f-600">Se hello StrAttribute ha un formato GUID, restituisce una rappresentazione binaria, in caso contrario, restituire un valore Null.</span><span class="sxs-lookup"><span data-stu-id="5e95f-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="5e95f-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="5e95f-601">IsNull</span></span>
<span data-ttu-id="5e95f-602">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-602">**Description:**</span></span>  
<span data-ttu-id="5e95f-603">Se hello espressione tooNull, funzione IsNull hello restituisce true.</span><span class="sxs-lookup"><span data-stu-id="5e95f-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="5e95f-604">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="5e95f-605">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-605">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-606">Per un attributo, un valore Null è espresso dall'assenza di hello dell'attributo hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="5e95f-607">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="5e95f-608">Restituisce True se l'attributo hello non è presente in hello CS o MV.</span><span class="sxs-lookup"><span data-stu-id="5e95f-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="5e95f-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="5e95f-609">IsNullOrEmpty</span></span>
<span data-ttu-id="5e95f-610">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-610">**Description:**</span></span>  
<span data-ttu-id="5e95f-611">Se l'espressione di hello è null o una stringa vuota, funzione IsNullOrEmpty hello restituisce true.</span><span class="sxs-lookup"><span data-stu-id="5e95f-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="5e95f-612">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="5e95f-613">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-613">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-614">Per un attributo, verrà restituito tooTrue se attributo hello è assente o è presente ma è una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="5e95f-615">funzione inversa di Hello di questa funzione è denominata IsPresent.</span><span class="sxs-lookup"><span data-stu-id="5e95f-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="5e95f-616">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="5e95f-617">Restituisce True se l'attributo hello non è presente o è una stringa vuota in hello CS o MV.</span><span class="sxs-lookup"><span data-stu-id="5e95f-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="5e95f-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="5e95f-618">IsNumeric</span></span>
<span data-ttu-id="5e95f-619">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-619">**Description:**</span></span>  
<span data-ttu-id="5e95f-620">Hello funzione IsNumeric restituisce un valore booleano che indica se un'espressione può essere valutata come tipo di numero.</span><span class="sxs-lookup"><span data-stu-id="5e95f-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="5e95f-621">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="5e95f-622">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-622">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-623">Utilizzare toodetermine se cnum () può essere espressione hello tooparse ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="5e95f-624">IsString</span><span class="sxs-lookup"><span data-stu-id="5e95f-624">IsString</span></span>
<span data-ttu-id="5e95f-625">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-625">**Description:**</span></span>  
<span data-ttu-id="5e95f-626">Se l'espressione hello può essere valutata tooa tipo stringa, quindi funzione IsString hello valuta tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5e95f-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="5e95f-627">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="5e95f-628">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-628">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-629">Utilizzare toodetermine se CStr () può essere espressione hello tooparse ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="5e95f-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="5e95f-630">IsPresent</span></span>
<span data-ttu-id="5e95f-631">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-631">**Description:**</span></span>  
<span data-ttu-id="5e95f-632">Se hello espressione stringa tooa che non è Null e non è vuoto, quindi hello IsPresent restituisce true.</span><span class="sxs-lookup"><span data-stu-id="5e95f-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="5e95f-633">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="5e95f-634">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-634">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-635">funzione inversa di Hello di questa funzione è denominata IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="5e95f-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="5e95f-636">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="5e95f-637">Elemento</span><span class="sxs-lookup"><span data-stu-id="5e95f-637">Item</span></span>
<span data-ttu-id="5e95f-638">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-638">**Description:**</span></span>  
<span data-ttu-id="5e95f-639">Hello funzione Item restituisce un elemento da una stringa o un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="5e95f-640">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="5e95f-641">attribute: attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-642">indice: elemento tooan indice stringa multivalore hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="5e95f-643">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-643">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-644">Hello funzione Item è utile insieme hello funzione Contains perché hello quest'ultima restituisce l'elemento tooan hello indice nell'attributo multivalore hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="5e95f-645">Genera un errore se l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="5e95f-646">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="5e95f-647">Restituisce hello indirizzo di posta elettronica primario.</span><span class="sxs-lookup"><span data-stu-id="5e95f-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="5e95f-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="5e95f-648">ItemOrNull</span></span>
<span data-ttu-id="5e95f-649">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-649">**Description:**</span></span>  
<span data-ttu-id="5e95f-650">Hello funzione ItemOrNull restituisce un elemento da una stringa o un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="5e95f-651">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="5e95f-652">attribute: attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="5e95f-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-653">indice: elemento tooan indice stringa multivalore hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="5e95f-654">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-654">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-655">funzione ItemOrNull Hello è utile insieme hello funzione Contains perché hello quest'ultima restituisce l'elemento tooan hello indice nell'attributo multivalore hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="5e95f-656">Se l'indice non è compreso nell'intervallo, restituisce un valore Null.</span><span class="sxs-lookup"><span data-stu-id="5e95f-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="5e95f-657">Join</span><span class="sxs-lookup"><span data-stu-id="5e95f-657">Join</span></span>
<span data-ttu-id="5e95f-658">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-658">**Description:**</span></span>  
<span data-ttu-id="5e95f-659">funzione Join Hello accetta una stringa multivalore e restituisce una stringa a valore singolo con il separatore specificato inserito tra ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="5e95f-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="5e95f-660">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="5e95f-661">attributo: attributo multivalore contenente stringhe toobe unita in join.</span><span class="sxs-lookup"><span data-stu-id="5e95f-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="5e95f-662">delimitatore: qualsiasi stringa, tooseparate utilizzati hello sottostringhe hello ha restituito una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="5e95f-663">Se omesso, hello carattere spazio ("") viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="5e95f-664">Se Delimiter è una stringa di lunghezza zero ("") o Nothing, tutti gli elementi nell'elenco di hello vengono concatenati senza delimitatori.</span><span class="sxs-lookup"><span data-stu-id="5e95f-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="5e95f-665">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="5e95f-665">**Remarks**</span></span>  
<span data-ttu-id="5e95f-666">Vi è parità tra hello Join e le funzioni di divisione.</span><span class="sxs-lookup"><span data-stu-id="5e95f-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="5e95f-667">Hello funzione Join accetta una matrice di stringhe e le unisce con una stringa di delimitazione tooreturn un'unica stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="5e95f-668">Hello funzione Split accetta una stringa e la separa in corrispondenza delimitatore hello, tooreturn una matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="5e95f-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="5e95f-669">Tuttavia, la differenza principale consiste nel fatto che Join può concatenare stringhe con qualsiasi stringa delimitatore, mentre Split può separare stringhe usando unicamente un delimitatore di un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="5e95f-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="5e95f-670">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="5e95f-671">Può restituire: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5e95f-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="5e95f-672">LCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-672">LCase</span></span>
<span data-ttu-id="5e95f-673">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-673">**Description:**</span></span>  
<span data-ttu-id="5e95f-674">Hello funzione LCase converte tutti i caratteri in una stringa toolower maiuscole.</span><span class="sxs-lookup"><span data-stu-id="5e95f-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="5e95f-675">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="5e95f-676">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="5e95f-677">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="5e95f-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="5e95f-678">Left</span><span class="sxs-lookup"><span data-stu-id="5e95f-678">Left</span></span>
<span data-ttu-id="5e95f-679">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-679">**Description:**</span></span>  
<span data-ttu-id="5e95f-680">funzione Left Hello restituisce un numero specificato di caratteri da sinistra hello di una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="5e95f-681">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="5e95f-682">stringa: hello tooreturn caratteri della stringa da</span><span class="sxs-lookup"><span data-stu-id="5e95f-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="5e95f-683">NumChars: un numero che identifica il numero di hello di tooreturn caratteri dall'inizio di hello (sinistra) della stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="5e95f-684">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-684">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-685">Stringa contenente i primi caratteri numChars hello nella stringa:</span><span class="sxs-lookup"><span data-stu-id="5e95f-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="5e95f-686">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5e95f-687">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="5e95f-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5e95f-688">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-688">If string is null, return empty string.</span></span>

<span data-ttu-id="5e95f-689">Se string contiene un minor numero di caratteri hello numero specificato in numChars, viene restituito un toostring identici stringa (che è, contenente tutti i caratteri nel parametro 1).</span><span class="sxs-lookup"><span data-stu-id="5e95f-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="5e95f-690">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="5e95f-691">Restituisce "Joh".</span><span class="sxs-lookup"><span data-stu-id="5e95f-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="5e95f-692">Len</span><span class="sxs-lookup"><span data-stu-id="5e95f-692">Len</span></span>
<span data-ttu-id="5e95f-693">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-693">**Description:**</span></span>  
<span data-ttu-id="5e95f-694">Hello funzione Len restituisce numero di caratteri in una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="5e95f-695">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="5e95f-696">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="5e95f-697">Restituisce 8</span><span class="sxs-lookup"><span data-stu-id="5e95f-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="5e95f-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="5e95f-698">LTrim</span></span>
<span data-ttu-id="5e95f-699">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-699">**Description:**</span></span>  
<span data-ttu-id="5e95f-700">Hello funzione LTrim rimuove gli spazi vuoti iniziali da una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="5e95f-701">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="5e95f-702">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="5e95f-703">Restituisce "Test"</span><span class="sxs-lookup"><span data-stu-id="5e95f-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="5e95f-704">Mid</span><span class="sxs-lookup"><span data-stu-id="5e95f-704">Mid</span></span>
<span data-ttu-id="5e95f-705">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-705">**Description:**</span></span>  
<span data-ttu-id="5e95f-706">Hello Mid restituisce un numero specificato di caratteri da una posizione specificata in una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="5e95f-707">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="5e95f-708">stringa: hello tooreturn caratteri della stringa da</span><span class="sxs-lookup"><span data-stu-id="5e95f-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="5e95f-709">Start: numero che identifica hello in caratteri della stringa tooreturn dalla posizione iniziale</span><span class="sxs-lookup"><span data-stu-id="5e95f-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="5e95f-710">NumChars: un numero che identifica il numero di hello di tooreturn caratteri dalla posizione nella stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="5e95f-711">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-711">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-712">Restituisce i caratteri in numChars a partire dalla posizione start nella stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="5e95f-713">Stringa contenente i caratteri specificati in numChars a partire dalla posizione start nella stringa:</span><span class="sxs-lookup"><span data-stu-id="5e95f-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="5e95f-714">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5e95f-715">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="5e95f-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5e95f-716">Se start > hello lunghezza della stringa, per restituire una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="5e95f-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="5e95f-717">Se start <= 0, restituisce la stringa di input.</span><span class="sxs-lookup"><span data-stu-id="5e95f-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="5e95f-718">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-718">If string is null, return empty string.</span></span>

<span data-ttu-id="5e95f-719">Se nella stringa non ci sono caratteri numChar rimanenti dalla posizione start, vengono restituiti quanti più caratteri possibile.</span><span class="sxs-lookup"><span data-stu-id="5e95f-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="5e95f-720">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="5e95f-721">Restituisce "hn Do".</span><span class="sxs-lookup"><span data-stu-id="5e95f-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="5e95f-722">Restituisce "Doe"</span><span class="sxs-lookup"><span data-stu-id="5e95f-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="5e95f-723">Now</span><span class="sxs-lookup"><span data-stu-id="5e95f-723">Now</span></span>
<span data-ttu-id="5e95f-724">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-724">**Description:**</span></span>  
<span data-ttu-id="5e95f-725">Hello ora funzione restituisce un valore DateTime specificando hello data corrente e l'ora, in base tooyour data di sistema del computer e l'ora.</span><span class="sxs-lookup"><span data-stu-id="5e95f-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="5e95f-726">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="5e95f-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="5e95f-727">NumFromDate</span></span>
<span data-ttu-id="5e95f-728">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-728">**Description:**</span></span>  
<span data-ttu-id="5e95f-729">Hello funzione NumFromDate restituisce una data nel formato di data dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="5e95f-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="5e95f-730">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="5e95f-731">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="5e95f-732">Restituisce 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="5e95f-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="5e95f-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="5e95f-733">PadLeft</span></span>
<span data-ttu-id="5e95f-734">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-734">**Description:**</span></span>  
<span data-ttu-id="5e95f-735">Hello PadLeft funzione sinistra Pad tooa una stringa specificata lunghezza utilizzando un carattere di riempimento specificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="5e95f-736">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="5e95f-737">stringa: hello toopad stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-737">string: hello string toopad.</span></span>
* <span data-ttu-id="5e95f-738">lunghezza: valore intero che rappresenta hello desiderato lunghezza della stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="5e95f-739">padCharacter: stringa costituita da un singolo carattere toouse come carattere di riempimento hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="5e95f-740">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-740">**Remarks:**</span></span>

* <span data-ttu-id="5e95f-741">Se hello lunghezza della stringa è minore della lunghezza, padCharacter viene aggiunto ripetutamente toohello inizio (sinistra) della stringa fino a quando non ha un toolength di uguale lunghezza.</span><span class="sxs-lookup"><span data-stu-id="5e95f-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="5e95f-742">PadCharacter può essere uno spazio, ma non un valore null.</span><span class="sxs-lookup"><span data-stu-id="5e95f-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="5e95f-743">Se la lunghezza hello della stringa è uguale tooor maggiore lunghezza, stringa viene restituita invariata.</span><span class="sxs-lookup"><span data-stu-id="5e95f-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="5e95f-744">Se string ha una lunghezza maggiore di o uguale toolength, viene restituito un toostring identiche di stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="5e95f-745">Se la lunghezza hello della stringa è minore della lunghezza, una nuova stringa di hello desiderato lunghezza viene restituita contenente string con l'aggiunta di padCharacter.</span><span class="sxs-lookup"><span data-stu-id="5e95f-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="5e95f-746">Se string è null, la funzione hello restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="5e95f-747">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="5e95f-748">Restituisce "000000User".</span><span class="sxs-lookup"><span data-stu-id="5e95f-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="5e95f-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="5e95f-749">PadRight</span></span>
<span data-ttu-id="5e95f-750">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-750">**Description:**</span></span>  
<span data-ttu-id="5e95f-751">Hello PadRight funzione destra riempie tooa una stringa specificata lunghezza utilizzando un carattere di riempimento specificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="5e95f-752">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="5e95f-753">stringa: hello toopad stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-753">string: hello string toopad.</span></span>
* <span data-ttu-id="5e95f-754">lunghezza: valore intero che rappresenta hello desiderato lunghezza della stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="5e95f-755">padCharacter: stringa costituita da un singolo carattere toouse come carattere di riempimento hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="5e95f-756">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-756">**Remarks:**</span></span>

* <span data-ttu-id="5e95f-757">Se hello lunghezza della stringa è minore della lunghezza, padCharacter viene aggiunto ripetutamente toohello fine (destra) della stringa fino a quando non ha un toolength di uguale lunghezza.</span><span class="sxs-lookup"><span data-stu-id="5e95f-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="5e95f-758">PadCharacter può essere uno spazio, ma non un valore null.</span><span class="sxs-lookup"><span data-stu-id="5e95f-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="5e95f-759">Se la lunghezza hello della stringa è uguale tooor maggiore lunghezza, stringa viene restituita invariata.</span><span class="sxs-lookup"><span data-stu-id="5e95f-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="5e95f-760">Se string ha una lunghezza maggiore di o uguale toolength, viene restituito un toostring identiche di stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="5e95f-761">Se la lunghezza hello della stringa è minore della lunghezza, una nuova stringa di hello desiderato lunghezza viene restituita contenente string con l'aggiunta di padCharacter.</span><span class="sxs-lookup"><span data-stu-id="5e95f-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="5e95f-762">Se string è null, la funzione hello restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="5e95f-763">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="5e95f-764">Restituisce "User000000".</span><span class="sxs-lookup"><span data-stu-id="5e95f-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="5e95f-765">PCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-765">PCase</span></span>
<span data-ttu-id="5e95f-766">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-766">**Description:**</span></span>  
<span data-ttu-id="5e95f-767">Hello funzione PCase converte hello primo carattere di ogni parola delimitato da spazi in un caso tooupper stringa e tutti gli altri caratteri vengono convertiti toolower case.</span><span class="sxs-lookup"><span data-stu-id="5e95f-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="5e95f-768">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="5e95f-769">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-769">**Remarks:**</span></span>

* <span data-ttu-id="5e95f-770">Questa funzione non fornisce attualmente tooconvert di maiuscole e minuscole appropriata una parola interamente in maiuscolo, ad esempio un acronimo.</span><span class="sxs-lookup"><span data-stu-id="5e95f-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="5e95f-771">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="5e95f-772">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="5e95f-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="5e95f-773">Restituisce "Test"</span><span class="sxs-lookup"><span data-stu-id="5e95f-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="5e95f-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="5e95f-774">RandomNum</span></span>
<span data-ttu-id="5e95f-775">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-775">**Description:**</span></span>  
<span data-ttu-id="5e95f-776">Hello funzione RandomNum restituisce un numero casuale tra un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="5e95f-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="5e95f-777">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="5e95f-778">Start: un numero identificativo hello limite inferiore di hello valore casuale toogenerate</span><span class="sxs-lookup"><span data-stu-id="5e95f-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="5e95f-779">fine: un numero identificativo hello limite massimo di hello valore casuale toogenerate</span><span class="sxs-lookup"><span data-stu-id="5e95f-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="5e95f-780">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="5e95f-781">Può restituire 734.</span><span class="sxs-lookup"><span data-stu-id="5e95f-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="5e95f-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="5e95f-782">RemoveDuplicates</span></span>
<span data-ttu-id="5e95f-783">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-783">**Description:**</span></span>  
<span data-ttu-id="5e95f-784">Hello funzione RemoveDuplicates accetta una stringa multivalore e assicurarsi che ogni valore univoco.</span><span class="sxs-lookup"><span data-stu-id="5e95f-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="5e95f-785">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="5e95f-786">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="5e95f-787">Restituisce un attributo proxyAddress purificato in cui sono stati rimossi tutti i valori duplicati.</span><span class="sxs-lookup"><span data-stu-id="5e95f-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="5e95f-788">Replace</span><span class="sxs-lookup"><span data-stu-id="5e95f-788">Replace</span></span>
<span data-ttu-id="5e95f-789">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-789">**Description:**</span></span>  
<span data-ttu-id="5e95f-790">Hello funzione Replace sostituisce tutte le occorrenze di una stringa tooanother stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="5e95f-791">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="5e95f-792">stringa: tooreplace una stringa i valori.</span><span class="sxs-lookup"><span data-stu-id="5e95f-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="5e95f-793">OldValue: hello stringa toosearch per e tooreplace.</span><span class="sxs-lookup"><span data-stu-id="5e95f-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="5e95f-794">NewValue: hello stringa tooreplace per.</span><span class="sxs-lookup"><span data-stu-id="5e95f-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="5e95f-795">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-795">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-796">funzione Hello riconosce hello moniker speciali seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e95f-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="5e95f-797">\n - Nuova riga</span><span class="sxs-lookup"><span data-stu-id="5e95f-797">\n – New Line</span></span>
* <span data-ttu-id="5e95f-798">\r - Ritorno a capo</span><span class="sxs-lookup"><span data-stu-id="5e95f-798">\r – Carriage Return</span></span>
* <span data-ttu-id="5e95f-799">\t - Tabulazione</span><span class="sxs-lookup"><span data-stu-id="5e95f-799">\t – Tab</span></span>

<span data-ttu-id="5e95f-800">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="5e95f-801">Sostituisce CRLF con una virgola e uno spazio e provocare troppo "Uno Microsoft modo, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="5e95f-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="5e95f-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="5e95f-802">ReplaceChars</span></span>
<span data-ttu-id="5e95f-803">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-803">**Description:**</span></span>  
<span data-ttu-id="5e95f-804">Hello funzione ReplaceChars sostituisce tutte le occorrenze dei caratteri trovati nella stringa ReplacePattern hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="5e95f-805">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="5e95f-806">stringa: tooreplace una stringa di caratteri.</span><span class="sxs-lookup"><span data-stu-id="5e95f-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="5e95f-807">ReplacePattern: una stringa contenente un dizionario con tooreplace caratteri.</span><span class="sxs-lookup"><span data-stu-id="5e95f-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="5e95f-808">formato hello è {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} in cui origine è hello carattere toofind e destinazione hello stringa tooreplace con.</span><span class="sxs-lookup"><span data-stu-id="5e95f-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="5e95f-809">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-809">**Remarks:**</span></span>

* <span data-ttu-id="5e95f-810">funzione Hello accetta ogni occorrenza dei valori Source definiti e li sostituisce con destinazioni hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="5e95f-811">origine Hello deve essere esattamente un carattere (unicode).</span><span class="sxs-lookup"><span data-stu-id="5e95f-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="5e95f-812">Hello origine non può essere vuoto o più di un carattere (errore di analisi).</span><span class="sxs-lookup"><span data-stu-id="5e95f-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="5e95f-813">destinazione Hello può contenere più caratteri, ad esempio ö: OE, β: ss.</span><span class="sxs-lookup"><span data-stu-id="5e95f-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="5e95f-814">destinazione Hello può essere vuoto che indica che il carattere di hello deve essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="5e95f-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="5e95f-815">origine Hello tra maiuscole e minuscole e deve essere una corrispondenza esatta.</span><span class="sxs-lookup"><span data-stu-id="5e95f-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="5e95f-816">Hello, (virgola) e: (due punti) sono riservati e non può essere sostituito con questa funzione.</span><span class="sxs-lookup"><span data-stu-id="5e95f-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="5e95f-817">Gli spazi e altri caratteri vuoti nella stringa ReplacePattern hello vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="5e95f-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="5e95f-818">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="5e95f-819">Restituisce Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="5e95f-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="5e95f-820">Restituisce "ONeil", singolo tick hello è definito toobe rimosso.</span><span class="sxs-lookup"><span data-stu-id="5e95f-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="5e95f-821">Right</span><span class="sxs-lookup"><span data-stu-id="5e95f-821">Right</span></span>
<span data-ttu-id="5e95f-822">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-822">**Description:**</span></span>  
<span data-ttu-id="5e95f-823">funzione Right Hello restituisce un numero specificato di caratteri da hello destra (fine) di una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="5e95f-824">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="5e95f-825">stringa: hello tooreturn caratteri della stringa da</span><span class="sxs-lookup"><span data-stu-id="5e95f-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="5e95f-826">NumChars: un numero che identifica il numero di hello di tooreturn caratteri dalla fine di hello (destra) della stringa</span><span class="sxs-lookup"><span data-stu-id="5e95f-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="5e95f-827">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-827">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-828">Caratteri NumChars vengono restituiti dall'ultima posizione di hello della stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="5e95f-829">Stringa contenente hello ultimi caratteri numChars in string:</span><span class="sxs-lookup"><span data-stu-id="5e95f-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="5e95f-830">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5e95f-831">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="5e95f-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5e95f-832">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-832">If string is null, return empty string.</span></span>

<span data-ttu-id="5e95f-833">Se string contiene un numero di caratteri inferiore a hello numero specificato in NumChars, viene restituito un toostring identiche di stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="5e95f-834">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="5e95f-835">Restituisce "Doe".</span><span class="sxs-lookup"><span data-stu-id="5e95f-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="5e95f-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="5e95f-836">RTrim</span></span>
<span data-ttu-id="5e95f-837">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-837">**Description:**</span></span>  
<span data-ttu-id="5e95f-838">Hello funzione RTrim rimuove gli spazi vuoti finali da una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="5e95f-839">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="5e95f-840">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="5e95f-841">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="5e95f-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="5e95f-842">Selezionare</span><span class="sxs-lookup"><span data-stu-id="5e95f-842">Select</span></span>
<span data-ttu-id="5e95f-843">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-843">**Description:**</span></span>  
<span data-ttu-id="5e95f-844">Elabora tutti i valori in un attributo multivalore, o nell'output di un'espressione, in base alla funzione specificata.</span><span class="sxs-lookup"><span data-stu-id="5e95f-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="5e95f-845">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="5e95f-846">elemento: rappresenta un elemento nell'attributo multivalore hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-847">attributo: attributo multivalore hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-848">expression: un'espressione che restituisce una raccolta di valori</span><span class="sxs-lookup"><span data-stu-id="5e95f-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="5e95f-849">condizione: qualsiasi funzione in grado di elaborare un elemento nell'attributo hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="5e95f-850">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="5e95f-851">Restituire tutti i valori hello in telefono di un attributo multivalore hello dopo avere rimosso trattini (-).</span><span class="sxs-lookup"><span data-stu-id="5e95f-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="5e95f-852">Split</span><span class="sxs-lookup"><span data-stu-id="5e95f-852">Split</span></span>
<span data-ttu-id="5e95f-853">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-853">**Description:**</span></span>  
<span data-ttu-id="5e95f-854">Hello funzione Split accetta una stringa separata dal delimitatore e lo rende una stringa multivalore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="5e95f-855">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="5e95f-856">valore: hello stringa con un tooseparate carattere delimitatore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="5e95f-857">delimitatore: single toobe di carattere utilizzato come delimitatore di hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="5e95f-858">limit: numero massimo di valori che saranno restituiti.</span><span class="sxs-lookup"><span data-stu-id="5e95f-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="5e95f-859">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="5e95f-860">Restituisce una stringa multivalore con 2 elementi utili per l'attributo proxyAddress hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="5e95f-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="5e95f-861">StringFromGuid</span></span>
<span data-ttu-id="5e95f-862">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-862">**Description:**</span></span>  
<span data-ttu-id="5e95f-863">Hello funzione StringFromGuid accetta un GUID binario e lo converte in stringa tooa</span><span class="sxs-lookup"><span data-stu-id="5e95f-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="5e95f-864">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="5e95f-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="5e95f-865">StringFromSid</span></span>
<span data-ttu-id="5e95f-866">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-866">**Description:**</span></span>  
<span data-ttu-id="5e95f-867">Hello funzione StringFromSid converte una matrice di byte contenente una stringa tooa identificatore di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5e95f-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="5e95f-868">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="5e95f-869">Switch</span><span class="sxs-lookup"><span data-stu-id="5e95f-869">Switch</span></span>
<span data-ttu-id="5e95f-870">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-870">**Description:**</span></span>  
<span data-ttu-id="5e95f-871">funzione Switch Hello è tooreturn utilizzato un singolo valore in base a condizioni valutate.</span><span class="sxs-lookup"><span data-stu-id="5e95f-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="5e95f-872">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="5e95f-873">Expr: espressione Variant da tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="5e95f-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="5e95f-874">valore: toobe valore restituito se l'espressione corrispondente hello è True.</span><span class="sxs-lookup"><span data-stu-id="5e95f-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="5e95f-875">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-875">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-876">argomento della funzione Switch elenco è costituito da coppie di espressioni e valori Hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="5e95f-877">Hello espressioni vengono valutate da sinistra tooright e viene restituito il valore di hello associato hello prima espressione tooevaluate tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5e95f-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="5e95f-878">Se non vengono accoppiate correttamente parti hello, si verifica un errore di run-time.</span><span class="sxs-lookup"><span data-stu-id="5e95f-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="5e95f-879">Ad esempio, se expr1 è True, Switch restituisce value1.</span><span class="sxs-lookup"><span data-stu-id="5e95f-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="5e95f-880">Se expr-1 è False, ma expr-2 è True, Switch restituisce value-2 e così via.</span><span class="sxs-lookup"><span data-stu-id="5e95f-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="5e95f-881">Switch restituisce Nothing se:</span><span class="sxs-lookup"><span data-stu-id="5e95f-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="5e95f-882">Nessuna delle espressioni di hello è True.</span><span class="sxs-lookup"><span data-stu-id="5e95f-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="5e95f-883">prima espressione True Hello ha un valore corrispondente è Null.</span><span class="sxs-lookup"><span data-stu-id="5e95f-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="5e95f-884">Switch valuta tutte le espressioni, anche se ne restituisce una sola.</span><span class="sxs-lookup"><span data-stu-id="5e95f-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="5e95f-885">Per questo motivo, è opportuno considerare attentamente gli effetti collaterali indesiderati.</span><span class="sxs-lookup"><span data-stu-id="5e95f-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="5e95f-886">Ad esempio, se i risultati di valutazione di hello di un'espressione in una divisione per zero, si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="5e95f-887">Valore può essere anche funzione di errore hello, che restituisce una stringa personalizzata.</span><span class="sxs-lookup"><span data-stu-id="5e95f-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="5e95f-888">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="5e95f-889">Restituisce hello lingua parlata in alcune città importanti, in caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="5e95f-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="5e95f-890">Trim</span><span class="sxs-lookup"><span data-stu-id="5e95f-890">Trim</span></span>
<span data-ttu-id="5e95f-891">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-891">**Description:**</span></span>  
<span data-ttu-id="5e95f-892">funzione Trim Hello rimuove iniziali e finali di spazi da una stringa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="5e95f-893">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="5e95f-894">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="5e95f-895">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="5e95f-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="5e95f-896">Rimuove spazi per ogni valore nell'attributo proxyAddress hello iniziali e finali.</span><span class="sxs-lookup"><span data-stu-id="5e95f-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="5e95f-897">UCase</span><span class="sxs-lookup"><span data-stu-id="5e95f-897">UCase</span></span>
<span data-ttu-id="5e95f-898">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-898">**Description:**</span></span>  
<span data-ttu-id="5e95f-899">Hello funzione UCase converte tutti i caratteri in una stringa tooupper maiuscole.</span><span class="sxs-lookup"><span data-stu-id="5e95f-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="5e95f-900">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="5e95f-901">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="5e95f-902">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="5e95f-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="5e95f-903">Where</span><span class="sxs-lookup"><span data-stu-id="5e95f-903">Where</span></span>

<span data-ttu-id="5e95f-904">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-904">**Description:**</span></span>  
<span data-ttu-id="5e95f-905">Restituisce un subset di valori di un attributo multivalore, o dell'output di un'espressione, in base alla condizione specifica.</span><span class="sxs-lookup"><span data-stu-id="5e95f-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="5e95f-906">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="5e95f-907">elemento: rappresenta un elemento nell'attributo multivalore hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-908">attributo: attributo multivalore hello</span><span class="sxs-lookup"><span data-stu-id="5e95f-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="5e95f-909">condizione: qualsiasi espressione che può essere valutata tootrue o false</span><span class="sxs-lookup"><span data-stu-id="5e95f-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="5e95f-910">expression: un'espressione che restituisce una raccolta di valori</span><span class="sxs-lookup"><span data-stu-id="5e95f-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="5e95f-911">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="5e95f-912">Restituire i valori del certificato hello in hello userCertificate di un attributo multivalore che non sono scaduti.</span><span class="sxs-lookup"><span data-stu-id="5e95f-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="5e95f-913">With</span><span class="sxs-lookup"><span data-stu-id="5e95f-913">With</span></span>
<span data-ttu-id="5e95f-914">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-914">**Description:**</span></span>  
<span data-ttu-id="5e95f-915">Hello con funzione fornisce un toosimplify modo un'espressione complessa utilizzando una variabile toorepresent una sottoespressione che viene visualizzato uno o più volte nell'espressione complessa hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="5e95f-916">**Sintassi**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="5e95f-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="5e95f-917">variabile: rappresenta hello sottoespressione.</span><span class="sxs-lookup"><span data-stu-id="5e95f-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="5e95f-918">subExpression: sottoespressione rappresentata dalla variabile.</span><span class="sxs-lookup"><span data-stu-id="5e95f-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="5e95f-919">complexExpression: un'espressione complessa.</span><span class="sxs-lookup"><span data-stu-id="5e95f-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="5e95f-920">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="5e95f-921">Dal punto di vista funzionale equivale a:</span><span class="sxs-lookup"><span data-stu-id="5e95f-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="5e95f-922">Che restituisce solo i valori del certificato non scadute nell'attributo userCertificate hello.</span><span class="sxs-lookup"><span data-stu-id="5e95f-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="5e95f-923">Word</span><span class="sxs-lookup"><span data-stu-id="5e95f-923">Word</span></span>
<span data-ttu-id="5e95f-924">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-924">**Description:**</span></span>  
<span data-ttu-id="5e95f-925">Hello funzione Word restituisce una parola contenuta in una stringa, in base ai parametri che descrivono toouse delimitatori hello e hello word numero tooreturn.</span><span class="sxs-lookup"><span data-stu-id="5e95f-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="5e95f-926">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="5e95f-927">stringa: hello tooreturn di stringa di una parola.</span><span class="sxs-lookup"><span data-stu-id="5e95f-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="5e95f-928">WordNumber: numero che identifica il numero di parole da restituire.</span><span class="sxs-lookup"><span data-stu-id="5e95f-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="5e95f-929">delimitatori: una stringa che rappresenta hello/i delimitatore / deve essere utilizzato tooidentify parole</span><span class="sxs-lookup"><span data-stu-id="5e95f-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="5e95f-930">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-930">**Remarks:**</span></span>  
<span data-ttu-id="5e95f-931">Ogni stringa di caratteri nella stringa separati da hello uno dei caratteri hello delimitatori vengono identificati come parole:</span><span class="sxs-lookup"><span data-stu-id="5e95f-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="5e95f-932">Se number è < 1, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="5e95f-933">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="5e95f-934">Se la stringa contiene meno delle parole specificate in number o se non contiene alcuna parola identificata da delimiters, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="5e95f-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="5e95f-935">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="5e95f-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="5e95f-936">Restituisce "brown"</span><span class="sxs-lookup"><span data-stu-id="5e95f-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="5e95f-937">Restituisce "has"</span><span class="sxs-lookup"><span data-stu-id="5e95f-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5e95f-938">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5e95f-938">Additional Resources</span></span>
* [<span data-ttu-id="5e95f-939">Informazioni sulle espressioni di provisioning dichiarativo</span><span class="sxs-lookup"><span data-stu-id="5e95f-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="5e95f-940">Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="5e95f-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="5e95f-941">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e95f-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
