---
layout: post
title: Las entrañas del sistema
---

Deja de leer, de verdad, no lo hagas. La entrada de hoy no es ninguna reflexión, simplemente el ordenador me ha estado dando guerra y de la mala ostia me he cargado varias cosas.

Como la cosa no pinta bien y puede que en cualquier momento deje de funcionar, sería una catástrofe perder toda la información y la ergonomía de trabajo que tanto esfuerzo me ha llevado cultivar, es por ello que me dispongo a dejar plasmado todo lo utilizado por si en un futuro necesito recolectar la configuración y programas utilizados en una instalación limpia.

## 21 de noviembre de 2011

La base es un Acer Predator G3610 a la cual se le han ido actualizando algunos componentes:

- OS: Debian 11.
- Memory: 24 GiB DDR3.
- CPU: Intel i7-2600 (8) @ 3.800GHz (2011).
- GPU: Gigabyte NVIDIA GeForce GTX 1650 SUPER - 4 GiB DDR6 (2019).

## *Neofetch*

Obviamente no me podía dejar de banda el buen *neofetch*:

![](assets/img/neofetch.png)

Ahora vamos a ir desgranando parte por parte.

### Packages:

- Okular o Zathura: para leer documentos pdf. 
- Steam, Firefox, Anki: obvio.
- PulseAudioControl: manejo de los dispositivos de audio.
- TexMaker: para la creación de documentos pdf (más adelante enseño cómo genero los documentos e instalo TexLive).
- Blueman Bluetooth Manager: manejo de los dispositivos con Bluetooth.
- Nvidia X Server Settings: en mi caso los genero directamente de la página web de Nvidia pues los paquetes que hay en los repositorios son muy antiguos.
- CPU-X y Psensor: control de la temperatura y parámetros del ordenador.

#### Firefox:

- Tab Session Manager.
- Wallabag.
- SingleFile.
- The Marvellous Suspender.
- Unhook.
- SteamDB.
- Keepa.

#### Anki:

- Button Colors Good Again.
- ReColor.
- Review Heatmap.
- Study Time Stats.

#### TexMaker:

1. Primero instalamos TexLive con **sudo apt-get install texlive-full**.
2. Seguimos con TexMaker **sudo apt-get install texmaker**.
3. Creamos un documento, que en mi caso hago uso de Markdown y LuaLaTex como compilador de PDF. Para el que quiera aquí tiene la plantilla completa:

![](assets/img/texmaker.png)

### AppImages:

- HardDisk Sentinel GUI: lectura de parámetros de los discos duros.
- BitWarden, Ledger, CDC-Defi, QBittorrent: obvio.
- Suyu: no quiero problemas con la gran N así que me lo reservo en mi GDrive.
- Real-Video-Enhancer: reescalado de imagenes de los vídeos mediante IA (top pero ojo con las temperaturas).

### Desktop Enviorment (DE), Window Manager (WM):

Como DE usamos KDE Plasma 5.20.5 (el que venía con Debian 11) y Kwin como WM pero modificados para parecerse lo máximo a un tipo i3WM pero con las comodidades de un DE. Para muestra un botón:

![](assets/img/de-wm.png)

KDE Plasma viene con una aplicación denominada *Plasma Style* donde yo la tengo configurada de la siguiente forma (puedes copiarla mediante *Get new...* en cada sección:

- Plasma Style > Breeze (Follow color scheme).
- Application Style > Window Decorations > Active Accent Frame.
- Colors > WhiteSurAlt.
- Icons > WhiteSurAlt.
- Cursors > WhiteSur Cursors.
- Window Management > Window Tiling > Behavior (Check y *Spawn windows at the layout end*) | Appearance (All Gaps 20px with check on *No border around tiled windows*).

Pondremos la barra de tareas arriba y le adjudicamos un espacio en el panel de 30px.

### Instalación de Debian

Si por algún casual te animas a instalar esta maravillosa distribución Linux te animo a que le pongas los siguientes parámetros:

- un Ext4 root "/", de 120GB aprox., para el sistema operativo y de tipo bootable.
- un Swap de la misma capacidad que la cantidad de GB RAM instalada.
- el resto para la Ext4 "/home" para tus datos.

Antes de finalizar la instalación te pedirá que pongas una contraseña para tu superusuario "root", pero OJO, Debian no da permisos de superusuario al mismo usuario que inice sesión en el ordenador con lo que te encontrarás el mítico problema de *user is not in the sudoers file*. Esto no ocurrirá si dejas la contraseña en blanco y Debian SÍ dará permisos de superusuario al primer usuario que se registre en el sistema.

Por si no te habías dado cuenta yo soy muy tonto y he aprendido la lección por errores de la vida, por lo que la solución a una instalación con contraseña en *root* y un usuario sin permisos es hacer *nano* a /etc/sudoers y añadir nuestro usuario, por ejemplo:

```
> # User privilege specification
> root    ALL=(ALL:ALL) ALL
> user   ALL=(ALL:ALL) ALL
```

Guardamos con *Ctrl+O* y salimos con *Ctrl+X*.

Si por algún casual no podemos editarlo por falta de permisos al usuario, debemos dejar que nuestro usuario pueda hacer uso del comando uso mediante **usermod -aG sudo TUUSUARIO**.

Finalmente hacemos un *reboot now* para que surjan efecto los cambios.

Hay veces que directamente no se puede solucionar siguiendo los pasos anteriores y lo único que queda es hacer *sudo* con cada comando ya que no nos deja permanecer como superusuarios o acceder a *root* poniendo **su** en la terminal (los cambios realizados mediante root se quedará en la carpeta de root y no en la de usuario del sistema).