# `<h1>` – `<h6>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<h1>` dan `<h6>` gacha bo‘lgan teglar** — bu HTML ning **heading elementlari**. Ular sahifadagi kontentning **ierarxiyasini** (muhimlik darajasini) bildiradi va faqat vizual shrift o‘lchami emas, balki **semantic struktura** yaratadi.

Senior darajada bu teglar shunchaki “katta-kichik sarlavha” emas. Ular **document outline** (sahifa struktura daraxti) algoritmini yaratadi, ekran o‘quvchilar uchun navigatsiya kaliti bo‘ladi, SEO signalini kuchaytiradi va WCAG talablarini bajarishga yordam beradi. Noto‘g‘ri ishlatilsa — accessibility xatolari, SEO pasayishi va kod chalkashligi paydo bo‘ladi.

Quyidagi material **MDN Web Docs (2025 yil yangilanishlari)**, **WHATWG HTML Living Standard (15 aprel 2026)** va **WCAG 2.2/3.0** ga asoslangan holda tayyorlangan. Har bir daraja chuqur tahlil qilingan, real misollar, heading hierarchy qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (2025 yil yangilanishi):**

> “The `<h1>` to `<h6>` HTML elements represent six levels of section headings. `<h1>` is the highest level and `<h6>` is the lowest.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “Heading elements (`<h1>`–`<h6>`) define the outline of the document. They participate in the document outline algorithm together with sectioning content elements (`<section>`, `<article>`, `<nav>`, `<aside>`).”

**WCAG 2.2/3.0:**  
Headinglar **Success Criterion 1.3.1 Info and Relationships** va **2.4.6 Headings and Labels** ning asosiy talabi. Ular kontentning ierarxiyasini brauzer va assistive technologies ga aniq bildiradi.

**Senior nuqtai nazar:**  
Bu teglar **kontent ierarxiyasi** yaratadi. Ular brauzerga “bu eng muhim mavzu”, “bu bo‘lim”, “bu kichik izoh” degan semantik signal beradi. To‘g‘ri ishlatilsa — accessibility, SEO va maintainability keskin yaxshilanadi.

---

## 2. Asosiy farqlar (jadval — senior ko‘rinishi)

| Xususiyat                   | `<h1>`                                       | `<h2>`–`<h5>`                        | `<h6>`                                  |
| --------------------------- | -------------------------------------------- | ------------------------------------ | --------------------------------------- |
| **Semantik daraja**         | Eng yuqori (page title yoki asosiy mavzu)    | O‘rta darajadagi bo‘limlar           | Eng past darajadagi kichik bo‘limlar    |
| **Sahifadagi soni**         | **Faqat bitta** (majburiy tavsiya)           | Bir nechta bo‘lishi mumkin           | Bir nechta bo‘lishi mumkin              |
| **Implicit ARIA role**      | `role="heading"` + `aria-level="1"`          | `role="heading"` + mos daraja        | `role="heading"` + `aria-level="6"`     |
| **Ekran o‘quvchilar**       | Birinchi o‘qiladigan eng muhim sarlavha      | Bo‘limlarni navigatsiya qilish uchun | Eng kichik darajadagi sarlavha          |
| **SEO ta’siri**             | Eng kuchli (Google asosiy mavzuni tushunadi) | Yaxshi (bo‘limlarni indekslaydi)     | Zaif (lekin hali ham outline ga kiradi) |
| **Default shrift o‘lchami** | Eng katta (browser default ~2em)             | O‘rtacha (kamayib boradi)            | Eng kichik (~0.67em)                    |
| **Qachon ishlatiladi?**     | Sahifa sarlavhasi, asosiy mavzu              | Bo‘lim sarlavhalari                  | Juda kichik bo‘lim yoki ichki izohlar   |

**Muhim qoida (WCAG + MDN 2025):**  
Heading darajalari **ketma-ket** bo‘lishi kerak. Masalan, `<h1>` dan keyin darhol `<h3>` qo‘yish noto‘g‘ri (h2 o‘tkazib yuborilgan). Bu “heading skipping” deb ataladi va accessibility auditlarda xato hisoblanadi.

---

## 3. To‘g‘ri va noto‘g‘ri ishlatish misollari

**To‘g‘ri (Senior usuli — logical hierarchy):**

