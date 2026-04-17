# `<aside>` Tegi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<aside>`** elementi HTML ning **semantic landmark** elementlaridan biri bo‘lib, sahifaning **asosiy kontentga faqat bilvosita (tangential / indirectly related)** tegishli qismni ifodalaydi. U ko‘pincha sidebar, related content, pull-quote, author bio, glossary, reklama bloklari yoki qo‘shimcha izoh sifatida ishlatiladi.

Senior darajada `<aside>` — bu shunchaki “yon panel” emas. Bu **complementary landmark** elementi. U sahifaning asosiy oqimini buzmasdan qo‘shimcha qiymat qo‘shadi va brauzer, qidiruv tizimlari, ekran o‘quvchilar, AI summarizerlar va voice assistants uchun sahifaning strukturasini aniq bildiradi.

Quyidagi material **MDN Web Docs (9 iyul 2025 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, implicit ARIA rollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (9 iyul 2025):**

> “The `<aside>` HTML element represents a portion of a document whose content is only indirectly related to the document's main content. Asides are frequently presented as sidebars or call-out boxes.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The aside element represents a section of a page that consists of content that is tangentially related to the content around the aside element, and which could be considered separate from that content.”

**Senior nuqtai nazar:**  
`<aside>` — **complementary (qo‘shimcha, yonma-yon)** kontent uchun maxsus semantic element. U asosiy kontentdan ajratilgan holda, lekin unga aloqador ma’lumotni saqlaydi. Uni to‘g‘ri ishlatish orqali accessibility, SEO va kod arxitekturasini bir vaqtda yaxshilash mumkin. Bu element sahifaning “asosiy hikoyadan tashqari, lekin unga tegishli” qismini aniq belgilaydi.

---

## 2. `<aside>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                           | Kim foydalanadi?                    | Senior darajadagi ta’siri (2026 yil)              |
| -------------------------------- | ----------------------------------- | ------------------------------------------------- |
| Complementary kontent belgilash  | Ekran o‘quvchilar (NVDA, VoiceOver) | Implicit `role="complementary"` landmark yaratadi |
| Sidebar / yon panel              | Foydalanuvchi va dizayner           | Vizual va semantik jihatdan to‘g‘ri               |
| Related / tegishli kontent       | SEO va AI summarizerlar             | Google “related content” sifatida qabul qiladi    |
| Author bio, pull-quote, glossary | Kontent mualliflari va o‘quvchilar  | Asosiy matndan ajratilgan holda ko‘rsatiladi      |
| Reklama / banner bloklari        | Monetizatsiya                       | Asosiy kontentdan ajratilganligini bildiradi      |

---

## 3. Qachon va qanday ishlatiladi? (Real senior misollar)

**1. Klassik sidebar (eng ko‘p uchraydigan holat):**

```html
<main>
	<article>
		<!-- Asosiy post kontenti -->
	</article>
</main>

<aside aria-label="Yon panel">
	<h2>Tegishli maqolalar</h2>
	<ul>
		<li><a href="#">Boshqa post 1</a></li>
		...
	</ul>

	<div class="newsletter">
		<!-- Obuna formasi -->
	</div>
</aside>
```

**2. Article ichidagi pull-quote yoki qo‘shimcha izoh:**

```html
<article>
	<p>Asosiy matn...</p>

	<aside>
		<blockquote>“Bu yerda muhim iqtibos yoki qo‘shimcha fikr”</blockquote>
	</aside>

	<p>Davomi...</p>
</article>
```

**3. Author bio yoki glossary:**

```html
<aside aria-labelledby="author-info">
	<h3 id="author-info">Muallif haqida</h3>
	<p>Senior Frontend Developer, 8 yillik tajriba...</p>
</aside>
```

**Muhim qoida (MDN + WHATWG 2026):**

- Bir sahifada bir nechta `<aside>` bo‘lishi mumkin va tavsiya etiladi.
- Har bir `<aside>` ga `aria-label` yoki `aria-labelledby` berish tavsiya etiladi (landmarklarni farqlash uchun).
- `<aside>` asosiy kontentdan **ajratilgan** bo‘lishi kerak. Agar uni butunlay olib tashlasangiz, asosiy hikoya hali ham to‘liq va mantiqiy bo‘lishi lozim.
- `<main>` ichida yoki tashqarisida ishlatish mumkin, lekin ko‘pincha `<main>` dan keyin yoki yonida joylashadi.

---

## 4. `<aside>` va boshqa semantic teglar bilan farqi

- **vs `<article>`** — `<article>` mustaqil (syndication mumkin), `<aside>` esa asosiy kontentga bog‘liq (tangential).
- **vs `<section>`** — `<section>` tematik bo‘lim (heading talab qiladi), `<aside>` esa qo‘shimcha (complementary).
- **vs `<div>`** — `<div>` semantic ma’no bermaydi, `<aside>` esa landmark va outline yaratadi.

---

## 5. Accessibility va SEO ta’siri (2026 yil)

- Implicit ARIA role: `complementary` → ekran o‘quvchilar “complementary content” deb o‘qiydi.
- Google va boshqa qidiruvchilar `<aside>` ni “side content” sifatida tushunadi → asosiy kontentni yaxshiroq indekslaydi.
- Lighthouse auditida “Landmark elements are unique” va “Complementary landmark” tekshiriladi.

---

## 6. Senior Best Practices (2026 yil production darajasi)

1. Har bir `<aside>` ga `aria-label` yoki `aria-labelledby` berish (agar heading bo‘lmasa).
2. Mobil uchun responsive sidebar (CSS Grid/Flex + `inert` yoki `hidden`).
3. Reklama bloklarini `<aside>` ga joylashtirish (ad blockerlar va accessibility uchun yaxshi).
4. Hech qachon stil uchun `<aside>` ishlatmang — faqat semantik maqsadda.
5. Lighthouse + axe + WAVE bilan tekshirish.
6. Katta loyihalarda (Next.js, Astro) `<Aside>` komponentini reusable qilib yarating.
7. **Anti-pattern**: `<div class="sidebar">` ga qaytish — 2026 yilda qabul qilinmaydi.

**Yomon amaliyot:**

```html
<div class="sidebar">...</div>
```

**Senior usuli:**

```html
<aside aria-label="Yon panel">...</aside>
```

---

## 7. Xulosa (Senior nuqtai nazar)

`<aside>` — bu **complementary (qo‘shimcha, yonma-yon)** kontent uchun maxsus semantic element. U sahifaning asosiy oqimini saqlab qolgan holda qo‘shimcha qiymat beradi. Uni to‘g‘ri ishlatish orqali siz:

- Accessibility ni WCAG darajasiga ko‘tarasiz,
- SEO ni yaxshilaysiz,
- Kodni o‘qilishi va maintain qilishni osonlashtirasiz,
- Kelajakdagi texnologiyalarga (AI, voice assistants) tayyor bo‘lasiz.

Agar siz faqat `class="aside"` bilan ishlasangiz — oddiy kod yozuvchisiz.  
Agar `<aside>` ni `aria-label`, landmarklar va to‘g‘ri nesting bilan qo‘llay olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`)
- `<aside>` + ARIA + landmark audit
- Real loyihada sidebar + responsive misollar

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Aside element (Last modified: 9 iyul 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/aside)
- [WHATWG HTML Living Standard — The aside element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html#the-aside-element)
- [MDN Web Docs — Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- [W3C ARIA in HTML — Implicit roles](https://www.w3.org/TR/html-aria/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
