---
title: "Настройка среды разработки клиентских веб-частей SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c7e48ed9dfc32d4e7aa04502507d0df532e8ed50
ms.sourcegitcommit: 53385f08de7c705ba76c6e4985c33d27ee76307e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2017
---
# <a name="set-up-your-sharepoint-client-side-web-part-development-environment"></a>Как настроить среду разработки клиентских веб-частей SharePoint

Для создания клиентских веб-частей SharePoint можно использовать Visual Studio или другую среду разработки. Вы можете использовать компьютер Mac либо компьютер под управлением Windows или Linux.

>**Примечание.** Прежде чем выполнять действия, указанные в этой статье, обязательно [настройте клиент Office 365](./set-up-your-developer-tenant.md).

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1).

<a href="https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="install-developer-tools"></a>Установка средств разработчика

### <a name="nodejs"></a>NodeJS

Установка [NodeJS версии 6.x](https://nodejs.org/download/release/latest-v6.x/). 

* Если у вас Windows, используйте установщики msi, чтобы было проще настроить NodeJS. Эти установщики можно скачать, перейдя по указанной выше ссылке.
* Если у вас уже установлена платформа NodeJS, убедитесь, что установлена последняя версия, с помощью команды `node -v`. Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/). 
* Если вы используете компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/). 

>**Примечание.** Конвейер сборки SharePoint Framework сейчас не поддерживает версию LTS Node.js. Скачайте [Node.js версии 6.11.5](https://nodejs.org/download/release/latest-v6.x/). При этом установится npm 3.10.10. Обратите внимание, что вы используете npm версии 5.x. Необходимо перейти на более раннюю версию npm, выполнив команду `npm install -g npm@3`.

### <a name="code-editors"></a>Редакторы кода

Установите редактор кода. Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:

* [Visual Studio Code](https://code.visualstudio.com/);
* [Atom](https://atom.io);
* [Webstorm](https://www.jetbrains.com/webstorm).

В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор.

### <a name="if-you-are-using-ubuntu"></a>Если используется Ubuntu

Необходимо установить средства компиляции с помощью следующей команды:

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a>Если используется Fedora

Необходимо установить средства компиляции с помощью следующей команды:

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a>Установка Yeoman и gulp

[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы. Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей. Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.

Чтобы установить Yeoman и gulp, введите следующую команду:

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a>Установка генератора Yeoman для SharePoint

С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.

Чтобы глобально установить генератор Yeoman для SharePoint Framework, введите такую команду:

```sh
npm install -g @microsoft/generator-sharepoint
```

Чтобы можно было переходить между различными проектами, созданными с помощью разных версий генератора Yeoman для SharePoint, установите генератор локально как зависимость разработки в папке проекта с помощью такой команды:

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a>Дополнительные средства

Вам также могут пригодиться следующие средства:

* [Fiddler](http://www.telerik.com/fiddler)
* [Подключаемый модуль Postman для Chrome](https://www.getpostman.com/docs/introduction)
* [Cmder для Windows](http://cmder.net/)
* [Oh My Zsh для Mac](http://ohmyz.sh/)
* [Службы управления версиями Git](https://git-scm.com/)

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part.md)!
