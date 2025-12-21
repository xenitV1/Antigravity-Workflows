---
name: mobile
description: Cross-platform mobile development guide. 2025 best practices for React Native and Flutter, performance optimization, and state management.
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
> Compliant with 2025 best practices and platform-specific optimizations.

---

## 🎯 Framework Selection

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

## 📱 React Native Best Practices

### Project Structure

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
```

### State Management (Zustand)

```typescript
// store/useAuthStore.ts
import { create } from 'zustand';
import { persist, createJSONStorage } from 'zustand/middleware';
import AsyncStorage from '@react-native-async-storage/async-storage';

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
```

### Secure Storage

```typescript
// ❌ INCORRECT - AsyncStorage is not secure
await AsyncStorage.setItem('token', userToken);

// ✅ CORRECT - Use SecureStore
import * as SecureStore from 'expo-secure-store';

await SecureStore.setItemAsync('token', userToken);
const token = await SecureStore.getItemAsync('token');
```

---

## 🐦 Flutter Best Practices

### Project Structure (Feature-First)

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
│   │   ├── domain/
│   │   └── presentation/
│   └── home/
├── services/
└── main.dart
```

### Widget Best Practices

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
```

### Performance Optimization

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
```

### Responsive Design

```dart
// ✅ Use MediaQuery
final size = MediaQuery.of(context).size;
final isTablet = size.width > 600;

// ✅ LayoutBuilder for constraint-based
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return WideLayout();
    }
    return NarrowLayout();
  },
)
```

---

## 🔒 Mobile Security

### Secure Data Storage

```typescript
// React Native - Encrypted storage
import EncryptedStorage from 'react-native-encrypted-storage';

await EncryptedStorage.setItem('user_session', JSON.stringify(session));
```

```dart
// Flutter - flutter_secure_storage
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

final storage = FlutterSecureStorage();
await storage.write(key: 'token', value: token);
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
  },
});
```

### Flutter

```dart
import 'dart:io' show Platform;

if (Platform.isIOS) {
  // iOS specific code
} else if (Platform.isAndroid) {
  // Android specific code
}
```

---

## ✅ Checklist

In every mobile project:

- [ ] TypeScript/Dart strict mode active
- [ ] Folder structure organized
- [ ] State management implemented
- [ ] Navigation configured
- [ ] Secure storage used
- [ ] API calls with error handling
- [ ] Loading, Empty, and Error states present
- [ ] Offline support considered
- [ ] Performance profiling performed
- [ ] Platform-specific optimizations applied

---

## 🔴 Don't List

❌ Do not keep sensitive data in AsyncStorage
❌ Do not use inline styles (use StyleSheet)
❌ Do not use anonymous functions in render
❌ Do not use large images without optimizing
❌ Do not leave console.log in production
❌ Do not mutate state directly
❌ Do not skip cleanup in useEffect
❌ Do not use ScrollView instead of FlatList for large lists

---

## ✅ Must Do List

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
**Version:** 1.0
