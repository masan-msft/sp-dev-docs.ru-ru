---
title: "Как настроить среду разработки SharePoint Framework"
ms.date: 12/11/2017
ms.prod: sharepoint
ms.openlocfilehash: 1259ceae3b13efdd0d359734fef6d080696a2c6a
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a>Как настроить среду разработки SharePoint Framework

Создавать решения SharePoint Framework можно в Visual Studio или другой среде разработки. Вы можете использовать компьютер Mac либо компьютер под управлением Windows или Linux.

>**Примечание.** Прежде чем выполнять действия, указанные в этой статье, обязательно [настройте клиент Office 365](./set-up-your-developer-tenant.md).

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).

<a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
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

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint в [репозитории sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!