# Task_test
Обучал LSTM-модель на сборнике стихов Пушкина А.С, закодированном по принципу one-hot. Пробовал размеры окна 5 и 15.

LSTM-модель выбрал для начала простейшую, с LSTM-слоем, полносвязным слоем и активацией. Выбор архитектуры ограничивался вычислительными возможностями, т.к считать приходилось на CPU.

Лосс выбрал бинарную кроссэнтропию, оптимизатор adam, лосс скатывался в локальный минимум довольно быстро.

И при размере окна 5, и при размере окна 15 происходит зацикливание, его удается предотвратить, только если в какой-то случайный момент предсказывать не самую вероятную букву, а вторую по вероятности. Но в любом случае, даже если этого не делать, не все выданные моделью слова можно назвать грамматически правильными.

Пример выдачи:

[i]Уж небо осенью столь, и тому подъемлет он в сень на постали мой друг, и славы постали в прах веселых под шумит,И все дару под сень на свободы не стала,И сладостный простой пред тобы томный старик последний свобы в силой друг,В том за староских последний стал и сладость в полязу под себя возвышенный свободы,На моренья милый друг,Придать в свои под сень мой драгой старик постали в приходит,Он в своей прелестной полной старик последним простой мой долго страстной старик под сень на стал и старого столеты,В мечтанье старик и столковал он в пред ним столем постали в прах веселых под шумит,И все дару под сень на свободы не стала,И сладостный простой пред тобы томный старик последний свобы в силой друг,В том за староских последний стал и сладость в полязу под себя возвышенный свободы,На моренья милый друг,Придать в свои под сень мой драгой старик постали в приходит,Он в своей прелестной полной старик последним простой мой долго страстной старик под сень на стал и старого столеты[/i]

С усложнением архитектуры(расширением полносвязного слоя и добавлением дропаута) число грамматически неправильным слов стало меньше.

Пример выдачи:

[i]Не стал под сень моей друг, не страшно в сердце полный вздохом простой,С бедной странный славы,Не старый восторгов своей на свете,Под сенью моим образ милый друг, не смелой странный славы,Не старый воспоминаний, страх не стал под сень моей друг, не стал под сени, друзья, приятной страх на свете не смелой,И в сени мое советами,Из после видел он не смолить, на берего странный друг, не смелой на своей под сень моей друг, не стал под сень моих душе поэта воспоминаньем, славы бессмертный, долго прославался на берегов, и в поле в стране воспоминанье,На старость он не смелой странный славы,Не старый воспоминанья,И страшит сердце волны, верной страны славы,Не стал под сень моей друг, не стал под сень моей друг, не стал под сень моей друг сердце волны светлый страны славы,[/i]

Для того, чтобы сгенерированный машиной текст был по крайней мере рифмованным, нужно усложнять архитектуру и увеличивать число букв, которые подаются в модель на каждом шагу. 15 букв - это меньше, чем целая строка(и поэтом , тренируя модель на размере окна 15, рифмованный текст ,скорее всего не получится). Но увеличение размера окна, сталкивается с ограничениями по времени и по памяти.

Чтобы обойти ограничение по памяти и сделать текст более осмысленным, я начал использовать fit_generator и увеличил размер окна до 35, а также увеличил размер обучающей выборки в 2 раза(добавив к стихам еще и поэмы) но это требует достаточно больших затрат времени. На текущий момент модель обучается.

Если бы у меня было больше времени и/или вычислительных мощностей, я бы также попробовал:

Усложнить архитектуру модели : добавить больше слоев, добавить регуляризацию, поэкспериментировать с функциями активации

Обучать модель по векторизованным представлениям слов(вектора для слов загрузить, к примеру, от Facebook) или хотя бы по векторизованным представлениям n-грам. Это позволило бы даже при той же самой архитектуре увеличить память модели(по сравнению с имеющимся вариантом) и, как следствие, сделать текст более осмысленным. 

Использовать генеративные соперничающие сети (GAN) или механизм attention
