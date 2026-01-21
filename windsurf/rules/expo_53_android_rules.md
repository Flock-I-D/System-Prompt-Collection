---
trigger: always_on
---

# 📱 Expo 53 + Android Rules

## Safe Areas & Layout
- Usar `<SafeAreaView>` o `<SafeAreaProvider>` para evitar superposiciones con notches o status bar.
- Formularios con `<KeyboardAvoidingView>` y `behavior` correcto para Android/iOS.
- Scrolls con `flexGrow: 1` para que llenen bien la pantalla.

## Touch & UX Android
- Siempre usar `TouchableRipple`, `Button` o `Pressable` con `android_ripple`.
- Manejar el botón físico back con `BackHandler` donde haga falta.

## StatusBar y orientación
- Configurar explícitamente `StatusBar` con `expo-status-bar`.
- Bloquear orientación a `portrait` con `expo-screen-orientation`.

## Theme spacing
- Extender el theme para incluir:

```tsx
export const theme = {
  ...DefaultTheme,
  spacing: (factor) => factor * 8
};
```

Y usar siempre `theme.spacing(n)`.

## Permisos
- Pedir permisos en runtime (no solo en `app.json`). Ej: cámara, ubicación.

## Ejemplo mínimo

```tsx
import { SafeAreaView } from 'react-native-safe-area-context';
import { KeyboardAvoidingView, ScrollView, Platform } from 'react-native';
import { StatusBar } from 'expo-status-bar';
import { Button, Text, useTheme } from 'react-native-paper';

export default function Example() {
  const theme = useTheme();

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <StatusBar style="dark" backgroundColor="#fff" />
      <KeyboardAvoidingView style={{ flex: 1 }} behavior={Platform.OS === 'ios' ? 'padding' : 'height'}>
        <ScrollView contentContainerStyle={{ flexGrow: 1, justifyContent: 'center', padding: theme.spacing(2) }}>
          <Text variant="titleLarge">Hola</Text>
          <Button mode="contained">Presioname</Button>
        </ScrollView>
      </KeyboardAvoidingView>
    </SafeAreaView>
  );
}
```

