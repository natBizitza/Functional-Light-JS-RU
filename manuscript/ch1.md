# Функционально-легкий JavaScript
# Глава 1: Почему Функциональное Программирование?

> Функциональщик: (сущ.) Тот парень, который называет переменные "x", функции "f", а паттерны -- "Зигохистоморфный Препроморфизм"
>
> Джеймс Ири @jamesiry 5/13/15
>
> https://twitter.com/jamesiry/status/598547781515485184

Функциональное Программирование (ФП) безусловно не является новой концепцией. В том или ином виде этот подход существовал на протяжении почти всей истории программирования. Тем не менее, хотя я не до конца уверен что это справедливое утрвеждение... эта концепция никогда не была сильно распространена среди практикующих программистов, до последних нескольких лет. Как мне кажется, ФП больше лежало в области интересов ученых.

Однако все меняется. ФП начинает получать все более широкую общественную поддержку, не только на уровне синтаксиса языков, но в том числе и на уровне библиотек и фреймворков. Очень может быть, что вы читаете этот текст потом, что наконец осознали, что ФП стало тем, что больше нельзя игнорировать. Или, возможно, вы также как и я, множество раз пытались подойти к изучению ФП, но каждый раз спотыкались продираясь через все эти термины и математические выражения.

Цель первой главы заключается в том, чтобы ответить на вопросы вроде "Почему я должен использовать ФП стиль для своего кода?" или "Как Функционально-легкий JavaScript соотносится с другими ФП подходами?" После завершения этой подготовительной работы, на протяжении оставшейся части книги мы будем постепенно раскрывать методы и шаблоны написания JS кода в Функционально-Легком стиле.

## Взгляд "одним глазом"

Давайте кратко проиллюстрируем понятие "Функционально-Легкий Javascript" путем сравнения кода, написанного с использованием различных подходов. Рассмотрим следующий фрагмент:

```js
var numbers = [4,10,0,27,42,17,15,-6,58];
var faves = [];
var magicNumber = 0;

pickFavoriteNumbers();
calculateMagicNumber();
outputMsg();                // The magic number is: 42

// ***************

function calculateMagicNumber() {
    for (let fave of faves) {
        magicNumber = magicNumber + fave;
    }
}

function pickFavoriteNumbers() {
    for (let num of numbers) {
        if (num >= 10 && num <= 20) {
            faves.push( num );
        }
    }
}

function outputMsg() {
    var msg = `The magic number is: ${magicNumber}`;
    console.log( msg );
}
```

А теперь взгляните на этот фрагмент, выполняющий ту же самую работу:

```js
var sumOnlyFavorites = FP.compose( [
    FP.filterReducer( FP.gte( 10 ) ),
    FP.filterReducer( FP.lte( 20 ) )
] )( sum );

var printMagicNumber = FP.pipe( [
    FP.reduce( sumOnlyFavorites, 0 ),
    constructMsg,
    console.log
] );

var numbers = [4,10,0,27,42,17,15,-6,58];

printMagicNumber( numbers );        // The magic number is: 42

// ***************

function sum(x,y) { return x + y; }
function constructMsg(v) { return `The magic number is: ${v}`; }
```

Как только вы начнете понимать ФП и Функционально-Легкий подход, скорее всего во втором фрагменте вы прочтете следующие:

> Сначала мы создаем функцию `sumOnlyFavorites(..)`, являющуюся комбинацией трех других функций. Мы объединяем два фильтра, одно сравнение с 10 и 20. После этого, мы добавляем редьюсер `sum(..)` в композицию трансьдюcера. На выходе получаем функцию `sumOnlyFavorites(..)`, являющуюся редьюсером, который проверяет, подпадает ли значение под оба фильтра, и если да, добавляет его к значению аккумулятора.
>
> Потом мы создаем другую функцию `printMagicNumber(..)`, которая применяет редьюсер `sumOnlyFavorites(..)` к списку чисел, получая на выходе только сумму искомых чисел. После чего `printMagicNumber(..)` пропускает это финальное значение через функцию `constructMsg(..)`, которая создает строковое представление результата, в конечном счете попадающего в `console.log(..)`.

Весь этот поток кода *говорит* с ФП программистом образом, который скорее всего ещё вам не знаком. Эта книга поможет вам начать *говорить* аналогичным образом, так что этот код станет для вас столь же читабельным, как любой ругой, если не более того!

Несколько замечаний по поводу данного сравнения фрагментов кода:

