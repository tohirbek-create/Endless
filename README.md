# Endless Runner 3D

Subway Surfers uslubidagi oddiy, low-poly 3D endless runner o'yin.
100% Kotlin + Android SDK'ning o'zidagi OpenGL ES 2.0 asosida yozilgan —
hech qanday tashqi o'yin motori yoki og'ir kutubxona ishlatilmagan.

## Loyihani ochish

1. Android Studio'ni oching → **Open** → shu papkani (`EndlessRunner3D`) tanlang.
2. Studio Gradle sinxronizatsiyasini avtomatik boshlaydi (birinchi marta internet
   kerak bo'ladi — Gradle wrapper distributivini yuklab olish uchun; bu har qanday
   yangi Android loyihasida bir martalik jarayon). Sinxronizatsiya tugagach,
   loyiha to'liq offline ishlaydi — o'yinning o'zi hech qanday internetga muhtoj emas.
3. **Run ▶** tugmasini bosing yoki **Build > Build Bundle(s)/APK(s) > Build APK(s)**
   orqali APK yig'ing. Hech qanday qo'shimcha fayl yaratish shart emas.

## Boshqaruv

- **Chapga surish** — chap yo'lakka o'tish
- **O'ngga surish** — o'ng yo'lakka o'tish
- **Yuqoriga surish** — sakrash (past to'siqlar ustidan)
- **Pastga surish** — egilish (balandda osilgan to'siqlar ostidan)

## To'siq turlari

- 🟥 Qizil (**BLOCK**) — butun yo'lakni to'sadi, faqat yo'lak almashtirib o'tish mumkin
- 🟧 To'q sariq (**LOW**) — past to'siq, sakrab o'tish kerak
- 🟪 Binafsha (**HIGH**) — osilgan to'siq, egilib o'tish kerak
- 🟡 Sariq kublar — tangalar, ustidan o'tsangiz yig'iladi

## Loyiha tuzilishi

```
EndlessRunner3D/
├── settings.gradle
├── build.gradle
├── gradle.properties
├── gradle/wrapper/gradle-wrapper.properties
└── app/
    ├── build.gradle
    ├── proguard-rules.pro
    └── src/main/
        ├── AndroidManifest.xml
        ├── java/com/endless/runner3d/
        │   ├── MainActivity.kt      – Activity, HUD, Game Over paneli
        │   ├── GameView.kt          – GLSurfaceView + swipe boshqaruvi
        │   ├── GameRenderer.kt      – OpenGL render tsikli, kamera, chizish
        │   ├── GameEngine.kt        – o'yin mantig'i (lane, jump, duck, ball)
        │   ├── Cube.kt              – qayta ishlatiluvchi low-poly kub mesh
        │   ├── ShaderUtil.kt        – GLSL shaderlarni yuklash
        │   └── GameListener.kt      – Engine → UI callback interfeysi
        └── res/
            ├── layout/activity_main.xml
            ├── values/strings.xml
            ├── values/colors.xml
            ├── values/themes.xml
            └── drawable/panel_background.xml, button_background.xml
```

## AndroidIDE (telefonda) uchun eslatma

Bu loyiha ataylab **eski, moslashuvchan Gradle uslubida** yozilgan
(`settings.gradle`da `dependencyResolutionManagement` yo'q, `app/build.gradle`da
yangi `plugins {}` bloki o'rniga `apply plugin:` ishlatilgan). Sababi: AndroidIDE
orqali `gradle wrapper` buyrug'ini bajarganda, bu buyruq avval qurilmada
o'rnatilgan **global (eski) Gradle** versiyasi bilan ishga tushadi — agar
`settings.gradle` faqat yangi Gradle versiyalarida mavjud funksiyalarni ishlatsa,
xato beradi. Eski uslub deyarli barcha Gradle versiyalari bilan ishlaydi.

Loyihani ochish tartibi:
1. ZIP faylni `/storage/emulated/0/AndroidIDEProjects/` (yoki boshqa) papkaga
   chiqaring va **settings.gradle qaysi papkada ekanini tekshiring** (ba'zan
   arxivlash ikki qavat papka hosil qiladi).
2. AndroidIDE terminalida, `settings.gradle` turgan papkaga kirib:
   ```
   gradle wrapper --gradle-version 8.4
   ```
3. AndroidIDE'da **Open Project** orqali o'sha papkani oching, sinxronizatsiya
   tugashini kuting, so'ng **Run ▶**.

## Texnik eslatmalar

- Grafika: qo'l bilan yozilgan OpenGL ES 2.0 shaderlar, oddiy diffuz yoritish.
- Fon: bitta rangli osmon (`glClearColor`) — teksturasiz, telefonni qiynamaydi.
- Barcha 3D obyektlar (o'yinchi, to'siqlar, tangalar, yer) bitta kub mesh'idan
  turli o'lcham/rang bilan hosil qilinadi — juda yengil.
- minSdk 21, compileSdk/targetSdk 34, Kotlin 1.9.22, AGP 8.1.4.
