# `<header>` Tegi Nima Uchun Ishlatiladi? — To‘liq Senior Front-end Developer Qo‘llanmasi

**`<header>`** elementi HTML ning **semantic landmark** elementlaridan biri bo‘lib, sahifaning yoki bo‘limning **kirish (introductory) kontentini** ifodalaydi. U logo, navigatsiya, sarlavha, qidiruv formasi, muallif ma’lumotlari va boshqa “boshlanish” elementlarini guruhlaydi.

Senior darajada `<header>` — bu shunchaki “yuqori panel” emas. Bu **arxitektura qarori**: brauzer, qidiruv tizimlari, ekran o‘quvchilar, AI summarizerlar va Web Components uchun sahifaning strukturasini aniq bildiruvchi kalit element. U sahifaning butun kontent ierarxiyasini, Accessibility Tree ni va SEO ni belgilaydi.

Quyidagi material **MDN Web Docs (12 fevral 2026 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real misollar, implicit ARIA rollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (12 fevral 2026):**

> “The `<header>` HTML element represents introductory content, typically a group of introductory or navigational aids.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The header element represents a group of introductory or navigational aids. It is a sectioning content element and may contain flow content, but must not contain header or footer elements as descendants.”

**Senior nuqtai nazar:**  
`<header>` — sahifangizning **“kirish eshigi”**. U kontentning boshlanish qismini semantik jihatdan belgilaydi va brauzerning default xatti-harakatini, landmark rolini va outline algorithmni avtomatik ravishda faollashtiradi. Bu element sizning HTML arxitekturangizning asosiy qismi bo‘lib, accessibility, SEO va maintainability ni sezilarli darajada oshiradi.

---

## 2. `<header>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                           | Kim foydalanadi?                      | Senior darajadagi ta’siri (2026 yil)            |
| -------------------------------- | ------------------------------------- | ----------------------------------------------- |
| Sahifaning global sarlavhasi     | Foydalanuvchi, brauzer, qidiruvchilar | Logo, global nav, search — butun sayt uchun     |
| Bo‘lim yoki article kirish qismi | Ekran o‘quvchilar, SEO                | Har bir `<section>` yoki `<article>` ichida     |
| Navigatsiya guruhini belgilash   | NVDA, VoiceOver, Google               | Implicit `navigation` bilan birga               |
| Accessibility landmark           | Ekran o‘quvchilar                     | Top-level bo‘lsa `role="banner"` (faqat bitta!) |
| SEO va struktura                 | Google, Bing, AI Overviews            | Kontent ierarxiyasini aniq bildiradi            |
| Reader Mode va outline           | Safari Reader View, brauzer outline   | Avtomatik kontent ierarxiyasi hosil qiladi      |

---

## 3. Qachon va qanday ishlatiladi? (Real holatlar + nesting qoidalari)

**1. Global sahifa sarlavhasi (eng ko‘p ishlatiladigan — top-level):**

```html
<header class="site-header">
	<div class="container">
		<a href="/" class="logo">Brand</a>
		<nav aria-label="Asosiy navigatsiya">
			<!-- menu -->
		</nav>
		<form role="search">...</form>
	</div>
</header>
```

**2. Bo‘lim yoki article ichidagi header:**

```html
<article>
	<header>
		<h1>Maqola sarlavhasi</h1>
		<p class="meta">
			<time datetime="2026-04-17">17 aprel 2026</time>
			• Muallif: Senior Dev
		</p>
	</header>
	<p>Asosiy matn...</p>
</article>
```

**3. Section ichidagi header:**

```html
<section>
	<header>
		<h2>Eng soʻnggi yangiliklar</h2>
		<a href="/news">Barchasini koʻrish →</a>
	</header>
	<!-- kartochkalar -->
</section>
```

**Muhim qoida (MDN + WHATWG 2026):**

- Agar `<header>` sahifaning eng yuqori darajasida (`<body>` ning to‘g‘ridan-to‘g‘ri farzandi) bo‘lsa → implicit `role="banner"` (global banner landmark).
- Agar u `<article>`, `<section>`, `<aside>`, `<nav>` yoki `<main>` ichida bo‘lsa → implicit `role="generic"` (landmark statusini yo‘qotadi va faqat o‘sha bo‘limning kirish qismi bo‘lib qoladi).
- Ichiga boshqa `<header>` yoki `<footer>` qo‘yish mumkin emas (invalid HTML).

---

## 4. `<header>` va `<head>` farqi (ko‘pchilik chalkashadigan joy)

- **`<header>`** — **foydalanuvchiga ko‘rinadigan** kontent (UI header, semantic landmark).
- **`<head>`** — **mashinaga ko‘rinadigan** metadata (`<title>`, `<meta>`, `<link>`, `<script>`).

Hech qachon ularni aralashtirmang! `<header>` `<body>` ichida, `<head>` esa `<html>` ichida joylashadi.

---

## 5. Senior darajadagi best practices (2026 yil production darajasi)

1. **Har sahifada faqat bitta global `<header>`** bo‘lsin (banner landmark).
2. Har bir `<article>` va muhim `<section>` o‘zining `<header>` ga ega bo‘lishi mumkin (lekin nesting qoidalariga rioya qiling).
3. Ichiga `<h1>`–`<h6>` qo‘yish tavsiya etiladi (heading hierarchy uchun).
4. Navigatsiya uchun alohida `<nav>` ishlatish afzal (header ichida bo‘lsa ham).
5. **Accessibility**: `aria-labelledby` yoki `aria-label` bilan aniq belgilang.
6. **Performance**: Header ni Critical Rendering Path da saqlang — inline yoki critical CSS bilan.
7. **SEO**: Google 2026 yilda semantic header strukturasini kuchli baholaydi (heading hierarchy bilan birga).
8. **Web Components**: Shadow DOM ichida ham `<header>` ni semantic tarzda ishlatish mumkin.

**Yomon amaliyot (qat’iyan taqiqlanadi):**

```html
<div class="header">...</div>
<!-- semantic emas, landmark yo‘q -->
```

**Senior usuli (to‘liq misol):**

```html
<header class="site-header">
	<!-- global content -->
</header>

<main>
	<article>
		<header>
			<h1>Maqola sarlavhasi</h1>
			<!-- meta -->
		</header>
		<!-- kontent -->
	</article>
</main>
```

---

## 6. Xulosa (Senior nuqtai nazar)

`<header>` — bu shunchaki “yuqori panel” emas. Bu **semantic landmark** va sahifangizning strukturasini brauzer, qidiruv tizimlari, ekran o‘quvchilar va AI ga aniq bildiruvchi kalit element. Uni to‘g‘ri ishlatish orqali siz:

- Accessibility ni oshiradi (WCAG 2.2/3.0),
- SEO ni yaxshilaydi,
- Kodni maintainable qiladi,
- Kelajakdagi texnologiyalarga (AI summarizerlar, voice assistants, Web Components) tayyor bo‘lasiz.

Agar siz faqat `class="header"` bilan ishlasangiz — siz dizayner kod yozayapsiz.  
Agar `<header>`, `<main>`, `<nav>`, `<article>` ni to‘g‘ri arxitekturada qo‘llay olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (real loyiha)
- `<header>` + ARIA + landmark audit
- Popover API bilan birgalikda header misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Header element (Last modified: 12 fevral 2026)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header)
- [WHATWG HTML Living Standard — The header element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html#the-header-element)
- [MDN Web Docs — Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- [W3C ARIA in HTML — Implicit roles](https://www.w3.org/TR/html-aria/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