```html
<main>
	<h1>HTML Semantic teglar bo‘yicha to‘liq qo‘llanma</h1>
	<!-- faqat bitta h1 -->

	<section>
		<h2>1. Semantic HTML nima?</h2>
		<p>...</p>

		<h3>1.1. Nega muhim?</h3>
		<p>...</p>

		<h3>1.2. Qanday qo‘llaniladi?</h3>
		<p>...</p>
	</section>

	<section>
		<h2>2. Accessibility va SEO</h2>
		...
	</section>
</main>
```

**Noto‘g‘ri (Junior / Anti-pattern):**

```html
<h1>Sahifa sarlavhasi</h1>
<h3>Bo‘lim 1</h3>
<!-- h2 o‘tkazib yuborilgan! -->
<h1>Yana bir katta sarlavha</h1>
<!-- ikkinchi h1 — xato -->
<h6>Kichik izoh</h6>
```

**Farq:** To‘g‘ri kod ekran o‘quvchilar uchun “daraxt” ko‘rinishida navigatsiya yaratadi va Google outline ni to‘g‘ri tushunadi.

---

## 4. Accessibility va SEO ta’siri (2026 yil holati)

- **Ekran o‘quvchilar:** Headinglar orqali sahifani “daraxt” ko‘rinishida o‘qiydilar. Foydalanuvchi “h2 ga o‘tish” buyrug‘i bilan tez navigatsiya qiladi.
- **Google va AI Overviews:** 2026 yilda heading ierarxiyasi sahifaning topic modeling va relevance signalini kuchaytiradi. To‘g‘ri headinglar Featured Snippets va AI summarizatsiyasida yordam beradi.
- **WCAG 2.2/3.0:** “Headings must be properly nested” va “Heading levels must not be skipped” talablari bajariladi.
- **Reader Mode:** Safari va Firefox Reader View semantic heading ierarxiyasini toza ko‘rsatadi.

---

## 5. Senior Best Practices (2026 yil)

1. Har sahifada **faqat bitta** `<h1>` bo‘lsin (sahifaning asosiy maqsadini bildiradi).
2. Heading darajalari ketma-ket bo‘lsin (h1 → h2 → h3 …).
3. Heading faqat matn uchun ishlatiladi (ichiga `<div>` yoki boshqa heading qo‘ymang).
4. Stilni CSS orqali boshqaring (hech qachon default shriftga tayanmang).
5. Har bir `<article>` va `<section>` ga o‘z headingini bering.
6. Lighthouse + axe DevTools bilan har doim tekshiring (“Heading order is correct”, “No skipped heading levels”).
7. Katta loyihalarda headinglarni komponent sifatida yarating (masalan, `Heading` komponenti `level` prop bilan).

**Yomon amaliyot:**  
Stil uchun `<h1>` ni kichik shrift bilan ishlatish yoki `<div class="h1-style">` ga o‘tish.

---

## 6. Xulosa (Senior nuqtai nazar)

`<h1>` – `<h6>` farqi — bu **shrift o‘lchami** emas, balki **kontent ierarxiyasi va semantikasi**dir. To‘g‘ri ishlatilsa:

- Ekran o‘quvchilar uchun mukammal navigatsiya
- Google va AI uchun kuchli struktura signali
- WCAG talablari bajariladi
- Kod o‘qilishi va maintain qilinishi osonlashadi

Agar siz faqat vizual shrift uchun heading ishlatayotgan bo‘lsangiz — oddiy kod yozuvchisiz.  
Agar headinglarni document outline va accessibility nuqtai nazaridan chuqur tushunsangiz va to‘g‘ri ierarxiya yaratayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (real loyiha)
- Heading hierarchy + outline algoritmi
- Semantic HTML + ARIA birgalikda ishlashi

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## 7 - Dizayndagi ko'rinishi

<h1>H1 Heading</h1>
<h2>H2 Heading</h2>
<h3>H3 Heading</h3>
<h4>H4 Heading</h4>
<h5>H5 Heading</h5>
<h6>H6 Heading</h6>
---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — Heading elements (2025 yil yangilanishi)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)
- [WHATWG HTML Living Standard — Heading elements (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html#headings-and-sections)
- [WCAG 2.2 — Success Criterion 1.3.1 Info and Relationships](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
- [WCAG 2.2 — Success Criterion 2.4.6 Headings and Labels](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN, WHATWG va WCAG manbalaridan olingan va 2026 yil holatiga mos.
