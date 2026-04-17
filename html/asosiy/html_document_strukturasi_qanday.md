# HTML Dokument Strukturasi — Toʻliq Senior Front-end Developer Qoʻllanmasi

**HTML dokumentining strukturasini** toʻgʻri tushunish — bu nafaqat “kod yozish” emas, balki **brauzer qanday parse qiladi**, **Critical Rendering Path** qanday hosil boʻladi, **DOM Tree** va **Render Tree** qanday yaratiladi, **Accessibility (a11y)**, **SEO**, **Performance** va **Maintainability** uchun asosiy poydevor hisoblanadi.

Senior darajada biz har doim **minimal valid HTML** + **semantic HTML** + **production-ready, optimized boilerplate** bilan ishlaymiz. Bu struktura notoʻgʻri boʻlsa, butun loyiha (React, Vue, Astro, Next.js yoki vanilla) sekinlashadi, SEO pasayadi va ekran oʻquvchilar uchun foydalanuvchilar qiynaladi.

Quyidagi material **MDN Web Docs (2025–2026)**, **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** va **WCAG 2.2** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan va amaliy misollar bilan boyitilgan.

---

## 1. Eng minimal (valid) HTML dokumenti

Brauzer tomonidan 100% valid qabul qilinadigan eng kichik struktura:

```html
<!DOCTYPE html>
<html lang="uz">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Sahifa sarlavhasi</title>
	</head>
	<body>
		<h1>Salom, dunyo!</h1>
	</body>
</html>
```

Bu — **brauzer parsing**ning asosiy nuqtasi. Har qanday qoʻshimcha element ixtiyoriy, lekin **senior loyihalarda** hech qachon shu darajada qoldirmaymiz.

---

## 2. Toʻliq Production-Ready Boilerplate (Senior + 2026 Best Practices)

```html
<!DOCTYPE html>
<html lang="uz" dir="ltr">
	<head>
		<!-- 1. Encoding — ENG BIRINCHI boʻlishi SHART! (brauzer parsingni toʻgʻri boshlaydi) -->
		<meta charset="UTF-8" />

		<!-- 2. Viewport — responsive va mobile-first uchun majburiy -->
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0, viewport-fit=cover"
		/>

		<!-- 3. Document metadata -->
		<title>Sahifa sarlavhasi — Sayt nomi</title>
		<meta
			name="description"
			content="Sahifa haqida qisqa, aniq tavsif (150-160 belgi). SEO uchun muhim."
		/>
		<meta name="author" content="Ismingiz yoki kompaniya nomi" />
		<meta name="robots" content="index, follow" />

		<!-- Open Graph / Social meta (Facebook, LinkedIn, X va boshqalar uchun) -->
		<meta property="og:title" content="Sahifa sarlavhasi" />
		<meta property="og:description" content="Tavsif" />
		<meta property="og:image" content="https://example.com/og-image.jpg" />
		<meta property="og:url" content="https://example.com/current-page" />
		<meta property="og:type" content="website" />
		<meta property="og:locale" content="uz_UZ" />

		<!-- Twitter Card (ixtiyoriy, lekin tavsiya etiladi) -->
		<meta name="twitter:card" content="summary_large_image" />

		<!-- Favicon va PWA manifest -->
		<link rel="icon" href="/favicon.ico" type="image/x-icon" />
		<link rel="apple-touch-icon" href="/apple-touch-icon.png" />
		<link rel="manifest" href="/manifest.json" />

		<!-- CSS (Critical CSS inline yoki alohida) -->
		<link rel="stylesheet" href="styles/main.css" media="all" />

		<!-- Preload muhim resurslar (Performance boost) -->
		<link
			rel="preload"
			href="fonts/inter.woff2"
			as="font"
			type="font/woff2"
			crossorigin="anonymous"
		/>
		<link rel="preload" href="critical.css" as="style" />

		<!-- JavaScript — defer yoki async (blocking emas) -->
		<script src="scripts/app.js" defer></script>
	</head>

	<body>
		<!-- Skip to main content (a11y uchun majburiy) -->
		<a href="#main-content" class="skip-link">Asosiy kontentga oʻtish</a>

		<!-- Header -->
		<header role="banner">
			<nav aria-label="Asosiy navigatsiya">...</nav>
		</header>

		<!-- Main content — FAQAT BITTA boʻlishi kerak! -->
		<main id="main-content" role="main">
			<article>
				<header>
					<h1>Maqola sarlavhasi</h1>
				</header>
				<section aria-labelledby="section1">
					<h2 id="section1">Birinchi boʻlim</h2>
					<!-- kontent -->
				</section>
			</article>

			<aside aria-label="Yon panel">
				<!-- Yon panel yoki qoʻshimcha maʼlumot -->
			</aside>
		</main>

		<!-- Footer -->
		<footer role="contentinfo">
			<!-- footer kontenti -->
		</footer>

		<!-- Modal, off-canvas, toast elementlar body oxirida (performance uchun) -->
	</body>
</html>
```

---

## 3. Har bir qismning senior darajadagi chuqur tahlili

