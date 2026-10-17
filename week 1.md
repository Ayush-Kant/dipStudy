# NPTEL Digital Image Processing — Week 1 One-Stop Revision Sheet

**Course:** Digital Image Processing (DIP)  
**Instructor:** Prof. P. K. Biswas, IIT Kharagpur  
**Purpose:** Fast revision for Week 1, based on Lectures 1–5 and the supplied Week 1 assignment.  
**Question note:** The 40 practice questions below are original exam-style practice questions, not actual or guaranteed NPTEL exam questions.

---

## Contents
1. Week 1 map
2. Concepts at a glance
3. Formula sheet
4. Quick methods for numerical questions
5. Your 10 assignment questions with solutions
6. Forty additional practice questions
7. Answer key
8. Last-minute checklist

---

# 1. Week 1 map

| Lecture | Main topics |
|---|---|
| 1. Introduction to Digital Image Processing | Digital image, image-processing goals, human perception vs machine analysis |
| 2. Applications of Digital Image Processing | Enhancement, inspection, compression, image analysis, video sequence/motion tracking |
| 3. Image Digitization, Sampling, Quantization and Display | Image model, sampling, quantization, pixels, impulse train/comb, Fourier transform vs Fourier series, Fourier-series coefficients of the comb, DFT |
| 4. Signal Reconstruction from Samples: Convolution Concept | Continuous/discrete convolution, convolution theorem, sampling in time and spectrum replication |
| 5. Signal Reconstruction from Image | 2D spatial frequencies, region of support, 2D sampling comb, spectral replicas, low-pass reconstruction, Nyquist condition, sampling-density effects |

## Core story of Week 1

A real-world image is modelled as a continuous function. To process it digitally, spatial locations are sampled and intensity values are quantized. Sampling can be represented using an impulse train. Its spectrum is also an impulse train, so sampling replicates the original signal/image spectrum. If replicated spectra overlap, aliasing occurs. If the signal is appropriately band-limited and the sampling rate is high enough, an ideal low-pass filter can isolate the original spectrum.

---

# 2. Concepts at a glance

## 2.1 Digital Image Processing (Lectures 1–2)

A grayscale image is represented by a two-dimensional intensity function:

\[
f(x,y)
\]

- \(x,y\): spatial coordinates.
- \(f(x,y)\): intensity at a location.
- Human-oriented processing improves visual appearance (e.g., enhancement or denoising).
- Machine-oriented processing extracts information for automatic tasks (e.g., inspection, detection, measurement, tracking).
- Industrial inspection may use **boundary/edge contours** for geometry, corners and dimensions.
- **Spatial redundancy:** nearby pixels often have predictable or similar values.
- **Temporal redundancy:** similarity between successive video frames.
- **Coding redundancy:** inefficiency in the code used to represent data.
- **Psychovisual redundancy:** information less noticeable to human vision.
- Consecutive frames are analysed to detect and track moving objects.

Intensity model mentioned in Lecture 3:

\[
f(x,y)=r(x,y)i(x,y)
\]

where \(r(x,y)\) is surface reflectance and \(i(x,y)\) is illumination.

## 2.2 Sampling and quantization (Lecture 3)

**Digitization has two distinct operations:**

1. **Sampling:** makes spatial locations discrete; an image is represented on a finite grid.
2. **Quantization:** maps each sampled intensity to one of a finite set of levels.

Do not confuse:
- Spatial resolution: density/number of sample locations.
- Intensity resolution: number of representable intensity levels.

If each pixel uses \(b\) bits:

\[
L=2^b,\qquad b=\log_2 L
\]

Examples: 1 bit → 2 levels; 4 bits → 16; 8 bits → 256; 10 bits → 1024. Conventional 8-bit grayscale has values 0–255; conventional RGB with 8 bits/channel uses 24 bits/pixel.

The lecture's processing pipeline is: original image → sampling → quantization → digital computer processing → D/A conversion/display (for the display system described).

## 2.3 Sampling interval and frequency

For a time-domain signal:

\[
f_s=\frac{1}{T_s}
\]

where \(T_s\) is the sampling interval in seconds and \(f_s\) is samples/second (Hz).

