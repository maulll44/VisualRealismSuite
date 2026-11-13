# 3D Visual Realism Suite (ThreeDViewing - Minggu 11)

**Nama   :** MAULANA FAWADH REZAKA
**NIM    :** 25050974036
**Kelas  :** 2025A
**Mata Kuliah :** Grafika Komputer
**Repo GitHub :** (isi sendiri)

Java 17+, LWJGL 3.3.3, JOML 1.10.5, GLSL 330 core. Project berbentuk **Maven** sehingga bisa langsung dibuka di NetBeans.

## Cara menjalankan di NetBeans
1. `File > Open Project...` lalu pilih folder `VisualRealismSuite` (ikon Maven).
2. Pastikan JDK 17 atau lebih baru (Tools > Java Platforms). Koneksi internet dibutuhkan sekali untuk mengunduh dependency LWJGL.
3. Klik kanan project > **Clean and Build**, lalu **Run** (F6). Main class: `com.grafkom.viewing3d.Main`.
4. Khusus macOS: tambahkan VM option `-XstartOnFirstThread` (Project Properties > Run > VM Options).

## Kontrol
| Tombol | Fungsi | Indikator |
|---|---|---|
| B | Phong <-> Blinn-Phong | 1 |
| F | Flat <-> Smooth Shading | 2 |
| Z | Z-Buffer Depth Test ON/OFF | 3 |
| C | Back-Face Culling ON/OFF | 3 |
| T | Texture ON/OFF | 4 |
| N | Nearest <-> Bilinear + Mipmap | 4 |
| S | Shadow Mapping ON/OFF | 5 |
| [ / ] | Kurangi / tambah Shadow Bias (amati Acne & Peter Panning) | 5 |
| 1 / 2 / 3 | Ganti mesh: Sphere / Torus / House | - |
| L / R | Animasi cahaya / rotasi objek | - |
| V | VSync ON/OFF (untuk uji FPS) | - |
| Mouse drag / scroll | Orbit / zoom kamera | - |

Status semua fitur dan FPS ditampilkan di judul window (berguna untuk screenshot laporan).

## Struktur kode
- `Main` : window GLFW, input, render loop 2-pass (depth pass lalu lighting pass).
- `Mesh`, `MeshFactory` : mesh dengan normal vertex + UV; buffer Smooth (normal rata-rata) dan Flat (normal per-face).
- `ShaderProgram` : loader/compiler GLSL dan setter uniform.
- `HSRManager` : Z-Buffer dan Back-Face Culling.
- `Texture2D` : loader STBImage, UV wrap, filtering Nearest/Mipmap.
- `ShadowMapFBO` : Depth FBO 2048x2048 untuk shadow map.
- `OrbitCamera` : kamera orbit.
- `resources/shaders/` : `phong.vert/frag` (Blinn-Phong per-pixel + tekstur + shadow PCF) dan `depth.vert/frag`.
