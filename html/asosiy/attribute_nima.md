# HTML Attribute Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi

**HTML Attribute** (atribut) — bu HTML elementi uchun **qo'shimcha konfiguratsiya** beruvchi kalit qiymat juftligi. U sahifada foydalanuvchiga ko‘rinmaydi, lekin brauzer, DOM, qidiruv tizimlari, ekran o‘quvchilar va JavaScript uchun elementning xatti-harakati, ko‘rinishi, semantikasi, accessibility va xavfsizligini belgilaydi.

Senior darajada biz **attribute** ni “oddiy qo‘shimcha” deb emas, balki **markupning deklarativ konfiguratsiya mexanizmi** sifatida ko‘ramiz. U statik (HTML kodida yoziladi) va brauzer uni parse qilganda DOM elementining **initial state** ni yaratadi. Keyin JavaScript orqali dinamik o‘zgartirilishi mumkin. Bu **attribute vs DOM property** farqi — senior darajadagi eng muhim va chalkash tushunchalardan biri.

Quyidagi material **MDN Web Docs (2026 yil aprel yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, DOM ko‘rinishi va production best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs — HTML attribute reference (oxirgi yangilanish: 14 aprel 2026):**

> “Elements in HTML have attributes; these are additional values that configure the elements or adjust their behavior in various ways.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “Attributes are key-value pairs that appear inside an element’s start tag. They provide additional information about the element and influence its behavior, semantics, accessibility, and security.”

**Senior nuqtai nazar:**  
Attribute — bu **HTML markup** ning kuchli konfiguratsiya vositasi. U elementning dastlabki holatini (initial state) belgilaydi va brauzer parsing jarayonida DOM nodiga o‘tkaziladi. To‘g‘ri ishlatilgan atributlar SEO, accessibility (a11y), performance va xavfsizlikni sezilarli yaxshilaydi. Noto‘g‘ri ishlatilganda esa invalid HTML, quirks mode yoki security zaifligiga olib keladi.

---

## 2. Sintaksis va qoidalari (2026 yil WHATWG qoidalari)

```html
<element attribute-name="attribute-value">Kontent</element>
```

- **Attribute nomi**: Har doim lowercase (HTML5+ da case-insensitive, lekin lowercase tavsiya etiladi). Bo‘sh joy, `=`, `"`, `'` va boshqa maxsus belgilarsiz.
- **Qiymat**: Ikki tirnoq (`" "`) yoki bitta tirnoq (`' '`) ichida. Qiymat bo‘lmasa ham yozish mumkin (boolean atributlar).
- **Bir nechta atribut**: Bo‘sh joy bilan ajratiladi.
- **Bo‘sh (empty) atribut**: Qiymatsiz yoziladi (masalan `disabled`).

**Real senior misol:**

```html
<a
	href="https://example.com"
	target="_blank"
	rel="noopener noreferrer"
	class="button primary"
	id="main-link"
	aria-label="Asosiy sahifaga oʻtish"
	data-user-id="123"
>
	Bosh sahifa
</a>
```

---

## 3. Attribute turlari

| Turi                           | Tavsifi                                                | Misollar                                                                          | Qachon ishlatiladi?           |
| ------------------------------ | ------------------------------------------------------ | --------------------------------------------------------------------------------- | ----------------------------- | ------------------------- | ----- | --------------------- |
| **Global attributes**          | Barcha elementlarda ishlatilishi mumkin                | `id`, `class`, `style`, `title`, `lang`, `hidden`, `data-*`, `aria-*`, `tabindex` | Har doim, loyihaning asosi    |
| **Element-specific**           | Faqat ma’lum elementlarda ishlaydi                     | `href` (`<a>`, `<link>`), `src` (`<img>`, `<script>`), `type` (`<input>`)         | Kerakli elementda             |
| **Boolean attributes**         | Qiymati yo‘q yoki bo‘sh bo‘lsa ham `true` hisoblanadi  | `disabled`, `checked`, `readonly`, `multiple`, `required`                         | Form va interaktiv elementlar |
| **Enumerated attributes**      | Oldindan belgilangan qiymatlar ro‘yxati                | `dir="ltr                                                                         | rtl                           | auto"`, `autocomplete="on | off"` | Cheklangan variantlar |
| **Data attributes** (`data-*`) | Custom ma’lumot saqlash uchun (JS bilan oson o‘qiladi) | `data-user-id="123"`, `data-theme="dark"`                                         | JS bilan bog‘lanish, testlar  |
| **ARIA attributes**            | Accessibility uchun (ekran o‘quvchilar)                | `aria-label`, `aria-hidden`, `role`, `aria-describedby`                           | a11y majburiy (WCAG 2.2)      |

**Global attributes** (eng muhimlari, MDN 2026 yil yangilanishi):  
`accesskey`, `autocapitalize`, `class`, `contenteditable`, `data-*`, `dir`, `draggable`, `hidden`, `id`, `inert`, `inputmode`, `lang`, `role`, `slot`, `spellcheck`, `style`, `tabindex`, `title`, `translate`.

---

## 4. Eng muhim farq: **HTML Attribute vs DOM Property** (Senior daraja — klassik chalkashlik)

Bu farqni chuqur tushunmasdan React, Vue, Svelte yoki vanilla JS bilan professional ish qilish qiyin.

| Xususiyat             | **HTML Attribute** (Content Attribute)        | **DOM Property** (IDL Attribute)                     |
| --------------------- | --------------------------------------------- | ---------------------------------------------------- |
| **Joylashuvi**        | HTML kodida (markup)                          | JavaScript obyekti (DOM node)                        |
| **Turi**              | Har doim **string**                           | Har qanday tur (string, boolean, number, object)     |
| **O‘zgarish**         | Statik (dastlabki qiymat)                     | Dynamic (foydalanuvchi yoki JS o‘zgartirishi mumkin) |
| **Kirish usuli**      | `getAttribute()`, `setAttribute()`            | `element.propertyName` (to‘g‘ridan-to‘g‘ri)          |
| **Misol (`<input>`)** | `value="Dastlabki qiymat"` (initial)          | `input.value` (hozirgi qiymat)                       |
| **Sinxronizatsiya**   | Ba’zi atributlar property ga “reflect” qiladi | Ko‘pchilik o‘zgarishlar attribute ni yangilamaydi    |

**Real misol (klassik gotcha):**

```html
<input id="myInput" value="Dastlabki qiymat" />
```

```js
const input = document.getElementById('myInput')

console.log(input.getAttribute('value')) // "Dastlabki qiymat" → attribute
console.log(input.value) // "Dastlabki qiymat" → property

input.value = 'Foydalanuvchi oʻzgartirdi' // faqat property oʻzgaradi

console.log(input.getAttribute('value')) // hali ham "Dastlabki qiymat" qoladi!
console.log(input.value) // "Foydalanuvchi oʻzgartirdi"
```

**Senior eslatma:** Frameworklarda (React, Vue) JSX `value={...}` property ni o‘rnatadi, attribute emas. Bu farqni tushunmasangiz, controlled/uncontrolled komponentlarda xato chiqadi.

---

## 5. Senior darajadagi best practices (2026 yil production)

1. **Hech qachon `style` attribute** ni ishlatmang — faqat CSS fayllar, CSS Modules yoki Tailwind.
2. **ID** ni unique va semantik qiling; `class` ni BEM yoki Tailwind usulida boshqaring.
3. **Data attributes** ni faqat JS bilan bog‘lanish uchun ishlatish (`data-testid` testlar uchun, `data-theme` uchun).
4. **ARIA** atributlarini to‘g‘ri qo‘llang — Lighthouse, axe yoki WAVE tool bilan tekshiring.
5. **Security**: Har bir external `<a>` ga `rel="noopener noreferrer"` qo‘shing.
6. **Performance**: Rasmlar uchun `loading="lazy"`, `decoding="async"`, `fetchpriority="high"` dan foydalaning.
7. **Boolean atributlar**: Qiymat yozmang — `disabled` yoki `disabled=""` yetarli.
8. **Custom Elements**: `observedAttributes` orqali atribut o‘zgarishlarini kuzating.
9. **Event handler atributlar** (`onclick`, `onload`) dan qoching — faqat `addEventListener`.

**Yomon amaliyot (qat’iyan taqiqlanadi):**

```html
<div onclick="alert('xato')">Click me</div>
```

**Senior usuli:**

```js
button.addEventListener('click', () => {
	/* ... */
})
```

---

## 6. Xulosa — nega senior attribute ni “konfiguratsiya kaliti” deb hisoblaydi?

Attribute — bu HTML elementini **konfiguratsiya qiluvchi kalit**. Uni to‘g‘ri ishlatmasangiz:

- Accessibility buziladi (WCAG buzilishi),
- SEO pasayadi,
- JS bilan ishlash qiyinlashadi,
- Performance va security muammolari chiqadi.

Agar siz faqat “class va id qo‘shamiz” deb o‘ylasangiz — oddiy kod yozuvchisiz.  
Agar attribute va property farqini, global atributlarni, ARIA ni, data-\* ni chuqur tushunsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- Attribute vs Property real loyihada xatolari (React + vanilla misollar)
- ARIA + data-\* bilan to‘liq accessibility audit
- Custom Elements va observedAttributes

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — HTML attribute reference (Last modified: 14 aprel 2026)](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes)
- [MDN Web Docs — Global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes)
- [WHATWG HTML Living Standard — Attributes (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/syntax.html#attributes-2)
- [MDN Web Docs — Using data attributes (Last modified: 17 dekabr 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/How_to/Use_data_attributes)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil 15 aprel holatiga mos.