Halve the sampling interval → double the sampling frequency.

For an image sampled at spatial intervals \(\Delta x,\Delta y\):

\[
f_{sx}=\frac{1}{\Delta x},\qquad
f_{sy}=\frac{1}{\Delta y}
\]

These spatial frequencies are measured in samples per unit length. Ordinary spatial frequency (cycles/unit length) and angular spatial frequency (radians/unit length) differ by \(2\pi\).

## 2.4 Dirac delta and impulse train

The shifted Dirac impulse is written \(\delta(t-a)\). Its sifting property is:

\[
\int_{-\infty}^{\infty}g(t)\delta(t-a)\,dt=g(a)
\]

The Dirac delta is mathematically a distribution; the impulse picture is an intuitive aid.

The one-dimensional comb (periodic impulse train) is:

\[
c(t)=\operatorname{comb}(t;T_s)
=\sum_{m=-\infty}^{\infty}\delta(t-mT_s)
\]

It consists of equally spaced impulses. The sampled signal is:

\[
x_s(t)=x(t)c(t)
=\sum_{m=-\infty}^{\infty}x(mT_s)\delta(t-mT_s)
\]

**Comb function vs sampled signal:** the comb defines the sampling locations; the sampled signal weights each impulse by the original value at that location.

## 2.5 Fourier transform, Fourier series and DFT (Lecture 3)

Using the lecture's angular-frequency convention:

For an aperiodic continuous-time signal, the Fourier transform is

\[
X(\omega)=\int_{-\infty}^{\infty}x(t)e^{-j\omega t}\,dt
\]

For a periodic signal of period \(T_0\), the complex Fourier-series representation is

\[
v(t)=\sum_{n=-\infty}^{\infty}C_ne^{jn\omega_0t},
\qquad \omega_0=\frac{2\pi}{T_0}
\]

and

\[
C_n=\frac{1}{T_0}\int_{T_0}
v(t)e^{-jn\omega_0t}\,dt
\]

The integral is over any one complete period.

For the unit-impulse comb with period \(T_s\), one period contains an impulse at zero. Using the delta sifting property:

\[
C_n=\frac{1}{T_s}\int_{\text{one period}}
\delta(t)e^{-jn\omega_0t}\,dt
=\frac{1}{T_s}e^0
=\frac{1}{T_s}=f_s
\]

Thus all integer-indexed Fourier-series coefficients of this ideal impulse train equal \(1/T_s\). This is special to the ideal impulse train, not a general rule for every periodic signal.

The Fourier-series expansion becomes

\[
c(t)=\frac{1}{T_s}\sum_{n=-\infty}^{\infty}
e^{jn2\pi t/T_s}
\]

The transcript's scanned inverse DFT display appears to omit the normalization factor. Using the standard convention consistent with the unnormalized forward DFT:

\[
X[k]=\sum_{n=0}^{N-1}x[n]e^{-j2\pi nk/N}
\]

\[
x[n]=\frac{1}{N}\sum_{k=0}^{N-1}X[k]e^{j2\pi nk/N}
\]

where \(N\) is the number of samples.

Frequency conversion:

\[
\omega=2\pi f,\qquad f=\frac{|\omega|}{2\pi}
\]

Use Hz (cycles/second) for ordinary frequency and rad/s for angular frequency.

## 2.6 Convolution (Lecture 4)

Continuous convolution:

\[
y(t)=(h*x)(t)=\int_{-\infty}^{\infty}
h(\tau)x(t-\tau)\,d\tau
\]

Recipe: time-reverse one signal, shift it, multiply corresponding values and integrate over the full domain.

Discrete convolution:

\[
y[n]=\sum_{m=-\infty}^{\infty}h[m]x[n-m]
\]

Useful impulse identity:

\[
x[n]*\delta[n-n_0]=x[n-n_0]
\]

Convolution with a shifted unit impulse shifts a sequence. Convolution with an impulse train makes shifted copies of the input sequence at the impulse locations.

## 2.7 Convolution theorem and sampling spectrum

With the Fourier transform convention used above:

\[
\mathcal F\{h*x\}=H(\omega)X(\omega)
\]

