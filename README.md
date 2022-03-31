# RussianMultiWOZ
Набор данных Multi-Domain Wizard-of-Oz (MultiWOZ) - полностью маркированная коллекция письменных разговоров между людьми, охватывающая множество областей и тем. При размере в 10 тыс. диалогов она как минимум на порядок больше всех предыдущих аннотированных корпораций, ориентированных на конкретные задачи.

# Data structure
Датасет содержит 3 406 однодоменных диалогов, включающих бронирование, если домен позволяет это сделать, и 7 032 многодоменных диалога, состоящих как минимум из 2-5 доменов. Для обеспечения воспроизводимости результатов, корпус был случайным образом разделен на обучающий, тестовый набор и набор для разработки. Наборы для тестирования и разработки содержат по 1 тыс. примеров. Несмотря на то, что все диалоги являются связными, некоторые из них не были закончены с точки зрения описания задачи. Поэтому наборы для проверки и тестирования содержат только полностью успешные диалоги, что позволяет справедливо сравнивать модели. В валидационном и тестовом наборах нет диалогов из доменов больницы и полиции.

Каждый диалог состоит из цели, нескольких высказываний пользователя и системы, а также состояния убеждений. Кроме того, добавлено описание задачи на естественном языке, представленное туркерам, работающим со стороны посетителя. Диалоги с MUL в названии относятся к многодоменным диалогам. Диалоги с SNG относятся к однодоменным диалогам (но возможен поддомен бронирования). Бронирование могло быть невозможно завершить, если опция fail_book не пуста в спецификации цели - турки об этом не знали.

Состояние убеждения состоит из трех разделов: semi, book и booked. Semi относится к слотам из определенного домена. Book относится к слотам бронирования для определенного домена, а booked - это подсписок словаря book с информацией о забронированном объекте (после того, как бронирование было сделано). Иногда туркеры ошибочно следуют к цели, что может привести к неверному состоянию убеждений. Совместная метрика точности включает ВСЕ слоты.


# Baseline

:bangbang: This part relates to the first version of the dataset and evaluation scripts.

### Requirements
Python 2 with `pip`, `pytorch==0.4.1`

### Preprocessing
To download and pre-process the data run:

```python create_delex_data.py```

### Training
To train the model run:

```python train.py [--args=value]```

Some of these args include:

```
// hyperparamters for model learning
--max_epochs        : numbers of epochs
--batch_size        : numbers of turns per batch
--lr_rate           : initial learning rate
--clip              : size of clipping
--l2_norm           : l2-regularization weight
--dropout           : dropout rate
--optim             : optimization method

// network structure
--emb_size          : word vectors emedding size
--use_attn          : whether to use attention
--hid_size_enc      : size of RNN hidden cell
--hid_size_pol      : size of policy hidden output
--hid_size_dec      : size of RNN hidden cell
--cell_type         : specify RNN type
```

## Testing
To evaluate the trained model, run:

```python test.py [--args=value]```

## Results
We ran a small grid search over various hyperparameter settings and reported the performance of the best model on the test set.
The selection criterion was 0.5*match + 0.5*success+100*BLEU on the validation set.
The final parameters were:

```
// hyperparamters for model learning
--max_epochs        : 20
--batch_size        : 64
--lr_rate           : 0.005
--clip              : 5.0
--l2_norm           : 0.00001
--dropout           : 0.0
--optim             : Adam

// network structure
--emb_size          : 50
--use_attn          : True
--hid_size_enc      : 150
--hid_size_pol      : 150
--hid_size_dec      : 150
--cell_type         : lstm
```

# License
MultiWOZ is an open source toolkit for building end-to-end trainable task-oriented dialogue models.
It is released by Paweł Budzianowski from Cambridge Dialogue Systems Group under the MIT License.

# Bug Report
If you have found any bugs in the code, please contact: budzianowski at gmail dot com
