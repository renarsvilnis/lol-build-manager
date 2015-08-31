## League of Legends Build Manager

Parent repository of the League of Legends Build Manager project for the [The Riot Games API Challenge 2.0](https://developer.riotgames.com/discussion/announcements/show/2lxEyIcE) contest entry.

**Category:** Item Sets

### Team
```
Renārs Vilnis
Role: Programming, Project leader
Country: Latvia
City: Bergi
LOL Summoner: citrons
LOL Region: eune
```
```    
Anete Jakobsone
Role: Design
Country: Latvia
City: Bergi
LOL Summoner: GorgeousCupcake
LOL Region: eune
```

### Idea
Idea is to help players get better at League of Legends by helping them learn new champions quicker by using the capabilities of League of Legends item-sets. We all have a time when we lookup a build in mobafire, probuilds, solomid etc.., it is easy to remember the spell order, but when it comes to champion build we usually end up alt-tabbing during the game. We feel like it could be done better and created an application that helps aid players get their desired champion builds into the game.

### Under the hood
We ❤ JavaScript - the ideology was to write isomorphic code, which we achieved with help of [node package manager](https://www.npmjs.com/) and code seperation into reusable modules. More about that in [Structure](#structure).

For now we have created a Chrome extension that checks a tab if it is supported by the Build Manager, if is then it displays an icon in the action bar of Chrome that allows with a single click to import the guide into the native application and thus into the game. It is achieved by registering a custom protocol in the operating system, similar like 'mailto:' to redirects you to your email client. Because of the code reusability and modularisation it is trivial to create additional browser extensions.

Now to the main show - the native app. It created using [Electron framework](https://github.com/atom/electron) which allows to create cross platform desktop applications using web technologies and [io.js](https://iojs.org/) (*node.js fork*). The goal is to add support for Windows and OSX, although for now we only support OSX, but the logic inside the code already handles Windows enviroment.

The native application allows its user to manage builds and guides, either externaly created or imported by the application. Even if the user hasn't installed any browser extension, he is able to manualy add a guide from a url within the application. The native application **doesn't** deal with the management of individual builds - changing items, build blocks. We just leave the League of Legends client to do so.

To make the application work offline - with limited functionality (*no importing*), we cache item and champion information and images through League of Legends static data api, this makes for a quicker and better user expierence. On each application launch it checks if there is a new League of Legends game version and automatically does any update processes related to cached items to keep the user up-to-date.

*Please visit [challenges.md](challenges.md) for a detailed description about the problems face during the development process and how we dealth with them.*

### Technology stack
- Languages: JavaScript (ES6), [SASS](http://sass-lang.com/) + [BEM](https://en.bem.info/method/naming-convention/), [io.js](https://iojs.org/)
- Build system: [babel](http://babeljs.io/), [gulp](http://gulpjs.com/), [browserify](http://browserify.org/), [bower](http://bower.io/)
- Frameworks & libraries: [React.js](http://facebook.github.io/react/) + [Biff](https://github.com/FormidableLabs/biff) (*for flux implementation*), [Electron framework](https://github.com/atom/electron)

### TODO
As of the time applying for the contest the application isn't yet considered usable. Due to the tight time constrains, new technologies, testing out different things we where unable to get the product to a level we considerate it done. But we will continue working on it, about the latest version please check the github repository.

### Sites supported
- mobafire.com/league-of-legends/build/

### Future support plans
- probuilds.net/guide/
- solomid.net/guide/view/
- lolpro.com/user-guides/
- lolpro.com/guides/

### Roadmap
- [ ] Add windows support
- [ ] Create additional browse extensions
- [ ] Add more website support
- [ ] Map and champion specific guides

### Structure
Project was structurized into several repositories as it provides a way to create isomorphic and reusable code.

- [lol-build-manager-design](https://github.com/renarsvilnis/lol-build-manager-design) - contains design files and export files related to all applications, used in other applications as a depenency to load assets through [bower](http://bower.io/)
- [lol-build-manager-config](https://github.com/renarsvilnis/lol-build-manager-config) - node module that contains configuration for League of Legends Build Manager applications
- [lol-build-manager-util](https://github.com/renarsvilnis/lol-build-manager-util) - node module that contains utility functions that are used accross League of Legends Build Manager applications
- [lol-build-manager-chrome-extension](https://github.com/renarsvilnis/lol-build-manager-chrome-extension) - Google Chrome Extension that communicates with the native application and provides the user a fast way to import builds into the native application
- [lol-build-manager-electron-app](https://github.com/renarsvilnis/lol-build-manager-electron-app) - Star of the show - Windows and OSX application that enables the user to import League of Legends champion guides from [supported 3rd party services](https://github.com/renarsvilnis/lol-build-manager#supported-websites).


