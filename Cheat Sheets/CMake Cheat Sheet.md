![[drawing1|1000]]

ternary generator exprssion
```
$<IF:$<CONFIG:Debug>,cppzmq,cppzmq-static>
```
```
```
    set(ULTRA_COMPILED_SHADERS_DIRECTORY ${base_dir}/$<IF:$<CONFIG:Debug>,Debug,Relese>/compiled_shaders)
   