* Вполне вероятно, что для многих читателей первый фрагмент выглядит более удобным/читаемым/поддерживаемым, чем второй. Абсолютно нормально, если это так. Я уверен, что если вы найдете в себе силы дочитать эту книгу и попробовать применить все практики, которые будут рассмотрены, второй фрагмент кода станет для вас гораздо более естественным, и возможно даже предпочтительным!

* Возможно, у вас есть способ решения той же задачи, кардинально отличающийся от предстваленных. Это тоже нормально. Данная книга не ставит себе целью выдавать предписания, каким способом решить ту или иную задачу. Цель состоит в иллюстрации плюсов и минусов различных паттернов, а также в том, чтобы научить вас принимать правильные решения, полагаясь на эти данные. К концу этой книги вы, вероятно, будете более склонны ко второму представленному варианту, нежели сейчас.

* Также возможно, что вы уже опытный разработчик FP, который просматривает начало этой книги, чтобы узнать, есть ли что-нибудь полезное для вас. И этот второй фрагмент конечно же уже выглядит для вас знакомым. Но я также готов поспорить, что вы вы пару раз подумали: «Хм, я бы этого не сделал * таким * образом ...». Это нормально и вполне разумно.

    Это не традиционная, каноническая книга по Функциональному Программированию. И временами используемые в ней подходы могут казаться весьма еретичными. Мы стремимся к достижению прагматического баланса между очевидными неоспоримыми преимуществами ФП и необходимостью поставки работоспособного, поддерживаемого JS кода без необходимости одолевать гору терминов и математических выражений. Это не *традиционное* ФП, это "Функционально-Легкий JavaScript".

Но независимо от причин, по которым вы читаете эту книгу, я говорю вам "Добро пожаловать"!

## Надежность

У меня есть очень простая точка зрения, которая лежит в основе всего, что я делаю как преподаватель разработки программного обеспечения (на JavaScript): код, которому нельзя доверять - это код, который ты не понимаешь. Обратное тоже верно: код, который не понятен - не заслуживает доверия. Больше того, если код непонятен и ему нельзя доверять, то нельзя быть уверенным, что этот код способен решить проблему, для решения которой он был написан. Запуск такой программы равноценен участию в лотерее.

Но что я имею в виду под "доверием"? Я имею в виду, что путем чтения кода и логических рассуждений вы можете понять то, что *будет* делать программа, не запуская её; избавляя себя от необходимости полагаться на то, что она *должна* делать. Возможно, мы чаще необходимого склонны полагаться на тесты и уровень покрытия ими кода чтобы убедиться в работоспособности программы. Я не хочу сказать, что тесты - это плохо. Но я думаю, что мы должны стремиться к тому, чтобы понимать наш код достаточно хорошо, чтобы быть уверенными, что тесты проходят, ещё до их запуска.

Принципы, лежащие в основе ФП разработанны с учетом того, чтобы иметь гораздо больше уверенности в том, что делает программа, просто прочитав её исходный код. Тот, кто понимает ФП и достаточно дисциплирован, чтобы использовать при написании кода, способен написать программу таким образом, что её задача и корректность реализации будет понятна **каждому** прочитавшему код.

Надежность программ также повышается, когда мы используем техники, помогающие минимизировать наиболее вероятные источники возникновения ошибок. Это, пожалуй один из главных аргументов в пользу ФП: в программах, написанных в функциональном  стиле часто меньше ошибок, а те, что есть, находятся в очевидных местах, поэтому их легко найти и исправить. Функциональный код имеет тенденцию быть более устойчивым к багам. Хотя конечно, не гарантирует их отсутствие.

В процессе чтения этой книги, вы начнете больше доверять написанному вами коду, потому что вы будете использовать шаблоны и практики, которые уже хорошо зарекомендовали себя, а также свободны от наиболее частых причин возникновения ошибок в работе программы!

## Общение

Почему Функциональное Программирование является столь важным? Чтобы ответить на этот вопрос, следует отойти на шаг назад и поговорить о важности программирования в целом.

Это может показаться странным, но я не считаю, что программа - это прежде всего набор инструкций для компьютера, предназначенный для решения определенной задачи. На самом деле, мне это кажется даже скорее счастливой случайностью.

Я горячо верю в то, что у кода есть куда более важная роль  - это средство коммуникации с другими людьми.

Наверняка, вам на собственном опыте пришлось убедиться, насколько большую часть времени программиста занимает чтение существующего кода. Лишь очень небольшая часть из нас имеет счастье тратить всё (или большую часть) времени на написание кода "с нуля", без необходимости иметь дело с кодом, написанным другими (или даже самим собой из прошлого).

