# Apk-mod (NJ Audio / Stereo DSP)

Pemutar audio dengan DSP stereo (L/R terpisah) dan efek untuk aplikasi lain.

## Pemutar internal
- EQ 10 band, HPF/LPF (6-48 dB/okt), gain, **polaritas (balik fase)**, mute, **reverb** (mix & ukuran)
- **Visualizer** spektrum 32 pita (dari sinyal keluaran setelah efek)
- **Jalan di latar belakang**: foreground service + notifikasi (Jeda/Putar, Stop), kontrol layar kunci/headset,
  audio focus (jeda otomatis saat aplikasi lain mulai memutar), wake lock CPU

## Efek untuk aplikasi lain (YouTube dll.)
Memakai `DynamicsProcessing` (gain, HPF/LPF, EQ) dan `PresetReverb` (reverb) yang dipasang ke sesi audio aplikasi lain.
Sesi ditemukan lewat broadcast `OPEN_AUDIO_EFFECT_CONTROL_SESSION` (pemutar yang mengumumkannya) dan
`dumpsys audio` (perlu izin sekali lewat ADB):

    adb shell pm grant com.stereodsp android.permission.DUMP

Keterbatasan Android: **polaritas/balik fase tidak bisa diterapkan ke aplikasi lain** (tidak ada di API efek);
reverb memakai preset ruang tanpa pengaturan mix.

## Build
Push ke GitHub: workflow `.github/workflows/build-apk.yml` menyusun struktur proyek dan membuat APK debug.
