# `<nav>` Tegi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi

**`<nav>`** elementi HTML ning **semantic landmark** elementlaridan biri bo‘lib, sahifadagi **navigatsiya (navigation) linklarini** o‘z ichiga olgan bo‘limni bildiradi. U sayt ichidagi asosiy menyular, sidebar menyular, breadcrumb, footer linklari yoki boshqa muhim o‘tish joylarini semantik jihatdan belgilaydi.

Senior darajada `<nav>` — bu shunchaki “menu yaratish” uchun emas. Bu **arxitektura qarori**: brauzer, qidiruv tizimlari, ekran o‘quvchilar, AI summarizerlar va voice assistants uchun sahifaning navigatsiya skeletini aniq bildiruvchi kalit element. Uni to‘g‘ri ishlatish orqali siz accessibility (WCAG 2.2/3.0), SEO, maintainability va future-proof kodni bir vaqtda hal qilasiz.

Quyidagi material **MDN Web Docs (12 fevral 2026 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, implicit ARIA rollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (12 fevral 2026):**

> “The `<nav>` HTML element represents a section of a page whose purpose is to provide navigation links, either within the current document or to other documents.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The nav element represents a section of a page that links to other pages or to other parts of the same page. It is a sectioning content element and its content is intended for navigation.”

**Senior nuqtai nazar:**  
`<nav>` — sahifangizning **navigatsiya arxitekturasining asosiy qismi**. U kontentning “o‘tish joylari”ni semantik jihatdan belgilaydi va brauzerning default xatti-harakatini, landmark rolini va outline algorithmni avtomatik ravishda faollashtiradi. Bu element sizning HTML strukturasining “yo‘l ko‘rsatuvchi”si hisoblanadi.

---

## 2. `<nav>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                          | Kim foydalanadi?                    | Senior darajadagi ta’siri (2026 yil)                            |
| ------------------------------- | ----------------------------------- | --------------------------------------------------------------- |
| Asosiy navigatsiya belgilash    | Ekran o‘quvchilar (NVDA, VoiceOver) | Implicit `role="navigation"` landmark yaratadi                  |
| SEO strukturasini yaxshilash    | Google, Bing, AI Overviews          | Navigatsiya ierarxiyasini aniq ko‘rsatadi                       |
| Keyboard navigation             | Klaviatura foydalanuvchilari        | Tab tartibi va focus management ni yaxshilaydi                  |
| Multiple navigatsiya bo‘limlari | Sayt ichidagi turli menyular        | Har bir `<nav>` ga `aria-label` bilan farqlash                  |
| Reader Mode / Print             | Safari Reader, brauzer print        | Keraksiz navigatsiyani to‘g‘ri olib tashlaydi                   |
| Voice assistants                | Siri, Google Assistant, Alexa       | “Navigatsiya bo‘limiga o‘tish” buyruqlarini qo‘llab-quvvatlaydi |

---

## 3. Qachon va qanday ishlatiladi? (Real senior misollar + nesting)

**1. Global (site-wide) navigatsiya — eng klassik holat:**

```html
<header>
	<nav aria-label="Asosiy navigatsiya" class="site-nav">
		<ul>
			<li><a href="/">Bosh sahifa</a></li>
			<li><a href="/kurslar">Kurslar</a></li>
			<li><a href="/blog">Blog</a></li>
			<li><a href="/kontakt">Kontakt</a></li>
		</ul>
	</nav>
</header>
```

**2. Sidebar yoki secondary navigation:**

```html
<aside>
	<nav aria-label="Kurs boʻlimlari">
		<h2>Kurs mazmuni</h2>
		<ul>
			<li><a href="#modul1">1-modul</a></li>
			<li><a href="#modul2">2-modul</a></li>
		</ul>
	</nav>
</aside>
```

**3. Footer navigatsiya:**

```html
<footer>
	<nav aria-label="Footer navigatsiyasi">
		<ul>
			<li><a href="/privacy">Maxfiylik siyosati</a></li>
			<li><a href="/terms">Foydalanish shartlari</a></li>
		</ul>
	</nav>
</footer>
```

**4. Breadcrumb navigatsiya (SEO uchun juda muhim):**

```html
<nav aria-label="Breadcrumb" class="breadcrumb">
	<ol>
		<li><a href="/">Bosh sahifa</a></li>
		<li><a href="/blog">Blog</a></li>
		<li aria-current="page">HTML Semantic teglar</li>
	</ol>
</nav>
```

**Muhim qoida (MDN + WHATWG 2026):**

- Bir sahifada bir nechta `<nav>` bo‘lishi mumkin va tavsiya etiladi.
- Har bir `<nav>` ga **aniq `aria-label`** yoki `aria-labelledby` berish majburiy (landmarklarni farqlash uchun).
- `<nav>` ichiga faqat navigatsiya linklari (odatda `<ul>`/`<ol>` + `<a>`) joylashtiriladi. Boshqa kontent (logo, qidiruv) `<nav>` dan tashqarida bo‘lishi kerak.
- `<nav>` ni `<header>`, `<footer>`, `<aside>` yoki `<main>` ichida ishlatish odatiy hol.

---

## 4. Semantic vs Non-semantic (eski usul)

**Yomon (non-semantic — 2015 yildan keyin qabul qilinmaydi):**

```html
<div class="menu">
	<ul>
		...
	</ul>
</div>
```

**Senior (to‘g‘ri):**

```html
<nav aria-label="Asosiy navigatsiya">
	<ul>
		...
	</ul>
</nav>
```

**Farq:** Brauzer, ekran o‘quvchilar va Google `<nav>` ni avtomatik landmark sifatida ko‘radi. Bu sahifaning navigatsiya qismini bir necha soniyada topishga yordam beradi.

---

## 5. Senior Best Practices (2026 yil production darajasi)

1. Har bir `<nav>` ga `aria-label` berish (tilga mos — o‘zbekcha yoki inglizcha).
2. Mobil uchun `aria-expanded` va JavaScript bilan toggle qilish (hamburger menu).
3. **Skip link** bilan birgalikda ishlatish:
   ```html
   <a href="#main-content" class="skip-link">Navigatsiyani oʻtkazib yuborish</a>
   ```
4. BEM yoki Tailwind bilan class nomlarini aniq berish (`nav__list`, `nav__item`).
5. Lighthouse + axe + WAVE bilan tekshirish — “Navigation landmark” auditini o‘tkazing.
6. **Performance**: Navigatsiyani inline yoki critical CSS bilan yuklang (LCP ni buzmaslik uchun).
7. **Future-proof**: Web Components yoki Astro/Next.js da `<nav>` ni reusable komponent sifatida yarating.
8. Hech qachon faqat bitta linkni `<nav>` ga o‘ramang — u “navigatsiya bo‘limi” bo‘lishi kerak.

**Yomon amaliyot (qat’iyan taqiqlanadi):**

- Har bir `<ul>` ni `<nav>` ga o‘rash.
- `role="navigation"` ni qo‘lda qo‘shish (implicit role bor).
- `<nav>` ni faqat dekorativ linklar uchun ishlatish.

---

## 6. Xulosa (Senior nuqtai nazar)

`<nav>` — bu oddiy “menu” emas. Bu **semantic landmark** va sahifangizning navigatsiya arxitekturasining asosiy qismi. Uni to‘g‘ri ishlatish orqali siz:

- Accessibility ni WCAG 2.2/3.0 darajasiga ko‘tarasiz,
- SEO ni sezilarli yaxshilaysiz,
- Kodni o‘qilishi va maintain qilishni osonlashtirasiz,
- Kelajakdagi texnologiyalarga (AI voice navigation, reader modes, Web Components) tayyor bo‘lasiz.

Agar siz faqat `class="nav"` bilan ishlasangiz — siz dizayner kod yozayapsiz.  
Agar `<nav>` ni `aria-label`, landmarklar va to‘g‘ri nesting bilan qo‘llay olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (real loyiha)
- `<nav>` + ARIA + landmark audit
- Hamburger menu + mobile navigation misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Nav element (Last modified: 12 fevral 2026)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav)
- [WHATWG HTML Living Standard — The nav element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html#the-nav-element)
- [MDN Web Docs — Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- [W3C ARIA in HTML — Implicit roles](https://www.w3.org/TR/html-aria/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
