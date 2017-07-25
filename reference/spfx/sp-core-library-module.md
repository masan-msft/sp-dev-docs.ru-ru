<span data-ttu-id="46e8b-p108">Этот класс представляет версии в строковом формате MAJOR.MINOR[.PATCH[.REVISION]], где MAJOR, MINOR, PATCH и REVISION — это целые числа. Параметры PATCH и REVISION — необязательные. Значения могут начинаться с нуля, но это никак не влияет на сравнение. Примеры: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004</span><span class="sxs-lookup"><span data-stu-id="46e8b-p108">This class represents versions that follow the string format of MAJOR.MINOR[.PATCH[.REVISION]] where MAJOR, MINOR, PATCH and REVISION are integers. PATCH and REVISION are optional. Leading zeros are allowed, but have no meaning in comparisons. Examples: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004</span></span> |
| [`Version`](./sp-core-library/version.md)     | Этот класс представляет версии в строковом формате MAJOR.MINOR[.PATCH[.REVISION]], где MAJOR, MINOR, PATCH и REVISION — это целые числа. Параметры PATCH и REVISION — необязательные. Значения могут начинаться с нуля, но это никак не влияет на сравнение. Примеры: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004 |



## <a name="interfaces"></a><span data-ttu-id="46e8b-154">Интерфейсы</span><span class="sxs-lookup"><span data-stu-id="46e8b-154">Interfaces</span></span>

| <span data-ttu-id="46e8b-155">Интерфейс</span><span class="sxs-lookup"><span data-stu-id="46e8b-155">Interface</span></span>    |  <span data-ttu-id="46e8b-156">Описание</span><span class="sxs-lookup"><span data-stu-id="46e8b-156">Description</span></span> |
|:-------------|:---------------|
| [`IRandomNumberGenerator`](./sp-core-library/irandomnumbergenerator.md)   | <span data-ttu-id="46e8b-157">Это интерфейс ServiceScope, который позволяет модульным тестам предоставлять детерминированный источник псевдослучайных чисел.</span><span class="sxs-lookup"><span data-stu-id="46e8b-157">This is a ServiceScope interface that enables unit tests to provide a deterministic source of pseudorandom numbers.</span></span>  |
| [`IServiceCollection`](./sp-core-library/iservicecollection.md)   | <span data-ttu-id="46e8b-158">Сокращенный шаблон для извлечения известных служб из объекта ServiceScope.</span><span class="sxs-lookup"><span data-stu-id="46e8b-158">A shorthand pattern for extracting well-known services from a ServiceScope.</span></span>  |
| [`ITimeProvider`](./sp-core-library/itimeprovider.md)   | <span data-ttu-id="46e8b-159">Это интерфейс ServiceScope, который позволяет модульным тестам имитировать системные часы.</span><span class="sxs-lookup"><span data-stu-id="46e8b-159">This is a ServiceScope interface that enables unit tests to simulate the system clock.</span></span>  |



## <a name="enumerations"></a><span data-ttu-id="46e8b-160">Перечисления</span><span class="sxs-lookup"><span data-stu-id="46e8b-160">Enumerations</span></span>

| <span data-ttu-id="46e8b-161">Перечисление</span><span class="sxs-lookup"><span data-stu-id="46e8b-161">Enumeration</span></span>      | <span data-ttu-id="46e8b-162">Описание</span><span class="sxs-lookup"><span data-stu-id="46e8b-162">Description</span></span>|
|:-----------|:------------|
|[`DisplayMode`](./sp-core-library/displaymode.md)    | <span data-ttu-id="46e8b-163">DisplayMode обозначает режим отображения страницы и/или ее содержимого (например, текста и веб-частей).</span><span class="sxs-lookup"><span data-stu-id="46e8b-163">DisplayMode indicates the mode in which a page and/or its contents (e.g. text and web parts) are dislayed.</span></span> |
|[`EnvironmentType`](./sp-core-library/environmenttype.md)    | <span data-ttu-id="46e8b-164">Перечисление, описывающее тип среды, в которой работает платформа.</span><span class="sxs-lookup"><span data-stu-id="46e8b-164">An enum that describes which type of enviroment the framework is running in.</span></span> |




