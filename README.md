# Imágenes de escritorio CloudLab

Esta carpeta contiene las imágenes Docker de escritorio utilizadas por CloudLab.
Todas están basadas en imágenes de [Kasm](https://www.kasmweb.com/) y están
preparadas para ejecutarse con el usuario `kasm-user` (UID `1000`).

## Imágenes disponibles

| Carpeta | Imagen base | Personalización |
| --- | --- | --- |
| `alpine/` | `kasmweb/core-alpine-323:1.19.0` | Instala `sudo` y `bash`. |
| `debian/` | `kasmweb/core-debian-trixie:1.19.0` | Instala `sudo`. |
| `fedora/` | `kasmweb/core-fedora-43:1.19.0` | Instala `sudo`. |
| `kali/` | `kasmweb/core-kali-rolling:1.19.0` | Configura `sudo`. |

Todas las imágenes:

- Copian `public/background.png` como fondo predeterminado.
- Configuran un prompt de terminal con usuario, host y directorio actual.
- Permiten ejecutar `sudo` sin contraseña para `kasm-user`.
- Usan `/home/kasm-user` como directorio de trabajo.
- Ejecutan el proceso final con UID `1000`, no como `root`.

## Requisitos

- Docker instalado y en ejecución.
- Acceso a Docker Hub para descargar las imágenes base de Kasm.
- Ejecutar los comandos desde esta carpeta (`images/`).

## Construir una imagen

```bash
docker build -t cloudlab/alpine:latest ./alpine
docker build -t cloudlab/debian:latest ./debian
docker build -t cloudlab/fedora:latest ./fedora
docker build -t cloudlab/kali:latest ./kali
```

Para construir solamente una imagen:

```bash
docker build -t cloudlab/<distribucion>:latest ./<distribucion>
```

Reemplaza `<distribucion>` por `alpine`, `debian`, `fedora` o `kali`.

## Ejecutar una imagen

Las imágenes requieren un entorno compatible con Kasm para proporcionar la
sesión de escritorio. Para una comprobación básica de que la imagen se puede
iniciar:

```bash
docker run --rm -it cloudlab/alpine:latest /bin/bash
```

Sustituye `alpine` por la distribución que quieras probar. Dentro del
contenedor, el usuario esperado es `kasm-user` y el directorio inicial es
`/home/kasm-user`.

## Agregar personalizaciones

1. Modifica el `Dockerfile` de la distribución correspondiente.
2. Mantén las rutas y permisos de Kasm, especialmente el usuario `kasm-user`.
3. Si cambias el fondo, reemplaza `public/background.png`.
4. Reconstruye la imagen después de cada cambio.

No agregues contraseñas, tokens ni otros secretos a los Dockerfiles o a los
archivos copiados durante la construcción.
