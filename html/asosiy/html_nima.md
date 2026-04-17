# HTML Nima? To‘liq Professional Qo‘llanma

**HTML** (to‘liq nomi: **HyperText Markup Language** — Gipermatnli belgilash tili) — bu veb-sahifalarni yaratish va tuzish uchun ishlatiladigan **standart belgilash tili** (markup language). U veb-sahifaning **mazmuni va strukturasini** belgilaydi: matn, rasmlar, linklar, jadval, video, forma va boshqa elementlarni qanday joylashtirishni brauzerga aytadi.

HTML — **dasturlash tili emas**, balki **belgilash tili**. U faqat sahifaning qanday ko‘rinishi va tuzilishini (strukturasini) tavsiflaydi. Sahifaning dizayni (ranglar, shriftlar, joylashuv, animatsiyalar) uchun **CSS** (Cascading Style Sheets), interaktivlik va dinamik xatti-harakatlar (tugmalar bosilganda, forma yuborilganda) uchun esa **JavaScript** ishlatiladi.

HTML vebning asosiy “skeleti” hisoblanadi. Har qanday zamonaviy veb-sayt, ilova yoki mobil veb HTML bilan boshlanadi.

---

## HTML qanday ishlaydi?

- HTML fayli oddiy matnli fayl bo‘lib, `.html` yoki `.htm` kengaytmaga ega.
- Unda maxsus **teglar** (tags) yordamida matn “belgilanadi”.
- Har bir element ochiluvchi (`<tag>`) va yopiluvchi (`</tag>`) teg bilan o‘raladi (ba’zi teglar o‘z-o‘zidan yopiladi, masalan `<img>`).
- Brauzer (Chrome, Firefox, Safari, Edge va boshqalar) HTML kodni o‘qib, uni **DOM** (Document Object Model) daraxtiga aylantiradi va foydalanuvchiga chiroyli, interaktiv sahifa sifatida ko‘rsatadi.

**Misol:**

```html
<p>Bu oddiy paragraf. <strong>Bu qalin matn</strong>.</p>
```

---

## HTMLning qisqa, ammo aniq tarixi

HTMLning rivoji vebning o‘zi bilan birga kechdi. Quyidagi ma’lumotlar rasmiy manbalarga asoslangan:

- **1989 yil (mart)**: Tim Berners-Lee (CERN laboratoriyasi, Shveytsariya) birinchi marta World Wide Web va HTML g‘oyasini taklif qildi. Maqsad — olimlar o‘rtasida hujjatlarni osongina almashish edi.
- **1991 yil**: Birinchi HTML versiyasi (informal).
- **1993 yil**: Birinchi rasmiy taklif (HTML 1.0).
- **1995 yil**: HTML 2.0 — birinchi standartlashtirilgan versiya.
- **1997 yil**: HTML 3.2.
- **1999 yil**: HTML 4.01 — uzoq vaqt davomida asosiy standart bo‘ldi.
- **2004 yil**: WHATWG (Web Hypertext Application Technology Working Group) guruhi HTML5 ustida ish boshladi (Apple, Mozilla, Opera tomonidan tashkil etilgan).
- **2014 yil (28 oktyabr)**: HTML5 W3C tomonidan rasman **Recommendation** (standart) sifatida qabul qilindi.
- **Hozirgi holat (2026 yil aprel)**: HTML “**Living Standard**” (doimiy yangilanadigan standart) bo‘lib, **WHATWG** tomonidan boshqariladi. W3C va WHATWG 2019 yildan beri hamkorlikda ishlaydi. W3C endi alohida versiyalarni chiqarmaydi — u WHATWG Living Standardga ishora qiladi.

**Manbalar**:

- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/) (so‘nggi yangilanish: 15 aprel 2026)
- [W3C HTML5 Recommendation (2014)](https://www.w3.org/TR/html5/)
- [CERN — Tim Berners-Lee va vebning tug‘ilishi](https://home.cern/science/computing/birth-web)

---

## Har bir HTML hujjatining asosiy strukturasining to‘liq namunasi (HTML5)

Har qanday to‘g‘ri HTML fayli quyidagi minimal struktura bilan boshlanishi kerak:

```html
<!DOCTYPE html>
<!-- Bu HTML5 ekanligini bildiradi va brauzerni "quirks mode"dan chiqaradi -->
<html lang="uz">
	<!-- Sahifa tili (SEO va ekran o‘quvchilar uchun muhim) -->
	<head>
		<meta charset="UTF-8" />
		<!-- Kodlash turi (o‘zbekcha harflar uchun zarur) -->
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<!-- Responsiv dizayn uchun -->
		<meta name="description" content="Sahifa tavsifi" />
		<!-- SEO uchun -->
		<title>Sahifa sarlavhasi — To‘liq va aniq</title>
		<!-- CSS va boshqa resurslar bu yerga qo‘shiladi -->
		<link rel="stylesheet" href="styles.css" />
	</head>
	<body>
		<header>
			<h1>Bu birinchi darajali sarlavha</h1>
		</header>

		<nav>
			<!-- Navigatsiya menyusi -->
		</nav>

		<main>
			<article>
				<h2>Maqola sarlavhasi</h2>
				<p>
					Bu oddiy paragraf matni. <strong>Bu qalin matn</strong>.
					<em>Bu kursiv matn</em>.
				</p>
				<a href="https://example.com" target="_blank" rel="noopener"
					>Bu havola (link)</a
				>
			</article>
		</main>

		<img
			src="rasm.jpg"
			alt="Rasmning to‘liq tavsifi — SEO va accessibility uchun majburiy"
			width="800"
			height="600"
			loading="lazy"
		/>

		<footer>
			<!-- Pastki qism -->
		</footer>
	</body>
</html>
```

---

## Eng muhim HTML elementlari (HTML5 semantikasi)

### Struktura va semantik teglar (Senior darajada tavsiya etiladi)

- `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`
- `<h1>`–`<h6>` (faqat bitta `<h1>` sahifada bo‘lishi kerak)

### Matn va kontent

- `<p>`, `<strong>`, `<em>`, `<mark>`, `<small>`, `<del>`, `<ins>`
- Ro‘yxatlar: `<ul>`, `<ol>`, `<li>`, `<dl>`, `<dt>`, `<dd>`

### Rasmlar va media

- `<img>`, `<picture>`, `<source>`, `<video>`, `<audio>`, `<iframe>`, `<figure>`, `<figcaption>`

### Forma va interaktiv elementlar

- `<form>`, `<input>`, `<button>`, `<label>`, `<select>`, `<textarea>`, `<fieldset>`, `<datalist>`

### Jadval

- `<table>`, `<caption>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`

### Boshqa muhim

- `<canvas>`, `<svg>`, `<details>`, `<summary>`, `<dialog>`

---

## HTML5 ning zamonaviy imkoniyatlari

- **Semantik teglar** — brauzer, qidiruv tizimlari (Google) va ekran o‘quvchilar (NVDA, VoiceOver) uchun mazmunni yaxshiroq tushunish.
- **Media elementlari** — video va audio to‘g‘ridan-to‘g‘ri qo‘llab-quvvatlash (Flash o‘ldi!).
- **Canvas va SVG** — brauzer ichida grafika va animatsiya.
- **Form yangiliklari** — `required`, `placeholder`, `pattern`, `email`, `tel`, `date` va boshqalar.
- **Web Storage** (`localStorage`, `sessionStorage`), **Geolocation**, **Drag & Drop**, **History API**.
- **Accessibility** (a11y) va **ARIA** atributlari bilan birgalikda ishlaydi.
- **Web Components** (Custom Elements, Shadow DOM) — HTMLning o‘zida komponentlar yaratish imkoniyati.

---

## Senior darajadagi Best Practices (Eng yaxshi amaliyotlar)

1. **Har doim `<!DOCTYPE html>`** bilan boshlang.
2. **Semantik HTML** ishlatish — `<div>` va `<span>`ni faqat kerak bo‘lganda qo‘llang.
3. **Har bir `<img>`** ga `alt` atributini yozing (bo‘sh bo‘lsa ham `alt=""`).
4. **Accessibility** — `aria-*` atributlari, to‘g‘ri heading ierarxiyasi, kontrast, keyboard navigatsiyasi.
5. **SEO** — to‘g‘ri `<title>`, meta teglar, headinglar, `rel="nofollow"` va boshqalar.
6. **Kodni toza saqlang** — indentatsiya, izohlar, validatsiya (https://validator.w3.org/).
7. **Responsivlik** — `viewport` meta tegi va media queries (CSS bilan).
8. **Performance** — `loading="lazy"` rasmlar uchun, keraksiz teglardan voz kechish.
9. **Xavfsizlik** — `target="_blank"` bilan `rel="noopener"` ishlatish.
10. **HTML ni CSS va JS bilan to‘g‘ri ajratish** — HTML faqat struktura, hech qachon stil yoki logika yozmang.

**Xatoliklar (Common Pitfalls):**

- Ko‘p `<div>` ishlatish (“div soup”).
- `<br>` bilan joylashtirish o‘rniga CSS `margin` ishlatish.
- Headinglarni stil uchun ishlatish (faqat mazmun ierarxiyasi uchun).

---

## Nima uchun HTML juda muhim? (Senior nuqtai nazar)

- Har bir veb-saytning **asosiy skeleti** — noto‘g‘ri HTML butun loyihani buzadi.
- **SEO** — Google sahifani HTML strukturasiga qarab indekslaydi.
- **Accessibility** — ko‘zi ojizlar va nogironlar uchun WCAG standartlariga mos kelishi kerak (qonuniy talab ko‘p mamlakatlarda).
- **Maintainability** — katta loyihalarda semantik HTML kodni o‘qishni osonlashtiradi.
- **Future-proof** — Living Standard doimiy yangilanadi, lekin asosiy tamoyillar o‘zgarmaydi.

HTMLni bilmasdan hech qanday zamonaviy frontend (React, Vue, Svelte, Angular) loyihasini to‘liq tushunib bo‘lmaydi — chunki hammasi HTMLga kompilyatsiya bo‘ladi.

---

## Qo‘shimcha resurslar va o‘qish uchun (Senior tavsiyalari)

- **Rasmiy hujjatlar**:
  - [MDN Web Docs — HTML](https://developer.mozilla.org/uz/docs/Web/HTML) (o‘zbekcha ham mavjud)
  - [WHATWG HTML Living Standard](https://html.spec.whatwg.org/)
- **Validator**: [W3C Markup Validation Service](https://validator.w3.org/)
- **Accessibility**: [WebAIM](https://webaim.org/), [A11Y Project](https://www.a11yproject.com/)
- **O‘rganish**: freeCodeCamp, MDN Learn HTML, “HTML and CSS: Design and Build Websites” (Jon Duckett)
