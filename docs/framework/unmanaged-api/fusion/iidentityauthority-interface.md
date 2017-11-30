---
title: IIdentityAuthority, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IIdentityAuthority
api_location: fusion.dll
api_type: COM
f1_keywords: IIdentityAuthority
helpviewer_keywords: IIdentityAuthority interface [.NET Framework fusion]
ms.assetid: 6277f914-51a8-49be-bec6-52d6d648527d
topic_type: apiref
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: c3f38d932fa0376186e2c22232d21857d5fa128f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="iidentityauthority-interface"></a><span data-ttu-id="4bebe-102">IIdentityAuthority, interface</span><span class="sxs-lookup"><span data-stu-id="4bebe-102">IIdentityAuthority Interface</span></span>
<span data-ttu-id="4bebe-103">Gère les clés d’identité pour les objets de code.</span><span class="sxs-lookup"><span data-stu-id="4bebe-103">Manages identity keys for code objects.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="4bebe-104">Méthodes</span><span class="sxs-lookup"><span data-stu-id="4bebe-104">Methods</span></span>  
  
|<span data-ttu-id="4bebe-105">Méthode</span><span class="sxs-lookup"><span data-stu-id="4bebe-105">Method</span></span>|<span data-ttu-id="4bebe-106">Description</span><span class="sxs-lookup"><span data-stu-id="4bebe-106">Description</span></span>|  
|------------|-----------------|  
|`IIdentityAuthority::AreDefinitionsEqual`|<span data-ttu-id="4bebe-107">Obtient une valeur qui indique si les deux spécifiés [IDefinitionIdentity](../../../../docs/framework/unmanaged-api/fusion/idefinitionidentity-interface.md) instances sont égales.</span><span class="sxs-lookup"><span data-stu-id="4bebe-107">Gets a value that indicates whether the two specified [IDefinitionIdentity](../../../../docs/framework/unmanaged-api/fusion/idefinitionidentity-interface.md) instances are equal.</span></span>|  
|`IIdentityAuthority::AreReferencesEqual`|<span data-ttu-id="4bebe-108">Obtient une valeur qui indique si les deux spécifiés [IReferenceIdentity](../../../../docs/framework/unmanaged-api/fusion/ireferenceidentity-interface.md) instances sont égales.</span><span class="sxs-lookup"><span data-stu-id="4bebe-108">Gets a value that indicates whether the two specified [IReferenceIdentity](../../../../docs/framework/unmanaged-api/fusion/ireferenceidentity-interface.md) instances are equal.</span></span>|  
|`IIdentityAuthority::AreTextualDefinitionsEqual`|<span data-ttu-id="4bebe-109">Obtient une valeur qui indique si les deux représentations sous forme de chaîne spécifiée définition identity sont égaux.</span><span class="sxs-lookup"><span data-stu-id="4bebe-109">Gets a value that indicates whether the two specified string definition identity representations are equal.</span></span>|  
|`IIdentityAuthority::AreTextualReferencesEqual`|<span data-ttu-id="4bebe-110">Obtient une valeur qui indique si les deux représentations sous forme de chaîne spécifiée référence identité sont égaux.</span><span class="sxs-lookup"><span data-stu-id="4bebe-110">Gets a value that indicates whether the two specified string reference identity representations are equal.</span></span>|  
|`IIdentityAuthority::CreateDefinition`|<span data-ttu-id="4bebe-111">Obtient un pointeur vers un nouveau `IDefinitionIdentity` instance qui représente l’objet de code dans la portée actuelle.</span><span class="sxs-lookup"><span data-stu-id="4bebe-111">Gets a pointer to a new `IDefinitionIdentity` instance that represents the code object in the current scope.</span></span>|  
|`IIdentityAuthority::CreateReference`|<span data-ttu-id="4bebe-112">Obtient un pointeur vers un nouveau `IReferenceIdentity` instance qui représente l’objet de code dans la portée actuelle.</span><span class="sxs-lookup"><span data-stu-id="4bebe-112">Gets a pointer to a new `IReferenceIdentity` instance that represents the code object in the current scope.</span></span>|  
|`IIdentityAuthority::DefinitionToText`|<span data-ttu-id="4bebe-113">Obtient une version de la chaîne mise en forme du `IDefinitionIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-113">Gets a formatted string version of the specified `IDefinitionIdentity`.</span></span>|  
|`IIdentityAuthority::DefinitionToTextBuffer`|<span data-ttu-id="4bebe-114">Remplit la mémoire tampon de caractères larges spécifié avec une version de chaîne de l’objet `IDefinitionIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-114">Fills the specified wide character buffer with a string version of the specified `IDefinitionIdentity`.</span></span>|  
|`IIdentityAuthority::DoesDefinitionMatchReference`|<span data-ttu-id="4bebe-115">Obtient une valeur qui indique si le texte spécifié `IDefinitionIdentity` et `IReferenceIdentity` instances font référence au même objet de code.</span><span class="sxs-lookup"><span data-stu-id="4bebe-115">Gets a value that indicates whether the specified `IDefinitionIdentity` and `IReferenceIdentity` instances refer to the same code object.</span></span>|  
|`IIdentityAuthority::DoesTextualDefinitionMatchTextualReference`|<span data-ttu-id="4bebe-116">Obtient une valeur qui indique si les chaînes spécifiées font référence au même objet de code.</span><span class="sxs-lookup"><span data-stu-id="4bebe-116">Gets a value that indicates whether the specified strings refer to the same code object.</span></span>|  
|`IIdentityAuthority::GenerateDefinitionKey`|<span data-ttu-id="4bebe-117">Obtient un pointeur vers une clé de chaîne qui vient d’être créée pour spécifié `IDefinitionIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-117">Gets a pointer to a newly created string key for the specified `IDefinitionIdentity`.</span></span>|  
|`IIdentityAuthority::GenerateReferenceKey`|<span data-ttu-id="4bebe-118">Obtient un pointeur vers une clé de chaîne qui vient d’être créée pour spécifié `IReferenceIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-118">Gets a pointer to a newly created string key for the specified `IReferenceIdentity`.</span></span>|  
|`IIdentityAuthority::HashDefinition`|<span data-ttu-id="4bebe-119">Obtient une valeur de hachage spécifié `IDefinitionIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-119">Gets a hash value for the specified `IDefinitionIdentity`.</span></span>|  
|`IIdentityAuthority::HashReference`|<span data-ttu-id="4bebe-120">Obtient une valeur de hachage spécifié `IreferenceIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-120">Gets a hash value for the specified `IreferenceIdentity`.</span></span>|  
|`IIdentityAuthority::ReferenceToText`|<span data-ttu-id="4bebe-121">Obtient une version de la chaîne mise en forme du `IReferenceIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-121">Gets a formatted string version of the specified `IReferenceIdentity`.</span></span>|  
|`IIdentityAuthority::ReferenceToTextBuffer`|<span data-ttu-id="4bebe-122">Remplit la mémoire tampon de caractères larges spécifié avec une version de chaîne de l’objet `IReferenceIdentity`.</span><span class="sxs-lookup"><span data-stu-id="4bebe-122">Fills the specified wide character buffer with a string version of the specified `IReferenceIdentity`.</span></span>|  
|`IIdentityAuthority::TextToDefinition`|<span data-ttu-id="4bebe-123">Obtient un pointeur d’interface vers un `IDefinitionIdentity` instance générée à partir de la chaîne de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4bebe-123">Gets an interface pointer to an `IDefinitionIdentity` instance generated from the specified formatted string.</span></span>|  
|`IIdentityAuthority::TextToReference`|<span data-ttu-id="4bebe-124">Obtient un pointeur d’interface vers un `IReferenceIdentity` instance générée à partir de la chaîne de mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4bebe-124">Gets an interface pointer to an `IReferenceIdentity` instance generated from the specified formatted string.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="4bebe-125">Spécifications</span><span class="sxs-lookup"><span data-stu-id="4bebe-125">Requirements</span></span>  
 <span data-ttu-id="4bebe-126">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4bebe-126">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4bebe-127">**En-tête :** Isolation.h</span><span class="sxs-lookup"><span data-stu-id="4bebe-127">**Header:** Isolation.h</span></span>  
  
 <span data-ttu-id="4bebe-128">**Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4bebe-128">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4bebe-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4bebe-129">See Also</span></span>  
 [<span data-ttu-id="4bebe-130">Interfaces de fusion</span><span class="sxs-lookup"><span data-stu-id="4bebe-130">Fusion Interfaces</span></span>](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)