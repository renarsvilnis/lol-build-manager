### Challenges faced
During the development of the project faced multiple issues that took alot of time from the contest period.

![Come at me bro!](http://beastmotivation.com/wp-content/uploads/2013/12/1450938_626904190681904_1232408617_n.jpg)

#### Communicating beetween browser extension and native application
First big problem faced was to figure out how to make a Chrome extension send data to the native application.

Found out there are several options of doing it:
1. create a remote webserver that acts as a midleman for communications
2. create a local webserver on an obscure port and do post requests to it. Example `localhost:44405`, [who even plays Mu Online anymore?](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
3. use [Chrome Native Messaging](https://developer.chrome.com/extensions/nativeMessaging) api
4. Register a custom protocol that native app can recieve. Example `myapp://path/sent/to/url?foo=bar`

The 1. and 2. option was set as last option, as we wanted to keep things simple and keep errors out, in the end, hopefully didn't managed to avoid them.

So far in the development hadn't choosen a platform to write the native app in, looked at options like [nw.js](http://nwjs.io/) and [electron](http://electron.atom.io/). Did tests with the 3. option in both framework options, but wasn't be able to recieve any data from the `process.stdin`, so we abandoned the options.

4. option seemed like a great fit - no additional system complexity, no operating system specific code. But each operating system handles the registering of custom protocols differently ([Windows](http://stackoverflow.com/questions/389204/how-do-i-create-my-own-url-protocol-e-g-so), [OSX](http://stackoverflow.com/questions/471581/how-to-map-a-custom-protocol-to-an-application-on-the-mac)), it can easily be added during packaging of the application. As of writing this [nw.js](http://nwjs.io/) doesn't offer a way anymore to read incoming data from a registered protocol. Whereas [electron](http://electron.atom.io/) offers an event `open-url`, which recieves the string and fires the app if closed. Great [electron](http://electron.atom.io/) it is.

#### Scraping data
Second biggest issue we faced was how to get guide data from champion guide websites. After examining the source code of the most popular websites, cried for 20 minutes, rolled my sleeves and said "Come at me bro!". First of all these websites are full of crapy code that looks like somehow stiched together to work, some even used 2-3 ui templating engines on a single website. Yuck! Including serverside rendering and also client side rendering after load. And to top everyhing, 96% time they don't have any references in the DOM which would indicate the id of something as in the League of Legends api. We needed to create a way to find id's from names. To make things even harder, search for items with enchantments would not work because their name is combined from tha base item + enchantment. So had to create a way that tries to find the parent element first and then the enchantment of it.

This was my first time creating a scraper, but quickly going through a [tutorial](https://scotch.io/tutorials/scraping-the-web-with-node-js) about scraping, felt confident. First the first website support we choose mobefire. As they seemed the like easiest of the bunch.

For adding support for additional websites later created a module system that calls a specific module depending on url that does all the scraping with it own logic and dependencies, and it simply returns an defined structured object which gets validated and returned as results. Thus making it easy to add new modules later on.