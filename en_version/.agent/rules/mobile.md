# Mobile Development Rule

## Activation
- **Mode:** Glob
- **Glob Pattern:** `*.tsx, App.*, screens/**, ios/**, android/**, lib/**`
- **Description:** Cross-platform mobile development guide for React Native and Flutter. Best practices for performance, state management, and platform-specific optimization.

---

## Framework Selection

| Criteria | React Native | Flutter |
|----------|--------------|---------|
| Language | TypeScript/JS | Dart |
| UI | Native components | Custom (Skia) |
| Performance | Excellent (Fabric) | Superior (Impeller) |
| Ecosystem | npm (massive) | pub.dev (growing) |
| Learning | Easy if React known | New language |

---

## React Native Best Practices

### Project Structure
```
src/
├── components/
│   ├── common/        # Reusable
│   └── screens/       # Screen components
├── hooks/             # Custom hooks
├── services/          # API, storage
├── store/             # State management
├── utils/             # Helpers
├── constants/
├── types/
└── App.tsx
```

### Functional Components
```typescript
export const UserCard: React.FC<Props> = React.memo(({ user, onPress }) => {
  const handlePress = useCallback(() => {
    onPress(user.id);
  }, [user.id, onPress]);

  return (
    <TouchableOpacity onPress={handlePress}>
      <Text>{user.name}</Text>
    </TouchableOpacity>
  );
});
```

### FlatList Optimization
```typescript
<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={(item) => item.id}
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  windowSize={5}
  getItemLayout={(data, index) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  })}
/>
```

---

## Flutter Best Practices

### Project Structure (Feature-First)
```
lib/
├── core/
│   ├── constants/
│   ├── theme/
│   └── widgets/
├── features/
│   └── auth/
│       ├── data/
│       ├── domain/
│       └── presentation/
└── main.dart
```

### Widget Best Practices
```dart
class MyButton extends StatelessWidget {
  const MyButton({super.key, required this.onPressed, required this.label});

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

### Performance
```dart
// Use ListView.builder (lazy loading)
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) => ItemCard(item: items[index]),
)

// Use const widgets
const SizedBox(height: 16),

// Use RepaintBoundary
RepaintBoundary(child: ExpensiveWidget())
```

---

## State Management

### React Native (Zustand)
```typescript
export const useAuthStore = create<AuthState>()(
  persist(
    (set) => ({
      user: null,
      login: (user, token) => set({ user, isAuthenticated: true }),
      logout: () => set({ user: null, isAuthenticated: false }),
    }),
    { name: 'auth-storage', storage: createJSONStorage(() => AsyncStorage) }
  )
);
```

### Flutter (Riverpod)
```dart
final authProvider = StateNotifierProvider<AuthNotifier, AuthState>((ref) {
  return AuthNotifier(ref.watch(authRepositoryProvider));
});
```

---

## Security

### Secure Storage
```typescript
// React Native - Use SecureStore, NOT AsyncStorage
import * as SecureStore from 'expo-secure-store';
await SecureStore.setItemAsync('token', userToken);
```

```dart
// Flutter - flutter_secure_storage
final storage = FlutterSecureStorage();
await storage.write(key: 'token', value: token);
```

### API Security
- Certificate pinning
- Code obfuscation
- No hardcoded secrets

---

## Platform-Specific Code

### React Native
```typescript
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: { shadowColor: '#000', shadowOpacity: 0.25 },
      android: { elevation: 4 },
    }),
  },
});
```

### Flutter
```dart
import 'dart:io' show Platform;

Platform.isIOS ? CupertinoButton(...) : ElevatedButton(...)
```

---

## Checklist

- [ ] TypeScript/Dart strict mode active
- [ ] Folder structure organized
- [ ] State management implemented
- [ ] Navigation configured
- [ ] Secure storage used
- [ ] Error handling present
- [ ] Loading/Empty/Error states
- [ ] Offline support considered
- [ ] Performance profiled
- [ ] Platform-specific optimizations

---

## Don't List

- Store sensitive data in AsyncStorage
- Use inline styles
- Anonymous functions in render
- Large images without optimization
- console.log in production
- Mutate state directly
- Skip useEffect cleanup
- Use ScrollView for large lists

---

## Must Do List

- React.memo / const widgets
- useCallback/useMemo memoization
- FlatList/ListView.builder for lists
- Secure storage for tokens
- Error boundaries
- Platform-specific UX
- Accessibility labels
- Deep linking support
- Push notification handling

---

**Version:** 2.0 (Antigravity Rule)