По общим оценкам, разработчики тратят примерно 70% своего времени на то, чтобы прочитать и разобраться с имеющейся кодовой базой. Это открывает глаза. 70%. Не удивительно, что средний программист пишет лишь около 10 строк в день. И мы убиваем до 7 часов в день, просто на чтение кода и попытки осознать, что же на самом деле должны делать эти 10 строк!

Мы должны гораздо больше времени уделять читабельности нашего кода. И, кстати - читабельность не обязательно означает сокращение количества символов. Читабельность больше всего зависит от того, насколько знакомым и близким для нас выглядит код<a href="#user-content-footnote-1"><sup>1</sup></a>

Если мы решили тратить время на написание кода, который будет более читаемым и понятным, стоит сконцетрироваться на принципах ФП. Эти принципы хорошо обоснованы, глубоко проверны и изучены, а кроме того, легко доказуемы. Потратив время на их изучение и практическое применение, вы в конечном итоге сможете создавать код, который будет знаком и близок вам и вашим коллегам. А с улучшением узнаваемость кода, последует и улучшение читабельности.

Например, как только вы усвоили, что делает `map(..)`, вы будете способны практически мгновенно понять, для чего он используется в конкретном месте кода программы. Но каждый раз, когда вы имеете дело с циклом `for`, придется полностью прочитать тело цикла, чтобы понять, для чего он предназначен. При этом сам синтакс `for` может выглядеть более знакомым, но сама суть того, что он делает - нет. Вы вынуждены будете тратить время на его *чтение* каждый раз.

Увеличивая процент кода, узнаваемого "с первого взгляда", и, таким образом, меньше времени тратя на его чтение, мы можем сосредоточиться на более высоких уровнях логики программы. Это в любом случае гораздо более важный вопрос, который больше всего требует нашего внимания.

ФП (по крайней мере, без всей этой утяжеляющей терминологии) - один из наиболее эффективных инструментов создания читаемого и поддерживаемого кода. И именно *поэтому* ознакомиться с ним столь важно.

## Читабельность

Readability is not a binary characteristic. It's a largely subjective human factor describing our relationship to code. And it will naturally vary over time as our skills and understanding evolve. I have experienced effects similar to the following figure, and anecdotally many others I've talked to have as well.

<p align="center">
    <img src="images/fig17.png" width="50%">
</p>

You may just find yourself experiencing similar effects as you work through the book. But take heart; if you stick this out, the curve comes back up!

*Imperative* describes the code most of us probably already write naturally; it's focused on precisely instructing the computer *how* to do something. Declarative code -- the kind we'll be learning to write, which adheres to FP principles -- is code that's more focused on describing the *what* outcome.

Let's revisit the two code snippets presented earlier in this chapter.

The first snippet is imperative, focused almost entirely on *how* to do the tasks; it's littered with `if` statements, `for` loops, temporary variables, reassignments, value mutations, function calls with side effects, and implicit data flow between functions. You certainly *can* trace through its logic to see how the numbers flow and change to the end state, but it's not at all clear or straightforward.

The second snippet is more declarative; it does away with most of those aforementioned imperative techniques. Notice there's no explicit conditionals, loops, side effects, reassignments, or mutations; instead, it employs well-known (to the FP world, anyway!) and trustable patterns like filtering, reduction, transducing, and composition. The focus shifts from low-level *how* to higher level *what* outcomes.

Instead of messing with an `if` statement to test a number, we delegate that to a well-known FP utility like `gte(..)` (greater-than-or-equal-to), and then focus on the more important task of combining that filter with another filter and a summation function.

Moreover, the flow of data through the second program is explicit:

1. A list of numbers goes into `printMagicNumber(..)`.
2. One at a time those numbers are processed by `sumOnlyFavorites(..)`, resulting in a single number total of only our favorite kinds of numbers.
3. That total is converted to a message string with `constructMsg(..)`.
4. The message string is printed to the console with `console.log(..)`.

You may still feel this approach is convoluted, and that the imperative snippet was easier to understand. You're much more accustomed to it; familiarity has a profound influence on our judgments of readability. By the end of this book, though, you will have internalized the benefits of the second snippet's declarative approach, and that familiarity will spring its readability to life.

I know asking you to believe that at this point is a leap of faith.

It takes a lot more effort, and sometimes more code, to improve its readability as I'm suggesting, and to minimize or eliminate many of the mistakes that lead to bugs. Quite honestly, when I started writing this book, I could never have written (or even fully understood!) that second snippet. As I'm now further along on my journey of learning, it's more natural and comfortable.

If you're hoping that FP refactoring, like a magic silver bullet, will quickly transform your code to be more graceful, elegant, clever, resilient, and concise -- that it will come easy in the short term -- unfortunately that's just not a realistic expectation.

