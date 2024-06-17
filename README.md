# SFMono-Nerd-Font-Ligaturized
This repository contains pre-patched opentype versions of macOS's SFMono fonts with support for Ligatures and Nerd Fonts. 

## Showcase
<img width="1087" alt="image" src="https://user-images.githubusercontent.com/71196912/205556850-5805aad7-3500-4a98-9ef2-b0cdc6aff957.png">
<img width="1514" alt="image" src="https://user-images.githubusercontent.com/71196912/205555115-7079b836-2c7e-43d7-b81b-256cc8d12807.png">

## Installation
### Universal
```bash
#!/bin/bash

if [ "$(uname)" == "Darwin" ]; then
	FONTS=$HOME/Library/Fonts
else
	FONTS=$HOME/.fonts
fi

wget https://github.com/xelorr/SFMono-Nerd-Font-Ligaturized/releases/latest/download/sf.tar.xz
mkdir -p $FONTS
tar xvf sf.tar.xz -C $FONTS/
rm sf.tar.xz
```
### Manual
#### Linux
Copy all of the font files to `~/.local/share/fonts` or `~/.fonts/`
```sh
wget https://github.com/xelorr/SFMono-Nerd-Font-Ligaturized/releases/latest/download/sf.tar.xz
mkdir -p $HOME/.fonts
tar xvf sf.tar.xz -C $HOME/.fonts/
rm sf.tar.xz
```

#### MacOS
Copy all of the font files to `~/Library/Fonts/`
```sh
wget https://github.com/xelorr/SFMono-Nerd-Font-Ligaturized/releases/latest/download/sf.tar.xz
mkdir -p $HOME/Library/Fonts
tar xvf sf.tar.xz -C $HOME/Library/Fonts/
rm sf.tar.xz
```

### Homebrew
Needs a working installation of `brew`
```sh
brew tap shaunsingh/SFMono-Nerd-Font-Ligaturized
brew install --cask font-sf-mono-nerd-font-ligaturized
```

### Nix (flake)
Add this repo as an input 
```nix
inputs = {
  # SFMono w/ patches
  sf-mono-liga-src = {
    url = "github:shaunsingh/SFMono-Nerd-Font-Ligaturized";
    flake = false;
  };
};
```

Then add the following overlay
```nix
(final: prev: {
  sf-mono-liga-bin = prev.stdenvNoCC.mkDerivation rec {
    pname = "sf-mono-liga-bin";
    version = "dev";
    src = inputs.sf-mono-liga-src;
    dontConfigure = true;
    installPhase = ''
      mkdir -p $out/share/fonts/opentype
      cp -R $src/*.otf $out/share/fonts/opentype/
    '';
  };
}) 
```

Now you can install `sf-mono-liga-bin` as normal
```nix
fonts = {
  fonts = with pkgs; [ sf-mono-liga-bin ];
};
```

## Features
Contains the following Iconsets:
- fontawesome
- fontawesomeextentions
- fontlogos
- octicons
- codicons
- pomicons
- powerline (height adjusted)
- powerlineextra (height adjusted)
- material
- weather

Ligatures are from FiraCode v3.1
