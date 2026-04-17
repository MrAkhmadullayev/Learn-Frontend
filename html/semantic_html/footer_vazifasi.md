# `<footer>` Tegi Nima Uchun Ishlatiladi? — To‘liq Senior Front-end Developer Qo‘llanmasi (2026 yil aprel holati)

**`<footer>`** elementi HTML ning **semantic landmark** elementlaridan biri bo‘lib, o‘zining **eng yaqin ancestor sectioning content** yoki **sectioning root** (`<body>`) elementi uchun **pastki qism (footer)** ni ifodalaydi. U odatda muallif haqidagi ma’lumot, copyright, tegishli hujjatlar havolalari, kontakt ma’lumotlari, social linklar va shunga o‘xshash “yakuniy” kontentni o‘z ichiga oladi.

Senior darajada `<footer>` — bu shunchaki “pastki panel” emas. Bu **semantic landmark** va sahifangizning yakuniy strukturasini brauzer, qidiruv tizimlari, ekran o‘quvchilar, AI summarizerlar va voice assistants uchun aniq bildiruvchi kalit element. Uni to‘g‘ri ishlatish orqali accessibility (WCAG 2.2/3.0), SEO, maintainability va future-proof kodni bir vaqtda hal qilasiz.

Quyidagi material **MDN Web Docs (6 avgust 2025 yangilanishi)** va **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism chuqur tahlil qilingan, real kod misollari, implicit ARIA rollari, nesting qoidalari va senior best practices bilan boyitilgan.

---

## 1. Rasmiy ta’rif va maqsadi

**MDN Web Docs (6 avgust 2025):**

> “The `<footer>` HTML element represents a footer for its nearest sectioning content or sectioning root element. A footer typically contains information about its section such as who wrote it, links to related documents, copyright data, and the like.”

**WHATWG HTML Living Standard (15 aprel 2026):**

> “The footer element represents a footer for its nearest ancestor sectioning content or sectioning root element. It is not a sectioning content element itself and does not create a new section in the document outline.”

**Senior nuqtai nazar:**  
`<footer>` — sahifangizning **“oxirgi nuqtasi”**. U asosiy kontentning yakuni sifatida semantik jihatdan belgilaydi va brauzerning default xatti-harakatini, landmark rolini va outline algoritmini avtomatik ravishda faollashtiradi. Bu element sizning HTML arxitekturangizning yakuniy qismi bo‘lib, accessibility, SEO va maintainability ni sezilarli darajada oshiradi.

---

## 2. `<footer>` ning asosiy vazifalari (Senior darajadagi to‘liq ro‘yxat)

| Vazifa                        | Kim foydalanadi?                      | Senior darajadagi ta’siri (2026 yil)                   |
| ----------------------------- | ------------------------------------- | ------------------------------------------------------ |
| Global sahifa footeri         | Foydalanuvchi, brauzer, qidiruvchilar | Copyright, privacy, sitemap, social linklar            |
| Bo‘lim yoki article footeri   | Ekran o‘quvchilar, SEO                | Har bir `<article>` yoki `<section>` ning yakuni       |
| Accessibility landmark        | NVDA, VoiceOver                       | Implicit `role="contentinfo"` (top-level footer uchun) |
| SEO va struktura              | Google, Bing, AI Overviews            | Sahifaning yakuniy ma’lumotlarini aniq ko‘rsatadi      |
| Author / kontakt ma’lumotlari | `<address>` bilan birgalikda          | Mualliflik huquqi semantikasi                          |

---

## 3. Qachon va qanday ishlatiladi? (Real senior misollar)

**1. Global sahifa footeri (eng klassik holat):**

```html
<footer class="site-footer" role="contentinfo">
	<div class="container">
		<p>&copy; 2026 DevUz. Barcha huquqlar himoyalangan.</p>

		<nav aria-label="Footer navigatsiyasi">
			<ul>
				<li><a href="/privacy">Maxfiylik siyosati</a></li>
				<li><a href="/terms">Foydalanish shartlari</a></li>
				<li><a href="/about">Biz haqimizda</a></li>
			</ul>
		</nav>

		<address>
			<a href="mailto:info@devuz.uz">info@devuz.uz</a> •
			<a href="tel:+998901234567">+998 90 123 45 67</a>
		</address>
	</div>
</footer>
```

**2. Article yoki section ichidagi lokal footer:**

```html
<article>
  <header><h1>Maqola sarlavhasi</h1></header>
  <!-- asosiy kontent -->

  <footer>
    <p>Maqola muallifi:
      <address>
        <a href="/author/senior-dev">Senior Frontend Developer</a>
      </address>
    </p>
    <p>Yaratilgan sana:
      <time datetime="2026-04-17">17 aprel 2026</time>
    </p>
    <div class="share-buttons">
      <!-- share linklari -->
    </div>
  </footer>
</article>
```

