# `<meta>` Tegi Nima Qiladi? — To‘liq Senior Front-end Developer Qo‘llanmasi

**`<meta>`** elementi HTML dokumentining **ko‘rinmas, lekin juda kuchli** qismi hisoblanadi. U sahifada foydalanuvchiga ko‘rinmaydi, ammo brauzer, qidiruv tizimlari (Google, Yandex), ijtimoiy tarmoqlar, ekran o‘quvchilar, PWA, xavfsizlik mexanizmlari va hatto AI/LLM summarizerlar uchun **metadata** (ma’lumotlar haqidagi ma’lumot) beradi.

Senior darajada biz `<meta>` ni “oddiy teg” deb emas, balki **declarative konfiguratsiya vositasi** sifatida ko‘ramiz. U **Critical Rendering Path (CRP)** ga bevosita ta’sir qiladi, sahifaning birinchi 1-2 KB ichida yuklanishi kerak va butun loyihaning SEO, Performance, Security, Accessibility va Mobile Experience ni belgilaydi.

Quyidagi material **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** va **MDN Web Docs (2025 yil noyabr va 2026 yil yangilanishlari)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real misollar va production best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va asosiy maqsadi

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The `meta` element represents various kinds of metadata that cannot be expressed using the `title`, `base`, `link`, `style`, and `script` elements.”

**MDN Web Docs (so‘nggi yangilanish: 7 noyabr 2025):**  
`<meta>` — boshqa meta-related elementlar (`<title>`, `<base>`, `<link>`, `<style>`, `<script>`) orqali ifodalab bo‘lmaydigan metadata uchun ishlatiladi.

**Senior nuqtai nazar:**  
`<meta>` — bu **brauzer va mashinalarga konfiguratsiya beruvchi** vosita. U sahifaning:

- Kodlashini (charset),
- Mobil moslashuvini (viewport),
- SEO va ijtimoiy sharingni,
- Xavfsizlik siyosatini (CSP, referrer),
- Rang sxemasini (theme-color, color-scheme),
- va hatto PWA o‘rnatilishini boshqaradi.

Har bir `<meta>` tagi brauzerning parsing jarayoniga ta’sir qiladi va sahifaning birinchi 1024 bayt ichida bo‘lishi tavsiya etiladi (ayniqsa `charset` uchun).

---

## 2. Sintaksis va atributlar (to‘liq va aniq ro‘yxat, 2026 yil)

`<meta>` har doim `<head>` ichida joylashadi. Bu **bo‘sh element** (self-closing emas, lekin yopilmaydi).

**Asosiy atributlar (WHATWG + MDN bo‘yicha):**

| Atribut      | Maqsadi                                                            | Majburiy / Tavsiya                   | Misol                                             |
| ------------ | ------------------------------------------------------------------ | ------------------------------------ | ------------------------------------------------- |
| `charset`    | Dokument kodlash turini belgilash (eng muhim!)                     | Majburiy (eng birinchi)              | `<meta charset="UTF-8">`                          |
| `name`       | Metadata turini belgilaydi (description, viewport, robots va h.k.) | Ko‘pincha ishlatiladi                | `<meta name="viewport" ...>`                      |
| `content`    | `name` yoki `http-equiv` uchun qiymatni beradi                     | `name` yoki `http-equiv` bilan birga | `content="width=device-width, initial-scale=1.0"` |
| `http-equiv` | HTTP header taqlid qilish (pragma directives)                      | Kamroq tavsiya etiladi               | `http-equiv="Content-Security-Policy"`            |
| `property`   | Open Graph, RDFa va boshqa structured data uchun                   | OG uchun majburiy                    | `property="og:title"`                             |
| `media`      | Media query (faqat `theme-color` uchun)                            | `theme-color` bilan                  | `media="(prefers-color-scheme: dark)"`            |
| `itemprop`   | Microdata / Schema.org uchun (user-defined metadata)               | Structured Data loyihalarida         | —                                                 |

**Muhim qoida (WHATWG):**  
Har bir `<meta>` da **faqat bitta** `name`, `http-equiv`, `charset` yoki `itemprop` bo‘lishi mumkin. `content` atributi ko‘pincha majburiy.

---

## 3. Eng muhim `<meta>` turlari (2026 yil production best practices)

### A. Majburiy (har bir sahifada bo‘lishi kerak)

1. **Charset** (eng birinchi bo‘lishi shart!)
   ```html
   <meta charset="UTF-8" />
   ```

- Nima qiladi? Brauzerga matnni to‘g‘ri dekod qilishni aytadi. UTF-8 — yagona to‘g‘ri tanlov (WHATWG talabi).

2. **Viewport** (responsive va mobile-first uchun majburiy)

   ```html
   <meta
   	name="viewport"
   	content="width=device-width, initial-scale=1.0, viewport-fit=cover"
   />
   ```

   - Container Queries bilan birgalikda ishlatiladi. Lighthouse avtomatik tekshiradi.

3. **Description** (SEO + Click-Through Rate)
   ```html
   <meta
   	name="description"
   	content="Sahifa haqida aniq, 150-160 belgi ichidagi tavsif. Foydalanuvchi va Google uchun muhim."
   />
   ```

### B. Zamonaviy va professional (senior loyihalarda majburiy)

- **Robots va indekslash**

  ```html
  <meta name="robots" content="index, follow, max-image-preview:large" />
  <meta name="googlebot" content="index, follow" />
  ```

