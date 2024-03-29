![[Pasted image 20230813220550.png]]
![[Pasted image 20230813220609.png]]
- **Call Stack** / Стек вызовов
- **Task queue** / Очередь макрозадач - заполняется синхронными функциями, setTimeout, setInterval, AJAX(?) в момент установки и т.д.
- **Microtask queue** / Очередь микрозадач - заполняется микротасками (Promise, queueMicrotask, MutationObserver) и выполняется сразу после макрозадачи, но до отрисовки. Это гарантирует, что общее окружение останется тем же между микрозадачами (координаты мыши те же (рендера не было), новые данные по сети не получены). Если за периодов времени задач добавляется больше, чем разгребается, то здесь зависнет.
- **Render queue** / Очередь отрисовки - не может выполняться, пока что-то есть в стеке вызовов. Сюда попадают задачи анимации, установки и пересчета стилей, размещение HTML, отрисовки. Эти задачи оптимизируются браузером.
- WEB API / Browser API - здесь обитают таймеры, интервалы, Promise, MutationObserser'ы, event listener'ы после установки через Call Stack в ожидании вызова callback. После срабатывания триггера callback отправляется либо в **Task queue** (таймеры, интервалы)**, Microtask queue** (Promise, MutationObserver'ы).
- Event Loop - единственное место, через которое задачи могут попасть в Call Stack.


**Работа Event Loop заключается в том**, синхронизировать работу Call Stack, Task queue, Microtask queue, Render queue. Если в Task queue или Microtask queue что-то есть, а стек вызовов пуст то поместить в стек первый элемент из очереди.


Порядок работы такой:

1. выполнить текущую макрозадачу из **Task queue**
2. выполнить все микрозадачи из **Microtask queue**
3. выполнить все задачи из **Render queue**, когда стек вызовов очистится
4. выбрать следующую макрозадачу из **Task queue** (т.е. перейти к шагу 1).

  

Примеры работы:

1. **Синхронная функция** попадает в **Task queue**.
2. Все **Promise / async / await / try catch finally** устанавливается в стеке вызовов, а внутренние функции отлетают в очередь **Microtask queue**.
3. **setTimeout, setInterval** устанавливается в стеке вызовов, а callback с таймером отлетает в WEB API. Как только таймер срабатывает, то callback попадает в **Task queue**.
4. **addEventListener** устанавливается в стеке вызовов, попадает в WEB API и висит там постоянно. Как только происходит событие, то callback попадает в **Task queue (?)**.


[источник 1 (видео)](https://www.youtube.com/watch?v=8aGhZQkoFbQ&ab_channel=JSConf) 
[источник 2 (статья)](https://learn.javascript.ru/event-loop#makrozadachi-i-mikrozadachi)
[источник 3 (статья)](https://habr.com/ru/post/461401/)