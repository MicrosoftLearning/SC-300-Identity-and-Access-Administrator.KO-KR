---
title: 온라인 호스팅 지침
permalink: index.html
layout: home
ms.openlocfilehash: 3f1d9eb9d23b41f212641797985d518792859159
ms.sourcegitcommit: 317faec6fdf204c92dfe1461d4a30f5b8d8ea950
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2022
ms.locfileid: "138357271"
---
# <a name="content-directory"></a>콘텐츠 디렉터리

필요한 랩 파일은 [여기서 다운로드](https://github.com/MicrosoftLearning/SC-300-Identity-and-Access-Administrator/archive/master.zip)할 수 있습니다.

다음은 각 랩 연습 및 데모의 하이퍼링크입니다.

## <a name="labs"></a>랩

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| 모듈 | 랩 |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
