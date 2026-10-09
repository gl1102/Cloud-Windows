[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

# ☁️ Cloud-Windows — Escritorio Windows gratuito en la nube

Convierte una máquina virtual Windows gratuita de GitHub Actions en un escritorio en la nube accesible desde el navegador. Abres una página web y tienes un PC con Windows; lo cierras cuando terminas. Totalmente gratis.

## ✨ Características

- 🖥️ Escritorio Windows completo, operado directamente en el navegador (cliente web noVNC)
- 📐 **Resolución automática**: al abrir la página, la resolución del escritorio se adapta automáticamente al tamaño de la ventana del navegador — móvil y PC cada uno con su ajuste; también se reajusta al redimensionar la ventana
- 🌐 Acceso mediante túnel de Cloudflare — sin IP pública, sin abrir puertos
- ⌨️ Método de entrada Sogou (搜狗输入法, Sogou Pinyin) integrado, chino listo para usar desde el primer momento (cambia entre chino e inglés con `Win + Space`)
- 🖱️ Conéctate desde el móvil, la tableta o el ordenador
- ⏱️ Cada ejecución dura hasta ~6 horas y puedes cancelarla cuando quieras
- 📦 **Edición RustDesk**: también hay un workflow con RustDesk que descarga automáticamente el RustDesk más reciente en la unidad D y lo instala de forma silenciosa en `D:\RustDesk`

## 🚀 Cómo usarlo (funciona nada más hacer fork)

### Paso 1: Haz un Fork del proyecto

Haz clic en el botón **Fork** arriba a la derecha de esta página para copiar el proyecto a tu propia cuenta de GitHub. Al terminar el fork llegarás al repositorio `tu-usuario/Cloud-Windows`.

> 💡 ¿Por qué hacer fork? GitHub Actions solo puede ejecutarse en repositorios de tu propia cuenta: con el fork obtienes permiso para ejecutarlo.

### Paso 2: Inicia el escritorio en la nube

1. Entra en la página del repositorio que forkeaste y haz clic en la pestaña **Actions** de arriba
2. A la izquierda elige un workflow (uno de los dos):
   - **Windows Cloud Desktop**: el escritorio en la nube estándar
   - **Windows Cloud Desktop + RustDesk**: la edición estándar más la descarga automática del RustDesk más reciente en la unidad D con instalación silenciosa en `D:\RustDesk` (la versión no está fijada en el código: siempre se obtiene la última release oficial)
3. Haz clic en el botón **Run workflow** de la derecha: se abre un diálogo con tres campos

| Parámetro | Descripción |
|------|------|
| Contraseña VNC | La contraseña que introducirás al conectarte al escritorio: solo letras y números, hasta 8 caracteres (p. ej. `abc12345`). **Anótala** |
| Duración | Minutos que se mantendrá activo este escritorio en la nube. Por defecto 300 (5 horas), máximo 350 |
| Resolución | Resolución inicial del escritorio, por defecto 1920x1080; al abrir la página en el navegador se reajustará automáticamente al tamaño de la ventana |

4. Pulsa el botón verde **Run workflow** para confirmar: el escritorio en la nube empieza a arrancar

### Paso 3: Obtén la dirección de acceso

1. En la página de Actions, entra en la ejecución que acabas de iniciar (la de más arriba; el punto amarillo indica que está en curso)
2. Espera unos 3–5 minutos a que la máquina virtual instale el software y cree el túnel
3. Haz clic en el paso **启动服务并建立隧道**, despliega el registro y baja hasta encontrar una dirección como esta:

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copia la dirección y ábrela en el navegador (vale el navegador que trae el móvil)

### Paso 4: Conéctate al escritorio

1. En la página de noVNC que se abre, pulsa **Connect**
2. Introduce la contraseña VNC que configuraste en el paso 2
3. Ya ves el escritorio de Windows: a usarlo 🎉
4. En unos 10 segundos tras abrir la página, la resolución del escritorio se adaptará automáticamente a tu ventana del navegador; si redimensionas la ventana se reajusta sola (eligiendo entre las resoluciones que admite tu tarjeta gráfica)

> ⌨️ Para cambiar el método de entrada pulsa **Win + Space**: alterna entre Sogou Pinyin y el teclado inglés.

### Paso 5: Ciérralo al terminar

- Vuelve a la página de Actions, entra en esa ejecución y pulsa **Cancel run** arriba a la derecha: la máquina virtual se destruye y el túnel deja de funcionar
- Al superar la duración configurada termina automáticamente, así que no te preocupes por dejarlo corriendo

## ⚠️ Notas

- **La dirección cambia en cada ejecución**: la dirección anterior deja de funcionar en cuanto termina la ejecución previa; usa siempre la del registro de la última ejecución
- **Los datos no se guardan**: al destruirse la máquina virtual, los archivos, descargas y sesiones del escritorio se borran por completo; saca a tiempo los archivos importantes
- **Reglas de la contraseña**: solo letras y números, hasta 8 caracteres; si es más larga o lleva caracteres especiales puede fallar la conexión (error `Authentication failed`)
- **No pulses Re-run**: para abrir un escritorio nuevo pulsa **Run workflow**; Re-run ejecuta código antiguo
- **Conexión lenta/con cortes**: el túnel pasa por Cloudflare; la velocidad desde China continental depende de tu red, pero se puede usar
- **La página no abre**: primero confirma que la ejecución siga en curso (punto amarillo); si ya se canceló o terminó, la dirección ha caducado

## ❓ Preguntas frecuentes

| Síntoma | Causa / solución |
|------|-----------|
| `loopback connections are not enabled` | Bug de una versión antigua: vuelve a ejecutar con el código más reciente desde Run workflow |
| `Server is not configured properly` | Bug de una versión antigua: vuelve a ejecutar con el código más reciente desde Run workflow |
| `Authentication failed` | Contraseña VNC incorrecta, o la contraseña supera los 8 caracteres / contiene caracteres especiales |
| La página muestra 502 / 1033 | El túnel aún no está listo o se ha caído: espera unos minutos o vuelve a ejecutar |
| La resolución no cambia sola | Espera unos 10 segundos; confirma que la ventana del navegador haya cambiado de tamaño de verdad; algunas resoluciones no estándar no las admite la tarjeta gráfica y se elige automáticamente la más cercana |

## 🛠️ ¿Quieres modificarlo tú mismo?

Los archivos del workflow están en `.github/workflows/` (`windows-vnc.yml` para la edición estándar, `windows-vnc-rustdesk.yml` para la edición RustDesk): puedes editarlos directamente en la web de GitHub y los cambios surten efecto al confirmar el commit.