- **Theme-color va Color-scheme** (mobil brauzerlar va PWA uchun)

  ```html
  <meta
  	name="theme-color"
  	content="#0066ff"
  	media="(prefers-color-scheme: light)"
  />
  <meta
  	name="theme-color"
  	content="#0044aa"
  	media="(prefers-color-scheme: dark)"
  />
  <meta name="color-scheme" content="light dark" />
  ```

- **Open Graph (Facebook, LinkedIn, X, Telegram va boshqalar)**

  ```html
  <meta property="og:title" content="Sahifa sarlavhasi" />
  <meta property="og:description" content="Tavsif" />
  <meta property="og:image" content="https://example.com/og-image.jpg" />
  <meta property="og:url" content="https://current-page" />
  <meta property="og:type" content="website" />
  <meta property="og:locale" content="uz_UZ" />
  ```

- **Xavfsizlik (Security)**

  ```html
  <meta name="referrer-policy" content="strict-origin-when-cross-origin" />
  <meta
  	http-equiv="Content-Security-Policy"
  	content="default-src 'self'; script-src 'self' https://trusted.cdn;"
  />
  ```

- **PWA va Installability**
  ```html
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="mobile-web-app-capable" content="yes" />
  ```

---

## 4. Senior darajadagi best practices (2026 yil)

1. **Tartib juda muhim** — `<head>` ichida:
   - 1. `<meta charset="UTF-8">`
   - 2. `<meta name="viewport" ...>`
   - 3. `<title>`
   - 4. Boshqa meta teglar (description, OG, robots)
   - 5. Preload, CSS, JS

2. **Hech qachon takrorlanmasin** — bir xil `name` yoki `http-equiv` bir necha marta bo‘lmasin (brauzer oxirgisini oladi).

3. **Performance** — `og:image` 1200×630 px, < 1 MB bo‘lsin. Meta teglar og‘ir bo‘lmasin.

4. **Security** — CSP ni `<meta>` orqali qo‘shish mumkin, lekin HTTP header orqali (server-side) qo‘shish ancha afzal (meta CSP kechroq ishlaydi).

5. **Lighthouse / Web Vitals** — har doim tekshiring:
   - “Document has a meta description”
   - “Viewport tag present”
   - “Document has a `<title>`”

6. **LLM-friendly meta** (2025-2026 trend) — ba’zi loyihalarda `name="llms:website"` yoki `name="ai:summary"` kabi yangi meta qo‘shilmoqda.

---

## 5. To‘liq Senior Production `<head>` misoli

```html
<head>
	<!-- 1. Encoding (eng birinchi!) -->
	<meta charset="UTF-8" />

	<!-- 2. Viewport -->
	<meta
		name="viewport"
		content="width=device-width, initial-scale=1.0, viewport-fit=cover"
	/>

	<!-- 3. Title -->
	<title>Sahifa sarlavhasi — Sayt nomi</title>

	<!-- 4. Asosiy metadata -->
	<meta
		name="description"
		content="150-160 belgi ichidagi aniq va jozibali tavsif..."
	/>
	<meta name="robots" content="index, follow, max-image-preview:large" />

	<!-- Open Graph / Social -->
	<meta property="og:title" content="Sahifa sarlavhasi" />
	<meta property="og:description" content="Tavsif" />
	<meta property="og:image" content="https://example.com/og-image.jpg" />
	<meta property="og:url" content="https://current-page" />
	<meta property="og:type" content="website" />

	<!-- Theme & PWA -->
	<meta
		name="theme-color"
		content="#0066ff"
		media="(prefers-color-scheme: light)"
	/>
	<meta
		name="theme-color"
		content="#0044aa"
		media="(prefers-color-scheme: dark)"
	/>
	<meta name="color-scheme" content="light dark" />

	<!-- Security -->
	<meta name="referrer-policy" content="strict-origin-when-cross-origin" />
</head>
```

---

## 6. Xulosa — nega senior `<meta>` ni “kichik, lekin kuchli” deb hisoblaydi?

`<meta>` tagi — bu sahifangizning **ko‘rinmas skeleti**. Uni to‘g‘ri ishlatmasangiz:

- SEO pasayadi,
- Mobil tajriba buziladi,
- Xavfsizlik zaiflashadi,
- Core Web Vitals yomonlashadi.

**Senior maslahat:** Har bir yangi loyihada birinchi narsa — `charset`, `viewport`, `title` va keyin to‘liq meta to‘plami. Bu sizning loyihangizni **future-proof** qiladi.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- CSP meta vs HTTP header (real misollar bilan)
- Open Graph + Twitter Card to‘liq qo‘llanma
- Schema.org + itemprop bilan structured data

Savolingiz bo‘lsa yoki real loyiha misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [WHATWG HTML Living Standard — The `meta` element (Last Updated 15 aprel 2026)](https://html.spec.whatwg.org/multipage/semantics.html#the-meta-element)
- [MDN Web Docs — `<meta>`: The metadata element (Last modified 7 noyabr 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)
- [MDN Web Docs — Standard metadata names](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta/name)
- [WHATWG Standard Metadata Names](https://html.spec.whatwg.org/multipage/semantics.html#standard-metadata-names)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy WHATWG va MDN manbalaridan olingan va 2026 yil 15 aprel holatiga mos.
