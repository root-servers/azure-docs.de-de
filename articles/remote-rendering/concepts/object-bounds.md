---
title: Objektbegrenzungen
description: Es wird beschrieben, wie räumliche Objektbegrenzungen abgefragt werden können.
author: florianborn71
ms.author: flborn
ms.date: 02/03/2020
ms.topic: conceptual
ms.custom: devx-track-csharp
ms.openlocfilehash: 099b0175b906e48034e663b575517e49bce7e753
ms.sourcegitcommit: 419cf179f9597936378ed5098ef77437dbf16295
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89021849"
---
# <a name="object-bounds"></a>Objektbegrenzungen

Bei Objektbegrenzungen handelt es sich um den Umfang, der von einer [Entität](entities.md) und ihren untergeordneten Elementen belegt wird. In Azure Remote Rendering werden Objektbegrenzungen immer als *an Achsen ausgerichteter Begrenzungsrahmen* (Axis-Aligned Bounding Box, AABB) bereitgestellt. Objektbegrenzungen können sich entweder im *lokalen Raum* oder im *allgemeinen Raum* befinden. In beiden Fällen sind sie immer an den Achsen ausgerichtet. Dies bedeutet, dass sich Ausmaß und Umfang für die Darstellung im lokalen und im allgemeinen Raum unterscheiden können.

## <a name="querying-object-bounds"></a>Abfragen von Objektbegrenzungen

Der lokale Begrenzungsrahmen (AABB) eines [Gittermodells](meshes.md) kann direkt über die Gittermodellressource abgefragt werden. Diese Begrenzungen können über die Transformation der Entität in den lokalen oder allgemeinen Raum einer Entität transformiert werden.

Es ist möglich, auf diese Weise die Begrenzungen einer gesamten Objekthierarchie zu berechnen. Hierfür muss aber die Hierarchie durchlaufen werden, und die Begrenzungen jedes Gittermodells müssen abgefragt und manuell kombiniert werden. Dieser Vorgang ist sowohl aufwendig als auch ineffizient.

Eine bessere Möglichkeit ist das Aufrufen von `QueryLocalBoundsAsync` oder `QueryWorldBoundsAsync` für eine Entität. Die Berechnung wird dann auf den Server verlagert, und das Ergebnis wird mit minimaler Verzögerung zurückgegeben.

```cs
private BoundsQueryAsync _boundsQuery = null;

public void GetBounds(Entity entity)
{
    _boundsQuery = entity.QueryWorldBoundsAsync();
    _boundsQuery.Completed += (BoundsQueryAsync bounds) =>
    {
        if (bounds.IsRanToCompletion)
        {
            Double3 aabbMin = bounds.Result.min;
            Double3 aabbMax = bounds.Result.max;
            // ...
        }
    };
}
```

```cpp
void GetBounds(ApiHandle<Entity> entity)
{
    ApiHandle<BoundsQueryAsync> boundsQuery = *entity->QueryWorldBoundsAsync();
    boundsQuery->Completed([](ApiHandle<BoundsQueryAsync> bounds)
    {
        if (bounds->GetIsRanToCompletion())
        {
            Double3 aabbMin = bounds->GetResult().min;
            Double3 aabbMax = bounds->GetResult().max;
            // ...
        }
    });
}
```

## <a name="next-steps"></a>Nächste Schritte

* [Räumliche Abfragen](../overview/features/spatial-queries.md)
