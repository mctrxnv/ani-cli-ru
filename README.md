# anicli-ru

---

Скрипт для поиска и просмотра аниме из терминала с русской озвучкой или субтитрами.
Поддерживает unix, linux, windows 10/11 (windows terminal)

https://github.com/vypivshiy/ani-cli-ru/assets/59173419/bf7e78bd-cdd1-4871-a5b3-f48e6ed7ec28

## Установка

- Поддерживает python 3.8 или выше
- требуется [mpv видеоплеер](https://github.com/mpv-player/mpv)
  - поддержка vlc присутствует, работоспособность мало тестировалась

| менеджер пакетов                                                       | установка                   | обновление                        |
| ---------------------------------------------------------------------- | --------------------------- | --------------------------------- |
| [uv (рекомендуется)](https://docs.astral.sh/uv/#installation)          | `uv tool install anicli-ru` | `uv tool upgrade anicli-ru`       |
| [pipx](https://pipx.pypa.io/stable/installation/)                      | `pipx install anicli-ru`    | `pipx upgrade anicli-ru`          |
| [pip (не рекомендуется см PEP 668)](https://peps.python.org/pep-0668/) | `pip install anicli-ru`     | `pip install anicli-ru --upgrade` |

Если нужен только программный api интерфейс парсеров: [anicli-api](https://github.com/vypivshiy/anicli-api)

## Nix

- Во [флейке](./flake.nix) имеются:

  1. packages `nix run github:vypivshiy/ani-cli-ru`, a также вместо `run` `build` для `./result`
  2. devShells `nix shell github:vypivshiy/ani-cli-ru`
  3. overlays `pkgs.anicli-ru -> inputs.anicli-ru.packages.<system>.default` ! может не работать

- Установка:

  1. system-wide `environment.systemPackages = [ pkgs.anicli-ru ];`
  2. user-only `home.packages = [ pkgs.anicli-ru ];`

## Usage:

```shell
anicli-ru
```

### Примеры:

Сменить источник:

```shell
anicli-ru -s anilibria
```

Запуск поиска/онгоингов при старте:

```shell
# запуск и поиск тайтлов по фразе `lain`
anicli-ru --search "lain"
# запуск и вывод онгоингов
anicli-ru --ongoing
```

Передача дополнительных аргументов в плеер.
Например, если у вас специально настроенный профиль в mpv плеере:

```shell
anicli-ru -pa="--profile=my_profile"
```

## Ключи запуска

```
-s --source - выбор источника. По умолчанию "animego"
-q --quality - минимально выбранное разрешение видео. Доступны: 0, 144, 240, 360, 480, 720, 1080. По умолчанию 1080
  Например, если вы установили 1080 и такое видео отсутстует - выведет максимально допустимое
--ffmpeg - использовать ffmpeg для перенаправления видеопотока в видеоплеер
-p --player - какой видеоплеер использовать. доступны "vlc", "mpv". По умолчанию "mpv"
--m3u - для SLICE-режима просмотра создавать плейлист (ЭКСПЕРИМЕНТАЛЬНЫЙ РЕЖИМ, СОБИРАЕТ ВИДЕО МЕДЛЕННО)
--m3u-size - максимальный размер m3u плейлиста. По умолчанию 12
-pa --playlist-args - дополнительные аргументы для плеера. Например, -pa="--profile=foo" -pa="--no-video".
  подробнее о них смотрите в документации по плееру
--search - запустить и найти тайтл по строке
--ongoing - запустить и найти онгоинги
```
