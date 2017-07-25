<span data-ttu-id="6907b-p107">Если вызвать метод ServiceScope.consume() до вызова метода finish(), возникнет ошибка. Самый надежный способ защитить компонент от этой ошибки — вызывать метод consume() из функции обратного вызова whenFinished(). Если область службы уже готова, обратный вызов будет выполнен немедленно. В противном случае он будет выполнен позже, когда создание области будет завершено.</span><span class="sxs-lookup"><span data-stu-id="6907b-p107">It is an error to call ServiceScope.consume() before finish() has been called. The most reliable way to protect your component against this error is to perform the consume() calls inside a whenFinished() callback. If the service scope is already finished, then the callback will be executed immediately; otherwise, it will be executed later when the scope is finished.</span></span> |
|[`whenFinished(callback)`](whenfinished-servicescope.md)     | `public` | `void` | Если вызвать метод ServiceScope.consume() до вызова метода finish(), возникнет ошибка. Самый надежный способ защитить компонент от этой ошибки — вызывать метод consume() из функции обратного вызова whenFinished(). Если область службы уже готова, обратный вызов будет выполнен немедленно. В противном случае он будет выполнен позже, когда создание области будет завершено. |





