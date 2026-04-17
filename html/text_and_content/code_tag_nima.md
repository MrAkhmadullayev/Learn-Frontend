# `<code>` Tegi Nima? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<code>`** elementi HTML ning **inline semantik** elementlaridan biri bo‘lib, **kompyuter kodi yoki dasturlash tilidagi qisqa fragmentni** ifodalaydi. U matnni monospace shriftda (bir xil kenglikdagi harflar) va kodga xos uslubda ko‘rsatadi.

Senior darajada `<code>` — bu shunchaki “kod shrifti” emas. Bu **semantik** element bo‘lib, matnning turini (kod ekanligini) brauzer, ekran o‘quvchilar, qidiruv tizimlari va AI summarizerlar uchun aniq bildiradi. Ko‘pincha `<pre>` bilan birgalikda ishlatiladi, lekin o‘zi inline bo‘lgani uchun paragraf ichida ham qo‘llaniladi. Noto‘g‘ri ishlatilsa, accessibility va SEO zaiflashadi.

Quyidagi material **MDN Web Docs (2025 yil yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (2025 yil yangilanishi):**

> “The `<code>` HTML element displays its contents styled in a fashion intended to indicate that the text is a short fragment of computer code.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The code element represents a fragment of computer code.”

**Senior nuqtai nazar:**  
`<code>` — inline semantik element. U brauzerga “bu yerda kompyuter kodi yoki texnik fragment joylashgan” degan aniq signal beradi. U matn oqimi ichida ishlatiladi va ko‘pincha `<pre>` bilan birgalikda kod bloklarini yaratish uchun ishlatiladi.

---

## 2. Asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                                | Nima qiladi?                                           | Senior darajadagi ta’siri (2026 yil)   |
| ------------------------------------- | ------------------------------------------------------ | -------------------------------------- |
| **Kod fragmentini belgilash**         | Matnni kod sifatida ko‘rsatadi                         | Semantik ma’no beradi                  |
| **Monospace shrift**                  | Bir xil kenglikdagi shriftda chiqaradi                 | Kod o‘qilishini osonlashtiradi         |
| **Accessibility**                     | Ekran o‘quvchilar “code” deb o‘qiydi                   | Yaxshi semantika                       |
| **SEO**                               | Google kod fragmentini tushunadi                       | Texnik kontentni yaxshiroq indekslaydi |
| **Inline ishlatish**                  | Matn oqimi ichida ishlatiladi (`<p>` ichida)           | Block element emas                     |
| **Syntax highlighting tayyorgarligi** | `<pre><code>` kombinatsiyasi bilan birgalikda ishlaydi | Highlight.js, Prism va h.k. uchun asos |

---

## 3. Amaliy misollar (To‘g‘ri va noto‘g‘ri ishlatish)

**To‘g‘ri (Senior usuli — eng yaxshi amaliyot):**

```html
<!-- Inline kod (eng ko'p ishlatiladigan) -->
<p>
	HTMLda funksiya yaratish uchun <code>function</code> kalit soʻzidan
	foydalanamiz.
</p>

<!-- Kod ichidagi oʻzgaruvchi -->
<p>Bu yerda <code>userId</code> oʻzgaruvchisi saqlanadi.</p>

<!-- Blok kod bilan birgalikda (eng yaxshi amaliyot) -->
<pre><code>function salom() {
    console.log("Salom, dunyo!");
}</code></pre>
```

**Noto‘g‘ri (Anti-pattern — qat’iyan taqiqlanadi):**

```html
<code>Bu butun paragraf kod emas.</code>
<!-- noto'g'ri, <p> ichida bo'lishi kerak -->
<div class="code">function test()</div>
<!-- semantik yo'qotilgan -->
```

**Muhim qoida:**

- `<code>` inline element bo‘lgani uchun faqat **phrasing content** (matn, `<a>`, `<strong>`, `<em>` va h.k.) bilan birgalikda ishlatiladi.
- Blok kod uchun har doim `<pre><code>...</code></pre>` kombinatsiyasidan foydalaning.

---

## 4. Senior Best Practices (2026 yil production darajasi)

1. **Inline kod** uchun faqat `<code>` ishlatish.
2. **Blok kod** uchun har doim `<pre><code>...</code></pre>` kombinatsiyasidan foydalanish (syntax highlighting uchun Highlight.js, Prism yoki shunga o‘xshash kutubxonalar bilan).
3. Stilni CSS orqali boshqarish:
   ```css
   code {
   	font-family:
   		ui-monospace, SFMono-Regular, 'Menlo', 'Monaco', 'Consolas', monospace;
   	background: #f4f4f4;
   	padding: 2px 6px;
   	border-radius: 4px;
   	font-size: 0.95em;
   	color: #d63384;
   }
   ```
4. Accessibility uchun: katta kod bloklariga `aria-label` yoki `role="code"` qo‘shish mumkin (lekin odatda kerak emas).
5. SEO uchun: texnik maqolalarda `<code>` ni to‘g‘ri ishlatish Googlega yordam beradi.
6. Modern loyihalarda (Tailwind, Astro, Next.js) `<Code>` komponentini reusable qilib yarating.
7. **Hech qachon** oddiy matnni kod qilish uchun `<code>` ishlatmang.

---

## 5. Accessibility va SEO ta’siri (2026 yil)

- **Accessibility:** Ekran o‘quvchilar “code” deb o‘qiydi va monospace shriftni yaxshiroq tushunadi.
- **SEO:** Google `<code>` ni texnik termin yoki kod fragmenti sifatida qabul qiladi va developerlarga yo‘naltirilgan qidiruvlarda yordam beradi.
- **WCAG:** 1.3.1 (Info and Relationships) talablarini bajarishga yordam beradi.
- **Reader Mode:** Safari va Firefox Reader View `<code>` ni toza va mantiqiy ko‘rsatadi.

---

## 6. Xulosa (Senior nuqtai nazar)

`<code>` — **inline semantik kod elementi**. U matn ichidagi kichik kod fragmentlarini aniq belgilaydi va ko‘pincha `<pre>` bilan birgalikda ishlatiladi. Uni to‘g‘ri ishlatish kodni professional, o‘qilishi oson va mashinalar uchun tushunarli qiladi.

Agar siz faqat shrift o‘zgartirish uchun `<code>` ishlatayotgan bo‘lsangiz — oddiy kod yozuvchisiz.  
Agar uni semantika, accessibility va SEO bilan birgalikda to‘g‘ri qo‘llayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq kod blok komponenti (Prism + Tailwind misoli)
- `<code>` va `<pre>` birgalikda accessibility optimizatsiyasi
- Real loyihada `<code>` audit misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Code element (2025 yil yangilanishi)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/code)
- [WHATWG HTML Living Standard — The code element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-code-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