**Muhim qoida (MDN + WHATWG 2026):**

- Agar `<footer>` `<body>` ning to‘g‘ridan-to‘g‘ri farzandi bo‘lsa → implicit `role="contentinfo"` (global footer landmark).
- Agar u `<article>`, `<section>`, `<aside>` yoki boshqa sectioning element ichida bo‘lsa → `role="generic"` bo‘ladi (oddiy footer, landmark emas).
- Bir sahifada bir nechta `<footer>` bo‘lishi mumkin va tavsiya etiladi (global + article footerlari).

---

## 4. Muhim qoidalar (senior daraja bilishi shart)

- **Nesting taqiqlari:** `<footer>` ichida boshqa `<footer>` yoki `<header>` qo‘yish mumkin emas (invalid).
- `<footer>` **sectioning content** emas → yangi heading hierarchy yaratmaydi va document outline’da yangi section hosil qilmaydi.
- Ichiga faqat **flow content** (p, nav, address, ul, ol, div va h.k.) qo‘yiladi.
- Kontakt ma’lumotlari uchun ichida `<address>` ishlatish majburiy tavsiya etiladi (semantik jihatdan to‘g‘ri).
- `<footer>` ni `<main>` ichida yoki tashqarisida ishlatish mumkin, lekin ko‘pincha sahifaning oxirida joylashadi.

---

## 5. Accessibility va SEO ta’siri (2026 yil)

- **Implicit ARIA role:** `contentinfo` (top-level) yoki `generic`.
- Ekran o‘quvchilar “content information” yoki “footer” deb o‘qiydi.
- Google `<footer>` ni sahifaning yakuniy ma’lumotlari sifatida tushunadi → SEO ni yaxshilaydi (mualliflik, kontakt va copyright ma’lumotlari).
- Lighthouse auditida “Footer landmark” va “Landmark elements are unique” tekshiriladi.

---

## 6. Senior Best Practices (2026 yil production darajasi)

1. Har bir loyihada **global `<footer>`** ni alohida reusable komponent sifatida yarating (Next.js, Astro, Vue).
2. Har bir `<article>` ga o‘zining kichik `<footer>` ni qo‘shing (muallif, sana, share buttonlar).
3. Hech qachon stil uchun `<div class="footer">` ishlatmang — semanticdan foydalaning.
4. `aria-label` yoki `aria-labelledby` ni faqat kerak bo‘lganda qo‘shing.
5. Mobil uchun sticky footer yoki responsive dizaynni CSS Grid/Flex bilan boshqaring.
6. Lighthouse + axe + WAVE bilan har doim tekshiring.
7. **Anti-pattern:** `<footer>` ni faqat dekorativ maqsadda ishlatish yoki ichiga asosiy kontent qo‘yish.

**Yomon amaliyot:**

```html
<div class="footer">...</div>
```

**Senior usuli:**

```html
<footer class="site-footer" role="contentinfo">...</footer>
```

---

## 7. Xulosa (Senior nuqtai nazar)

`<footer>` — bu shunchaki “pastki chiziq” emas. Bu **semantic landmark** va sahifangizning yakuniy strukturasini brauzer, qidiruv tizimlari va ekran o‘quvchilarga aniq bildiruvchi kalit element. Uni to‘g‘ri ishlatish orqali siz:

- Accessibility ni WCAG 2.2/3.0 darajasiga ko‘tarasiz,
- SEO ni yaxshilaysiz,
- Kodni o‘qilishi va maintain qilishni osonlashtirasiz,
- Kelajakdagi texnologiyalarga (AI summarizerlar, voice assistants) tayyor bo‘lasiz.

Agar siz faqat `class="footer"` bilan ishlasangiz — oddiy kod yozuvchisiz.  
Agar `<footer>` ni `role`, nesting, `<address>` va landmarklar bilan chuqur boshqara olsangiz — bu **haqiqiy senior** daraja.

Agar xohlasangiz, keyingi bosqichda quyidagilarni chuqurroq ko‘rib chiqamiz:

- To‘liq semantic sahifa struktura misoli (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`)
- `<footer>` + ARIA + landmark audit
- Real loyihada global + article footer misollari

Savolingiz bo‘lsa yoki real kod misolini xohlasangiz — darhol yozing!

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — The Footer element (Last modified: 6 avgust 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer)
- [WHATWG HTML Living Standard — The footer element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/sections.html#the-footer-element)
- [MDN Web Docs — Semantics in HTML](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- [W3C ARIA in HTML — Implicit roles](https://www.w3.org/TR/html-aria/)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
