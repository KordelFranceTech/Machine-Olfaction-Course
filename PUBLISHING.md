# Preparing the Markdown course for private GitHub Pages

This workspace contains a complete learner-facing directory, `docs/`. New deliverables are Markdown, including frontmatter, navigation, text diagrams, equations, and executable code blocks. No generated site assets or deployment configuration are included in the delivered source. A temporary local build was used for validation; no remote repository or hosting registration was created.

## Publish only the course directory

Use a fresh publishing repository containing only the `docs/` directory. Copy that directory deliberately; do not upload the entire enclosing workspace. The course's relative links remain within `docs/`, and its entry point is [docs/index.md](docs/index.md).

With GitHub Pages' standard branch build, select the appropriate branch and `/docs` as the publishing folder. GitHub recognizes `index.md` as an entry file and uses Jekyll for this build mode. The exact repository owner and branch can be chosen when hosting is configured. [GitHub: creating a Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

## Establish website access before enabling publication

A private repository alone does not make its Pages site private. GitHub documents private Pages access for organization-owned project sites on GitHub Enterprise Cloud, subject to organization policy. Private sites are accessible to people with repository read access; organization sites have different access-control limitations. Use an eligible project repository and explicitly select private visibility. If the account does not support private Pages, keep the repository as the reading surface or use another authenticated hosting arrangement. [GitHub: privately published sites](https://docs.github.com/en/enterprise-cloud@latest/pages/getting-started-with-github-pages/about-privately-published-github-pages-sites)

After deployment, test access both while signed in as an intended reader and in a signed-out session. Confirm that unauthorized access is denied. An obscure URL, a search-engine exclusion, or a private source repository is not a substitute for website authentication.

## Markdown-only compatibility

Every course page has frontmatter specifying `layout: default` and a title. GitHub Pages' current defaults include the Primer theme and the relative-links plugin. The plugin converts links to Markdown files into their rendered destinations, allowing the same source to be read in the repository. Equations are plain text, so no MathJax configuration is required; tree and circuit diagrams use code blocks, so no Mermaid plugin is required. [Pages configuration source](https://github.com/github/pages-gem/blob/master/lib/github-pages/configuration.rb), [default plugins](https://github.com/github/pages-gem/blob/master/lib/github-pages/plugins.rb), [relative-links documentation](https://github.com/benbalter/jekyll-relative-links)

Do not add a `.nojekyll` file to this Markdown source workflow; it would disable the conversion relied on here. A different static generator can also work, but its build and link handling need separate configuration and testing.

No YAML, HTML, JavaScript, CSS, JSON, or executable script files are required among the delivered source files for this standard path. Site configuration can be added later if a custom theme or navigation system is desired. Keep any such changes in the publishing repository and recheck the build.

## Navigation maintenance

The global menu links Home, Start, Modules, Labs, Projects, Library, and Site map. Each lesson identifies its section and position; previous/next links follow the numbered module and lab sequences. Project lessons form a separate guided route. The [site map](docs/navigation.md) lists every learner page with subject keywords.

Keep links relative to the current Markdown file and retain the `.md` extension in source. The relative-links plugin rewrites those links during the build, including nested paths and configured site prefixes. Explicit `section-...` anchors make contents links stable across rendering conventions. Collapsible contents use native `<details>` markup with `markdown="1"` inside the Markdown files. There is no required client-side script.

When adding or renaming a page, update its section hub, the site map, breadcrumbs, and adjacent previous/next links. When changing a heading, update its explicit anchor and contents link together. Repeated navigation is intentionally self-contained in each Markdown page; moving it into a theme include requires a new link-conversion check.

## Release verification

Before enabling hosting, inspect the staged file list and confirm it contains only the intended course files. Review the content boundaries in [EDITORIAL.md](EDITORIAL.md). Confirm the material's reuse terms and choose a license for original course content only if desired; no license has been assigned automatically.

After the first build, check the home page, a deeply nested module, a lab code block, a bibliography link, and a return-to-home link. Verify the rendered destinations on the actual private-site URL, which may use a dedicated subdomain. Test at narrow browser widths and with enlarged text. A custom build or domain can affect path behavior.

Local checks are recorded in [VALIDATION.md](VALIDATION.md). They do not establish a hosted build or access-control result. No publication or account configuration was performed while preparing the curriculum.

Hosting documentation checked: **22 November 2026**. Recheck current plan and organization requirements when publishing.
