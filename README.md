# ESLint Web Site

[![Join the chat at https://gitter.im/smocean/eslint-zh](https://badges.gitter.im/smocean/eslint-zh.svg)](https://gitter.im/smocean/eslint-zh?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This contains the code running on eslint.org.

## Pull Requests

Please note that all HTML documentation is split between this repository and the main [ESLint repository](https://github.com/eslint/eslint). Documentation for rules and APIs is located in the core repository, the rest is located in this repository. You can easily determine if original documentation file is native to website repository by checking for `<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->` comment just below the header of the markdown file. If that header is present, this file is located in the core ESLint repository and any pull requests should be send there. Otherwise, file is native to this site repository and can be fixed by creating a pull request in this repository.

## How to add your company/project logo to the site

* Create a fork of this repository
* Clone it locally
* Create a new branch
* Add your logo image to /img/logos/ directory. Logo should be at least 150px of height. Name your logo with your company/project name.
* Update /_data/logos.yml file and add an entry for your company with the name, url and src (should point to the logo you just added).
* Commit your changes to your fork and create a pull request into the main repository.

## License

MIT
