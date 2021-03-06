---
title: Propriété Description | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9a97e1e63e3896cd451c68d6198baa991945e7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704518"
---
# <a name="description-property"></a>Description, propriété
Décrit un [erreur](../../../ado/reference/ado-api/error-object.md) objet.  
  
## <a name="return-value"></a>Valeur de retour  
 Retourne un **chaîne** valeur qui contient une description de l’erreur.  
  
## <a name="remarks"></a>Notes  
 Utilisez le **Description** propriété pour obtenir une brève description de l’erreur. Afficher cette propriété pour avertir l’utilisateur d’une erreur que vous ne pouvez pas ou ne souhaitez pas gérer. La chaîne proviendront de ADO ou un fournisseur.  
  
 Les fournisseurs sont chargés de transmettre le texte d’erreur spécifique à ADO. ADO ajoute un [erreur](../../../ado/reference/ado-api/error-object.md) de l’objet à la **erreurs** collection pour chaque fournisseur d’erreur ou avertissement de reçu. Énumérer les **erreurs** collection pour identifier les erreurs par le fournisseur transmet.  
  
## <a name="applies-to"></a>S'applique à  
 [Error, objet](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Description, HelpContext, HelpFile, NativeError, nombre, Source et SQLState, propriétés-exemple (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, nombre, Source et SQLState, propriétés-exemple (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext, HelpFile, propriétés](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number, propriété (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source, propriété (objet Error ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
