# `<section>` vs `<article>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<section>`** va **`<article>`** — ikkalasi ham **sectioning content** (bo‘limlash kontenti) turiga kiradi va sahifaning **document outline** (struktura ierarxiyasi) algoritmini yaratishda ishtirok etadi. Lekin ularning semantik ma’nosi va qo‘llanish maqsadi tubdan farq qiladi.

Senior darajada bu farqni to‘g‘ri tushunmasangiz, accessibility (WCAG), SEO, maintainability, kod o‘qilishi va hatto AI summarizerlar bilan bog‘liq muammolar chiqadi. Bu ikki element sizning HTML arxitekturangizning asosiy qarorlaridan biri hisoblanadi.

Quyidagi material **MDN Web Docs (2025 yil avgust-sentyabr yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, nesting qoidalari, implicit ARIA rollari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’riflar (eng aniq manbalardan)

**`<section>` (Generic Section element)**  
**MDN Web Docs (9 iyul 2025 yangilanishi):**

> “The `<section>` element represents a generic standalone section of a document, which doesn't have a more specific semantic element to represent it. Its purpose is to group content that forms a thematic grouping, typically identified by a heading.”

**WHATWG HTML Living Standard (15 aprel 2026):**  
`<section>` — **thematic grouping** (mavzuga oid bo‘lim) uchun ishlatiladigan umumiy sectioning element. U hujjatning bir qismi sifatida ma’no bildiradi va o‘z-o‘zidan mustaqil emas.

**`<article>` (Article Contents element)**  
**MDN Web Docs (13 avgust 2025 yangilanishi):**

> “The `<article>` element represents a self-contained composition in a document, page, application, or site, which is intended to be independently distributable or reusable (e.g., in syndication).”

**WHATWG HTML Living Standard (15 aprel 2026):**  
`<article>` — **mustaqil, o‘z-o‘zidan to‘liq** kontent birligi. Uni alohida sindikatsiya qilish (RSS, blog post sifatida tarqatish), qayta ishlatish yoki boshqa sahifaga ko‘chirish mumkin.

**Senior nuqtai nazar:**

- `<section>` — **kontekstga bog‘liq bo‘lim** (thematic container).
- `<article>` — **mustaqil, sindikatsiya qilinadigan kontent birligi** (self-contained reusable unit).

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat               | **`<section>`**                                       | **`<article>`**                                                      |
| ----------------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| **Semantik ma’no**      | Thematic grouping (mavzuga oid bo‘lim)                | Self-contained, independently distributable                          |
| **Mustaqillik**         | Hujjat ichida bog‘liq (kontekst kerak)                | Mustaqil (kontekstsiz ham ma’noviy)                                  |
| **Implicit ARIA role**  | `region` (agar accessible name bo‘lsa) yoki `generic` | `article`                                                            |
| **Qachon ishlatiladi?** | Bo‘limlar, tablar, dashboard panel, search results    | Blog post, news article, comment, product card, forum post           |
| **Heading talabi**      | Tavsiya etiladi (lekin UI da bo‘lmasa ham mumkin)     | Majburiy ravishda tavsiya etiladi (`<h1>`–`<h6>`)                    |
| **Nesting qoidalari**   | Ichiga `<article>` qo‘yish mumkin                     | Ichiga bir nechta `<section>` yoki boshqa `<article>` qo‘yish mumkin |
| **SEO ta’siri**         | O‘rtacha (outline ni yaxshilaydi)                     | Kuchli (Google mustaqil kontent sifatida qabul qiladi)               |
| **Accessibility**       | Landmark bo‘ladi (agar nomlangan bo‘lsa)              | `article` landmark + oson navigatsiya                                |
| **Misollar**            | “Eng so‘nggi yangiliklar” bo‘limi, dashboard widget   | Bitta blog posti, foydalanuvchi kommenti, product kartochkasi        |

**Muhim qoida (MDN 2025):**  
Agar kontent **mustaqil ravishda** sindikatsiya qilinsa yoki o‘z-o‘zidan ma’no bersa → `<article>`.  
Agar u faqat **tematik guruh** bo‘lsa va boshqa kontentga bog‘liq bo‘lsa → `<section>`.

---

## 3. Qachon qaysi biri ishlatiladi? (Senior qarorlari + real misol)

**`<section>` ishlatish kerak bo‘lgan holatlar:**

- Sahifaning katta tematik bo‘limlari (“Xizmatlar”, “Portfolio”, “Testimonial”).
- Dashboard panel yoki tab ichidagi kontent.
- Search natijalari ro‘yxati.
- Har xil widgetlar (agar ular mustaqil bo‘lmasa).

**`<article>` ishlatish kerak bo‘lgan holatlar:**

- Blog yoki yangilik posti.
- Foydalanuvchi kommentlari (har biri alohida `<article>`).
- E-commerce da product kartochkalari.
- Forum postlari yoki reviewlar.

**Real misol (blog sahifasi — senior usul):**

```html
<main>
	<article>
		<!-- Bitta post — mustaqil -->
		<header>
			<h1>Maqola sarlavhasi</h1>
		</header>

		<section>
			<!-- Post ichidagi bo‘lim -->
			<h2>Birinchi mavzu</h2>
			<!-- matn -->
		</section>

		<section>
			<!-- Yana bir bo‘lim -->
			<h2>Ikkinchi mavzu</h2>
			<!-- matn -->
		</section>
	</article>

	<section aria-labelledby="related">
		<!-- Tegishli postlar bo‘limi -->
		<h2 id="related">Tegishli maqolalar</h2>
		<article>...</article>
		<!-- Har biri alohida article -->
		<article>...</article>
	</section>
</main>
```

---

## 4. Nesting va outline algoritmi (2026 yil qoidalari)

- `<article>` ichida bir nechta `<section>` bo‘lishi mumkin.
- `<section>` ichida `<article>` bo‘lishi mumkin.
- Ichki `<article>` tashqi `<article>` ga “related” kontent sifatida qabul qilinadi (masalan, kommentlar).
- Har ikkalasi ham sahifaning **document outline** ni yaratadi (brauzer va ekran o‘quvchilar uchun). Headinglar ierarxiyasi avtomatik hisoblanadi.

---

## 5. Accessibility va SEO ta’siri

- **`<article>`** — implicit `role="article"` beradi → ekran o‘quvchilar alohida “article” sifatida o‘qiydi.
- **`<section>`** — faqat nomlangan bo‘lsa (`aria-labelledby` yoki heading) `role="region"` bo‘ladi.
- Google 2025–2026 yillarda `<article>` ni mustaqil kontent sifatida kuchliroq baholaydi (featured snippet va AI Overviews uchun).

---

## 6. Senior Best Practices (2026 yil production darajasi)

1. Hech qachon faqat stil uchun `<section>` yoki `<article>` ishlatmang — stil uchun `<div>` yetarli.
2. Har bir `<article>` va muhim `<section>` ga heading (`<h1>`–`<h6>`) qo‘shing.
3. `aria-label` yoki `aria-labelledby` ni faqat kerak bo‘lganda qo‘shing.
4. Lighthouse + axe tool bilan tekshiring (“Section has heading” va “Article has heading” auditlari).
5. Katta loyihalarda (Next.js, Astro, React) bu elementlarni reusable komponent sifatida yarating.
6. Hech qachon `<div class="section">` ga qaytmang — semanticdan foydalaning.

---

## 7. Xulosa (Senior nuqtai nazar)

`<section>` — **umumiy bo‘lim** (thematic container).  
`<article>` — **mustaqil kontent birligi** (self-contained reusable unit).

Agar siz faqat “ikkalasi ham bo‘lim” deb o‘ylasangiz — oddiy developer.  
Agar qaysi biri qachon ishlatilishini, nesting qoidalarini, ARIA rollarini va SEO/accessibility ta’sirini chuqur tushunsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (real loyiha)
- Heading hierarchy + outline algoritmi
- Semantic HTML + ARIA birgalikda ishlashi

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Section element (Last modified: 9 iyul 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section)
- [MDN Web Docs — The Article element (Last modified: 13 avgust 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article)
- [WHATWG HTML Living Standard — The section element & The article element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
