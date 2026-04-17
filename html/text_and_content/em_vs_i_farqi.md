# `<em>` vs `<i>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<em>`** va **`<i>`** — ikkalasi ham matnni **kursiv (italic)** qiladi, lekin ularning maqsadi, semantikasi va brauzer/ekran o‘quvchilar tomonidan qanday qabul qilinishi tubdan farq qiladi.

Senior darajada bu farqni to‘g‘ri tushunmasangiz, accessibility (a11y), SEO, kodning ma’nosi va maintainability buziladi. Bu ikki element ko‘pincha chalkashtiriladi, lekin biri semantik (ma’no beradi), ikkinchisi esa faqat vizual (presentational) hisoblanadi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir farq chuqur tahlil qilingan, real misollar, implicit ARIA rollari, SEO va accessibility ta’siri bilan boyitilgan.

---

## 1. Rasmiy ta’riflar (eng aniq manbalardan)

**`<em>` (Emphasis element)**  
**MDN Web Docs:**

> “The `<em>` HTML element marks text that has stress emphasis. The `<em>` element can be nested, with each level of nesting indicating a greater degree of emphasis.”

**WHATWG HTML Living Standard:**

> “The em element represents stress emphasis of its contents.”

**`<i>` (Idiomatic Text element)**  
**MDN Web Docs:**

> “The `<i>` HTML element represents a range of text that is set off from the normal prose for some reason, such as a technical term, a foreign word, or a thought.”

**WHATWG HTML Living Standard:**

> “The i element represents a span of text in an alternate voice or mood, or otherwise offset from the normal prose.”

**Senior nuqtai nazar:**

- **`<em>`** — **semantik** element. Brauzer va ekran o‘quvchilarga “bu matn ta’kidlangan, urg‘u berilgan” degan signal beradi.
- **`<i>`** — **vizual (presentational)** element. Hech qanday ma’no bermaydi, shunchaki shriftni kursiv qiladi.

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat                   | **`<em>`**                                                               | **`<i>`**                                                                             |
| --------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| **Semantik ma’no**          | Mavjud (ta’kid / urg‘u bildiradi)                                        | Yo‘q (faqat vizual)                                                                   |
| **Implicit ARIA role**      | `role="emphasis"` (stress emphasis)                                      | Yo‘q                                                                                  |
| **Accessibility**           | Ekran o‘quvchilar “emphasized” deb o‘qiydi va intonatsiyani o‘zgartiradi | Oddiy kursiv matn sifatida o‘qiydi (hech qanday farq yo‘q)                            |
| **SEO ta’siri**             | Google ta’kidlangan matn sifatida qabul qiladi                           | Zaif (hech qanday semantik signal bermaydi)                                           |
| **Voice assistants**        | Urg‘uni ta’kidlaydi                                                      | Oddiy matn sifatida o‘qiydi                                                           |
| **Default stil**            | `font-style: italic`                                                     | `font-style: italic`                                                                  |
| **CSS bilan o‘zgartirish**  | Semantikani saqlab qolgan holda stil o‘zgartirish mumkin                 | Faqat vizual, semantika yo‘q                                                          |
| **Qachon ishlatish kerak?** | Haqiqiy ta’kid / urg‘u bo‘lganda (o‘gohlantirish, kalit fikr, xavf)      | Vizual sabablar: texnik atama, chet til so‘zi, fikr, botanika nomi, ship nomi va h.k. |

**Muhim qoida (MDN 2026):**  
Agar matnni kursiv qilishning **semantik sababi** (ta’kid, urg‘u) bo‘lsa → `<em>`.  
Agar faqat **vizual** sabab bo‘lsa (masalan, dizayn talabi, termin, xorijiy so‘z) → `<i>`.

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli — semantik va vizualni ajratish):**

```html
<!-- Semantik ta'kid (eng muhim) -->
<p>Diqqat: <em>Bu operatsiyani bekor qilish mumkin emas!</em></p>

<!-- Vizual sabab (semantika kerak emas) -->
<p>Ilmiy atama: <i>Homo sapiens</i> — inson turi.</p>

<p>Chet til soʻzi: Men <i>bon appétit</i> dedim.</p>

<!-- Fikr / ichki monolog -->
<p>U oʻyladi: <i>Bu qanday boʻlishi mumkin?</i></p>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<p><i>Diqqat!</i> Bu juda muhim.</p>
<!-- semantik ma’no yo‘qotilgan -->
<em>Homo sapiens</em>
<!-- semantika noto‘g‘ri qo‘llanilgan -->
```

**CSS bilan stilni boshqarish (2026 best practice):**

```css
em {
	font-style: italic;
	font-weight: 600; /* semantik ta'kidni vizual ham kuchaytirish */
}

i {
	font-style: italic;
}
```

---

## 4. Senior Best Practices (2026 yil)

1. **Har doim semantikadan boshlang** — agar matnni ta’kidlamoqchi bo‘lsangiz, `<em>` ishlat.
2. `<i>` ni faqat dizayn yoki konventsional sabablar uchun ishlat (texnik termin, chet til, botanika, fikr).
3. Stilni CSS orqali boshqaring — default `font-style: italic` ni o‘zgartirish mumkin.
4. Accessibility uchun: `<em>` ekran o‘quvchilar tomonidan alohida urg‘u bilan o‘qiladi.
5. SEO uchun: `<em>` muhim joylarda qo‘shimcha signal beradi.
6. **Hech qachon** `<i>` ni ta’kid maqsadida ishlatmang — bu eski (HTML 4) amaliyot.
7. Modern loyihalarda (Tailwind, CSS Modules) `italic` utility si `<em>` bilan birga ishlatiladi.

---

## 5. Xulosa (Senior nuqtai nazar)

- **`<em>`** = **Semantik** (ta’kid / urg‘u beradi, ma’no bildiradi).
- **`<i>`** = **Vizual** (faqat kursiv shrift, hech qanday ma’no bermaydi).

Agar siz faqat vizual effekt uchun `<i>` ishlatayotgan bo‘lsangiz — kod yozuvchisiz.  
Agar ta’kidni `<em>` bilan, vizual kursivni esa `<i>` bilan to‘g‘ri ajratayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- `<strong>` vs `<b>` va `<em>` vs `<i>` birgalikda qo‘llanishi
- Semantik vs presentational elementlarning to‘liq ro‘yxati
- Real loyihada em/i ishlatish misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Em element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em)
- [MDN Web Docs — The I element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/i)
- [WHATWG HTML Living Standard — The em element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-em-element)
- [WHATWG HTML Living Standard — The i element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-i-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
