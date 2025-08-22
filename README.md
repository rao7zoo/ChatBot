# MultiAiChat - Android

This repository is a ready-to-import Android Studio project implementing a Multi-AI Chat app.

**What it includes**
- Jetpack Compose UI with a professional theme and splash screen.
- Provider registry + example adapters for OpenAI and Anthropic.
- ViewModel + Room persistence skeleton.
- Network examples (OkHttp + Gson).
- BuildConfig placeholders for API keys (DO NOT ship production keys).

**Notes**
- Replace API keys in `app/build.gradle` or better yet use a secure backend proxy.
- Verify provider request/response shapes against provider docs before production.

Enjoy!

## Production / Release Checklist (automated additions)

1. **Server Proxy**
   - Deploy the `/server` app to a secure host (Heroku, Render, DigitalOcean, AWS, etc).
   - Copy `.env.sample` to `.env` and set your provider API keys.
   - Ensure your proxy is served over HTTPS and set `ALLOWED_ORIGINS` to your app's domains.

2. **Privacy Policy**
   - Host `server/public/privacy_policy.html` at a stable HTTPS URL and use that URL in Play Console when submitting.

3. **Signing & Keystore**
   - Copy `keystore.properties.sample` -> `keystore.properties` and provide path/passwords.
   - Generate a keystore using `keytool` and do NOT commit it to the repo.

4. **API Keys**
   - Never embed production API keys in the mobile client. Use the server proxy above.

5. **Play Store Assets**
   - Replace `playstore_assets/*` placeholders with real screenshots and a proper feature graphic.

6. **Build & Publish**
   - In Android Studio: Build -> Generate Signed Bundle / APK, select your keystore, and produce an AAB for Play Store.
   - Fill Play Store listing, privacy policy URL, and content rating.

7. **Optional Hardening**
   - Configure ProGuard/R8 rules, monitor network usage, add telemetry (respecting privacy), and set up analytics.


## Direct API (no server) mode
This repository supports a mode where the mobile app calls AI provider APIs directly. To use direct API mode:
- Open the app Settings and enter your API keys for OpenAI and/or Anthropic. Keys are stored encrypted on-device (EncryptedSharedPreferences).
- The app will prefer the keys you set in settings; if none are set it falls back to `BuildConfig` placeholders in `app/build.gradle`.

**Important security & policy notes**
- Storing provider API keys on the client can be risky. If someone extracts your key they can use your quota and potentially accrue charges.
- This approach may violate some providers' terms of service or Play Store policies if keys are embedded or misused. Use direct API mode only for testing or if each user supplies their own key.
- For production and multi-user apps, we still strongly recommend using the server proxy included in `/server` to keep keys server-side and to add rate limiting, abuse protection, and monitoring.
