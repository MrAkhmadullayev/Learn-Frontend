# HTML va CSS Farqi Nima? To‘liq Professional Qo‘llanma

**HTML** va **CSS** — zamonaviy veb-ishlab chiqishning ikki asosiy “qavat”i. Ular birgalikda ishlasa-da, vazifalari butunlay farq qiladi. Bu farqni chuqur tushunish **Separation of Concerns** (mas’uliyatlarni ajratish) printsipining asosidir — har qanday katta loyihada, framework (React, Vue, Svelte) yoki dizayn-tizimda muvaffaqiyat kaliti shu.

Quyida senior darajada, amaliy misollar, zamonaviy best practices va ishonchli manbalar bilan to‘liq tahlil berilgan.

---

## 1. Asosiy taʼrif va maqsad

**HTML (HyperText Markup Language)**  
HTML veb-sahifaning **mazmuni (content)** va **strukturasini** belgilaydigan **markup tili**.  
U sahifada qanday elementlar borligini, ularning semantik ma’nosini va ierarxiyasini belgilaydi.

**MDN rasmiy ta’rifi (2025 yil dekabr holati):**

> “HTML (HyperText Markup Language) is the most basic building block of the Web. It defines the meaning and structure of web content.”

HTML faqat **“nima bor?”** (What) degan savolga javob beradi: bu sarlavha, bu paragraf, bu navigatsiya, bu asosiy kontent.

**CSS (Cascading Style Sheets)**  
CSS HTML elementlarining **taqdimoti (presentation)**, dizayni, joylashuvi, rangi, shrifti, animatsiyasi va vizual xatti-harakatlarini boshqaradigan **declarative (qoida asosidagi) til**.

**MDN rasmiy ta’rifi:**

> “Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML or XML.”

CSS faqat **“qanday ko‘rinishi kerak?”** (How) degan savolga javob beradi.

---

## 2. Eng muhim farq — Separation of Concerns (SoC) printsipi

Senior darajada bu printsip — loyiha arxitekturasining asosi:

- **HTML** = **Kontent va semantika** (Content Layer)
- **CSS** = **Dizayn va taqdimot** (Presentation Layer)
- **JavaScript** = **Xatti-harakat va interaktivlik** (Behavior Layer)

**Nima uchun bu ajratish juda muhim?**

- **Maintainability** — dizayn o‘zgarsa, faqat CSS faylni o‘zgartirasiz.
- **Accessibility (a11y)** — ekran o‘quvchilar (NVDA, VoiceOver) faqat HTML strukturasini o‘qiydi.
- **SEO** — Google sahifani HTML semantikasiga qarab indekslaydi.
- **Performance** — CSS alohida fayl sifatida cache qilinadi va parallel yuklanadi.
- **Team work** — dizayner CSS bilan, frontend developer HTML + JS bilan ishlay oladi.
- **Scalability** — katta loyihalarda (design system) kodni qayta ishlatish oson.

Agar HTML ichiga `style=""` yozsangiz yoki `<div>` bilan hamma stilni qo‘ysangiz — bu **anti-pattern** (yomon amaliyot).

---

## 3. Batafsil taqqoslash jadvali (Senior ko‘rinishi, 2026 yil)

| Xususiyat                    | HTML                                      | CSS                                                                     |
| ---------------------------- | ----------------------------------------- | ----------------------------------------------------------------------- |
| **Maqsadi**                  | Struktura + semantika + mazmun            | Taqdimot + dizayn + layout + animatsiya                                 |
| **Turi**                     | Markup language                           | Stylesheet language (rule-based, declarative)                           |
| **Fayl kengaytmasi**         | `.html`                                   | `.css`                                                                  |
| **Sintaksis**                | Teglar (`<h1>`, `<section>`, `<article>`) | Selector + declaration (`h1 { color: red; }`)                           |
| **Brauzer qanday ishlatadi** | DOM Tree yaratadi                         | DOMni stillaydi → Render Tree → Paint                                   |
| **Cascade / Inheritance**    | Yo‘q                                      | Bor (Cascading, Specificity, Inheritance)                               |
| **Zamonaviy imkoniyatlar**   | Semantic teglar, ARIA, Web Components     | Flexbox/Grid, Container Queries, `:has()`, `@layer`, logical properties |
| **Accessibility**            | Asosiy rol (semantic HTML)                | Yordamchi (contrast, focus styles, responsive)                          |
| **O‘zgarish tezligi**        | Kam o‘zgaradi (Living Standard)           | Tez-tez yangilanadi (2026 yilda juda kuchli)                            |