Time-domain convolution becomes frequency-domain multiplication.

Time-domain multiplication becomes frequency-domain convolution, with normalization:

\[
\mathcal F\{h(t)x(t)\}
=\frac{1}{2\pi}[H*X](\omega)
\]

The Fourier transform of the one-dimensional comb is:

\[
C(\omega)=\frac{2\pi}{T_s}
\sum_{n=-\infty}^{\infty}\delta(\omega-n\Omega_s),
\qquad \Omega_s=\frac{2\pi}{T_s}
\]

Therefore, for impulse-train sampling:

\[
X_s(\omega)=\frac{1}{T_s}
\sum_{n=-\infty}^{\infty}X(\omega-n\Omega_s)
\]

The original spectrum is replicated at integer multiples of the sampling angular frequency.

## 2.8 Nyquist condition, reconstruction and aliasing

For a real band-limited signal with maximum ordinary frequency \(f_{\max}\), the course uses the strict ideal-reconstruction condition:

\[
f_s>2f_{\max}
\]

The Nyquist rate is \(2f_{\max}\). Its Nyquist frequency at a specified sampling rate is \(f_s/2\).

If spectral copies are separated, an ideal low-pass filter can keep the central copy and reject the others. If the copies overlap, **aliasing** occurs, and ideal low-pass filtering cannot generally recover the original exactly.

In angular frequency, if the signal is supported within \([-\Omega_m,\Omega_m]\), a cutoff can be selected when:

\[
\Omega_m<\Omega_c<\Omega_s-\Omega_m
\]

which requires \(\Omega_s>2\Omega_m\).

**Aliasing calculation for real sinusoids:** when a component lies above the Nyquist frequency, find its folded frequency in the baseband. For a single real sinusoid at frequency \(f\), a useful folding calculation is the distance from \(f\) to the nearest integer multiple of \(f_s\), folded into \([0,f_s/2]\). For the assignment's 175 Hz component sampled at 200 Hz, the alias is \(|175-200|=25\) Hz.

## 2.9 Two-dimensional image sampling (Lecture 5)

A continuous image is \(f(x,y)\). Sample it at \((m\Delta x,n\Delta y)\):

\[
f_s(x,y)=\sum_m\sum_n f(m\Delta x,n\Delta y)
\delta(x-m\Delta x)\delta(y-n\Delta y)
\]

Define angular spatial sampling frequencies:

\[
\Omega_{sx}=\frac{2\pi}{\Delta x},\qquad
\Omega_{sy}=\frac{2\pi}{\Delta y}
\]

The sampled spectrum consists of copies shifted along **both** spatial-frequency axes:

\[
F_s(\omega_x,\omega_y)=\frac{1}{\Delta x\Delta y}
\sum_m\sum_n
F(\omega_x-m\Omega_{sx},\omega_y-n\Omega_{sy})
\]

This expression uses angular spatial frequencies and the matching Fourier convention. The repeated spectra form a 2D grid.

If the image is band-limited along each axis, its component-wise conditions are:

\[
f_{sx}>2f_{x,\max},\qquad
f_{sy}>2f_{y,\max}
\]

where these are ordinary spatial frequencies (cycles/unit length). Equivalently, for angular spatial frequency limits \(\Omega_{xm},\Omega_{ym}\):

\[
\Omega_{sx}>2\Omega_{xm},\qquad
\Omega_{sy}>2\Omega_{ym}
\]

The **region of support** is the region in the \((\omega_x,\omega_y)\) frequency plane where the original image spectrum can be nonzero. Reconstruction retains the central region around the origin using an ideal 2D low-pass filter when the copies do not overlap.

The lecture illustrates 50, 100, 600 and 1200 dots/inch: very low sampling gives poor/blurred detail; higher density makes edges smoother; the improvement from 600 to 1200 in that example is comparatively smaller. This is an illustration, not a universal claim that resolution never helps above one fixed density.

---

# 3. Formula sheet — quick reference