FP is a very different way of thinking about how code should be structured, to make the flow of data much more obvious and to help your reader follow your thinking. It will take time. This effort is eminently worthwhile, but it can be an arduous journey.

It still often takes me multiple attempts at refactoring a snippet of imperative code into more declarative FP, before I end up with something that's clear enough for me to understand later. I've found converting to FP is a slow iterative process rather than a quick binary flip from one paradigm to another.

I also apply the "teach it later" test to every piece of code I write. After I've written a piece of code, I leave it alone for a few hours or days, then come back and try to read it with fresh eyes, and pretend as if I need to teach or explain it to someone else. Usually, it's jumbled and confusing the first few passes, so I tweak it and repeat!

I'm not trying to dampen your spirits. I really want you to hack through these weeds. I am glad I did it. I can finally start to see the curve bending upward toward improved readability. The effort has been worth it. It will be for you, too.

## Perspective

Большинство других текстов ФП, похоже, придерживаются подхода "сверху вниз", но мы собираемся пойти в противоположном направлении: работая с нуля, мы раскроем основные основополагающие принципы, которые, я полагаю, официальные разработчики ФП признали бы основой для всего, что они делают. Но по большей части мы будем держаться на расстоянии вытянутой руки от большей части пугающей терминологии или математических обозначений, которые так легко могут расстроить учащихся.

Я считаю, что менее важно, как вы что-то называете, и более важно, чтобы вы понимали, что это такое и как это работает. Это не значит, что общая терминология неважна - она несмоненно упрощает общение между опытными профессионалами. Хотя я обнаружил, что для ученика это может быть отвлекающим.

Итак, в этой книге мы сконцентрируемся больше на фундаментальных концепциях и меньше на замысловатостях. Это не значит, что мы не используем терминологию; она точно будет. Однако не зацикливайтесь на завороченных словах. Везде, где это необходимо, обращайте внимание на идеи, стоящими за ними.

Я называю здесь менее формальную практику "Функционально-лёгким программированием", потому что я думаю, что формализм истинного ФП страдает от того, что он может быть довольно подавляющим, если вы еще не привыкли к формальному мышлению. Я не просто предполагаю; это моя собственная личная история. Даже после преподавания ФП и написания этой книги, я всё ещё могу сказать, что формализм терминов и обозначений в ФП  мне очень, очень трудно усвоить. Я пытался, и пытался, и, похоже, не могу справиться со многим из этого.

Я знаю многих разработчиков ФП, которые верят в то, что формализм помогает обучению. Но, я считаю, что здесь явно есть предел, где это становится правдой только тогда, когда вы достигаете определённого комфорта с формализмом. Если у вас уже есть математическое образование или даже определённый опыт в компьютерной науке, это может показаться вам более знакомым. Многие из нас не имеют этого, и несмотря на наши старания, формализм продолжает мешать нам.

Итак, эта книга знакомит с концепциями, на которых, как я полагаю, построен ФП, но при этом даёт вам толчок снизу, чтобы подняться по отвесной стене, вместо того, чтобы снисходительно кричать на вас сверху, подталкивая подсказывает вам, как карабкаться по ходу дела.

## Как найти баланс

Если ты уже достаточно времени в программировании, есть возможность, что ты слышал фразу "YAGNI" раньше: "You Ain't Gonna Need It" ("Тебе это не понадобится"). Этот принцип в первую очередь исходит из экстремального программирования и подчёркивает высокий риск и стоимость создания функциональности до того, как она понадобится.

Иногда мы предполагаем, что нам будет нужна определённая функциональность в будущем, мы создаём её сейчас, полагая, что так будет проще, пока мы работаем над другими, а затем понимаем, что мы ошиблись, и функциональность не нужна или должна была быть совсем другой.
Other times we guess right, but build a feature too early, and suck up time from the features that are genuinely needed now; we incur an opportunity cost in diluting our energy.

YAGNI challenges us to remember: even if it's counterintuitive in a situation, we often should postpone building something until it's presently needed. We tend to exaggerate our mental estimates of the future refactoring cost of adding it later when it is needed. Odds are, it won't be as hard to do later as we might assume.

As it applies to functional programming, I would offer this admonition: there will be plenty of interesting and compelling patterns discussed in this text, but just because you find some pattern exciting to apply, it may not necessarily be appropriate to do so in a given part of your code.

