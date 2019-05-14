# CustomBuildForGodot For iOS
Project contain custom compiled binary for godot engine and steps to reproduce without facing any error.

### What you need before compile

1. Download Godot Stable Version 3.1 and its export template from this [Link](https://downloads.tuxfamily.org/godotengine/3.1/)
2. Open Godot 3.1 and install it's export template that you download from step 1.
3. Download Godot 3.1 Stable Source code from [Godot 3.1 Source](https://github.com/godotengine/godot/releases)
4. Open terminal change directory to your godot source code.(In my case `/Downloads/GodotSource/godot`)
5. Run following command to generate ios custom export template.

```
scons p=iphone tools=no target=debug arch=arm
scons p=iphone tools=no target=debug arch=arm64
```
above steps will give you two binery in `godot/bin` named `libgodot.iphone.debug.arm.a` and `libgodot.iphone.debug.arm64.a`.

6. Run below command to generate *.fat binary from above two files.

```
lipo -create bin/libgodot.iphone.debug.arm64.a bin/libgodot.iphone.debug.arm.a  -output bin/libgodot.iphone.debug.fat.a
```
will give you **libgodot.iphone.debug.fat.a** in `godot/bin` folder.

7. Copy above **libgodot.iphone.debug.fat.a** from `godot/bin` to `godot/misc/dist/ios_xcode` folder (replaced).
8. Copy **ios_xcode** folder in documents, rename **ios_xcode** to **iphone**, then zip it. you'll get result **iphone.zip** in Document folder.
9. Then replace **iphone.zip** with `/Library/Application\ Support/Godot/templates/3.1.stable`

### Export Project
1. create simple project in godot or open your project.
2. export your project
3. Open your exported project in xcode. (in my case Xcode 10.0, with developer account)
4. In xcode open `Images.xcassets` and delete all images(my icon is not ready to i delete all) Like [this](https://imgur.com/JZgqcNz)
5. Disable `pushnotification` from `Target>Capabilities`
6. Change `Deployment Target` to 10.0 in project and target general tab.
7. **Signing :** Check automatically manage signing and select team. [Look like this](https://imgur.com/RPuV2er)
8. Open `issue navigator` from left side in xcode and click under `validate project Settings`. [Image](https://imgur.com/OmGeEs8)
9. As you click xcode will popup like this [image](https://imgur.com/ieyiIT9)
10. Click on button `Perform Changes`.
11. Before you hit **Run** make sure you close **Godot Engie**. (If i keep open and hit run in xcode its freez my machine.)
12. Done. you are compile your ios project using custom ios template.









