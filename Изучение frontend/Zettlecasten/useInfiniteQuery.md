2025 03 2016 58
Tags: #react #tanstack-qurey
###### Links: 
1) [[Хуки]]
# Заметка
Чтобы применить хук useInfiniteQuery, нужно передать querryKey, queryFn, initionalPageParam и функцию getNextPageParam для перехода между страницами. Дата будет сохраняться между запросами. В queryFn не нужно явно передавать pageParam, как и любые другие переменные. Их можно передать через querykey, получив нужные переменные уже в самой функции. Для типизации переменной используется `QuerryFunctionContext[querryKey]`