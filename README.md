
# 🌙 NanoTheme

**A lightweight, zero-dependency theme management library for Android**

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![API](https://img.shields.io/badge/API-21%2B-brightgreen.svg)](https://android-arsenal.com/api?level=21)
[![Size](https://img.shields.io/badge/Size-35KB-blue)]()

---

## 📖 Introduction

**NanoTheme** is a **private**, lightweight library for managing themes (Light/Dark) in Android applications. With this library, your users can easily switch between Light and Dark themes, and this change will be applied across all parts of the application.

### Why NanoTheme?

- **Zero Dependencies:** Unlike many libraries, NanoTheme has no dependencies on other libraries (like Material Design or AndroidX) and works only with the Android SDK.
- **Lightweight & Fast:** The library size is less than 50KB and puts no extra pressure on your app.
- **Simple & Powerful:** Manage your app's theme with just a few lines of code.
- **Flexible:** Developers have complete freedom to customize every part of the application.

---

## ⚙️ How It Works & Compatibility

**NanoTheme** is built from scratch using only the **Android SDK**, without any external dependencies or frameworks.

### 🔧 Built with Pure Android SDK
- **No Gradle Plugins:** Unlike many libraries, NanoTheme is not built with Gradle plugins or third-party build tools. It's a pure, handcrafted Android library.
- **No External Dependencies:** Zero reliance on libraries like `androidx`, `material`, or `com.google.android.material`.
- **100% Kotlin/Java Compatible:** Works seamlessly with both Kotlin and Java projects.

### 📦 Gradle Compatibility
Even though NanoTheme is built independently, it is **fully compatible with Gradle-based projects**. You can easily add it to your `build.gradle` or `build.gradle.kts` files using the standard `implementation project(':nanotheme')` syntax.

### ✅ Why This Matters
- **Lightweight:** No bloated dependencies, just pure Android code.
- **Stable:** No conflicts with other libraries because there are no transitive dependencies.
- **Transparent:** You know exactly what's inside the library – no hidden frameworks.

> 💡 **Good to know:** NanoTheme works with **any Android project**, regardless of your build system. Whether you use **Gradle**, **Maven**, or even **Ant**, you can integrate it with ease.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🚀 **Zero Dependencies** | Works only with Android SDK, no conflicts with other libraries. |
| 💾 **Auto Save** | User's theme selection is automatically saved in `SharedPreferences`. |
| 🌐 **Global Theme Change** | Changing theme in one screen updates all Activities and Fragments. |
| 🎨 **Status Bar Management** | Status bar color automatically syncs with the theme. |
| 🖼️ **Icon Tinting** | Easily tint icons to match the current theme using `tintIcon()`. |
| 🚫 **No White/Black Flash** | With `windowDisablePreview`, app starts smoothly with no flash. |
| 🛠️ **Full Customization** | Developers can customize every view to their liking. |
| 📱 **Dialog Support** | Create theme-aware dialogs with `createDialogBuilder()`. |

---

## 🆓 Freedom & Flexibility

**NanoTheme gives you complete freedom, not restrictions!**

| What you can do | How |
|-----------------|-----|
| **Use custom colors** | Set `android:textColor="#FF5722"` directly on any view |
| **Use theme colors** | Use `?android:textColorPrimary` to follow the theme |
| **Custom fonts** | Inherit from `Theme.Nano.Starting` and add your font |
| **Custom views** | Implement `NanoThemeable` to react to theme changes |
| **Disable features** | Turn off status bar management with `setStatusBarEnabled(false)` |
| **Ignore the library** | Don't use `tintIcon()` or `createDialogBuilder()` and manage everything yourself |

### 🧠 The Library Works FOR You, Not AGAINST You

- **No forced styles** – You control every view.
- **No hidden logic** – Everything is transparent.
- **No restrictions** – You can override anything.

> 💡 **Remember:** NanoTheme is a **toolkit**, not a cage. Use what you need, ignore what you don't.

---

## 📥 Installation & Setup

### 1. Add the Library to Your Project

Download the library from this repository and add it to your project:

**Step 1:** Place the `nanotheme` folder next to your `app` folder.

**Step 2:** Open `settings.gradle` and add this line:
```gradle
include ':app', ':nanotheme'
```

Step 3: Open build.gradle (module: app) and add this line to dependencies:

```gradle
dependencies {
    implementation project(':nanotheme')
}
```

Step 4: Click Sync Now.

---

2. Register the Library in AndroidManifest.xml

To enable automatic theme management across the entire app, you need to register NanoThemeApplication as the android:name of your application. Also, set the default theme to Theme.Nano.Starting to fix the white/black flash issue.

```xml
<application
    android:name="com.codebloom.nanotheme.NanoThemeApplication"
    android:theme="@style/Theme.Nano.Starting"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    ... >
    
    <activity android:name=".MainActivity" android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
    
    <!-- Other activities -->
    
</application>
```

Note: If you want to use a custom font or other changes globally, create a custom theme that inherits from Theme.Nano.Starting and use it here. (See Advanced Customization section for details).

---

🎨 Usage Guide (Step-by-Step)

1. Changing Theme

To change the theme, simply use the NanoThemeManager methods:

```java
import com.codebloom.nanotheme.NanoTheme;
import com.codebloom.nanotheme.NanoThemeManager;

// Switch to Dark Theme
NanoThemeManager.saveTheme(this, NanoTheme.DARK);
NanoThemeManager.applyTheme(this, NanoTheme.DARK);

// Switch to Light Theme
NanoThemeManager.saveTheme(this, NanoTheme.LIGHT);
NanoThemeManager.applyTheme(this, NanoTheme.LIGHT);
```

Note: saveTheme() stores the theme in memory, and applyTheme() applies it and recreates the activity. For a complete change, call both methods.

---

2. Using Theme Colors in XML

To make your views automatically adapt to theme changes, use ?android: values in your XML attributes:

```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="?android:windowBackground"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Sample Text"
        android:textColor="?android:textColorPrimary"
        android:textSize="18sp"/>

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Sample Button"
        android:backgroundTint="?android:colorAccent"/>

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Input text"
        android:textColorHint="?android:textColorPrimary"
        android:backgroundTint="?android:colorAccent"/>

</LinearLayout>
```

---

3. Tinting Icons to Match Theme

To tint icons to match the current theme, use the tintIcon() method:

```java
ImageView myIcon = findViewById(R.id.my_icon);

// Auto-tint to match theme (black or white)
NanoThemeManager.tintIcon(myIcon);

// Or use a custom color (e.g., Red)
NanoThemeManager.tintIcon(myIcon, Color.RED);
```

Note: This is a helper method and is optional. If you have a colored icon and don't want it to change, simply don't use this method.

---

4. Creating Theme-Aware Dialogs

To create dialogs that match the app theme, use createDialogBuilder():

```java
AlertDialog.Builder builder = NanoThemeManager.createDialogBuilder(this);
builder.setTitle("Dialog Title")
       .setMessage("Dialog message")
       .setPositiveButton("Confirm", null)
       .setNegativeButton("Cancel", null)
       .show();
```

---

5. Disabling Status Bar Management

If you don't want the library to manage the status bar color, you can disable this feature:

```java
// Disable automatic status bar management
NanoThemeApplication.setStatusBarEnabled(false);
```

---

🛠️ Advanced Customization

1. Adding a Custom Font

To use a custom font alongside the library, create a new theme that inherits from Theme.Nano.Starting:

Step 1: Open your res/values/styles.xml file.

```xml
<resources>
    <style name="Theme.MyApp" parent="Theme.Nano.Starting">
        <!-- Add custom font -->
        <item name="android:fontFamily">@font/iran_sans</item>
        
        <!-- Optional: Change default colors -->
        <item name="android:colorPrimary">#FF5722</item>
        <item name="android:colorPrimaryDark">#D84315</item>
        <item name="android:colorAccent">#4CAF50</item>
    </style>
</resources>
```

Step 2: Use your custom theme in AndroidManifest.xml:

```xml
<application
    android:name="com.codebloom.nanotheme.NanoThemeApplication"
    android:theme="@style/Theme.MyApp">
    ...
</application>
```

Important: Your theme must inherit from Theme.Nano.Starting. Otherwise, the library's core features will break and themes won't work properly.

---

2. Custom Views

If you have a custom view that needs to react to theme changes, implement the NanoThemeable interface:

```java
public class MyCustomView extends View implements NanoThemeable {

    public MyCustomView(Context context, AttributeSet attrs) {
        super(context, attrs);
        applyThemeAttributes(R.style.Theme_Nano_Light);
    }

    @Override
    public void onThemeChanged(int newThemeResId) {
        // Update view colors/styles based on new theme
        if (newThemeResId == R.style.Theme_Nano_Dark) {
            setBackgroundColor(Color.BLACK);
        } else {
            setBackgroundColor(Color.WHITE);
        }
    }

    @Override
    public void applyThemeAttributes(int themeResId) {
        // Apply initial attributes
        onThemeChanged(themeResId);
    }
}
```

---

3. Custom Colors in XML with attrs.xml

Using the attrs.xml defined in the library, you can set custom colors for individual views:

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Custom colored text"
    app:nanoTextColor="#FF5722"
    app:nanoBackgroundColor="#1A1A1A" />
```

---

❌ Common Mistakes & Solutions

1. Forgetting to Inherit from Library Theme for Customization

When adding custom fonts or other changes, your theme must inherit from Theme.Nano.Starting. Otherwise, the library's core features will break.

```xml
<!-- ❌ Wrong -->
<style name="Theme.MyApp">
    <item name="android:fontFamily">@font/iran_sans</item>
</style>

<!-- ✅ Correct -->
<style name="Theme.MyApp" parent="Theme.Nano.Starting">
    <item name="android:fontFamily">@font/iran_sans</item>
</style>
```

---

2. Not Registering NanoThemeApplication in Manifest

If you don't register NanoThemeApplication in AndroidManifest.xml, automatic theme management won't work.

```xml
<!-- ❌ Wrong -->
<application>
    ...
</application>

<!-- ✅ Correct -->
<application
    android:name="com.codebloom.nanotheme.NanoThemeApplication"
    ...>
</application>
```

---

3. Using Hardcoded Colors for Theme-Aware Views

If you want a view to change with the theme, use ?android: attributes:

```xml
<!-- ❌ Wrong (won't change with theme) -->
<TextView
    android:textColor="#000000" />

<!-- ✅ Correct (changes with theme) -->
<TextView
    android:textColor="?android:textColorPrimary" />
```

---

4. Forgetting the Starting Theme for Flash Fix

To fix the white/black flash issue on app startup, always use Theme.Nano.Starting:

```xml
<!-- ❌ Wrong (flash will appear) -->
<application
    android:theme="@style/Theme.Nano.Light">

<!-- ✅ Correct (no flash) -->
<application
    android:theme="@style/Theme.Nano.Starting">
```

---

🧩 Complete Example (Activity)

```java
package com.example.myapp;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import com.codebloom.nanotheme.NanoTheme;
import com.codebloom.nanotheme.NanoThemeManager;

public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnLight = findViewById(R.id.btnLight);
        Button btnDark = findViewById(R.id.btnDark);
        Button btnGoToSecond = findViewById(R.id.btnGoToSecond);

        btnLight.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                NanoThemeManager.saveTheme(MainActivity.this, NanoTheme.LIGHT);
                NanoThemeManager.applyTheme(MainActivity.this, NanoTheme.LIGHT);
            }
        });

        btnDark.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                NanoThemeManager.saveTheme(MainActivity.this, NanoTheme.DARK);
                NanoThemeManager.applyTheme(MainActivity.this, NanoTheme.DARK);
            }
        });

        btnGoToSecond.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(MainActivity.this, SecondActivity.class));
            }
        });
    }
}
```

---

📄 License

This library is released under the MIT License. You are free to use, modify, and distribute it, even in commercial projects.

---

🤝 Contributing

If you have ideas, suggestions, or find any issues, feel free to open an Issue. Pull requests are also welcome!

---

📞 Contact

· GitHub: codebloomir-dev
· Email: codebloomir@gmail.com

---

⭐ Support

If you like this library, please give it a Star ⭐ on GitHub to help others discover it!

---

Built with ❤️ by codebloom

Thank you for using NanoTheme! ☕

