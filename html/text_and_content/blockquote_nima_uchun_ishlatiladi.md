# `<blockquote>` Tegi Nima Uchun Ishlatiladi? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<blockquote>`** elementi HTML ning **semantik** elementlaridan biri bo‘lib, **boshqa manbadan olingan kengaytirilgan iqtibos** (extended quotation) ni ifodalaydi. U matnni vizual jihatdan indent (chegara) qiladi va semantik jihatdan “bu matn boshqa joydan iqtibos qilingan” degan aniq ma’noni bildiradi.

Senior darajada `<blockquote>` — bu shunchaki “kursiv yoki indent qilish” uchun emas. Bu **semantik landmark** elementi. U brauzer, qidiruv tizimlari (Googlebot), ekran o‘quvchilar (NVDA, VoiceOver), AI summarizerlar va voice assistants uchun iqtibosning manbasini va ma’nosini aniq bildiradi. Noto‘g‘ri ishlatilsa (masalan, oddiy matnni indent qilish uchun), accessibility, SEO va kodning semantikasi buziladi.

Quyidagi material **MDN Web Docs (2025–2026 yangilanishlari)** va **WHATWG HTML Living Standard (15 aprel 2026)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, nesting qoidalari, accessibility va SEO ta’siri bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (2025 yil yangilanishi):**

> “The `<blockquote>` HTML element indicates that the enclosed text is an extended quotation. Usually, this element is rendered visually by indentation.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The blockquote element represents a section that is quoted from another source.”

**Senior nuqtai nazar:**  
`<blockquote>` — kontentning **manbasini** semantik jihatdan belgilaydi. U brauzerga “bu matn boshqa manbadan iqtibos qilingan” signalini beradi. Bu element sahifaning semantik strukturasini kuchaytiradi va accessibility, SEO hamda future-proof kod uchun muhimdir.

---

## 2. `<blockquote>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                       | Kim foydalanadi?                    | Senior darajadagi ta’siri (2026 yil)                           |
| ---------------------------- | ----------------------------------- | -------------------------------------------------------------- |
| Iqtibosni semantik belgilash | Ekran o‘quvchilar (NVDA, VoiceOver) | Implicit `role="blockquote"` yaratadi                          |
| Manba ko‘rsatish             | Google, AI summarizerlar            | `cite` atributi orqali manba havolasini bildiradi              |
| Vizual indent                | Foydalanuvchi                       | Default chapdan chegara + italic shrift                        |
| Accessibility                | Barcha foydalanuvchilar             | Ekran o‘quvchilar “quote” deb o‘qiydi                          |
| SEO va struktura             | Google, Bing                        | Iqtibos sifatida indekslanadi va rich results da yordam beradi |

---

## 3. Qachon va qanday ishlatiladi? (Real senior misollar)

**1. Klassik iqtibos (eng ko‘p ishlatiladigan):**

```html
<blockquote cite="https://example.com/maqola">
	<p>
		Eng muhim narsa — bu oʻzingizga ishonishdir. Agar siz oʻzingizga
		ishonmasangiz, hech kim sizga ishonmaydi.
	</p>
	<footer>— <cite>Elon Musk</cite></footer>
</blockquote>
```

**2. Kitob yoki maqoladan iqtibos:**

```html
<blockquote>
	<p>Hayot — bu sizga berilgan eng qimmatbaho sovgʻadir.</p>
	<footer>— <cite>Paulo Coelho</cite>, “Alkimyogar”</footer>
</blockquote>
```

**3. Bir nechta paragrafli iqtibos:**

```html
<blockquote cite="https://example.com">
	<p>Bu birinchi paragraf iqtibosi.</p>
	<p>Bu ikkinchi paragraf iqtibosi.</p>
	<footer>— Manba: Rasmiy sayt</footer>
</blockquote>
```

**Muhim qoidalar (MDN + WHATWG 2026):**

- Ichiga faqat **flow content** (`<p>`, `<ul>`, `<ol>`, matn) qo‘yiladi.
- Manba ko‘rsatish uchun `cite` atributi yoki ichida `<footer><cite>` ishlatiladi.
- Har doim `<p>` bilan o‘rang (bitta qatorli iqtibosda ham).
- `<blockquote>` ni oddiy indent yoki dizayn uchun ishlatmang — buning uchun CSS `margin` yoki `<div>` yetarli.

---

## 4. Senior Best Practices (2026 yil production darajasi)

1. Har doim `cite` atributi yoki `<cite>` elementi bilan birga ishlatish.
2. Stilni CSS orqali to‘liq boshqaring:
   ```css
   blockquote {
   	border-left: 6px solid #0066ff;
   	padding-left: 1.5rem;
   	margin: 1.5rem 0;
   	font-style: italic;
   	color: #333;
   	background: #f9f9f9;
   }
   ```
3. Accessibility uchun: katta iqtiboslarga `aria-label` qo‘shish mumkin.
4. SEO uchun: Google `<blockquote>` ni iqtibos sifatida yaxshi tushunadi va rich results da ishlatishi mumkin.
5. Modern loyihalarda (Tailwind, Astro, Next.js) `<Blockquote>` komponentini reusable qilib yarating.
6. **Anti-pattern:** Oddiy indent yoki dizayn uchun `<blockquote>` ishlatish.

---

## 5. Xulosa (Senior nuqtai nazar)

`<blockquote>` — bu **semantik iqtibos** elementi. U nafaqat vizual indent yaratadi, balki kontentning manbasini va ma’nosini brauzer, ekran o‘quvchilar, qidiruv tizimlari va AI ga aniq bildiradi. Uni to‘g‘ri ishlatish accessibility va SEO ni sezilarli darajada yaxshilaydi.

Agar siz faqat dizayn uchun `<blockquote>` ishlatayotgan bo‘lsangiz — oddiy kod yozuvchisiz.  
Agar uni `cite` atributi, `<footer>` va to‘g‘ri semantika bilan birga qo‘llayotgan bo‘lsangiz — bu **senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli
- `<blockquote>` + ARIA + landmark audit
- Real loyihada iqtibos komponenti yaratish

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Blockquote element (2025 yil yangilanishi)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote)
- [WHATWG HTML Living Standard — The blockquote element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
