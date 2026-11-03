# Catatan Riset Mandiri: Dinamika Galaksi & Materi Gelap
*Disusun untuk Periset Mandiri (Alumni S1 Astronomi ITB) | Fokus: Teori, Penurunan Rumus, & Analisis Data*

---

## 1. Peta Ekosistem & Isolasi Lingkungan Komputasi

Pemisahan ruang kerja komputasi diatur modular menggunakan Windows 11 dan WSL2 Ubuntu:

| Ruang Kerja | Lokasi Sistem | Teknologi / Dependensi |
| :--- | :--- | :--- |
| **Web Dev** | Windows (Herd) & Ubuntu (WSL) | Laravel, PHP, Next.js, Node.js LTS (`~/projects/`) |
| **AI & Deep Learning** | Ubuntu (WSL) - Environment Terpisah | PyTorch, Transformers, Accelerate (`~/ai-research/.venv/`) |
| **Riset Astronomi Mandiri** | Ubuntu (WSL) - Environment Khusus | Astropy, Lightkurve, Scipy, Matplotlib (`~/research/astro-lab/venv/`) |

> **Prinsip Isolasi:** Setiap sesi terminal berjalan independen. Terminal riset astronomi mengaktifkan `source venv/bin/activate` di `~/research/astro-lab` dan tidak saling mengganggu dengan sesi AI atau web dev.

---

## 2. Latar Belakang & Paper Tonggak Sejarah (NGC 3198)

Pada 1970-an, Vera Rubin dan Kent Ford mengamati kurva rotasi galaksi secara optik ($H\alpha$). Skeptisisme saat itu menduga kurva akan anjlok setelah piringan bintang habis. 

Untuk mengujinya, astronom radio beralih ke **garis emisi 21 cm Hidrogen Netral (H I)** dingin yang membentang jauh melampaui piringan bintang optik.

### Dua Paper Monumental:
1. **van Albada, T. S., Bahcall, J. N., Begeman, K., & Sancisi, R. (1985)**  
   *"Distribution of dark matter in the spiral galaxy NGC 3198"*, **The Astrophysical Journal (ApJ)**, 295, 305–313.
2. **Begeman, K. G. (1989)**  
   *"HI rotation curves of spiral galaxies. I. NGC 3198"*, **Astronomy and Astrophysics (A&A)**, 223, 47–60.

**Temuan Kunci:** Piringan optik bintang NGC 3198 habis di $r \approx 11\text{ kpc}$. Tetapi gas H I terdeteksi hingga $r = 30\text{ kpc}$ dengan kecepatan orbit tetap stabil pada kisaran $\sim 150\text{ km/s}$.

---

## 3. Penurunan Matematis Lengkap: Dari Newton ke Pseudo-Isothermal Halo

### A. Kesetimbangan Gravitasi vs Sentrifugal
$$\frac{m v^2(r)}{r} = F_{\text{grav}} = \frac{G M(r) m}{r^2} \implies v(r) = \sqrt{\frac{G M(r)}{r}}$$

* **Jika massa hanya materi tampak di pusat:**  
  Di luar piringan bintang ($r > R_{\text{disk}}$), $M(r) \approx M_{\text{tot}} = \text{konstan}$.  
  Maka berlaku penurunan Keplerian: $v(r) \propto r^{-1/2}$.
* **Observasi Nyata (Kurva Datar):**  
  Kecepatan konstan: $v(r) \approx v_0 = \text{konstan}$.  
  $$v_0^2 = \frac{G M(r)}{r} \implies M(r) = \left( \frac{v_0^2}{G} \right) r \propto r$$
  *Massa terlingkupi wajib bertambah secara linier terhadap radius!*

### B. Menghitung Kerapatan Ruang $\rho(r)$
$$M(r) = \int_0^r 4\pi r'^2 \rho(r') \, dr' \implies \frac{dM(r)}{dr} = 4\pi r^2 \rho(r)$$

Karena $M(r) \propto r$, maka $\frac{dM}{dr} = \frac{v_0^2}{G} = \text{konstan}$.
$$4\pi r^2 \rho(r) = \frac{v_0^2}{G} \implies \rho(r) = \frac{v_0^2}{4\pi G} \frac{1}{r^2} \propto r^{-2}$$
*(Singular Isothermal Sphere / SIS)*.

