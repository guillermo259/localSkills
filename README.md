<!-- Improved compatibility of back to top link -->
<a id="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![License][license-shield]][license-url]

<br />
<div align="center">
  <h3 align="center">localSkills</h3>

  <p align="center">
    Una colección de Skills que uso día a día con agentes de IA para automatizar tareas repetitivas y asegurar que no me salte ningún paso importante.
    <br />
    <br />
    <a href="https://github.com/guillermo259/localSkills/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/guillermo259/localSkills/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
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
    <li><a href="#available-skills">Available Skills</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

**localSkills** es un conjunto de instrucciones en Markdown que le indican a un agente de IA exactamente cómo ejecutar tareas específicas paso a paso. Cada skill cubre un área de trabajo concreta: GitHub, SEO, documentación, etc.

El proyecto nace de la necesidad de no tener que recordar ni repetir los mismos flujos de trabajo manualmente. Le pasas la skill al agente, y él se encarga de seguir el proceso completo sin saltarse nada.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

[![Markdown][markdown-shield]][markdown-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

### Prerequisites

- Un agente de IA compatible con instrucciones en Markdown (Kiro, ChatGPT, Claude, Cursor, etc.)
- No se requiere instalación de software adicional

### Installation

1. Clona o descarga este repositorio en tu máquina local:
   ```sh
   git clone https://github.com/guillermo259/localSkills.git
   ```
2. Copia la carpeta `skills/` (o el repositorio completo) dentro de tu proyecto de trabajo.
3. Cuando necesites usar una skill, referencia el archivo directamente en tu conversación con el agente.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

Para usar una skill, simplemente indícale al agente que la revise y luego dile qué quieres hacer:

```
Revisa /SEO/seo-auditor.md y analiza mi landing actual para ver qué errores tengo.
```

```
Revisa /GITHUB/commit-format.md y genera el commit para los cambios actuales.
```

El agente leerá las instrucciones de la skill y las aplicará sobre tu proyecto de forma consistente.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Available Skills

### 🐙 GITHUB
| Skill | Descripción |
|-------|-------------|
| `commit-format.md` | Genera commits con un formato consistente y descriptivo |
| `readme-generator.md` | Genera un README profesional para proyectos de GitHub |
| `release-version.md` | Gestiona el proceso completo de lanzamiento de una nueva versión |
| `security-precommit.md` | Revisa el código antes de un commit en busca de vulnerabilidades de seguridad |

### 🔍 SEO
| Skill | Descripción |
|-------|-------------|
| `seo-auditor.md` | Audita una página o landing para identificar errores y oportunidades de SEO |

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Roadmap

- [x] Skills de GITHUB
  - [x] Formato de commits
  - [x] Generador de README
  - [x] Release y versionado
  - [x] Pre-commit de seguridad
- [x] Skills de SEO
  - [x] Auditor SEO
- [ ] Skills de Documentación
  - [ ] Generador de documentación técnica
  - [ ] Generador de changelogs
- [ ] Otras skills planeadas
  - [ ] Skills adicionales en desarrollo

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Las contribuciones son bienvenidas. Si quieres agregar o mejorar una skill:

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NuevaSkill`)
3. Commit your Changes (`git commit -m 'Add: nueva skill para X'`)
4. Push to the Branch (`git push origin feature/NuevaSkill`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distribuido bajo la licencia **Creative Commons Attribution 4.0 International (CC BY 4.0)**.

Puedes usar, modificar y redistribuir estas skills libremente, siempre y cuando hagas mención de que te basaste en el trabajo original de este repositorio.

Ver [LICENSE](LICENSE) para más información.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

Guillermo Hernandez - [@guillermo259](https://github.com/guillermo259)

Project Link: [https://github.com/guillermo259/localSkills](https://github.com/guillermo259/localSkills)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [Choose an Open Source License](https://choosealicense.com)
* [Creative Commons Licenses](https://creativecommons.org/licenses/)
* [Img Shields](https://shields.io)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/guillermo259/localSkills.svg?style=for-the-badge
[contributors-url]: https://github.com/guillermo259/localSkills/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/guillermo259/localSkills.svg?style=for-the-badge
[forks-url]: https://github.com/guillermo259/localSkills/network/members
[stars-shield]: https://img.shields.io/github/stars/guillermo259/localSkills.svg?style=for-the-badge
[stars-url]: https://github.com/guillermo259/localSkills/stargazers
[issues-shield]: https://img.shields.io/github/issues/guillermo259/localSkills.svg?style=for-the-badge
[issues-url]: https://github.com/guillermo259/localSkills/issues
[license-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg?style=for-the-badge
[license-url]: https://creativecommons.org/licenses/by/4.0/
[markdown-shield]: https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white
[markdown-url]: https://www.markdownguide.org

---

## Changelog

### [1.0.0] - 2026-07-28

#### Agregado
- Skill `GITHUB/commit-format.md` — generación de commits con formato consistente
- Skill `GITHUB/readme-generator.md` — generador de README profesionales para GitHub
- Skill `GITHUB/release-version.md` — proceso completo de release y versionado
- Skill `GITHUB/security-precommit.md` — revisión de seguridad antes de hacer commit
- Skill `SEO/seo-auditor.md` — auditoría SEO de páginas y landings
- `README.md` inicial del proyecto con estructura, uso y roadmap
- `.gitignore` con patrones para OS, editores, secretos y dependencias