---

## 4. Amaliy misol: Yomon usul vs Senior usuli

**Yomon usul (Junior daraja — inline stil):**

```html
<div
	style="background: #0066ff; color: white; padding: 40px; font-size: 28px; text-align: center; border-radius: 12px;"
>
	<b>Salom, dunyo!</b>
</div>
```

**Senior usuli (To‘g‘ri ajratilgan, zamonaviy):**

```html
<!-- index.html -->
<header class="hero">
	<h1 class="hero__title">Salom, dunyo!</h1>
</header>
```

```css
/* styles.css */
@layer base, components, utilities; /* Cascade Layers — 2026 best practice */

.hero {
	background: var(--primary-blue);
	padding: clamp(2rem, 5vw, 4rem);
	border-radius: 1rem;
	text-align: center;
}

.hero__title {
	color: white;
	font-size: clamp(1.8rem, 4vw, 2.8rem);
	font-weight: 700;
}
```

Bu kodni o‘zgartirish, qayta ishlatish, test qilish va saqlash ancha oson.

---

## 5. Zamonaviy CSS — 2026 yilda senior bilishi shart bo‘lgan narsalar

HTML deyarli o‘zgarmagan (faqat yangi semantic teglar va Web Components qo‘shilmoqda). CSS esa 2022–2026 yillarda katta sakrash qildi:

- **Container Queries** (`@container`) — parent o‘lchamiga qarab stil berish (viewport emas!).
- **`:has()` selector** — “agar ichida bola elementi bo‘lsa” (parent selector).
- **Native nesting** (`&` belgisi bilan).
- **Cascade Layers** (`@layer`) — specificity muammosini hal qilish.
- **Logical Properties** (`margin-inline`, `padding-block` — RTL tillar uchun mukammal).
- **Scroll-driven animations**, **View Transitions**, **@property**.

**Manba:** MDN Container Queries (oxirgi yangilanish: 2026 yil mart), W3C CSS Snapshot 2026.

---

## 6. Senior maslahatlar (10+ yillik tajribadan)

1. Har doim **semantic HTML**dan boshlang (`<main>`, `<article>`, `<nav>`, `<section>`).
2. CSS fayllarni **modullar**ga ajrating (BEM, CSS Modules, Tailwind yoki vanilla + Cascade Layers).
3. **Specificity**ni boshqaring — `!important`dan qoching, `@layer`dan foydalaning.
4. **Responsive design**ni Container Queries bilan qiling (media queries o‘rniga).
5. Har bir loyihada **design system** yarating (CSS Custom Properties + design tokens).
6. **Performance** — kritikal CSS inline, qolganini async yuklang.
7. **Accessibility** — CSS bilan contrast, focus-visible, prefers-reduced-motion qo‘llang.
8. Har doim kodni **W3C Validator** va Lighthouse bilan tekshiring.
9. Frameworklarda ham (React, Vue) HTML va CSS ajratilishi saqlanishi kerak.
10. Yangi xususiyatlarni **progressive enhancement** tamoyili bilan qo‘llang.

---

## Nima uchun bu farqni bilish juda muhim?

- Noto‘g‘ri ajratish loyihani “div soup”ga aylantiradi va saqlashni qiyinlashtiradi.
- To‘g‘ri ajratish — tez rivojlanish, yaxshi SEO, mukammal a11y va katta jamoada samarali hamkorlik.
- 2026 yilda ham HTML “skelet”, CSS esa “go‘zallik va moslashuvchanlik” vazifasini bajaradi.

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) (oxirgi yangilanish: 2025 yil dekabr)
- [MDN Web Docs — CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) (oxirgi yangilanish: 2025 yil dekabr)
- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/) (oxirgi yangilanish: 15 aprel 2026)
- [W3C CSS Snapshot 2026](https://www.w3.org/TR/css-2026/)
- [MDN Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries)

**Muallif**: Senior Web Developer darajasida tayyorlandi. Barcha faktlar MDN, WHATWG va W3C rasmiy manbalaridan olingan va 2026 yil aprel holatiga mos.
