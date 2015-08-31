## League of Legends Build Manager

Parent repository of the League of Legends Build Manager project for the [The Riot Games API Challenge 2.0](https://developer.riotgames.com/discussion/announcements/show/2lxEyIcE).

**Category: Item Sets**

### Team members
1. Renārs Vilnis
  Role: Programming, Project leader
  Country: Latvia
  City: Bergi
  LOL Summoner: citrons
  LOL Region: eune
2. Anete Jakobsone
  Role: Design
  Country: Latvia
  City: Bergi
  LOL Summoner: GorgeousCupcake
  LOL Region: eune

### Idea
Idea was to help players get better at League of Legends by helping them learn new champions using the capabilities of League of Legends item-sets. We all have a time when we lookup a build in mobafire, probuilds, solomid etc.., it is easy to remember the spell order, but when it comes to champion build we usually end up alt-tabbing during the game. Felt like that could have been done better so we built applications that help aid players get their wanted champion builds in game through scraping the website.

### Under the hood
We use JavaScript everwhere - the ideology was to create isomorphic code, which we achieved with help of node package manager and code seperation into reusable modules.
For now we have created a Chrome extension that checks each tab, whether it is supported by the native application, if so then it displays an icon in the action bar of Chrome that allows with a single click to import the game into the native application what is achieved by registering a custom protocol on operating system, similar like 'mailto:' to works. Because of the code reusability and modularisation it is trivial to create different brower extensions. 
Now the main show - the native app. It created using Electron frameworks which allows to create cross platform desktop applications using web technologies and node. The goal is to add support for Windows and OSX, although for now we only support OSX, need to do testing on it. The native application allows its user to manage builds and guides, either externaly created or by the application. Even if the user hasn't installed any browser extension, he is able to manualy add the url within the application.
To make the application work offline - with limited functionality, we save item and champion information and images through League of Legends static data api. On each application boot it checks if there are a new game version it automaticly update its required assets.

### TODO
As of the time applying for the contest the application isn't yet considered usable. Due to the tight time constrains, new technologies, testing out different things we where unable to get the product to a level we considerate it done. But we will continue working on it, about the latest version please check the github repository.

**Technology stack:** JavaScript, ES6, Babel + FLux, io.js, Electron framework. lowdb

### Sites supported
mobafire.com/league-of-legends/build/

### Future support plans
probuilds.net/guide/
solomid.net/guide/view/
lolpro.com/user-guides/
lolpro.com/guides

### Roadmap
- Add windows support
- Add more website support
- Map and champion specific guides

### Structure
Project was structurized into several repositories as it provides a way to create isomorphic code.

- [lol-build-manager-design](https://github.com/renarsvilnis/lol-build-manager-design) - contains design files and export files related to applications
- [lol-build-manager-config](https://github.com/renarsvilnis/lol-build-manager-config) - node module that contains configuration for League of Legends Build Manager applications
- [lol-build-manager-util](https://github.com/renarsvilnis/lol-build-manager-util) - node module that contains utility functions that are used accross League of Legends Build Manager applications
- [lol-build-manager-chrome-extension](https://github.com/renarsvilnis/lol-build-manager-chrome-extension) - Google Chrome Extension that communicates with the native application and provides the user a fast way to import builds into the native application
- [lol-build-manager-electron-app](https://github.com/renarsvilnis/lol-build-manager-electron-app) - Star of the show - Windows and OSX application that enables the user to import League of Legends champion guides from [supported 3rd party services](https://github.com/renarsvilnis/lol-build-manager#supported-websites).


