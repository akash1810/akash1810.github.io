# profile-badge-app

A simple app inspired by the [Polymer starter project](https://www.polymer-project.org/docs/start/tutorial/intro.html)
and seeded from the [Yeoman Polymer Generator](https://github.com/yeoman/generator-polymer).

It displays a set of badges for a set of online profiles. The badges are provided from [font-awesome](http://fortawesome.github.io/Font-Awesome/).

The list of badges are provided from a json file, the location of which is specified in [app.js](scripts/app.js).

## Development
This project was seeded from the [Yeoman Polymer Generator](https://github.com/yeoman/generator-polymer).
There are a number of Grunt tasks available. Refer to the [Yeoman Polymer Generator](https://github.com/yeoman/generator-polymer)
for more information on these.

### sass
sass is required to compile the css.

[rvm](https://rvm.io/) is used in this project to manage the ruby environment, with the gemset managed by [bundler](http://bundler.io/).
Ensure rvm is installed then run:

```sh
bundle install
```

## Configuration
Configuration is controlled in [app.js](scripts/app.js) and there are two options available for configuration:

### appName
The text that appears in the header section.

### profileUrl
The location of a json file that contains the profile definitions.

This json file represents a list of objects with the following structure:

```javascript
  {
    "name": "[required] The name of the Platform",
    "url": "[required] The URL to the Platform profile",
    "faClass": "[optional] The font-awesome icon class to use if not the same as name"
  }
```
