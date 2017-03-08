# MacOS Terminal to Gnome Terminal

MTGT is a simple script that takes '.terminal' plist files for MacOS Terminal.app themes, and converts them to dconf settings for use with Gnome Terminal.  Such themes can be found [here](https://github.com/mbadolato/iTerm2-Color-Schemes).

## Requirements

  * Ruby (tested with 2.3.1)
  * Bundler gem (technically optional; you can manually install dependencies)
  * user-permissions to run dconf and modify your Gnome settings

## Usage

Install the dependencies with bundler, e.g:

`bundle install`

then run the script, with a '.terminal' file as the sole argument, and it will output the necessary dconf settings like so:

```
$ bundle exec ruby mtgt Japanesque.terminal
[org/gnome/terminal/legacy/profiles:]
list=['b1dcc9dd-5262-4d8d-a863-c897e6d979b9', 'fda28217-f0a7-4ea8-9caf-a1f81db84ec2', '738aa737-b900-4f09-b538-73b9c93784dd', '7a9cee47-ff17-4927-a4d8-ea90bdafb371', '77ccc766-f8a4-4abb-bb26-d2cb8b613e06', '857cd41c-122f-4c5e-bd9a-01f8d0f0e915']

[org/gnome/terminal/legacy/profiles:/:857cd41c-122f-4c5e-bd9a-01f8d0f0e915]
visible-name='Japanesque'
use-theme-colors=false
use-theme-background=false
use-theme-transparency=false
bold-color-same-as-fg=false
bold-color='rgb(255,255,249)'
foreground-color='rgb(247,246,236)'
background-color='rgb(29,29,29)'
pallet=['rgb(52,56,53)', 'rgb(206,62,96)', 'rgb(123,183,91)', 'rgb(232,179,42)', 'rgb(76,153,211)', 'rgb(165,127,196)', 'rgb(56,154,172)', 'rgb(249,250,246)', 'rgb(88,90,88)', 'rgb(209,142,166)', 'rgb(118,126,43)', 'rgb(119,89,46)', 'rgb(19,88,121)', 'rgb(95,65,144)', 'rgb(118,187,202)', 'rgb(177,181,174)']
```

You can either then manually add the output to a file, or pipe it directly into dconf to automatically import and add the theme:

```
$ bundle exec ruby mtgt Japanesque.terminal | dconf load /
```

The script will automatically pull the current list of themes you have, and append it's uuid to the array.  If you want to import the settings, but not "enable" the theme, simply remove that section of the dconf output.

## License

This project is licensed under the MIT license.

