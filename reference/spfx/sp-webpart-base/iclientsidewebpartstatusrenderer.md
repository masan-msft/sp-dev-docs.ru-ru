# <a name="iclientsidewebpartstatusrenderer-interface"></a><span data-ttu-id="aff03-101">Интерфейс IClientSideWebPartStatusRenderer</span><span class="sxs-lookup"><span data-stu-id="aff03-101">IClientSideWebPartStatusRenderer interface</span></span>







<span data-ttu-id="aff03-102">Интерфейс компонента, который должен отображать индикатор загрузки и сообщения об ошибках для веб-части.</span><span class="sxs-lookup"><span data-stu-id="aff03-102">Interface to be implemented by a component that should display the loading indicator and error messages for a webpart.</span></span>







## <a name="methods"></a><span data-ttu-id="aff03-103">Методы</span><span class="sxs-lookup"><span data-stu-id="aff03-103">Methods</span></span>

| <span data-ttu-id="aff03-104">Метод</span><span class="sxs-lookup"><span data-stu-id="aff03-104">Method</span></span>       |  <span data-ttu-id="aff03-105">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="aff03-105">Returns</span></span>   | <span data-ttu-id="aff03-106">Описание</span><span class="sxs-lookup"><span data-stu-id="aff03-106">Description</span></span>|
|:-------------|:-------|:-----------|
|[`clearError(domElement)`](clearerror-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="aff03-107">Удаление сообщения об ошибке веб-части.</span><span class="sxs-lookup"><span data-stu-id="aff03-107">Clear the webpart error message.</span></span> |
|[`clearLoadingIndicator(domElement)`](clearloadingindicator-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="aff03-108">Удаление индикатора загрузки.</span><span class="sxs-lookup"><span data-stu-id="aff03-108">Clear the loading indicator.</span></span> |
|[`displayLoadingIndicator(domElement,loadingMessage,timeout)`](displayloadingindicator-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="aff03-109">Отображение индикатора загрузки.</span><span class="sxs-lookup"><span data-stu-id="aff03-109">Display a loading spinner.</span></span> |
|[`renderError(domElement,error)`](rendererror-iclientsidewebpartstatusrenderer.md)      | `void` | <span data-ttu-id="aff03-110">Отображение указанного сообщения об ошибке в контейнере веб-части div.</span><span class="sxs-lookup"><span data-stu-id="aff03-110">Render the provided error message in the webpart container div.</span></span> |




