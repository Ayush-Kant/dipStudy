# NPTEL Digital Image Processing — Week 1 Revision Handbook

> **Course:** Digital Image Processing (DIP)  
> **Instructor:** Prof. P. K. Biswas, IIT Kharagpur  
> **Scope:** Lectures 1–5 and the supplied Week 1 assignment  
> **Goal:** Revise the concepts, recognise the right formula, and learn how to apply it to NPTEL-style questions.

The formulae below use GitHub-rendered LaTeX so equations appear as mathematics instead of plain text. Each important formula has a **when to use it** note and a worked **NPTEL-style example**. The original 10 assignment questions and 40 additional practice questions are included later.

> [!IMPORTANT]
> The 40 additional questions are original practice questions based on the lecture topics. They are **not actual or guaranteed future NPTEL exam questions**. For the original assignment, follow the values stated in the question and check the instructor's explanation if a quiz badge appears inconsistent with those values.

---

## Contents

1. [Week 1 in one picture](#1-week-1-in-one-picture)
2. [Lecture-wise concepts](#2-lecture-wise-concepts)
3. [Formula-by-formula guide: when and how to use each one](#3-formula-by-formula-guide-when-and-how-to-use-each-one)
4. [Quick formula reference](#4-quick-formula-reference)
5. [Original Week 1 assignment: 10 questions with solutions](#5-original-week-1-assignment-10-questions-with-solutions)
6. [40 additional NPTEL-style practice questions](#6-40-additional-nptel-style-practice-questions)
7. [Answer key with explanations](#7-answer-key-with-explanations)
8. [Last-minute revision checklist](#8-last-minute-revision-checklist)

---

# 1. Week 1 in one picture

A real-world image is modelled as a continuous function. A digital image is obtained by sampling its spatial coordinates and quantizing its intensity. Sampling can be represented by multiplying the signal/image by a periodic impulse train. In the frequency domain, this creates repeated copies of the original spectrum. If those copies overlap, aliasing occurs. If the spectrum is band-limited and the sampling rate is high enough, an ideal low-pass filter can isolate the original spectrum.

| Stage | What happens | Exam keywords |
|---|---|---|
| Image model | Intensity varies with position | $f(x,y)$, reflectance, illumination |
| Sampling | Spatial locations become discrete | sampling interval, sampling rate, pixels |
| Quantization | Intensity is mapped to finite levels | bits/pixel, $L=2^b$ |
| Impulse-train model | Samples are represented at regular locations | Dirac delta, comb function |
| Frequency-domain view | Sampling replicates the spectrum | Fourier transform, shifted replicas |
| Reconstruction | A suitable low-pass filter isolates the original band | Nyquist rate, aliasing, region of support |

## The five lectures

| Lecture | Focus | What you should be able to do |
|---|---|---|
| 1 | Introduction to digital image processing | Explain what an image is and distinguish human-oriented improvement from machine-oriented analysis |
| 2 | Applications | Recognise boundary contours, redundancy, inspection and motion tracking |
| 3 | Digitisation, sampling, quantisation and display | Use sampling/bit-depth equations; recognise delta, comb, Fourier series, Fourier transform and DFT |
| 4 | Convolution and reconstruction from samples | Calculate small convolutions; state the convolution theorem; explain spectrum replication |
| 5 | Two-dimensional image sampling | Apply Nyquist limits along both axes; explain the 2D spectrum and low-pass reconstruction |

---

# 2. Lecture-wise concepts

## 2.1 Lectures 1–2 — Digital image processing and applications

A grayscale image is represented as a two-dimensional intensity function:

$$
f(x,y)
$$

- $x,y$ are spatial coordinates.
- $f(x,y)$ is the intensity at the location $(x,y)$.
- **Human-oriented processing** aims to improve visual appearance, for example enhancement or denoising.
- **Machine-oriented processing** aims to extract information for automated tasks, such as inspection, detection, measurement and tracking.
- In industrial inspection, **boundary or edge contours** can reveal an object's outline, corners and dimensions.
- **Spatial redundancy:** nearby pixels often have similar or predictable values.
- **Temporal redundancy:** successive video frames often contain similar information.
- **Coding redundancy:** data representation uses more bits than necessary.
- **Psychovisual redundancy:** information that is less noticeable to human vision.
- Comparing consecutive video frames can reveal moving regions and help track objects.

### Image intensity model

An image intensity may be modelled in the lecture as reflectance multiplied by illumination:

$$
f(x,y)=r(x,y)i(x,y)
$$

Here, $r(x,y)$ is surface reflectance and $i(x,y)$ is illumination.

**Exam distinction:** boundary contours are associated with shape and structural defects; neighbouring-pixel predictability is spatial redundancy; changes between video frames are useful for motion detection/tracking.

## 2.2 Lecture 3 — Sampling, quantisation and image digitisation

Digitisation contains two different operations.

| Operation | What becomes discrete? | Common exam trap |
|---|---|---|
| **Sampling** | Spatial coordinates / sample locations | Do not confuse it with intensity levels |
| **Quantisation** | Intensity values | Do not confuse it with pixel-grid density |

- **Spatial resolution** concerns the number or density of spatial samples.
- **Intensity resolution** concerns how many intensity values can be represented.
- With $b$ bits per pixel, the maximum number of representable intensity levels is $2^b$.
- Conventional 8-bit grayscale has 256 levels, usually numbered 0–255.
- Conventional RGB with 8 bits per channel uses 24 bits per pixel.
- In the lecture's display pipeline, the sampled and quantised representation is processed digitally and then converted for display.

## 2.3 Sampling intervals and frequency units

For time sampling, $T_s$ is measured in seconds and $f_s$ in samples per second (Hz). For image sampling, $\Delta x$ and $\Delta y$ are spatial intervals; the sample densities are samples per unit length.

Do not mix these quantities:

| Quantity | Meaning | Typical unit |
|---|---|---|
| $f$ | Ordinary temporal frequency | cycles/second (Hz) |
| $\omega$ | Angular temporal frequency | rad/s |
| $f_x,f_y$ | Ordinary spatial frequency | cycles/unit length |
| $\omega_x,\omega_y$ | Angular spatial frequency | rad/unit length |
| $f_s$ | Temporal sampling frequency | samples/s |
| $f_{sx},f_{sy}$ | Image sampling densities | samples/unit length |

Ordinary frequency and angular frequency differ by a factor of $2\pi$.

## 2.4 Lecture 3 — Dirac delta and comb function

The shifted Dirac delta, $\delta(t-a)$, is an ideal mathematical impulse. Its most useful property in elementary questions is **sifting**: it selects the value of the function at the impulse location.

A comb function is a regularly spaced, infinite train of impulses. It specifies where sampling takes place. The sampled signal is obtained when each impulse is weighted by the signal's value at that location.

Keep these two objects separate:

- **Comb:** impulse locations only.
- **Sampled signal:** impulses weighted by the original signal samples.

## 2.5 Lecture 3 — Fourier transform, Fourier series and DFT

These are related but different representations.

| Representation | Used for | Key point |
|---|---|---|
| Fourier transform | Aperiodic continuous-time signal (under the usual conditions) | Describes the continuous frequency spectrum |
| Fourier series | Periodic signal | Represents the signal as integer harmonics of a fundamental frequency |
| Discrete Fourier transform (DFT) | A finite sequence of $N$ samples | Produces $N$ discrete frequency-domain values |

For a periodic signal, the Fourier-series coefficient integral can be evaluated over **any one complete period**. The ideal impulse comb is a special case: its coefficients are all equal to the reciprocal of its period.

The standard forward/inverse DFT pair used here places a factor $1/N$ in the inverse transform. The scanned transcript's inverse-DFT display appears to omit this normalisation factor, so the conventional pair is shown explicitly below.

## 2.6 Lecture 4 — Convolution

Convolution combines two signals. In continuous time, it uses an integral; for discrete sequences, it uses a sum. One useful interpretation is to reverse and shift one signal, multiply the overlapping values, and integrate or sum.

Important identities:

- Time-domain convolution corresponds to frequency-domain multiplication.
- Time-domain multiplication corresponds to frequency-domain convolution, with a factor determined by the Fourier-transform convention.
- Convolution with a shifted impulse shifts a signal.
- Convolution with an impulse train creates shifted copies of the signal.

## 2.7 Lectures 4–5 — Spectrum replication, aliasing and reconstruction

Sampling multiplies a signal by an impulse train in the spatial/time domain. Under the Fourier-transform relationship, this creates repeated shifted copies of the original spectrum.

- **No overlap:** the original spectrum can, under the ideal band-limited assumptions, be separated by a low-pass reconstruction filter.
- **Overlap:** spectral replicas interfere; this is aliasing.
- **Nyquist rate:** twice the highest ordinary frequency present in a band-limited signal.
- **Nyquist frequency:** half the chosen sampling frequency.
- **Region of support:** the region in the frequency plane where a spectrum may be nonzero.

For a 2D image, examine the horizontal and vertical spatial frequencies separately. A sufficient component-wise condition must be satisfied along **both** axes.

## 2.8 Lecture 5 — Sampling density demonstration

The lecture compares example images displayed at 50, 100, 600 and 1200 dots per inch. Low sampling density loses fine detail and makes edges look rough; denser sampling gives a smoother representation. The shown difference between 600 and 1200 dots per inch is comparatively smaller in that example. Treat this as an illustration from the lecture, not as a universal threshold for all images and displays.

---

# 3. Formula-by-formula guide: when and how to use each one

Each entry gives the formula, when it is useful, and a worked question in the style of the concepts covered in Week 1.

## F1. Image intensity = reflectance × illumination

**Formula**

$$
f(x,y)=r(x,y)i(x,y)
$$

**Use it when:** a question asks about the lecture's image-formation model or asks you to find intensity when reflectance and illumination are given.

**NPTEL-style question:** At one image location, reflectance is $0.6$ and illumination is $120$. Using the stated model, find the intensity.

**How to solve:** Substitute both values into $f=ri$.

$$
f=0.6\times120=72
$$

**Answer:** $72$ in the model's intensity units.

## F2. Number of quantisation levels and bits

**Formulae**

$$
L=2^b
$$

$$
b=\log_2 L
$$

Here, $b$ is the number of bits per pixel and $L$ is the number of representable intensity levels.

**Use it when:** a question gives bit depth and asks for levels, or gives a power-of-two number of levels and asks how many bits are needed.

**NPTEL-style question A:** How many levels can 6 bits represent?

$$
L=2^6=64
$$

**Answer:** 64 levels.

**NPTEL-style question B:** How many bits are required for 256 levels?

$$
b=\log_2 256=8
$$

**Answer:** 8 bits.

**Fast exam shortcut:** memorise $2^1=2$, $2^4=16$, $2^8=256$, and $2^{10}=1024$.

## F3. Temporal sampling frequency

**Formula**

$$
f_s=\frac{1}{T_s}
$$

Here, $T_s$ is the time between successive samples in seconds, while $f_s$ is the sampling frequency in samples/second.

**Use it when:** a question gives a sampling interval and asks for the sampling frequency, or when comparing how a changed interval affects sample rate.

**NPTEL-style question:** A signal is sampled once every $0.002$ seconds. Find $f_s$.

**How to solve:** Take the reciprocal of the interval.

$$
f_s=\frac{1}{0.002}=500\text{ Hz}
$$

**Answer:** 500 samples/s.

**Common trap:** convert milliseconds to seconds first. For example, $2$ ms is $0.002$ s, not $2$ s.

## F4. Spatial sampling densities of an image

**Formulae**

$$
f_{sx}=\frac{1}{\Delta x},
\qquad
f_{sy}=\frac{1}{\Delta y}
$$

Here, $\Delta x,\Delta y$ are the spacings between samples along the two axes. These expressions give sample density, not the image's highest content frequency.

**Use it when:** the problem gives horizontal/vertical pixel spacing and asks how densely the image is sampled.

**NPTEL-style question:** An image is sampled every $0.01$ unit along $x$ and every $0.02$ unit along $y$. Find the sampling densities.

$$
f_{sx}=\frac{1}{0.01}=100
$$

$$
f_{sy}=\frac{1}{0.02}=50
$$

**Answer:** 100 samples/unit along $x$, and 50 samples/unit along $y$.

## F5. Ordinary frequency and angular frequency

**Formulae**

$$
\omega=2\pi f
\qquad\Longleftrightarrow\qquad
f=\frac{|\omega|}{2\pi}
$$

For a sinusoid $\cos(\omega t+\phi)$ or $\sin(\omega t+\phi)$, the ordinary frequency is $|\omega|/(2\pi)$ cycles/s. Use the absolute value for the non-negative frequency of a real sinusoid.

**Use it when:** a sine or cosine has a coefficient multiplying $t$ and you need the frequency in Hz.

**NPTEL-style question:** Find the frequency of $x(t)=\cos(350\pi t)$.

**How to solve:** The angular frequency is $350\pi$ rad/s.

$$
f=\frac{350\pi}{2\pi}=175\text{ Hz}
$$

**Answer:** 175 Hz.

**For images:** the same $2\pi$ conversion applies to spatial frequencies, with units of rad/unit length and cycles/unit length rather than rad/s and Hz.

## F6. Dirac delta sifting property

**Formula**

$$
\int_{-\infty}^{\infty}g(t)\delta(t-a)\,dt=g(a)
$$

**Use it when:** an integral contains a shifted delta function. Do not try to integrate the full ordinary function; the impulse selects its value at $t=a$.

**NPTEL-style question:** Evaluate

$$
\int_{-\infty}^{\infty}(t^2+1)\delta(t-2)\,dt
$$

**How to solve:** Substitute $t=2$ into $g(t)=t^2+1$.

$$
g(2)=2^2+1=5
$$

**Answer:** 5.

## F7. Comb function (periodic impulse train)

**Formula**

$$
c(t)=\sum_{m=-\infty}^{\infty}\delta(t-mT_s)
$$

**Use it when:** asked to identify the comb function, its spacing, or its relationship to sampling.

**NPTEL-style question:** If adjacent impulses in a comb are separated by $0.01$ s, what is the corresponding sampling frequency?

**How to solve:** The period/spacing is $T_s=0.01$ s. Use the reciprocal.

$$
f_s=\frac{1}{T_s}=\frac{1}{0.01}=100\text{ Hz}
$$

**Answer:** 100 samples/s.

**Concept check:** the comb is unweighted; it marks locations. The sampled signal below includes the original signal values.

## F8. Signal sampled using an impulse train

**Formula**

$$
x_s(t)=x(t)c(t)
=\sum_{m=-\infty}^{\infty}x(mT_s)\delta(t-mT_s)
$$

**Use it when:** asked to write the mathematical impulse-train representation of a sampled signal, or to distinguish the comb from the sampled signal.

**NPTEL-style question:** A signal has $x(0)=2$ and $x(T_s)=5$. Write the contributions from the impulses at $t=0$ and $t=T_s$.

**How to solve:** Weight each impulse by the sample value at its location.

$$
x_s(t)=2\delta(t)+5\delta(t-T_s)+\cdots
$$

**Answer:** each impulse has the amplitude of the corresponding original sample.

## F9. Continuous-time Fourier transform (FT)

**Formula — angular-frequency convention**

$$
X(\omega)=\int_{-\infty}^{\infty}x(t)e^{-j\omega t}\,dt
$$

**Use it when:** a question asks for the transform definition, the meaning of $X(\omega)$, or the frequency-domain representation of a simple signal.

**NPTEL-style question:** What is the Fourier transform of $\delta(t)$ under this convention?

**How to solve:** By the delta sifting property, the integral evaluates the exponential at $t=0$.

$$
\mathcal{F}\{\delta(t)\}
=\int_{-\infty}^{\infty}\delta(t)e^{-j\omega t}\,dt
=e^0=1
$$

**Answer:** $X(\omega)=1$ for all $\omega$.

## F10. Fourier series for a periodic signal

**Formulae**

$$
v(t)=\sum_{n=-\infty}^{\infty}C_ne^{jn\omega_0t}
$$

$$
\omega_0=\frac{2\pi}{T_0}
$$

$$
C_n=\frac{1}{T_0}\int_{\text{one period}}v(t)e^{-jn\omega_0t}\,dt
$$

**Use it when:** a question asks for the fundamental angular frequency, the coefficient formula, or the distinction between Fourier series and Fourier transform.

**NPTEL-style question:** A periodic signal has period $T_0=4$ s. Find its fundamental angular frequency.

$$
\omega_0=\frac{2\pi}{4}=\frac{\pi}{2}\text{ rad/s}
$$

**Answer:** $\pi/2$ rad/s.

**Coefficient reminder:** the integral spans one complete period; the factor outside the integral is $1/T_0$.

## F11. Fourier-series coefficients of the ideal impulse comb

**Formula**

$$
C_n=\frac{1}{T_s}
$$

for every integer harmonic index $n$, for the ideal unit-impulse comb with period $T_s$.

**How this follows in the lecture's convention:** one period has an impulse at the origin, so the exponential is evaluated at zero and equals 1.

$$
C_n=\frac{1}{T_s}
\int_{\text{one period}}\delta(t)e^{-jn\omega_0t}\,dt
=\frac{1}{T_s}
$$

**Use it when:** asked for the Fourier-series coefficients of the periodic impulse train. Do not apply this result to every arbitrary periodic waveform.

**NPTEL-style question:** An ideal unit-impulse comb has period $T_s=0.02$ s. What is $C_n$?

$$
C_n=\frac{1}{0.02}=50
$$

**Answer:** every integer-indexed coefficient equals 50 under this idealised model.

## F12. Discrete Fourier transform (DFT) and inverse DFT

**Formulae — standard convention**

$$
X[k]=\sum_{n=0}^{N-1}x[n]e^{-j2\pi nk/N}
$$

$$
x[n]=\frac{1}{N}\sum_{k=0}^{N-1}X[k]e^{j2\pi nk/N}
$$

**Use it when:** asked to identify the forward DFT, the inverse DFT, or the normalisation factor in the inverse transform.

**NPTEL-style question:** In the standard $N$-point inverse DFT shown above, what factor appears before the sum?

**Answer:** $1/N$.

**Useful check:** if $X[k]=1$ for every $k=0,\ldots,N-1$, then inverse DFT reconstruction yields $x[0]=1$ and $x[n]=0$ for $n=1,\ldots,N-1$.

> [!NOTE]
> The supplied scanned transcript appears to omit the $1/N$ factor in its inverse-DFT display. This revision sheet uses the standard inverse DFT paired with the unnormalised forward DFT above; follow any explicitly stated convention if a question defines a different pair.

## F13. Continuous-time convolution

**Formula**

$$
y(t)=(h*x)(t)=\int_{-\infty}^{\infty}h(\tau)x(t-\tau)\,d\tau
$$

**Use it when:** asked for the definition of convolution, or when solving continuous-signal overlap problems.

**How to interpret it:**
1. Reverse one signal in time as required by the expression.
2. Shift it by the output time.
3. Multiply the signals over their overlap.
4. Integrate the product over the full domain.

**NPTEL-style conceptual question:** Which operation combines two time-domain signals and is represented by this integral?

**Answer:** continuous-time convolution.

## F14. Discrete convolution

**Formula**

$$
y[n]=\sum_{m=-\infty}^{\infty}h[m]x[n-m]
$$

**Use it when:** a finite sequence question gives a few non-zero samples and asks for a particular output $y[n]$. Only terms where both sequence values are non-zero contribute.

**NPTEL-style question:** Let $x[0]=2$, $x[1]=3$, $h[0]=4$, and $h[1]=1$, with all other samples zero. Find $y[1]$.

**How to solve:** From $y[1]=\sum_m h[m]x[1-m]$, the two non-zero contributions are $h[0]x[1]$ and $h[1]x[0]$.

$$
y[1]=4(3)+1(2)=14
$$

**Answer:** $y[1]=14$.

## F15. Convolution with a shifted impulse or impulse train

**Formulae**

$$
x[n]*\delta[n-n_0]=x[n-n_0]
$$

For a unit impulse train with impulses spaced every $M$ samples,

$$
c[n]=\sum_{k=-\infty}^{\infty}\delta[n-kM]
$$

and

$$
y[n]=(x*c)[n]=\sum_{k=-\infty}^{\infty}x[n-kM]
$$

**Use it when:** an assignment describes a sequence convolved with a regularly spaced impulse train. Find which shifted copy can contribute to the requested index.

**NPTEL-style question:** Suppose $x[-2]=2$ and is zero outside the given sequence range. The unit impulse train has spacing $M=9$. Find $y[7]$.

**How to solve:** Use $y[7]=\sum_kx[7-9k]$. For $k=1$, the argument is $7-9=-2$, so this contributes 2. Other terms are outside the non-zero range.

$$
y[7]=x[-2]=2
$$

**Answer:** 2.

## F16. Convolution theorem

**Formula**

$$
\mathcal{F}\{h*x\}=H(\omega)X(\omega)
$$

**Use it when:** asked what time-domain convolution becomes in the frequency domain, or asked how to simplify a system calculation in the frequency domain.

**NPTEL-style question:** If $h(t)$ and $x(t)$ are convolved in time, do their Fourier transforms add or multiply?

**Answer:** they multiply point by point: $Y(\omega)=H(\omega)X(\omega)$.

**Memory cue:** *convolution in time ↔ multiplication in frequency.*

## F17. Time-domain multiplication property

**Formula — same angular-frequency convention**

$$
\mathcal{F}\{h(t)x(t)\}
=\frac{1}{2\pi}\,[H*X](\omega)
$$

**Use it when:** a question asks for the transform-domain operation corresponding to multiplication in time. Keep the factor $1/(2\pi)$ for the convention used in this sheet.

**NPTEL-style question:** If two time-domain functions are multiplied, what operation combines their Fourier transforms?

**Answer:** frequency-domain convolution, with the convention-dependent factor $1/(2\pi)$ shown above.

**Exam trap:** do not reverse the two dual properties. Time convolution becomes frequency multiplication; time multiplication becomes frequency convolution.

## F18. Fourier transform of the impulse comb and sampled spectrum

**Formulae**

$$
\Omega_s=\frac{2\pi}{T_s}
$$

$$
C(\omega)=\frac{2\pi}{T_s}
\sum_{n=-\infty}^{\infty}\delta(\omega-n\Omega_s)
$$

$$
X_s(\omega)=\frac{1}{T_s}
\sum_{n=-\infty}^{\infty}X(\omega-n\Omega_s)
$$

**Use it when:** a question asks how sampling changes the frequency spectrum, where the repeated copies are centred, or how far apart the replicas are.

**NPTEL-style question:** A signal is sampled at $f_s=100$ Hz. At what interval are the spectrum replicas spaced in ordinary frequency, and what is the sampling angular frequency?

**How to solve:**

$$
\text{Replica spacing}=f_s=100\text{ Hz}
$$

$$
\Omega_s=2\pi f_s=200\pi\text{ rad/s}
$$

**Answer:** replicas are spaced by 100 Hz; $\Omega_s=200\pi$ rad/s.

**Interpretation:** the replica indexed by $n$ is shifted by $n\Omega_s$ from the original spectrum.

## F19. One-dimensional Nyquist condition

**Formulae**

$$
\text{Nyquist rate}=2f_{\max}
$$

$$
f_s>2f_{\max}
$$

The course uses the strict inequality for ideal reconstruction.

**Use it when:** a question asks for the minimum required sampling rate or tests whether a proposed sampling frequency is sufficient.

**NPTEL-style question:** A band-limited signal contains no frequency above 3 kHz. What sampling frequency satisfies the course's strict ideal-reconstruction condition?

**How to solve:**

$$
f_s>2(3\text{ kHz})=6\text{ kHz}
$$

**Answer:** choose a rate strictly greater than 6 kHz under the lecture's convention.

**Do not confuse:**
- Nyquist **rate** is twice the highest signal frequency.
- Nyquist **frequency** for a chosen sample rate is $f_s/2$.

## F20. Folding a frequency into the baseband (aliasing)

A useful baseband-folding expression for a real sinusoid sampled at rate $f_s$ is:

$$
f_{\text{alias}}
=\left|\left((f+f_s/2)\bmod f_s\right)-f_s/2\right|
$$

It returns a non-negative aliased frequency in the interval from 0 to $f_s/2$. The lecture's replica picture can also be used to find the closest equivalent component in the baseband.

**Use it when:** a sinusoidal component lies above the Nyquist frequency and the problem asks what frequency appears after sampling/reconstruction.

**NPTEL-style question:** A 175 Hz sinusoid is sampled at 200 Hz. Find its baseband alias.

**How to solve:**

$$
f_{\text{alias}}
=\left|\left((175+100)\bmod 200\right)-100\right|
$$

$$
=\left|75-100\right|=25\text{ Hz}
$$

**Answer:** 25 Hz.

**Important:** aliasing is a sampling effect, not a new original component. Once the replicas overlap, ideal low-pass filtering alone generally cannot recover the original signal uniquely.

## F21. Ideal low-pass reconstruction condition

If the original signal is band-limited to $[-\Omega_m,\Omega_m]$, an ideal reconstruction cutoff can separate its central spectrum from the nearest replica when:

$$
\Omega_m<\Omega_c<\Omega_s-\Omega_m
$$

This interval can exist when:

$$
\Omega_s>2\Omega_m
$$

**Use it when:** a question asks whether a low-pass reconstruction cutoff can be chosen between the original signal's highest angular frequency and the nearest replica.

**NPTEL-style question:** Given $\Omega_m=50$ rad/s and $\Omega_s=140$ rad/s, state an allowable range for $\Omega_c$.

**How to solve:**

$$
50<\Omega_c<140-50
$$

$$
50<\Omega_c<90\text{ rad/s}
$$

**Answer:** any ideal cutoff strictly between 50 and 90 rad/s meets this interval condition.

## F22. Two-dimensional sampled image

**Formula**

$$
f_s(x,y)=
\sum_{m=-\infty}^{\infty}\sum_{n=-\infty}^{\infty}
f(m\Delta x,n\Delta y)
\delta(x-m\Delta x)\delta(y-n\Delta y)
$$

**Use it when:** asked to express how a continuous image is sampled on a rectangular 2D grid, or to distinguish the two spatial sample spacings.

**NPTEL-style conceptual question:** Does 2D sampling occur along one coordinate or both?

**Answer:** both; the impulses occur at grid positions $(m\Delta x,n\Delta y)$ and are weighted by $f(m\Delta x,n\Delta y)$.

## F23. Two-dimensional angular sampling frequencies

**Formulae**

$$
\Omega_{sx}=\frac{2\pi}{\Delta x},
\qquad
\Omega_{sy}=\frac{2\pi}{\Delta y}
$$

**Use it when:** a question gives the image sample spacings and asks for angular spatial sampling frequencies.

**NPTEL-style question:** If $\Delta x=0.5$ unit, find $\Omega_{sx}$.

$$
\Omega_{sx}=\frac{2\pi}{0.5}=4\pi
\text{ rad/unit length}
$$

**Answer:** $4\pi$ rad/unit length.

## F24. Spectrum of a sampled 2D image

**Formula**

$$
F_s(\omega_x,\omega_y)=
\frac{1}{\Delta x\Delta y}
\sum_{m=-\infty}^{\infty}
\sum_{n=-\infty}^{\infty}
F(\omega_x-m\Omega_{sx},\omega_y-n\Omega_{sy})
$$

**Use it when:** asked what sampling does to a 2D spatial-frequency spectrum. The formula says that copies of $F$ are shifted along both axes to form a grid of replicas.

**NPTEL-style question:** In which directions are the replicas shifted?

**Answer:** by integer multiples of $\Omega_{sx}$ in $\omega_x$ and integer multiples of $\Omega_{sy}$ in $\omega_y$.

**Interpretation:** the factor $1/(\Delta x\Delta y)$ scales the replicas under the Fourier convention used here; their positions are controlled by the two angular sampling frequencies.

## F25. Component-wise Nyquist condition for images

**Formulae — ordinary spatial frequencies**

$$
f_{sx}>2f_{x,\max}
$$

$$
f_{sy}>2f_{y,\max}
$$

**Equivalent angular-frequency form**

$$
\Omega_{sx}>2\Omega_{xm},
\qquad
\Omega_{sy}>2\Omega_{ym}
$$

**Use it when:** the image contains spatial sinusoids and the question asks for the necessary sampling densities in the horizontal and vertical directions.

**NPTEL-style question from the assignment:** Given

$$
f(x,y)=\cos(20\pi x+60\pi y)+\sin(80\pi x-10\pi y),
$$

find the required sampling densities.

**Step 1 — Rewrite using $2\pi$.**

$$
\cos(2\pi(10x+30y))
+\sin(2\pi(40x-5y))
$$

The largest absolute $x$-frequency is $40$ cycles/unit; the largest absolute $y$-frequency is $30$ cycles/unit.

**Step 2 — Double each maximum.**

$$
f_{sx}>2(40)=80
$$

$$
f_{sy}>2(30)=60
$$

**Answer:** $f_{sx}>80$ and $f_{sy}>60$ samples/unit, matching the result derived from the stated signal.

## F26. Region of support

**Concept rather than a separate calculation formula**

The **region of support** is the region in the $(\omega_x,\omega_y)$ plane where the original image spectrum can be non-zero.

**Use it when:** a question asks which region should be passed during ideal reconstruction or what spectral overlap means geometrically.

**NPTEL-style question:** What should an ideal 2D low-pass reconstruction filter retain if the spectral replicas do not overlap?

**Answer:** the central original spectral region around the origin while rejecting the replicated copies.

---

# 4. Quick formula reference

Use this section for last-minute scanning. For worked applications, return to the matching F-number in Section 3.

| No. | Topic | Formula / result |
|---:|---|---|
| F1 | Image intensity model | $f(x,y)=r(x,y)i(x,y)$ |
| F2 | Quantisation levels | $L=2^b$ |
| F2 | Bits from levels | $b=\log_2 L$ |
| F3 | Temporal sampling | $f_s=1/T_s$ |
| F4 | Image sampling density | $f_{sx}=1/\Delta x,\; f_{sy}=1/\Delta y$ |
| F5 | Angular ↔ ordinary frequency | $\omega=2\pi f,\; f=|\omega|/(2\pi)$ |
| F6 | Delta sifting | $\int g(t)\delta(t-a)\,dt=g(a)$ |
| F7 | Comb | $c(t)=\sum_m\delta(t-mT_s)$ |
| F8 | Sampled signal | $x_s(t)=\sum_mx(mT_s)\delta(t-mT_s)$ |
| F9 | Fourier transform | $X(\omega)=\int x(t)e^{-j\omega t}\,dt$ |
| F10 | Fundamental angular frequency | $\omega_0=2\pi/T_0$ |
| F10 | Fourier-series coefficient | $C_n=(1/T_0)\int_{\text{one period}}v(t)e^{-jn\omega_0t}\,dt$ |
| F11 | Comb Fourier-series coefficient | $C_n=1/T_s=f_s$ |
| F12 | Forward DFT | $X[k]=\sum_{n=0}^{N-1}x[n]e^{-j2\pi nk/N}$ |
| F12 | Inverse DFT | $x[n]=(1/N)\sum_{k=0}^{N-1}X[k]e^{j2\pi nk/N}$ |
| F13 | Continuous convolution | $y(t)=\int h(\tau)x(t-\tau)\,d\tau$ |
| F14 | Discrete convolution | $y[n]=\sum_mh[m]x[n-m]$ |
| F15 | Shifted impulse | $x[n]*\delta[n-n_0]=x[n-n_0]$ |
| F15 | Impulse train spacing $M$ | $y[n]=\sum_kx[n-kM]$ |
| F16 | Convolution theorem | $\mathcal F\{h*x\}=HX$ |
| F17 | Multiplication theorem | $\mathcal F\{hx\}=(1/2\pi)(H*X)$ |
| F18 | Sampling angular frequency | $\Omega_s=2\pi/T_s=2\pi f_s$ |
| F18 | Sampled 1D spectrum | $X_s(\omega)=(1/T_s)\sum_nX(\omega-n\Omega_s)$ |
| F19 | 1D Nyquist condition | $f_s>2f_{\max}$ |
| F20 | Baseband alias frequency | $f_{\text{alias}}=\left|\left((f+f_s/2)\bmod f_s\right)-f_s/2\right|$ |
| F21 | Ideal reconstruction cutoff | $\Omega_m<\Omega_c<\Omega_s-\Omega_m$ |
| F22 | Sampled image | $f_s(x,y)=\sum_{m,n}f(m\Delta x,n\Delta y)\delta(x-m\Delta x)\delta(y-n\Delta y)$ |
| F23 | 2D angular sampling rates | $\Omega_{sx}=2\pi/\Delta x,\; \Omega_{sy}=2\pi/\Delta y$ |
| F24 | Sampled 2D spectrum | $F_s=(1/(\Delta x\Delta y))\sum_{m,n}F(\omega_x-m\Omega_{sx},\omega_y-n\Omega_{sy})$ |
| F25 | 2D Nyquist condition | $f_{sx}>2f_{x,\max},\; f_{sy}>2f_{y,\max}$ |

---

# 5. Original Week 1 assignment: 10 questions with solutions

These are the 10 assignment questions previously extracted from the supplied Week 1 quiz PDF. They are formatted here as revision questions with their working. For question wording and options, use the original assignment PDF alongside this summary.

## Q1. Required sampling densities for a 2D image

**Question**

Given

$$
f(x,y)=\cos(20\pi x+60\pi y)+\sin(80\pi x-10\pi y),
$$

find the required sampling densities along $x$ and $y$.

**Solution**

Rewrite the signal using $2\pi$:

$$
f(x,y)=\cos(2\pi(10x+30y))
+\sin(2\pi(40x-5y))
$$

Therefore:

- Maximum absolute $x$-frequency: $f_{x,\max}=40$ cycles/unit.
- Maximum absolute $y$-frequency: $f_{y,\max}=30$ cycles/unit.

Apply the component-wise Nyquist condition:

$$
f_{sx}>2(40)=80
$$

$$
f_{sy}>2(30)=60
$$

**Answer:** option D: $f_{sx}>80$ and $f_{sy}>60$ samples/unit.

## Q2. Aliasing and ideal low-pass reconstruction

**Question**

$$
x(t)=\cos(100\pi t)+\cos(350\pi t)
$$

is sampled at 200 Hz and reconstructed using an ideal low-pass filter with cutoff 100 Hz. Which frequency components pass?

**Solution**

Convert angular frequency to ordinary frequency:

$$
f_1=\frac{100\pi}{2\pi}=50\text{ Hz}
$$

$$
f_2=\frac{350\pi}{2\pi}=175\text{ Hz}
$$

The Nyquist frequency for $f_s=200$ Hz is:

$$
f_N=\frac{f_s}{2}=100\text{ Hz}
$$

The 50 Hz component is below Nyquist. The 175 Hz component folds to 25 Hz:

$$
f_{\text{alias}}=|175-200|=25\text{ Hz}
$$

Both 25 Hz and 50 Hz are below the stated 100 Hz ideal low-pass cutoff.

**Answer:** option B: 25 Hz and 50 Hz.

## Q3. Sequence convolved with a unit impulse train

**Question**

The sequence has $x[-2]=2$, $x[-1]=5$, $x[0]=7$, $x[1]=9$, $x[2]=3$, and is zero elsewhere. Convolve it with a unit impulse train whose impulses are spaced nine samples apart. Find $y[7]$.

**Solution**

For spacing $M=9$:

$$
y[n]=\sum_kx[n-9k]
$$

At $n=7$:

$$
y[7]=\sum_kx[7-9k]
$$

For $k=1$, $7-9=-2$, so the contribution is $x[-2]=2$. Other terms are outside the non-zero range.

**Answer:** option B: 2.

## Q4. Meaning of the comb function

**Question**

What does the comb function represent?

**Solution**

$$
c(t)=\sum_{m=-\infty}^{\infty}\delta(t-mT_s)
$$

It represents an infinite, one-dimensional array of equally spaced Dirac impulses.

**Answer:** option C: an infinite array of regularly spaced Dirac delta functions.

## Q5. Convolution theorem

**Question**

What is the frequency-domain equivalent of convolution in the time domain?

**Solution**

$$
\mathcal{F}\{x(t)*h(t)\}=X(\omega)H(\omega)
$$

**Answer:** option B: multiplication of the corresponding frequency spectra.

## Q6. Delta-function sifting

**Question**

Evaluate:

$$
\int_{-\infty}^{\infty}f(t)\delta(t-2)\,dt
$$

**Solution**

The shifted impulse selects the function's value at $t=2$.

$$
\int_{-\infty}^{\infty}f(t)\delta(t-2)\,dt=f(2)
$$

**Answer:** option B: $f(2)$.

## Q7. Effect of sampling in the frequency domain

**Question**

What happens to the spectrum of a continuous band-limited signal when it is sampled?

**Solution**

Sampling multiplies the signal by a periodic impulse train in the signal domain. The corresponding frequency-domain operation creates periodically shifted copies of the original spectrum.

$$
X_s(\omega)=\frac{1}{T_s}
\sum_{n=-\infty}^{\infty}X(\omega-n\Omega_s)
$$

**Answer:** option B: the spectrum is replicated at intervals determined by the sampling frequency.

## Q8. Automated refractory-brick inspection

**Question**

Which image feature helps identify structural defects such as missing corners or dimensional irregularities?

**Solution**

Boundary or edge contours reveal the outline, corners and geometry of the object.

**Answer:** option B: boundary/edge contours.

## Q9. Predictability between neighbouring pixels

**Question**

What type of redundancy is present when a pixel can be predicted from neighbouring pixels?

**Solution**

Predictability among nearby spatial locations is spatial (pixel) redundancy.

**Answer:** option C: spatial/pixel redundancy.

## Q10. Consecutive video frames

**Question**

Why analyse consecutive frames in security surveillance or medical organ tracking?

**Solution**

Frame-to-frame changes help identify moving regions and follow an object over time.

**Answer:** option B: detect and track moving parts/targets against the background.

> [!NOTE]
> The working above follows the numerical values stated in each question. If an answer badge in a supplied screenshot appears inconsistent with those values, verify it against the original quiz page or instructor explanation rather than memorising the badge without checking the calculation.

---

# 6. 40 additional NPTEL-style practice questions

These questions are new practice material based on the topics covered in Week 1. Try answering them before opening the answer key.

## Section A — MCQs (Q1–Q25)

### Q1. Image representation

A grayscale image is most directly represented as:

A. A one-dimensional scalar only  
B. A two-dimensional intensity function $f(x,y)$  
C. A list of Fourier coefficients only  
D. A probability distribution only

### Q2. Digitisation

Which pair represents the two principal stages of image digitisation?

A. Filtering and segmentation  
B. Sampling and quantisation  
C. Compression and display  
D. Convolution and differentiation

### Q3. Sampling versus quantisation

Sampling primarily discretises:

A. Spatial locations  
B. Intensity levels  
C. Fourier coefficients only  
D. Display brightness only

### Q4. Intensity levels

How many possible levels can be represented using 6 bits per pixel?

A. 6  
B. 12  
C. 32  
D. 64

### Q5. Sampling interval

A signal is sampled every $0.005$ seconds. What is the sampling frequency?

A. 50 Hz  
B. 100 Hz  
C. 200 Hz  
D. 500 Hz

### Q6. Angular-frequency conversion

The frequency of $\cos(80\pi t)$ is:

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

The integral $\int_{-\infty}^{\infty}g(t)\delta(t-4)\,dt$ equals:

A. $g(0)$  
B. $g(4)$  
C. $g(-4)$  
D. 4

### Q10. Comb function

In $\sum_m\delta(t-mT_s)$, the distance between adjacent impulses is:

A. $2T_s$  
B. $1/T_s$  
C. $T_s$  
D. $T_s^2$

### Q11. Fourier-series coefficient

The coefficient formula for a periodic signal with period $T_0$ includes the factor:

A. $T_0$  
B. $1/T_0$  
C. $2\pi T_0$  
D. $1/(2\pi)$ only

### Q12. Fourier-series representation

Which describes a Fourier series for a periodic signal?

A. A sum over integer harmonics  
B. A sum over spatial pixels only  
C. A single DC value  
D. A probability density function

### Q13. Comb coefficients

For the ideal unit-impulse comb with period $T_s$, the complex Fourier-series coefficients are:

A. All zero  
B. $n/T_s$  
C. $1/T_s$ for every integer $n$  
D. Only the coefficient for $n=1$ is non-zero

### Q14. Inverse DFT

For the standard $N$-point inverse DFT used in this sheet, the normalisation factor is:

A. $N$  
B. $1/N$  
C. $2\pi/N$  
D. $1/(2\pi)$

### Q15. Continuous convolution

Which is the standard continuous-time convolution formula?

A. $y(t)=h(t)x(t)$  
B. $y(t)=\int h(\tau)x(t-\tau)\,d\tau$  
C. $y(t)=h(t)+x(t)$  
D. $y(t)=x(t)/h(t)$

### Q16. Convolution theorem

Time-domain convolution corresponds to what frequency-domain operation?

A. Addition  
B. Differentiation only  
C. Multiplication  
D. Quantisation

### Q17. Time multiplication

Under the Fourier convention in this sheet, time-domain multiplication corresponds to:

A. Frequency-domain convolution with the appropriate convention factor  
B. Frequency-domain subtraction  
C. Sampling with no spectrum change  
D. Only a DC component

### Q18. Spectrum replication

What is the frequency-domain result of impulse-train sampling?

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

A. Non-overlapping spectral copies  
B. Overlap of replicated spectra after sampling  
C. Perfect sampling  
D. Intensity quantisation alone

### Q21. Spatial frequency units

Image spatial frequency is conventionally expressed in:

A. Cycles per second only  
B. Cycles per unit length  
C. Bits per pixel  
D. Pixels per frame only

### Q22. Two-dimensional image spectrum

For an image $f(x,y)$, its two-dimensional frequency spectrum is represented as:

A. A function of one frequency variable only in all cases  
B. $F(\omega_x,\omega_y)$  
C. $F(t)$ only  
D. $F(b)$

### Q23. Two-dimensional sampling

The spectral copies of a sampled 2D image repeat:

A. Along only one axis  
B. Along both spatial-frequency axes  
C. Only at the origin  
D. Only in the spatial domain

### Q24. 2D reconstruction condition

For an image with maximum ordinary spatial frequencies $f_{x,\max}$ and $f_{y,\max}$, the component-wise sampling requirements are:

A. $f_{sx}>f_{x,\max}$ and $f_{sy}>f_{y,\max}$  
B. $f_{sx}>2f_{x,\max}$ and $f_{sy}>2f_{y,\max}$  
C. $f_{sx}=f_{sy}=0$  
D. Only the vertical sampling rate matters

### Q25. Redundancy

Predictability among neighbouring pixel values is most closely related to:

A. Temporal redundancy  
B. Spatial redundancy  
C. Motion tracking  
D. Fourier-series period

## Section B — Fill in the blanks (Q26–Q40)

### Q26
The number of possible intensity levels for a pixel represented by $b$ bits is ________.

### Q27
If the sampling interval is $T_s$, the sampling frequency is ________.

### Q28
The relationship between angular frequency and ordinary frequency is $\omega=$ ________.

### Q29
The integral $\int_{-\infty}^{\infty}g(t)\delta(t-a)\,dt$ evaluates to ________.

### Q30
A regular infinite train of equally spaced impulses is called a ________ function.

### Q31
The Fourier-series fundamental angular frequency for period $T_0$ is ________.

### Q32
The complex Fourier-series coefficient of the ideal unit-impulse comb of period $T_s$ is ________ for every integer harmonic index.

### Q33
In the standard inverse DFT, the normalisation factor is ________.

### Q34
The discrete convolution equation is $y[n]=\sum_m$ ________.

### Q35
The Fourier transform of a time-domain convolution is the ________ of the two Fourier transforms.

### Q36
Sampling with an impulse train produces repeated copies of the spectrum at intervals determined by the ________ frequency.

### Q37
The Nyquist rate for a maximum ordinary frequency $f_{\max}$ is ________.

### Q38
Image spatial frequency is measured in cycles per unit ________.

### Q39
The region in the $(\omega_x,\omega_y)$ plane where the original image spectrum can be non-zero is called its region of ________.

### Q40
The 2D sampled-image spectrum contains replicas along both the ________ and ________ spatial-frequency axes.

---

# 7. Answer key with explanations

## MCQs (Q1–Q25)

| Q | Answer | Why |
|---:|:---:|---|
| 1 | B | A grayscale image is represented as a 2D intensity function. |
| 2 | B | Digitisation has sampling and quantisation stages. |
| 3 | A | Sampling discretises the spatial locations. |
| 4 | D | $2^6=64$ possible levels. |
| 5 | C | $f_s=1/0.005=200$ Hz. |
| 6 | B | $80\pi/(2\pi)=40$ Hz. |
| 7 | C | The Nyquist rate is $2(3)=6$ kHz. |
| 8 | A | $f_s=100$ Hz; a 90 Hz component folds to $|100-90|=10$ Hz. |
| 9 | B | The shifted delta selects $g(4)$. |
| 10 | C | Adjacent impulses are separated by $T_s$. |
| 11 | B | The coefficient formula contains $1/T_0$. |
| 12 | A | A periodic signal is represented as a sum of integer harmonics. |
| 13 | C | The ideal comb's coefficients all equal $1/T_s$. |
| 14 | B | The standard inverse DFT includes the factor $1/N$. |
| 15 | B | This is the continuous convolution definition. |
| 16 | C | Time-domain convolution becomes frequency-domain multiplication. |
| 17 | A | Time multiplication becomes frequency convolution, with the convention factor. |
| 18 | B | Impulse-train sampling replicates the original spectrum. |
| 19 | B | The ideal filter isolates the central spectrum. |
| 20 | B | Overlapping replicas cause aliasing. |
| 21 | B | Spatial frequencies are cycles per unit length. |
| 22 | B | Two spatial coordinates require two frequency coordinates. |
| 23 | B | The spectral replicas form a grid along both axes. |
| 24 | B | Apply Nyquist separately along both image axes. |
| 25 | B | Nearby-pixel predictability is spatial redundancy. |

## Fill in the blanks (Q26–Q40)

| Q | Answer |
|---:|---|
| 26 | $2^b$ |
| 27 | $1/T_s$ |
| 28 | $2\pi f$ |
| 29 | $g(a)$ |
| 30 | Comb (impulse-train) |
| 31 | $2\pi/T_0$ |
| 32 | $1/T_s$ |
| 33 | $1/N$ |
| 34 | $h[m]x[n-m]$ |
| 35 | Product / multiplication |
| 36 | Sampling |
| 37 | $2f_{\max}$ |
| 38 | Length |
| 39 | Support |
| 40 | $\omega_x$ and $\omega_y$ |

---

# 8. Last-minute revision checklist

Before the exam, make sure you can do each item without looking at your notes.

- [ ] Explain what $f(x,y)$ represents.
- [ ] Distinguish human-oriented processing from machine-oriented analysis.
- [ ] Recognise spatial, temporal, coding and psychovisual redundancy.
- [ ] Explain why boundary contours help industrial inspection and why frame changes help motion tracking.
- [ ] Distinguish sampling from quantisation.
- [ ] Compute $L=2^b$ and $b=\log_2 L$.
- [ ] Convert between sampling interval and sampling frequency.
- [ ] Convert between angular frequency and ordinary frequency.
- [ ] Use the Dirac delta sifting property without doing unnecessary integration.
- [ ] Recognise the comb and write the sampled-signal expression.
- [ ] Explain the difference between Fourier transform, Fourier series and DFT.
- [ ] Recall why the ideal impulse comb has Fourier-series coefficients $1/T_s$.
- [ ] Use the standard forward and inverse DFT equations and know the $1/N$ factor.
- [ ] Calculate a small discrete convolution and use the shifted-impulse identity.
- [ ] State the convolution theorem and the dual multiplication property with the correct normalisation convention.
- [ ] Explain why sampling creates spectrum replicas and why overlap produces aliasing.
- [ ] Apply the 1D Nyquist condition and fold a frequency into the baseband.
- [ ] Explain the ideal low-pass reconstruction cutoff condition.
- [ ] Apply the 2D Nyquist condition independently along $x$ and $y$.
- [ ] Explain the 2D sampled spectrum and the region of support.

## A reliable method for numerical NPTEL questions

1. **Write down the requested quantity and its unit.** Are you being asked for Hz, rad/s, cycles/unit length, or samples/unit length?
2. **Choose the matching formula.** Do not use an angular-frequency formula on a quantity already expressed in ordinary frequency without converting.
3. **Substitute the values with units.** Convert milliseconds to seconds before taking a reciprocal.
4. **For a Nyquist problem, find the highest absolute frequency first.** In a 2D problem, calculate the maximum horizontal and vertical frequencies separately.
5. **For an aliasing question, calculate the Nyquist frequency and fold each component that lies above it.** Then check the reconstruction-filter cutoff.
6. **For a convolution question, list only non-zero contributing samples.** This avoids unnecessary arithmetic and indexing mistakes.
7. **Check the answer against the concept.** A sampling-density answer should have sample-density units; a frequency in Hz should not be reported in rad/s.

**Best revision order:** formula guide (Section 3) → original assignment (Section 5) → 40 practice questions under timed conditions (Section 6) → answer key and checklist (Sections 7–8).
