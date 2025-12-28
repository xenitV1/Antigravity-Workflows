---
name: mobile
description: Cross-platform mobile development guide. 2025 best practices, performance optimization, and state management for React Native and Flutter.
metadata:
  skillport:
    category: development
    tags:
      - react-native
      - flutter
      - mobile
      - cross-platform
      - ios
      - android
---

# Mobile Development Skill

> Guide for developing modern, performant cross-platform mobile applications with React Native and Flutter.
> 2025 best practices and platform-specific optimizations.

---

# 📋 Contents

1. [Framework Selection](#1-framework-selection)
2. [React Native Best Practices](#2-react-native-best-practices)
3. [Flutter Best Practices](#3-flutter-best-practices)
4. [Mobile Security](#4-mobile-security)
5. [Platform-Specific Code](#5-platform-specific-code)
6. [Checklist](#6-checklist)
7. [Don't List](#7-dont-list)
8. [Must Do List](#8-must-do-list)

---

# 1. Framework Selection

| Criterion | React Native | Flutter |
|--------|--------------|---------|
| **Language** | TypeScript/JavaScript | Dart |
| **UI** | Native components | Custom rendering (Skia) |
| **Performance** | Very Good (Fabric) | Excellent (Impeller) |
| **Hot Reload** | ✅ | ✅ (Faster) |
| **Ecosystem** | npm (huge) | pub.dev (growing) |
| **Learning** | Easy if you know React | Learn new language |
| **Web support** | React Native Web | Flutter Web |

---

# 2. React Native Best Practices

## 2.1 Project Structure

```
src/
├── components/
│   ├── common/           # Reusable components
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.styles.ts
│   │   │   └── index.ts
│   │   └── Input/
│   ├── screens/          # Screen components
│   └── navigation/       # Navigation setup
├── hooks/                # Custom hooks
├── services/             # API, storage, etc.
├── store/                # State management
├── utils/                # Helper functions
├── constants/            # App constants
├── types/                # TypeScript types
└── App.tsx
```

## 2.2 Functional Components & Hooks

```typescript
// ✅ Modern functional component
import React, { useState, useCallback, useMemo } from 'react';
import { View, Text, TouchableOpacity, StyleSheet } from 'react-native';

interface UserCardProps {
  user: User;
  onPress: (id: string) => void;
}

export const UserCard: React.FC<UserCardProps> = React.memo(({ user, onPress }) => {
  const handlePress = useCallback(() => {
    onPress(user.id);
  }, [user.id, onPress]);

  const fullName = useMemo(() => 
    `${user.firstName} ${user.lastName}`,
    [user.firstName, user.lastName]
  );

  return (
    <TouchableOpacity onPress={handlePress} style={styles.card}>
      <Text style={styles.name}>{fullName}</Text>
      <Text style={styles.email}>{user.email}</Text>
    </TouchableOpacity>
  );
});

const styles = StyleSheet.create({
  card: {
    padding: 16,
    backgroundColor: '#fff',
    borderRadius: 8,
    marginBottom: 8,
  },
  name: {
    fontSize: 16,
    fontWeight: '600',
  },
  email: {
    fontSize: 14,
    color: '#666',
  },
});
```

## 2.3 Performance Optimization

```typescript
// ✅ FlatList optimization
import { FlatList } from 'react-native';

<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={(item) => item.id}
  // Performance props
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  windowSize={5}
  initialNumToRender={10}
  getItemLayout={(data, index) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  })}
/>

// ✅ Memoization
const renderItem = useCallback(({ item }: { item: ItemType }) => (
  <ItemComponent item={item} />
), []);

// ✅ useMemo for expensive calculations
const sortedItems = useMemo(() => 
  items.sort((a, b) => b.date - a.date),
  [items]
);
```

## 2.4 State Management (Zustand)

```typescript
// store/useAuthStore.ts
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';
import AsyncStorage from '@react-native-async-storage/async-storage';

interface AuthState {
  user: User | null;
  token: string | null;
  isAuthenticated: boolean;
  login: (user: User, token: string) => void;
  logout: () => void;
}

export const useAuthStore = create<AuthState>()(
  persist(
    (set) => ({
      user: null,
      token: null,
      isAuthenticated: false,
      login: (user, token) => set({ user, token, isAuthenticated: true }),
      logout: () => set({ user: null, token: null, isAuthenticated: false }),
    }),
    {
      name: 'auth-storage',
      storage: createJSONStorage(() => AsyncStorage),
    }
  )
);

// Usage
const { user, login, logout } = useAuthStore();
```

## 2.5 Secure Storage

```typescript
// ❌ INCORRECT - AsyncStorage is not secure
await AsyncStorage.setItem('token', userToken);

// ✅ CORRECT - Use SecureStore
import * as SecureStore from 'expo-secure-store';

await SecureStore.setItemAsync('token', userToken);
const token = await SecureStore.getItemAsync('token');
await SecureStore.deleteItemAsync('token');
```

## 2.6 Navigation (React Navigation)

```typescript
// navigation/types.ts
export type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
  Settings: undefined;
};

// navigation/RootNavigator.tsx
import { createNativeStackNavigator } from '@react-navigation/native-stack';

const Stack = createNativeStackNavigator<RootStackParamList>();

export function RootNavigator() {
  const { isAuthenticated } = useAuthStore();

  return (
    <Stack.Navigator>
      {isAuthenticated ? (
        <>
          <Stack.Screen name="Home" component={HomeScreen} />
          <Stack.Screen name="Profile" component={ProfileScreen} />
        </>
      ) : (
        <Stack.Screen name="Login" component={LoginScreen} />
      )}
    </Stack.Navigator>
  );
}
```

---

# 3. Flutter Best Practices

## 3.1 Project Structure (Feature-First)

```
lib/
├── core/
│   ├── constants/
│   ├── theme/
│   ├── utils/
│   └── widgets/          # Shared widgets
├── features/
│   ├── auth/
│   │   ├── data/
│   │   │   ├── models/
│   │   │   ├── repositories/
│   │   │   └── datasources/
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   └── usecases/
│   │   └── presentation/
│   │       ├── screens/
│   │       ├── widgets/
│   │       └── providers/
│   └── home/
├── services/
└── main.dart
```

## 3.2 Widget Best Practices

```dart
// ✅ Use const constructor
class MyButton extends StatelessWidget {
  const MyButton({
    super.key,
    required this.onPressed,
    required this.label,
  });

  final VoidCallback onPressed;
  final String label;

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: Text(label),
    );
  }
}

// ✅ Break down into smaller widgets
class UserProfile extends StatelessWidget {
  const UserProfile({super.key, required this.user});
  final User user;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        _UserAvatar(user: user),      // Separate widget
        _UserInfo(user: user),        // Separate widget
        _UserActions(user: user),     // Separate widget
      ],
    );
  }
}
```

## 3.3 State Management (Riverpod)

```dart
// providers/auth_provider.dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// State class
class AuthState {
  final User? user;
  final bool isLoading;
  final String? error;

  const AuthState({this.user, this.isLoading = false, this.error});

  AuthState copyWith({User? user, bool? isLoading, String? error}) {
    return AuthState(
      user: user ?? this.user,
      isLoading: isLoading ?? this.isLoading,
      error: error,
    );
  }
}

// Notifier
class AuthNotifier extends StateNotifier<AuthState> {
  AuthNotifier(this._authRepository) : super(const AuthState());

  final AuthRepository _authRepository;

  Future<void> login(String email, String password) async {
    state = state.copyWith(isLoading: true, error: null);
    try {
      final user = await _authRepository.login(email, password);
      state = state.copyWith(user: user, isLoading: false);
    } catch (e) {
      state = state.copyWith(error: e.toString(), isLoading: false);
    }
  }

  void logout() {
    state = const AuthState();
  }
}

// Provider
final authProvider = StateNotifierProvider<AuthNotifier, AuthState>((ref) {
  return AuthNotifier(ref.watch(authRepositoryProvider));
});

// Usage
class LoginScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final authState = ref.watch(authProvider);
    
    return authState.isLoading
      ? const CircularProgressIndicator()
      : LoginForm(onSubmit: (email, password) {
          ref.read(authProvider.notifier).login(email, password);
        });
  }
}
```

## 3.4 Performance Optimization

```dart
// ✅ Use ListView.builder (lazy loading)
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ItemCard(item: items[index]);
  },
)

// ✅ Mark const widgets
const SizedBox(height: 16),
const Divider(),

// ✅ Isolate rebuilds with RepaintBoundary
RepaintBoundary(
  child: ExpensiveWidget(),
)

// ✅ Use Isolate for CPU-heavy tasks
Future<List<User>> parseUsers(String jsonString) async {
  return compute(_parseUsers, jsonString);
}

List<User> _parseUsers(String jsonString) {
  final json = jsonDecode(jsonString) as List;
  return json.map((e) => User.fromJson(e)).toList();
}
```

## 3.5 Responsive Design

```dart
// ✅ Use MediaQuery
class ResponsiveLayout extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final size = MediaQuery.of(context).size;
    final isTablet = size.width > 600;

    return isTablet
      ? TabletLayout()
      : MobileLayout();
  }
}

// ✅ LayoutBuilder for constraint-based
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return WideLayout();
    }
    return NarrowLayout();
  },
)

// ✅ FittedBox for scaling
FittedBox(
  fit: BoxFit.scaleDown,
  child: Text('Long text that should scale'),
)
```

---

# 4. Mobile Security

## 4.1 Secure Data Storage

```typescript
// React Native - Encrypted storage
import EncryptedStorage from 'react-native-encrypted-storage';

await EncryptedStorage.setItem('user_session', JSON.stringify(session));
const session = await EncryptedStorage.getItem('user_session');
```

```dart
// Flutter - flutter_secure_storage
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

final storage = FlutterSecureStorage();
await storage.write(key: 'token', value: token);
final token = await storage.read(key: 'token');
```

## 4.2 API Security

```typescript
// ✅ Certificate pinning
import { fetch } from 'react-native-ssl-pinning';

const response = await fetch(url, {
  method: 'GET',
  sslPinning: {
    certs: ['cert1', 'cert2'],
  },
});
```

## 4.3 Code Obfuscation

```bash
# React Native (Hermes + ProGuard)
# android/app/proguard-rules.pro
-keep class com.yourapp.** { *; }
-keepattributes *Annotation*

# Flutter
flutter build apk --obfuscate --split-debug-info=./debug-info
```

---

# 5. Platform-Specific Code

## 5.1 React Native

```typescript
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    paddingTop: Platform.select({
      ios: 20,
      android: 0,
    }),
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.25,
      },
      android: {
        elevation: 4,
      },
    }),
  },
});

// Platform-specific file
// Button.ios.tsx
// Button.android.tsx
```

## 5.2 Flutter

```dart
import 'dart:io' show Platform;

if (Platform.isIOS) {
  // iOS specific code
} else if (Platform.isAndroid) {
  // Android specific code
}

// Platform-specific widgets
Platform.isIOS
  ? CupertinoButton(child: Text('iOS'), onPressed: () {})
  : ElevatedButton(child: Text('Android'), onPressed: () {})
```

---

# 6. Checklist

In every mobile project:

- [ ] TypeScript/Dart strict mode active
- [ ] Folder structure organized
- [ ] State management implemented
- [ ] Navigation configured
- [ ] Secure storage used
- [ ] API calls with error handling
- [ ] Loading states present
- [ ] Empty states present
- [ ] Error states present
- [ ] Offline support considered
- [ ] Performance profiling performed
- [ ] Platform-specific optimizations applied

---

# 7. Don't List

❌ Do not keep sensitive data in AsyncStorage
❌ Do not use inline styles (use StyleSheet)
❌ Do not use anonymous functions in render
❌ Do not use large images without optimizing
❌ Do not leave console.log in production
❌ Do not mutate state directly
❌ Do not skip cleanup in useEffect
❌ Do not use ScrollView instead of FlatList for large lists

---

# 8. Must Do List

✅ Use React.memo / const widgets
✅ Memoization with useCallback/useMemo
✅ Lazy loading with FlatList/ListView.builder
✅ Store tokens with secure storage
✅ Implement error boundaries
✅ Loading/Error/Empty states
✅ Platform-specific UX
✅ Accessibility labels
✅ Deep linking support
✅ Push notification handling

---

**Last Update:** December 2025
**Version:** 2.0
