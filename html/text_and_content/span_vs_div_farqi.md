# **`<span>` vs `<div>` Farqi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)**

**`<span>`** va **`<div>`** — HTML ning ikkita eng ko‘p ishlatiladigan, lekin **hech qanday semantik ma’no bermaydigan** (generic) elementlari. Ular faqat **vizual yoki JavaScript maqsadida** ishlatiladi va brauzer, qidiruv tizimlari, ekran o‘quvchilar yoki AI summarizerlarga kontentning ma’nosini bildirishmaydi.

Senior darajada bu ikki elementni chalkashtirish yoki noto‘g‘ri joyda ishlatish “div soup” (divlar to‘plami) muammosiga olib keladi, kodni chalkashtiradi, accessibility va SEO ni zaiflashtiradi. Ularning asosiy farqi — **display xususiyati**, **joylashuv xatti-harakati** va **foydalanish konteksti**da yotadi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, nesting qoidalari, performance va modern best practices bilan boyitilgan.

---

## 1. Rasmiy ta’riflar

**`<div>` (Division element)**  
**MDN Web Docs:**

> “The `<div>` HTML element is the generic container for flow content. It has no special meaning and is used to group elements for styling or scripting purposes.”

**WHATWG HTML Living Standard:**

> “The div element has no special meaning at all. It is a generic flow content element that can be used to group other elements.”

**`<span>` (Span element)**  
**MDN Web Docs:**

> “The `<span>` HTML element is a generic inline container for phrasing content, which does not inherently represent anything.”

**WHATWG HTML Living Standard:**

> “The span element has no special meaning and is used to group phrasing content for styling or scripting purposes.”

**Senior nuqtai nazar:**  
Ikkalasining ham **semantikasi yo‘q**. Ular faqat dizayn yoki JS maqsadida ishlatiladi. Agar kontentning ma’nosi bo‘lsa — `<p>`, `<article>`, `<section>`, `<header>` kabi semantic teglardan foydalaning.

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat                       | **`<div>`**                                              | **`<span>`**                                                       |
| ------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| **Display turi (default)**      | `display: block`                                         | `display: inline`                                                  |
| **Joylashuv**                   | Yangi qatordan boshlanadi, to‘liq kenglikni egallaydi    | Matn oqimi ichida qoladi, yangi qator yaratmaydi                   |
| **Kenglik / Balandlik**         | To‘liq kenglikni egallaydi (agar belgilansa)             | Faqat kontent kengligini egallaydi                                 |
| **Semantik ma’no**              | Yo‘q (generic container)                                 | Yo‘q (generic inline container)                                    |
| **Implicit ARIA role**          | Yo‘q                                                     | Yo‘q                                                               |
| **Ichiga nima qo‘yish mumkin?** | Block va inline elementlar (h1, p, div, span va h.k.)    | Faqat inline (phrasing content): matn, a, strong, em, span va h.k. |
| **SEO ta’siri**                 | Zaif (struktura bermaydi)                                | Zaif                                                               |
| **Accessibility**               | Zaif (landmark bermaydi)                                 | Zaif                                                               |
| **Eng ko‘p ishlatiladigan joy** | Layout konteyneri, wrapper, flex/grid container, section | Matn ichidagi stil (rang, shrift, hover, icon)                     |
| **CSS bilan o‘zgartirish**      | `display: flex`, `grid`, `inline` qilish mumkin          | `display: block`, `inline-block` qilish mumkin                     |

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli):**

```html
<!-- <div> – layout va struktura uchun -->
<div class="card">
	<h2>Kartochka sarlavhasi</h2>
	<p>Matn paragrafi...</p>
</div>

<!-- <span> – matn ichidagi kichik o‘zgarish uchun -->
<p>
	Bu oddiy matn. <span class="highlight">Muhim qism</span> shu yerda ajratilgan.
</p>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<span class="container">
	<!-- noto‘g‘ri! block elementlarni inline ga joylashtirish -->
	<h2>Sarlavha</h2>
</span>

<div class="price">120 000 soʻm</div>
<!-- matn uchun div ishlatish yomon amaliyot -->
```

**CSS bilan o‘zgartirish misoli:**

```css
/* <span> ni block qilish mumkin, lekin kodni chalkashtiradi */
span.block {
	display: block;
}

/* <div> ni inline qilish mumkin */
div.inline {
	display: inline;
}
```

---

## 4. Senior darajadagi muhim nuqtalar (2026 yil best practices)

1. **Hech qachon** semantik maqsadda `<div>` yoki `<span>` ishlatmang. Agar kontentning ma’nosi bo‘lsa — semantic teglardan foydalaning (`<p>`, `<article>`, `<section>` va h.k.).
2. **“Div soup” dan qoching** — ko‘p nesting DOM ni kattalashtiradi va renderingni sekinlashtiradi.
3. **CSS bilan o‘zgartirish mumkin**, lekin bu kodni chalkashtiradi va maintain qilishni qiyinlashtiradi. Imkon qadar default display turini saqlang.
4. **Accessibility**: Ikkalasining ham implicit role yo‘q. Shuning uchun `role`, `aria-label` va h.k. kerak bo‘lganda qo‘shish talab etiladi.
5. **Modern CSS / Tailwind** da:
   - `<div>` — container, flex/grid wrapper, card kabi struktura uchun.
   - `<span>` — inline text elementlarni stilash uchun (highlight, badge, icon).
6. **Performance**: Semantic teglarni imkon qadar ko‘proq ishlatib, generic elementlar sonini kamaytiring.

---

## 5. Xulosa (Senior nuqtai nazar)

- **`<div>`** — **block konteyneri** (layout, wrapper, struktura uchun).
- **`<span>`** — **inline matn elementi** (faqat matn ichidagi kichik o‘zgarishlar uchun).

Ikkalasining ham semantikasi yo‘q, shuning uchun ularni faqat **stil yoki JavaScript** maqsadida ishlatish kerak. Agar kontentning ma’nosi bo‘lsa — **semantic teglar** ishlatish shart.

Agar siz faqat `<div>` va `<span>` bilan kod yozayotgan bo‘lsangiz — siz “div soup” yaratayapsiz.  
Agar to‘g‘ri joyda semantic teglar, to‘g‘ri joyda `<div>` yoki `<span>` ishlatayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- Div soup va semantic HTML real loyiha misollari
- Tailwind + semantic taglar bilan to‘liq komponent yaratish
- Performance va accessibility auditlari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The div element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div)
- [MDN Web Docs — The span element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span)
- [WHATWG HTML Living Standard — The div element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-div-element)
- [WHATWG HTML Living Standard — The span element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-span-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
