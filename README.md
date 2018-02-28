# research-recsys

### Данный репозиторий является отчетом о моей научной деятельности перед научным руководителем. Основным объектом исследований являются **системы рекомендаций.**
---

## 2018-02-27

На сайте [RecSys Challenge](https://www.recsyschallenge.com/2018/) уже анонсированы некоторые детали предстоящего конкурса. Задача будет заключаться в автоматическом продолжении списка воспроизведения, то есть добавление одного или нескольких треков в плейлист так, чтобы сохранились его исходные целевые характеристики. 

В рамках этой задачи Spotify выпустил датасет из 1 миллиона пользовательских плейлистов. Набор данных включает название каждого плейлиста, а также список треков и некоторые метаданные (автор, альбом и т.д.). Тестовый набор будет состоять из набора плейлистов, в которых пропущены несколько треков. Задача будет заключаться в том, чтобы предсказать недостающие треки в этих плейлистах.

Для более подробного понимания задачи прочитал несколько статей:

1. [Steerable Playlist Generation by Learning Song Similarity from Radio Station Playlists (2009)](https://github.com/amirassov/research-recsys/tree/master/papers/https://github.com/amirassov/research-recsys/blob/master/papers/STEERABLE%20PLAYLIST%20GENERATION%20BY%20LEARNING%20SONG%20SIMILARITY%20FROM%20RADIO%20STATION%20PLAYLISTS%20(2009).pdf)
Основная идея статьи заключается в обучении классификатора на датасете, где объектами являются пары/тройки песен, а ответы равны единице, если эти песни встречаются вместе в каком-нибудь плейлисте и нулю, иначе. В качестве признаков используются аудиопризнаки. 

2. [Automated generation of music playlists. Survey and experiments (2014)](https://github.com/amirassov/research-recsys/blob/master/papers/Automated%20generation%20of%20music%20playlists.%20Survey%20and%20experiments%20(2014).pdf)
Дается обзор методам генераций плейлистов. Многие описанные алгоритмы можно использовать как начальный бейзлайн.

3. [Exploiting Music Play Sequence for Music Recommendation (2017) (2017)](https://github.com/amirassov/research-recsys/blob/master/papers/Exploiting%20Music%20Play%20Sequence%20for%20Music%20Recommendation%20(2017).pdf), [Sequence-based context-aware music recommendation](https://github.com/amirassov/research-recsys/blob/master/papers/Sequence-based%20context-aware%20music%20recommendation%20(2017).pdf)
Предложены методы song2vec, music2vec, которые являются аналогоми алгоритма word2vec.

4. [Learning to embed music and metadata for context-aware music recommendation (2017)](https://github.com/amirassov/research-recsys/blob/master/papers/Learning%20to%20embed%20music%20and%20metadata%20for%20context-aware%20music%20recommendation%20(2017).pdf)
Статья от авторов music2vec, где дополнительно используется метаинформация. Получаем аналог метода doc2vec.

5. [Current Challenges and Visions in Music Recommender Systems Research (2017)](https://github.com/amirassov/research-recsys/blob/master/papers/Current%20Challenges%20and%20Visions%20in%20Music%20Recommender%20Systems%20Research%20(2017).pdf)
Обзор состояния музыкальных рекомендательных систем от организаторов Spotify RecSys Challenge 2018.

6. [Music Playlist Continuation by Learning from Hand-Curated Examples and Song Features (2017)](https://github.com/amirassov/research-recsys/blob/master/papers/Music%20Playlist%20Continuation%20by%20Learning%20from%20Hand-Curated%20Examples%20and%20Song%20Features%20(2017).pdf)
Решается задача автоматической генерации плейлиста путем классификации всех песен по плейлистам. В качестве алгоритма используется нейронная сеть с $$\{2, 3, 4\}$$ слоями. Признаки генерируется с аудиосигнала, метаданных. Также создаются латентные признаки из другого датасета методом коллаборативной фильтрации. Алгоритм сложно масштабируем для 1 млн плейлистов. 

7. [A Hybrid Approach to Music Playlist Continuation Based on Playlist-Song Membership (2018)](https://github.com/amirassov/research-recsys/blob/master/papers/A%20Hybrid%20Approach%20to%20Music%20Playlist%20Continuation%20Based%20on%20Playlist-Song%20Membership%20(2018).pdf)
Статья от авторов предыдущей статьи, где задача решается путем классификации пары <плейлист, песня> на два класса: 1, если песня встречается в плейлисте, 0 если иначе. Используется нейронная сеть с двумя блоками: первый блок кодирует признаки во векторное представление. Дальше конкатенируется вектор песни со средним вектором всех песен в плейлисте и проходит через блок классификации.

**Выводы:**
1. Задачу автоматического продолжения плейлиста можно рассматривать как обычную задачу рекомендаций, где пользователями являются плейлисты. Тогда для её решения мы можем применять уже существующие методы рекомендательных систем. Например, FFM.

2. Хочется попробовать улучшить идею статьи [A Hybrid Approach to Music Playlist Continuation Based on Playlist-Song Membership (2018)](https://github.com/amirassov/research-recsys/blob/master/papers/A%20Hybrid%20Approach%20to%20Music%20Playlist%20Continuation%20Based%20on%20Playlist-Song%20Membership%20(2018).pdf). Например, учесть порядок песен в плейлисте.





## 2017-12-26

Разбирался с непрерывным представлением пользователей и предметов для рекомендательных систем. Прочитал следующие статьи:

1. Оригинальные статьи про модель **word2vec**: [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781), [Distributed Representations of Words and Phrases and their Compositionality](https://arxiv.org/abs/1310.4546):
    - Предлагаются две архитектуры для построения непрерывных представлений слов. Обе являются нейронными сетями с одним скрытым слоем. Первая модель **CBOW** (Continuous Bag-of-Words) пытается предсказать слово по его контексту, а следующая модель **skip-gram**, наоборот, по слову предсказывает контекст. 
    - Сразу же предлагается метод оптимизации для обучения **skip-gram**, которая называется **негативным сэмплированием** (Negative Sampling). Суть метода заключается в том, что сумма по всем контекстам, которая возникает как нормировка при вычислении вероятности контекста при условии определенного слова как softmax-функцию, заменяется на сумму по сэмплированным негативным контекстам. Подробно описывается здесь [word2vec Explained: deriving Mikolov et al.'s negative-sampling word-embedding method.
](https://arxiv.org/abs/1402.3722)

2. [E-commerce in Your Inbox: Product Recommendations at Scale](https://arxiv.org/abs/1606.07154):
	* В данной статье ученые из Yahoo предлагают модель для непрерывного представления пользователей и предметов **prod2vec**, которая основывается на идее **word2vec**: если пользователь $$u$$ покупал предметы в порядке $$(p_1, p_2, \cdots, p_n)$$, тогда мы можем рассматривать этот вектор как предложение, а предметы как слова и обучать **skip-gram** с негативным сэмплированием.
	* Авторы рассматривают задачу рекомендаций для пользователей Yahoo Mail. Поэтому пользователь может купить несколько предметов одновременно. Для решения проблемы предлагается модель **bagged-prod2vec**, которая обучается на уровне писем, а не предметов. Письма представляются в виде bag-of-words от предметов.
	* Аналогично модели **doc2vec**, предлагается модель **user2vec**, где используется архитектура CBOW не только с контекстами на входе, но и информацией о пользователе.
	* Сложно оценить качество предложенных моделей, так как в статье не раскрывается точность (accuracy) после проведения эксперимента. Но видно, что **prod2vec** работает лучше, чем предлагать самые популярные товары и метод, который основан на частоте пар предметов. 

3. [Meta-Prod2Vec - Product Embeddings Using Side-Information for Recommendation](https://arxiv.org/abs/1607.07326):
	* В статье предлается метод **Meta-prod2vec**, который является модификацией **prod2vec** с учетом метаданных предмета.
	* Функция потерь **Meta-prod2vec** расширяется до суммы пяти слагаемых, которые описывают условные вероятности $$p(context | item)$$, $$p(context | item\_metadata)$$, $$p (item | item\_metadata)$$, $$p (context\_metadata | item)$$, $$p (context\_metadata  | item\_metadata)$$.
	* Авторы сравнивают методы на задаче рекомендаций музыки. В результате получают, что линейный ансамбль **Meta-prod2vec** и коллаборативной модели с косинусным расстоянием предметов показывает лучшее качество по всем метрикам (**HR@K**, **NDCG@K**). Также авторы показывают, что при условии холодного старта **Meta-prod2vec** работает лучше метода **prod2vec**.
