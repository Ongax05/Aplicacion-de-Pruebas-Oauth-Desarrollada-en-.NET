# Configuración de Proyecto Web con Autenticación Individual Oauth y MySQL

Este tutorial te guiará a través de la configuración de un proyecto web con autenticación individual y MySQL en ASP.NET Core. También se incluye información sobre cómo habilitar la autenticación de Google en el proyecto. Este tutorial se basa en el uso de `dotnet` y herramientas relacionadas.

# Tabla de Contenidos

- [Configuración de Proyecto Web con Autenticación Individual y MySQL](#configuración-de-proyecto-web-con-autenticación-individual-y-mysql)
  - [Crear un Proyecto Web con Autenticación Individual](#crear-un-proyecto-web-con-autenticación-individual)
  - [Configurar MySQL](#configurar-mysql)
  - [Instalar Microsoft.VisualStudio.Web.CodeGeneration.Design](#instalar-microsoftvisualstudiowebcodegenerationdesign)
  - [Generar Vistas y Controladores](#generar-vistas-y-controladores)
  - [Configurar Autenticación de Google](#configurar-autenticación-de-google)
  - [Configuración de Página HTTPS](#configuración-de-página-https)
  
> Hecho por "Jhosep Deangelo Pulido Plata"

## Crear un Proyecto Web con Autenticación Individual

Para comenzar, crea un proyecto web con autenticación individual utilizando el siguiente comando `dotnet`:

```bash
dotnet new webapp --auth individual -uld -o nombre
```

Asegúrate de reemplazar `nombre` con el nombre deseado para tu proyecto.

## Configurar MySQL

Si deseas utilizar MySQL como base de datos, instala el paquete `Pomelo.EntityFrameworkCore.MySql`:

```bash
dotnet add package Pomelo.EntityFrameworkCore.MySql
```
**Modificaciones de Migraciones**

Es importante destacar que la plantilla de autenticación por defecto utiliza `DateTimeOffset` y `nvarchar(max)` en las migraciones. Si prefieres utilizar `DateTime` en lugar de `DateTimeOffset` y `LONGTEXT` en lugar de `nvarchar(max)`, tendrás que realizar estas modificaciones manualmente en las migraciones generadas.

## Instalar Microsoft.VisualStudio.Web.CodeGeneration.Design

Para generar vistas y controladores automáticamente, instala la herramienta `dotnet-aspnet-codegenerator` con el siguiente comando:

```bash
dotnet tool install -g dotnet-aspnet-codegenerator
```

## Instalar Microsoft.VisualStudio.Web.CodeGeneration.Design

Para generar vistas y controladores automáticamente, instala la herramienta `dotnet-aspnet-codegenerator` con el siguiente comando:

```bash
dotnet tool install -g dotnet-aspnet-codegenerator
```

## Generar Vistas y Controladores

Para generar vistas y controladores basados en tu contexto de aplicación, ejecuta el siguiente comando:

```bash
dotnet aspnet-codegenerator identity -dc {Your_Application_NameSpace}.ApplicationDbContext
```
Reemplaza ``{Your_Application_NameSpace}`` con el espacio de nombres de tu aplicación.

## Configurar Autenticación de Google

Si deseas habilitar la autenticación de Google en tu proyecto, primero instala el paquete `Microsoft.AspNetCore.Authentication.Google` con el siguiente comando:

```bash
dotnet add package Microsoft.AspNetCore.Authentication.Google
```

**Configurar Autenticación de Google**

1. Ve a [https://console.cloud.google.com/apis](https://console.cloud.google.com/apis) para crear un servicio y obtener las credenciales `ClientId` y `ClientSecret`.

2. En tu programa principal (normalmente `Program.cs`), configura la autenticación de Google utilizando `AddAuthentication` y `AddGoogle`, junto con una lambda en `AddGoogle` para configurar `ClientId` y `ClientSecret`.

## Configuración de Página HTTPS

Para utilizar la autenticación, necesitas una página HTTPS. Puedes configurar esto en el archivo `Properties/launchSettings.json` de tu proyecto.

Esto debería ayudarte a configurar un proyecto web con autenticación individual y MySQL, además de habilitar la autenticación de Google. Asegúrate de seguir las buenas prácticas de seguridad al implementar autenticación en tu aplicación. ¡Buena suerte con tu proyecto!

# Notas

1. Este proyecto también cuenta con autorización a través de Facebook, y los pasos para configurarlo son muy similares a los de Google. Te invitamos a consultar la documentación oficial de Facebook en [https://developers.facebook.com/docs/](https://developers.facebook.com/docs/) para obtener más información.