This is where I will differ from many formal FPers: just because you *can* apply FP to something doesn't mean you *should* apply FP to it. Moreover, there are many ways to slice a problem, and even though you may have learned a more sophisticated approach that is more "future-proof" to maintenance and extensibility, a simpler FP pattern might be more than sufficient in that spot.

Generally, I'd recommend seeking balance in what you code, and to be conservative in your application of FP concepts as you get the hang of things. Default to the YAGNI principle in deciding if a certain pattern or abstraction will help that part of the code be more readable or if it's just introducing clever sophistication that isn't (yet) warranted.

> Reminder, any extensibility point that’s never used isn’t just wasted effort, it’s likely to also get in your way as well
>
> Jeremy D. Miller @jeremydmiller 2/20/15
>
> https://twitter.com/jeremydmiller/status/568797862441586688

Remember, every single line of code you write has a reader cost associated with it. That reader may be another team member, or even your future self. Neither of those readers will be impressed with overly clever, unnecessary sophistication just to show off your FP prowess.

The best code is the code that is most readable in the future because it strikes exactly the right balance between what it can/should be (idealism) and what it must be (pragmatism).

## Resources

I have drawn on a great many different resources to be able to compose this text. I believe you, too, may benefit from them, so I wanted to take a moment to point them out.

### Books

Some FP/JavaScript books that you should definitely read:

* [Professor Frisby's Mostly Adequate Guide to Functional Programming](https://drboolean.gitbooks.io/mostly-adequate-guide/content/ch1.html) by [Brian Lonsdorf](https://twitter.com/drboolean)
* [JavaScript Allongé](https://leanpub.com/javascriptallongesix) by [Reg Braithwaite](https://twitter.com/raganwald)
* [Functional JavaScript](http://shop.oreilly.com/product/0636920028857.do) by [Michael Fogus](https://twitter.com/fogus)

### Blogs/sites

Some other authors and content you should check out:

* [Fun Fun Function Videos](https://www.youtube.com/watch?v=BMUiFMZr7vk) by [Mattias P Johansson](https://twitter.com/mpjme)
* [Awesome FP JS](https://github.com/stoeffel/awesome-fp-js)
* [Kris Jenkins](http://blog.jenkster.com/2015/12/what-is-functional-programming.html)
* [Eric Elliott](https://medium.com/@_ericelliott)
* [James A Forbes](https://james-forbes.com/)
* [James Longster](https://github.com/jlongster)
* [André Staltz](http://staltz.com/)
* [Functional Programming Jargon](https://github.com/hemanth/functional-programming-jargon#functional-programming-jargon)
* [Functional Programming Exercises](https://github.com/InceptionCode/Functional-Programming-Exercises)

### Libraries

The code snippets in this book largely do not rely on libraries. Each operation that we discover, we'll derive how to implement it in standalone, plain ol' JavaScript. However, as you begin to build more of your real code with FP, you'll soon want a library to provide optimized and highly reliable versions of these commonly accepted utilities.

By the way, you need to check the documentation for the library functions you use to ensure you know how they work. There will be a lot of similarities in many of them to the code we build on in this text, but there will undoubtedly be some differences, even between popular libraries.

Here are a few popular FP libraries for JavaScript that are a great place to start your exploration with:

* [Ramda](http://ramdajs.com)
* [lodash/fp](https://github.com/lodash/lodash/wiki/FP-Guide)
* [functional.js](http://functionaljs.com/)
* [Immutable.js](https://github.com/facebook/immutable-js)

[Appendix C takes a deeper look at these libraries](apC.md/#stuff-to-investigate) and others.

## Summary

You may have a variety of reasons for starting to read this book, and different expectations of what you'll get out of it. This chapter has explained why I want you to read the book and what I want you to get out of the journey. It also helps you articulate to others (like your fellow developers) why they should come on the journey with you!

Functional programming is about writing code that is based on proven principles so we can gain a level of confidence and trust over the code we write and read. We shouldn't be content to write code that we anxiously *hope* works, and then abruptly breathe a sigh of relief when the test suite passes. We should *know* what it will do before we run it, and we should be absolutely confident that we've communicated all these ideas in our code for the benefit of other readers (including our future selves).

This is the heart of Functional-Light JavaScript. The goal is to learn to effectively communicate with our code but not have to suffocate under mountains of notation or terminology to get there.

The journey to learning functional programming starts with deeply understanding the nature of what a function is. That's what we tackle in the next chapter.

----

<a name="footnote-1"><sup>1</sup></a>Buse, Raymond P. L., and Westley R. Weimer. “Learning a Metric for Code Readability.” IEEE Transactions on Software Engineering, IEEE Press, July 2010, dl.acm.org/citation.cfm?id=1850615.
