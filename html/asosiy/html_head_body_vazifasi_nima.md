# `<html>`, `<head>`, `<body>` Teglarining Vazifalari — To‘liq Senior Front-end Developer Qo‘llanmasi

**`<html>`, `<head>` va `<body>`** — bu HTML dokumentining **asosiy skeleti** (document skeleton). Ular nafaqat kod yozish uchun, balki **brauzer rendering pipeline**, **DOM Tree qurilishi**, **Critical Rendering Path (CRP)**, **Accessibility Tree**, **SEO** va **maintainability** uchun asosiy poydevor hisoblanadi.

Senior darajada biz bu teglarni “oddiy teglar” deb emas, balki **brauzer qanday parse qiladi**, **qidiruv tizimlari va ekran o‘quvchilar qanday o‘qiydi** va **loyihaning kelajakdagi barqarorligi** nuqtai nazaridan chuqur tahlil qilamiz.

Quyidagi material **MDN Web Docs (2025 yil iyul va sentyabr yangilanishlari)** hamda **WHATWG HTML Living Standard (15 aprel 2026 yangilanishi)** ga asoslangan holda tayyorlangan. Har bir qism batafsil, misollar bilan va real amaliyotlar bilan boyitilgan.

---

## 1. `<html>` — Dokumentning **Root (Ildiz) Elementi** (Eng yuqori darajadagi element)

**Rasmiy ta’rif (MDN + WHATWG):**  
`<html>` elementi HTML dokumentining **root (top-level) elementi** hisoblanadi. Barcha boshqa elementlar uning avlodlari (descendants) bo‘lishi **shart**. Dokumentda **faqat bitta** `<html>` elementi bo‘ladi.

**Senior darajadagi vazifalari:**

- Brauzer **DOM Tree** ni qurishni shu elementdan boshlaydi (parsingning birinchi nuqtasi).
- Butun sahifaning **global kontekstini** belgilaydi: til, yozish yo‘nalishi, namespace.
- **Accessibility (a11y)** uchun eng muhim: `lang="uz"` atributi ekran o‘quvchilarga (NVDA, VoiceOver, TalkBack) sahifa tilini to‘g‘ri e’lon qiladi. Agar yo‘q bo‘lsa, OS tili ishlatiladi va talaffuz xato bo‘ladi (WCAG 2.2 — Success Criterion 3.1.1 “Language of Page”).
- **SEO**: Google, Yandex va boshqa botlar sahifaning asosiy tilini shu yerdan o‘qiydi → indekslash yaxshilanadi.
- **Performance**: Brauzer parsing va renderingni `<html>` dan boshlab, butun hujjatni shu kontekstda qayta ishlaydi.

**Senior Best Practice (2026):**

```html
<!DOCTYPE html>
<html lang="uz" dir="ltr">
	<!-- dir="rtl" faqat arabcha, forscha, ivritcha sahifalar uchun -->
	<head>
		...
	</head>
	<body>
		...
	</body>
</html>
```

**Hech qachon** `lang` atributisiz qoldirmang. Bu kichik narsa, lekin accessibility auditlarda (Lighthouse) va real foydalanuvchilar tajribasida katta farq qiladi.

---

## 2. `<head>` — **Metadata (Mashina o‘qiy oladigan ma’lumotlar) konteyneri**

**Rasmiy ta’rif:**  
`<head>` elementi dokument haqidagi **mashina (brauzer, botlar, ekran o‘quvchilar)** o‘qiy oladigan ma’lumotlarni (metadata) saqlaydi. U faqat **bitta** bo‘lishi mumkin va `<html>` ning **birinchi bolasi** bo‘lishi kerak.

**Senior darajadagi vazifalari:**

- **Critical Rendering Path (CRP)** ning birinchi va eng muhim bosqichi. Brauzer `<head>` ni to‘liq parse qilmaguncha `<body>` ni render qilmaydi.
- `charset`, `viewport` va `<title>` — bu uchta narsa birinchi 1-2 KB ichida bo‘lishi **shart** (FCP va LCP ni yaxshilash uchun).
- Stil, skript, favicon, manifest, Open Graph meta teglari shu yerda joylashadi.
- Foydalanuvchiga ko‘rinmaydi (faqat `<title>` brauzer yorlig‘ida ko‘rinadi).

**Majburiy va tavsiya etiladigan bolalar (2026 yil):**

- `<title>` — **majburiy** (faqat bitta).
- `<meta charset="UTF-8">` — **eng birinchi** bo‘lishi kerak.
- `<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">`
- `<link rel="stylesheet">`, `<script defer>`, favicon, manifest, OG meta teglari.

**Yomon amaliyot:** `<head>` ga og‘ir, bloklovchi skriptlarni qo‘yish — renderingni sekinlashtiradi.

---

## 3. `<body>` — **Ko‘rinadigan va interaktiv kontent konteyneri** (User-facing qism)

**Rasmiy ta’rif:**  
`<body>` elementi HTML dokumentining **ko‘rinadigan va foydalanuvchi bilan to‘g‘ridan-to‘g‘ri aloqada bo‘lgan** kontentini o‘z ichiga oladi. Dokumentda **faqat bitta** `<body>` bo‘lishi mumkin va u `<html>` ning **ikkinchi bolasi** bo‘lishi kerak.

**Senior darajadagi vazifalari:**

