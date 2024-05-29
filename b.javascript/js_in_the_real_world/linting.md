## Style guides

### [Airbnb Style Guide](https://github.com/airbnb/javascript)

### [Github Style Guide](https://standardjs.com/)

### [Google Style Guide](https://google.github.io/styleguide/jsguide.html)

# Linting
The style guides mentioned above are full of really helpful advice for formatting, organizing and composing your code. But there are a lot of rules - it can be difficult to internalize them all. **Linters** are tools that will scan your code with a set of style rules and will report any errors to you that they find. In some cases, they can even auto-fix the errors!

Linting in JavaScript refers to the process of analyzing your code for potential errors, stylistic issues, and other problems using a tool called a linter. A linter is a program that checks your source code for patterns that might indicate errors or violations of coding standards.

Linters help developers maintain consistent and error-free code by enforcing coding conventions and best practices. They can catch common programming mistakes, such as syntax errors, undefined variables, and potential bugs. Additionally, linters can enforce a specific coding style, ensuring that the codebase follows a consistent and readable format.

One popular JavaScript linter is ESLint, which is highly configurable and widely used in the JavaScript community. ESLint allows you to define your own linting rules or choose from existing rule sets to suit your project's requirements. It can be integrated into your development workflow through various tools and IDEs, providing real-time feedback to developers as they write code.

Linting is an essential part of modern software development, helping teams catch and fix issues early in the development process, leading to more maintainable and reliable code.

## ESLint

### How does it work?
ESLint is an open source, JavaScript linting utility originally created by Nicholas C. Zakas.

ESLint is a CLI tool which is wrapped around two other open source projects. One is Espree, which creates an Abstract Syntax Tree (AST) from JavaScript code. Based on this, AST ESLint uses another project called Estraverse which provides traversal functions for an AST. During the traversal, ESLint emits an event for each visited node where the node type is the Event name, e.g. *FunctionExpression* or *WithStatement*. ESLint rules are therefore just functions subscribing to node types it wants to check.

The AST is an abstract representation of your code structure. Every entry in the AST is a Node object, consisting of a ‘type’ property and a SourceLocation Object. The type property is a string representing the different Node variants in the AST. The SourceLocation Object consists of a start and end property. The type, start, and end line number provide us with information about the structure of our code. Generally, a JavaScript AST consists of Statements, Expressions and Declarations.

For traversing the AST, ESLint relies on the Estraverse project which traverses over the generated AST (from Espree). Estraverse provides a traverse functionality which executes a given statement. In this traverse function we can subscribe to specific types of nodes and complete our analysis.

