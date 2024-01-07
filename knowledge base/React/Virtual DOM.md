### Virtual DOM

React для рендеринга и отслеживания изменений использует Virtual DOM.

**Virtual DOM** - объектная модель документа, которая состоит из нод - компонентов и тегов. Каждая нода хранит свои пропсы и атрибуты.

Virtual DOM нужен:
1. Для снижения количества затратных манипуляций с DOM-деревом документа.
2. Чтобы избавить программиста от реальных манипуляций с DOM-деревом.

### Rendering

Рассмотрим механизм работы с начальной загрузки документа поэтапно.
##### 1. Compile

Некоторые фреймворки (Vue.js, например) должны сначала скомпилировать Шаблон документа в render-функции. **Для React это не нужно.**

##### 2. Mount

1. Runtime renderer запускает отработку всех рендер-функций рекурсивно. Эти функции возвращают объекты, из которых строится **Current Tree** - текущее дерево Virtual DOM.
2. Далее это дерево передается в **Rendering Environment**, где оно монтируется в документ.

##### 3. Reconciliation

Когда изменяется какая-то зависимость, то происходит реконсилиация:

1. Cоздается новое дерево Virtual DOM - **Work-In-Progress Tree**.
2. Runtime renderer проходит по этому дереву и сравнивает узлы с Current Tree и получает массив отличий - где ноды были добавлены, где удалены, где заменены.
3. Далее массив изменений передается в Rendering Env, который вносит эти изменения в реальный DOM.

Чтобы сократить время при обновлении, в React используется не строгая, а **эвристическая функция сравнения**, которая основана не утверждениях:

1. Если теги старого и нового элемента отличаются - элемент заменяется на новый.
2. Если ключи текущего и нового элемента отличаются - элемент заменяется на новый.
3. Если какой-то атрибут изменился, то обновляется только этот атрибут с сохранением состояния элемента.

Такая апроксимация позволила свести алгоритм сравнения к O(n) вместо O(n^3).

### Rendering Environment

Функция построения дерева вынесена в пакет React Core, а Rendering Environment вынесен в отдельные библиотеки, т.к. среда отрисовки дерева может изменяться. Например, для web-приложения используется Web окружение, а для нативных - окружение React Native.


### Приоритезация DOM-операций

Обновление данных разбивается на маленькие операции, которые называются юниты. Каждому юниту присваивается приоритет, а юниты сортируются в порядке приоритета по убыванию. 

Например, hover-анимация является более приоритетной, чем обновление данных в блоке, которые даже не во viewport.

Приоритет операций определяется с помощью пакета [scheduler](https://github.com/facebook/react/tree/main/packages/scheduler).
Всего операции разделены на 6 приоритетов:
```
export const NoPriority = 0;
export const ImmediatePriority = 1;
export const UserBlockingPriority = 2;
export const NormalPriority = 3;
export const LowPriority = 4;
export const IdlePriority = 5;
```

Каждый приоритет имеет таймаут выполнения - [source](https://github.com/facebook/react/blob/c5b9375767e2c4102d7e5559d383523736f1c902/packages/scheduler/src/forks/SchedulerMock.js#L60).

В основе приоритезации лежат функции:
	1. [window.requestAnimationFrame(callback)](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) - для приоритетных операци. Частота вызова этой функции в браузере примерно 60 fps. 
	2. [window.requestIdleCallback(callback, options)](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback) - для менее приоритетных операций.




Полезное
[Подробно о React Reconciliation, или Как React добился 60 fps](https://www.youtube.com/watch?v=NPXJnKytER4)
[Optimizing React: Virtual DOM explained](https://evilmartians.com/chronicles/optimizing-react-virtual-dom-explained)