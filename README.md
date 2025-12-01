# 📡 Android Broadcast Receiver

 guide and example implementation of Broadcast Receivers in Android.

## 📖 What is a Broadcast Receiver?

A **Broadcast Receiver** is one of the four fundamental components in Android that allows your app to receive and respond to system-wide broadcast messages or events. Think of it as a listener that waits for specific events to happen and reacts accordingly.

### Real-World Analogy
Imagine a radio station broadcasting news. Your Broadcast Receiver is like a radio tuned to a specific frequency - it only "hears" the broadcasts you're interested in and ignores everything else.

## 🎯 How It Works

```
Android System → Broadcasts Event → IntentFilter (checks) → BroadcastReceiver → Your Code Runs
```

1. **System** generates an event (e.g., charger connected)
2. **IntentFilter** checks if this event matches what you're listening for
3. **BroadcastReceiver** gets notified if there's a match
4. **Your code** in `onReceive()` executes

## 🔧 Key Components

### 1. BroadcastReceiver
The component that receives and handles broadcast messages.

```kotlin
class MyBroadcastReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        // Handle the broadcast here
    }
}
```

### 2. IntentFilter
Specifies which broadcasts you want to receive.

```kotlin
val filter = IntentFilter()
filter.addAction(Intent.ACTION_POWER_CONNECTED)
filter.addAction(Intent.ACTION_POWER_DISCONNECTED)
```

### 3. Registration
Subscribe to broadcasts (like subscribing to a newsletter).

```kotlin
registerReceiver(broadcastReceiver, filter)
```

### 4. Unregistration
Unsubscribe when done (prevents memory leaks).

```kotlin
unregisterReceiver(broadcastReceiver)
```

## 🎬 Common Use Cases

- 📶 Detecting network connectivity changes
- 🔋 Monitoring battery status
- 🔌 Detecting charger connection/disconnection
- 📱 Responding to incoming calls or SMS
- ✈️ Detecting airplane mode changes
- 🚀 Running tasks on device boot
- 📅 Responding to time/date changes
- Network changes

### Always Unregister
Failing to unregister receivers causes **memory leaks**!

```kotlin
override fun onDestroy() {
    super.onDestroy()
    unregisterReceiver(myReceiver) // ⚠️ CRITICAL!
}
```

### Keep onReceive() Fast
The `onReceive()` method runs on the main thread and has ~10 seconds timeout.
- ✅ DO: Quick operations, start services
- ❌ DON'T: Network calls, heavy processing

## 📱 Example: Power Connection Monitor

This repository contains a simple example that monitors charger connection/disconnection events.
