# ShapeCorners
<img src="https://i.imgur.com/H9nuCv8.png" alt="Three desktop windows demonstrating the Rounded corner effect." align="right" width="400px">
KDE effect rounds/chisels corners of your windows.

Fork of [this](https://github.com/khanhas/ShapeCorners), which is a fork of [this](https://sourceforge.net/projects/shapecorners/). Implements KDE 5.23 fixes from [matinlotfali's fork](https://github.com/matinlotfali/KDE-Rounded-Corners).

Using an older version of KDE? Check out [the `pre-5.23`](https://github.com/ZacharyTalis/ShapeCorners/tree/pre-5.23) and [`5.23`](https://github.com/ZacharyTalis/ShapeCorners/tree/5.23) branches!

### Features:
- Customizable via config file
- Different types of corner: `Rounded` and `Chiseled`
- Each corner can have different radius
- Ability to square corner when windows edge is at screen edge
- Ability to define `Whitelist` and `Blacklist` to exclude/force applying ShapeCorners

## Why this fork?
We've got:
- The experimental corner type `Squircled` type and its `SquircleRatio`
- `SquareEdgesX` and `SquareEdgesY`, which allow you to define extra coordinates at which `SquareAtScreenEdge` will take effect. Particularly useful for multi-monitor setups

## Dependencies
- Distro Debian based (Ubuntu, Kubuntu):
```
sudo apt install git cmake g++ gettext extra-cmake-modules qttools5-dev libqt5x11extras5-dev libkf5configwidgets-dev libkf5crash-dev libkf5globalaccel-dev libkf5kio-dev libkf5notifications-dev kinit-dev kwin-dev 
```
- Distro Arch based:
```
sudo pacman -S git cmake gcc gettext extra-cmake-modules qt5-tools qt5-x11extras kcrash kglobalaccel kde-dev-utils kio knotifications kinit kwin
```

## Build
```
git clone https://github.com/ZacharyTalis/ShapeCorners
cd ShapeCorners
mkdir build; cd build
cmake ../ -DCMAKE_INSTALL_PREFIX=/usr -DQT5BUILD=ON
make && sudo make install
kwin_x11 --replace &
```

It should be now activated.

## Config
- Create file `shapecornersrc` in `~/.config`
- Follow this template:
```ini
[General]
Radius=10
Type=Rounded
SquareAtScreenEdge=false
FilterShadow=false
Whitelist=
Blacklist=
SquareEdgesX=
SquareEdgesY=
SquircleRatio=1.0
```

- `Radius`: Define all corners' or specific corner's radius. Accept 1 to 4 numbers, separate by `,`. E.g.:
    - `Radius=20`: All corners have 20 radius
    - `Radius=10,20`: Top Left and Bottom Right has 10; Top Right and Bottom Left has 20
    - `Radius=30,40,50`: Top Left has 30; Top Right and Bottom Left has 40; Bottom Right has 50
    - `Radius=20,50,30,10`: Top Left has 20; Top Right has 50; Bottom Right has 30; Bottom Left has 10
- `Type`: `Rounded`, `Chiseled`, or `Squircled`
- `SquareAtScreenEdge`: Square off corner at when window edge is at screen edge. Boolean `true` or `false`.
- `FilterShadow`: Since there is no way to change corners of shadow layer, you might want to remove shadow layer out. Boolean `true` or `false`.
- `Whitelist`: List of window class names that will be forced to apply ShapeCorners. Separate them by `,`. E.g.:
    - `Whitelist=conky`
    - `Whitelist=plasma,conky`
- `Blacklist`: List of window class names that will be excluded from applying ShapeCorners. Separate them by `,`. E.g.:
    - `Blacklist=krunner`
    - `Blacklist=krunner,display`
- `SquareEdgesX`: Extra X coordinates in which SquareAtScreenEdge should take effect. Useful when monitors are placed horizontally from each other, or with monitors of different resolutions. E.g.:
    - `SquareEdgesX=1080,1081,3000,3001`
- `SquareEdgesY`: Extra Y coordinates in which SquareAtScreenEdge should take effect. Useful when monitors are placed vertically from each other, or with monitors of different resolutions. E.g.:
    - `SquareEdgesY=1920`
- `SquircleRatio`: Behind the scenes, squircle corners are approximated using cubic Bézier curves. Use this value to adjust the strength of all Bézier control points. Just don't stray too far from the default `1.0`! E.g.:
  - `SquircleRatio=1.043`

After changing config, run:
```bash
kwin_x11 --replace &
```

Happy Squircling!

<img src="https://i.imgur.com/4e0VFku.png" alt="A file browser and a terminal in KDE featuring squircle-ish rounded corners. The terminals shows off colorful ASCII art of a cow saying, 'ShapeCorners gets Squircled!'">
