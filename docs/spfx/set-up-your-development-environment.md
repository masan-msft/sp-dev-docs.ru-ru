# <a name="set-up-your-sharepoint-client-side-web-part-development-environment"></a>Настройка среды разработки клиентских веб-частей SharePoint

Для создания клиентских веб-частей SharePoint можно использовать Visual Studio или другую среду разработки. Вы можете использовать компьютер Mac либо компьютер под управлением Windows или Linux.

>**Примечание.** Прежде чем выполнять действия, указанные в этой статье, обязательно [настройте клиент Office 365](./set-up-your-developer-tenant).

Эти действия также показаны в видео [канала YouTube, посвященного SharePoint PnP](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1). 

<a href="https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
    <img src="../../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="install-developer-tools"></a>Установка средств разработчика

### <a name="nodejs"></a>NodeJS
Установите [NodeJS](https://nodejs.org/en/) с долгосрочной поддержкой (LTS).

* Если у вас уже установлена библиотека NodeJS, убедитесь, что установлена последняя версия, с помощью команды `node -v`. Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/). 
* Если вы используете компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/). 

> Обратите внимание на то, что конвейер сборки SPFx сейчас **НЕ** поддерживает npm 5.x, поэтому нужна версия 3 или 4. На момент написания этой статьи LTS-версия NodeJS (6.11.0) устанавливает npm 3.10.10. Когда изменится ситуация с поддержкой, мы добавим соответствующие сведения в этот раздел. Вы можете перейти на использование более ранней версии npm с помощью команды `npm install -g npm@3`.

### <a name="code-editors"></a>Редакторы кода
Установите редактор кода. Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:

* [Visual Studio Code](https://code.visualstudio.com/);
* [Atom](https://atom.io);
* [Webstorm](https://www.jetbrains.com/webstorm). 

В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор. 

### <a name="if-you-are-using-ubuntu"></a>Если используется Ubuntu

Необходимо установить средства компиляции с помощью следующей команды:
    
```
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a>Если используется Fedora

Необходимо установить средства компиляции с помощью следующей команды:
    
```
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a>Установка Yeoman и gulp

[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы. Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей. Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.

Чтобы установить Yeoman и gulp, введите следующую команду:
    
```
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a>Установка генератора Yeoman для SharePoint

С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.

Чтобы установить генератор yeoman для SharePoint, введите следующую команду:
    
```
npm install -g @microsoft/generator-sharepoint 
```
>**Примечание.** Генератор yeoman для SharePoint должен развертываться глобально с первой общедоступной версией. Существуют известные проблемы при локальной установке в проекте, которые планируется устранить после выпуска общедоступной версии.


## <a name="optional-tools"></a>Дополнительные средства

Вам также могут пригодиться следующие средства:

* [Fiddler](http://www.telerik.com/fiddler)
* [Подключаемый модуль Postman для Chrome](https://www.getpostman.com/docs/introduction)
* [Cmder для Windows](http://cmder.net/)
* [Oh My Zsh для Mac](http://ohmyz.sh/)
* [Службы управления версиями Git](https://git-scm.com/)

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part)!
