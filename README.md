# Easy Search Bar 2

A Flutter plugin to help you handle search inside your application. Can be used inside appBar or
inside your application body depending on your necessities.

## Preview

![Default AppBar Preview](https://raw.githubusercontent.com/4inka/flutter_easy_search_bar/main/preview/preview.gif)
![Floating AppBar Preview](https://raw.githubusercontent.com/4inka/flutter_easy_search_bar/main/preview/preview2.gif)

## Installation

In the `pubspec.yaml` of your flutter project, add the following dependency:

``` yaml
dependencies:
  easy_search_bar_2: ^1.0.0-alpha.0
```

## Migrating from `easy_search_bar` to `easy_search_bar_2`

Not a lot of changes are necessary, actually:

- Find and replace all occurrences of `easy_search_bar` -> `easy_search_bar_2`
- Find and replace all occurrences of `EasySearchBar` -> `EasySearchBar2`
- If wanted, migrate to the new generic setup (`EasySearchBar2` accepts a generic parameter and you
  might want to provide the named parameters `suggestionToString`)

## Basic example with suggestions

You can create a simple searchbar example widget with suggestions with the following example:

``` dart
import 'package:easy_search_bar/easy_search_bar.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyHomePage());
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  String searchValue = '';
  final List<String> _suggestions = ['Afeganistan', 'Albania', 'Algeria', 'Australia', 'Brazil', 'German', 'Madagascar', 'Mozambique', 'Portugal', 'Zambia'];

  @override
  Widget build(BuildContext context) {
    return  MaterialApp(
      title: 'Example',
      theme: ThemeData(
        primarySwatch: Colors.orange
      ),
      home: Scaffold(
        appBar: EasySearchBar(
          title: const Text('Example'),
          onSearch: (value) => setState(() => searchValue = value),
          suggestions: _suggestions
        ),
        drawer: Drawer(
          child: ListView(
            padding: EdgeInsets.zero,
            children: [
              const DrawerHeader(
                decoration: BoxDecoration(
                  color: Colors.blue,
                ),
                child: Text('Drawer Header'),
              ),
              ListTile(
                title: const Text('Item 1'),
                onTap: () => Navigator.pop(context)
              ),
              ListTile(
                title: const Text('Item 2'),
                onTap: () => Navigator.pop(context)
              )
            ]
          )
        ),
        body: Center(
          child: Text('Value: $searchValue')
        )
      )
    );
  }
}
```

**Note:** If you want to create a FloatingAppBar and want the body content to go behind the AppBar
you need to set `extendBodyBehindAppBar` Scaffold property to true. And it's also recommended to
wrap your Scaffold inside a SafeArea.

## API

| Attribute                 | Type                                          |      Required      | Description                                                                                                            | Default value               |
|:--------------------------|:----------------------------------------------|:------------------:|:-----------------------------------------------------------------------------------------------------------------------|:----------------------------|
| title                     | `Widget`                                      | :heavy_check_mark: | The title to be displayed inside AppBar                                                                                |                             |
| onSearch                  | `Function(String)`                            | :heavy_check_mark: | Returns the current search value.When search is closed, this method returns an empty value to clear the current search |                             |
| actions                   | `List<Widget>`                                |        :x:         | Extra custom actions that can be displayed inside AppBar                                                               |                             |
| leading                   | `Widget`                                      |        :x:         | Can be used to add leading icon to AppBar                                                                              |                             |
| backgroundColor           | `Color`                                       |        :x:         | Can be used to change AppBar background color                                                                          |                             |
| foregroundColor           | `Color`                                       |        :x:         | Can be used to change AppBar foreground color                                                                          |                             |
| elevation                 | `double`                                      |        :x:         | Can be used to change AppBar elevation                                                                                 | 5                           |
| iconTheme                 | `IconThemeData`                               |        :x:         | Can be used to set custom icon theme for AppBar icons                                                                  |                             |
| appBarHeight              | `double`                                      |        :x:         | Can be used to change AppBar height                                                                                    | 56                          |
| animationDuration         | `Duration`                                    |        :x:         | Can be used to set a duration for the AppBar search show and hide animation                                            | Duration(milliseconds: 450) |
| isFloating                | `bool`                                        |        :x:         | Can be used to determine if it will be a normal or floating AppBar                                                     | false                       |
| openOverlayOnSearch       | `bool`                                        |        :x:         | Can be used to determine if the suggestions overlay will be opened when clicking search                                | false                       |
| titleTextStyle            | `TextStyle`                                   |        :x:         | Can be used to set the AppBar title style                                                                              |                             |
| searchBackgroundColor     | `Color`                                       |        :x:         | Can be used to set the search input background color                                                                   |                             |
| searchCursorColor         | `Color`                                       |        :x:         | Can be used to set search textField cursor color                                                                       |                             |
| searchHintText            | `String`                                      |        :x:         | Can be used to set search textField hint text                                                                          |                             |
| searchHintStyle           | `TextStyle`                                   |        :x:         | Can be used to set search textField hint style                                                                         |                             |
| searchTextStyle           | `TextStyle`                                   |        :x:         | Can be used to set search textField text style                                                                         |                             |
| searchTextKeyboardType    | `KeyboardType`                                |        :x:         | Can be used to set search textField keyboard type                                                                      |                             |
| searchBackIconTheme       | `IconThemeData`                               |        :x:         | Can be used to set custom icon theme for the search textField back button                                              |                             |
| systemOverlayStyle        | `SystemUiOverlayStyle`                        |        :x:         | Can be used to set SystemUiOverlayStyle to the AppBar                                                                  |                             |
| suggestions               | `List<String>`                                |        :x:         | Can be used to create a suggestions list                                                                               |                             |
| asyncSuggestions          | `Future<List<String>> Function(String value)` |        :x:         | Can be used to set async suggestions list                                                                              |                             |
| suggestionsElevation      | `double`                                      |        :x:         | Can be used to change suggestion list elevation                                                                        | 5                           |
| suggestionLoaderBuilder   | `Widget Function()`                           |        :x:         | A function that can be used to create a widget to display a custom suggestions loader                                  |                             |
| suggestionTextStyle       | `TextStyle`                                   |        :x:         | Can be used to change the suggestions text style                                                                       |                             |
| suggestionBackgroundColor | `Color`                                       |        :x:         | Can be used to change suggestions list background color                                                                |                             |
| suggestionBuilder         | `Widget Function(String data)`                |        :x:         | Can be used to create custom suggestion item widget                                                                    |                             |
| onSuggestionTap           | `Function(String data)`                       |        :x:         | Instead of using the default suggestion tap action that fills the textField, you can set your own custom action for it |                             |
| debounceDuration          | `Duration`                                    |        :x:         | Can be used to set the debounce time for async data fetch                                                              | Duration(milliseconds: 400) |
| showClearSearchIcon       | `bool`                                        |        :x:         | Can be used to show search clear textField button                                                                      | false                       |
| searchClearIconTheme      | `IconThemeData`                               |        :x:         | Can be used to set custom icon theme for the search clear textField button                                             |                             |
| searchTextDirection       | `TextDirection`                               |        :x:         | Can be used to change text direction                                                                                   | TextDirection.ltr           |
| putActionsOnRight         | `bool`                                        |        :x:         | Can be used to determine if the actions button will be placed at right of the appbar                                   | false                       |
| cancelableSuggestions     | `bool`                                        |        :x:         | Can be used to allow the user to cancel the suggestions overlay by pressing escape or the back button on mobile        | false                       |

## Issues & Suggestions

If you encounter any issue you or want to leave a suggestion you can do it by filling
an [issue](https://github.com/ThexXTURBOXx/flutter_easy_search_bar_2/issues).

## Contributions

Here's the list of our awesome contributors:

- [Inka](https://github.com/4inka)
- [Seiji Tanaka](https://github.com/yameguun)
- [Victor Gabriel](https://github.com/vctrgbrl)
- [Ivan Terekhin](https://github.com/JEuler)
- [Dolev Franco](https://github.com/dtkdt100)
- [Nico Mexis](https://github.com/ThexXTURBOXx)

### Thank you for the support!
