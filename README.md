# Renga.Wpf.Styles
[ENG](#eng), [RUS](#rus)


<a name="eng"></a>Renga.Wpf.Styles is a simple WPF library for styling your application
or plugin in Renga style.

The library includes styles for the classes:
- Window (there is an extended DialogWindow style for styling the dialog box)
- ListBox
- Button
- GroupBox
- CheckBox
- RadioButton
- TextBox
- ComboBox

## Usage
- Add a reference to Renga.WPF.Styles.dll to your project
- Add a dictionary with WPF resources that references the style library resources (examples below). After that, the styles will be automatically applied to all controls (TextBox, Button, etc).
- Set a style for each window, e.g. ```Style="{DynamicResource Renga.WPF.Style.DialogWindow}"```

### Adding a dictionary

To add a resource dictionary to your application, in the App.xaml file, add:

```
<Application.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/Renga.WPF.Styles;component/Themes/Renga.Implicit.xaml"/>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Application.Resources>
```

If you are writing a plugin and do not have an App.xaml file, you can add a similar
block to your window's xaml:

```
<Window.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/Renga.WPF.Styles;component/Themes/Renga.Implicit.xaml"/>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Window.Resources>
```

### Features of styling plugin windows

When styling a plugin window there may be a problem accessing the style library.
This is due to the fact that the assembly resolving occurs in the application folder,
i.e. Renga, not in the plugin folder. In order to load dependencies from the plugin folder,
use the ```AssemblyResolve``` event. For example, you can add the following code to the implementation of the
```IPlugin::Initialize``` method:

```
AppDomain.CurrentDomain.AssemblyResolve += (sender, e) =>
{
  var missingName = new AssemblyName(e.Name);
  var missingPath = Path.Combine(plugInFolder, missingName.Name + ".dll");

  if (File.Exists(missingPath))
    return Assembly.LoadFrom(missingPath);
  else
    return null;
};
```

## Authors:
- [@vinesworth](https://github.com/vinesworth)


<a name="rus"></a>
# Renga.Wpf.Styles

Renga.Wpf.Styles - это простая WPF библиотека для стилизации вашего приложения 
или плагина в стиле Renga.

Библиотека включает в себя стили для классов:
- Window (есть расширенный стиль DialogWindow для стилизации диалогового окна)
- ListBox
- Button
- GroupBox
- CheckBox
- RadioButton
- TextBox
- ComboBox

## Использование
- Добавьте в проект ссылку на Renga.WPF.Styles.dll
- Добавьте словарь с WPF ресурсами, который ссылается на ресурсы библиотеки стилей (примеры ниже). После этого стили автоматически применятся для всех контролов (TextBox, Button, etc).
- Задайте стиль для каждого окна, e.g. ```Style="{DynamicResource Renga.WPF.Style.DialogWindow}"```


### Добавление словаря

Для добавления словаря ресурсов в приложение в файле App.xaml добавьте:

```
<Application.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/Renga.WPF.Styles;component/Themes/Renga.Implicit.xaml"/>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Application.Resources>
```

В случае, если вы пишете плагин и у вас нет файла App.xaml вы можете добавить аналогичный
блок в xaml вашего окна:

```
<Window.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/Renga.WPF.Styles;component/Themes/Renga.Implicit.xaml"/>
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Window.Resources>
```

### Особенности стилизации окон плагинов

При стилизации окна плагина может возникнуть проблема обращения к библиотеке стилей.
Это связанно с тем, что поиск сборки библиотеки стилей происходит в расположении запущенного приложения, 
т.е. Renga, а не в расположении плагина. Для того, чтобы загрузить зависимости из папки плагина
воспользуйтесь событием ```AssemblyResolve```. Например, вы можете добавить следующий код в реализацию 
метода ```IPlugin::Initialize```:

```

AppDomain.CurrentDomain.AssemblyResolve += (sender, e) =>
{
  var missingName = new AssemblyName(e.Name);
  var missingPath = Path.Combine(plugInFolder, missingName.Name + ".dll");

  if (File.Exists(missingPath))
    return Assembly.LoadFrom(missingPath);
  else
    return null;
};
```

## Авторы:
- [@vinesworth](https://github.com/vinesworth)