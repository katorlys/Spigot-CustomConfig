# Spigot-CustomConfig
[![License](https://img.shields.io/badge/license-GPLv3-blue?style=for-the-badge)](https://www.gnu.org/licenses/gpl-3.0.html)  ![Pull Requests](https://img.shields.io/github/issues-pr-closed/katorlys/Spigot-CustomConfig?style=for-the-badge) ![Issues](https://img.shields.io/github/issues-closed/katorlys/Spigot-CustomConfig?style=for-the-badge)

## Introduction
Bukkit API only allows you to create one config for each plugins, and there is no sign that it will change the situation in the future versions.<br>
Now this piece of code allows you to create custom configs in Bukkit/Spigot plugins, and you can set where the config should be saved.<br>
What's more, the code extends `org.bukkit.configuration.file.YamlConfiguration` so that you can use methods such as `getConfig()` and `saveConfig()` as usual.<br>

However, I didn't rewrite method `reloadConfig()` so it will remove all the comments as Bukkit API does. Maybe I'll rewrite it next time.🤣<br>

## Usage
### Create Config
For example, I would like to create a custom YML config named "AConfig" for MyPlugin in "plugins/MyPlugin/settings/".<br>
First, register the config in the main class:<br>
```java
public class MyPlugin extends JavaPlugin {
    public static ConfigReader AConfig;
}
```
Second, load the config on plugin enable:<br>
```java
public void onEnable() {
    AConfig = new ConfigReader(this,"settings/","AConfig.yml");
	AConfig.saveDefaultConfig();
}
```
After all that work, you can use all methods in the rest of the plugin.<br>
Here is some examples:<br>
```java
FileConfiguration aconfig = AConfig.getConfig();
List<String> value1 = aconfig.getStringList("First-List");
aconfig.set("First-object","element");
aconfig.reloadConfig();
aconfig.saveConfig();
```
There are also Javadoc comments before every method.<br>