# Функционально-Легкий JavaScript

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-blue.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<a href="https://leanpub.com/fljs"><img src="manuscript/images/marketing/front-cover-small.png" width="25%" align="right" hspace="20" vspace="20" title="Functional-Light JavaScript" alt="Book Cover"></a>

Эта книга представляет собой сбалансированный и прагматичный взгляд на Функциональное Программирование на языке JavaScript. Здесь вы можете прочесть первое издание, либо купить книгу онлайн:

<p align="center">
    <a href="https://leanpub.com/fljs"><img src="https://img.shields.io/badge/Buy-Leanpub-yellow.svg" title="Купить на Leanpub" alt="Купить на Leanpub"></a> <a href="http://amazon.fljsbook.com"><img src="https://img.shields.io/badge/Buy-Amazon-yellow.svg" title="Купить на Amazon" alt="Купить на Amazon"></a>
</p>

"Функционально-Лёгкий JavaScript" раскрывает основные принципы функционального программирования (ФП) в контексте их применения на языке JavaScript. Однако, данную книгу от большинства изданий отличает то, что в ней описывается исключительно практический подход к данным принципам, без погружения в узкоспециализированную терминологию. В процессе повествования мы постараемся раскрыть подмножество фундамемнтальных ФП концепций, которые я называл "Функционально-Легким Программированием" (ФЛП) и реализуем их на JavaScript.

**Примечание:** Не смотря на слово "Легкий" в названии, эта книга не подходит для новичков и не рекомендуется в качестве первого шага в изучении JavaScript. От читателя ожидается уверенное знание JS, так как книга содержит множество специфических нюансов, которые могут ускользнуть от понимания человека, не достаточно глубоко знакомого с языком. "Легкий" - означает прежде всего ограниченный по объему; Вместо широкого и поверхностного описания, которое встречается в большинстве книг по ФП на JavaScript, мы более глубоко погрузимся в каждую из тематик, касающихся функционального программирования на JavaScript.

Необходимо признать: если вы, как и я, не являетесь членом закрытого клуба экспертов в ФП, утверждения вида: "Монада это просто моноид в категории эндофункторов", не несут для вас ровно никакого смысла.

Однако, я не хочу сказать что ФП терминология лишена смысла полностью, или что её использование является "дурным тоном". Я надеюсь, что ознакомившись с "Функционально-Легким" подходом, вы, возможно, заинтересуетесь более формальным изучением Функционально Программирования и получите достаточное количество информации о том где и как следует применять соответствующую терминологию.

Я хочу чтобы вы были способны применять некоторые из фундаментальных принципов ФП уже сейчас, ибо верю, что это пожет вам писать более качественный, осымсленный и поддерживаемый код.

**Более подробно с мотивацией, подтолкнувшей меня к написанию данного материала, вы можете ознакомиться в [Предисловии](manuscript/preface.md).**

## Книга

[Содержание](manuscript/README.md/#table-of-contents)

* [Введение](manuscript/foreword.md/#foreword) ([Brian Lonsdorf, aka "Prof Frisby"](https://twitter.com/DrBoolean))
* [Предисловие](manuscript/preface.md/#preface)
* [Глава 1: Почему Функциональное Программирование?](manuscript/ch1.md/#chapter-1-why-functional-programming)
* [Глава 2: Природа функций](manuscript/ch2.md/#chapter-2-the-nature-of-functions)
* [Глава 3: Работа с аргументами](manuscript/ch3.md/#chapter-3-managing-function-inputs)
* [Глава 4: Композиция](manuscript/ch4.md/#chapter-4-composing-functions)
* [Глава 5: Уменьшение побочных эффектов](manuscript/ch5.md/#chapter-5-reducing-side-effects)
* [Глава 6: Ценность иммутабелности](manuscript/ch6.md/#chapter-6-value-immutability)
* [Глава 7: Замыкание против Объекта](manuscript/ch7.md/#chapter-7-closure-vs-object)
* [Глава 8: Рекурсия](manuscript/ch8.md/#chapter-8-recursion)
* [Глава 9: Работа с массивами](manuscript/ch9.md/#chapter-9-list-operations)
* [Глава 10: Асинхронность в ФП](manuscript/ch10.md/#chapter-10-functional-async)
* [Глава 11: Собираем все вместе](manuscript/ch11.md/#chapter-11-putting-it-all-together)
* [Приложение A: Преобразования (Transducing)](manuscript/apA.md/#appendix-a-transducing)
* [Приложение B: О Скромной Монаде](manuscript/apB.md/#appendix-b-the-humble-monad)
* [Приложение C: ФП Библиотеки](manuscript/apC.md/#appendix-c-fp-libraries)

## Публикация

Данная книга в оригинале [была опубликована и доступна к покупке на  Leanpub](https://leanpub.com/fljs/). Я также работаю над доступностью бумажной версии, но на текущий момент её судьба пока не известна.

[![Купить на Leanpub](https://img.shields.io/badge/Buy-Leanpub-yellow.svg)](https://leanpub.com/fljs)

Если вы хотите поддержать материально мои усилия, помимо покупки книги, это можно сделать на [patreon](https://www.patreon.com/getify).

<a href="https://www.patreon.com/getify">[![patreon.png](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/getify)</a>

## Персональные тренинги

Информация в этой книге основывается на материалах проводимого мной одноименного тренинга.

Если вам понравился материал этой книги, вы можете связаться со мной по поводу проведения тренинга по этой или любой другой тематике, связанной с JS/HTML5/Node.js по email: getify @ gmail

## Онлайн тренинги

У меня также есть несколько JS тренингов, доступных онлайн. Я [веду курсы](https://FrontendMasters.com/teachers/kyle-simpson) на платформе [Frontend Masters](https://FrontendMasters.com), где вы можете найти мой воркшоп [Functional-Light JavaScript v2](https://frontendmasters.com/courses/functional-javascript-v2/). Некоторые из моих курсов также доступны на [PluralSight](https://www.pluralsight.com/search?q=kyle%20simpson&categories=all).


## Лицензия

Права на все материалы принадлежат Kyle Simpson. (c) 2016-2018

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br /><a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivs 4.0 Unported License</a>.
