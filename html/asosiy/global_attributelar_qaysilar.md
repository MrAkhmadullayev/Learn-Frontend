# HTML Global Attributes (Global Atributlar) — To‘liq Senior Front-end Developer Qo‘llanmasi

**Global attributes** — bu **barcha HTML elementlarida** (hatto custom va non-standard elementlarda ham) ishlatilishi mumkin bo‘lgan atributlar. Ular elementning xatti-harakatini, ko‘rinishini, accessibility’ni, xavfsizligini, performance’ni va JavaScript bilan bog‘lanishini boshqaradi.

Senior darajada biz global atributlarni “oddiy qo‘shimcha” deb emas, balki **HTML markup’ning deklarativ konfiguratsiya tizimi** sifatida ko‘ramiz. Ular sizga kodni takrorlanmasdan, semantik, maintainable va future-proof qilish imkonini beradi. To‘g‘ri ishlatilganda ular **DOM parsing**, **Accessibility Tree**, **Critical Rendering Path**, **SEO**, **security** va **Web Components** arxitekturasiga katta ta’sir qiladi.

Quyidagi material **MDN Web Docs (15 dekabr 2025 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir atribut chuqur tahlil qilingan, real misollar va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (15 dekabr 2025):**

> “Global attributes are attributes common to all HTML elements; they can be used on all elements, though they may have no effect on some elements.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The following attributes may be specified on any HTML element (unless explicitly forbidden by the element’s definition). They are collectively known as the global attributes.”

**Senior nuqtai nazar:**  
Global atributlar — bu HTML’ning **universal konfiguratsiya mexanizmi**. Ular brauzer parsing vaqtida elementning dastlabki holatini (initial state) yaratadi va DOM nodiga “reflect” qilinadi. Senior loyihalarda ularni **performance**, **a11y**, **SEO**, **CSP security** va **Shadow DOM** bilan bog‘liq holda chuqur tahlil qilamiz. Noto‘g‘ri ishlatish invalid HTML, Lighthouse xatolari yoki accessibility buzilishiga olib keladi.

---

## 2. To‘liq ro‘yxat (2025–2026 yil holati — MDN + WHATWG)

### A. Asosiy (Core) Global Attributes

| Atribut                 | Tavsifi (nima qiladi?)                                                        | Senior darajadagi muhim eslatmalar (2026)                                |
| ----------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| `accesskey`             | Klaviatura shortcut (Alt + harf)                                              | Brauzer birinchi mos kelganini ishlatadi; a11y uchun ehtiyotkorlik bilan |
| `anchor`                | Anchor positioning (CSS Anchor API)                                           | **Yangi 2025** — positioned elementlarni anchor bilan bog‘lash           |
| `autocapitalize`        | Avtomatik katta harf qilish (`sentences`, `words`, `characters`, `none`)      | Mobil klaviaturalar uchun juda foydali                                   |
| `autocorrect`           | Avtomatik imlo tuzatish                                                       | Password, email inputlarda `off` qilish tavsiya etiladi                  |
| `autofocus`             | Sahifa yuklanganda avtomatik focus                                            | Boolean; dialog ochilganda ham ishlaydi; performance ehtiyotkorlik       |
| `class`                 | CSS klasslari (space bilan ajratilgan)                                        | BEM, Tailwind, CSS Modules bilan ishlatish — asosiy                      |
| `contenteditable`       | Elementni foydalanuvchi tahrirlay oladi (`true` / `false` / `plaintext-only`) | Rich text editor uchun; security va performance xavfi yuqori             |
| `data-*`                | Custom ma’lumot saqlash (`data-user-id="123"`)                                | `dataset` API orqali JS’da oson o‘qiladi; testlar va state uchun ideal   |
| `dir`                   | Matn yo‘nalishi (`ltr`, `rtl`, `auto`)                                        | RTL tillar uchun majburiy; a11y va SEO uchun                             |
| `draggable`             | Drag & Drop imkoniyatini yoqadi (`true` / `false`)                            | Drag and Drop API bilan birga                                            |
| `enterkeyhint`          | Virtual klaviaturada “Enter” tugmasi matnini belgilaydi                       | Mobil UX ni sezilarli yaxshilaydi                                        |
| `exportparts`           | Shadow DOM qismini ochiq qilish (`::part()`)                                  | **Yangi** — nested Web Components styling uchun                          |
| `hidden`                | Elementni render qilmaslik                                                    | Accessibility uchun to‘g‘ri ishlatish kerak (display:none emas)          |
| `id`                    | Unikal identifikator                                                          | Har doim unique bo‘lishi shart! Fragment linklar uchun                   |
| `inert`                 | Elementni butunlay “o‘chirish” (klik, focus, hover ishlamaydi)                | **Kuchli yangilik** — modal, loading state uchun ideal                   |
| `inputmode`             | Virtual klaviatura turini belgilaydi (`numeric`, `email`, `tel` va h.k.)      | Mobil inputlar uchun juda muhim                                          |
| `is`                    | Oddiy elementni custom element kabi ishlatish                                 | Web Components uchun                                                     |
| `lang`                  | Element tili (`uz`, `en`, `ru`)                                               | Accessibility va SEO uchun majburiy                                      |
| `nonce`                 | CSP (Content Security Policy) uchun kriptografik nonce                        | Inline script/style xavfsizligi uchun muhim                              |
| `part`                  | Shadow DOM qismini ochiq qilish (`::part()`)                                  | Web Components styling uchun asosiy                                      |
| `popover`               | Elementni popover (overlay) qilish                                            | **2024–2026 yangilik** — Popover API (JS siz dialog va tooltip)          |
| `slot`                  | Shadow DOM slotiga bog‘lash                                                   | Web Components kompozitsiyasi uchun                                      |
| `spellcheck`            | Imlo tekshirishni yoqish/o‘chirish                                            | Browser-dependent                                                        |
| `style`                 | Inline CSS                                                                    | Production’da tavsiya etilmaydi (CSS Custom Properties afzal)            |
| `tabindex`              | Focus tartibi (`-1`, `0`, `>0`)                                               | Accessibility uchun juda muhim; minimal ishlatish                        |
| `title`                 | Tooltip matni                                                                 | Faqat maslahat; a11y uchun asosiy emas (aria-label afzal)                |
| `translate`             | Tarjima qilinishini boshqarish (`yes` / `no`)                                 | Lokalizatsiya loyihalarida                                               |
| `virtualkeyboardpolicy` | Virtual klaviatura ko‘rinishini boshqarish (`auto` / `manual`)                | **Yangi** — touch qurilmalar uchun                                       |
| `writingsuggestions`    | Brauzer yozuv takliflarini (AI/grammar) yoqish/o‘chirish                      | **Yangi 2025–2026** — AI-assisted inputlar uchun                         |

### B. Microdata atributlari (Schema.org uchun)

- `itemscope`, `itemtype`, `itemprop`, `itemref`, `itemid`

### C. Global Event Handler atributlari (`on*` — 50+ ta)

`onclick`, `onload`, `onkeydown`, `onfocus` va h.k.

**Senior maslahat:** Production’da hech qachon ishlatmang! `addEventListener()` dan foydalaning (inline event handlerlar — eski, xavfli va maintainability ni buzadi).

---

## 3. Eng muhim yangiliklar (2025–2026)

- `popover` — Popover API’ning deklarativ varianti (JS siz tooltip, menu, dialog).
- `inert` — Butun bo‘limni interaktivlikdan chiqarish (modal, loading state uchun ideal).
- `virtualkeyboardpolicy` va `writingsuggestions` — Mobil va AI-assisted inputlar uchun.
- `exportparts` va `anchor` — Shadow DOM va CSS Anchor Positioning’ni kuchaytirdi.
- `part` — Web Components styling’ni yanada moslashuvchan qildi.

---

## 4. Senior darajadagi best practices (2026 yil)

1. **Accessibility birinchi** — `lang`, `tabindex`, `inert`, `aria-*` (ARIA global emas, lekin ko‘pincha birga ishlatiladi) ni to‘g‘ri qo‘llang.
2. **Data attributes** — faqat JS bilan bog‘lanish uchun (`data-testid` testlar uchun, `data-theme` uchun).
3. **Hech qachon** `style` atributini production’da ishlatmang — CSS Custom Properties + external CSS yoki Tailwind.
4. **Security** — Har bir external `<a>` ga `rel="noopener noreferrer"` + `nonce` (CSP).
5. **Performance** — `hidden` va `inert` ni to‘g‘ri ishlatib, keraksiz renderlarni oldini oling.
6. **Lighthouse / axe / WAVE** bilan tekshiring — global atributlar ko‘p auditlarda chiqadi.
7. **Web Components** — `is`, `part`, `slot`, `exportparts` ni chuqur biling.
8. **Boolean atributlar** — qiymat yozmang (`disabled` yoki `disabled=""` yetarli).

---

## 5. Xulosa (Senior nuqtai nazar)

Global atributlar — HTML’ning “konfiguratsiya kaliti”. Ular sizga kodni qisqa, kuchli, semantik va kelajakka mos qilish imkonini beradi.

Agar siz faqat `class` va `id` ni bilsangiz — oddiy developer.  
Agar `inert`, `popover`, `nonce`, `data-*`, `tabindex`, `part` va `virtualkeyboardpolicy` ni chuqur tushunsangiz va ularni arxitekturada to‘g‘ri qo‘llay olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- `inert` + `popover` bilan real modal misollari
- `data-*` va `dataset` API bilan state management
- ARIA + global atributlar bilan to‘liq accessibility audit

Savolingiz bo‘lsa yoki real loyiha misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — Global attributes (Last modified: 15 dekabr 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes)
- [WHATWG HTML Living Standard — Global attributes (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/global-attributes.html)
- [MDN Web Docs — HTML attribute reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
