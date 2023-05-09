# Tom's Website

Hello there!

This repo contains the files required to build my website with [Hugo](https://gohugo.io).

## License

Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg

## General usage

Clone the repo
```
$ git clone https://github.com/tvillega/dcc-webpage
```

Enter the directory
```
$ cd dcc-webpage
```

Create a new post
```
$ hugo new posts/slug-name.md
```

Live update preview
```
$ hugo serve -t terminal
```

Production build
```
$ hugo -t terminal -d /path/to/build/
```
