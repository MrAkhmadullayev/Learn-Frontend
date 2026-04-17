# `<strong>` vs `<b>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<strong>`** va **`<b>`** — ikkalasi ham matnni **qalin (bold)** qiladi, lekin ularning maqsadi, semantikasi va brauzer/ekran o‘quvchilar tomonidan qanday qabul qilinishi tubdan farq qiladi.

Senior darajada bu farqni to‘g‘ri tushunmasangiz, accessibility (a11y), SEO, kodning ma’nosi va maintainability buziladi. Bu ikki element ko‘pincha chalkashtiriladi, lekin ularning biri semantik (ma’no beradi), ikkinchisi esa faqat vizual (presentational) hisoblanadi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir farq chuqur tahlil qilingan, real misollar, implicit ARIA rollari, SEO va accessibility ta’siri bilan boyitilgan.

---

## 1. Rasmiy ta’riflar (eng aniq manbalardan)

**`<strong>` (Strong Importance element)**  
**MDN Web Docs:**

> “The `<strong>` HTML element indicates that its contents have strong importance, seriousness, or urgency.”

**WHATWG HTML Living Standard:**

> “The strong element represents strong importance, seriousness, or urgency for its contents.”

**`<b>` (Bring Attention To element)**  
**MDN Web Docs:**

> “The `<b>` HTML element draws the reader’s attention to the element’s contents, which are not otherwise given special importance.”

**WHATWG HTML Living Standard:**

> “The b element represents a span of text to which attention is being drawn for utilitarian purposes, without conveying any extra importance.”

**Senior nuqtai nazar:**

- **`<strong>`** — **semantik** element. Brauzer va ekran o‘quvchilarga “bu matn juda muhim” degan signal beradi.
- **`<b>`** — **vizual (presentational)** element. Hech qanday ma’no bermaydi, shunchaki shriftni qalin qiladi.

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat                   | **`<strong>`**                                                         | **`<b>`**                                                                                 |
| --------------------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Semantik ma’no**          | Mavjud (muhimlik bildiradi)                                            | Yo‘q (faqat vizual)                                                                       |
| **Implicit ARIA role**      | `role="strong"` (strong emphasis)                                      | Yo‘q                                                                                      |
| **Accessibility**           | Ekran o‘quvchilar “strong emphasis” deb o‘qiydi va ta’kidlaydi         | Oddiy qalin matn sifatida o‘qiydi (hech qanday farq yo‘q)                                 |
| **SEO ta’siri**             | Google muhimlik signali sifatida qabul qiladi                          | Zaif (hech qanday semantik signal bermaydi)                                               |
| **Voice assistants**        | Muhimligini ta’kidlaydi                                                | Oddiy matn sifatida o‘qiydi                                                               |
| **Default stil**            | `font-weight: bold`                                                    | `font-weight: bold`                                                                       |
| **CSS bilan o‘zgartirish**  | Semantikani saqlab qolgan holda stil o‘zgartirish mumkin               | Faqat vizual, semantika yo‘q                                                              |
| **Qachon ishlatish kerak?** | Haqiqiy muhimlik bo‘lganda (o‘gohlantirish, kalit so‘z, xavf, urgency) | Faqat vizual e’tiborni tortish kerak bo‘lganda (brend nomi, mahsulot nomi, dizayn talabi) |

**Muhim qoida (MDN 2026):**  
Agar matnni qalin qilishning **semantik sababi** bo‘lsa → `<strong>`.  
Agar faqat **vizual** sabab bo‘lsa (masalan, dizayn talabi, UI kit’da belgilangan stil) → `<b>`.

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli — semantik va vizualni ajratish):**

```html
<!-- Semantik muhimlik -->
<p>
	Diqqat:
	<strong>Bu operatsiya qaytmas oqibatlarga olib kelishi mumkin!</strong>
</p>

<!-- Vizual e’tibor (semantika kerak emas) -->
<p>Brend nomi: <b>Grok</b> — xAI tomonidan yaratilgan.</p>

<!-- Kalit so‘zlar (SEO uchun) -->
<p>
	Bu sahifada <strong>HTML semantic teglar</strong> haqida to‘liq ma’lumot
	berilgan.
</p>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<p><b>Diqqat!</b> Bu juda muhim.</p>
<!-- semantik ma’no yo‘qotilgan -->
<strong>Brend nomi: Grok</strong>
<!-- semantika noto‘g‘ri qo‘llanilgan -->
```

**CSS bilan stilni boshqarish (2026 best practice):**

```css
strong {
	font-weight: 700;
	color: var(--accent-red); /* muhimlikni vizual ham kuchaytirish */
}

b {
	font-weight: 700;
}
```

---

## 4. Senior Best Practices (2026 yil)

1. **Har doim semantikadan boshlang** — agar matn muhim bo‘lsa, `<strong>` ishlat.
2. `<b>` ni faqat dizayn talabi bo‘lganda (masalan, UI kit’da belgilangan stil, brend nomi, mahsulot nomi) ishlat.
3. Stilni CSS orqali boshqaring — default `font-weight: bold` ni o‘zgartirish mumkin.
4. Accessibility uchun: `<strong>` ni ishlatganda ekran o‘quvchilar avtomatik ta’kidlaydi.
5. SEO uchun: `<strong>` kalit so‘zlar va muhim fikrlarni ta’kidlaydi (Google muhimlik signali sifatida qabul qiladi).
6. **Hech qachon** `<b>` ni semantik maqsadda ishlatmang — bu eski (HTML 4) amaliyot.
7. Modern loyihalarda (Tailwind, CSS Modules) `font-bold` utility si `<strong>` bilan birga ishlatiladi.

---

## 5. Xulosa (Senior nuqtai nazar)

- **`<strong>`** = **Semantik** (ma’no beradi, muhimlik bildiradi).
- **`<b>`** = **Vizual** (faqat shriftni qalin qiladi, ma’no bermaydi).

Agar siz faqat vizual effekt uchun `<b>` ishlatayotgan bo‘lsangiz — kod yozuvchisiz.  
Agar muhimlikni `<strong>` bilan bildirayotgan bo‘lsangiz va qolgan hollarda `<b>` ni to‘g‘ri ajratayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- `<em>` vs `<i>` farqi (kursiv analogi)
- Semantik vs presentational elementlarning to‘liq ro‘yxati
- Real loyihada strong/b ishlatish misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Strong element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong)
- [MDN Web Docs — The B element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/b)
- [WHATWG HTML Living Standard — The strong element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-strong-element)
- [WHATWG HTML Living Standard — The b element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-b-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
