---
name: mobile
description: Cross-platform mobile geliştirme rehberi. React Native ve Flutter için 2025 best practices, performans optimizasyonu ve state management.
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

> React Native ve Flutter ile modern, performanslı cross-platform mobile uygulama geliştirme rehberi.
> 2025 best practices ve platform-specific optimizasyonlar.

---

## 🎯 Framework Seçimi

| Kriter | React Native | Flutter |
|--------|--------------|---------|
| **Dil** | TypeScript/JavaScript | Dart |
| **UI** | Native components | Custom rendering (Skia) |
| **Performans** | Çok iyi (Fabric) | Mükemmel (Impeller) |
| **Hot Reload** | ✅ | ✅ (Daha hızlı) |
| **Ekosistem** | npm (devasa) | pub.dev (büyüyen) |
| **Öğrenme** | React biliyorsan kolay | Yeni dil öğrenme |
| **Web desteği** | React Native Web | Flutter Web |

---

## 📱 React Native Best Practices

### Proje Yapısı

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

### Functional Components & Hooks

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

### Performance Optimization

```typescript
// ✅ FlatList optimizasyonu
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

### State Management (Zustand)

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

// Kullanım
const { user, login, logout } = useAuthStore();
```

### Secure Storage

```typescript
// ❌ YANLIŞ - AsyncStorage güvenli değil
await AsyncStorage.setItem('token', userToken);

// ✅ DOĞRU - SecureStore kullan
import * as SecureStore from 'expo-secure-store';

await SecureStore.setItemAsync('token', userToken);
const token = await SecureStore.getItemAsync('token');
await SecureStore.deleteItemAsync('token');
```

### Navigation (React Navigation)

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

## 🐦 Flutter Best Practices

### Proje Yapısı (Feature-First)

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

### Widget Best Practices

```dart
// ✅ const constructor kullan
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

// ✅ Küçük widget'lara böl
class UserProfile extends StatelessWidget {
  const UserProfile({super.key, required this.user});
  final User user;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        _UserAvatar(user: user),      // Ayrı widget
        _UserInfo(user: user),        // Ayrı widget
        _UserActions(user: user),     // Ayrı widget
      ],
    );
  }
}
```

### State Management (Riverpod)

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

// Kullanım
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

### Performance Optimization

```dart
// ✅ ListView.builder kullan (lazy loading)
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ItemCard(item: items[index]);
  },
)

// ✅ const widget'ları işaretle
const SizedBox(height: 16),
const Divider(),

// ✅ RepaintBoundary ile rebuild izole et
RepaintBoundary(
  child: ExpensiveWidget(),
)

// ✅ Isolate ile CPU-heavy işlemler
Future<List<User>> parseUsers(String jsonString) async {
  return compute(_parseUsers, jsonString);
}

List<User> _parseUsers(String jsonString) {
  final json = jsonDecode(jsonString) as List;
  return json.map((e) => User.fromJson(e)).toList();
}
```

### Responsive Design

```dart
// ✅ MediaQuery kullan
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

// ✅ LayoutBuilder ile constraint-based
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return WideLayout();
    }
    return NarrowLayout();
  },
)

// ✅ FittedBox ile scaling
FittedBox(
  fit: BoxFit.scaleDown,
  child: Text('Long text that should scale'),
)
```

---

## 🔒 Mobile Security

### Secure Data Storage

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

### API Security

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

### Code Obfuscation

```bash
# React Native (Hermes + ProGuard)
# android/app/proguard-rules.pro
-keep class com.yourapp.** { *; }
-keepattributes *Annotation*

# Flutter
flutter build apk --obfuscate --split-debug-info=./debug-info
```

---

## 📱 Platform-Specific Code

### React Native

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

### Flutter

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

## ✅ Kontrol Listesi

Her mobile projede:

- [ ] TypeScript/Dart strict mode aktif
- [ ] Folder structure organize
- [ ] State management implement edildi
- [ ] Navigation yapılandırıldı
- [ ] Secure storage kullanılıyor
- [ ] API calls error handling ile
- [ ] Loading states var
- [ ] Empty states var
- [ ] Error states var
- [ ] Offline support düşünüldü
- [ ] Performance profiling yapıldı
- [ ] Platform-specific optimizasyonlar

---

## 🔴 Yapma Listesi

❌ AsyncStorage'da hassas veri tutma
❌ Inline styles (StyleSheet kullan)
❌ Anonymous functions in render
❌ Large images optimize etmeden kullanma
❌ Console.log production'da bırakma
❌ State'i doğrudan mutate etme
❌ useEffect'te cleanup yapmamak
❌ FlatList yerine ScrollView (büyük listeler için)

---

## ✅ Mutlaka Yap Listesi

✅ React.memo / const widgets kullan
✅ useCallback/useMemo ile memoization
✅ FlatList/ListView.builder ile lazy loading
✅ Secure storage ile token saklama
✅ Error boundaries implement et
✅ Loading/Error/Empty states
✅ Platform-specific UX
✅ Accessibility labels
✅ Deep linking support
✅ Push notification handling

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 1.0
