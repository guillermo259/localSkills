---
inclusion: manual
version: "1.0.0"
---

# README Generator — Instrucciones del Agente

## Propósito

Cuando el usuario pida generar un README profesional para su proyecto de GitHub, sigue este flujo exacto: primero reúne la información necesaria haciendo preguntas, luego produce el README completo en Markdown usando la plantilla base definida más abajo.

---

## Flujo de trabajo

### Paso 1 — Recopilar información

Antes de escribir una sola línea de Markdown, haz al usuario **todas las preguntas siguientes en un solo mensaje**, agrupadas de forma clara y conversacional. Pídele que responda de una sola vez.

```
Para generar tu README necesito algunos datos. Responde lo que puedas y omite lo que no aplique:

**Identidad del proyecto**
1. ¿Cuál es el nombre del proyecto?
2. ¿Una descripción corta (1-2 líneas)?
3. ¿Qué problema resuelve o por qué existe?
4. ¿Tienes logo, screenshot o demo disponibles? (URLs o rutas de imagen)

**Tecnologías**
5. ¿Qué lenguajes, frameworks y herramientas principales usa el proyecto? (p. ej. React, Node.js, PostgreSQL)

**Instalación y uso**
6. ¿Cuáles son los prerequisitos (versiones de Node, Python, herramientas, etc.)?
7. ¿Cuáles son los pasos de instalación, en orden?
8. ¿Necesita alguna API key o variable de entorno? ¿Cómo se configura?
9. ¿Tienes un ejemplo de uso o snippet de código que muestre cómo se usa?

**Roadmap y licencia**
10. ¿Qué funcionalidades ya están listas? ¿Cuáles están planeadas?
11. ¿Qué tipo de licencia usa el proyecto? (MIT, Apache 2.0, GPL, etc.)

**Contacto y repositorio**
12. Tu nombre completo o alias
13. Tu usuario de Twitter/X (opcional)
14. Tu email de contacto
15. Tu URL de perfil de LinkedIn (opcional)
16. La URL completa del repositorio en GitHub (https://github.com/usuario/repo)
```

### Paso 2 — Generar el README

Una vez que el usuario haya respondido, produce el README completo en Markdown siguiendo estas reglas:

- **Reemplaza todo** el contenido de ejemplo de la plantilla con la información real proporcionada.
- **No dejes ningún placeholder** (sin `your_username`, `example.com`, `email@example.com`, etc.).
- Construye los badges de shields.io usando la URL real del repositorio del usuario.
- Si el usuario no proporcionó logo o screenshot, **elimina** esas líneas del Markdown (no pongas rutas de ejemplo).
- Si el usuario no tiene Twitter/X o LinkedIn, **elimina** esos campos del contacto y del badge.
- Adapta o elimina las secciones que no apliquen (por ejemplo, si no hay API key, omite ese paso en Installation).
- El Roadmap debe reflejar exactamente lo que el usuario indicó: marca con `[x]` lo ya hecho y con `[ ]` lo pendiente.
- Usa los badges de tecnología correctos de shields.io para cada tecnología mencionada. Si no existe un badge estándar, créalo con el formato genérico: `https://img.shields.io/badge/<nombre>-<color>?style=for-the-badge&logo=<logo-slug>&logoColor=white`
- Entrega el resultado como un único bloque de código Markdown listo para copiar y pegar.

---

## Plantilla base

Usa esta plantilla como estructura. No alteres el orden de las secciones salvo para eliminar las que no apliquen.

````markdown
<!-- Improved compatibility of back to top link -->
<a id="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![License][license-shield]][license-url]
<!-- Incluir solo si el usuario proporcionó LinkedIn -->
[![LinkedIn][linkedin-shield]][linkedin-url]

<!-- PROJECT LOGO — incluir solo si hay logo disponible -->
<br />
<div align="center">
  <a href="REPO_URL">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">PROJECT_NAME</h3>

  <p align="center">
    SHORT_DESCRIPTION
    <br />
    <a href="REPO_URL"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <!-- Incluir View Demo solo si hay demo -->
    <a href="DEMO_URL">View Demo</a>
    &middot;
    <a href="REPO_URL/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="REPO_URL/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a>
      <ul><li><a href="#built-with">Built With</a></li></ul>
    </li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

<!-- Screenshot — incluir solo si hay screenshot disponible -->
[![Product Screenshot][product-screenshot]](DEMO_URL)

WHY_THE_PROJECT_EXISTS

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

<!-- Lista de badges de tecnologías reales del proyecto -->

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

### Prerequisites

<!-- Prerequisitos reales del proyecto -->

### Installation

<!-- Pasos de instalación reales, numerados -->

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

<!-- Ejemplo de uso real con código si aplica -->

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Roadmap

<!-- Items reales del roadmap con [x] / [ ] -->

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distributed under the LICENSE_TYPE License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

YOUR_NAME - [@twitter_handle](https://twitter.com/twitter_handle) - YOUR_EMAIL

Project Link: [REPO_URL](REPO_URL)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [Choose an Open Source License](https://choosealicense.com)
* [Img Shields](https://shields.io)
* [GitHub Pages](https://pages.github.com)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/GITHUB_USER/REPO_NAME.svg?style=for-the-badge
[contributors-url]: https://github.com/GITHUB_USER/REPO_NAME/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/GITHUB_USER/REPO_NAME.svg?style=for-the-badge
[forks-url]: https://github.com/GITHUB_USER/REPO_NAME/network/members
[stars-shield]: https://img.shields.io/github/stars/GITHUB_USER/REPO_NAME.svg?style=for-the-badge
[stars-url]: https://github.com/GITHUB_USER/REPO_NAME/stargazers
[issues-shield]: https://img.shields.io/github/issues/GITHUB_USER/REPO_NAME.svg?style=for-the-badge
[issues-url]: https://github.com/GITHUB_USER/REPO_NAME/issues
[license-shield]: https://img.shields.io/github/license/GITHUB_USER/REPO_NAME.svg?style=for-the-badge
[license-url]: https://github.com/GITHUB_USER/REPO_NAME/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/LINKEDIN_USER
[product-screenshot]: images/screenshot.png
````

---

## Reglas de calidad

- Nunca entregues el README con placeholders sin reemplazar.
- Si falta información crítica (nombre del repo, descripción), pídela antes de generar.
- Si el usuario da información parcial, genera el README con lo disponible y señala al final qué secciones quedaron incompletas y qué datos adicionales podrían mejorarlas.
- El output final debe ser un bloque de código Markdown único, completo y listo para usar.
