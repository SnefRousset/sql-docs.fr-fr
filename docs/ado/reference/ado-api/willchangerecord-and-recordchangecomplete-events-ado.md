---
title: "WillChangeRecord et RecordChangeComplete, événements (ADO) | Documents Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b72e7f1a2e69b23f9c696a5ce544153a5a0e8a3e
ms.contentlocale: fr-fr
ms.lasthandoff: 09/09/2017

---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord et RecordChangeComplete, événements (ADO)
Le **WillChangeRecord** événement est appelé avant qu’un ou plusieurs enregistrements (lignes) le [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) modifier. Le **RecordChangeComplete** événement est appelé après un ou plusieurs enregistrements changent.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Paramètres  
 *adReason*  
 Un [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valeur qui spécifie la raison de cet événement. Sa valeur peut être **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, ou **adRsnFirstChange**.  
  
 *cRecords*  
 A **Long** valeur qui indique le nombre d’enregistrements de modification (affectés).  
  
 *pError*  
 Un [erreur](../../../ado/reference/ado-api/error-object.md) objet. Elle décrit l’erreur qui s’est produite si la valeur de *ne* est **contraire**; sinon, elle n’est pas définie.  
  
 *N'*  
 Un [il ne](../../../ado/reference/ado-api/eventstatusenum.md) valeur d’état.  
  
 Lorsque **WillChangeRecord** est appelée, ce paramètre est défini sur **adStatusOK** si l’opération qui a provoqué l’événement a réussi. Il est défini sur **adStatusCantDeny** si cet événement ne peut pas demander l’annulation de l’opération en attente.  
  
 Lorsque **RecordChangeComplete** est appelée, ce paramètre est défini sur **adStatusOK** si l’opération qui a provoqué l’événement a réussi, ou pour **contraire** si l’opération a échoué.  
  
 Avant de **WillChangeRecord** retourne, définissez ce paramètre sur **adStatusCancel** pour demander l’annulation de l’opération qui a provoqué cet événement ou ce paramètre la valeur ** adStatusUnwantedEvent** pour éviter toute notification.  
  
 Avant de **RecordChangeComplete** retourne, définissez ce paramètre sur **adStatusUnwantedEvent** pour éviter toute notification.  
  
 *Connection*  
 A **Recordset** objet. Le **Recordset** pour laquelle cet événement s’est produit.  
  
## <a name="remarks"></a>Notes  
 A **WillChangeRecord** ou **RecordChangeComplete** événement peut se produire pour le premier champ modifié dans une ligne en raison de ce qui suit **Recordset** operations : [ Mise à jour](../../../ado/reference/ado-api/update-method.md), [supprimer](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), et [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). La valeur de la **Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) détermine les opérations qui déclenchent les événements se produisent.  
  
 Lors de la **WillChangeRecord** événement, le **Recordset** [filtre](../../../ado/reference/ado-api/filter-property.md) est définie sur **adFilterAffectedRecords**. Vous ne pouvez pas modifier cette propriété lors du traitement de l’événement.  
  
 Vous devez définir le **ne** paramètre **adStatusUnwantedEvent** pour chaque possible **adReason** valeur arrêter complètement la notification d’événement pour tout événement qui inclut un **adReason** paramètre.  
  
## <a name="see-also"></a>Voir aussi  
 [Exemple de modèle d’événements ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Résumé du Gestionnaire d’événements ADO](../../../ado/guide/data/ado-event-handler-summary.md)