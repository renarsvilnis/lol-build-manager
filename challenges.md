### Challenges faced

#### Communicating beetween browser extension and native application
First big problem we faced was to figure out how to make a Chrome extension send data to the native application.

After some Google search results found out there are several options of doing it:

1. create a remote webserver that acts as a middleman for communications
2. create a local webserver on an obscure port and do post requests to it. Example `localhost:44405`, [who even plays Mu Online anymore?](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
3. use [Chrome Native Messaging](https://developer.chrome.com/extensions/nativeMessaging) api, limiting browser extension count to only Chrome Extensions
4. Register a custom protocol that native app can recieve. Example `myapp://path/sent/to/url?foo=bar`

The 1. and 2. option was set as last option, as we wanted to keep things simple and keep issues out. In the end, hopefully, didn't managed to avoid them.

So far in the development hadn't choosen a platform to write the native app in. Looked at options like [nw.js](http://nwjs.io/) and [electron](http://electron.atom.io/). Did tests with the 3. option in both frameworks and wasn't able to recieve data from the `process.stdin`, *althought it worked for a simple node.js programm*, so we abandoned the option.

The last 4. option seemed like a great fit - no additional system complexity or wierd hacks. The only issue is that each operating system handles the registering of custom protocols differently ([Windows](http://stackoverflow.com/questions/389204/how-do-i-create-my-own-url-protocol-e-g-so), [OSX](http://stackoverflow.com/questions/471581/how-to-map-a-custom-protocol-to-an-application-on-the-mac)). This issue is easily solvable during the packaging of the application. As of writing this, [nw.js](http://nwjs.io/) doesn't offer a way, to read incoming data from a registered protocol. Whereas [electron](http://electron.atom.io/) offers an app module event `open-url`, which recieves the string and fires the app if closed. Great [electron](http://electron.atom.io/) it is.

#### Scraping data
<img src="https://s-media-cache-ak0.pinimg.com/originals/39/a8/9e/39a89e9793dcbadc5165d0084ec281f8.gif" width="300">

Second biggest issue we faced was how to get the guide data from champion guide websites -  we needed a scraper. This was our first time creating a scraper, but quickly going through a simple [tutorial](https://scotch.io/tutorials/scraping-the-web-with-node-js) felt confident we can do it.

After examining the source code of some of the guide websites and crying for 20 minutes, we rolled our sleeves and said to our screens: *"Come at me bro!"*.

<img src="http://i.giphy.com/ozhDtzrmemc0w.gif" width="300">

First of all these websites are full of akward code that looks like barely stitched together to work. Some even used 2-3 UI templating engines on a single website. Yuck! Others included a mix of serverside and client side rendering and on top that, 99% of time, they don't have any references in the DOM attribute which would indicate anything about an item or champion. Forget about simply scraping an id matching with an data entry from the League of Legends api. So for that we needed to create a way to find id's from strings. To make things even harder, simple string compare wouldn't work, as there are items with enchantments that are a string combination of `item` + `enchantment`. So had to create a way that tries to find the parent element first and then the enchantment for it.

For the first website support we choose mobefire. As it seemed the like easiest of the bunch. For adding support for additional websites later on created scraping as a module system that calls a specific module depending on url that does all the scraping with it own logic and dependencies, and it simply returns an defined structured object which gets validated and returned as results. Thus making it easy to add new modules later on. So each of the modules privately deal with the scraping as needed. 