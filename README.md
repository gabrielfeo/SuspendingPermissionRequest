# SuspendingPermissionRequest
An idiomatic permissions API with Kotlin Coroutines

## Usage

`requestPermissionsAsync` can be called from any `Activity` or `Fragment` with a set of permissions and a request code:

```kotlin
val camera = Manifest.permission.CAMERA
val mic = Manifest.permission.RECORD_AUDIO
try {
    requestPermissionsAsync(arrayOf(camera, mic), "13949")) // suspend
} catch (exception: PermissionsDeniedException) {
    when {
        camera in exception.permanentlyDeniedPermissions -> // respect the user's decision
        else -> // explain you really need access to the camera
    }
}
```

Permissions will first be checked and the ones which aren't yet granted will be requested to the user, throwing a `PermissionsDeniedException` if any is denied. `PermissionsDeniedException` specifies which were permanently denied so that it's easy to decide what to do from there.

`requestPermissionsAsync` is available as an extension function on `androidx.app.FragmentActivity` and `androidx.fragment.Fragment`.