| Topic | Formula |
|---|---|
| Image intensity model | \(f(x,y)=r(x,y)i(x,y)\) |
| Number of intensity levels | \(L=2^b\) |
| Bits for \(L\) levels | \(b=\log_2L\) |
| Sampling frequency | \(f_s=1/T_s\) |
| Spatial sampling | \(f_{sx}=1/\Delta x,\ f_{sy}=1/\Delta y\) |
| Angular/ordinary frequency | \(\omega=2\pi f,\ f=|\omega|/(2\pi)\) |
| Delta sifting | \(\int g(t)\delta(t-a)dt=g(a)\) |
| Comb function | \(c(t)=\sum_m\delta(t-mT_s)\) |
| Sampled signal | \(x_s(t)=\sum_mx(mT_s)\delta(t-mT_s)\) |
| Fourier transform | \(X(\omega)=\int x(t)e^{-j\omega t}dt\) |
| Fourier series | \(v(t)=\sum_nC_ne^{jn\omega_0t}\) |
| Fourier coefficient | \(C_n=(1/T_0)\int_{T_0}v(t)e^{-jn\omega_0t}dt\) |
| Comb Fourier coefficient | \(C_n=1/T_s=f_s\) |
| Fundamental angular frequency | \(\omega_0=2\pi/T_0\) |
| Forward DFT | \(X[k]=\sum_{n=0}^{N-1}x[n]e^{-j2\pi nk/N}\) |
| Inverse DFT | \(x[n]=(1/N)\sum_{k=0}^{N-1}X[k]e^{j2\pi nk/N}\) |
| Continuous convolution | \(y(t)=\int h(\tau)x(t-\tau)d\tau\) |
| Discrete convolution | \(y[n]=\sum_mh[m]x[n-m]\) |
| Convolution theorem | \(\mathcal F\{h*x\}=HX\) |
| Time multiplication property | \(\mathcal F\{hx\}=(1/2\pi)(H*X)\) |
| Sampling spectrum | \(X_s(\omega)=(1/T_s)\sum_nX(\omega-n\Omega_s)\) |
| 1D Nyquist condition | \(f_s>2f_{\max}\) |
| 2D Nyquist condition | \(f_{sx}>2f_{x,\max},\ f_{sy}>2f_{y,\max}\) |
| 2D angular sampling frequencies | \(\Omega_{sx}=2\pi/\Delta x,\ \Omega_{sy}=2\pi/\Delta y\) |
| 2D sampled spectrum | \(F_s=(1/(\Delta x\Delta y))\sum_{m,n}F(\omega_x-m\Omega_{sx},\omega_y-n\Omega_{sy})\) |

---

# 4. Quick methods for numerical questions

## Method A: Sampling a 2D sinusoidal image

Given a sum of terms such as:

\[
f(x,y)=\cos(20\pi x+60\pi y)+\sin(80\pi x-10\pi y)
\]

1. Write each term as a sinusoid with \(2\pi\) multiplying the spatial frequency coefficients.
2. Find the largest absolute \(x\)-frequency coefficient.
3. Find the largest absolute \(y\)-frequency coefficient.
4. Double each maximum for the Nyquist threshold.

The example above has maximum ordinary spatial frequency 40 along \(x\) and 30 along \(y\), so the thresholds are \(f_{sx}>80\) and \(f_{sy}>60\) samples/unit.

## Method B: Find frequency from a cosine

For \(x(t)=\cos(\omega t)\):

\[
f=\frac{|\omega|}{2\pi}
\]

Example: \(\cos(350\pi t)\) has frequency 175 Hz.

## Method C: Find an aliased frequency

1. Convert each angular frequency to hertz.
2. Calculate \(f_N=f_s/2\).
3. Fold any component above \(f_N\) into the baseband using sampling-frequency replicas.
4. Apply the reconstruction-filter cutoff to see which components pass.

Example: 175 Hz sampled at 200 Hz aliases to 25 Hz.

## Method D: Delta-function integral

For a shifted impulse, directly substitute the shift:

\[
\int_{-\infty}^{\infty}g(t)\delta(t-a)dt=g(a)
\]

## Method E: Discrete convolution with an impulse train

Use:

\[
y[n]=\sum_kx[n-9k]
\]

for a unit impulse train with spacing nine. Identify which shifted copy contributes to the requested output index rather than multiplying every zero.

