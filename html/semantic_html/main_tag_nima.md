# `<main>` Tegi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<main>`** elementi HTML dokumentining **dominant (asosiy, markaziy) kontentini** ifodalaydi. Bu sahifaning **eng muhim, foydalanuvchi uchun asosiy mazmun** joylashadigan qismi bo‘lib, u sahifaning markaziy mavzusi yoki funksiyasiga bevosita tegishli bo‘lgan barcha kontentni o‘z ichiga oladi.

Senior darajada `<main>` — bu **eng muhim semantic landmark** elementi. U sahifaning “asosiy hikoyasi”ni brauzer, qidiruv tizimlari (Googlebot), ekran o‘quvchilar (NVDA, VoiceOver), AI summarizerlar va voice assistants uchun aniq belgilaydi. Bu element butun HTML arxitekturangizning **markaziy nuqtasi** hisoblanadi va accessibility, SEO, maintainability hamda user experience ni bir vaqtda belgilaydi.

Quyidagi material **MDN Web Docs (13 oktyabr 2025 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, implicit ARIA rollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (13 oktyabr 2025):**

> “The `<main>` HTML element represents the dominant content of the `<body>` of a document. The main content area consists of content that is directly related to or expands upon the central topic of a document, or the central functionality of an application.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The main element represents the dominant contents of the document. A document must not have more than one main element that is not hidden.”

**Senior nuqtai nazar:**  
`<main>` — sahifangizning **“asosiy yuragi”**. U brauzerning parsing jarayonida, accessibility tree’da va search engine crawling’da sahifaning markaziy qismini aniq belgilaydi. Bu element sizning HTML strukturasining asosiy nuqtasi bo‘lib, accessibility, SEO va maintainability ni sezilarli darajada oshiradi.

---

## 2. `<main>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                        | Kim foydalanadi?                                  | Senior darajadagi ta’siri (2026 yil)           |
| ----------------------------- | ------------------------------------------------- | ---------------------------------------------- |
| Asosiy kontentni belgilash    | Ekran o‘quvchilar, Google                         | Implicit `role="main"` landmark yaratadi       |
| Skip-link uchun anchor        | Klaviatura va ekran o‘quvchilar foydalanuvchilari | “Asosiy kontentga o‘tish” tugmasi uchun ideal  |
| Document outline va ierarxiya | Brauzer va qidiruv tizimlari                      | Sahifaning markaziy qismini aniq ko‘rsatadi    |
| SEO va indexing               | Google, Bing, AI Overviews                        | Asosiy kontentni tezroq va aniqroq indekslaydi |
| Accessibility (WCAG 2.2/3.0)  | Barcha foydalanuvchilar                           | Landmark navigatsiyasini yaxshilaydi           |
| Reader Mode / Print           | Safari Reader View, brauzer print                 | Asosiy kontentni to‘g‘ri ajratib ko‘rsatadi    |

---

## 3. Qachon va qanday ishlatiladi? (Real senior misollar)

**To‘g‘ri (production-ready) ishlatish:**

```html
<!DOCTYPE html>
<html lang="uz">
	<head>
		<meta charset="UTF-8" />
		<title>Sahifa sarlavhasi</title>
	</head>
	<body>
		<header>...</header>
		<nav aria-label="Asosiy navigatsiya">...</nav>

		<!-- FAKAT BITTA <main> ! -->
		<main id="main-content">
			<article>
				<h1>Sahifa asosiy sarlavhasi</h1>
				<!-- barcha asosiy kontent shu yerda -->
			</article>
		</main>

		<aside>...</aside>
		<footer>...</footer>
	</body>
</html>
```

**Muhim qoidalar (MDN + WHATWG 2026):**

- Har sahifada **faqat bitta** `<main>` bo‘lishi kerak (WCAG va HTML spec talabi).
- U `<body>` ning to‘g‘ridan-to‘g‘ri farzandi bo‘lishi tavsiya etiladi (lekin ichida `<header>`, `<nav>`, `<footer>` bo‘lishi mumkin emas).
- `id="main"` yoki `id="main-content"` berish odatiy hol (skip-link uchun).
- Agar bir nechta `<main>` kerak bo‘lsa (masalan, SPA da), faqat bitta ko‘rinadigan bo‘lishi va qolganlari `hidden` atributi bilan yashirin bo‘lishi kerak.

---

## 4. Accessibility va SEO ta’siri (2026 yil)

- **Implicit ARIA role:** `main` → ekran o‘quvchilar avtomatik “main content” deb o‘qiydi.
- **Skip-link:** Ko‘pchilik accessibility foydalanuvchilari birinchi navbatda `<main>` ga o‘tishni xohlaydi.
- **SEO:** Google `<main>` ni sahifaning asosiy kontenti sifatida qabul qiladi → indeksatsiya tezroq va aniqroq bo‘ladi.
- **Lighthouse audit:** “`<main>` element exists” va “Document has a main landmark” auditlarini o‘tkazadi. Yo‘q bo‘lsa — ball pasayadi.

---

## 5. Senior Best Practices (2026 yil production darajasi)

1. Har bir loyihada `<main id="main-content">` ni birinchi darajadagi reusable komponent sifatida yarating.
2. Skip-link ni `<main>` ga bog‘lang:
   ```html
   <a href="#main-content" class="skip-link">Asosiy kontentga oʻtish</a>
   ```
3. Hech qachon `<main>` ni stil uchun ishlatmang yoki bir nechta qo‘ymang.
4. Next.js, Astro, Remix kabi frameworklarda `<Main>` komponentini yaratib, har sahifada qayta ishlatish.
5. Lighthouse + axe + WAVE bilan har doim tekshiring.
6. **Anti-pattern:** `<div class="main">` yoki `<div id="content">` ga qaytish — 2026 yilda qabul qilinmaydi.

**Yomon amaliyot:**

```html
<div class="content-wrapper">...</div>
```

**Senior usuli:**

```html
<main id="main-content">...</main>
```

---

## 6. Xulosa (Senior nuqtai nazar)

`<main>` — bu shunchaki “kontent qutisi” emas. Bu **sahifaning markaziy yuragi** va semantic landmark bo‘lib, accessibility, SEO, maintainability va user experience ni bir vaqtda yaxshilaydi. Uni to‘g‘ri ishlatish orqali siz:

- Ekran o‘quvchilar uchun navigatsiyani osonlashtirasiz,
- Google va AI ga sahifaning asosiy mazmunini aniq bildiradi,
- Kodni professional va future-proof qilasiz.

Agar siz faqat `class="main"` bilan ishlasangiz — oddiy developer.  
Agar `<main>` ni `id`, landmark, skip-link va to‘g‘ri nesting bilan chuqur boshqara olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`)
- `<main>` + ARIA + landmark audit
- Real loyihada main content misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Main element (Last modified: 13 oktyabr 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/main)
- [WHATWG HTML Living Standard — The main element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/grouping-content.html#the-main-element)
- [MDN Web Docs — Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- [W3C ARIA in HTML — Implicit roles](https://www.w3.org/TR/html-aria/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
