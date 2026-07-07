# NetfloxPyDesk - España (PyQt6)

## Integrantes
- Tomas B. Ezequiel Guzman - [https://github.com/tomasgz7](https://github.com/tomasgz7)
- Natalia Laime - [github.com/natuchess](https://github.com/natuchess)
- Graciela Vergottini - [github.com/vergottinigra49](https://github.com/vergottinigra49)

> **Warning**: usar PyQt6 > PyQt6-6.8.1 PyQt6-Qt6-6.8.2 PyQt6-sip-13.10.0 (`pip install PyQt6`)

![widgets_view](img/image-1.png)

![home_vie](img/image-2.png)

NetfloxPyDesk es una aplicación de escritorio hecha con Python, Qt Designer y PyQt6, construida sobre un template base UIXCore (dark/flat GUI para PyQt6).

Incluye navegación por menú dinámico con las secciones HOME, Add User, Custom Widgets y Movies (listado de películas en grilla).

Este proyecto funciona muy bien en Windows; en Linux y macOS hay problemas conocidos con el tamaño de las fuentes y la barra de título personalizada no funciona correctamente (heredado del template base).

## Requerimientos

```sh
python -m venv env
.\env\Scripts\Activate
pip install PyQt6
```

## Cómo correr

```sh
python main.py
```

## Menús

![add-menus](img/image-3.png)

- **HOME** - página de inicio
- **Add User** - (en desarrollo)
- **Custom Widgets** - showcase de widgets del template
- **Movies** - listado de películas en formato de grilla (ver detalle abajo). Es la sección que se muestra por defecto al iniciar la aplicación.


## Movies (v0) - Listado de Películas

<img width="732" height="510" alt="image" src="https://github.com/user-attachments/assets/88e73961-89e1-4f6f-8a22-7f2b1d55ae92" />


Al hacer clic en el menú **"Movies"** (o al iniciar la aplicación, ya que queda seleccionado
por defecto) se despliega una pantalla única que contiene solamente una grilla
(`QTableWidget`) con el listado de películas, sin distracciones adicionales.

### Columnas de la grilla

| Columna  | Descripción                       |
|----------|------------------------------------|
| Title    | Título de la película              |
| Year     | Año de estreno (release_date)      |
| Duration | Duración en minutos                |

### Características

- La grilla **no permite edición**: un doble clic sobre una celda no activa el modo edición.
- La grilla **no permite ordenamiento** por columnas.
- La selección solo puede hacerse **por fila completa**, una fila a la vez.
- Los datos son de **prueba (hardcode)**: una lista de diccionarios en memoria con las
  claves `title`, `year` y `duration`. (Pendiente para una próxima versión: reemplazar
  por datos reales, por ejemplo desde `movies_full_data.csv` o una base PostgreSQL).
- Se aplica un **estilo dark** consistente con el resto de la aplicación (fondo oscuro,
  texto claro, selección en celeste).

### Archivo

La funcionalidad vive en un módulo aparte, `movies_module.py`, que define la clase
`MovieListPage` (hereda de `QWidget`). Se integra en `main.py` agregándose al layout
de `page_movies` dentro del `QStackedWidget`:

```python
from movies_module import MovieListPage

self.movie_list_page = MovieListPage(self.ui.page_movies)
self.ui.verticalLayout_movies.addWidget(self.movie_list_page)
```

### Ejecución independiente (para pruebas)

El módulo puede ejecutarse solo, sin necesidad de levantar toda la aplicación:

```sh
python movies_module.py
```

Esto abre una ventana de 600x400 mostrando únicamente la grilla de películas de prueba,
útil para depurar el comportamiento de la tabla de forma aislada.

## Créditos
Basado en el template UIXCore (PyQt6) - desk template dark/flat GUI.