---

# 5. Your original Week 1 assignment — 10 questions with solutions

These solutions follow the supplied assignment material. They are presented as study notes, not as a substitute for the original quiz interface. The topics and values below are based on the supplied Week 1 quiz PDF.

## Q1. Sampling frequencies for a 2D image

**Question:** Given

\[
f(x,y)=\cos(20\pi x+60\pi y)+\sin(80\pi x-10\pi y)
\]

find the required sampling frequencies in the two directions.

**Solution:** Rewrite the terms as:

\[
\cos(2\pi(10x+30y)),\qquad
\sin(2\pi(40x-5y))
\]

Maximum absolute frequencies: \(f_{x,\max}=40\), \(f_{y,\max}=30\).

Therefore:

\[
f_{sx}>2(40)=80,\qquad f_{sy}>2(30)=60
\]

**Answer:** Option D, \(f_{sx}>80\) and \(f_{sy}>60\).

## Q2. Aliasing after sampling

**Question:** \(x(t)=\cos(100\pi t)+\cos(350\pi t)\) is sampled at 200 Hz and reconstructed through an ideal low-pass filter with cutoff 100 Hz. Identify the frequency components.

**Solution:**

\[
f_1=\frac{100\pi}{2\pi}=50\text{ Hz},\qquad
f_2=\frac{350\pi}{2\pi}=175\text{ Hz}
\]

Nyquist frequency = \(200/2=100\) Hz. The 175 Hz component folds to:

\[
|175-200|=25\text{ Hz}
\]

Both 25 Hz and 50 Hz pass the 100 Hz low-pass filter.

**Answer:** Option B, 25 Hz and 50 Hz.

## Q3. Convolution with an impulse train

**Question:** The sequence has \(x[-2]=2, x[-1]=5, x[0]=7, x[1]=9, x[2]=3\), zero elsewhere. It is convolved with a unit impulse train whose impulses are spaced nine samples apart. Find \(y[7]\).

**Solution:**

\[
y[n]=\sum_kx[n-9k]
\]

At \(n=7\), the contributing copy is \(x[7-9]=x[-2]=2\). Other terms are outside the nonzero range.

**Answer:** Option B, 2.

## Q4. Meaning of the comb function

**Question:** What does the comb function represent?

**Solution:**

\[
c(t)=\sum_{m=-\infty}^{\infty}\delta(t-mT_s)
\]

It is an infinite array of equally spaced impulses with spacing \(T_s\).

**Answer:** Option C, an infinite one-dimensional array of regularly spaced Dirac delta functions.

## Q5. Convolution theorem

**Question:** What is the frequency-domain equivalent of convolution in the time domain?

**Solution:**

\[
\mathcal F\{x(t)*h(t)\}=X(\omega)H(\omega)
\]

**Answer:** Option B, point-by-point multiplication of the frequency spectra.

## Q6. Delta-function sifting property

**Question:** Evaluate:

\[
\int_{-\infty}^{\infty}f(t)\delta(t-2)\,dt
\]

**Solution:** The shifted impulse selects the value at \(t=2\).

\[
\boxed{f(2)}
\]

**Answer:** Option B, \(f(2)\).

## Q7. Effect of sampling in the frequency domain

**Question:** What happens to the spectrum of a continuous band-limited signal when it is sampled?

**Solution:** Sampling multiplies the signal by an impulse train in time. Under the Fourier-transform multiplication/convolution relationship, the original spectrum is replicated at regular intervals in frequency.

**Answer:** Option B, the spectrum is replicated at intervals set by the sampling frequency.

## Q8. Automated refractory-brick inspection

**Question:** Which feature is primarily used to identify structural defects such as missing corners or dimensional irregularities?

**Solution:** Boundary or edge contours represent the object's outline, corners and geometry.

**Answer:** Option B, boundary or edge contours.

## Q9. Neighbouring-pixel predictability

**Question:** What type of redundancy occurs when a pixel can be predicted from neighbouring pixels?

**Solution:** Similarity or predictability across nearby spatial locations is spatial (pixel) redundancy.

**Answer:** Option C, pixel/spatial redundancy.

