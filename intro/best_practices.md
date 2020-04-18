# Best Practices

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/LICENSE.md)

Starting to manage your projects with `git` can be overwhelming. Answering
simple questions such as "How often should I commit?" and "How should I organize
my repository?" can be difficult. This module seeks to provide
guidance on `git` best practices for those just starting to find their way.
A small but important caveat here: each development team/organization/research
group will mostly like use `git` differently so while the rules provided
here are generally considered good practice they will not apply in all
situations. So with that in mind, I hope this module helps to answer some of
your questions about organizing projects with `git`.

## Guidelines

- Repositories should have a short, memorable, and topical name. Avoid the use
of capital letters and special characters.

- Repositories should only contain source code or source-code-tangent
information. Do not use `git` for storing analysis results, figures, or sample
outputs. They are more appropriately stored on a cloud storage system.

- Repositories should contain a detailed `README.md` file which should include the following:
  - A detailed description of the project
  - Installation/setup instructions
  - Links to detailed documentation
  - At least one interest-provoking figure or example

- Repositories should be intuitively organized (e.g., tests should be located in
a `test` folder, source in a `src` folder). Follow the conventions provided by
your coding language for organizing your projects. When naming directories do
not use capital letters, spaces, and special characters.

- Commit after completing a specific task (hour or two of coding). If you
would describe your work with a commit message of "made various changes" then
that commit should be broken across multiple commits where each commit should
describe one and only one of the changes made.

- Commit messages should be short and to the point. Prefer specific descriptions
over general ones. To reduce boiler plate text such as "bug fix" prefer the use
of an emoji such as :bug:. A list of useful emojis and what they mean are
provided [here](https://jpvantassel.github.io/git-course/#/adv/emojis).

- Use branches when developing prospective features or implementing breaking
changes. Only merge these branches into `master` after the changes have been
accepted for production and due notice has been provided to users.
