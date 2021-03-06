---
title: Mise en forme de plages sur une jauge (Générateur de rapports et SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3b332d8470c9a7502a168863a48b08c4d3f24e47
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285357"
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>Mise en forme de plages sur une jauge (Générateur de rapports et SSRS)
 Dans un rapport paginé [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , une plage de jauge est une zone ou une partie de l’échelle de la jauge qui indique une sous-section importante de valeurs sur la jauge. Une plage de jauge vous permet d'indiquer visuellement lorsque la valeur de pointeur entre dans une certaine plage de valeurs. Les plages sont délimitées par une valeur de début et une valeur de fin.  
  
 Vous pouvez également utiliser des plages pour définir des différentes sections d'une jauge. Par exemple, sur une jauge dont les valeurs vont de 0 à 10, vous pouvez définir une plage rouge pour les valeurs de 0 à 3, une plage jaune pour les valeurs de 4 à 7 et une plage verte pour les valeurs de 8 à 10. Si la valeur de début que vous avez spécifiée est supérieure à la valeur de fin spécifiée, les valeurs sont inversées, la valeur de début devenant alors la valeur de fin et vice versa.  
  
 Vous pouvez positionner la plage comme vous positionnez des pointeurs sur une échelle. Les propriétés **Position** et **Distance par rapport à l’échelle** déterminent la position de la plage. Pour plus d’informations, consultez [Jauges &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a> Voir aussi  
 [Mise en forme des échelles sur une jauge &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Mise en forme des pointeurs sur une jauge &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Définir un minimum ou un maximum sur une jauge &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Didacticiel : Ajouter un indicateur de performance clé à un rapport &#40;Générateur de rapports&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Jauges &#40;Générateur de rapports et SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
