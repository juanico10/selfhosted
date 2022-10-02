## CodiMD es un editor de código abierto que ofrece colaboración en tiempo real, además de ser compatible con Markdown.

##Introducción

Una poderosa herramienta que te permite colaborar con tu equipo de desarrollo en tiempo real, y lo mejor, usando Markdown para editar documentos.

CodiMD se creó y se basó en el código fuente de HackMD.

Con esta herramienta, puede alojar y controlar fácilmente el contenido de su proyecto.

El soporte para Markdown en CodiMD es excelente, incluso es compatible con la sintaxis de CommonMark.

Algunos plugins interesantes de la herramienta:

    MathJax - Utilizando para representar fórmulas matemáticas.
    Mermaid & Graphviz – Diagramación de UML.
    Vega-lite - Para aquellos que necesitan ver datos.
    Emojis - Para poner un poco más de expresión en sus documentos.

El sitio web oficial de CodiMD está en [Github](https://github.com/hackmdio/codimd)

# Instalación

## Requisitos

* [Traefik en funcionamiento](../traefik).
* Un subdominio de su elección, este ejemplo utiliza `codimd`.
  * Debería poder crear un subdominio con su proveedor de DNS, utilice un `A record` o `CNAME` con la misma dirección IP que su dominio raíz.

## Configuración

Reemplace las variables de entorno en `.env` con las suyas propias, luego ejecute :

```bash
sudo docker-compose up -d
```

Ahora debería ser capaz de acceder a la instrucción de configuración de codimd, es bastante straigthforward y no se requiere nada. 

# Actualización

La imagen se actualiza automáticamente con [watchtower](../watchtower) gracias a la siguiente etiqueta :

```yaml
  # Watchtower Update
  - "com.centurylinklabs.watchtower.enable=true"
```
