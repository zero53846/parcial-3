# parcial-3
proyecto flutter
# Parcial App


# chat - Proyecto Flutter
# Estructura del proyecto

```text
lib/
│
├── data/
│   ├── models/
│   │   └── product_model.dart
│   │
│   └── services/
│       └── api_service.dart
│
├── domain/
│   └── entities/
│       └── product_entity.dart
│
├── presentation/
│   ├── providers/
│   │   └── message_provider.dart
│   │
│   └── screens/
│       └── home_screen.dart
│
└── main.dart
```

---

# Dependencias

```yaml
dependencies:
  flutter:
    sdk: flutter

  provider: ^6.1.2
  http: ^1.2.1
```

---

# Código principal

## main.dart

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(const TecnarMessenger());
}

class TecnarMessenger extends StatelessWidget {
  const TecnarMessenger({super.key});

  @override
  Widget build(BuildContext context) {

    return MultiProvider(
      providers: [],

      child: MaterialApp(
        debugShowCheckedModeBanner: false,

        title: 'Tecnar Messenger',

        theme: ThemeData.dark(),

        home: const HomeScreen(),
      ),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {

    return Scaffold(

      appBar: AppBar(
        title: const Text('Tecnar Messenger'),
        centerTitle: true,
      ),

      body: ListView(
        children: const [

          ListTile(
            leading: CircleAvatar(
              child: Icon(Icons.person),
            ),

            title: Text('Producto encontrado'),

            subtitle: Text('Información obtenida desde internet'),
          ),

          ListTile(
            leading: CircleAvatar(
              child: Icon(Icons.shopping_bag),
            ),

            title: Text('FakeStoreAPI'),

            subtitle: Text('Consumo de API REST exitoso'),
          ),

          ListTile(
            leading: CircleAvatar(
              child: Icon(Icons.code),
            ),

            title: Text('Flutter Provider'),

            subtitle: Text('Arquitectura DDD implementada'),
          ),

          ListTile(
            leading: CircleAvatar(
              child: Icon(Icons.message),
            ),

            title: Text('Sistema de mensajería'),

            subtitle: Text('Interfaz estilo chat'),
          ),
        ],
      ),
    );
  }
}
```

---

# Entidad principal

## product_entity.dart

```dart
class ProductEntity {

  final String title;
  final String image;

  ProductEntity({
    required this.title,
    required this.image,
  });
}
```

---

# Modelo de datos

## product_model.dart

```dart
import '../../domain/entities/product_entity.dart';

class ProductModel extends ProductEntity {

  ProductModel({
    required super.title,
    required super.image,
  });

  factory ProductModel.fromJson(Map<String, dynamic> json) {

    return ProductModel(
      title: json['title'],
      image: json['image'],
    );
  }
}
```

---

# Servicio API

## api_service.dart

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

import '../models/product_model.dart';

class ApiService {

  Future<List<ProductModel>> getProducts() async {

    final response = await http.get(
      Uri.parse('https://fakestoreapi.com/products'),
    );

    final data = jsonDecode(response.body);

    return List<ProductModel>.from(
      data.map((item) => ProductModel.fromJson(item)),
    );
  }
}
```

---

# Provider

## message_provider.dart

```dart
import 'package:flutter/material.dart';

class MessageProvider extends ChangeNotifier {

  List<String> messages = [];

  void addMessage(String text) {

    messages.add(text);

    notifyListeners();
  }
}
```

---

# API utilizada

https://fakestoreapi.com/products

---


# Ejecución del proyecto

```bash
flutter pub get
flutter run
```

---



#MIGUEL MORON
