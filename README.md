# films_list
## Описание
Этот проект представляет собой каталог фильмов с их общим описанием: аннотация к фильму, актерский состав, режиссер,  год и страна производства, жанр, продолжительность.
Пользователь — это человек, который хочет: находить информацию о фильмах; сохранять понравившиеся; вести список «Хочу посмотреть»; быстро искать произведения по жанру, автору или названию.
Действия, выполняемые пользователем на сайте: просмотр каталога; поиск по названию; фильтрация по жанру; просмотр карточки фильма; добавление в «Хочу посмотреть»; регистрация и логин.

## Структура БД
### Таблица "countries"
|     Поле     | Тип Данных |      Атрибут     |     Описание    |
|  country_id  |   INTEGER  |         -        |  Первичный ключ |
| counrty_name |    TEXT    |  NOT NULL UNIQUE | Название страны |
### Таблица "genres"
|     Поле     | Тип Данных |      Атрибут     |    Описание    |
|   genre_id   |   INTEGER  |         -        | Первичный ключ |
|  genre_name  |    TEXT    |  NOT NULL UNIQUE | Название жанра |
### Таблица "directors"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|   director_id    |   INTEGER  |     -     |   Первичный ключ  |
|  name_director   |    TEXT    |  NOT NULL |   Имя режиссера   |
| surname_director |    TEXT    |  NOT NULL | Фамилия режиссера |
| url_img_director |    TEXT    |     -     |   Ссылка на фото  |
Дополнительно: UNIQUE (name_director, surname_director)
### Таблица "actors"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|     actor_id     |   INTEGER  |     -     |   Первичный ключ  |
|    name_actor    |    TEXT    |  NOT NULL |     Имя актера    |
|   surname_actor  |    TEXT    |  NOT NULL |   Фамилия актера  |
|   url_img_actor  |    TEXT    |     -     |   Ссылка на фото  |
Дополнительно: UNIQUE (name_actor, surname_actor)
### Таблица "movies"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|     movie_id     |   INTEGER  |     -     |   Первичный ключ  |
|      title       |    TEXT    |  NOT NULL |  Название фильма  |
|     duration     |    TEXT    |  NOT NULL |    Длительность   |
|    description   |    TEXT    |  NOT NULL |      Описание     |
|  year_of_release |    TEXT    |  NOT NULL |     Год релиза    |
|    country_id    |   INTEGER  | REFERESCES|       Страна      |
Дополнительно: UNIQUE (title, year_of_release, country_id)
### Таблица "actor_cast"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|     actor_id     |   INTEGER  |  NOT NULL |     ID актера     |
|     movie_id     |   INTEGER  |  NOT NULL |     ID фильма     |
Дополнительно: 
FOREIGN KEY (movie_id) REFERENCES movies(movie_id),
FOREIGN KEY (actor_id) REFERENCES actors(actor_id),
UNIQUE (actor_id, movie_id)
### Таблица "genre_cast"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|     genre_id     |   INTEGER  |  NOT NULL |      ID жанра     |
|     movie_id     |   INTEGER  |  NOT NULL |     ID фильма     |
Дополнительно: 
FOREIGN KEY (movie_id) REFERENCES movies(movie_id) ON DELETE CASCADE,
FOREIGN KEY (genre_id) REFERENCES genres(genre_id) ON DELETE CASCADE,
UNIQUE (genre_id, movie_id)
### Таблица "director_cast"
|      Поле        | Тип Данных |  Атрибут  |      Описание     |
|   director_id    |   INTEGER  |  NOT NULL |    ID режиссера   |
|     movie_id     |   INTEGER  |  NOT NULL |     ID фильма     |
Дополнительно: 
FOREIGN KEY (movie_id) REFERENCES movies(movie_id) ON DELETE CASCADE,
FOREIGN KEY (director_id) REFERENCES directors(director_id) ON DELETE CASCADE,
UNIQUE (movie_id, director_id)
