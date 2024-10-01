

### Simple Version Upload Workflow

1. Go to Production
2. Create New Release on top right
3. go to pubspec.yaml and increment the version and build number
```
version: 1.0.1+15
```
to 
```
version: 1.0.2+16
```
4. compile flutter app using the following commnad:
```
dart run build_runner build
flutter build appbundle
```
this will generate a file in `build/app/outputs/bundle/release/app.aab`
4. drag and drop the file into the console
5. continue with whatever prompts