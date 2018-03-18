# Task_test
Обучал LSTM-модель на сборнике стихов Пушкина А.С, закодированном по принципу one-hot. Пробовал размеры окна 5 и 15.

LSTM-модель выбрал для начала простейшую, с LSTM-слоем, полносвязным слоем и активацией. Выбор архитектуры ограничивался вычислительными возможностями, т.к считать приходилось на CPU.

Лосс выбрал бинарную кроссэнтропию, оптимизатор adam, лосс скатывался в локальный минимум довольно быстро.

И при размере окна 5, и при размере окна 15 происходит зацикливание, его удается предотвратить, только если в какой-то случайный момент предсказывать не самую вероятную букву, а вторую по вероятности. Но в любом случае, даже если этого не делать, не все выданные моделью слова можно назвать грамматически правильными.

Буду пробовать видоизменять архитектуру, если и этого не хватит - добавлять больше данных.
