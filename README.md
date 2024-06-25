🛒 Super Store Ecommerce App
Welcome to the Super Store Ecommerce App! This project showcases a comprehensive ecommerce
solution built with Flutter, leveraging Firebase for authentication, database, and other backend services.
🌟 Features
🛍️ Product Listings: Browse a variety of products with detailed descriptions and images.
🔍 Search: Easily find products with a powerful search functionality.
🛒 Shopping Cart: Add items to your cart and manage your selections.
💳 Checkout: Secure and straightforward checkout process.
🔐 User Authentication: Register, log in, and manage user profiles with Firebase Authentication.
📦 Order Management: Track and manage orders efficiently.
⭐ Reviews and Ratings: Rate products and read reviews from other customers.
🔔 Notifications: Stay updated with push notifications about orders and promotions.


🚀 Getting Started

Prerequisites
Before you begin, ensure you have the following:

Flutter SDK: Install Flutter
Firebase Project: Create a Firebase project
Firebase CLI: Install Firebase CLI
Clone the Repository:

git clone https://github.com/AMNAMAHAR
/
super_store_ecommerce_app.git
cd super_store_ecommerce_app

Add Firebase to Your Flutter App:
Follow the official Firebase documentation: Add Firebase to your Flutter app.

Add Dependencies:
Add the following dependencies in your pubspec.yaml file:

dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.0.0
  firebase_auth: ^4.0.0
  cloud_firestore: ^4.0.0
  provider: ^6.1.1
  url_launcher: ^6.2.4
  google_fonts: ^6.1.0
  http: ^1.2.0
  icons_plus: ^5.0.0
  fluttertoast: ^8.0.9
  cupertino_icons: ^1.0.3
Initialize Firebase:
Initialize Firebase in your main.dart file:


import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Super Store Ecommerce App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Super Store Ecommerce App'),
        ),
        body: Center(child: Text('Welcome to Super Store!')),
      ),
    );
  }
}
📚 Firebase Integration
Authentication:
Set up Firebase Authentication to enable user registration and login:

import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  final FirebaseAuth _auth = FirebaseAuth.instance;

  Future<User?> signInWithEmail(String email, String password) async {
    try {
      UserCredential result = await _auth.signInWithEmailAndPassword(email: email, password: password);
      return result.user;
    } catch (e) {
      print(e.toString());
      return null;
    }
  }

  Future<User?> registerWithEmail(String email, String password) async {
    try {
      UserCredential result = await _auth.createUserWithEmailAndPassword(email: email, password: password);
      return result.user;
    } catch (e) {
      print(e.toString());
      return null;
    }
  }

  Future<void> signOut() async {
    await _auth.signOut();
  }
}
Firestore:
Configure Firestore for storing product data, user profiles, and orders:

import 'package:cloud_firestore/cloud_firestore.dart';

class DatabaseService {
  final FirebaseFirestore _db = FirebaseFirestore.instance;

  Future<void> addProduct(Map<String, dynamic> productData) async {
    await _db.collection('products').add(productData);
  }

  Stream<QuerySnapshot> getProducts() {
    return _db.collection('products').snapshots();
  }

  Future<void> addOrder(Map<String, dynamic> orderData) async {
    await _db.collection('orders').add(orderData);
  }

  Stream<QuerySnapshot> getUserOrders(String userId) {
    return _db.collection('orders').where('userId', isEqualTo: userId).snapshots();
  }
}

⚙️ Firestore Rules
Ensure your Firestore rules are set up to allow the necessary read and write operations:

service cloud.firestore {
  match /databases/{database}/documents {
    match /products/{productId} {
      allow read, write: if request.auth != null;
    }
    match /orders/{orderId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
    }
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}

🎉 Running the App
Run the app using the following command:
flutter run
🤝 Contributing
Contributions are welcome! Please fork this repository and submit pull requests.

📝 License
This project is licensed under the MIT License - see the LICENSE file for details.


![Screenshot_20240624-110810](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/d5678b93-5c49-4137-97d8-1a4dd3da211c)

![Screenshot_20240624-110815](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/77602fd7-9e7e-453d-ad27-3f0eec6ddd3d)


![Screenshot_20240624-110823](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/d02f1a58-ea88-43c4-b18c-937d6dd2165f)


![Screenshot_20240624-111146](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/cdb08a08-95d9-4268-8615-02fa11e2a51b)

![Screenshot_20240624-111223](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/71738d32-1a06-4fbd-a484-17f9fd88c20f)

![Screenshot_20240624-111257](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/71950c2a-e303-4d26-acea-c47ee765793c)

![Screenshot_20240624-111324](https://github.com/AMNAMAHAR/super_store_ecommerce_app/assets/158574242/ff974da2-7f60-47fb-b41a-f9c3c57a48d1)














