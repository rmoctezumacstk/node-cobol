
[![cobol](http://i.imgur.com/DutRzDr.png)](#)

# cobol

 [![Support me on Patreon][badge_patreon]][patreon] [![Buy me a book][badge_amazon]][amazon] [![PayPal][badge_paypal_donate]][paypal-donations] [![Version](https://img.shields.io/npm/v/cobol.svg)](https://www.npmjs.com/package/cobol) [![Downloads](https://img.shields.io/npm/dt/cobol.svg)](https://www.npmjs.com/package/cobol)

> COBOL bridge for NodeJS which allows you to run COBOL code from NodeJS.

## Can I use this on production?

Of course, you can! It's production ready! If you ever did such a thing, [ping me (@IonicaBizau)](https://twitter.com/IonicaBizau). :boom: :dizzy:


## Installation

Currently GNUCobol is required. If you are using a debian-based distribution you can install it using:

```sh
$ sudo apt-get install open-cobol
```

:bulb: It would be interesting to fallback into a COBOL compiler written in NodeJS. [Contributions are welcome!][contributing] :smile:

Then, install the `cobol` package.

```sh
$ npm i cobol
```

## :clipboard: Example



```js
// Dependencies
var Cobol = require("cobol");

// Execute some COBOL snippets
Cobol(function () {/*
                   IDENTIFICATION DIVISION.
                   PROGRAM-ID. HELLO.
                   ENVIRONMENT DIVISION.
                   DATA DIVISION.
                   PROCEDURE DIVISION.
                   PROGRAM-BEGIN.
                   DISPLAY "Hello world".
                   PROGRAM-DONE.
                   STOP RUN.
                   */}, function (err, data) {
    console.log(err || data);
});
// => "Hello World"

Cobol(__dirname + "/args.cbl", {
    args: ["Alice"]
}, function (err, data) {
    console.log(err || data);
});
// => "Your name is: Alice"

// This will read data from stdin
Cobol(function () {/*
                   IDENTIFICATION DIVISION.
                   PROGRAM-ID. APP.
                   *> http://stackoverflow.com/q/938760/1420197
                   ENVIRONMENT DIVISION.
                   INPUT-OUTPUT SECTION.
                   FILE-CONTROL.
                   SELECT SYSIN ASSIGN TO KEYBOARD ORGANIZATION LINE SEQUENTIAL.
                   DATA DIVISION.
                   FILE SECTION.
                   FD SYSIN.
                   01 ln PIC X(64).
                   88 EOF VALUE HIGH-VALUES.
                   WORKING-STORAGE SECTION.
                   PROCEDURE DIVISION.
                   DISPLAY "Write something and then press the <Enter> key"
                   OPEN INPUT SYSIN
                   READ SYSIN
                   AT END SET EOF TO TRUE
                   END-READ
                   PERFORM UNTIL EOF
                   DISPLAY "You wrote: ", ln
                   DISPLAY "------------"
                   READ SYSIN
                   AT END SET EOF TO TRUE
                   END-READ
                   END-PERFORM
                   CLOSE SYSIN
                   STOP RUN.
                   */}, {
    stdin: process.stdin,
    stdout: process.stdout
}, function (err) {
    if (err) {
        console.log(err);
    }
});
// => Write something and then press the <Enter> key
// <= Hi there!
// => You wrote: Hi there!
// => ------------
```

## :memo: Documentation


### `Cobol(input, options, callback)`
Runs COBOL code from Node.JS side.

#### Params
- **Function|String|Path** `input`: A function containing a comment with inline COBOL code, the cobol code itself or a path to a COBOL file.
- **Object** `options`: An object containing the following fields:
 - `cwd` (String): Where the COBOL code will run (by default in the current working directory)
 - `args` (Array): An array of strings to pass to the COBOL process.
 - `free` (Boolean): Use free option while compiling with GnuCobol
 - `stdin` (Stream): An optional stdin stream used to pipe data to the stdin stream of the COBOL process.
 - `stderr` (Stream): An optional stderr stream used to pipe data to the stdin stream of the COBOL process.
 - `stdeout` (Stream): An optional stdout stream used to pipe data to the stdin stream of the COBOL process.
 - `remove` (Boolean): Should the compiled executable be removed after running, default is true.
 - `precompiled` (Boolean): Run the precompiled executable instead of re-compiling, default is false.
- **Function** `callback`: The callback function called with `err`, `stdout` and `stderr`.



## :newspaper: Press Highlights

This project seems to more popular than I expected. :smile: If you wrote or found an article about this project which is not added in this list, [add it][contributing].


 - [Calling 1959 from your Web code: A COBOL bridge for Node.js](http://arstechnica.com/information-technology/2015/08/calling-1959-from-your-web-code-a-cobol-bridge-for-node-js/) ([ArsTechnica](http://arstechnica.com/), by [Sean Gallagher](http://arstechnica.com/author/sean-gallagher/))
 - [Cobol -- yes, Cobol -- gets a bridge to Node.js](http://www.infoworld.com/article/2972314/application-development/cobol-nodejs-bridge.html) ([InfoWorld](http://www.infoworld.com/), by [Paul Krill](http://www.infoworld.com/author/Paul-Krill/))
 - [Ein COBOL-Plug-in für Node.js](http://www.heise.de/newsticker/meldung/Ein-COBOL-Plug-in-fuer-Node-js-2783225.html) ([Heise Online](http://heise.de), by [Alexander Neumann](http://www.heise.de/ix/editors/ix_redakteur_907177.html))
 - [Dit krijg je als je Node.js met COBOL kruist](http://webwereld.nl/open-source/88040-dit-krijg-je-als-je-node-js-met-cobol-kruist) ([Webwereld](http://webwereld.nl/), by [Chris Koenis](http://webwereld.nl/auteur/chris-koenis))
 - [COBOL for Node.js](http://www.i-programmer.info/news/98-languages/8904-cobol-for-nodejs.html) ([I Programmer](http://www.i-programmer.info/), by [Kay Ewbank](https://twitter.com/KayEwbank))
 - [Nagyon durva: Már COBOL-ból is lehet programozni a Node.js-t](http://prog.hu/hirek/4012/nagyon-durva-mar-cobol-bol-is-lehet-programozni-a-node-js-t) ([prog.hu](http://prog.hu/), by [Sting](http://prog.hu/azonosito/info/Sting?pop=1))
 - [Micro Focus Updates COBOL for Visual Studio 2015](http://www.eweek.com/developer/micro-focus-updates-cobol-for-visual-studio-2015.html) ([eWeek](http://eweek.com/), by [Darryl K. Taft](http://www.eweek.com/cp/bio/Darryl-K.-Taft/))
 - [Sur GitHub, un projet relie Cobol et Node.js](http://www.lemondeinformatique.fr/actualites/lire-sur-github-un-projet-relie-cobol-et-nodejs-62116.html) ([LeMondeInformatique](http://lemondeinformatique.fr/), by [Maryse Gros avec IDG News Service](mailto:redac_weblmi@it-news-info.com))
 - [3 open source projects for modern COBOL development](http://opensource.com/life/15/10/open-source-cobol-development) ([OpenSource.com](http://opensource.com/), by [Joshua Allen Holm](http://opensource.com/users/holmja))

## :yum: How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].


## :sparkling_heart: Support my projects

I open-source almost everything I can, and I try to reply everyone needing help using these projects. Obviously,
this takes time. You can integrate and use these projects in your applications *for free*! You can even change the source code and redistribute (even resell it).

However, if you get some profit from this or just want to encourage me to continue creating stuff, there are few ways you can do it:

 - Starring and sharing the projects you like :rocket:
 - [![PayPal][badge_paypal]][paypal-donations]—You can make one-time donations via PayPal. I'll probably buy a ~~coffee~~ tea. :tea:
 - [![Support me on Patreon][badge_patreon]][patreon]—Set up a recurring monthly donation and you will get interesting news about what I'm doing (things that I don't share with everyone).
 - **Bitcoin**—You can send me bitcoins at this address (or scanning the code below): `1P9BRsmazNQcuyTxEqveUsnf5CERdq35V6`

    ![](https://i.imgur.com/z6OQI95.png)

Thanks! :heart:


## :dizzy: Where is this library used?
If you are using this library in one of your projects, add it in this list. :sparkles:


 - [`cobol-promises`](https://github.com/IonicaBizau/node-cobol-promises)—COBOL bridge for NodeJS with promises support.

## :sparkles: Related

 - [`node.cobol`](https://github.com/IonicaBizau/node.cobol#readme)—Node.js bridge for COBOL which allows you to run Node.js code from COBOL.
 - [`fortran`](https://github.com/IonicaBizau/node-fortran)—Fortran bridge for Node.js which allows you to run Fortran code from Node.js.
 - [`node.fortran`](https://github.com/IonicaBizau/node.fortran#readme)—Execute Node.js in your Fortran programs.


## :scroll: License

[MIT][license] © [Ionică Bizău][website]

[badge_patreon]: http://ionicabizau.github.io/badges/patreon.svg
[badge_amazon]: http://ionicabizau.github.io/badges/amazon.svg
[badge_paypal]: http://ionicabizau.github.io/badges/paypal.svg
[badge_paypal_donate]: http://ionicabizau.github.io/badges/paypal_donate.svg
[patreon]: https://www.patreon.com/ionicabizau
[amazon]: http://amzn.eu/hRo9sIZ
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RVXDDLKKLQRJW
[donate-now]: http://i.imgur.com/6cMbHOC.png

[license]: http://showalicense.com/?fullname=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica%40gmail.com%3E%20(https%3A%2F%2Fionicabizau.net)&year=2013#license-mit
[website]: https://ionicabizau.net
[contributing]: /CONTRIBUTING.md
[docs]: /DOCUMENTATION.md
