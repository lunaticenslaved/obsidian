## Как стили попадают на страницу

Перечислим источники, из которых браузер получает правила оформления:

- Браузерные стили — `default (user agent) style sheet`. Их можно переопределять самостоятельно или с помощью библиотек. Например, `normalize.css`.
- Пользовательские стили. Их нельзя не учитывать, равно как не стоит пренебрегать использованием `!important`.
- Ссылка на таблицу стилей: `link` и `rel="stylesheet"`.
- Тег `style`.
- Атрибут `style` — этот метод часто используется вместе с JS.

## Специфичность селекторов

// TODO


## Методологии

### OOCSS

**OOCSS** — это объектно-ориентированный CSS. Подобный подход позволяет применять метод «разделяй и властвуй». Другие методологии возникли как развитие идей OOCSS.

**Принцип**: внешний вид элемента не зависит от того, где он расположен. Вместо` .my-element button { ... }` создаём отдельный стиль `.control` для конкретного случая.

У подхода есть минус — сложная поддержка при изменении элемента. В таком случае, скорее всего, придётся добавлять классы в разметку. Большой проблемы в этом нет, но часто считают дурным тоном. 

В результате OOCSS применяется не так часто. Он остаётся абстрактным идеалом, недостижимым на практике.


### БЭМ

БЭМ — аббревиатура для «Блок, Элемент, Модификатор».

#### Блок

Блок — функционально независимый компонент страницы, который может быть использован повторно. 

Название блока должно характеризовать смысл, а не состояние. Отвечает на вопрос «что это?». «Меню» — `menu`, «кнопка» — `button`.

Название блока не отвечает на вопросы состояния, например «какой, как выглядит?». «Красный», «большой» и другие описания состояний не подходят для блока.

#### Элемент

Элемент — часть блока, которая не может быть использована в отрыве от него.

Для названия элемента верно всё то же, что и для названия блока. Оно описывает смысл, а не состояние и отвечает на вопрос «что это?». «Пункт» — `item`, «текст» — `text`.

Структура имени элемента соответствует схеме: имя-блока__имя-элемента. Использование двойного подчёркивания — не строгое правило, а сложившаяся практика. Никто не запрещает изменять разделители. Однако не стоит без веских причин отказываться от популярных условностей — они помогают делать код единообразным и понятным.

#### Модификатор

Модификатор определяет внешний вид, состояние или поведение блока, или элемента.

Название модификатора должно характеризовать:

- внешний вид — «размер»: `size_s`, «тему»: `theme_island`;
- состояние — «отключён»: `disabled`, «фокусированный»: `focused`;
- поведение — «направление»: `directions_left-top`.

Имя модификатора отделяют одним подчёркиванием: `имя-блока__имя-элемента_имя-модификатора`.


### CSS Modules

### CSS через JS

У такого подхода есть ряд преимуществ:

- JS более гибкий и позволяет делать всё, что захотите;
- можно задавать различные темы и стили страницы в runtime;
- уменьшение размера загружаемых стилей и ускорение первого рендера;
- нет кеша.

Но есть и минусы:

- сложнее покрывать автотестами систему без классов и адекватных имён;
- управлять стилями гораздо сложнее, чем классами в долгосрочной перспективе.

Библиотеки: JSS, Styled Components

  

## Препроцессоры

Препроцессоры CSS помогают писать стили, как будто это язык программирования.

Препроцессоров много, но самые популярные:

- LESS,
- Stylus,
- Sass или SCSS — Syntactically Awesome Stylesheets.

##### PostCSS

Препроцессоры предлагают множество функций, из которых разработчики пользуются меньшей частью. Иногда всего несколькими: переменными, миксинами и вложенностью. Использовать для этого тяжёлые препроцессоры может быть не эффективно.

PostCSS — это плагинная система, которая позволяет выстроить трансформацию стилей так, как нужно вашей команде. Все плагины атомарны и добавляют отдельные возможности:

- поддержку переменных,
- поддержку вложенности,
- поддержку разных браузеров
