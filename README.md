# Spigot-CustomConfig
[![License](https://img.shields.io/badge/license-GPLv3-blue?style=flat-square)](https://www.gnu.org/licenses/gpl-3.0.html) [![Pull Requests](https://img.shields.io/github/issues-pr-closed/katorlys/Spigot-CustomConfig?style=flat-square)](https://github.com/katorlys/Spigot-CustomConfig/pulls) [![Issues](https://img.shields.io/github/issues-closed/katorlys/Spigot-CustomConfig?style=flat-square)](https://github.com/katorlys/Spigot-CustomConfig/issues) [![Lines](https://img.shields.io/tokei/lines/github/katorlys/Spigot-CustomConfig?style=flat-square)](https://github.com/katorlys/Spigot-CustomConfig)

## Introduction
Bukkit API only allows you to create one config for each plugins, and there is no sign that it will change the situation in the future versions.  
Now this piece of code allows you to create custom configs in Bukkit/Spigot plugins, and you can set where the config should be saved.  
What's more, the code extends `org.bukkit.configuration.file.YamlConfiguration` so that you can use methods such as `getConfig()` and `saveConfig()` as usual.  

~~However, I didn't rewrite method `reloadConfig()` so it will remove all the comments as Bukkit API does. Maybe I'll rewrite it next time.🤣~~  
Starting from Minecraft 1.19, `reloadConfig()` will not remove all comments.  

## Usage
### Create Config
For example, I would like to create a custom YML config named "AConfig" for MyPlugin in "plugins/MyPlugin/settings/".  
First, register the config in the main class:  
```java
public class MyPlugin extends JavaPlugin {
    public static ConfigReader AConfig;
}
```
Second, load the config on plugin enable:  
```java
public void onEnable() {
    AConfig = new ConfigReader(this,"settings/","AConfig.yml");
	AConfig.saveDefaultConfig();
}
```
After all that work, you can use all methods in the rest of the plugin.  
Here is some examples:  
```java
FileConfiguration aconfig = AConfig.getConfig();
List<String> value1 = aconfig.getStringList("First-List");
aconfig.set("First-object","element");
aconfig.reloadConfig();
aconfig.saveConfig();
```
There are also Javadoc comments before every method.  

### Save Config
Combining `saveConfig()` with `reloadConfig()`, this can be used on plugin disable and after setting some keys in a config.  
```java
ConfigReader.save(this.AConfig);
```
