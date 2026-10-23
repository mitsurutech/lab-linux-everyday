# Lab de comandos de Linux de cada día: ls, grep, tail -f, ssh, scp y kill en una VM Ubuntu

[English](README.md) | [Français](README.fr.md) | [日本語](README.ja.md) | [Español](README.es.md)

[![check](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml/badge.svg)](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml)

Un **lab de comandos de Linux** listo para el aula, de la [plataforma de aprendizaje MitsuruTech](https://mitsurutech.co.uk/es/learning), donde los centros dan a cada estudiante su propia máquina Ubuntu y una terminal en el navegador. Tiene algo real para cada comando que una persona que desarrolla software escribe sin buscarlo: **recorrer y buscar archivos** (`ls`, `cd`, `find`, `grep`), **leer un registro que aún se está escribiendo** (`tail -f`), **encontrar y detener un proceso** (`ps | grep`, `kill`, `kill -9`), **descargar y descomprimir archivos** (`curl`, `wget`, `zip`, `gzip`) y **entrar en otra cuenta y copiarle archivos** (`ssh`, `scp`). No se instala nada en el ordenador del estudiante.

## Qué hay en la máquina

| Qué | Dónde | Para |
| --- | --- | --- |
| Un registro con una hora de líneas que crece cada dos segundos | `/var/log/test.log` | `tail`, `grep`, contar errores |
| Un archivo comprimido y un archivo para comprimir | `~/test.zip`, `~/test` | `unzip`, `gzip` |
| Un árbol pequeño para recorrer y una carpeta donde borrar sin riesgo | `~/projects`, `~/scratch` | `ls`, `cd`, `find`, `cp`, `mv`, `rm -rf` |
| Un servidor web en el puerto 8000 con dos archivos pequeños | `localhost:8000` | `curl`, `wget` |
| Dos procesos, uno de los cuales ignora un `kill` simple | `lab-worker`, `lab-stubborn` | `ps`, `kill`, `kill -9` |
| Una segunda cuenta, `dev`, a la que se entra con clave como `devbox` | `ssh devbox` | `ssh`, `scp` |

La segunda cuenta está en la **misma máquina**, no en otra: los comandos son los mismos y una segunda VM solo añadiría espera. El lab no tiene comprobación ni tarea. Las cinco lecciones de la plataforma son la actividad, y quien quiera poner nota prepara su propia entrega.

## Qué hay en el archivo

`linux-everyday.lab.yaml` es una **definición de lab de VM** completa, exactamente lo que ejecuta la plataforma:

| Clave | Qué es |
| --- | --- |
| `cpus`, `memory`, `disk` | el tamaño de la VM de cada estudiante: 1 CPU, 1024 MB y 10 GB |
| `open` | los puertos que se abren en el navegador: ninguno, el lab es la terminal |
| `setup` | un script que se ejecuta una vez, como root, la primera vez que arranca la VM de cada estudiante: instala unos paquetes del archivo de Ubuntu, crea el registro, los archivos, los dos procesos, el servidor web y la segunda cuenta, y escribe un README en la carpeta personal |

## Usarlo en la plataforma

1. En tu módulo, añade una tarea y elige la tarjeta **Lab de VM Ubuntu**.
2. Pulsa el ejemplo, o pega el contenido de `linux-everyday.lab.yaml`. Usar un ejemplo sustituye el texto, y Deshacer recupera el tuyo.
3. Publica y prueba primero tu propia copia. Cada estudiante recibe una VM propia, que se conserva entre sesiones.
4. Asígnala como cualquier tarea, o abre las lecciones de la biblioteca y pulsa Ejecutar junto a un comando.

La [página del manual para este lab](https://mitsurutech.co.uk/es/help/lab-linux-everyday), su [guía de los labs de VM Ubuntu](https://mitsurutech.co.uk/es/help/labs) y su [página de labs de ejemplo](https://mitsurutech.co.uk/es/help/sample-labs) explican el resto. ¿Aún no tienes cuenta de centro? [Tu primer año es gratis](https://mitsurutech.co.uk/es/pricing) hasta 50 estudiantes, y [registrarse](https://mitsurutech.co.uk/es/signup) pide una dirección de correo.

## Comprobar el archivo

En cada push, `.github/workflows/check.yml` comprueba que el archivo es YAML válido con las claves de arriba y que `setup` cabe en el límite de 16 KB de la plataforma. No arranca ninguna VM: eso se hace en las máquinas de la plataforma.

## Qué no funciona en un lab

La VM llega al archivo de paquetes de Ubuntu, PyPI, npm y GitHub, y a nada más, así que no se puede apuntar a un servidor de internet. Por eso el servidor web está dentro del lab.

## Acerca de

Hecho por [Mitsuru Technologies](https://mitsurutech.co.uk) para la [plataforma de aprendizaje MitsuruTech](https://mitsurutech.co.uk/es/learning): Python, Java, Go, Node, SQL y Linux en el navegador para centros educativos, con labs de contenedores, labs de VM, aplicaciones web desplegadas desde GitHub y cuestionarios que se corrigen solos. Prueba código sin cuenta en el [área de pruebas](https://mitsurutech.co.uk/es/playground).

Más labs del mismo sitio: [lab-linux-admin](https://github.com/mitsurutech/lab-linux-admin), [lab-linux-privesc](https://github.com/mitsurutech/lab-linux-privesc), [lab-incident-response](https://github.com/mitsurutech/lab-incident-response), [lab-netlab](https://github.com/mitsurutech/lab-netlab), [lab-git-gitea](https://github.com/mitsurutech/lab-git-gitea) y [lab-sample](https://github.com/mitsurutech/lab-sample).

## Licencia

Esta obra está bajo la licencia [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). Puedes compartirla y adaptarla para aprender y enseñar, si citas a Mitsuru Technologies Ltd, no la usas con fines comerciales y compartes lo que hagas con ella bajo la misma licencia. El texto completo está en el archivo `LICENSE`.

`zip`, `unzip`, `curl`, `wget`, `openssh-server`, `vim` y `python3` se instalan desde el archivo de Ubuntu cuando arranca una VM; aquí no se distribuye nada de ellos.