## Q10. Consecutive video frames

**Question:** Why analyse consecutive frames for security surveillance or medical organ tracking?

**Solution:** Changes across frames allow a system to detect moving regions and track objects over time.

**Answer:** Option B, detect and track moving parts or targets against a background.

### Important source-quality note

A couple of marked numerical values in the supplied screenshots appeared inconsistent with the values visible in the question. For revision, use the derivation and verify the original quiz/instructor explanation before memorising any conflicting answer badge. The solutions above show the calculations implied by the stated inputs.

---

# 6. Forty additional exam-style practice questions

These are **original practice questions** based on the Week 1 lecture concepts and assignment style. They are not actual NPTEL questions, and their appearance in a future exam is not guaranteed.

Try answering all questions before checking the answer key.

## Section A — MCQs (1–25)

### Q1. Image fundamentals
A grayscale image is most directly represented mathematically as:

A. A one-dimensional scalar only  
B. A two-dimensional intensity function \(f(x,y)\)  
C. A list of Fourier coefficients only  
D. A probability distribution only

### Q2. Digitization
Which pair represents the two principal stages of image digitization?

A. Filtering and segmentation  
B. Sampling and quantization  
C. Compression and display  
D. Convolution and differentiation

### Q3. Sampling vs quantization
Sampling primarily discretizes:

A. Spatial locations  
B. Intensity levels  
C. Fourier coefficients only  
D. Display brightness only

### Q4. Number of intensity levels
How many possible levels can be represented using 6 bits per pixel?

A. 6  
B. 12  
C. 32  
D. 64

### Q5. Sampling interval
A signal is sampled every 0.005 seconds. What is its sampling frequency?

A. 50 Hz  
B. 100 Hz  
C. 200 Hz  
D. 500 Hz

### Q6. Frequency conversion
The frequency of \(\cos(80\pi t)\) is:

A. 20 Hz  
B. 40 Hz  
C. 80 Hz  
D. 160 Hz

### Q7. Nyquist rate
A band-limited signal contains no frequency above 3 kHz. Its Nyquist rate is:

A. 1.5 kHz  
B. 3 kHz  
C. 6 kHz  
D. 9 kHz

### Q8. Aliasing
A 90 Hz sinusoid is sampled at 100 Hz. Its baseband alias frequency is:

A. 10 Hz  
B. 40 Hz  
C. 50 Hz  
D. 90 Hz

### Q9. Delta function
The value of \(\int g(t)\delta(t-4)dt\), over the full real line, is:

A. \(g(0)\)  
B. \(g(4)\)  
C. \(g(-4)\)  
D. 4

### Q10. Comb function
In the expression \(\sum_m\delta(t-mT_s)\), the distance between adjacent impulses is:

A. \(2T_s\)  
B. \(1/T_s\)  
C. \(T_s\)  
D. \(T_s^2\)

### Q11. Fourier-series coefficient
The coefficient formula for a periodic signal of period \(T_0\) includes the factor:

A. \(T_0\)  
B. \(1/T_0\)  
C. \(2\pi T_0\)  
D. \(1/(2\pi)\) only

### Q12. Fourier representation
Which representation is used for the Fourier-series expansion of a periodic signal?

A. A sum over integer harmonics  
B. A sum over spatial pixels only  
C. A single DC value  
D. A probability density function

### Q13. Impulse-train Fourier coefficients
For the ideal unit-impulse comb with period \(T_s\), the complex Fourier-series coefficients are:

A. All zero  
B. \(n/T_s\)  
C. \(1/T_s\) for all integer \(n\)  
D. Only the coefficient for \(n=1\) is nonzero

### Q14. DFT
For an \(N\)-point standard DFT, the inverse-transform normalization factor is:

A. \(N\)  
B. \(1/N\)  
C. \(2\pi/N\)  
D. \(1/2\pi\)

### Q15. Continuous convolution
The standard continuous convolution formula is:

A. \(y(t)=h(t)x(t)\)  
B. \(y(t)=\int h(\tau)x(t-\tau)d\tau\)  
C. \(y(t)=h(t)+x(t)\)  
D. \(y(t)=x(t)/h(t)\)

