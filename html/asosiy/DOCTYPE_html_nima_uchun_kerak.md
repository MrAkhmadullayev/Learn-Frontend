# `<!DOCTYPE html>` Nima Uchun Kerak? — To‘liq Senior Front-end Developer Qo‘llanmasi

**`<!DOCTYPE html>`** — HTML dokumentining **birinchi va majburiy satri** (preamble). Bu oddiy ko‘rinadigan bitta qator, lekin u butun sahifaning **qanday render bo‘lishini** belgilaydi. Senior darajada biz uni “majburiy” deb hisoblaymiz, chunki u brauzerning to‘g‘ri ishlashini ta’minlaydi.

Quyidagi material **MDN Web Docs (2025 yil iyul yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real misollar, brauzer ichki mexanizmlari va amaliy maslahatlar bilan boyitilgan.

---

## 1. Qisqacha va aniq javob (Senior darajada yetarli emas)

`<!DOCTYPE html>` brauzerga “Bu HTML5 (yoki undan keyingi **Living Standard**) dokumenti” deb bildiradi.  
**Yagona maqsadi:** Brauzerni **Quirks Mode**dan chiqarib, **No-Quirks Mode** (Standards Mode) ga o‘tkazish.

Agar u bo‘lmasa, brauzer eski (1990-yillar IE5/Netscape davridagi) “quirky” xatti-harakatlar rejimida ishlaydi. Bu sizning CSS layout, box-model, font inheritance va hatto ba’zi JavaScript xususiyatlaringizni buzadi.

**MDN rasmiy ta’rifi (2025 yil iyul):**

> “Its sole purpose is to prevent a browser from switching into so-called ‘quirks mode’ when rendering a document.”

---

## 2. Nima uchun kerak? (Asosiy sabab — Rendering Modes)

Brauzerlar (Chrome, Firefox, Safari, Edge) HTMLni ikki (ba’zan uch) xil **rendering rejimi**da ko‘rsatadi:

| Rejim              | Rasmiy nomi (HTML5+)  | Qachon ishga tushadi?                                | Natija (Senior nuqtai nazar, 2026 yil)                                                         |
| ------------------ | --------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Standards Mode** | **No-Quirks Mode**    | `<!DOCTYPE html>` mavjud bo‘lsa                      | To‘liq W3C/CSS spec bo‘yicha ishlaydi. Predictable, consistent, modern.                        |
| **Quirks Mode**    | Quirks Mode           | DOCTYPE yo‘q yoki noto‘g‘ri bo‘lsa                   | Eski IE5 “bug”lari taqlid qilinadi. CSS box-model, table layout va boshqa ko‘p narsa buziladi. |
| **Limited-Quirks** | Almost Standards Mode | Ba’zi eski DOCTYPE lar (masalan HTML 4 Transitional) | O‘rtacha — faqat ba’zi quirks saqlanadi.                                                       |

**WHATWG HTML Living Standard (15 aprel 2026):**

> “DOCTYPEs are required for legacy reasons. When omitted, browsers tend to use a different rendering mode that is incompatible with some specifications. Including the DOCTYPE in a document ensures that the browser makes a best-effort attempt at following the relevant specifications.”

**MDN (2025 yil iyul):**

> “The recommended DOCTYPE is `<!doctype html>`, which is the simplest possible and activates no-quirks mode in all existing browsers.”

---

## 3. Tarixiy kontekst (nima uchun shunday bo‘ldi?)

- **1990-yillar**: Brauzerlar (Netscape Navigator, Internet Explorer) o‘zlaricha “yaxshiroq” deb hisoblagan qoidalarda ishlagan.
- **2000-yillar boshida**: W3C standartlari paydo bo‘ldi. Brauzerlar eski millionlab sahifalarni buzmaslik uchun **DOCTYPE Switching** mexanizmini o‘ylab topdi.
- **HTML5 (2014)**: Hammasini soddalashtirdi — endi faqat `<!DOCTYPE html>` yetarli. Hech qanday DTD (Document Type Definition) yoki uzun sintaksis kerak emas.

2026 yilda ham bu mexanizm saqlanmoqda, chunki internetdagi eski sahifalarni qo‘llab-quvvatlash kerak.

---

## 4. Agar `<!DOCTYPE html>` bo‘lmasa nima bo‘ladi?

Quirks Mode’da quyidagi muammolar chiqadi (Chrome, Firefox, Safari, Edge’da bir xil):

- **Box Model xatosi**

  ```css
  .box {
  	width: 300px;
  	padding: 20px;
  	border: 10px solid;
  }
  ```

  - **Standards Mode**: umumiy kenglik = 300 + 40 + 20 = 360px
  - **Quirks Mode**: umumiy kenglik = 300px (padding va border ichiga kiradi — IE5 usuli)

- **Font inheritance** — `body { font-size: 16px; }` bo‘lsa ham, `table`, `button`, `input` kabi elementlar o‘ziga xos eski qiymatni oladi.

- **Table layout** — `table { width: 100%; }` noto‘g‘ri hisoblanadi.

- **Vertical alignment va inline-block** xatti-harakati o‘zgaradi.

- **Zamonaviy CSS** (Flexbox, Grid, Container Queries, `:has()`) ba’zan noto‘g‘ri ishlaydi yoki butunlay buziladi.

- **Lighthouse audit** avtomatik ravishda xato ko‘rsatadi:  
  “Page lacks the HTML doctype, thus triggering quirks mode.”

**Natija:** Sahifangiz har xil brauzer va qurilmalarda **har xil** ko‘rinadi. Production loyihada bu — katta xato va mijoz shikoyati.

**Tekshirish usuli (DevTools):**  
`document.compatMode`

- `"CSS1Compat"` → No-Quirks (to‘g‘ri)
- `"BackCompat"` → Quirks (xato)

---

## 5. 2026 yilgi WHATWG rasmiy sintaksisi

```html
<!DOCTYPE html>
```

Yoki legacy (faqat kerak bo‘lganda):

```html
<!DOCTYPE html SYSTEM "about:legacy-compat">
```

- **Case-insensitive** (`<!doctype HTML>` yoki `<!DoCtYpE hTmL>` ham ishlaydi).
- Eng birinchi satrda bo‘lishi kerak (oldinga faqat whitespace yoki comment qo‘yish mumkin).
- Hech qanday qo‘shimcha parametr yoki DTD kerak emas.

---

## 6. Senior darajadagi best practices (loyihada qo‘llash)

1. **Har doim** birinchi satrda yozing — hatto komponentlarda (React SSR, Vue, Astro, Next.js) ham.
2. Hech qachon eski shakldan (`<!DOCTYPE HTML PUBLIC ...>`) foydalanmang — bu limited-quirks trigger qilishi mumkin.
3. Production build’da (Vite, Webpack, Parcel, Next.js) avtomatik qo‘shilishini tekshiring.
4. Har safar **Lighthouse + Web Vitals** bilan tekshiring.
5. Web Components yoki Shadow DOM ishlatganda ham **parent document**da DOCTYPE bo‘lishi shart.
6. Agar legacy support kerak bo‘lsa ham — asosiy sahifada DOCTYPE majburiy.
7. Yangi loyihada birinchi narsa: `<!DOCTYPE html>` + `<html lang="uz" dir="ltr">` + `<meta charset="UTF-8">`.

---

## 7. Xulosa — nega senior buni “majburiy” deb hisoblaydi?

`<!DOCTYPE html>` — bu faqat “bir satr kod” emas.  
Bu — **brauzer rendering engine**ni to‘g‘ri yo‘nalishga o‘tkazuvchi kalit.  
U yo‘q bo‘lsa, sizning butun CSS arxitekturangiz, performance optimizatsiyalaringiz, accessibility testinglaringiz va SEO ishlashingiz befoyda bo‘ladi.

**Senior maslahat:** Har bir yangi loyihada birinchi narsa — `<!DOCTYPE html>` + to‘liq semantic struktura. Bu sizning loyihangizni **future-proof** qiladi va 10 yildan keyin ham muammosiz ishlaydi.

---

## 8. Qo‘shimcha chuqur mavzular (keyingi bosqichlar)

Agar xohlasangiz, quyidagilarni yanada chuqurroq ko‘rib chiqamiz:

- Quirks vs Standards rejimlaridagi 10 ta aniq CSS farqi (kod + screenshot misollari bilan)
- DOCTYPE bo‘lmaganda real loyihada qanday xatolar chiqadi (live test)
- Modern build tool’larda (Vite, Next.js) DOCTYPE qanday boshqariladi
- `document.compatMode` va brauzer console’da quirks mode haqida warning

Savolingiz bo‘lsa yoki misollar bilan test qilmoqchi bo‘lsangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [WHATWG HTML Living Standard — The DOCTYPE (Last Updated 15 April 2026)](https://html.spec.whatwg.org/multipage/syntax.html#the-doctype)
- [MDN Web Docs — Quirks Mode and Standards Mode (Last modified 9 July 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Quirks_mode_and_standards_mode)
- [MDN Web Docs — Doctype Glossary](https://developer.mozilla.org/en-US/docs/Glossary/Doctype)
- [WHATWG Quirks Mode Standard (15 March 2026)](https://quirks.spec.whatwg.org/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy WHATWG va MDN manbalaridan olingan va 2026 yil 15 aprel holatiga mos.
