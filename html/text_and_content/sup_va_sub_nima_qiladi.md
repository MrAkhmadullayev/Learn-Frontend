# `<sup>` va `<sub>` Teglari Nima Qiladi? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<sup>`** (Superscript) va **`<sub>`** (Subscript) — HTML ning ikkita maxsus **inline** (phrasing content) elementi bo‘lib, matnni **yuqori indeks** (superscript) yoki **pastki indeks** (subscript) holatiga joylashtiradi. Ular nafaqat vizual effekt yaratadi, balki matnning **texnik, matematik, kimyoviy yoki ilmiy** ma’nosini ham semantik jihatdan bildiradi.

Senior darajada bu teglar shunchaki “shriftsiz o‘zgartirish” emas. Ular **semantik** elementlar bo‘lib, brauzer, ekran o‘quvchilar, qidiruv tizimlari va AI summarizerlar uchun matnning texnik ma’nosini aniq bildiradi. Noto‘g‘ri ishlatilsa (masalan, oddiy matnni vizual ravishda yuqori/pastki qilish uchun), accessibility, SEO va kodning ma’nosi buziladi. Zamonaviy loyihalarda ularni CSS `vertical-align` yoki MathML bilan birgalikda ishlatish tavsiya etiladi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir farq chuqur tahlil qilingan, real kod misollari, accessibility, SEO va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’riflar (eng aniq manbalardan)

**`<sup>` (Superscript element)**  
**MDN Web Docs:**

> “The `<sup>` HTML element specifies inline text which should be displayed as superscript for typographical reasons (e.g., exponents, footnotes).”

**WHATWG HTML Living Standard:**

> “The sup element represents a superscript.”

**`<sub>` (Subscript element)**  
**MDN Web Docs:**

> “The `<sub>` HTML element specifies inline text which should be displayed as subscript for typographical reasons (e.g., chemical formulas, mathematical variables).”

**WHATWG HTML Living Standard:**

> “The sub element represents a subscript.”

**Senior nuqtai nazar:**  
Ikkalasi ham **semantik** elementlar. Ular faqat texnik/matematik/kimyoviy ma’noga ega bo‘lgan matnlarda ishlatilishi kerak. Oddiy vizual effekt uchun CSS `vertical-align: super/sub` yoki `font-variant-position` (yangi) ishlatish afzal.

---

## 2. Batafsil taqqoslash jadvali (Senior daraja)

| Xususiyat                       | **`<sup>`** (Superscript)                        | **`<sub>`** (Subscript)                           |
| ------------------------------- | ------------------------------------------------ | ------------------------------------------------- |
| **Vizual effekt**               | Matnni yuqoriga ko‘taradi                        | Matnni pastga tushiradi                           |
| **Eng ko‘p ishlatiladigan joy** | Darajalar, kvadrat/kub, footnote, 10³, x²        | Kimyoviy formulalar, matematik indekslar, H₂O, x₁ |
| **Semantik ma’no**              | Yuqori indeks (exponent, power, ordinal)         | Pastki indeks (subscript, chemical, variable)     |
| **Accessibility**               | Ekran o‘quvchilar “superscript” deb o‘qiydi      | Ekran o‘quvchilar “subscript” deb o‘qiydi         |
| **SEO ta’siri**                 | Matematik/kimyoviy kontentni yaxshiroq tushunadi | Xuddi shunday                                     |
| **Default shrift o‘lchami**     | Kichikroq (browser ~75%)                         | Kichikroq (browser ~75%)                          |
| **CSS bilan boshqarish**        | `vertical-align: super`                          | `vertical-align: sub`                             |
| **Qachon ishlatish kerak?**     | Haqiqiy yuqori indeks bo‘lganda                  | Haqiqiy pastki indeks bo‘lganda                   |

**Muhim qoida (WHATWG 2026):**  
Ular faqat **texnik** yoki **matematik** ma’noga ega bo‘lganda ishlatilishi kerak. Oddiy matnni vizual ravishda yuqori/pastki qilish uchun CSS (`vertical-align`) ishlatish tavsiya etiladi.

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli — semantik va texnik):**

```html
<!-- Matematika -->
<p>a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup></p>

<!-- Kimyo -->
<p>Suvning formulas: H<sub>2</sub>O</p>

<!-- Ilmiy atama / daraja -->
<p>10<sup>6</sup> (million) va 10<sup>-3</sup> (milli)</p>

<!-- Footnote raqami -->
<p>Bu juda muhim fikr.<sup>1</sup></p>

<!-- Kombinatsiya (ikkalasini birga) -->
<p>x<sub>1</sub><sup>2</sup> + x<sub>2</sub><sup>3</sup></p>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<p>Bu matnni<sup>yuqoriga</sup> ko‘tarish kerak edi.</p>
<!-- semantik ma’no yo‘q -->
<p>H<sub>2</sub>O ni <sub>pastki</sub> qilish</p>
<!-- noto‘g‘ri joyda -->
```

**CSS bilan stilni boshqarish (2026 best practice):**

```css
sup,
sub {
	font-size: 0.75em;
	line-height: 0;
	vertical-align: baseline;
}

sup {
	vertical-align: super;
}
sub {
	vertical-align: sub;
}
```

---

## 4. Senior Best Practices (2026 yil)

1. **Har doim semantik maqsadda** ishlatish. Vizual effekt uchun CSS `vertical-align: super/sub` yoki `font-variant-position: super/sub` (yangi) ishlatish afzal.
2. Matematik kontent uchun MathML bilan birgalikda ishlatish (zamonaviy loyihalarda tavsiya etiladi).
3. Stilni CSS orqali to‘liq boshqarish.
4. Accessibility uchun: katta formulalarda `aria-label` qo‘shish mumkin (masalan, “H 2 O”).
5. SEO uchun: ilmiy, texnik va matematik sahifalarda `<sup>` va `<sub>` Google va AI summarizerlarga yordam beradi.
6. Modern loyihalarda (Tailwind, Astro) `sup` va `sub` ni reusable komponent sifatida yarating.
7. **Anti-pattern:** Oddiy vizual effekt uchun ularni ishlatish yoki `<span>` bilan almashtirish.

---

## 5. Xulosa (Senior nuqtai nazar)

- **`<sup>`** → **Yuqori indeks** (daraja, kvadrat, footnote).
- **`<sub>`** → **Pastki indeks** (kimyo, matematik o‘zgaruvchi).

Ikkalasi ham **semantik** elementlar bo‘lib, faqat texnik/matematik/kimyoviy ma’noga ega matnlarda ishlatilishi kerak. Oddiy vizual effekt uchun ularni ishlatish — eski va noto‘g‘ri amaliyot.

Agar siz faqat shriftni o‘zgartirish uchun `<sup>` va `<sub>` ishlatayotgan bo‘lsangiz — oddiy kod yozuvchisiz.  
Agar ularni to‘g‘ri semantika, accessibility va matematik kontent bilan birgalikda qo‘llayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- MathML bilan birgalikda matematik formulalar yaratish
- `<sup>` va `<sub>` bilan bog‘liq accessibility optimizatsiyasi
- Real loyihada ilmiy kontent misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Sup element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sup)
- [MDN Web Docs — The Sub element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sub)
- [WHATWG HTML Living Standard — The sup element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-sup-element)
- [WHATWG HTML Living Standard — The sub element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-sub-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
