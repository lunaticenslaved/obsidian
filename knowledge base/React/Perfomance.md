Быстрый JavaScript. Как писать фронденд эффективно

Метрики
1. First Containtful Paint - уменьшить размер бандла
2. Время до интерактивнивсти - уменьшить размер бандла
3. FPS - стабильная отрисовка
4. Память/трафик - сжимать картинки, не перебирать большие объемы данных
5. другое

Интрументы
1. Вкладка перфоманс
	- уменьшить скорость соединения, уменьшить кол-во CPU
	- there is a timeline with scripts call and snapshots at second
2. React Profiler - allows to watch for rerenders in the app
 
Advices
1. Not use extra libs - any lib cause bundle size increasing.
2. Use debounce and throttling to prevent extra requests and state changes
3. Server Side Rendering for desktop / mobile - exec on the server different scripts to prerender desktop and mobile HTML. This reduces bundle size sent to the client
4. Internalization (i18n) - make bundles for different locales like for desktop / mobile components
5. Compress files with `gzip` - use middleware `compression`
6. Minimization
7. Lazy loading - works for images, fonts, libs, heavy components, redux reducers (with `redux-dynamic-modules` lib)
8. Webpack tree shaking - webpack throws dead code away what reduces bundle size. It works with lazy-loading and decomposition.
9. Rerendering. Decomposition and `memo` allow to reduce rerenders.
10. `useMemo` and `useCallback`
11. Use `createSelector` for heavy selectors from redux store
12. Use container/component approach. Why?

Source:
https://www.youtube.com/watch?v=VNNLNC5h7ZI