# ValueVue LLC — Website

A professional business website for ValueVue LLC, a commercial real estate appraisal and advisory firm based in Texas.

Built with **Astro**, **Tailwind CSS**, and configured for **Netlify** deployment.

---

## Local Development

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- npm (comes with Node.js)

### Setup

```bash
cd site
npm install
npm run dev
```

The dev server starts at `http://localhost:4321`.

### Build

```bash
npm run build
```

Static output is generated in the `dist/` directory.

### Preview production build locally

```bash
npm run preview
```

---

## Deploy to Netlify

### Option A: Connect via GitHub (Recommended)

1. Push this repo to GitHub.
2. Go to [Netlify](https://app.netlify.com/) → **Add new site** → **Import an existing project**.
3. Connect your GitHub repo.
4. Set the following build settings:
   - **Base directory:** `site`
   - **Build command:** `npm run build`
   - **Publish directory:** `site/dist`
5. Click **Deploy site**.

Netlify will automatically rebuild on every push to your main branch.

### Option B: Manual Deploy (Netlify CLI)

```bash
npm install -g netlify-cli
cd site
npm run build
netlify deploy --prod --dir=dist
```

---

## Connect a GoDaddy Domain to Netlify

1. In Netlify, go to your site → **Domain management** → **Add a custom domain**.
2. Enter your domain (e.g., `www.valuevuellc.com`) and confirm.
3. Netlify will provide DNS settings. You have two options:

### Option A: Use Netlify DNS (Recommended)

1. In Netlify, go to **Domain management** → **Set up Netlify DNS**.
2. Netlify will provide 4 nameservers (e.g., `dns1.p01.nsone.net`).
3. In GoDaddy, go to your domain → **DNS** → **Nameservers** → **Change** → **Enter my own nameservers**.
4. Enter the 4 Netlify nameservers.
5. Save. DNS propagation takes up to 48 hours.

### Option B: Use GoDaddy DNS with CNAME

1. In GoDaddy, go to your domain → **DNS** → **DNS Records**.
2. Add a **CNAME** record:
   - **Name:** `www`
   - **Value:** Your Netlify site URL (e.g., `your-site-name.netlify.app`)
   - **TTL:** 1 hour
3. For the root domain (`@`), add a **forwarding rule** in GoDaddy to redirect to `www.yourdomain.com`.
4. In Netlify, verify the domain and enable HTTPS (automatic with Let's Encrypt).

---

## Formspree Contact Form Setup

The contact form is located in `src/pages/contact.astro`.

### Steps

1. Go to [Formspree](https://formspree.io/) and create a free account.
2. Create a new form — Formspree will give you an endpoint like: `https://formspree.io/f/xyzabcde`
3. Open `src/pages/contact.astro` and replace the placeholder:

```javascript
const formAction = 'https://formspree.io/f/YOUR_FORM_ID';
```

with your actual Formspree endpoint:

```javascript
const formAction = 'https://formspree.io/f/xyzabcde';
```

4. (Optional) You can also use an environment variable:
   - Copy `.env.example` to `.env`
   - Set `PUBLIC_FORMSPREE_ENDPOINT=https://formspree.io/f/xyzabcde`
   - Update the form action to: `import.meta.env.PUBLIC_FORMSPREE_ENDPOINT`
   - Add the env variable in Netlify: **Site settings** → **Environment variables**

---

## Project Structure

```
site/
├── public/
│   ├── favicon.svg            # Placeholder favicon
│   └── og-image.jpg           # Placeholder Open Graph image
├── src/
│   ├── components/
│   │   ├── CTA.astro          # Call-to-action banner
│   │   ├── Footer.astro       # Site footer
│   │   ├── Header.astro       # Sticky navigation header
│   │   ├── Hero.astro         # Hero section (home + page variants)
│   │   ├── SectionHeading.astro # Reusable section heading
│   │   └── ServiceCard.astro  # Service card component
│   ├── layouts/
│   │   └── BaseLayout.astro   # Base HTML layout with SEO
│   ├── pages/
│   │   ├── index.astro        # Home page
│   │   ├── services.astro     # Services page
│   │   ├── about.astro        # About page
│   │   └── contact.astro      # Contact page
│   └── styles/
│       └── global.css         # Global styles + Tailwind imports
├── astro.config.mjs           # Astro configuration
├── tailwind.config.mjs        # Tailwind configuration
├── netlify.toml               # Netlify build configuration
├── package.json
├── tsconfig.json
├── .env.example               # Environment variable template
└── .gitignore
```

---

## Replacing Placeholder Content

Look for these markers throughout the codebase:

- `[ ... placeholder ]` — image/photo placeholders
- `Placeholder` — text content to be replaced
- `+1 (000) 000-0000` — phone number placeholder
- `info@valuevuellc.com` — email placeholder
- `YOUR_FORM_ID` — Formspree endpoint placeholder
- `og-image.jpg` — replace with actual Open Graph image (1200×630px recommended)
- `favicon.svg` — replace with actual brand favicon

---

## Tech Stack

- **Framework:** [Astro](https://astro.build/) v4 (static output)
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) v3
- **Fonts:** Inter + Playfair Display (Google Fonts)
- **Forms:** [Formspree](https://formspree.io/)
- **Hosting:** [Netlify](https://www.netlify.com/)
- **No JavaScript frameworks** — plain Astro components only
