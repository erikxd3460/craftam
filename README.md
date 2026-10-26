# craftam
Minecraft copia
name: Construir APK
on: workflow_dispatch
jobs:
  apk:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q craftam3d.zip -d proyecto
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.7
      - run: gradle assembleDebug --no-daemon
        working-directory: proyecto
      - uses: actions/upload-artifact@v4
        with:
          name: craftam-apk
          path: proyecto/app/build/outputs/apk/debug/app-debug.apk
