# Instalación

En este tutorial utilizaremos Magic junto con la tecnología sky130, que es la que podemos fabricar. Tenemos que realizar 2 instalaciones:

* La herramienta [Magic](https://github.com/RTimothyEdwards/magic) 
* La tecnología sky130

## Instalación de Magic

La manera más directa de instalar mágic, usando la última versión, es utilizando el ejecutabe **appimage** que se encuentra en la zona de las Releases: [https://github.com/RTimothyEdwards/magic/releases](https://github.com/RTimothyEdwards/magic/releases)

La que usamos para este tutorial es la versión **8.3.681**

Descargamos el ejecutable appimage correspondiente, que en nuestro caso es: [Magic-8.3.681.20260807.4432d7ec-x86_64-EL10.AppImage](https://github.com/RTimothyEdwards/magic/releases/download/8.3.681/Magic-8.3.681.20260807.4432d7ec-x86_64-EL10.AppImage)


Lo renombramos a `magic` y lo copiamos en un directorio accesible desde el path. Yo voy a instalarlo en `~/.local/bin`

Para comprobar que arranca correctamente abrimos un terminal y escribimos `magic`:

```bash
obijuan@JANEL:~$ magic
-- # Starting Magic
```

Esto es lo que nos aparece:

![Imagen instalacion 1](images/install-magic-01.png)

De momento vamos a **Cerrar** la aplicación, pinchando en **File/Quit**

![Imagen instalacion 2](images/install-magic-02.png)

¡Ya tenemos Magic funcionando!

## Instalando el gestor ciel
