# bdd-testcafe

E2E tests are a very important part of your projects, mainly to avoid regressions and bugs, especially on specific parts of your application which are not regularly tested.

Their purpose is to test your product, and not your code. This a very common mistake when writting e2e tests: testing the code, and the business logic of the app. In fact, these tests should be written by product owners, and not by developers. More important, theses business tests should be used as a source of documentation and specifications for the project.

Cucumber offers you this opportunity, with the possibility to write understandable tests with Gherkin.

TestCafe has been prefered over Selenium because of the setup simplicity, and the lot of possibilities it offers (remote tests, multi browsers, concurrency, ie...).

## Presentation
This library main goal is to allow you to launch e2e tests using cucumber and TestCafe. Tests are feature files written in Gherkin, and are executed by Cucumber. The browser is started and managed by Testcafe APIs.

## Setup
```
npm i bdd-testcafe --save-dependencies
```

## How to launch your BDD tests?
Then add this command to you package.json file:
```javascript
{
  "scripts": {
    ...
    "e2e": "./node_modules/.bin/cucumber-js ./test.feature --config ./bdd-config.json --require ./node_modules/bdd-testcafe/lib/support/**/*.js --require ./node_modules/bdd-testcafe/lib/step_definitions/**/*.js --format json:./reports/report.json"
  }
}
```

This command starts cucumber-js, with the following arguments:
* *./test.feature*: Path to you feature file(s)

These files are written using Gherkin, and look as below:
```
@sample
Feature: Authentication

  <h2>Test d'authentification</h2>
  <p>L'utilisateur se connecte à l'application et a accès à ses fonctionnalités</p>

  Scenario Outline: User login

    When Je clique sur le bouton Icône "Connexion"
    Then Je devrais voir apparaître la modale "Authentification"

    When Je saisis la valeur "<login>" dans le champ de saisie "Login"
    And Je saisis la valeur "<password>" dans le champ de saisie "Mot de passe"
    And Je clique sur le bouton "Connexion"
    Then Je devrais naviguer sur la page "Liste des marchés"

    Examples:
    | login | password |
    | spongeBob | 1234 |
```

* *--config ./bdd-config.json*: library config file path (default is *./bdd-config.json*).

```javascript
{
    "tests": {
      "proxy": "",
      "browsers": "firefox",
      "screenshotsPath": "reports/screenshots/",
      "concurrency": 1,
      "testFile": "./node_modules/bdd-testcafe/lib/test.js"
    }
}
```  

* *--require ./node_modules/bdd-testcafe/lib/support/**/*.js*: path to the lib hooks which are used to handle the launch of TestCafe.

* *--require ./node_modules/bdd-testcafe/lib/step_definitions/**/*.js*: path to the spec definitions. These are the library spec definitions, but you couls also add your own spec definitions files.

* *--format json:./reports/report.json*: Type and path of the report generated by the command.

## How to generate an HTML report?
Add the following command to you package.json file:
```javascript
"report-e2e:demo": "node ./node_modules/bdd-testcafe/lib/report/report.js --jsonFile ./reports/report.json --output ./reports/report.html"
```

* *--jsonFile ./reports/report.json*: path to the report generated by the tests.
* *--output ./reports/report.html*: path to the HTML report

## Available Spec Definitions
TODO