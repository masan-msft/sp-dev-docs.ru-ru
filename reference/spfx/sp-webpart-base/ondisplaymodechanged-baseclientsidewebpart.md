# <a name="ondisplaymodechangedolddisplaymode"></a>onDisplayModeChanged(oldDisplayMode)




Этот API вызывается при изменении режима отображения веб-части. Версия этого API по умолчанию вызывает метод render, чтобы обновить веб-часть. Если разработчик веб-части не хочет, чтобы после изменения режима отображения происходило полное обновление, он может переопределить этот API и выполнить обновления модели DOM веб-части, чтобы изменить режим отображения.

**Подпись:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_

**Что возвращается**: `void`





#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `oldDisplayMode`    | [`DisplayMode`](../sp-core-library/displaymode.md) | Старый режим отображения. |


