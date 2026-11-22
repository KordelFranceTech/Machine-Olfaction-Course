# Preparing the Markdown course for private GitHub Pages

This workspace contains a complete learner-facing directory, `docs/`. The curriculum is Markdown, including frontmatter, navigation, text diagrams, equations, and executable code blocks. Four small theme support files enable the requested appearance. Generated website output stays outside the source directory. Temporary local builds were used for validation; this update did not create a remote repository or hosting registration.

## Publish only the course directory

Use a fresh publishing repository containing only the `docs/` directory. Copy that directory deliberately; do not upload the entire enclosing workspace. The course's relative links remain within `docs/`, and its entry point is [docs/index.md](docs/index.md).

With GitHub Pages' standard branch build, select the appropriate branch and `/docs` as the publishing folder. GitHub recognizes `index.md` as an entry file and uses Jekyll for this build mode. The exact repository owner and branch can be chosen when hosting is configured. [GitHub: creating a Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

## Establish website access before enabling publication

A private repository alone does not make its Pages site private. GitHub documents private Pages access for organization-owned project sites on GitHub Enterprise Cloud, subject to organization policy. Private sites are accessible to people with repository read access; organization sites have different access-control limitations. Use an eligible project repository and explicitly select private visibility. If the account does not support private Pages, keep the repository as the reading surface or use another authenticated hosting arrangement. [GitHub: privately published sites](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/about-privately-published-github-pages-sites)

After deployment, test access both while signed in as an intended reader and in a signed-out session. Confirm that unauthorized access is denied. An obscure URL, a search-engine exclusion, or a private source repository is not a substitute for website authentication.

## Markdown content and the Minima theme

Every course page has frontmatter specifying `layout: default` and a title. The active theme is **Minima**, customized with a black background, Avenir with system-font fallbacks, gray body text, white headings, teal links, orange hover/focus states, and dark code blocks. No font files or external font service are required. Avenir is used when available on the reader's device.

The four theme support files are:

| File | Purpose |
| --- | --- |
| [docs/_config.yml](docs/_config.yml) | Activates Minima, Kramdown/Rouge, relative links, and the section menu |
| [docs/assets/main.scss](docs/assets/main.scss) | Imports Minima and applies the dark styling, responsive layout, and syntax palette |
| [docs/_includes/header.html](docs/_includes/header.html) | Adds a native keyboard-operated section menu and skip link |
| [docs/_includes/footer.html](docs/_includes/footer.html) | Adds a compact footer below the content |

Keep these files alongside the Markdown when copying `docs/` to a publishing repository. Jekyll expects the exact filename `_config.yml`. The theme's default layout loads `assets/main.css`, compiled from `assets/main.scss`. There is no client-side JavaScript dependency for navigation. [GitHub: adding and customizing a Jekyll theme](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)

The teal is slightly brighter than the supplied base color to improve text contrast. Links are underlined, the menu has visible keyboard focus, and the footer stays in document flow so that it cannot cover lesson content. Tables and code blocks scroll within their own regions on narrow screens.

The relative-links plugin converts Markdown destinations into rendered URLs. Equations use plain text and diagrams use code blocks, so MathJax and Mermaid plugins are not required. Do not add `.nojekyll`: this source workflow relies on Jekyll conversion. [Relative-links documentation](https://github.com/benbalter/jekyll-relative-links)

The configuration deliberately omits a fixed `url` and `baseurl`, allowing the standard GitHub Pages build to supply its publishing address. If a custom build is used, set `url` to the site's origin and `baseurl` to its path prefix without a trailing slash, or an empty string at the domain root. Use the curriculum's own destination rather than an unrelated documentation site's address. Both URL arrangements were tested locally; check the actual deployed address before sharing.

## Navigation maintenance

The global menu links Home, Start, Modules, Labs, Projects, Library, and Site map. Each lesson identifies its section and position; previous/next links follow the numbered module and lab sequences. Project lessons form a separate guided route. The [site map](docs/navigation.md) lists every learner page with subject keywords.

Keep links relative to the current Markdown file and retain the `.md` extension in source. The relative-links plugin rewrites those links during the build, including nested paths and configured site prefixes. Explicit `section-...` anchors make contents links stable across rendering conventions. Collapsible contents use native `<details>` markup with `markdown="1"` inside the Markdown files. There is no required client-side script.

When adding or renaming a page, update its section hub, the site map, breadcrumbs, and adjacent previous/next links. If a main section changes, also update the `navigation` entries in `_config.yml`; these drive the header menu. When changing a heading, update its explicit anchor and contents link together. The Markdown navigation remains self-contained for reading on GitHub. The theme menu is generated separately from configured rendered URLs using Jekyll's `relative_url` filter; keep its destinations aligned with the Markdown hubs.

## Release verification

Before enabling hosting, inspect the staged file list and confirm it contains only the intended course files. Review the content boundaries in [EDITORIAL.md](EDITORIAL.md). Confirm the material's reuse terms and choose a license for original course content only if desired; no license has been assigned automatically.

After the first build, check the home page, a deeply nested module, a lab code block, a bibliography link, and a return-to-home link. Verify the rendered destinations on the actual private-site URL, which may use a dedicated subdomain. Test at narrow browser widths and with enlarged text. A custom build or domain can affect path behavior.

Local checks are recorded in [VALIDATION.md](VALIDATION.md). They do not establish a hosted build or access-control result. No publication or account configuration was performed while preparing the curriculum.

Hosting documentation checked: **22 November 2026**. Recheck current plan and organization requirements when publishing.
