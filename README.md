# research-recsys

### Данный репозиторий является отчетом о моей научной деятельности перед научным руководителем. Основным объектом исследований являются **системы рекомендаций.**
---

## 2017-12-26

Разбирался с непрерывным представлением пользователей и предметов для рекомендательных систем. Прочитал следующие статьи:

1. Оригинальные статьи про модель **word2vec**: [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781), [Distributed Representations of Words and Phrases and their Compositionality](https://arxiv.org/abs/1310.4546):
    - Предлагаются две архитектуры для построения непрерывных представлений слов. Обе являются нейронными сетями с одним скрытым слоем. Первая модель **CBOW** (Continuous Bag-of-Words) пытается предсказать слово по его контексту, а следующая модель **skip-gram**, наоборот, по слову предсказывает контекст. 
    - Сразу же предлагается метод оптимизации для обучения **skip-gram**, которая называется **негативным сэмплированием** (Negative Sampling). Суть метода заключается в том, что сумма по всем контекстам, которая возникает как нормировка при вычислении вероятности контекста при условии определенного слова как softmax-функцию, заменяется на сумму по сэмплированным негативным контекстам. Подробно описывается здесь [word2vec Explained: deriving Mikolov et al.'s negative-sampling word-embedding method.
](https://arxiv.org/abs/1402.3722)

2. [E-commerce in Your Inbox: Product Recommendations at Scale](https://arxiv.org/abs/1606.07154):
	* В данной статье ученые из Yahoo предлагают модель для непрерывного представления пользователей и предметов **prod2vec**, которая основывается на идее **word2vec**: если пользователь $$u$$ покупал предметы в порядке $$(p_1, p_2, \cdots, p_n)$$, тогда мы можем рассматривать этот вектор как предложение, а предметы как слова и обучать **skip-gram** с негативным сэмплированием.
<<<<<<< HEAD
	* Авторы рассматривают задачу рекомендаций для пользователей Yahoo Mail. Поэтому пользователь может купить несколько предметов одновременно. Для решения проблемы предлагается модель **bagged-prod2vec**, которая обучается на уровне писем, а не предметов. Письма представляются в виде bag-of-words от предметов.
=======
	* Авторы рассматривают задачу рекомендаций для пользователей Yahoo Mail. Поэтому пользователь может купить несколько предметов одновременно. Для решения проблемы предлагается модель **bagged-prod2vec**, которая обучается на уровне писем, а не предметов. Письма представляется в виде bag-of-words от предметов.
>>>>>>> 623d0448a503e983f9f057068e2f98bdcfa4c3db
	* Аналогично модели **doc2vec**, предлагается модель **user2vec**, где используется архитектура CBOW не только с контекстами на входе, но и информацией о пользователе.
	* Сложно оценить качество предложенных моделей, так как в статье не раскрывается точность (accuracy) после проведения эксперимента. Но видно, что **prod2vec** работает лучше, чем предлагать самые популярные товары и метод, который основан на частоте пар предметов. 

3. [Meta-Prod2Vec - Product Embeddings Using Side-Information for Recommendation](https://arxiv.org/abs/1607.07326):
	* В статье предлается метод **Meta-prod2vec**, который является модификацией **prod2vec** с учетом метаданных предмета.
	* Функция потерь **Meta-prod2vec** расширяется до суммы пяти слагаемых, которые описывают условные вероятности $$p(context | item)$$, $$p(context | item\_metadata)$$, $$p (item | item\_metadata)$$, $$p (context\_metadata | item)$$, $$p (context\_metadata  | item\_metadata)$$.
	* Авторы сравнивают методы на задаче рекомендаций музыки. В результате получают, что линейный ансамбль **Meta-prod2vec** и коллаборативной модели с косинусным расстоянием предметов показывает лучшее качество по всем метрикам (**HR@K**, **NDCG@K**). Также авторы показывают, что при условии холодного старта **Meta-prod2vec** работает лучше метода **prod2vec**.
