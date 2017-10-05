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
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="308f6-103">Servizio di sincronizzazione Azure AD Connect: Riferimento alle funzioni</span><span class="sxs-lookup"><span data-stu-id="308f6-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="308f6-104">In Azure AD Connect le funzioni vengono usate per modificare il valore di un attributo durante la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="308f6-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="308f6-105">La sintassi delle funzioni viene espressa nel formato seguente: </span><span class="sxs-lookup"><span data-stu-id="308f6-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="308f6-106">Se una funzione è in overload e accetta più sintassi, verranno elencate tutte quelle valide.</span><span class="sxs-lookup"><span data-stu-id="308f6-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="308f6-107">Le funzioni sono fortemente tipizzate e verificano che il tipo passato corrisponda al tipo documentato.</span><span class="sxs-lookup"><span data-stu-id="308f6-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="308f6-108">Se il tipo non corrisponde, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="308f6-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="308f6-109">I tipi vengono espressi con la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="308f6-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="308f6-110">**bin** : binario</span><span class="sxs-lookup"><span data-stu-id="308f6-110">**bin** – Binary</span></span>
* <span data-ttu-id="308f6-111">**bool** : booleano</span><span class="sxs-lookup"><span data-stu-id="308f6-111">**bool** – Boolean</span></span>
* <span data-ttu-id="308f6-112">**dt** : data/ora UTC</span><span class="sxs-lookup"><span data-stu-id="308f6-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="308f6-113">**enum** : enumerazione di costanti note</span><span class="sxs-lookup"><span data-stu-id="308f6-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="308f6-114">**exp** : espressione per cui è prevista la restituzione di un valore booleano</span><span class="sxs-lookup"><span data-stu-id="308f6-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="308f6-115">**mvbin** : binario multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="308f6-116">**mvstr** : stringa multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="308f6-117">**mvref** : riferimento multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="308f6-118">**num** : numerico</span><span class="sxs-lookup"><span data-stu-id="308f6-118">**num** – Numeric</span></span>
* <span data-ttu-id="308f6-119">**ref** : riferimento</span><span class="sxs-lookup"><span data-stu-id="308f6-119">**ref** – Reference</span></span>
* <span data-ttu-id="308f6-120">**str** : stringa</span><span class="sxs-lookup"><span data-stu-id="308f6-120">**str** – String</span></span>
* <span data-ttu-id="308f6-121">**var** : variante di (quasi) tutti gli altri tipi</span><span class="sxs-lookup"><span data-stu-id="308f6-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="308f6-122">**void** : non restituisce un valore</span><span class="sxs-lookup"><span data-stu-id="308f6-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="308f6-123">Le funzioni con i tipi **mvbin**, **mvstr** e **mvref** possono operare solo con gli attributi multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="308f6-124">Le funzioni con **bin**, **str** e **ref** operano con gli attributi a valore singolo e multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="308f6-125">Riferimento alle funzioni</span><span class="sxs-lookup"><span data-stu-id="308f6-125">Functions Reference</span></span>
| <span data-ttu-id="308f6-126">Elenco di funzioni</span><span class="sxs-lookup"><span data-stu-id="308f6-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="308f6-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="308f6-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="308f6-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="308f6-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="308f6-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="308f6-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="308f6-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="308f6-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="308f6-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="308f6-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="308f6-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="308f6-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="308f6-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="308f6-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="308f6-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="308f6-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="308f6-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="308f6-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="308f6-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="308f6-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="308f6-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="308f6-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="308f6-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="308f6-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="308f6-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="308f6-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="308f6-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="308f6-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="308f6-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="308f6-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="308f6-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="308f6-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="308f6-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="308f6-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="308f6-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="308f6-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="308f6-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="308f6-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="308f6-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="308f6-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="308f6-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="308f6-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="308f6-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="308f6-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="308f6-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="308f6-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="308f6-150">**Conversione**</span><span class="sxs-lookup"><span data-stu-id="308f6-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="308f6-151">CBool</span><span class="sxs-lookup"><span data-stu-id="308f6-151">CBool</span></span>](#cbool) |[<span data-ttu-id="308f6-152">CDate</span><span class="sxs-lookup"><span data-stu-id="308f6-152">CDate</span></span>](#cdate) |[<span data-ttu-id="308f6-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="308f6-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="308f6-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="308f6-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="308f6-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="308f6-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="308f6-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="308f6-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="308f6-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="308f6-158">CNum</span><span class="sxs-lookup"><span data-stu-id="308f6-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="308f6-159">CRef</span><span class="sxs-lookup"><span data-stu-id="308f6-159">CRef</span></span>](#cref) |[<span data-ttu-id="308f6-160">CStr</span><span class="sxs-lookup"><span data-stu-id="308f6-160">CStr</span></span>](#cstr) |[<span data-ttu-id="308f6-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="308f6-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="308f6-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="308f6-163">**Data/Ora**</span><span class="sxs-lookup"><span data-stu-id="308f6-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="308f6-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="308f6-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="308f6-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="308f6-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="308f6-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="308f6-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="308f6-167">Now</span><span class="sxs-lookup"><span data-stu-id="308f6-167">Now</span></span>](#now) | |
| [<span data-ttu-id="308f6-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="308f6-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="308f6-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="308f6-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="308f6-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="308f6-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="308f6-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="308f6-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="308f6-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="308f6-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="308f6-173">**Versione di valutazione**</span><span class="sxs-lookup"><span data-stu-id="308f6-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="308f6-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="308f6-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="308f6-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="308f6-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="308f6-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="308f6-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="308f6-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="308f6-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="308f6-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="308f6-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="308f6-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="308f6-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="308f6-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="308f6-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="308f6-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="308f6-182">IsString</span><span class="sxs-lookup"><span data-stu-id="308f6-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="308f6-183">**Matematiche**</span><span class="sxs-lookup"><span data-stu-id="308f6-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="308f6-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="308f6-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="308f6-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="308f6-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="308f6-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="308f6-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="308f6-187">**A più valori**</span><span class="sxs-lookup"><span data-stu-id="308f6-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="308f6-188">Contiene</span><span class="sxs-lookup"><span data-stu-id="308f6-188">Contains</span></span>](#contains) |[<span data-ttu-id="308f6-189">Numero</span><span class="sxs-lookup"><span data-stu-id="308f6-189">Count</span></span>](#count) |[<span data-ttu-id="308f6-190">Elemento</span><span class="sxs-lookup"><span data-stu-id="308f6-190">Item</span></span>](#item) |[<span data-ttu-id="308f6-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="308f6-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="308f6-192">Join</span><span class="sxs-lookup"><span data-stu-id="308f6-192">Join</span></span>](#join) |[<span data-ttu-id="308f6-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="308f6-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="308f6-194">Split</span><span class="sxs-lookup"><span data-stu-id="308f6-194">Split</span></span>](#split) | | |
| <span data-ttu-id="308f6-195">**Flusso del programma**</span><span class="sxs-lookup"><span data-stu-id="308f6-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="308f6-196">Errore</span><span class="sxs-lookup"><span data-stu-id="308f6-196">Error</span></span>](#error) |[<span data-ttu-id="308f6-197">IIF</span><span class="sxs-lookup"><span data-stu-id="308f6-197">IIF</span></span>](#iif) |[<span data-ttu-id="308f6-198">Selezionare</span><span class="sxs-lookup"><span data-stu-id="308f6-198">Select</span></span>](#select) |[<span data-ttu-id="308f6-199">Switch</span><span class="sxs-lookup"><span data-stu-id="308f6-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="308f6-200">Dove</span><span class="sxs-lookup"><span data-stu-id="308f6-200">Where</span></span>](#where) |[<span data-ttu-id="308f6-201">With</span><span class="sxs-lookup"><span data-stu-id="308f6-201">With</span></span>](#with) | | | |
| <span data-ttu-id="308f6-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="308f6-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="308f6-203">GUID</span><span class="sxs-lookup"><span data-stu-id="308f6-203">GUID</span></span>](#guid) |[<span data-ttu-id="308f6-204">InStr</span><span class="sxs-lookup"><span data-stu-id="308f6-204">InStr</span></span>](#instr) |[<span data-ttu-id="308f6-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="308f6-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="308f6-206">LCase</span><span class="sxs-lookup"><span data-stu-id="308f6-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="308f6-207">Left</span><span class="sxs-lookup"><span data-stu-id="308f6-207">Left</span></span>](#left) |[<span data-ttu-id="308f6-208">Len</span><span class="sxs-lookup"><span data-stu-id="308f6-208">Len</span></span>](#len) |[<span data-ttu-id="308f6-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="308f6-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="308f6-210">Mid</span><span class="sxs-lookup"><span data-stu-id="308f6-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="308f6-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="308f6-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="308f6-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="308f6-212">PadRight</span></span>](#padright) |[<span data-ttu-id="308f6-213">PCase</span><span class="sxs-lookup"><span data-stu-id="308f6-213">PCase</span></span>](#pcase) |[<span data-ttu-id="308f6-214">Replace</span><span class="sxs-lookup"><span data-stu-id="308f6-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="308f6-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="308f6-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="308f6-216">Right</span><span class="sxs-lookup"><span data-stu-id="308f6-216">Right</span></span>](#right) |[<span data-ttu-id="308f6-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="308f6-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="308f6-218">Trim</span><span class="sxs-lookup"><span data-stu-id="308f6-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="308f6-219">UCase</span><span class="sxs-lookup"><span data-stu-id="308f6-219">UCase</span></span>](#ucase) |[<span data-ttu-id="308f6-220">Word</span><span class="sxs-lookup"><span data-stu-id="308f6-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="308f6-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="308f6-221">BitAnd</span></span>
<span data-ttu-id="308f6-222">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-222">**Description:**</span></span>  
<span data-ttu-id="308f6-223">La funzione BitAnd imposta i bit specificati su un valore.</span><span class="sxs-lookup"><span data-stu-id="308f6-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="308f6-224">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="308f6-225">value1, value2: valori numerici da unire con AND</span><span class="sxs-lookup"><span data-stu-id="308f6-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="308f6-226">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-226">**Remarks:**</span></span>  
<span data-ttu-id="308f6-227">Questa funzione converte entrambi i parametri nella rappresentazione binaria e imposta un bit su:</span><span class="sxs-lookup"><span data-stu-id="308f6-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="308f6-228">0: se il valore di uno o entrambi i bit corrispondenti nella *maschera* e nel *flag* sono pari a 0</span><span class="sxs-lookup"><span data-stu-id="308f6-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="308f6-229">1: se entrambi i bit corrispondenti sono pari a 1.</span><span class="sxs-lookup"><span data-stu-id="308f6-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="308f6-230">In altre parole, restituisce 0 in tutti i casi tranne quando i bit corrispondenti di entrambi i parametri sono pari a 1.</span><span class="sxs-lookup"><span data-stu-id="308f6-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="308f6-231">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="308f6-232">Restituisce 7 perché i valori esadecimali "F" E "F7" restituiscono questo valore.</span><span class="sxs-lookup"><span data-stu-id="308f6-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="308f6-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="308f6-233">BitOr</span></span>
<span data-ttu-id="308f6-234">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-234">**Description:**</span></span>  
<span data-ttu-id="308f6-235">La funzione BitOr imposta i bit specificati su un valore.</span><span class="sxs-lookup"><span data-stu-id="308f6-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="308f6-236">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="308f6-237">value1, value2: valori numerici da unire con OR</span><span class="sxs-lookup"><span data-stu-id="308f6-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="308f6-238">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-238">**Remarks:**</span></span>  
<span data-ttu-id="308f6-239">Questa funzione converte entrambi i parametri nella rappresentazione binaria e imposta un bit su 1 se il valore di uno o entrambi i bit corrispondenti nella maschera e nel flag è pari a 1 e su 0 se entrambi i bit corrispondenti sono pari a 0.</span><span class="sxs-lookup"><span data-stu-id="308f6-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="308f6-240">In altre parole, restituisce 1 in tutti i casi tranne dove i bit corrispondenti di entrambi i parametri sono pari a 0.</span><span class="sxs-lookup"><span data-stu-id="308f6-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="308f6-241">CBool</span><span class="sxs-lookup"><span data-stu-id="308f6-241">CBool</span></span>
<span data-ttu-id="308f6-242">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-242">**Description:**</span></span>  
<span data-ttu-id="308f6-243">La funzione CBool restituisce un valore booleano basato sull'espressione valutata.</span><span class="sxs-lookup"><span data-stu-id="308f6-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="308f6-244">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="308f6-245">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-245">**Remarks:**</span></span>  
<span data-ttu-id="308f6-246">Se l'espressione restituisce un valore diverso da zero, CBool restituisce True. In caso contrario restituisce False.</span><span class="sxs-lookup"><span data-stu-id="308f6-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="308f6-247">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="308f6-248">Restituisce True se entrambi gli attributi hanno lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="308f6-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="308f6-249">CDate</span><span class="sxs-lookup"><span data-stu-id="308f6-249">CDate</span></span>
<span data-ttu-id="308f6-250">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-250">**Description:**</span></span>  
<span data-ttu-id="308f6-251">La funzione CDate restituisce un valore di data/ora UTC da una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="308f6-252">DateTime non è un attributo nativo in Sync, ma viene usato da alcune funzioni.</span><span class="sxs-lookup"><span data-stu-id="308f6-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="308f6-253">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="308f6-254">Value: una stringa con una data, un'ora e facoltativamente un fuso orario</span><span class="sxs-lookup"><span data-stu-id="308f6-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="308f6-255">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-255">**Remarks:**</span></span>  
<span data-ttu-id="308f6-256">La stringa restituita è sempre espressa in UTC.</span><span class="sxs-lookup"><span data-stu-id="308f6-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="308f6-257">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="308f6-258">Restituisce un valore di data/ora basato sull'ora di inizio del dipendente</span><span class="sxs-lookup"><span data-stu-id="308f6-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="308f6-259">Restituisce un valore di data/ora che rappresenta "2013-01-11 12:00 AM"</span><span class="sxs-lookup"><span data-stu-id="308f6-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="308f6-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="308f6-260">CertExtensionOids</span></span>
<span data-ttu-id="308f6-261">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-261">**Description:**</span></span>  
<span data-ttu-id="308f6-262">Restituisce i valori Oid di tutte le estensioni critiche di un oggetto certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="308f6-263">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="308f6-264">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-265">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="308f6-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="308f6-266">CertFormat</span></span>
<span data-ttu-id="308f6-267">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-267">**Description:**</span></span>  
<span data-ttu-id="308f6-268">Restituisce il nome del formato di questo certificato X.509v3.</span><span class="sxs-lookup"><span data-stu-id="308f6-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="308f6-269">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="308f6-270">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-271">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="308f6-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="308f6-272">CertFriendlyName</span></span>
<span data-ttu-id="308f6-273">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-273">**Description:**</span></span>  
<span data-ttu-id="308f6-274">Restituisce l'alias associato per un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="308f6-275">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="308f6-276">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-277">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="308f6-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="308f6-278">CertHashString</span></span>
<span data-ttu-id="308f6-279">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-279">**Description:**</span></span>  
<span data-ttu-id="308f6-280">Restituisce il valore hash SHA1 per il certificato X.509v3 come stringa esadecimale.</span><span class="sxs-lookup"><span data-stu-id="308f6-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="308f6-281">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="308f6-282">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-283">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="308f6-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="308f6-284">CertIssuer</span></span>
<span data-ttu-id="308f6-285">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-285">**Description:**</span></span>  
<span data-ttu-id="308f6-286">Restituisce il nome dell'autorità di certificazione che ha emesso il certificato X.509v3.</span><span class="sxs-lookup"><span data-stu-id="308f6-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="308f6-287">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="308f6-288">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-289">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="308f6-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="308f6-290">CertIssuerDN</span></span>
<span data-ttu-id="308f6-291">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-291">**Description:**</span></span>  
<span data-ttu-id="308f6-292">Restituisce il nome distintivo dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="308f6-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="308f6-293">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="308f6-294">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-295">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="308f6-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="308f6-296">CertIssuerOid</span></span>
<span data-ttu-id="308f6-297">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-297">**Description:**</span></span>  
<span data-ttu-id="308f6-298">Restituisce il valore Oid dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="308f6-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="308f6-299">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="308f6-300">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-301">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="308f6-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="308f6-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="308f6-303">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-303">**Description:**</span></span>  
<span data-ttu-id="308f6-304">Restituisce le informazioni dell'algoritmo a chiave per il certificato X.509v3 sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="308f6-305">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="308f6-306">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-307">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="308f6-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="308f6-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="308f6-309">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-309">**Description:**</span></span>  
<span data-ttu-id="308f6-310">Restituisce i parametri dell'algoritmo a chiave per il certificato X.509v3 sotto forma di stringa esadecimale.</span><span class="sxs-lookup"><span data-stu-id="308f6-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="308f6-311">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="308f6-312">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-313">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="308f6-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="308f6-314">CertNameInfo</span></span>
<span data-ttu-id="308f6-315">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-315">**Description:**</span></span>  
<span data-ttu-id="308f6-316">Restituisce i nomi del soggetto e dell'autorità di certificazione di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="308f6-317">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="308f6-318">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-319">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="308f6-320">X509NameType: il valore X509NameType per il soggetto.</span><span class="sxs-lookup"><span data-stu-id="308f6-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="308f6-321">includesIssuerName: true per includere il nome dell'autorità di certificazione, in caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="308f6-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="308f6-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="308f6-322">CertNotAfter</span></span>
<span data-ttu-id="308f6-323">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-323">**Description:**</span></span>  
<span data-ttu-id="308f6-324">Restituisce la data nell'ora locale dopo la quale un certificato non è più valido.</span><span class="sxs-lookup"><span data-stu-id="308f6-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="308f6-325">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="308f6-326">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-327">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="308f6-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="308f6-328">CertNotBefore</span></span>
<span data-ttu-id="308f6-329">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-329">**Description:**</span></span>  
<span data-ttu-id="308f6-330">Restituisce la data nell'ora locale in cui un certificato diventa valido.</span><span class="sxs-lookup"><span data-stu-id="308f6-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="308f6-331">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="308f6-332">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-333">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="308f6-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="308f6-334">CertPublicKeyOid</span></span>
<span data-ttu-id="308f6-335">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-335">**Description:**</span></span>  
<span data-ttu-id="308f6-336">Restituisce l'Oid della chiave pubblica per il certificato X.509v3.</span><span class="sxs-lookup"><span data-stu-id="308f6-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="308f6-337">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="308f6-338">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-339">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="308f6-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="308f6-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="308f6-341">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-341">**Description:**</span></span>  
<span data-ttu-id="308f6-342">Restituisce l'Oid dei parametri della chiave pubblica per il certificato X.509v3.</span><span class="sxs-lookup"><span data-stu-id="308f6-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="308f6-343">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="308f6-344">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-345">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="308f6-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="308f6-346">CertSerialNumber</span></span>
<span data-ttu-id="308f6-347">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-347">**Description:**</span></span>  
<span data-ttu-id="308f6-348">Restituisce il numero di serie del certificato X.509v3.</span><span class="sxs-lookup"><span data-stu-id="308f6-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="308f6-349">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="308f6-350">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-351">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="308f6-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="308f6-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="308f6-353">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-353">**Description:**</span></span>  
<span data-ttu-id="308f6-354">Restituisce l'Oid dell'algoritmo usato per creare la firma di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="308f6-355">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="308f6-356">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-357">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="308f6-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="308f6-358">CertSubject</span></span>
<span data-ttu-id="308f6-359">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-359">**Description:**</span></span>  
<span data-ttu-id="308f6-360">Ottiene il nome distintivo del soggetto da un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="308f6-361">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="308f6-362">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-363">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="308f6-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="308f6-364">CertSubjectNameDN</span></span>
<span data-ttu-id="308f6-365">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-365">**Description:**</span></span>  
<span data-ttu-id="308f6-366">Restituisce il nome distintivo del soggetto di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="308f6-367">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="308f6-368">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-369">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="308f6-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="308f6-370">CertSubjectNameOid</span></span>
<span data-ttu-id="308f6-371">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-371">**Description:**</span></span>  
<span data-ttu-id="308f6-372">Restituisce l'Oid del nome del soggetto di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="308f6-373">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="308f6-374">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-375">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="308f6-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="308f6-376">CertThumbprint</span></span>
<span data-ttu-id="308f6-377">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-377">**Description:**</span></span>  
<span data-ttu-id="308f6-378">Restituisce l'identificazione personale di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="308f6-379">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="308f6-380">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-381">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="308f6-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="308f6-382">CertVersion</span></span>
<span data-ttu-id="308f6-383">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-383">**Description:**</span></span>  
<span data-ttu-id="308f6-384">Restituisce la versione in formato X.509 di un certificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="308f6-385">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="308f6-386">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-387">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="308f6-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-388">CGuid</span></span>
<span data-ttu-id="308f6-389">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-389">**Description:**</span></span>  
<span data-ttu-id="308f6-390">La funzione CGuid converte la rappresentazione di stringa di un GUID nella corrispondente rappresentazione binaria.</span><span class="sxs-lookup"><span data-stu-id="308f6-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="308f6-391">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="308f6-392">Stringa formattata con questo schema: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="308f6-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="308f6-393">Contiene</span><span class="sxs-lookup"><span data-stu-id="308f6-393">Contains</span></span>
<span data-ttu-id="308f6-394">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-394">**Description:**</span></span>  
<span data-ttu-id="308f6-395">La funzione Contains trova una stringa all'interno di un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="308f6-396">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-396">**Syntax:**</span></span>  
<span data-ttu-id="308f6-397">`num Contains (mvstring attribute, str search)` - distinzione maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="308f6-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="308f6-398">`num Contains (mvref attribute, str search)` - distinzione maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="308f6-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="308f6-399">attribute: l'attributo multivalore da cercare.</span><span class="sxs-lookup"><span data-stu-id="308f6-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="308f6-400">search: stringa da trovare nell'attributo.</span><span class="sxs-lookup"><span data-stu-id="308f6-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="308f6-401">Casetype: CaseInsensitive o CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="308f6-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="308f6-402">Restituisce l'indice nell'attributo multivalore in cui è stata trovata la stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="308f6-403">Se la stringa non viene trovata, restituisce 0.</span><span class="sxs-lookup"><span data-stu-id="308f6-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="308f6-404">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-404">**Remarks:**</span></span>  
<span data-ttu-id="308f6-405">Per gli attributi stringa multivalore, viene effettuata la ricerca di sottostringhe nei valori.</span><span class="sxs-lookup"><span data-stu-id="308f6-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="308f6-406">Per gli attributi di riferimento, la stringa cercata deve corrispondere esattamente al valore per essere considerata una corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="308f6-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="308f6-407">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="308f6-408">Se l'attributo proxyAddresses include un indirizzo di posta elettronica primario (indicato da "SMTP:") viene restituito l'attributo proxyAddress. In caso contrario viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="308f6-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="308f6-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="308f6-409">ConvertFromBase64</span></span>
<span data-ttu-id="308f6-410">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-410">**Description:**</span></span>  
<span data-ttu-id="308f6-411">La funzione ConvertFromBase64 converte il valore con codifica Base 64 specificato in una stringa normale.</span><span class="sxs-lookup"><span data-stu-id="308f6-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="308f6-412">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-412">**Syntax:**</span></span>  
<span data-ttu-id="308f6-413">`str ConvertFromBase64(str source)`: presuppone l'uso di Unicode per la codifica</span><span class="sxs-lookup"><span data-stu-id="308f6-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="308f6-414">source: stringa con codifica Base 64</span><span class="sxs-lookup"><span data-stu-id="308f6-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="308f6-415">Encoding: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="308f6-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="308f6-416">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="308f6-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="308f6-417">Entrambi gli esempi restituiscono "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="308f6-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="308f6-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="308f6-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="308f6-419">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-419">**Description:**</span></span>  
<span data-ttu-id="308f6-420">La funzione ConvertFromUTF8Hex converte il valore con codifica esadecimale UTF8 specificato in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="308f6-421">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="308f6-422">source: stringa con codifica a 2 byte UTF8</span><span class="sxs-lookup"><span data-stu-id="308f6-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="308f6-423">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-423">**Remarks:**</span></span>  
<span data-ttu-id="308f6-424">La differenza tra questa funzione e ConvertFromBase64([],UTF8) è che il risultato può essere usato per l'attributo DN.</span><span class="sxs-lookup"><span data-stu-id="308f6-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="308f6-425">Questo formato viene utilizzato da Azure Active Directory come DN.</span><span class="sxs-lookup"><span data-stu-id="308f6-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="308f6-426">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="308f6-427">Restituisce "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="308f6-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="308f6-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="308f6-428">ConvertToBase64</span></span>
<span data-ttu-id="308f6-429">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-429">**Description:**</span></span>  
<span data-ttu-id="308f6-430">La funzione ConvertToBase64 converte una stringa in una stringa Base 64 Unicode.</span><span class="sxs-lookup"><span data-stu-id="308f6-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="308f6-431">Converte il valore di una matrice di interi nella rappresentazione di stringa equivalente in cifre con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="308f6-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="308f6-432">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="308f6-433">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="308f6-434">Restituisce "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="308f6-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="308f6-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="308f6-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="308f6-436">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-436">**Description:**</span></span>  
<span data-ttu-id="308f6-437">La funzione ConvertToUTF8Hex converte una stringa in un valore con codifica esadecimale UTF8.</span><span class="sxs-lookup"><span data-stu-id="308f6-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="308f6-438">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="308f6-439">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-439">**Remarks:**</span></span>  
<span data-ttu-id="308f6-440">Il formato di output di questa funzione viene usato da Azure Active Directory come formato dell'attributo DN.</span><span class="sxs-lookup"><span data-stu-id="308f6-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="308f6-441">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="308f6-442">Restituisce 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="308f6-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="308f6-443">Numero</span><span class="sxs-lookup"><span data-stu-id="308f6-443">Count</span></span>
<span data-ttu-id="308f6-444">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-444">**Description:**</span></span>  
<span data-ttu-id="308f6-445">La funzione Count restituisce il numero di elementi in un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="308f6-446">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="308f6-447">CNum</span><span class="sxs-lookup"><span data-stu-id="308f6-447">CNum</span></span>
<span data-ttu-id="308f6-448">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-448">**Description:**</span></span>  
<span data-ttu-id="308f6-449">La funzione CNum accetta una stringa e restituisce un tipo di dati numerico.</span><span class="sxs-lookup"><span data-stu-id="308f6-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="308f6-450">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="308f6-451">CRef</span><span class="sxs-lookup"><span data-stu-id="308f6-451">CRef</span></span>
<span data-ttu-id="308f6-452">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-452">**Description:**</span></span>  
<span data-ttu-id="308f6-453">Converte una stringa in un attributo di riferimento.</span><span class="sxs-lookup"><span data-stu-id="308f6-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="308f6-454">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="308f6-455">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="308f6-456">CStr</span><span class="sxs-lookup"><span data-stu-id="308f6-456">CStr</span></span>
<span data-ttu-id="308f6-457">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-457">**Description:**</span></span>  
<span data-ttu-id="308f6-458">La funzione CStr esegue la conversione in un tipo di dati stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="308f6-459">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="308f6-460">value: può essere un valore numerico, un attributo di riferimento o un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="308f6-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="308f6-461">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="308f6-462">Può restituire "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="308f6-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="308f6-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="308f6-463">DateAdd</span></span>
<span data-ttu-id="308f6-464">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-464">**Description:**</span></span>  
<span data-ttu-id="308f6-465">Restituisce un valore Date contenente una data alla quale è stato aggiunto un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="308f6-466">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="308f6-467">interval: espressione stringa che corrisponde all'intervallo di tempo da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="308f6-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="308f6-468">La stringa deve avere almeno uno dei valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="308f6-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="308f6-469">yyyy Year</span><span class="sxs-lookup"><span data-stu-id="308f6-469">yyyy Year</span></span>
  * <span data-ttu-id="308f6-470">q Quarter</span><span class="sxs-lookup"><span data-stu-id="308f6-470">q Quarter</span></span>
  * <span data-ttu-id="308f6-471">m Month</span><span class="sxs-lookup"><span data-stu-id="308f6-471">m Month</span></span>
  * <span data-ttu-id="308f6-472">y Day of year</span><span class="sxs-lookup"><span data-stu-id="308f6-472">y Day of year</span></span>
  * <span data-ttu-id="308f6-473">d Day</span><span class="sxs-lookup"><span data-stu-id="308f6-473">d Day</span></span>
  * <span data-ttu-id="308f6-474">w Weekday</span><span class="sxs-lookup"><span data-stu-id="308f6-474">w Weekday</span></span>
  * <span data-ttu-id="308f6-475">ww Week</span><span class="sxs-lookup"><span data-stu-id="308f6-475">ww Week</span></span>
  * <span data-ttu-id="308f6-476">h Hour</span><span class="sxs-lookup"><span data-stu-id="308f6-476">h Hour</span></span>
  * <span data-ttu-id="308f6-477">n Minute</span><span class="sxs-lookup"><span data-stu-id="308f6-477">n Minute</span></span>
  * <span data-ttu-id="308f6-478">s Second</span><span class="sxs-lookup"><span data-stu-id="308f6-478">s Second</span></span>
* <span data-ttu-id="308f6-479">value: numero di unità da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="308f6-479">value: The number of units you want to add.</span></span> <span data-ttu-id="308f6-480">Può essere positivo (per ottenere date nel futuro) o negativo (per ottenere date nel passato).</span><span class="sxs-lookup"><span data-stu-id="308f6-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="308f6-481">date: data/ora che rappresenta la data alla quale viene aggiunto l'intervallo.</span><span class="sxs-lookup"><span data-stu-id="308f6-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="308f6-482">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="308f6-483">Aggiunge 3 mesi e restituisce un valore di data/ora che rappresenta "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="308f6-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="308f6-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="308f6-484">DateFromNum</span></span>
<span data-ttu-id="308f6-485">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-485">**Description:**</span></span>  
<span data-ttu-id="308f6-486">La funzione DateFromNum converte un valore nel formato di data di Active Directory in un tipo di data/ora.</span><span class="sxs-lookup"><span data-stu-id="308f6-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="308f6-487">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="308f6-488">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="308f6-489">Restituisce un valore di data/ora che rappresenta 2012-01-01 23:00:00</span><span class="sxs-lookup"><span data-stu-id="308f6-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="308f6-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="308f6-490">DNComponent</span></span>
<span data-ttu-id="308f6-491">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-491">**Description:**</span></span>  
<span data-ttu-id="308f6-492">La funzione DNComponent restituisce il valore di un componente DN specificato, a partire da sinistra.</span><span class="sxs-lookup"><span data-stu-id="308f6-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="308f6-493">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="308f6-494">dn: attributo di riferimento da interpretare</span><span class="sxs-lookup"><span data-stu-id="308f6-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="308f6-495">ComponentNumber: componente nel DN da restituire</span><span class="sxs-lookup"><span data-stu-id="308f6-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="308f6-496">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="308f6-497">Se dn è "cn=Joe,ou=…," verrà restituito Joe</span><span class="sxs-lookup"><span data-stu-id="308f6-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="308f6-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="308f6-498">DNComponentRev</span></span>
<span data-ttu-id="308f6-499">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-499">**Description:**</span></span>  
<span data-ttu-id="308f6-500">La funzione DNComponentRev restituisce il valore di un componente DN specificato, a partire da destra (dalla fine).</span><span class="sxs-lookup"><span data-stu-id="308f6-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="308f6-501">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="308f6-502">dn: attributo di riferimento da interpretare</span><span class="sxs-lookup"><span data-stu-id="308f6-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="308f6-503">ComponentNumber: componente nel DN da restituire</span><span class="sxs-lookup"><span data-stu-id="308f6-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="308f6-504">Options: DC - Ignora tutti i componenti con "dc="</span><span class="sxs-lookup"><span data-stu-id="308f6-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="308f6-505">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-505">**Example:**</span></span>  
<span data-ttu-id="308f6-506">Se dn è "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com", allora</span><span class="sxs-lookup"><span data-stu-id="308f6-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="308f6-507">restituiscono entrambi US.</span><span class="sxs-lookup"><span data-stu-id="308f6-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="308f6-508">Errore</span><span class="sxs-lookup"><span data-stu-id="308f6-508">Error</span></span>
<span data-ttu-id="308f6-509">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-509">**Description:**</span></span>  
<span data-ttu-id="308f6-510">La funzione Error viene usata per restituire un errore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="308f6-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="308f6-511">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="308f6-512">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="308f6-513">Se l'attributo accountName non è presente, viene generato un errore nell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="308f6-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="308f6-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="308f6-514">EscapeDNComponent</span></span>
<span data-ttu-id="308f6-515">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-515">**Description:**</span></span>  
<span data-ttu-id="308f6-516">La funzione EscapeDNComponent accetta un componente di un DN e inserisce un carattere di escape per consentirne la rappresentazione in LDAP.</span><span class="sxs-lookup"><span data-stu-id="308f6-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="308f6-517">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="308f6-518">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="308f6-519">Verifica che sia possibile creare l'oggetto in una directory LDAP, anche se l'attributo displayName include caratteri che devono essere preceduti da un carattere di escape in LDAP.</span><span class="sxs-lookup"><span data-stu-id="308f6-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="308f6-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="308f6-520">FormatDateTime</span></span>
<span data-ttu-id="308f6-521">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-521">**Description:**</span></span>  
<span data-ttu-id="308f6-522">La funzione FormatDateTime viene usata per formattare un valore di data/ora in una stringa con un formato specificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="308f6-523">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="308f6-524">value: valore nel formato di data/ora</span><span class="sxs-lookup"><span data-stu-id="308f6-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="308f6-525">format: stringa che rappresenta il formato in cui effettuare la conversione.</span><span class="sxs-lookup"><span data-stu-id="308f6-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="308f6-526">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-526">**Remarks:**</span></span>  
<span data-ttu-id="308f6-527">I valori possibili per il formato sono disponibili qui: [Formati di data/ora definiti dall'utente (funzione Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="308f6-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="308f6-528">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="308f6-529">Il risultato è "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="308f6-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="308f6-530">Può restituire "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="308f6-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="308f6-531">GUID</span><span class="sxs-lookup"><span data-stu-id="308f6-531">GUID</span></span>
<span data-ttu-id="308f6-532">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-532">**Description:**</span></span>  
<span data-ttu-id="308f6-533">La funzione GUID genera un nuovo GUID casuale.</span><span class="sxs-lookup"><span data-stu-id="308f6-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="308f6-534">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="308f6-535">IIF</span><span class="sxs-lookup"><span data-stu-id="308f6-535">IIF</span></span>
<span data-ttu-id="308f6-536">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-536">**Description:**</span></span>  
<span data-ttu-id="308f6-537">La funzione IIF restituisce uno dei possibili valori di un set, in base a una condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="308f6-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="308f6-538">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="308f6-539">condition: qualsiasi valore o espressione che possa restituire true o false.</span><span class="sxs-lookup"><span data-stu-id="308f6-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="308f6-540">valueIfTrue: se la condizione restituisce true, il valore restituito.</span><span class="sxs-lookup"><span data-stu-id="308f6-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="308f6-541">valueIfFalse: se la condizione restituisce false, il valore restituito.</span><span class="sxs-lookup"><span data-stu-id="308f6-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="308f6-542">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="308f6-543">Se l'utente è uno stagista, restituisce l'alias di un utente, aggiungendo "t-" all'inizio. In caso contrario restituisce l'alias dell'utente invariato.</span><span class="sxs-lookup"><span data-stu-id="308f6-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="308f6-544">InStr</span><span class="sxs-lookup"><span data-stu-id="308f6-544">InStr</span></span>
<span data-ttu-id="308f6-545">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-545">**Description:**</span></span>  
<span data-ttu-id="308f6-546">La funzione InStr trova la prima occorrenza di una sottostringa in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="308f6-547">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="308f6-548">stringcheck: stringa da cercare</span><span class="sxs-lookup"><span data-stu-id="308f6-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="308f6-549">stringmatch: stringa da trovare</span><span class="sxs-lookup"><span data-stu-id="308f6-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="308f6-550">start: posizione iniziale per la ricerca della sottostringa</span><span class="sxs-lookup"><span data-stu-id="308f6-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="308f6-551">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="308f6-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="308f6-552">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-552">**Remarks:**</span></span>  
<span data-ttu-id="308f6-553">Restituisce la posizione in cui è stata trovata la sottostringa o 0 se non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="308f6-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="308f6-554">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="308f6-555">Restituisce 5</span><span class="sxs-lookup"><span data-stu-id="308f6-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="308f6-556">Restituisce 7</span><span class="sxs-lookup"><span data-stu-id="308f6-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="308f6-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="308f6-557">InStrRev</span></span>
<span data-ttu-id="308f6-558">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-558">**Description:**</span></span>  
<span data-ttu-id="308f6-559">La funzione InStrRev trova l'ultima occorrenza di una sottostringa in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="308f6-560">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="308f6-561">stringcheck: stringa da cercare</span><span class="sxs-lookup"><span data-stu-id="308f6-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="308f6-562">stringmatch: stringa da trovare</span><span class="sxs-lookup"><span data-stu-id="308f6-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="308f6-563">start: posizione iniziale per la ricerca della sottostringa</span><span class="sxs-lookup"><span data-stu-id="308f6-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="308f6-564">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="308f6-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="308f6-565">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-565">**Remarks:**</span></span>  
<span data-ttu-id="308f6-566">Restituisce la posizione in cui è stata trovata la sottostringa o 0 se non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="308f6-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="308f6-567">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="308f6-568">Restituisce 7</span><span class="sxs-lookup"><span data-stu-id="308f6-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="308f6-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="308f6-569">IsBitSet</span></span>
<span data-ttu-id="308f6-570">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-570">**Description:**</span></span>  
<span data-ttu-id="308f6-571">La funzione IsBitSet verifica se un bit è o non è impostato.</span><span class="sxs-lookup"><span data-stu-id="308f6-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="308f6-572">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="308f6-573">value: valore numerico valutato. flag: valore numerico contenente il bit da valutare</span><span class="sxs-lookup"><span data-stu-id="308f6-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="308f6-574">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="308f6-575">Restituisce True perché il bit "4" è impostato come valore esadecimale "F"</span><span class="sxs-lookup"><span data-stu-id="308f6-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="308f6-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="308f6-576">IsDate</span></span>
<span data-ttu-id="308f6-577">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-577">**Description:**</span></span>  
<span data-ttu-id="308f6-578">Se l'espressione può essere valutata come tipo di data/ora, la funzione IsDate restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="308f6-579">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="308f6-580">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-580">**Remarks:**</span></span>  
<span data-ttu-id="308f6-581">Usata per determinare se CDate() riuscirà.</span><span class="sxs-lookup"><span data-stu-id="308f6-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="308f6-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="308f6-582">IsCert</span></span>
<span data-ttu-id="308f6-583">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-583">**Description:**</span></span>  
<span data-ttu-id="308f6-584">Restituisce true se i dati non elaborati possono essere serializzati nell'oggetto certificato X509Certificate2 di .NET.</span><span class="sxs-lookup"><span data-stu-id="308f6-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="308f6-585">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="308f6-586">certificateRawData: rappresentazione in forma di matrice di byte di un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="308f6-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="308f6-587">La matrice di byte può essere costituita da dati X.509 in codifica binaria (DER) o Base64.</span><span class="sxs-lookup"><span data-stu-id="308f6-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="308f6-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="308f6-588">IsEmpty</span></span>
<span data-ttu-id="308f6-589">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-589">**Description:**</span></span>  
<span data-ttu-id="308f6-590">Se l'attributo è presente in CS o MV, ma restituisce una stringa vuota, la funzione IsEmpty restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="308f6-591">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="308f6-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-592">IsGuid</span></span>
<span data-ttu-id="308f6-593">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-593">**Description:**</span></span>  
<span data-ttu-id="308f6-594">Se la stringa può essere convertita in un GUID, la funzione IsGuid restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="308f6-595">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="308f6-596">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-596">**Remarks:**</span></span>  
<span data-ttu-id="308f6-597">Un GUID viene definito come stringa in base a uno degli schemi seguenti: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="308f6-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="308f6-598">Usata per determinare se CGuid() riuscirà.</span><span class="sxs-lookup"><span data-stu-id="308f6-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="308f6-599">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="308f6-600">Se StrAttribute ha un formato GUID, restituisce una rappresentazione binaria. In caso contrario restituisce Null.</span><span class="sxs-lookup"><span data-stu-id="308f6-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="308f6-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="308f6-601">IsNull</span></span>
<span data-ttu-id="308f6-602">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-602">**Description:**</span></span>  
<span data-ttu-id="308f6-603">Se l'espressione restituisce Null, la funzione IsNull restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="308f6-604">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="308f6-605">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-605">**Remarks:**</span></span>  
<span data-ttu-id="308f6-606">Per un attributo, Null è espresso dall'assenza dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="308f6-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="308f6-607">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="308f6-608">Restituisce True se l'attributo non è presente in CS o MV.</span><span class="sxs-lookup"><span data-stu-id="308f6-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="308f6-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="308f6-609">IsNullOrEmpty</span></span>
<span data-ttu-id="308f6-610">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-610">**Description:**</span></span>  
<span data-ttu-id="308f6-611">Se l'espressione è Null o una stringa vuota, la funzione IsNullOrEmpty restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="308f6-612">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="308f6-613">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-613">**Remarks:**</span></span>  
<span data-ttu-id="308f6-614">Per un attributo, verrà restituito True se l'attributo è assente oppure se è presente, ma è una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="308f6-615">La funzione inversa di questa funzione è denominata IsPresent.</span><span class="sxs-lookup"><span data-stu-id="308f6-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="308f6-616">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="308f6-617">Restituisce True se l'attributo non è presente oppure è una stringa vuota in CS o MV.</span><span class="sxs-lookup"><span data-stu-id="308f6-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="308f6-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="308f6-618">IsNumeric</span></span>
<span data-ttu-id="308f6-619">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-619">**Description:**</span></span>  
<span data-ttu-id="308f6-620">La funzione IsNumeric restituisce un valore booleano che indica se un'espressione può essere valutata come tipo di numero.</span><span class="sxs-lookup"><span data-stu-id="308f6-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="308f6-621">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="308f6-622">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-622">**Remarks:**</span></span>  
<span data-ttu-id="308f6-623">Usata per determinare se CNum() riuscirà ad analizzare l'espressione.</span><span class="sxs-lookup"><span data-stu-id="308f6-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="308f6-624">IsString</span><span class="sxs-lookup"><span data-stu-id="308f6-624">IsString</span></span>
<span data-ttu-id="308f6-625">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-625">**Description:**</span></span>  
<span data-ttu-id="308f6-626">Se l'espressione può essere valutata come tipo stringa, la funzione IsString restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="308f6-627">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="308f6-628">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-628">**Remarks:**</span></span>  
<span data-ttu-id="308f6-629">Usata per determinare se CStr() riuscirà ad analizzare l'espressione.</span><span class="sxs-lookup"><span data-stu-id="308f6-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="308f6-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="308f6-630">IsPresent</span></span>
<span data-ttu-id="308f6-631">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-631">**Description:**</span></span>  
<span data-ttu-id="308f6-632">Se l'espressione restituisce una stringa non Null e non vuota, la funzione IsPresent restituisce True.</span><span class="sxs-lookup"><span data-stu-id="308f6-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="308f6-633">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="308f6-634">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-634">**Remarks:**</span></span>  
<span data-ttu-id="308f6-635">La funzione inversa di questa funzione è denominata IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="308f6-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="308f6-636">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="308f6-637">Elemento</span><span class="sxs-lookup"><span data-stu-id="308f6-637">Item</span></span>
<span data-ttu-id="308f6-638">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-638">**Description:**</span></span>  
<span data-ttu-id="308f6-639">La funzione Item restituisce un elemento da una stringa o un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="308f6-640">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="308f6-641">attribute: attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="308f6-642">index: indice di un elemento nella stringa multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="308f6-643">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-643">**Remarks:**</span></span>  
<span data-ttu-id="308f6-644">La funzione Item usata con la funzione Contains è utile, perché quest'ultima restituisce l'indice di un elemento nell'attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="308f6-645">Genera un errore se l'indice non è compreso nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="308f6-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="308f6-646">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="308f6-647">Restituisce l'indirizzo di posta elettronica primario.</span><span class="sxs-lookup"><span data-stu-id="308f6-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="308f6-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="308f6-648">ItemOrNull</span></span>
<span data-ttu-id="308f6-649">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-649">**Description:**</span></span>  
<span data-ttu-id="308f6-650">La funzione ItemOrNull restituisce un elemento da una stringa o un attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="308f6-651">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="308f6-652">attribute: attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="308f6-653">index: indice di un elemento nella stringa multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="308f6-654">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-654">**Remarks:**</span></span>  
<span data-ttu-id="308f6-655">La funzione ItemOrNull usata con la funzione Contains è utile, perché quest'ultima restituisce l'indice di un elemento nell'attributo multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="308f6-656">Se l'indice non è compreso nell'intervallo, restituisce un valore Null.</span><span class="sxs-lookup"><span data-stu-id="308f6-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="308f6-657">Join</span><span class="sxs-lookup"><span data-stu-id="308f6-657">Join</span></span>
<span data-ttu-id="308f6-658">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-658">**Description:**</span></span>  
<span data-ttu-id="308f6-659">La funzione Join accetta una stringa multivalore e restituisce una stringa a valore singolo con il separatore specificato inserito tra ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="308f6-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="308f6-660">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="308f6-661">attribute: attributo multivalore contenente stringhe da unire.</span><span class="sxs-lookup"><span data-stu-id="308f6-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="308f6-662">delimiter: qualsiasi stringa usata per separare le sottostringhe nella stringa restituita.</span><span class="sxs-lookup"><span data-stu-id="308f6-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="308f6-663">Se omessa, viene usato uno spazio (" ").</span><span class="sxs-lookup"><span data-stu-id="308f6-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="308f6-664">Se Delimiter è una stringa di lunghezza zero ("") o Nothing, tutti gli elementi nell'elenco vengono concatenati senza delimitatori.</span><span class="sxs-lookup"><span data-stu-id="308f6-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="308f6-665">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-665">**Remarks**</span></span>  
<span data-ttu-id="308f6-666">Esiste un'analogia tra le funzioni Join e Split.</span><span class="sxs-lookup"><span data-stu-id="308f6-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="308f6-667">La funzione Join accetta una matrice di stringhe e le unisce usando una stringa delimitatore per restituire una singola stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="308f6-668">La funzione Split accetta una stringa e la separa in corrispondenza del delimitatore per restituire una matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="308f6-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="308f6-669">Tuttavia, la differenza principale consiste nel fatto che Join può concatenare stringhe con qualsiasi stringa delimitatore, mentre Split può separare stringhe usando unicamente un delimitatore di un solo carattere.</span><span class="sxs-lookup"><span data-stu-id="308f6-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="308f6-670">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="308f6-671">Può restituire: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="308f6-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="308f6-672">LCase</span><span class="sxs-lookup"><span data-stu-id="308f6-672">LCase</span></span>
<span data-ttu-id="308f6-673">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-673">**Description:**</span></span>  
<span data-ttu-id="308f6-674">La funzione LCase converte tutti i caratteri in una stringa in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="308f6-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="308f6-675">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="308f6-676">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="308f6-677">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="308f6-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="308f6-678">Left</span><span class="sxs-lookup"><span data-stu-id="308f6-678">Left</span></span>
<span data-ttu-id="308f6-679">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-679">**Description:**</span></span>  
<span data-ttu-id="308f6-680">La funzione Left restituisce un numero di caratteri specificato a partire da sinistra di una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="308f6-681">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="308f6-682">string: stringa dalla quale restituire i caratteri</span><span class="sxs-lookup"><span data-stu-id="308f6-682">string: the string to return characters from</span></span>
* <span data-ttu-id="308f6-683">NumChars: numero che identifica il numero di caratteri da restituire dall'inizio (sinistra) della stringa</span><span class="sxs-lookup"><span data-stu-id="308f6-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="308f6-684">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-684">**Remarks:**</span></span>  
<span data-ttu-id="308f6-685">Una stringa contenente i primi caratteri numChars della stringa:</span><span class="sxs-lookup"><span data-stu-id="308f6-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="308f6-686">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="308f6-687">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="308f6-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="308f6-688">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-688">If string is null, return empty string.</span></span>

<span data-ttu-id="308f6-689">Se string contiene un numero di caratteri inferiore al numero specificato in numChars, viene restituita una stringa identica a string (ovvero contenente tutti i caratteri nel parametro 1).</span><span class="sxs-lookup"><span data-stu-id="308f6-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="308f6-690">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="308f6-691">Restituisce "Joh".</span><span class="sxs-lookup"><span data-stu-id="308f6-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="308f6-692">Len</span><span class="sxs-lookup"><span data-stu-id="308f6-692">Len</span></span>
<span data-ttu-id="308f6-693">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-693">**Description:**</span></span>  
<span data-ttu-id="308f6-694">La funzione Len restituisce il numero di caratteri in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="308f6-695">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="308f6-696">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="308f6-697">Restituisce 8</span><span class="sxs-lookup"><span data-stu-id="308f6-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="308f6-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="308f6-698">LTrim</span></span>
<span data-ttu-id="308f6-699">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-699">**Description:**</span></span>  
<span data-ttu-id="308f6-700">La funzione LTrim rimuove gli spazi vuoti iniziali da una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="308f6-701">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="308f6-702">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="308f6-703">Restituisce "Test"</span><span class="sxs-lookup"><span data-stu-id="308f6-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="308f6-704">Mid</span><span class="sxs-lookup"><span data-stu-id="308f6-704">Mid</span></span>
<span data-ttu-id="308f6-705">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-705">**Description:**</span></span>  
<span data-ttu-id="308f6-706">La funzione Mid restituisce un numero di caratteri specificato a partire da una posizione specificata di una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="308f6-707">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="308f6-708">string: stringa dalla quale restituire i caratteri</span><span class="sxs-lookup"><span data-stu-id="308f6-708">string: the string to return characters from</span></span>
* <span data-ttu-id="308f6-709">start: numero che identifica la posizione in una stringa dalla quale iniziare a restituire caratteri</span><span class="sxs-lookup"><span data-stu-id="308f6-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="308f6-710">NumChars: numero che identifica il numero di caratteri da restituire dalla posizione nella stringa</span><span class="sxs-lookup"><span data-stu-id="308f6-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="308f6-711">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-711">**Remarks:**</span></span>  
<span data-ttu-id="308f6-712">Restituisce i caratteri in numChars a partire dalla posizione start nella stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="308f6-713">Stringa contenente i caratteri specificati in numChars a partire dalla posizione start nella stringa:</span><span class="sxs-lookup"><span data-stu-id="308f6-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="308f6-714">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="308f6-715">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="308f6-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="308f6-716">Se start è > della lunghezza della stringa, restituisce la stringa di input.</span><span class="sxs-lookup"><span data-stu-id="308f6-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="308f6-717">Se start <= 0, restituisce la stringa di input.</span><span class="sxs-lookup"><span data-stu-id="308f6-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="308f6-718">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-718">If string is null, return empty string.</span></span>

<span data-ttu-id="308f6-719">Se nella stringa non ci sono caratteri numChar rimanenti dalla posizione start, vengono restituiti quanti più caratteri possibile.</span><span class="sxs-lookup"><span data-stu-id="308f6-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="308f6-720">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="308f6-721">Restituisce "hn Do".</span><span class="sxs-lookup"><span data-stu-id="308f6-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="308f6-722">Restituisce "Doe"</span><span class="sxs-lookup"><span data-stu-id="308f6-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="308f6-723">Now</span><span class="sxs-lookup"><span data-stu-id="308f6-723">Now</span></span>
<span data-ttu-id="308f6-724">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-724">**Description:**</span></span>  
<span data-ttu-id="308f6-725">La funzione Now restituisce un valore di data/ora che specifica la data e l'ora correnti, in base alla data e all'ora di sistema del computer.</span><span class="sxs-lookup"><span data-stu-id="308f6-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="308f6-726">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="308f6-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="308f6-727">NumFromDate</span></span>
<span data-ttu-id="308f6-728">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-728">**Description:**</span></span>  
<span data-ttu-id="308f6-729">La funzione NumFromDate restituisce una data nel formato di AD.</span><span class="sxs-lookup"><span data-stu-id="308f6-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="308f6-730">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="308f6-731">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="308f6-732">Restituisce 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="308f6-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="308f6-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="308f6-733">PadLeft</span></span>
<span data-ttu-id="308f6-734">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-734">**Description:**</span></span>  
<span data-ttu-id="308f6-735">La funzione PadLeft aggiunge a sinistra di una stringa il carattere di riempimento specificato, fino alla lunghezza indicata.</span><span class="sxs-lookup"><span data-stu-id="308f6-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="308f6-736">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="308f6-737">string: stringa da riempire.</span><span class="sxs-lookup"><span data-stu-id="308f6-737">string: the string to pad.</span></span>
* <span data-ttu-id="308f6-738">length: intero che rappresenta la lunghezza della stringa desiderata.</span><span class="sxs-lookup"><span data-stu-id="308f6-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="308f6-739">padCharacter: stringa costituita da un singolo carattere da usare come carattere di riempimento</span><span class="sxs-lookup"><span data-stu-id="308f6-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="308f6-740">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-740">**Remarks:**</span></span>

* <span data-ttu-id="308f6-741">Se la lunghezza di string è minore di length, padCharacter viene aggiunto ripetutamente all'inizio (sinistra) di string finché avrà una lunghezza uguale a length.</span><span class="sxs-lookup"><span data-stu-id="308f6-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="308f6-742">PadCharacter può essere uno spazio, ma non un valore null.</span><span class="sxs-lookup"><span data-stu-id="308f6-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="308f6-743">Se la lunghezza di string è uguale a o maggiore di length, la stringa viene restituita invariata.</span><span class="sxs-lookup"><span data-stu-id="308f6-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="308f6-744">Se string ha una lunghezza maggiore di o uguale a length, viene restituita una stringa identica a string.</span><span class="sxs-lookup"><span data-stu-id="308f6-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="308f6-745">Se la lunghezza di string è minore di length, viene restituita una nuova stringa con la lunghezza desiderata contenente il valore di string con l'aggiunta di padCharacter.</span><span class="sxs-lookup"><span data-stu-id="308f6-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="308f6-746">Se la stringa è Null, la funzione restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="308f6-747">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="308f6-748">Restituisce "000000User".</span><span class="sxs-lookup"><span data-stu-id="308f6-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="308f6-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="308f6-749">PadRight</span></span>
<span data-ttu-id="308f6-750">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-750">**Description:**</span></span>  
<span data-ttu-id="308f6-751">La funzione PadRight aggiunge a destra di una stringa il carattere di riempimento specificato, fino alla lunghezza indicata.</span><span class="sxs-lookup"><span data-stu-id="308f6-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="308f6-752">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="308f6-753">string: stringa da riempire.</span><span class="sxs-lookup"><span data-stu-id="308f6-753">string: the string to pad.</span></span>
* <span data-ttu-id="308f6-754">length: intero che rappresenta la lunghezza della stringa desiderata.</span><span class="sxs-lookup"><span data-stu-id="308f6-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="308f6-755">padCharacter: stringa costituita da un singolo carattere da usare come carattere di riempimento</span><span class="sxs-lookup"><span data-stu-id="308f6-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="308f6-756">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-756">**Remarks:**</span></span>

* <span data-ttu-id="308f6-757">Se la lunghezza di string è minore di length, padCharacter viene aggiunto ripetutamente alla fine (destra) di string finché avrà una lunghezza uguale a length.</span><span class="sxs-lookup"><span data-stu-id="308f6-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="308f6-758">PadCharacter può essere uno spazio, ma non un valore null.</span><span class="sxs-lookup"><span data-stu-id="308f6-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="308f6-759">Se la lunghezza di string è uguale a o maggiore di length, la stringa viene restituita invariata.</span><span class="sxs-lookup"><span data-stu-id="308f6-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="308f6-760">Se string ha una lunghezza maggiore di o uguale a length, viene restituita una stringa identica a string.</span><span class="sxs-lookup"><span data-stu-id="308f6-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="308f6-761">Se la lunghezza di string è minore di length, viene restituita una nuova stringa con la lunghezza desiderata contenente il valore di string con l'aggiunta di padCharacter.</span><span class="sxs-lookup"><span data-stu-id="308f6-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="308f6-762">Se la stringa è Null, la funzione restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="308f6-763">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="308f6-764">Restituisce "User000000".</span><span class="sxs-lookup"><span data-stu-id="308f6-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="308f6-765">PCase</span><span class="sxs-lookup"><span data-stu-id="308f6-765">PCase</span></span>
<span data-ttu-id="308f6-766">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-766">**Description:**</span></span>  
<span data-ttu-id="308f6-767">La funzione PCase converte in maiuscolo il primo carattere di ogni parola delimitata da spazi contenuta in una stringa, mentre tutti gli altri caratteri vengono convertiti in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="308f6-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="308f6-768">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="308f6-769">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-769">**Remarks:**</span></span>

* <span data-ttu-id="308f6-770">Questa funzione attualmente non offre una corretta conversione di maiuscole e minuscole in caso di parola interamente in maiuscolo, come un acronimo.</span><span class="sxs-lookup"><span data-stu-id="308f6-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="308f6-771">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="308f6-772">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="308f6-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="308f6-773">Restituisce "Test"</span><span class="sxs-lookup"><span data-stu-id="308f6-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="308f6-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="308f6-774">RandomNum</span></span>
<span data-ttu-id="308f6-775">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-775">**Description:**</span></span>  
<span data-ttu-id="308f6-776">La funzione RandomNum restituisce un numero casuale compreso in un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="308f6-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="308f6-777">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="308f6-778">start: numero che identifica il limite inferiore del valore casuale da generare</span><span class="sxs-lookup"><span data-stu-id="308f6-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="308f6-779">end: numero che identifica il limite superiore del valore casuale da generare</span><span class="sxs-lookup"><span data-stu-id="308f6-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="308f6-780">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="308f6-781">Può restituire 734.</span><span class="sxs-lookup"><span data-stu-id="308f6-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="308f6-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="308f6-782">RemoveDuplicates</span></span>
<span data-ttu-id="308f6-783">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-783">**Description:**</span></span>  
<span data-ttu-id="308f6-784">La funzione RemoveDuplicates accetta una stringa multivalore e verifica che ogni valore sia univoco.</span><span class="sxs-lookup"><span data-stu-id="308f6-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="308f6-785">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="308f6-786">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="308f6-787">Restituisce un attributo proxyAddress purificato in cui sono stati rimossi tutti i valori duplicati.</span><span class="sxs-lookup"><span data-stu-id="308f6-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="308f6-788">Replace</span><span class="sxs-lookup"><span data-stu-id="308f6-788">Replace</span></span>
<span data-ttu-id="308f6-789">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-789">**Description:**</span></span>  
<span data-ttu-id="308f6-790">La funzione Replace sostituisce tutte le occorrenze di una stringa in un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="308f6-791">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="308f6-792">string: stringa in cui sostituire i valori.</span><span class="sxs-lookup"><span data-stu-id="308f6-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="308f6-793">OldValue: stringa da cercare e sostituire.</span><span class="sxs-lookup"><span data-stu-id="308f6-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="308f6-794">NewValue: stringa oggetto della sostituzione.</span><span class="sxs-lookup"><span data-stu-id="308f6-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="308f6-795">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-795">**Remarks:**</span></span>  
<span data-ttu-id="308f6-796">La funzione riconosce i moniker speciali seguenti:</span><span class="sxs-lookup"><span data-stu-id="308f6-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="308f6-797">\n - Nuova riga</span><span class="sxs-lookup"><span data-stu-id="308f6-797">\n – New Line</span></span>
* <span data-ttu-id="308f6-798">\r - Ritorno a capo</span><span class="sxs-lookup"><span data-stu-id="308f6-798">\r – Carriage Return</span></span>
* <span data-ttu-id="308f6-799">\t - Tabulazione</span><span class="sxs-lookup"><span data-stu-id="308f6-799">\t – Tab</span></span>

<span data-ttu-id="308f6-800">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="308f6-801">Sostituisce CRLF con una virgola e uno spazio e può generare "One Microsoft Way, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="308f6-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="308f6-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="308f6-802">ReplaceChars</span></span>
<span data-ttu-id="308f6-803">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-803">**Description:**</span></span>  
<span data-ttu-id="308f6-804">La funzione ReplaceChars sostituisce tutte le occorrenze dei caratteri trovati nella stringa ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="308f6-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="308f6-805">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="308f6-806">string: stringa in cui sostituire i caratteri.</span><span class="sxs-lookup"><span data-stu-id="308f6-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="308f6-807">ReplacePattern: stringa contenente un dizionario con i caratteri da sostituire.</span><span class="sxs-lookup"><span data-stu-id="308f6-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="308f6-808">Il formato è {source1}:{target1},{source2}:{target2},{sourceN},{targetN} dove source è il carattere da trovare e target la stringa con cui sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="308f6-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="308f6-809">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-809">**Remarks:**</span></span>

* <span data-ttu-id="308f6-810">La funzione accetta ogni occorrenza delle origini definite e le sostituisce con le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="308f6-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="308f6-811">Source deve corrispondere esattamente a un carattere (Unicode).</span><span class="sxs-lookup"><span data-stu-id="308f6-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="308f6-812">Source non può essere una stringa vuota e non può essere più lunga di un carattere (errore di analisi).</span><span class="sxs-lookup"><span data-stu-id="308f6-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="308f6-813">Il target può contenere più caratteri, ad esempio ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="308f6-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="308f6-814">Target può essere una stringa vuota, per indicare che il carattere deve essere rimosso.</span><span class="sxs-lookup"><span data-stu-id="308f6-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="308f6-815">Source fa distinzione tra maiuscole e minuscole e deve essere una corrispondenza esatta.</span><span class="sxs-lookup"><span data-stu-id="308f6-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="308f6-816">I caratteri , (virgola) e : (due punti) sono riservati e non possono essere sostituiti usando questa funzione.</span><span class="sxs-lookup"><span data-stu-id="308f6-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="308f6-817">Spazi e altri caratteri vuoti nella stringa ReplacePattern vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="308f6-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="308f6-818">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="308f6-819">Restituisce Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="308f6-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="308f6-820">Restituisce "ONeil". Viene definita la rimozione della virgoletta singola.</span><span class="sxs-lookup"><span data-stu-id="308f6-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="308f6-821">Right</span><span class="sxs-lookup"><span data-stu-id="308f6-821">Right</span></span>
<span data-ttu-id="308f6-822">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-822">**Description:**</span></span>  
<span data-ttu-id="308f6-823">La funzione Right restituisce un numero di caratteri specificato a partire dalla destra (fine) di una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="308f6-824">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="308f6-825">string: stringa dalla quale restituire i caratteri</span><span class="sxs-lookup"><span data-stu-id="308f6-825">string: the string to return characters from</span></span>
* <span data-ttu-id="308f6-826">NumChars: numero che identifica il numero di caratteri da restituire dalla fine (destra) della stringa</span><span class="sxs-lookup"><span data-stu-id="308f6-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="308f6-827">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-827">**Remarks:**</span></span>  
<span data-ttu-id="308f6-828">I caratteri NumChars vengono restituiti dall'ultima posizione della stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="308f6-829">Stringa contenente gli ultimi caratteri numChars in string:</span><span class="sxs-lookup"><span data-stu-id="308f6-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="308f6-830">Se numChars = 0, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="308f6-831">Se numChars < 0, restituisce una stringa di input.</span><span class="sxs-lookup"><span data-stu-id="308f6-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="308f6-832">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-832">If string is null, return empty string.</span></span>

<span data-ttu-id="308f6-833">Se string contiene un numero di caratteri inferiore al numero specificato in NumChars, viene restituita una stringa identica a string.</span><span class="sxs-lookup"><span data-stu-id="308f6-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="308f6-834">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="308f6-835">Restituisce "Doe".</span><span class="sxs-lookup"><span data-stu-id="308f6-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="308f6-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="308f6-836">RTrim</span></span>
<span data-ttu-id="308f6-837">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-837">**Description:**</span></span>  
<span data-ttu-id="308f6-838">La funzione RTrim rimuove gli spazi vuoti finali da una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="308f6-839">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="308f6-840">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="308f6-841">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="308f6-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="308f6-842">Selezionare</span><span class="sxs-lookup"><span data-stu-id="308f6-842">Select</span></span>
<span data-ttu-id="308f6-843">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-843">**Description:**</span></span>  
<span data-ttu-id="308f6-844">Elabora tutti i valori in un attributo multivalore, o nell'output di un'espressione, in base alla funzione specificata.</span><span class="sxs-lookup"><span data-stu-id="308f6-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="308f6-845">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="308f6-846">item: rappresenta un elemento nell'attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="308f6-847">attribute: l'attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="308f6-848">expression: un'espressione che restituisce una raccolta di valori</span><span class="sxs-lookup"><span data-stu-id="308f6-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="308f6-849">condition: qualsiasi funzione in grado di elaborare un elemento nell'attributo</span><span class="sxs-lookup"><span data-stu-id="308f6-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="308f6-850">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="308f6-851">Restituisce tutti i valori dell'attributo multivalore otherPhone dopo che sono stati rimossi i trattini (-).</span><span class="sxs-lookup"><span data-stu-id="308f6-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="308f6-852">Split</span><span class="sxs-lookup"><span data-stu-id="308f6-852">Split</span></span>
<span data-ttu-id="308f6-853">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-853">**Description:**</span></span>  
<span data-ttu-id="308f6-854">La funzione Split accetta una stringa con valori separati da delimitatore e la converte in una stringa multivalore.</span><span class="sxs-lookup"><span data-stu-id="308f6-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="308f6-855">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="308f6-856">value: stringa con un carattere delimitatore da separare.</span><span class="sxs-lookup"><span data-stu-id="308f6-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="308f6-857">delimiter: singolo carattere da usare come delimitatore.</span><span class="sxs-lookup"><span data-stu-id="308f6-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="308f6-858">limit: numero massimo di valori che saranno restituiti.</span><span class="sxs-lookup"><span data-stu-id="308f6-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="308f6-859">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="308f6-860">Restituisce una stringa multivalore con 2 elementi utili per l'attributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="308f6-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="308f6-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="308f6-861">StringFromGuid</span></span>
<span data-ttu-id="308f6-862">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-862">**Description:**</span></span>  
<span data-ttu-id="308f6-863">La funzione StringFromGuid accetta un GUID binario e lo converte in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="308f6-864">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="308f6-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="308f6-865">StringFromSid</span></span>
<span data-ttu-id="308f6-866">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-866">**Description:**</span></span>  
<span data-ttu-id="308f6-867">La funzione StringFromSid converte una matrice di byte contenente un ID di sicurezza in una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="308f6-868">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="308f6-869">Switch</span><span class="sxs-lookup"><span data-stu-id="308f6-869">Switch</span></span>
<span data-ttu-id="308f6-870">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-870">**Description:**</span></span>  
<span data-ttu-id="308f6-871">La funzione Switch viene usata per restituire un singolo valore basato sulle condizioni valutate.</span><span class="sxs-lookup"><span data-stu-id="308f6-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="308f6-872">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="308f6-873">expr: espressione di tipo variant da valutare.</span><span class="sxs-lookup"><span data-stu-id="308f6-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="308f6-874">value: valore da restituire se l'espressione corrispondente è True.</span><span class="sxs-lookup"><span data-stu-id="308f6-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="308f6-875">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-875">**Remarks:**</span></span>  
<span data-ttu-id="308f6-876">L'elenco di argomenti della funzione Switch è costituito da coppie di espressioni e valori.</span><span class="sxs-lookup"><span data-stu-id="308f6-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="308f6-877">Le espressioni vengono valutate da sinistra a destra e viene restituito il valore associato alla prima espressione valutata in True.</span><span class="sxs-lookup"><span data-stu-id="308f6-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="308f6-878">Se le parti non vengono accoppiate correttamente, si verifica un errore di runtime.</span><span class="sxs-lookup"><span data-stu-id="308f6-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="308f6-879">Ad esempio, se expr1 è True, Switch restituisce value1.</span><span class="sxs-lookup"><span data-stu-id="308f6-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="308f6-880">Se expr-1 è False, ma expr-2 è True, Switch restituisce value-2 e così via.</span><span class="sxs-lookup"><span data-stu-id="308f6-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="308f6-881">Switch restituisce Nothing se:</span><span class="sxs-lookup"><span data-stu-id="308f6-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="308f6-882">Nessuna espressione è True.</span><span class="sxs-lookup"><span data-stu-id="308f6-882">None of the expressions are True.</span></span>
* <span data-ttu-id="308f6-883">La prima espressione True ha un valore corrispondente Null.</span><span class="sxs-lookup"><span data-stu-id="308f6-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="308f6-884">Switch valuta tutte le espressioni, anche se ne restituisce una sola.</span><span class="sxs-lookup"><span data-stu-id="308f6-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="308f6-885">Per questo motivo, è opportuno considerare attentamente gli effetti collaterali indesiderati.</span><span class="sxs-lookup"><span data-stu-id="308f6-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="308f6-886">Ad esempio, se la valutazione di un'espressione restituisce un errore di divisione per zero, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="308f6-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="308f6-887">Value può anche essere la funzione Error che restituirà una stringa personalizzata.</span><span class="sxs-lookup"><span data-stu-id="308f6-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="308f6-888">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="308f6-889">Restituisce la lingua parlata in alcune città importanti. In caso contrario restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="308f6-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="308f6-890">Trim</span><span class="sxs-lookup"><span data-stu-id="308f6-890">Trim</span></span>
<span data-ttu-id="308f6-891">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-891">**Description:**</span></span>  
<span data-ttu-id="308f6-892">La funzione Trim rimuove gli spazi vuoti iniziali e finali da una stringa.</span><span class="sxs-lookup"><span data-stu-id="308f6-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="308f6-893">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="308f6-894">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="308f6-895">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="308f6-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="308f6-896">Rimuove gli spazi iniziali e finali per ogni valore nell'attributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="308f6-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="308f6-897">UCase</span><span class="sxs-lookup"><span data-stu-id="308f6-897">UCase</span></span>
<span data-ttu-id="308f6-898">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-898">**Description:**</span></span>  
<span data-ttu-id="308f6-899">La funzione UCase converte tutti i caratteri in una stringa in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="308f6-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="308f6-900">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="308f6-901">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="308f6-902">Restituisce "test".</span><span class="sxs-lookup"><span data-stu-id="308f6-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="308f6-903">Where</span><span class="sxs-lookup"><span data-stu-id="308f6-903">Where</span></span>

<span data-ttu-id="308f6-904">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-904">**Description:**</span></span>  
<span data-ttu-id="308f6-905">Restituisce un subset di valori di un attributo multivalore, o dell'output di un'espressione, in base alla condizione specifica.</span><span class="sxs-lookup"><span data-stu-id="308f6-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="308f6-906">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="308f6-907">item: rappresenta un elemento nell'attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="308f6-908">attribute: l'attributo multivalore</span><span class="sxs-lookup"><span data-stu-id="308f6-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="308f6-909">condition: qualsiasi espressione che possa restituire true o false</span><span class="sxs-lookup"><span data-stu-id="308f6-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="308f6-910">expression: un'espressione che restituisce una raccolta di valori</span><span class="sxs-lookup"><span data-stu-id="308f6-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="308f6-911">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="308f6-912">Restituisce i valori del certificato non scaduti nell'attributo multivalore userCertificate.</span><span class="sxs-lookup"><span data-stu-id="308f6-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="308f6-913">With</span><span class="sxs-lookup"><span data-stu-id="308f6-913">With</span></span>
<span data-ttu-id="308f6-914">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-914">**Description:**</span></span>  
<span data-ttu-id="308f6-915">La funzione With consente di semplificare un'espressione complessa usando una variabile per rappresentare una sottoespressione che appare una o più volte nell'espressione complessa.</span><span class="sxs-lookup"><span data-stu-id="308f6-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="308f6-916">**Sintassi**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="308f6-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="308f6-917">variable: rappresenta la sottoespressione.</span><span class="sxs-lookup"><span data-stu-id="308f6-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="308f6-918">subExpression: sottoespressione rappresentata dalla variabile.</span><span class="sxs-lookup"><span data-stu-id="308f6-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="308f6-919">complexExpression: un'espressione complessa.</span><span class="sxs-lookup"><span data-stu-id="308f6-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="308f6-920">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="308f6-921">Dal punto di vista funzionale equivale a:</span><span class="sxs-lookup"><span data-stu-id="308f6-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="308f6-922">Che restituisce solo i valori del certificato non scaduti nell'attributo userCertificate.</span><span class="sxs-lookup"><span data-stu-id="308f6-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="308f6-923">Word</span><span class="sxs-lookup"><span data-stu-id="308f6-923">Word</span></span>
<span data-ttu-id="308f6-924">**Descrizione:**</span><span class="sxs-lookup"><span data-stu-id="308f6-924">**Description:**</span></span>  
<span data-ttu-id="308f6-925">La funzione Word restituisce una parola contenuta in una stringa, in base ai parametri che descrivono i delimitatori da usare e il numero della parola da restituire.</span><span class="sxs-lookup"><span data-stu-id="308f6-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="308f6-926">**Sintassi:**</span><span class="sxs-lookup"><span data-stu-id="308f6-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="308f6-927">string: stringa dalla quale restituire una parola.</span><span class="sxs-lookup"><span data-stu-id="308f6-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="308f6-928">WordNumber: numero che identifica il numero di parole da restituire.</span><span class="sxs-lookup"><span data-stu-id="308f6-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="308f6-929">delimiters: stringa che rappresenta uno o più delimitatori da usare per identificare le parole</span><span class="sxs-lookup"><span data-stu-id="308f6-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="308f6-930">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="308f6-930">**Remarks:**</span></span>  
<span data-ttu-id="308f6-931">Ogni stringa di caratteri contenuta nella stringa con valori separati da uno dei caratteri specificati nei delimitatori viene identificata come una parola:</span><span class="sxs-lookup"><span data-stu-id="308f6-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="308f6-932">Se number è < 1, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="308f6-933">Se string è Null, restituisce una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="308f6-934">Se la stringa contiene meno delle parole specificate in number o se non contiene alcuna parola identificata da delimiters, viene restituita una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="308f6-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="308f6-935">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="308f6-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="308f6-936">Restituisce "brown"</span><span class="sxs-lookup"><span data-stu-id="308f6-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="308f6-937">Restituisce "has"</span><span class="sxs-lookup"><span data-stu-id="308f6-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="308f6-938">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="308f6-938">Additional Resources</span></span>
* [<span data-ttu-id="308f6-939">Informazioni sulle espressioni di provisioning dichiarativo</span><span class="sxs-lookup"><span data-stu-id="308f6-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="308f6-940">Servizio di sincronizzazione Azure AD Connect: Personalizzazione delle opzioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="308f6-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="308f6-941">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="308f6-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