### Q16. Convolution theorem
Time-domain convolution corresponds to which operation in the frequency domain?

A. Addition  
B. Differentiation only  
C. Multiplication  
D. Quantization

### Q17. Multiplication property
Under the angular-frequency Fourier convention used in the notes, time-domain multiplication corresponds to:

A. Frequency-domain convolution with the transform-convention factor  
B. Frequency-domain subtraction  
C. Sampling with no spectrum change  
D. Only a DC component

### Q18. Spectrum replication
The frequency-domain result of impulse-train sampling is:

A. Only one spectral value  
B. Repeated shifted copies of the original spectrum  
C. A spectrum with no negative frequencies  
D. Complete removal of high frequencies

### Q19. Reconstruction
An ideal low-pass filter reconstructs a band-limited signal by:

A. Passing all replicated bands  
B. Passing the central original band and rejecting other copies  
C. Replacing every sample by zero  
D. Increasing the sampling interval

### Q20. Aliasing cause
Aliasing is associated with:

A. Non-overlapping spectrum copies  
B. Overlap of replicated spectra after sampling  
C. Perfect sampling  
D. Intensity quantization alone

### Q21. Image frequency
Image spatial frequency is conventionally expressed in:

A. Cycles per second only  
B. Cycles per unit length  
C. Bits per pixel  
D. Pixels per frame only

### Q22. Two-dimensional image spectrum
For an image \(f(x,y)\), the frequency spectrum is represented as a function of:

A. One frequency variable only in all cases  
B. \(F(\omega_x,\omega_y)\)  
C. \(F(t)\) only  
D. \(F(b)\)

### Q23. 2D sampling
A sampled 2D image has spectral copies repeated:

A. Along only one axis  
B. Along both spatial-frequency axes  
C. Only at the origin  
D. Only in the spatial domain

### Q24. Image reconstruction condition
For an image with maximum ordinary spatial frequencies \(f_{x,\max}\) and \(f_{y,\max}\), the ideal component-wise sampling requirements are:

A. \(f_{sx}>f_{x,\max}\) and \(f_{sy}>f_{y,\max}\)  
B. \(f_{sx}>2f_{x,\max}\) and \(f_{sy}>2f_{y,\max}\)  
C. \(f_{sx}=f_{sy}=0\)  
D. Only the vertical sampling rate matters

### Q25. Application
Predictability among neighbouring pixel values is most closely related to:

A. Temporal redundancy  
B. Spatial redundancy  
C. Motion tracking  
D. Fourier-series period

## Section B — Fill in the blanks (26–40)

### Q26.
The number of possible intensity levels for a pixel represented by \(b\) bits is ________.

### Q27.
If the sampling interval is \(T_s\), the sampling frequency is ________.

### Q28.
The relationship between angular frequency and ordinary frequency is \(\omega=\) ________.

### Q29.
The shifted Dirac impulse integral \(\int_{-\infty}^{\infty}g(t)\delta(t-a)dt\) evaluates to ________.

### Q30.
A regular infinite train of equally spaced impulses is called a ________ function.

### Q31.
The Fourier-series fundamental angular frequency for period \(T_0\) is ________.

### Q32.
The complex Fourier-series coefficient of the ideal unit-impulse comb of period \(T_s\) is ________ for every integer harmonic index.

### Q33.
In the standard inverse DFT, the normalization factor is ________.

### Q34.
The discrete convolution equation is \(y[n]=\sum_m\) ________.

### Q35.
The Fourier transform of time-domain convolution is the ________ of the two Fourier transforms.

### Q36.
Sampling an appropriately represented continuous signal with an impulse train causes repeated copies of its spectrum at intervals determined by the ________ frequency.

### Q37.
The Nyquist rate for maximum ordinary frequency \(f_{\max}\) is ________.

### Q38.
In an image, frequency is measured in cycles per unit ________.

### Q39.
The base/extent of a 2D image spectrum in the \((\omega_x,\omega_y)\) plane is called its region of ________.

### Q40.
The two-dimensional sampled-image spectrum contains replicas along both the ________ and ________ spatial-frequency axes.

---

# 7. Answer key for the 40 practice questions