### Quick Setup
[ESLint Getting Started](https://eslint.org/docs/latest/use/getting-started)

To use ESLint, you must have Node.js installed and built with SSL support. (If you are using an official Node.js distribution, SSL is always built in.)

You can install and configure ESLint using this command:

`npm init @eslint/config`

This configuration presents the option to choose airbnb-base style guide as the style rules base.

Note: npm init @eslint/config assumes you have a package.json file already. If you don’t, make sure to run npm init or yarn init beforehand.

The basic way to use this tool is to simply run the eslint command in your terminal with a specific file. Example:

`npx eslint ./src/index.js`

But the recommended next step is to install the linting plugin in your prefferred text editor. These plugins allow you to automatically lint your code as you are writing it, and will show the errors right in the editor, which makes resolving them much simpler.

**VSCode ESLint extension:** Integrates ESLint into VS Code. The extension uses the ESLint library installed in the opened workspace folder. If the folder doesn't provide one the extension looks for a global install version. If you haven't installed ESLint either locally or globally, do so by running `npm init @eslint/config` (this will install eslint locally and let you configure the installation.)

ESLint can be further modified to automatically fix errors every time a `.js` file is saved. To do this open up your settings.json file (Manage -->> Settings -->> Open Settings(JSON)).  For ESLint to fix errors when you save your `.js` file, you will need to write the following code in settings.json:

```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
},
"eslint.validate": ["javascript"]
```

With this code in your settings.json file, ESLint will now automatically correct errors and validate JavaScript on save.

# Formatting
## Prettier
Prettier is an opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules that take the maximum line length into account, wrapping code when necessary. Its primary purpose is to automatically format your code according to a set of predefined rules, ensuring consistency and a standardized code style across your project. This can be especially useful when working on projects with multiple developers, as it helps maintain a clean and readable codebase.

Key features of Prettier include:

1. **Automatic Code Formatting:** Prettier parses your JavaScript code and reprints it with its own rules, automatically adjusting indentation, line breaks, and other formatting details.

2. **Configurability:** While Prettier comes with default formatting rules, you can also configure it to match your team's or project's specific coding style by providing a configuration file (e.g., a `.prettierrc` file).

3. **Support for Various Languages:** While initially designed for JavaScript, Prettier has expanded its support to various languages, including TypeScript, HTML, CSS, and more.

4. **Command-Line Interface (CLI):** Prettier can be used from the command line, making it easy to integrate into your development workflow or build processes.

Here's a basic example of how to use Prettier:

1. **Install Prettier:**
   ```bash
   npm install --save-dev prettier
   ```

2. **Run Prettier:**
   ```bash
   npx prettier --write src/*.js
   ```
   This command will format all JavaScript files in the `src` directory.

3. **Integrate with Your Editor:** Many code editors have extensions or plugins that can automatically run Prettier on your code each time you save a file. This helps maintain consistent formatting as you work.

  **VSCode Prettier Plugin:** It’s still important to install Prettier locally in every project, so each project gets the correct Prettier version.

By using Prettier, you can focus on writing code without worrying too much about formatting details. It helps prevent debates over code style within a team and contributes to a more maintainable and collaborative codebase.

## Using ESLint and Prettier together
Using ESLint and Prettier together causes conflicts. **The recommended way of integrating Prettier with linters is to let Prettier do the formatting and configure the linter to not deal with formatting rules.**

In order to fix the conflict between ESLint and Prettier, follow the instructions to install [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier#installation). It turns off all ESLint rules that are unnecessary or might conflict with Prettier. Doing just this is enough to resolve the conflict and get them both working smoothly with one another.

Prettier can be further modified to automatically format the file every time it is saved. To do this open up your settings.json file (Manage -->> Settings -->> Open Settings(JSON)). For Prettier to format when you save your `.js` or `.css` files, you will need to write the following code in settings.json:

```json
"editor.defaultFormatter": "esbenp.prettier-vscode",
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
},
"[css]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```

```"editor.defaultFormatter": "esbenp.prettier-vscode"``` rule will also set Prettier as the default Formatter so that it doesn't conflict with ESLint.

---
### Knowledge Check

**Q1.** What is linting?

**A1.** Linting in JavaScript refers to the process of analyzing your code for potential errors, stylistic issues, and other problems using a tool called a linter. A linter is a program that checks your source code for patterns that might indicate errors or violations of coding standards.

**Q2.** Which problems can linting prevent?

**A2.** Linters help developers maintain consistent and error-free code by enforcing coding conventions and best practices. They can catch common programming mistakes, such as syntax errors, undefined variables, and potential bugs. Additionally, linters can enforce a specific coding style, ensuring that the codebase follows a consistent and readable format.

One popular JavaScript linter is ESLint, which is highly configurable and widely used in the JavaScript community. ESLint allows you to define your own linting rules or choose from existing rule sets to suit your project's requirements. It can be integrated into your development workflow through various tools and IDEs, providing real-time feedback to developers as they write code.

Linting is an essential part of modern software development, helping teams catch and fix issues early in the development process, leading to more maintainable and reliable code.

**Q3.** Why should you use Prettier?

**A3.** Prettier is an opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules that take the maximum line length into account, wrapping code when necessary. Its primary purpose is to automatically format your code according to a set of predefined rules, ensuring consistency and a standardized code style across your project. This can be especially useful when working on projects with multiple developers, as it helps maintain a clean and readable codebase.

Prettier parses your JavaScript code and reprints it with its own rules, automatically adjusting indentation, line breaks, and other formatting details.

While Prettier comes with default formatting rules, you can also configure it to match your team's or project's specific coding style by providing a configuration file (e.g., a `.prettierrc` file).

Many code editors have extensions or plugins that can automatically run Prettier on your code each time you save a file. This helps maintain consistent formatting as you work.

By using Prettier, you can focus on writing code without worrying too much about formatting details. It helps prevent debates over code style within a team and contributes to a more maintainable and collaborative codebase.

Using ESLint and Prettier together causes conflicts. **The recommended way of integrating Prettier with linters is to let Prettier do the formatting and configure the linter to not deal with formatting rules.**

In order to fix the conflict between ESLint and Prettier, follow the instructions to install [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier#installation). It turns off all ESLint rules that are unnecessary or might conflict with Prettier. Doing just this is enough to resolve the conflict and get them both working smoothly with one another.

Prettier can be further modified to automatically format the file every time it is saved. To do this open up your settings.json file (Manage -->> Settings -->> Open Settings(JSON)). For Prettier to format when you save your file, you will need to write the following code in settings.json:

```json
"editor.defaultFormatter": "esbenp.prettier-vscode",
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```

```"editor.defaultFormatter": "esbenp.prettier-vscode"``` rule will also set Prettier as the default Formatter so that it doesn't conflict with ESLint.

**Q4.** What is a template repository?

**A4.** On Github, we can create a template from an existing repository. Anyone with access to the template repository can create a new repository based on the template with the same directory structure, branches, and files.

To create a template repository, you must create a repository, then make the repository a template.

After you make your repository a template, anyone with access to the repository can generate a new repository with the same directory structure and files as your default branch. They can also choose to include all the other branches in your repository. Branches created from a template have unrelated histories, so you cannot create pull requests or merge between the branches.

Template repositories are often used for setting up standard project structures, license files, documentation templates, and other common project elements. 

