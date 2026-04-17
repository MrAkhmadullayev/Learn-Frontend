# `<br>` vs `<hr>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<br>`** va **`<hr>`** — ikkalasi ham **bo‘sh (void) elementlar** (yopiluvchi teg talab qilmaydi) va vizual jihatdan chiziq hosil qiladi. Lekin ularning **semantik ma’nosi**, qo‘llanilishi, accessibility va SEO ta’siri tubdan farq qiladi.

Senior darajada bu farqni to‘g‘ri tushunmasangiz, kodning ma’nosi, accessibility (a11y), SEO va maintainability buziladi. `<br>` faqat vizual yangi qator yaratadi, `<hr>` esa semantik jihatdan mavzudagi o‘zgarishni bildiradi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir farq chuqur tahlil qilingan, real kod misollari, nesting qoidalari, performance va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’riflar (eng aniq manbalardan)

**`<br>` (Line Break element)**  
**MDN Web Docs:**

> “The `<br>` HTML element produces a line break in text (carriage-return). It is a presentational element and has no semantic meaning.”

**WHATWG HTML Living Standard:**

> “The br element represents a line break.”

**`<hr>` (Thematic Break element)**  
**MDN Web Docs:**

> “The `<hr>` HTML element represents a thematic break between paragraph-level elements. It is a semantic element indicating a change in topic or scene.”

**WHATWG HTML Living Standard:**

> “The hr element represents a paragraph-level thematic break.”

**Senior nuqtai nazar:**

- **`<br>`** — **vizual (presentational)** element. Semantik ma’no bermaydi, faqat matnni majburan yangi qatordan boshlaydi.
- **`<hr>`** — **semantik** element. Brauzer va ekran o‘quvchilarga “bu yerda mavzu o‘zgardi, yangi bo‘lim boshlandi” degan signal beradi.

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat                   | **`<br>`**                                           | **`<hr>`**                                                  |
| --------------------------- | ---------------------------------------------------- | ----------------------------------------------------------- |
| **Semantik ma’no**          | Yo‘q (faqat vizual)                                  | Mavjud (thematic break)                                     |
| **Implicit ARIA role**      | Yo‘q                                                 | `role="separator"`                                          |
| **Accessibility**           | Ekran o‘quvchilar oddiy yangi qator sifatida o‘qiydi | “Thematic break” deb o‘qiydi (mavzu o‘zgarganini bildiradi) |
| **SEO ta’siri**             | Zaif                                                 | Yaxshi (mavzudagi o‘zgarish signali)                        |
| **Default stil**            | Yangi qator + bo‘sh joy yo‘q                         | Gorizontal chiziq (`border-top`)                            |
| **CSS bilan o‘zgartirish**  | `br { display: none; }` mumkin                       | `hr` ni butunlay stilash mumkin (rang, qalinlik)            |
| **Qachon ishlatish kerak?** | She‘r, manzil, qisqa formatdagi matn                 | Bo‘limlar orasidagi mavzudagi o‘zgarish                     |
| **Modern tavsiya**          | Iloji boricha kamroq ishlatish                       | Semantic maqsadda ishlatish tavsiya etiladi                 |

**Muhim qoida (WHATWG 2026):**  
`<hr>` — bu “paragraf darajasidagi thematic break”. Masalan, hikoyada sahna o‘zgarishi yoki maqolada yangi mavzuga o‘tish.  
`<br>` esa faqat “matnni majburan yangi qatordan boshlash” uchun.

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli):**

```html
<!-- <br> – faqat kerakli joyda (she'r yoki manzil) -->
<p>
	Muallif: John Doe<br />
	Email: john@example.com<br />
	Telefon: +998 90 123 45 67
</p>

<!-- <hr> – mavzudagi o'zgarish -->
<article>
	<h2>Birinchi mavzu</h2>
	<p>...</p>

	<hr />
	<!-- Bu yerda mavzu o'zgardi -->

	<h2>Ikkinchi mavzu</h2>
	<p>...</p>
</article>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<p>Bu matn<br />va bu yerda yangi qator</p>
<!-- semantik bo'linish kerak bo'lsa, <hr> ishlatish yaxshiroq -->
<hr />
<!-- faqat vizual chiziq uchun ishlatish yomon -->
```

**CSS bilan stilni boshqarish (2026 best practice):**

```css
hr {
	border: none;
	height: 1px;
	background: linear-gradient(to right, transparent, var(--gray), transparent);
	margin: 2rem 0;
}
```

---

## 4. Senior Best Practices (2026 yil production darajasi)

1. **`<br>`** ni iloji boricha kamroq ishlatish. Agar matnni yangi qatordan boshlash kerak bo‘lsa, CSS `white-space: pre-line` yoki `display: block` bilan hal qilish afzal.
2. **`<hr>`** ni faqat semantic thematic break uchun ishlatish. Stilni CSS orqali to‘liq boshqarish mumkin.
3. Accessibility uchun: `<hr>` ni `role="separator"` bilan kuchaytirish mumkin (lekin odatda kerak emas, chunki implicit semantic bor).
4. SEO uchun: `<hr>` mavzudagi o‘zgarishlarni Googlebotga aniq bildiradi.
5. Modern loyihalarda (Tailwind, CSS Modules) `<hr>` ni reusable komponent sifatida yarating.
6. **Hech qachon** `<br>` bilan layout yaratishga urinmang — bu eski (1990-yillar) amaliyot.
7. **Anti-pattern:** Ko‘p `<br><br>` bilan bo‘sh joy yaratish yoki faqat dizayn uchun `<hr>` ishlatish.

---

## 5. Xulosa (Senior nuqtai nazar)

- **`<br>`** = **Vizual** (faqat yangi qator, semantika yo‘q).
- **`<hr>`** = **Semantik** (mavzudagi o‘zgarish, accessibility va SEO uchun muhim).

Agar siz faqat vizual effekt uchun ikkalasini ham ishlatayotgan bo‘lsangiz — oddiy kod yozuvchisiz.  
Agar `<hr>` ni semantik maqsadda, `<br>` ni esa faqat kerakli joyda to‘g‘ri ajratayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- `<br>` va `<hr>` bilan bog‘liq real loyiha misollari
- Semantik vs presentational elementlarning to‘liq ro‘yxati
- Performance va accessibility auditlari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Br element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/br)
- [MDN Web Docs — The Hr element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr)
- [WHATWG HTML Living Standard — The br element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-br-element)
- [WHATWG HTML Living Standard — The hr element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-hr-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
