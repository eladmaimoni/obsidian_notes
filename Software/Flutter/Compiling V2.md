
# cloning and gclient
- things are a bit "simpler now", engine is within the flutter repo and gclient runs within the flutter repo's root
- glclient is a shitty tool, it seems to corrupt things by trying to parallelize.
  do this `gclient sync --no-history --jobs 2` instead of default "gclient"
- after setting up the "et" tool, it wants you to run it using powershell, not git bash


```
git checkout 3.35.6
rm -rf ./out
gclient sync -D --no-history --jobs 2
cd .\engine\src\
python .\flutter\tools\gn --no-goma
ninja -C ./out/host_debug
```