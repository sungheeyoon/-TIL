# Your first Flutter app

- 작성일: 2024-01-10
- 참조: [codelab - Your first Flutter app](https://codelabs.developers.google.com/codelabs/flutter-codelab-first#0)

## Flutter 소개

Flutter는 Google에서 개발한 오픈 소스 UI 소프트웨어 개발 키트로, 모바일 앱, 웹 앱, 데스크톱 앱 등을 개발하기 위한 도구이다.

## Flutter 개발 환경 설정

Flutter를 사용하기 위해선 Flutter SDK와 Dart SDK를 설치 및 Visual Studio Code와 Android Studio 등의 IDE를 활용하여 개발할 수 있다.

## 프로젝트 생성

Visual Studio Code를 실행하고 명령 팔레트를 열고 Flutter: New Project 명령을 선택한다.

```dart
// main.dart

import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => MyAppState(), // MyAppState를 관리하는 ChangeNotifierProvider
      child: MaterialApp(
        title: 'Namer App',
        theme: ThemeData(
          useMaterial3: true,
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepOrange),
        ),
        home: MyHomePage(),
      ),
    );
  }
}

class MyAppState extends ChangeNotifier {
  var current = WordPair.random();
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var appState = context.watch<MyAppState>();

    return Scaffold(
      body: Column(
        children: [
          Text('A random idea:'),
          Text(appState.current.asLowerCase),
        ],
      ),
    );
  }
}
```

colorScheme 변경에따라 색상변경, ChangeNotifier로 앱 상태관리를 예시로 들고있다.

## pubspec . yaml

`pubspec.yaml` 파일은 현재 버전, 종속성, 함께 제공될 자산 등 앱에 대한 기본 정보를 지정한다.

```
name: namer_app
description: A new Flutter project.

publish_to: 'none' # Remove this line if you wish to publish to pub.dev

version: 0.0.1+1

environment:
  sdk: '>=2.19.4 <4.0.0'

dependencies:
  flutter:
    sdk: flutter

  english_words: ^4.0.0
  provider: ^6.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter

  flutter_lints: ^2.0.0

flutter:
  uses-material-design: true
```

## Widget 개념 이해

Flutter에서는 모든 것이 Widget으로 이루어져 있다. `StatelessWidget`과 `StatefulWidget`을 통해 UI를 구성하고, 위젯 트리를 이해하는 것이 중요하다.

## Hot Reload

Flutter의 Hot Reload를 사용하여 코드를 수정하고 즉시 결과를 확인한다. 이 기능은 앱을 실행 중에도 소스 코드를 수정하고, 앱을 중단시키지 않고도 수정 사항을 즉시 적용할 수 있게 해준다.

참조: [Flutter Hot Reload 문서](https://flutter.dev/docs/development/tools/hot-reload)