- Barcha **flow content** (matn, rasmlar, video, forma, `<section>`, `<article>`, `<nav>` va h.k.) shu yerda joylashadi.
- **Accessibility Tree** ning asosiy qismi: skip-link, landmark role’lar (`<main>`, `<header>`, `<footer>`) shu yerda.
- Brauzer `<head>` ni tugatgandan keyin `<body>` ni parse va render qilishni boshlaydi.
- Event handlerlar (`onload`, `onresize` va boshqalar) shu elementda yoki undan pastroqda ishlaydi.

**Senior Best Practice:**

- Birinchi farzand sifatida **skip-link** qo‘ying (klaviatura va ekran o‘quvchi foydalanuvchilari uchun majburiy).
- `<main id="main-content" role="main">` — faqat bitta bo‘lishi kerak (WCAG 2.2).
- Og‘ir skriptlarni oxirida yoki `defer`/`async` bilan joylashtiring.
- Hech qachon `<body>` ni `display: none` qilmang — bu SEO va a11y ni buzadi.

---

## 4. Uchala elementning o‘zaro munosabati va brauzer ichki mexanizmi (Senior chuqur tahlil)

| Element  | Joylashuvi             | Asosiy vazifasi                             | Soni (majburiy) | Senior muhimligi (2026)                   |
| -------- | ---------------------- | ------------------------------------------- | --------------- | ----------------------------------------- |
| `<html>` | Root (eng yuqori)      | Butun dokumentning ildizi + global kontekst | 1 ta            | DOM Tree root, lang/dir, CRP boshlanishi  |
| `<head>` | `<html>` ning 1-bolasi | Metadata (mashina uchun)                    | 1 ta            | Critical Rendering Path, SEO, meta teglar |
| `<body>` | `<html>` ning 2-bolasi | Ko‘rinadigan kontent (foydalanuvchi uchun)  | 1 ta            | Accessibility landmarks, user experience  |

**WHATWG qoidasi (15 aprel 2026):**  
`<html>` → `<head>` + (ixtiyoriy tag omission bilan) `<body>`. Brauzerlar tag omission ni qo‘llab-quvvatlaydi, lekin **senior kod** da har doim to‘liq yozamiz — bu kodni o‘qish, debug qilish, Git history va maintain qilish uchun zarur.

**Brauzer qanday ishlaydi (Critical Rendering Path):**

1. `<html>` → parsing boshlanadi.
2. `<head>` → metadata yuklanadi (charset, viewport, title).
3. CSSOM + DOM Tree birlashadi.
4. `<body>` → render boshlanadi.

---

## 5. To‘liq Production-Ready Minimal Struktura (Senior boilerplate)

```html
<!DOCTYPE html>
<html lang="uz" dir="ltr">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0, viewport-fit=cover"
		/>
		<title>Sahifa sarlavhasi — Sayt nomi</title>
		<!-- boshqa metadata, OG, favicon, critical CSS -->
	</head>
	<body>
		<!-- Accessibility uchun birinchi element -->
		<a href="#main-content" class="skip-link">Asosiy kontentga oʻtish</a>

		<main id="main-content" role="main">
			<!-- Sahifaning asosiy kontenti -->
		</main>

		<!-- Footer va boshqa elementlar -->
	</body>
</html>
```

---

## 6. Senior maslahatlar (10+ yillik tajribadan, loyihada qo‘llash)

1. **Hech qachon** bu uchta tegni o‘tkazib yubormang — garchi brauzer “tuzatib” bersa ham (maintainability buziladi).
2. `lang` ni `<html>` da, `charset` ni `<head>` ning **eng boshida** qo‘ying.
3. `<body>` ichida faqat semantic elementlardan (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`) foydalaning.
4. Har bir sahifani **Lighthouse** bilan tekshiring: “Document has a `<html>` with `lang` attribute”, “Document has `<title>`”, “No `<body>` element” kabi auditlarni o‘tkazing.
5. Katta loyihalarda (Next.js, Astro, Remix, Vue SSR) bu struktura avtomatik yaratiladi, lekin siz uni **override** qilish va to‘g‘rilashni bilishingiz kerak.
6. Web Components yoki Shadow DOM ishlatganda ham **parent document** da to‘g‘ri `<html>` struktura bo‘lishi shart.
7. **Progressive Enhancement** tamoyili: HTML skeleti birinchi, keyin CSS va JS ustiga qo‘shiladi.

---

## 7. Umumiy xatolar (Common Pitfalls) va oldini olish

- `<html>` ni bir necha marta qo‘yish yoki `lang`siz qoldirish → a11y va SEO muammolari.
- `<head>` ni `<body>` dan keyin yozish → brauzer xato tuzatadi, lekin CRP buziladi.
- `<body>` ni butunlay `display:none` qilish → ekran o‘quvchilar sahifani bo‘sh ko‘radi.
- Tag omissiondan foydalanish (productionda) → kod o‘qilishi qiyinlashadi.

---

## Rasmiy va ishonchli manbalar (2026 yil aprel holati)

- [MDN Web Docs — `<html>`: The HTML Document / Root element (Last modified: 24 sentyabr 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/html)
- [MDN Web Docs — `<head>`: The Document Metadata element (Last modified: 9 iyul 2025)](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/head)
- [MDN Web Docs — `<body>`: The Document Body element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/body)
- [WHATWG HTML Living Standard — Semantics: The `<html>` element (Last Updated: 15 aprel 2026)](https://html.spec.whatwg.org/multipage/semantics.html#the-html-element)
- [W3C WCAG 2.2 — Language of Page (3.1.1)](https://www.w3.org/WAI/WCAG22/Understanding/language-of-page)

**Muallif**: Senior Front-end Developer darajasida tayyorlandi. Barcha faktlar rasmiy MDN va WHATWG manbalaridan olingan va 2026 yil holatiga mos.
