# stylix-video

## installing

```nix
{

  inputs = {
    # ...
    stylix.url = "github:danth/stylix";
  };

  outputs = { nixpkgs, ... }@inputs: {
    nixosConfigurations.default = nixpkgs.lib.nixosSystem {
      specialArgs = {inherit inputs;};
      modules = [
        ./configuration.nix
        inputs.stylix.nixosModules.stylix
      ];
    };
  };
  
}
```

## home-manager installing

```nix
{

  inputs = {
    # ...
    stylix.url = "github:danth/stylix";
  };

  outputs = { nixpkgs, home-manager, stylix, ... }@inputs: {
    homeConfigurations."«username»" = home-manager.lib.homeManagerConfiguration {
      pkgs = nixpkgs.legacyPackages.x86_64-linux;
      modules = [ 
        ./home.nix
        stylix.homeManagerModules.stylix
      ];
    };
  }
  
}
```

## selecting scheme

```nix
{ pkgs, ... }: 

{

  stylix.base16Scheme = "${pkgs.base16-schemes}/share/themes/gruvbox-dark-medium.yaml";
  
  # OR
  
  stylix.base16Scheme = {
    base00 = "282828";
    base01 = "3c3836";
    base02 = "504945";
    base03 = "665c54";
    base04 = "bdae93";
    base05 = "d5c4a1";
    base06 = "ebdbb2";
    base07 = "fbf1c7";
    base08 = "fb4934";
    base09 = "fe8019";
    base0A = "fabd2f";
    base0B = "b8bb26";
    base0C = "8ec07c";
    base0D = "83a598";
    base0E = "d3869b";
    base0F = "d65d0e";
  };
  
  # Don't forget to apply wallpaper
  
  stylix.image = ./my-cool-wallpaper.png;

}
```

# example get cursor/scheme names

```bash
$ nix build nixpkgs#bibata-cursors
$ nix build nixpkgs#base16-schemes

$ cd result

$ nix run nixpkgs#eza -- --tree --level 3
```

# fonts and cursors
```nix
{ pkgs, ... }:

{
  # ...

  stylix.cursor.package = pkgs.bibata-cursors;
  stylix.cursor.name = "Bibata-Modern-Ice";

  stylix.fonts = {
    monospace = {
      package = pkgs.nerdfonts.override {fonts = ["JetBrainsMono"];};
      name = "JetBrainsMono Nerd Font Mono";
    };
    sansSerif = {
      package = pkgs.dejavu_fonts;
      name = "DejaVu Sans";
    };
    serif = {
      package = pkgs.dejavu_fonts;
      name = "DejaVu Serif";
    };
  };

}
```

# other options

```nix
{ pkgs, ... }: 

{
  # ...

  stylix.fonts.sizes = {
    applications = 12;
    terminal = 15;
    desktop = 10;
    popups = 10;
  };

  stylix.opacity = {
    applications = 1.0;
    terminal = 1.0;
    desktop = 1.0;
    popups = 1.0;
  };
  
  stylix.polarity = "dark" # "light" or "either"

}
```