| Qism                         | Maqsadi (nima uchun?)                          | Senior Best Practice (2026)                                                                |
| ---------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `<!DOCTYPE html>`            | Brauzerga “bu HTML5” deb bildirish             | Hech qachon eski DOCTYPE ishlatmang — quirks mode’ni oldini oladi.                         |
| `<html lang="uz" dir="ltr">` | Sahifa tilini va yozish yoʻnalishini belgilash | `dir="rtl"` qoʻshish kerak boʻlsa qoʻshing. Ekran oʻquvchilar va i18n uchun majburiy.      |
| `<head>`                     | Metadata, resurslar va brauzer koʻrsatmalari   | Charset birinchi! Keyin viewport. Boshqa meta teglar tartib bilan (performance).           |
| `<meta charset="UTF-8">`     | Kodlashni belgilash                            | UTF-8 — yagona toʻgʻri tanlov (oʻzbekcha, emoji, xalqaro tillar uchun).                    |
| `<meta viewport>`            | Mobil va responsive moslashuv                  | `viewport-fit=cover` + `initial-scale=1.0` — Container Queries bilan birgalikda ishlatish. |
| `<title>`                    | Brauzer tab + SEO + bookmark                   | 50-60 belgi. Brend + sahifa nomi. Har sahifada unique boʻlsin.                             |
| `<main>`                     | Sahifaning asosiy mazmuni                      | Har sahifada **faqat bitta** `<main>` (WCAG 2.2 Success Criterion 1.3.1).                  |
| Semantic elementlar          | Struktura, maʼno va outline                    | `<header>`, `<nav>`, `<section>`, `<article>`, `<aside>`, `<footer>` — har doim ishlatish. |

---

## 4. Brauzer HTMLni qanday parse qiladi? (Senior daraja — Critical Rendering Path)

1. **Tokenization** → Brauzer HTMLni baytma-bayt oʻqib, teglarni tokenlarga aylantiradi.
2. **Parsing** → Tokenlardan **DOM Tree** hosil qiladi (HTML Parser algoritmi — WHATWG spec).
3. **CSSOM Tree** yaratiladi (agar CSS yuklangan boʻlsa).
4. **Render Tree** hosil boʻladi (DOM + CSSOM birlashadi).
5. **Layout (Reflow)** → elementlar joylashuvi hisoblanadi.
6. **Paint** → pikselma-piksel chiziladi.
7. **Composite** → GPU layerlar birlashtiriladi.

**Senior maslahat**: `<head>`dagi resurslarni toʻgʻri tartiblasangiz (charset birinchi, preload, defer), **First Contentful Paint (FCP)** va **Largest Contentful Paint (LCP)** sezilarli yaxshilanadi.

---

## 5. Nima uchun semantic struktura juda muhim?

- **Brauzer** — DOM Tree ni tezroq va toʻgʻri quradi.
- **Qidiruv tizimlari (Google, Yandex)** — sahifani yaxshiroq tushunib, yuqori reyting beradi.
- **Ekran oʻquvchilar (NVDA, VoiceOver, TalkBack)** — foydalanuvchilarga toʻgʻri navigatsiya va landmarklar beradi.
- **Future-proof** — Web Components, AI summarizerlar, voice assistants va yangi brauzer xususiyatlari semantic HTMLga asoslanadi.
- **HTML Outline Algorithm** — `<h1>–<h6>` va sectioning elements orqali avtomatik kontent ierarxiyasi hosil boʻladi.

---

## 6. WHATWG HTML Living Standard

HTML endi “versiya” emas — **Living Standard**. U doimiy yangilanadi.

**Asosiy yangi va kuchaytirilgan elementlar (2024–2026):**

- `<search>` — qidiruv bloklari uchun maxsus semantic element (4.4.15 boʻlim).
- `<dialog>` — modal dialoglar uchun toʻliq qoʻllab-quvvatlanadi.
- `<details>` va `<summary>` — yanada kuchli interaktivlik.
- Global atributlar: `popover`, `inert`, `enterkeyhint` va boshqalar yangilangan.

**Manba**: [WHATWG HTML Living Standard — Last Updated 15 April 2026](https://html.spec.whatwg.org/)

---

## 7. Senior maslahatlar (10+ yillik tajribadan, loyihada qoʻllash)

1. Har doim **Lighthouse** (Chrome DevTools) bilan tekshiring: Performance 90+, Accessibility 100, SEO 100.
2. `<head>` ni iloji boricha qisqa tuting — Critical CSS inline, qolgan CSS async.
3. Hech qachon “div soup” qilmang — semantic elementlardan maksimal foydalaning.
4. `id` lar sahifada unique boʻlsin, `aria-*` atributlari kerak boʻlganda qoʻshing.
5. Loyiha katta boʻlsa — **HTML templating** (Astro Islands, Next.js App Router yoki Web Components) dan foydalaning.
6. Har sahifada **Document Outline**ni tekshiring (https://validator.w3.org/ yoki browser extension).
7. **Progressive Enhancement** tamoyili: HTML asos boʻlsin, CSS va JS ustiga qoʻshilsin.
8. Test: Real foydalanuvchilar (ekran oʻquvchi bilan) va real qurilmalar (mobile, tablet, desktop).

---

## 8. Umumiy xatolar (Common Pitfalls) va ularni qanday oldini olish

- Koʻp `<div>` va `<span>` ishlatish → “div hell”.
- Bir nechta `<main>` qoʻyish → WCAG buziladi.
- `<title>` va meta teglarni unutish → SEO va social sharing yomonlashadi.
- Skip link yoʻqligi → keyboard foydalanuvchilari qiynaladi.
- Charsetni oxirida qoʻyish → baʼzi brauzerlarda matn buziladi.

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [WHATWG HTML Living Standard — Last Updated 15 April 2026](https://html.spec.whatwg.org/)
- [MDN Web Docs — HTML: HyperText Markup Language](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [MDN Web Docs — Structuring documents](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Structuring_documents) (25 avgust 2025 yangilanish)
- [W3C WCAG 2.2 — Semantic Structure](https://www.w3.org/WAI/WCAG22/quickref/)
- [W3C Markup Validation Service](https://validator.w3.org/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy WHATWG va MDN manbalaridan olingan va 2026 yil 15 aprel holatiga mos.
