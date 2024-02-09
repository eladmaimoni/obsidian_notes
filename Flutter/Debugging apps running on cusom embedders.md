How to set the observatory port?

- when the JIT engine is running, you will see the following message:


the port is determined randomly unless specified to the engine arguments explicitly:
```
config.engine_switches.push_back("ultrawis.exe");

config.engine_switches.push_back("--observatory-port=50052");

config.engine_switches.push_back("--vm-service-port=50053");

config.engine_switches.push_back("--disable-service-auth-codes");

  

...

  

FlutterProjectArgs flutterProjectArgs {

.struct_size = sizeof(FlutterProjectArgs),

.assets_path = assets_path_str.c_str(),

.icu_data_path = icu_data_path_str.c_str(),

.platform_message_callback = nullptr, // PlatformMessageStatic,

//.root_isolate_create_callback = RootIsolateCreateStatic,

.vsync_callback = EnqueueHandleNotifyOnNextVSyncRequestStatic,

.custom_task_runners = &_taskRunners,

.compositor = &_compositor.GetFlutterCompositor(),

.aot_data = _aotData.get(),

};

  

flutterProjectArgs.command_line_argc = (int)_config.engine_switches.size();

flutterProjectArgs.command_line_argv = _config.engine_switches.data();
```

and here is a launch.json that works for attaching:
```
{

"type": "dart",

"name": "Flutter Embedded Attach",

"request": "attach",

"vmServiceUri": "http://127.0.0.1:50053/"

}
```

[https://github.com/sony/flutter-embedded-linux/wiki/How-to-debug-Flutter-apps](https://github.com/sony/flutter-embedded-linux/wiki/How-to-debug-Flutter-apps)

[https://github.com/flutter/flutter/wiki/Using-custom-embedders-with-the-Flutter-CLI](https://github.com/flutter/flutter/wiki/Using-custom-embedders-with-the-Flutter-CLI)