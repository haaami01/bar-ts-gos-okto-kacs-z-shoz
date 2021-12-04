Wenn Deine Website ein unabhängiges Projekt ist, kannst Du ein neues Repository erstellen, um den Quellcode Deiner Website zu speichern. If your site is associated with an existing project, you can add the source code {% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.22" or currentVersion == "github-ae@latest" %}to that project's repository, in a `/docs` folder on the default branch or on a different branch.{% else %}for your site to a `gh-pages` branch or a `docs` folder on the `master` branch in that project's repository.{% endif %} For example, if you're creating a site to publish documentation for a project that's already on {% data variables.product.product_name %}, you may want to store the source code for the site in the same repository as the project.

Wenn Du eine Website in einem vorhandenen Repository erstellen möchtest, springe zum Abschnitt „[Erstellen Deiner Website](#creating-your-site)".