### C. Model Pseudo-Isothermal Sphere (Core Radius)
Agar densitas di pusat galaksi tidak meledak ($r \to 0$):
$$\rho(r) = \frac{\rho_0}{1 + \left(\frac{r}{r_c}\right)^2}$$

### D. Integrasi Massa Halo $M_{\text{halo}}(r)$
$$M_{\text{halo}}(r) = 4\pi \rho_0 \int_0^r \frac{r'^2}{1 + (r'/r_c)^2} \, dr'$$

Substitusi $u = r'/r_c \implies r' = r_c u$ dan $dr' = r_c du$:
$$M_{\text{halo}}(r) = 4\pi \rho_0 r_c^3 \int_0^{r/r_c} \frac{u^2}{1 + u^2} \, du = 4\pi \rho_0 r_c^3 \left[ u - \arctan(u) \right]_0^{r/r_c}$$
$$M_{\text{halo}}(r) = 4\pi \rho_0 r_c^2 \left[ r - r_c \arctan\left(\frac{r}{r_c}\right) \right]$$

### E. Kecepatan Sirkular Halo $v_{\text{halo}}(r)$
$$v_{\text{halo}}^2(r) = \frac{G M(r)}{r} = 4\pi G \rho_0 r_c^2 \left[ 1 - \frac{r_c}{r} \arctan\left(\frac{r}{r_c}\right) \right]$$

Definisikan kecepatan asimtotik saat $r \to \infty$: $v_\infty \equiv \sqrt{4\pi G \rho_0 r_c^2}$.
$$v_{\text{halo}}(r) = v_\infty \sqrt{1 - \frac{r_c}{r} \arctan\left(\frac{r}{r_c}\right)}$$

---

## 4. Empat Asumsi Fisis Utama
1. **Superposisi Kuadrat Kecepatan:** $\vec{g}_{\text{tot}} = \vec{g}_{\text{disk}} + \vec{g}_{\text{gas}} + \vec{g}_{\text{halo}} \implies v_{\text{tot}}^2 = v_{\text{disk}}^2 + v_{\text{gas}}^2 + v_{\text{halo}}^2$.
2. **Simetri Bola pada Halo:** Piringan bintang pipih, tetapi halo materi gelap terdistribusi kuasi-sferis.
3. **Maximum Disk Hypothesis:** Rasio $M/L$ bintang dimaksimalkan. Tetap gagal menjelaskan daerah luar galaksi ($r > 12\text{ kpc}$).
4. **Gas H I sebagai Tracer Uji:** Dispersi kecepatan gas sangat kecil ($\sim 8-10\text{ km/s}$) dibandingkan rotasi ($\sim 150\text{ km/s}$).

---

## 5. Skala Medan Lemah Einstein vs Newton
Mengapa Relativitas Umum (GR) tereduksi ke gravitasi Newton di skala galaksi?
* Rasio medan gravitasi: $\frac{|\Phi|}{c^2} = \frac{GM}{r c^2} \approx 10^{-6} \ll 1$
* Rasio kecepatan: $\left(\frac{v}{c}\right)^2 \approx 5 \times 10^{-7} \ll 1$

Galaksi berada pada rezim *ultra-weak field* dan *slow motion*, sehingga geodesik GR tereduksi secara eksak ke persamaan Poisson Newtonian $\nabla^2 \Phi = 4\pi G \rho$.

---

## 6. Kode Eksperimen Python & Hasil Fitting
Parameter hasil fitting data SPARC NGC 3198:
* $v_\infty \approx 149.8\text{ km/s}$
* Radius inti halo $r_c \approx 2.45\text{ kpc}$

---

## 7. Roadmap Langkah Riset Berikutnya
* **Bab 2:** Profil NFW (*Navarro-Frenk-White*) dari simulasi kosmologi $\Lambda\text{CDM}$ vs Profil Burkert.
* **Bab 3:** Pengujian Hipotesis MOND (*Modified Newtonian Dynamics*).
* **Bab 4:** Analisis Kurva Rotasi Bima Sakti dengan data **Gaia DR3**.
