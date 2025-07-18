# 🚀 awesome_shake_widget

A customizable Flutter widget that adds shake animations with haptic and vibration feedback. Perfect for invalid forms, error indicators, or drawing attention to UI components.

![Pub Version](https://img.shields.io/pub/v/awesome_shake_widget.svg)
![Platform](https://img.shields.io/badge/platform-flutter-blue)
![License](https://img.shields.io/github/license/juanmadelboca/awesome_shake_widget)

---

## ✨ Features

- Shake any widget on demand
- Built-in presets: `light`, `medium`, `heavy`
- Optional vibration (custom or haptic)
- Fully customizable offset, pattern & intensities
- Easy to trigger using a `GlobalKey`

---

## 📦 Installation

```yaml
dependencies:
  awesome_shake_widget: ^1.0.1
```

Run:
```bash
flutter pub get
```

---

## 🧪 Usage

### 1️⃣ Standard (Shake + Vibration)

```dart
final shakeKey = GlobalKey<ShakeWidgetState>();

ShakeWidget(
  key: shakeKey,
  preset: ShakePreset.medium,
  child: Text("Tap Me"),
);

// Somewhere else, e.g., on button press:
shakeKey.currentState?.shake();
```

---

### 2️⃣ Shake Only (No Vibration)

```dart
ShakeWidget(
  key: shakeKey,
  preset: ShakePreset.custom,
  customConfig: ShakeConfig(
    offset: 20,
    vibrationType: VibrationType.none,
  ),
  child: Icon(Icons.info),
);
```

---

### 3️⃣ Full Custom (Offset + Pattern + Intensities)

```dart
ShakeWidget(
  key: shakeKey,
  preset: ShakePreset.custom,
  customConfig: ShakeConfig(
    offset: 32,
    pattern: [0, 50, 100, 50],
    intensities: [255, 0, 255, 0],
    vibrationType: VibrationType.custom,
  ),
  child: Text("Custom Shake!"),
);
```

Trigger it via:

```dart
shakeKey.currentState?.shake();
```

---

## 🧩 API Reference

### Enum: `ShakePreset`

| Value   | Offset | Vibration       |
|---------|--------|-----------------|
| light   | 8      | Haptic          |
| medium  | 16     | Haptic          |
| heavy   | 24     | Patterned Vibe  |
| custom  | User-defined | Custom    |

---

### Enum: `VibrationType`

- `none` – no vibration
- `haptic` – system haptic feedback
- `custom` – vibration with pattern/intensity (Android only)

---

### `ShakeConfig`

```dart
ShakeConfig({
  required double offset,
  List<int>? pattern,
  List<int>? intensities,
  VibrationType vibrationType = VibrationType.haptic,
});
```

---

## 💡 Example App

Clone and run the example:

```bash
cd example
flutter run
```

Example `main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:awesome_shake_widget/shake_widget.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ShakeDemo(),
    );
  }
}

class ShakeDemo extends StatelessWidget {
  final shakeKey = GlobalKey<ShakeWidgetState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Shake Demo')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ShakeWidget(
              key: shakeKey,
              preset: ShakePreset.heavy,
              child: const Icon(Icons.warning, size: 64),
            ),
            const SizedBox(height: 32),
            ElevatedButton(
              onPressed: () => shakeKey.currentState?.shake(),
              child: const Text("Shake it!"),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## 📄 License

MIT © [Juanma Del Boca](https://github.com/juanmadelboca)
