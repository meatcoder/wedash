**wedash** is a fork of the popular weather CLI app, **wego**. 

Note that this fork is currently a WIP and mostly identical to **wego** for now. The changes planned are described in the following paragraph. 

**wedash** is meant to primarily operate in dashboard mode. It runs and updates indefinitely on a terminal window until the user quits it. It is handy to run on a terminal window or a pane in a multiplexer program like tmux.



![Screenshots](http://schachmat.github.io/wego/wego.gif)

## Dev Setup and Build Instructions

This program uses a nix flake based dev setup. It requires that nix flakes be setup and installed. The instructions for doing so can be found here: 

- Nix install guide: https://nixos.wiki/wiki/Nix_Installation_Guide
- Nix flakes config guide: https://nixos.wiki/wiki/Flakes
- Install and configure direnv using the most convenient method for you: https://direnv.net/docs/installation.html

Once you have enabled nix, the following will setup the dev environment:

1. Clone the repo with the following command:

    `git clone https://github.com/meatcoder/wedash.git`

2. Change into the directory with the following command:

    `cd wedash`

3. Enable direnve with: `direnv allow`. This will automatically build the dev environment. This will take some time, please allow it to finish.

4. Build the app using: `nix build`. The resulting binary should now be: `result/bin/wedash`.

## Updating Dependencies in Nix

If you add any new go dependencies, you will need to tell nix about them by updating the `gomod2nix.toml` file. Running the `gomod2nix` command should update that file from the changes made in the `go.mod` file. 

## Features

* show forecast for 1 to 7 days
* nice ASCII art icons
* displayed info (metric or imperial units):
  * temperature range ([felt](https://en.wikipedia.org/wiki/Wind_chill) and measured)
  * windspeed and direction
  * viewing distance
  * precipitation amount and probability
* ssl, so the NSA has a harder time learning where you live or plan to go
* multi language support
* config file for default location which can be overridden by commandline
* Automatic config management with [ingo](https://github.com/schachmat/ingo)

## Installation

Check your distribution for packaging:

[![Packaging status](https://repology.org/badge/vertical-allrepos/wego.svg)](https://repology.org/project/wego/versions)

To directly install or update the wego binary from Github into your `$GOPATH` as usual, run:
```shell
go install github.com/schachmat/wego@latest
```

## Setup

0. Run `wego` once. You will get an error message, but the `.wegorc` config file
   will be generated in your `$HOME` directory (it will be hidden in some file
   managers due to the filename starting with a dot).
0. __With an [Openweathermap](https://home.openweathermap.org/) account__
    * You can create an account and get a free API key by [signing up](https://home.openweathermap.org/users/sign_up)
    * Update the following `.wegorc` config variables to fit your needs:
    ```
      backend=openweathermap
      location=New York
      owm-api-key=YOUR_OPENWEATHERMAP_API_KEY_HERE
    ```
0. __With a [Worldweatheronline](http://www.worldweatheronline.com/) account__
    * Worldweatheronline no longer gives out free API keys. [#83](https://github.com/schachmat/wego/issues/83)
    * Update the following `.wegorc` config variables to fit your needs:
    ```
      backend=worldweatheronline
      location=New York
      wwo-api-key=YOUR_WORLDWEATHERONLINE_API_KEY_HERE
    ```
0. You may want to adjust other preferences like `days`, `units` and `…-lang` as
   well. Save the file.
0. Run `wego` once again and you should get the weather forecast for the current
   and next few days for your chosen location.
0. If you're visiting someone in e.g. London over the weekend, just run `wego 4
   London` or `wego London 4` (the ordering of arguments makes no difference) to
   get the forecast for the current and the next 3 days.

You can set the `$WEGORC` environment variable to override the default config
file location.

## Todo

* more [backends and frontends](https://github.com/schachmat/wego/wiki/How-to-write-a-new-backend-or-frontend)
* resolve ALL the [issues](https://github.com/schachmat/wego/issues)
* don't forget the [TODOs in the code](https://github.com/schachmat/wego/search?q=TODO&type=Code)

## License - ISC

Copyright (c) 2014-2017,  <teichm@in.tum.de>

Permission to use, copy, modify, and/or distribute this software for any purpose
with or without fee is hereby granted, provided that the above copyright notice
and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH
REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT,
INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS
OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER
TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF
THIS SOFTWARE.
