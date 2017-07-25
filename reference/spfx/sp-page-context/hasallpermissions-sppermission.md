# <a name="hasallpermissionsrequestedperms"></a><span data-ttu-id="9932e-101">hasAllPermissions(...requestedPerms)</span><span class="sxs-lookup"><span data-stu-id="9932e-101">hasAllPermissions(...requestedPerms)</span></span>




<span data-ttu-id="9932e-102">Эта функция определяет, есть ли в заданной маске разрешений все запрашиваемые разрешения.</span><span class="sxs-lookup"><span data-stu-id="9932e-102">Function for determining if a given permission mask has all of the requested permissions.</span></span>

<span data-ttu-id="9932e-103">**Подпись:** _public hasAllPermissions(...requestedPerms: [SPPermission](../sp-page-context/sppermission.md)[]): boolean;_</span><span class="sxs-lookup"><span data-stu-id="9932e-103">**Signature:** _public hasAllPermissions(...requestedPerms: [SPPermission](../sp-page-context/sppermission.md)[]): boolean;_</span></span>

<span data-ttu-id="9932e-104">**Что возвращается**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="9932e-104">**Returns**: `boolean`</span></span>





#### <a name="parameters"></a><span data-ttu-id="9932e-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="9932e-105">Parameters</span></span>


| <span data-ttu-id="9932e-106">Параметр</span><span class="sxs-lookup"><span data-stu-id="9932e-106">Parameter</span></span>    | <span data-ttu-id="9932e-107">Тип</span><span class="sxs-lookup"><span data-stu-id="9932e-107">Type</span></span>    | <span data-ttu-id="9932e-108">Описание</span><span class="sxs-lookup"><span data-stu-id="9932e-108">Description</span></span> |
|:-------------|:---------------|:------------|
| `...requestedPerms`    | <span data-ttu-id="9932e-109">[`SPPermission`](../sp-page-context/sppermission.md)[]</span><span class="sxs-lookup"><span data-stu-id="9932e-109"></span></span> | <span data-ttu-id="9932e-110">Любое количество объектов SPPermission для сравнения с оригиналом.</span><span class="sxs-lookup"><span data-stu-id="9932e-110">Any number of SPPermission objects to be compared against the original</span></span> |