## MCQs

| Q | Answer | Reason |
|---:|---|---|
| 1 | B | A grayscale image is a 2D intensity function. |
| 2 | B | Digitization uses sampling and quantization. |
| 3 | A | Sampling discretizes the spatial locations. |
| 4 | D | \(2^6=64\). |
| 5 | C | \(1/0.005=200\) Hz. |
| 6 | B | \(80\pi/(2\pi)=40\) Hz. |
| 7 | C | Nyquist rate = \(2(3)=6\) kHz. |
| 8 | A | \(|100-90|=10\) Hz. |
| 9 | B | The impulse selects \(g(4)\). |
| 10 | C | The interval between impulses is \(T_s\). |
| 11 | B | The coefficient uses \(1/T_0\). |
| 12 | A | A periodic signal is represented by a sum over harmonics. |
| 13 | C | The comb coefficients equal \(1/T_s\). |
| 14 | B | The standard inverse DFT factor is \(1/N\). |
| 15 | B | This is the continuous convolution definition. |
| 16 | C | Time convolution becomes frequency multiplication. |
| 17 | A | Multiplication maps to frequency convolution, with normalization. |
| 18 | B | Sampling replicates the frequency spectrum. |
| 19 | B | The ideal filter isolates the central original band. |
| 20 | B | Overlapping replicas cause aliasing. |
| 21 | B | Image frequency is spatial, measured per unit length. |
| 22 | B | Two spatial coordinates require two frequency coordinates. |
| 23 | B | The replicas form a grid in two dimensions. |
| 24 | B | Apply the Nyquist requirement along both axes. |
| 25 | B | Nearby-pixel predictability is spatial redundancy. |

## Fill in the blanks

| Q | Answer |
|---:|---|
| 26 | \(2^b\) |
| 27 | \(1/T_s\) |
| 28 | \(2\pi f\) |
| 29 | \(g(a)\) |
| 30 | Comb (impulse-train) |
| 31 | \(2\pi/T_0\) |
| 32 | \(1/T_s\) |
| 33 | \(1/N\) |
| 34 | \(h[m]x[n-m]\) |
| 35 | Product / multiplication |
| 36 | Sampling |
| 37 | \(2f_{\max}\) |
| 38 | Length |
| 39 | Support |
| 40 | \(\omega_x\), \(\omega_y\) |

---

# 8. Last-minute checklist

Before the Week 1 exam, make sure you can do all of the following without looking at your notes:

- [ ] Distinguish sampling from quantization.
- [ ] Convert angular frequency to hertz and back.
- [ ] Calculate a sampling frequency from the sampling interval.
- [ ] Apply the Nyquist condition to a 1D signal and separately to the two axes of a 2D image.
- [ ] Use the Dirac delta sifting property.
- [ ] Recognize and write the comb function.
- [ ] Explain the difference between a Fourier transform, Fourier series and DFT.
- [ ] Explain why the Fourier-series coefficients of the ideal impulse train equal \(1/T_s\).
- [ ] Calculate a small discrete convolution.
- [ ] State the convolution theorem with the correct transform convention.
- [ ] Explain why sampling replicates the spectrum.
- [ ] Explain why spectral overlap causes aliasing.
- [ ] Identify the role of an ideal low-pass reconstruction filter.
- [ ] Explain spatial redundancy, boundary contours and video motion tracking.

## Final exam strategy

1. **Solve the original 10 assignment questions independently.** Do not memorise option letters; learn the method.
2. **Practise the 40 questions in this sheet under timed conditions.** Review every mistake and identify whether it came from a formula, concept, sign or arithmetic error.
3. **Revise formulas and units last.** In sampling questions, check whether a frequency is ordinary frequency or angular frequency, and whether the question asks for Hz, rad/s, cycles/unit length or samples/unit length.
4. **Treat the source wording carefully.** The lecture transcript's scanned DFT display appears to omit the standard inverse-transform normalization factor; this sheet uses the conventional mathematically consistent DFT pair and calls out that distinction.

This document is designed as a single Week 1 revision resource, with the main lecture concepts, formula reference, original assignment solutions and additional exam-style practice in one place.
