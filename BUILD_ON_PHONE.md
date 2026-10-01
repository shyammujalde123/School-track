# Build the APK from a phone

This project is designed so the Android SDK does **not** need to be installed in GitHub Codespaces. GitHub Actions provides the Android build environment.

1. Upload the **contents of this folder** to the root of a GitHub repository (not the ZIP file itself).
2. Open **Actions**.
3. Select **Build School Track APK**.
4. Tap **Run workflow**.
5. When it finishes, open the run and download the artifact **school-track-release-apk**.
6. The artifact ZIP contains `app-release.apk`.

## Optional Firebase / Maps configuration

For a real deployment, add these GitHub repository secrets:

- `FIREBASE_OPTIONS_DART`: the complete contents of the generated `lib/firebase_options.dart` from `flutterfire configure`.
- `MAPS_API_KEY`: your Android Google Maps API key.

The app can still be compiled without these secrets, but Firebase services and Google Maps will not be connected to your project.
