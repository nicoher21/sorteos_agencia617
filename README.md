# Sorteos a Telegram — Agencia 617

Este repositorio hace una sola cosa: entra a la página de Caja Social de Santiago del Estero
después de cada sorteo y te manda el resultado a tu Telegram, con el posteo ya armado para
copiar y pegar.

**No depende de ninguna computadora.** Corre en la nube de GitHub, así que funciona aunque
tengas la PC apagada, suspendida o desconectada.

---

## Cómo funciona

| Sorteo | Hora Argentina | Se ejecuta |
|---|---|---|
| La Previa | 10:30 | lunes a sábado |
| Matutina | 12:35 | todos los días |
| Vespertina | 15:30 | todos los días |
| Tardecita | 20:00 | lunes a sábado |
| Nocturna | 22:30 | lunes a sábado |

Los domingos solo corren Matutina y Vespertina, que son los dos sorteos que hay ese día.

No hay que decirle qué sorteo mandar: el sistema mira la hora UTC y lo deduce solo. Por eso
el archivo de configuración es tan corto.

Si la página oficial se atrasa con la publicación, el sistema espera hasta 25 minutos
consultando cada minuto, y recién ahí se rinde.

---

## Instalación (se hace una sola vez)

### 1. Crear la cuenta y el repositorio

1. Entrá a **github.com** y creá una cuenta (es gratis).
2. Arriba a la derecha, en el **`+`** → **New repository**.
3. Poné un nombre, por ejemplo `sorteos-agencia617`.
4. Marcá **Private** (privado).
5. **No** tildes "Add a README file" — ya trae uno este paquete.
6. Clic en **Create repository**.

### 2. Subir estos archivos

En la pantalla que queda, clic en **uploading an existing file** y arrastrá **todo el
contenido de esta carpeta**, incluyendo la carpeta oculta `.github`.

> Importante: la carpeta `.github` tiene que subir tal cual. Si no la ves en tu computadora
> es porque Windows oculta las carpetas que empiezan con punto — arrastrá la carpeta
> completa igual, se sube igual.

Después clic en **Commit changes**.

### 3. Cargar las dos claves secretas

1. En el repositorio, entrá a **Settings** (arriba a la derecha).
2. En el menú de la izquierda: **Secrets and variables** → **Actions**.
3. Clic en **New repository secret** y cargá estas dos, una por vez:

   | Name | Value |
   |---|---|
   | `TELEGRAM_TOKEN` | el token de tu bot |
   | `TELEGRAM_CHAT_ID` | `6086015389` |

### 4. Probar que funciona

1. Entrá a la pestaña **Actions** del repositorio.
2. A la izquierda, clic en **Sorteos a Telegram**.
3. A la derecha, botón **Run workflow** → dejá la rama en `main` → **Run workflow**.
4. Esperá unos segundos: si el icono queda **verde con un tilde**, salió todo bien y te
   tiene que haber llegado el mensaje al celular.

Si queda **rojo**, entrá al trabajo fallido y fijate el error (normalmente es una de las dos
claves mal cargadas).

---

## Uso diario

No tenés que hacer nada. Te llega el mensaje solo después de cada sorteo.

Si algún día querés mandar un sorteo por fuera del horario: pestaña **Actions** →
**Run workflow**. No hay que elegir nada: el sistema mira la hora y manda el sorteo que
corresponde a ese momento.

---

## Si algo falla

**GitHub avisa por correo** cuando un trabajo falla. Para que te llegue:
**Settings** (de tu cuenta, no del repo) → **Notifications** → asegurate de tener
habilitado el correo en *Actions*.

Causas habituales de falla:

- El sitio de Caja Social está caído o cambió el formato de la página.
- Pasaron más de 25 minutos y el sorteo todavía no se publicó.
- Una de las dos claves secretas está mal cargada.

**Un aviso:** si pasan 60 días sin que toques el repositorio, GitHub puede desactivar las
tareas programadas. Te avisa por correo y se reactiva con un clic desde la pestaña Actions,
así que no es grave — pero si dejan de llegarte los mensajes después de mucho tiempo,
revisá eso primero.

---

## Archivos

| Archivo | Qué hace |
|---|---|
| `enviar_sorteos.py` | Busca el sorteo, arma el posteo y lo manda a Telegram |
| `.github/workflows/sorteos.yml` | Define los 5 horarios en que se ejecuta |

No usa ninguna librería externa: funciona con Python estándar y nada más.
