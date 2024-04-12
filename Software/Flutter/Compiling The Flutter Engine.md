### Official Docs

* [Setting up the Engine development environment](https://github.com/flutter/flutter/wiki/Setting-up-the-Engine-development-environment)
* [Compiling the engine](https://github.com/flutter/flutter/wiki/Compiling-the-engine)
* [Builidng the engine for embedded devices](https://www.industrialflutter.com/blogs/building-the-flutter-engine-for-embedded-hardware/)


```
# clone flutter repo
git clone https://github.com/flutter/flutter.git
# checkout to your desired tag / commit or desired channel
git checkout 2.10.5 // specific commit
flutter channel stable // stable channel
flutter channel master // master channel
# check which engine version (git commit) your flutter version needs
cat ./bin/internal/engine.version # mine was 57d3bac3dd5cb5b0e464ab70e7bc8a0d8cf083ab
# add the bin directory to the PATH
setx PATH="$PATH:/new/path/to/append"
# run flutter tool so it will download stuff
flutter

# switch to your desired channel / commit again and rerun flutter tool

# add depot tools to path (C:\libs\depot_tools)

```

### Important
* Run all commands via powershell as adsministrator

### Tools & Environment
* Visual Studio
* Windows SDK & Debugging Tools For Windows
if you already have Windows SDK, you can go to programs & features, click modify and add Debugging Tools For Windows
* Chromium's [depot_tools](https://commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools_tutorial.html#_setting_up)
  Add the depot_tools directory to the front of your PATH.
* Download & install Python 2.7 and python3. make sure python 2.7 is first on your PATH. 
* using powershell run:
`Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled" -Value 1 -Force`
* add system envirnoment variables:
```
DEPOT_TOOLS_WIN_TOOLCHAIN=0
GYP_MSVS_OVERRIDE_PATH="C:\Program Files\Microsoft Visual Studio\2022\Community" # (or your location for Visual Studio)
WINDOWSSDKDIR="C:\Program Files (x86)\Windows Kits\10" # (or your location for Windows Kits)
```

Cloning & Downloading

1. Configure your machine with an SSH key that is known to github by following the directions [here](https://help.github.com/articles/generating-ssh-keys/).
2. Fork https://github.com/flutter/engine into your own GitHub account. Do not clone it locally. gclient will do that for you in a later step.
Create an empty directory called **engine **for your copy of the repository and cd into it.
Create a .gclient file in the engine directory with the following contents, replacing <your_name_here> with your GitHub account name:
```
solutions = [
  {
    "managed": False,
    "name": "src/flutter",
    "url": "git@github.com:eladm-ultrawis/engine.git",
    "custom_deps": {},
    "deps_file": "DEPS",
    "safesync_url": "",
  },
]
```

3. With powershell **as admin**:
* cd to the engine directory you just created
* run `gclient sync`
```
gclient sync --revision=src/flutter@cdbeda788a293fa29665dc3fa3d6e63bd221cb0d
(revision is the git hash specified in engine.version)
```
gclient sync in that directory. On Windows, gclient sync must be run as Administrator due to [this issue](https://github.com/flutter/flutter/issues/94580). This will fetch all the source code that Flutter depends on. Avoid interrupting this script, as doing so can leave your repository in an inconsistent state that is tedious to clean up. (This step automatically runs git clone, among other things.)

4. Add a remote for the upstream repository:
* `cd src/flutter` (This was created in your engine directory by gclient sync.)
* `git remote add upstream git@github.com:flutter/engine.git` (So that you fetch from the master flutter/engine repository, not your clone, when running git fetch et al.)
* `git remote rm origin` (Remove the old origin so we can replace it.)
* `git remote add origin git@github.com:eladm-ultrawis/engine.git`
* `cd ..` (Return to the src directory that gclient sync created in your engine directory.)

### Matching the engine version to your flutter sdk version
- look for a file named engine.version
- this file points to a commit in engine/src/flutter that matches the SDK you have installed
- go to engine/src/flutter and checkout to this commit.

### building the project
1. generate the Visual Studio solution using gn:
```
C:\Libraries\engine\src> python .\flutter\tools\gn --no-goma --unoptimized
C:\Libraries\engine\src> python .\flutter\tools\gn --no-goma --unoptimized --runtime-mode=release
C:\Libraries\engine\src> python .\flutter\tools\gn --no-goma --runtime-mode=release
C:\Libraries\engine\src> python .\flutter\tools\gn --no-goma
```
* the --unpoptimized flag meand whether to build the engine in debug / release build
* --no-goma means don't use some google tool
* --runtime-mode means whether to build the AOT engine or the JIT engine

2. run ninja: **(Don't open the VS solution file!)**
```
ninja -C .\out\<dir created by previous step>

ninja -C .\out\host_debug\
ninja -C .\out\host_debug_unopt\
ninja -C .\out\host_release\
ninja -C .\out\host_release_unopt\
```
### Updating an existing engine
```

cd C:/Libraries/engine/src/flutter
git pull / git checkout 
cd C:/Libraries/engine
gclient sync
cd C:/Libraries/engine/src/
python .\flutter\tools\gn --no-goma
ninja -C .\out\host_debug\
python .\flutter\tools\gn --no-goma --runtime-mode=release
ninja -C .\out\host_release\
```

- I think it is necessary to delete the out folder manually.































