# **`<pre>` Tegi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)**

**`<pre>`** (Preformatted Text) elementi HTML ning maxsus block-level elementi bo‘lib, matnni **to‘g‘ridan-to‘g‘ri formatlangan** (preformatted) holda ko‘rsatadi. U matndagi barcha whitespace (bo‘sh joylar, tablar, yangi qatorlar, indentatsiyalar va bo‘sh satrlar) ni saqlab qoladi va monospace shriftda (odatda Courier yoki shunga o‘xshash) chiqaradi.

Senior darajada `<pre>` — bu shunchaki “kod ko‘rsatish” uchun emas. Bu matnning **asl formatini** (strukturasini va o‘qilishini) saqlash kerak bo‘lgan joylarda ishlatiladigan kuchli vosita. Noto‘g‘ri ishlatilsa, accessibility (a11y), SEO, performance va kod maintainability buzilishi mumkin.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, nesting qoidalari, CSS optimizatsiyasi va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (2025 yil yangilanishi):**

> “The `<pre>` HTML element represents preformatted text which is to be presented exactly as written in the HTML file. The text is typically rendered using a non-proportional (monospace) font.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The pre element represents a block of preformatted text, in which structure is represented by typographic conventions rather than by elements.”

**Senior nuqtai nazar:**  
`<pre>` brauzerga “bu matnni asl formatida, hech narsani o‘zgartirmasdan ko‘rsat” degan aniq ko‘rsatma beradi. U `white-space: pre` xususiyatiga ega va whitespace ni saqlaydi. Bu element faqat kerakli joyda ishlatilishi kerak, aks holda oddiy `<p>` yoki `<div>` yetarli bo‘ladi.

---

## 2. Asosiy xususiyatlari (jadval)

| Xususiyat                       | Tavsifi                                                           | Default qiymati / xatti-harakati   |
| ------------------------------- | ----------------------------------------------------------------- | ---------------------------------- |
| **Display turi**                | Block-level                                                       | `display: block`                   |
| **Whitespace**                  | Barcha bo‘sh joy, tab, yangi qator va indentatsiyalarni saqlaydi  | `white-space: pre`                 |
| **Shrift**                      | Monospace (bir xil kenglikdagi harflar)                           | `font-family: monospace`           |
| **Semantik ma’no**              | Yo‘q (presentational element)                                     | —                                  |
| **Implicit ARIA role**          | Yo‘q                                                              | —                                  |
| **Ichiga nima qo‘yish mumkin?** | Inline elementlar (`<code>`, `<span>`, `<a>`, `<strong>` va h.k.) | Block elementlar tavsiya etilmaydi |
| **Scroll xatti-harakati**       | Uzun matn uchun gorizontal scroll avtomatik paydo bo‘ladi         | `overflow-x: auto` (CSS bilan)     |

---

## 3. Qachon va qanday ishlatiladi? (Real holatlar)

Eng ko‘p ishlatiladigan joylar:

- Kod bloklari (eng mashhur)
- She‘r yoki matnning formatini saqlash kerak bo‘lgan joylar
- ASCII art
- Terminal/log chiqishlari
- Config fayllar (JSON, YAML, .env va h.k.)
- Matematik formulalar yoki jadval ko‘rinishidagi matn

**To‘g‘ri ishlatish (Senior usuli — eng yaxshi amaliyot):**

```html
<!-- Eng yaxshi amaliyot: <pre> + <code> (syntax highlighting uchun tayyor) -->
<pre><code>function salom() {
    console.log("Salom, dunyo!");
    return "Hello, World!";
}</code></pre>

<!-- She'r yoki format saqlash uchun -->
<pre>
Bir kun kelar,
  Seni eslayman...
    Yuragimda.
</pre>
```

**Noto‘g‘ri ishlatish (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<pre>
    <h2>Bu xato!</h2> <!-- block element qo‘yish mumkin emas -->
</pre>

<pre>Bu oddiy matn uchun ishlatish yomon amaliyot</pre>
<!-- <p> yetarli edi -->
```

**Muhim qoida (WHATWG + MDN):**

- `<pre>` ichiga **faqat phrasing content** (inline elementlar) qo‘yiladi. Block elementlar (`<h2>`, `<p>`, `<div>` va h.k.) invalid HTML hosil qiladi.
- Eng yaxshi amaliyot: `<pre><code>...</code></pre>` kombinatsiyasi (syntax highlighting uchun Prism, Highlight.js yoki shunga o‘xshash kutubxonalar bilan).

---

## 4. Senior Best Practices (2026 yil production darajasi)

1. **Kod uchun** har doim `<pre><code>...</code></pre>` kombinatsiyasidan foydalaning.
2. Stilni CSS orqali to‘liq boshqaring:
   ```css
   pre {
   	background: #f4f4f4;
   	padding: 1.5rem;
   	border-radius: 8px;
   	overflow-x: auto;
   	tab-size: 4; /* tab kengligini boshqarish */
   	line-height: 1.5;
   	font-size: 0.95rem;
   }
   ```
3. Accessibility uchun: katta `<pre>` bloklariga `aria-label` yoki `role="region"` qo‘shing va `tabindex="0"` bilan keyboard scrollni yaxshilang.
4. **Performance**: Juda uzun kod bloklarini lazy-load qiling yoki collapsible qiling (details/summary bilan).
5. Hech qachon layout yaratish uchun `<pre>` ishlatmang — bu eski usul.
6. Modern loyihalarda (Tailwind, Astro, Next.js) `<Pre>` komponentini reusable qilib yarating va syntax highlighting kutubxonasini qo‘shing.
7. **Anti-pattern:** Stil uchun `<pre>` ni ishlatish yoki `<br>` bilan paragrafni buzish.

---

## 5. Accessibility va SEO ta’siri (2026 yil)

- **Accessibility:** Ekran o‘quvchilar whitespace ni saqlaydi va matnni to‘g‘ri o‘qiydi. Lekin juda uzun bloklar o‘qishni qiyinlashtirishi mumkin — shuning uchun scroll va aria-label tavsiya etiladi.
- **SEO:** Zaif. Google `<pre>` ni oddiy matn sifatida qabul qiladi, lekin ichidagi `<code>` semantikasi yordam beradi.
- **WCAG:** 1.3.1 (Info and Relationships) va 1.4.8 (Visual Presentation) talablarini bajarishga yordam beradi.
- **Reader Mode:** Safari va Firefox Reader View `<pre>` ni formatni saqlagan holda toza ko‘rsatadi.

---

## 6. Xulosa (Senior nuqtai nazar)

`<pre>` — matnning **asl formatini** saqlash uchun maxsus element. U faqat kerakli joyda (kod, she‘r, ASCII art, config fayllari va h.k.) ishlatilishi kerak. Aks holda, oddiy `<p>` yoki `<div>` yetarli bo‘ladi.

Agar siz faqat kod ko‘rsatish uchun `<pre>` ishlatayotgan bo‘lsangiz — yaxshi.  
Agar uni to‘g‘ri semantika, accessibility, CSS optimizatsiyasi va reusable komponent sifatida birlashtirayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq kod blok komponenti (Prism + Tailwind misoli)
- `<pre>` va `<code>` birgalikda accessibility optimizatsiyasi
- Real loyihada `<pre>` audit misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Pre element (2025 yil yangilanishi)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre)
- [WHATWG HTML Living Standard — The pre element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/grouping-content.html#the-pre-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
