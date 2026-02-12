# Evollure - Código Completo do Site

## 📁 Estrutura do Projeto

```
├── index.html
├── vite.config.ts
├── tailwind.config.ts
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── index.css
│   ├── lib/utils.ts
│   ├── contexts/LeadModalContext.tsx
│   ├── hooks/
│   │   ├── use-mobile.tsx
│   │   └── use-toast.ts
│   ├── pages/
│   │   ├── Index.tsx
│   │   └── NotFound.tsx
│   ├── components/
│   │   ├── Navbar.tsx
│   │   ├── NavLink.tsx
│   │   ├── HeroSection.tsx
│   │   ├── LogoCloud.tsx
│   │   ├── FeaturesSection.tsx
│   │   ├── MethodologySection.tsx
│   │   ├── AuthorityBlock.tsx
│   │   ├── SavingsCalculatorSection.tsx
│   │   ├── UrgencyBlock.tsx
│   │   ├── BeforeAfterSection.tsx
│   │   ├── FAQSection.tsx
│   │   ├── CTASection.tsx
│   │   ├── LeadModal.tsx
│   │   ├── Footer.tsx
│   │   └── ui/shimmer-button.tsx
│   └── integrations/supabase/
│       ├── client.ts
│       └── types.ts
├── supabase/functions/submit-lead/index.ts
```

---

## 📄 `index.html`

```html
<!doctype html>
<html lang="pt-BR" class="dark">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Evollure - Plataforma SaaS Empresarial</title>
    <meta name="description" content="A plataforma moderna para equipes que entregam rápido. Construída para escalar, projetada para velocidade." />
    <meta name="author" content="Evollure" />
    <meta property="og:title" content="Evollure - Plataforma SaaS Empresarial" />
    <meta property="og:description" content="A plataforma moderna para equipes que entregam rápido." />
    <meta property="og:type" content="website" />
    <meta name="twitter:card" content="summary_large_image" />
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

---

## 📄 `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";
import path from "path";
import { componentTagger } from "lovable-tagger";

export default defineConfig(({ mode }) => ({
  server: {
    host: "::",
    port: 8080,
    hmr: {
      overlay: false,
    },
  },
  plugins: [react(), mode === "development" && componentTagger()].filter(Boolean),
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
}));
```

---

## 📄 `tailwind.config.ts`

```ts
import type { Config } from "tailwindcss";

export default {
  darkMode: ["class"],
  content: ["./pages/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}", "./app/**/*.{ts,tsx}", "./src/**/*.{ts,tsx}"],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      fontFamily: {
        sans: ["Inter", "system-ui", "-apple-system", "sans-serif"],
        heading: ["Inter", "system-ui", "-apple-system", "sans-serif"],
      },
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
        sidebar: {
          DEFAULT: "hsl(var(--sidebar-background))",
          foreground: "hsl(var(--sidebar-foreground))",
          primary: "hsl(var(--sidebar-primary))",
          "primary-foreground": "hsl(var(--sidebar-primary-foreground))",
          accent: "hsl(var(--sidebar-accent))",
          "accent-foreground": "hsl(var(--sidebar-accent-foreground))",
          border: "hsl(var(--sidebar-border))",
          ring: "hsl(var(--sidebar-ring))",
        },
        zinc: {
          950: "hsl(var(--zinc-950))",
          900: "hsl(var(--zinc-900))",
          800: "hsl(var(--zinc-800))",
          700: "hsl(var(--zinc-700))",
          600: "hsl(var(--zinc-600))",
          500: "hsl(var(--zinc-500))",
          400: "hsl(var(--zinc-400))",
          300: "hsl(var(--zinc-300))",
          200: "hsl(var(--zinc-200))",
        },
        emerald: {
          500: "hsl(var(--emerald-500))",
          400: "hsl(var(--emerald-400))",
        },
        amber: {
          500: "hsl(var(--amber-500))",
          400: "hsl(var(--amber-400))",
          300: "hsl(var(--amber-300))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
        "shimmer-slide": {
          to: { transform: "translate(calc(100cqw - 100%), 0)" },
        },
        "spin-around": {
          "0%": { transform: "translateZ(0) rotate(0)" },
          "15%, 35%": { transform: "translateZ(0) rotate(90deg)" },
          "65%, 85%": { transform: "translateZ(0) rotate(270deg)" },
          "100%": { transform: "translateZ(0) rotate(360deg)" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
        "shimmer-slide": "shimmer-slide var(--speed) ease-in-out infinite alternate",
        "spin-around": "spin-around calc(var(--speed) * 2) infinite linear",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
} satisfies Config;
```

---

## 📄 `src/index.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 240 6% 4%;
    --foreground: 0 0% 98%;
    --card: 240 5% 8%;
    --card-foreground: 0 0% 98%;
    --popover: 240 5% 8%;
    --popover-foreground: 0 0% 98%;
    --primary: 152 56% 48%;
    --primary-foreground: 0 0% 100%;
    --secondary: 240 4% 14%;
    --secondary-foreground: 240 5% 65%;
    --muted: 240 4% 14%;
    --muted-foreground: 240 5% 55%;
    --accent: 240 4% 14%;
    --accent-foreground: 0 0% 98%;
    --destructive: 0 84% 60%;
    --destructive-foreground: 0 0% 98%;
    --border: 240 4% 16%;
    --input: 240 4% 16%;
    --ring: 152 56% 48%;
    --radius: 0.75rem;
    --sidebar-background: 240 6% 4%;
    --sidebar-foreground: 240 5% 65%;
    --sidebar-primary: 152 56% 48%;
    --sidebar-primary-foreground: 0 0% 100%;
    --sidebar-accent: 240 4% 14%;
    --sidebar-accent-foreground: 0 0% 98%;
    --sidebar-border: 240 4% 16%;
    --sidebar-ring: 152 56% 48%;
    --zinc-950: 240 6% 4%;
    --zinc-900: 240 4% 10%;
    --zinc-800: 240 4% 16%;
    --zinc-700: 240 4% 26%;
    --zinc-600: 240 4% 36%;
    --zinc-500: 240 4% 46%;
    --zinc-400: 240 5% 65%;
    --zinc-300: 240 5% 78%;
    --zinc-200: 240 5% 88%;
    --emerald-500: 152 56% 48%;
    --emerald-400: 152 56% 58%;
    --amber-500: 38 92% 50%;
    --amber-400: 38 92% 60%;
    --amber-300: 38 92% 70%;
    --heading-gradient: linear-gradient(to right, hsl(240 5% 65%), hsl(240 5% 78%), hsl(240 4% 50%));
    font-family: 'Inter', system-ui, -apple-system, sans-serif;
  }
}

@layer base {
  * { @apply border-border; }
  body { @apply bg-background text-foreground antialiased; }
  h1, h2, h3, h4, h5, h6 { font-family: 'Inter', system-ui, -apple-system, sans-serif; }
}

@keyframes pulse-glow {
  0%, 100% { opacity: 1; box-shadow: 0 0 0 0 hsl(152 56% 48% / 0.4); }
  50% { opacity: 0.8; box-shadow: 0 0 0 6px hsl(152 56% 48% / 0); }
}
.pulse-glow { animation: pulse-glow 2s ease-in-out infinite; }

@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
.animate-marquee { animation: marquee 30s linear infinite; }

.noise-overlay {
  position: fixed; inset: 0; z-index: 50; pointer-events: none; opacity: 0.03;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}

.feature-card { transition: border-color 0.3s ease, box-shadow 0.3s ease; }
.feature-card:hover { border-color: hsl(240 4% 22%); box-shadow: 0 0 30px -10px hsl(240 4% 16% / 0.5); }

@keyframes draw-line { from { stroke-dashoffset: 200; } to { stroke-dashoffset: 0; } }
.chart-line { stroke-dasharray: 200; animation: draw-line 2s ease-out forwards; }

.methodology-ring {
  background: conic-gradient(from 180deg, hsl(var(--emerald-500)) 0%, hsl(var(--emerald-400)) 25%, hsl(var(--zinc-800)) 50%, hsl(var(--zinc-900)) 75%, hsl(var(--emerald-500)) 100%);
  animation: spin-slow 12s linear infinite;
}

@keyframes spin-slow { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

@keyframes center-glow {
  0%, 100% { box-shadow: 0 0 40px 8px hsl(var(--emerald-500) / 0.08), 0 0 80px 20px hsl(var(--emerald-500) / 0.04); }
  50% { box-shadow: 0 0 60px 16px hsl(var(--emerald-500) / 0.15), 0 0 120px 40px hsl(var(--emerald-500) / 0.06); }
}
.methodology-center-glow { animation: center-glow 4s ease-in-out infinite; }

@keyframes dot-blink {
  0%, 20% { background-color: hsl(var(--emerald-500)); opacity: 1; }
  30%, 100% { background-color: transparent; opacity: 0.4; }
}
.methodology-dot { animation: dot-blink 2.4s ease-in-out infinite; }
.methodology-dot:nth-child(1) { animation-delay: 0s; }
.methodology-dot:nth-child(2) { animation-delay: 0.6s; }
.methodology-dot:nth-child(3) { animation-delay: 1.2s; }
.methodology-dot:nth-child(4) { animation-delay: 1.8s; }

@keyframes orbit-pulse {
  0%, 100% { opacity: 0.15; transform: scale(1); }
  50% { opacity: 0.05; transform: scale(1.04); }
}
.methodology-orbit { animation: orbit-pulse 5s ease-in-out infinite; }

@keyframes shimmer-spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
.animate-shimmer-spin {
  animation: shimmer-spin var(--shimmer-duration, 3s) linear infinite;
  background: conic-gradient(from 0deg, transparent 0%, var(--shimmer-color, rgba(255, 255, 255, 0.12)) 10%, transparent 20%, transparent 100%);
}
.shimmer-card { transition: box-shadow 0.3s ease; }
.shimmer-card:hover { box-shadow: 0 0 30px -10px hsl(240 4% 16% / 0.5); }

@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
.animate-float { animation: float 3s ease-in-out infinite; }
.animate-spin-slow { animation: spin-slow 12s linear infinite; }

@keyframes gridMove { 0% { transform: translate(0, 0); } 100% { transform: translate(60px, 60px); } }
@keyframes badgeShimmer { 0% { background-position: 200% 0; } 100% { background-position: -200% 0; } }

@media (max-width: 640px) { input, textarea, select { font-size: 16px !important; } }
.overflow-y-auto { -webkit-overflow-scrolling: touch; }
@supports (-webkit-touch-callout: none) { .max-h-\[90dvh\] { max-height: -webkit-fill-available; } }
```

---

## 📄 `src/main.tsx`

```tsx
import { createRoot } from "react-dom/client";
import App from "./App.tsx";
import "./index.css";

createRoot(document.getElementById("root")!).render(<App />);
```

---

## 📄 `src/App.tsx`

```tsx
import { Toaster } from "@/components/ui/toaster";
import { Toaster as Sonner } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { LeadModalProvider } from "@/contexts/LeadModalContext";
import LeadModal from "@/components/LeadModal";
import Index from "./pages/Index";
import NotFound from "./pages/NotFound";

const queryClient = new QueryClient();

const App = () => (
  <QueryClientProvider client={queryClient}>
    <TooltipProvider>
      <LeadModalProvider>
        <Toaster />
        <Sonner />
        <LeadModal />
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<Index />} />
            <Route path="*" element={<NotFound />} />
          </Routes>
        </BrowserRouter>
      </LeadModalProvider>
    </TooltipProvider>
  </QueryClientProvider>
);

export default App;
```

---

## 📄 `src/lib/utils.ts`

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

---

## 📄 `src/contexts/LeadModalContext.tsx`

```tsx
import { createContext, useContext, useState, ReactNode } from "react";

interface LeadModalContextType {
  isOpen: boolean;
  openModal: () => void;
  closeModal: () => void;
}

const LeadModalContext = createContext<LeadModalContextType | undefined>(undefined);

export const LeadModalProvider = ({ children }: { children: ReactNode }) => {
  const [isOpen, setIsOpen] = useState(false);
  return (
    <LeadModalContext.Provider
      value={{ isOpen, openModal: () => setIsOpen(true), closeModal: () => setIsOpen(false) }}
    >
      {children}
    </LeadModalContext.Provider>
  );
};

export const useLeadModal = () => {
  const ctx = useContext(LeadModalContext);
  if (!ctx) throw new Error("useLeadModal must be used within LeadModalProvider");
  return ctx;
};
```

---

## 📄 `src/hooks/use-mobile.tsx`

```tsx
import * as React from "react";

const MOBILE_BREAKPOINT = 768;

export function useIsMobile() {
  const [isMobile, setIsMobile] = React.useState<boolean | undefined>(undefined);
  React.useEffect(() => {
    const mql = window.matchMedia(`(max-width: ${MOBILE_BREAKPOINT - 1}px)`);
    const onChange = () => { setIsMobile(window.innerWidth < MOBILE_BREAKPOINT); };
    mql.addEventListener("change", onChange);
    setIsMobile(window.innerWidth < MOBILE_BREAKPOINT);
    return () => mql.removeEventListener("change", onChange);
  }, []);
  return !!isMobile;
}
```

---

## 📄 `src/pages/Index.tsx`

```tsx
import Navbar from "@/components/Navbar";
import HeroSection from "@/components/HeroSection";
import LogoCloud from "@/components/LogoCloud";
import FeaturesSection from "@/components/FeaturesSection";
import MethodologySection from "@/components/MethodologySection";
import AuthorityBlock from "@/components/AuthorityBlock";
import SavingsCalculatorSection from "@/components/SavingsCalculatorSection";
import UrgencyBlock from "@/components/UrgencyBlock";
import BeforeAfterSection from "@/components/BeforeAfterSection";
import FAQSection from "@/components/FAQSection";
import CTASection from "@/components/CTASection";
import Footer from "@/components/Footer";

const Index = () => {
  return (
    <div className="min-h-screen bg-background">
      <div className="noise-overlay" aria-hidden="true" />
      <Navbar />
      <main>
        <HeroSection />
        <LogoCloud />
        <FeaturesSection />
        <MethodologySection />
        <AuthorityBlock />
        <SavingsCalculatorSection />
        <UrgencyBlock />
        <BeforeAfterSection />
        <FAQSection />
        <CTASection />
      </main>
      <Footer />
    </div>
  );
};

export default Index;
```

---

## 📄 `src/pages/NotFound.tsx`

```tsx
import { useLocation } from "react-router-dom";
import { useEffect } from "react";

const NotFound = () => {
  const location = useLocation();
  useEffect(() => {
    console.error("404 Error: User attempted to access non-existent route:", location.pathname);
  }, [location.pathname]);

  return (
    <div className="flex min-h-screen items-center justify-center bg-muted">
      <div className="text-center">
        <h1 className="mb-4 text-4xl font-bold">404</h1>
        <p className="mb-4 text-xl text-muted-foreground">Oops! Page not found</p>
        <a href="/" className="text-primary underline hover:text-primary/90">Return to Home</a>
      </div>
    </div>
  );
};

export default NotFound;
```

---

## 📄 `src/components/Navbar.tsx`

```tsx
import logoEvollure from "@/assets/logo-evollure.png";

const Navbar = () => {
  return (
    <nav className="fixed top-4 left-1/2 -translate-x-1/2 z-50">
      <div className="flex items-center gap-1 px-2 py-2 rounded-full bg-zinc-900/80 border border-border backdrop-blur-xl">
        <a href="/" className="flex items-center gap-2 px-4 py-1.5">
          <div className="w-6 h-6 bg-foreground shrink-0" style={{
            WebkitMaskImage: `url(${logoEvollure})`,
            WebkitMaskSize: 'contain',
            WebkitMaskRepeat: 'no-repeat',
            WebkitMaskPosition: 'center',
            maskImage: `url(${logoEvollure})`,
            maskSize: 'contain',
            maskRepeat: 'no-repeat',
            maskPosition: 'center',
            maskMode: 'luminance'
          } as React.CSSProperties} />
          <span className="font-heading font-semibold text-foreground text-lg">Evollure</span>
        </a>
        <div className="hidden md:flex items-center gap-1">
          <a href="#recursos" className="px-3 py-1.5 text-sm text-muted-foreground hover:text-foreground transition-colors rounded-full">Sobre</a>
          <a href="#documentacao" className="px-3 py-1.5 text-sm text-muted-foreground hover:text-foreground transition-colors rounded-full">Metodologia</a>
          <a href="#blog" className="px-3 py-1.5 text-sm text-muted-foreground hover:text-foreground transition-colors rounded-full">Blog</a>
        </div>
        <div className="hidden md:flex items-center gap-1 ml-2">
          <a href="#entrar" className="px-3 py-1.5 text-sm text-muted-foreground hover:text-foreground transition-colors rounded-full">Entrar</a>
        </div>
      </div>
    </nav>
  );
};

export default Navbar;
```

---

## 📄 `src/components/NavLink.tsx`

```tsx
import { NavLink as RouterNavLink, NavLinkProps } from "react-router-dom";
import { forwardRef } from "react";
import { cn } from "@/lib/utils";

interface NavLinkCompatProps extends Omit<NavLinkProps, "className"> {
  className?: string;
  activeClassName?: string;
  pendingClassName?: string;
}

const NavLink = forwardRef<HTMLAnchorElement, NavLinkCompatProps>(
  ({ className, activeClassName, pendingClassName, to, ...props }, ref) => {
    return (
      <RouterNavLink
        ref={ref}
        to={to}
        className={({ isActive, isPending }) =>
          cn(className, isActive && activeClassName, isPending && pendingClassName)
        }
        {...props}
      />
    );
  },
);

NavLink.displayName = "NavLink";
export { NavLink };
```

---

## 📄 `src/components/HeroSection.tsx`

```tsx
import { ArrowRight } from "lucide-react";
import { ShimmerButton } from "@/components/ui/shimmer-button";
import { useLeadModal } from "@/contexts/LeadModalContext";
import headshot1 from "@/assets/headshot-1.png";
import headshot2 from "@/assets/headshot-2.png";
import headshot3 from "@/assets/headshot-3.png";
import headshot4 from "@/assets/headshot-4.png";
import headshot5 from "@/assets/headshot-5.png";

const avatars = [headshot1, headshot2, headshot3, headshot4, headshot5];

const HeroSection = () => {
  const { openModal } = useLeadModal();
  return (
    <section className="relative min-h-screen flex flex-col items-center justify-center px-4 pt-24 pb-20 md:pb-16 overflow-hidden">
      <div className="absolute inset-0 bg-gradient-to-b from-zinc-950 via-zinc-900/80 to-background pointer-events-none" />
      <div className="absolute inset-0 pointer-events-none overflow-hidden">
        <div className="absolute inset-0 opacity-[0.04]" style={{
          backgroundImage: 'linear-gradient(rgba(255,255,255,0.5) 1px, transparent 1px), linear-gradient(90deg, rgba(255,255,255,0.5) 1px, transparent 1px)',
          backgroundSize: '60px 60px',
          animation: 'gridMove 20s linear infinite'
        }} />
      </div>
      <div className="absolute top-1/4 left-1/2 -translate-x-1/2 w-[800px] h-[600px] bg-zinc-800/20 rounded-full blur-3xl pointer-events-none" />

      <div className="relative z-10 max-w-5xl mx-auto text-center">
        <div className="relative inline-flex items-center gap-2 px-4 py-2 rounded-full bg-zinc-900 border border-border mb-8 overflow-hidden">
          <div className="absolute inset-0 overflow-hidden rounded-full">
            <div className="absolute inset-0 opacity-20" style={{
              background: 'linear-gradient(90deg, transparent 0%, transparent 30%, rgba(16,185,129,0.6) 50%, transparent 70%, transparent 100%)',
              backgroundSize: '200% 100%',
              animation: 'badgeShimmer 5s ease-in-out infinite'
            }} />
          </div>
          <span className="relative w-2 h-2 rounded-full bg-emerald-500 pulse-glow" />
          <span className="relative text-sm text-muted-foreground">Especialistas em I.A para negócios</span>
        </div>

        <h1 className="text-3xl sm:text-5xl lg:text-6xl font-bold tracking-tight text-foreground mb-6 font-heading" style={{ lineHeight: 1.2 }}>
          <span className="block overflow-hidden pb-1">
            <span className="block text-foreground">Enquanto seus concorrentes</span>
          </span>
          <span className="block overflow-hidden pb-1">
            <span className="block text-foreground">contratam pessoas,</span>
          </span>
          <span className="block overflow-hidden pb-3">
            <span className="block bg-gradient-to-r from-zinc-400 via-zinc-300 to-zinc-500 bg-clip-text text-transparent">
              você constrói inteligência.
            </span>
          </span>
        </h1>

        <p className="text-base sm:text-xl text-muted-foreground max-w-2xl mx-auto mb-10 leading-relaxed px-2">
          <span className="hidden sm:inline">Reduza custos operacionais, elimine retrabalho e escale resultados com </span>
          <span className="hidden sm:inline font-bold text-foreground">inteligência artificial personalizada</span>
          <span className="hidden sm:inline"> aplicada de forma estratégica.</span>
          <span className="inline sm:hidden">Reduza custos operacionais, elimine retrabalho e escale resultados com</span>
          <br className="sm:hidden" />
          <span className="inline sm:hidden font-bold text-foreground">inteligência artificial personalizada</span>
          <br className="sm:hidden" />
          <span className="inline sm:hidden">aplicada de forma estratégica.</span>
        </p>

        <div className="flex flex-col sm:flex-row items-center justify-center gap-4 mb-12">
          <button onClick={openModal}>
            <ShimmerButton shimmerColor="rgba(255,255,255,0.3)" shimmerSize="0.08em" shimmerDuration="2s" background="hsl(152, 56%, 48%)" className="text-sm font-medium text-background shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300">
              <span className="flex items-center gap-2">
                Quero aplicar inteligência ao meu negócio
                <ArrowRight className="w-4 h-4 group-hover:translate-x-0.5 transition-transform" />
              </span>
            </ShimmerButton>
          </button>
        </div>
        <p className="text-xs text-muted-foreground text-center max-w-md mx-auto mt-4">
          Conversa rápida para entender seu cenário e mapear oportunidades reais — sem compromisso.
        </p>
      </div>
    </section>
  );
};

export default HeroSection;
```

---

## 📄 `src/components/LogoCloud.tsx`

```tsx
import geminiLogo from "@/assets/logos/gemini.svg";
import anthropicLogo from "@/assets/logos/anthropic.svg";
import chatgptLogo from "@/assets/logos/chatgpt.svg";
import claudeLogo from "@/assets/logos/claude.svg";
import n8nLogo from "@/assets/logos/n8n.svg";
import metaLogo from "@/assets/logos/meta.svg";
import googleAdsLogo from "@/assets/logos/googleads.svg";
import replicateLogo from "@/assets/logos/replicate.svg";
import vercelLogo from "@/assets/logos/vercel.svg";
import notionLogo from "@/assets/logos/notion.svg";

const logos = [
  { name: "Gemini", logo: geminiLogo },
  { name: "Anthropic", logo: anthropicLogo },
  { name: "ChatGPT", logo: chatgptLogo },
  { name: "Claude", logo: claudeLogo },
  { name: "N8N", logo: n8nLogo },
  { name: "Meta AI", logo: metaLogo },
  { name: "Google Ads", logo: googleAdsLogo },
  { name: "Replicate", logo: replicateLogo },
  { name: "Vercel", logo: vercelLogo },
  { name: "Notion", logo: notionLogo },
];

const LogoItem = ({ name, logo }: { name: string; logo: string }) => (
  <div className="flex items-center gap-3 px-6">
    <div className="w-8 h-8 flex items-center justify-center">
      <img src={logo} alt={name} className="w-6 h-6 object-contain opacity-70" />
    </div>
    <span className="text-sm text-muted-foreground whitespace-nowrap">{name}</span>
  </div>
);

const LogoCloud = () => {
  return (
    <section className="relative py-12 md:py-16 overflow-hidden">
      <div className="text-center mb-10">
        <p className="text-xs font-medium uppercase tracking-[0.2em] text-muted-foreground">
          As melhores plataformas personalizadas para você
        </p>
      </div>
      <div className="relative">
        <div className="absolute left-0 top-0 bottom-0 w-32 bg-gradient-to-r from-background to-transparent z-10 pointer-events-none" />
        <div className="absolute right-0 top-0 bottom-0 w-32 bg-gradient-to-l from-background to-transparent z-10 pointer-events-none" />
        <div className="flex animate-marquee">
          {[...logos, ...logos].map((logo, i) => (
            <LogoItem key={`${logo.name}-${i}`} name={logo.name} logo={logo.logo} />
          ))}
        </div>
      </div>
    </section>
  );
};

export default LogoCloud;
```

---

## 📄 `src/components/FeaturesSection.tsx`

```tsx
import { Activity, BarChart3, Crosshair, Zap, Command, ArrowRight } from "lucide-react";
import { ShimmerButton } from "@/components/ui/shimmer-button";
import { useLeadModal } from "@/contexts/LeadModalContext";
import React from "react";

interface ShimmerCardProps {
  children: React.ReactNode;
  shimmerColor?: string;
  shimmerDuration?: string;
}

const ShimmerCard = ({ children, shimmerColor = "hsl(152, 56%, 48%, 0.35)", shimmerDuration = "3s" }: ShimmerCardProps) => {
  return (
    <div
      className="shimmer-card relative rounded-xl overflow-hidden"
      style={{ "--shimmer-color": shimmerColor, "--shimmer-duration": shimmerDuration } as React.CSSProperties}
    >
      <div className="absolute inset-0 overflow-hidden rounded-xl pointer-events-none">
        <div className="shimmer-spark absolute inset-[-200%] animate-shimmer-spin" />
      </div>
      <div className="relative rounded-xl bg-card m-[1px] p-6 h-[calc(100%-2px)]">
        {children}
      </div>
    </div>
  );
};

const FeaturesSection = () => {
  const { openModal } = useLeadModal();
  return (
    <section id="recursos" className="relative py-16 md:py-24 px-4">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-16">
          <h2 className="text-3xl sm:text-4xl lg:text-5xl font-bold text-foreground mb-4 font-heading">Ganhe tempo e performance com estratégias sob medida.</h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto leading-relaxed">Da criação de mídia à venda, do operacional a análise de dados. Ajudamos sua empresa a sair na frente com inteligência artificial.</p>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          <ShimmerCard>
            <div className="w-10 h-10 rounded-lg bg-zinc-800 border border-border flex items-center justify-center mb-4">
              <Crosshair className="w-5 h-5 text-muted-foreground" />
            </div>
            <h3 className="text-lg font-semibold text-foreground mb-2 font-heading">Agentes Personalizados</h3>
            <p className="text-sm text-muted-foreground mb-6">Desenvolvemos agentes de IA sob medida para cada necessidade do seu negócio, treinados diretamente nos seus processos.</p>
            <div className="flex items-center gap-2"></div>
          </ShimmerCard>

          <ShimmerCard>
            <div className="w-10 h-10 rounded-lg bg-zinc-800 border border-border flex items-center justify-center mb-4">
              <BarChart3 className="w-5 h-5 text-muted-foreground" />
            </div>
            <h3 className="text-lg font-semibold text-foreground mb-2 font-heading">Resultados Mensuráveis</h3>
            <p className="text-sm text-muted-foreground mb-6">Nosso foco é simples: gerar resultados práticos, mensuráveis e rápidos. Cada solução nasce com métricas claras para acompanhar a performance desde o início.</p>
            <div className="mt-auto"></div>
          </ShimmerCard>

          <ShimmerCard>
            <div className="w-10 h-10 rounded-lg bg-zinc-800 border border-border flex items-center justify-center mb-4">
              <Zap className="w-5 h-5 text-muted-foreground" />
            </div>
            <h3 className="text-lg font-semibold text-foreground mb-2 font-heading">Inteligência Aplicada</h3>
            <p className="text-sm text-muted-foreground mb-6 font-light">Transformamos dados em insights acionáveis e automatizamos decisões que antes dependiam totalmente de intervenção humana.</p>
          </ShimmerCard>
        </div>

        <div className="flex justify-center mt-12">
          <button onClick={openModal}>
            <ShimmerButton
              shimmerColor="rgba(255,255,255,0.3)"
              shimmerSize="0.08em"
              shimmerDuration="2s"
              background="hsl(152, 56%, 48%)"
              className="text-sm font-medium text-background shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300"
            >
              <span className="flex items-center gap-2">
                Quero aplicar IA no meu negócio
                <ArrowRight className="w-4 h-4 group-hover:translate-x-0.5 transition-transform" />
              </span>
            </ShimmerButton>
          </button>
        </div>
      </div>
    </section>
  );
};

export default FeaturesSection;
```

---

## 📄 `src/components/MethodologySection.tsx`

```tsx
import { Shield, GraduationCap, Settings, Power, ExternalLink } from "lucide-react";
import logoEvollure from "@/assets/logo-evollure.png";
import { Button } from "@/components/ui/button";
import { useLeadModal } from "@/contexts/LeadModalContext";

const pillars = [
  { number: 1, label: "imersao_ia ()", icon: Shield, position: "left-top" as const },
  { number: 2, label: "diagnostico_para_ia ()", icon: GraduationCap, position: "left-bottom" as const },
  { number: 3, label: "desenvolver_ia ()", icon: Settings, position: "right-top" as const },
  { number: 4, label: "escalar_com_ia ()", icon: Power, position: "right-bottom" as const },
];

const MethodologySection = () => {
  const { openModal } = useLeadModal();
  return (
    <section id="metodologia" className="relative py-20 md:py-[72px] px-4 overflow-hidden">
      <div className="max-w-5xl mx-auto">
        <div className="text-center mb-12 sm:mb-16">
          <span className="text-xs font-semibold tracking-[0.2em] uppercase text-emerald-400 mb-4 block">
            Transformação AI First
          </span>
          <h2 className="text-2xl sm:text-4xl lg:text-5xl font-bold text-foreground mb-6 font-heading">
            Os <span className="text-zinc-200">4 pilares</span> do Método Evollure
          </h2>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-6 sm:gap-8 max-w-3xl mx-auto mt-10 sm:mt-12 text-left">
            {[
              { icon: Shield, title: "Imersão no seu negócio", text: "Entendemos profundamente seus processos, gargalos e oportunidades reais de automação." },
              { icon: GraduationCap, title: "Diagnóstico estratégico", text: "Identificamos onde a inteligência artificial gera mais impacto com menor esforço operacional." },
              { icon: Settings, title: "Desenvolvimento sob medida", text: "Criamos soluções de IA personalizadas, alinhadas à sua operação e objetivos." },
              { icon: Power, title: "Escala com resultados", text: "Transformamos cada solução em ganhos mensuráveis, automáticos e sustentáveis." },
            ].map((item, index) => {
              const Icon = item.icon;
              return (
                <div key={index} className="flex items-start gap-4">
                  <div className="w-9 h-9 rounded-lg bg-zinc-900 border border-border flex items-center justify-center shrink-0 mt-0.5">
                    <Icon className="w-4 h-4 text-emerald-400" />
                  </div>
                  <div>
                    <h3 className="text-sm font-semibold text-foreground mb-1">{item.title}</h3>
                    <p className="text-sm text-muted-foreground leading-relaxed">{item.text}</p>
                  </div>
                </div>
              );
            })}
          </div>
        </div>

        {/* Mobile: Vertical list layout */}
        <div className="flex flex-col items-center gap-6 mb-12 md:hidden">
          <div className="relative w-[200px] h-[200px] mb-4">
            <div className="absolute inset-0 rounded-full methodology-ring" />
            <div className="absolute inset-[3px] rounded-full bg-background methodology-center-glow" />
            <div className="absolute inset-0 flex flex-col items-center justify-center z-10">
              <span className="text-emerald-400 text-xs font-medium mb-1 tracking-wide">_método</span>
              <div className="w-12 h-12 mb-1 bg-foreground" style={{
                WebkitMaskImage: `url(${logoEvollure})`, WebkitMaskSize: 'contain', WebkitMaskRepeat: 'no-repeat', WebkitMaskPosition: 'center',
                maskImage: `url(${logoEvollure})`, maskSize: 'contain', maskRepeat: 'no-repeat', maskPosition: 'center', maskMode: 'luminance'
              } as React.CSSProperties} />
              <span className="text-xl font-bold text-foreground font-heading">Evollure</span>
              <span className="text-[10px] tracking-[0.15em] uppercase text-muted-foreground mt-1">IA para Negócios</span>
              <div className="flex gap-1.5 mt-2">
                {[0, 1, 2, 3].map(i => <div key={i} className="w-1.5 h-1.5 rounded-full border border-zinc-600 methodology-dot" />)}
              </div>
            </div>
          </div>
          <div className="hidden">
            {pillars.map(pillar => {
              const Icon = pillar.icon;
              return (
                <div key={pillar.number} className="flex items-center gap-3 px-4 py-3 rounded-xl bg-zinc-900 border border-border">
                  <span className="text-sm font-bold text-emerald-400 w-5 shrink-0">{pillar.number}</span>
                  <div className="w-8 h-8 rounded-lg bg-zinc-800 border border-border flex items-center justify-center shrink-0">
                    <Icon className="w-4 h-4 text-emerald-400" />
                  </div>
                  <span className="text-sm text-zinc-300 font-mono">{pillar.label}</span>
                </div>
              );
            })}
          </div>
        </div>

        {/* Desktop: Circular diagram */}
        <div className="relative hidden md:flex items-center justify-center mb-16">
          <div className="relative w-[380px] h-[380px] lg:w-[420px] lg:h-[420px]">
            <div className="absolute -inset-4 rounded-full border border-emerald-500/10 methodology-orbit" />
            <div className="absolute -inset-8 rounded-full border border-emerald-500/5 methodology-orbit" style={{ animationDelay: "2.5s" }} />
            <div className="absolute inset-0 rounded-full methodology-ring" />
            <div className="absolute inset-[3px] rounded-full bg-background methodology-center-glow" />
            <div className="absolute inset-0 flex flex-col items-center justify-center z-10">
              <span className="text-emerald-400 text-xs font-medium mb-1 tracking-wide">_método</span>
              <div className="w-16 h-16 lg:w-20 lg:h-20 mb-1 bg-foreground" style={{
                WebkitMaskImage: `url(${logoEvollure})`, WebkitMaskSize: 'contain', WebkitMaskRepeat: 'no-repeat', WebkitMaskPosition: 'center',
                maskImage: `url(${logoEvollure})`, maskSize: 'contain', maskRepeat: 'no-repeat', maskPosition: 'center', maskMode: 'luminance'
              } as React.CSSProperties} />
              <span className="text-3xl font-bold text-foreground font-heading lg:text-5xl">Evollure</span>
              <span className="text-xs tracking-[0.15em] uppercase text-muted-foreground mt-2">IA para Negócios</span>
              <div className="flex gap-1.5 mt-3">
                {[0, 1, 2, 3].map(i => <div key={i} className="w-1.5 h-1.5 rounded-full border border-zinc-600 methodology-dot" />)}
              </div>
            </div>

            {pillars.map(pillar => {
              const Icon = pillar.icon;
              const dotOnCircle: Record<string, { top: string; left: string }> = {
                "left-top": { top: "22%", left: "2%" },
                "left-bottom": { top: "78%", left: "2%" },
                "right-top": { top: "22%", left: "98%" },
                "right-bottom": { top: "78%", left: "98%" },
              };
              const positionClasses: Record<string, string> = {
                "left-top": "absolute right-full top-1/2 -translate-y-1/2 mr-3",
                "left-bottom": "absolute right-full top-1/2 -translate-y-1/2 mr-3",
                "right-top": "absolute left-full top-1/2 -translate-y-1/2 ml-3",
                "right-bottom": "absolute left-full top-1/2 -translate-y-1/2 ml-3",
              };
              const isRight = pillar.position.includes("right");
              const dot = dotOnCircle[pillar.position];
              return (
                <div key={pillar.number} className="absolute -translate-x-1/2 -translate-y-1/2 z-20" style={{ top: dot.top, left: dot.left }}>
                  <div className="w-2.5 h-2.5 rounded-full bg-emerald-400 relative">
                    <div className={positionClasses[pillar.position]}>
                      <div className="flex items-center gap-2 whitespace-nowrap">
                        {isRight && <span className="text-sm font-bold text-emerald-400">{pillar.number}</span>}
                        <div className="flex items-center gap-2 px-4 py-2 rounded-full bg-zinc-900 border border-border">
                          <Icon className="w-4 h-4 text-emerald-400" />
                          <span className="text-sm text-zinc-300 font-mono whitespace-nowrap">{pillar.label}</span>
                        </div>
                        {!isRight && <span className="text-sm font-bold text-emerald-400">{pillar.number}</span>}
                      </div>
                    </div>
                  </div>
                </div>
              );
            })}
          </div>
        </div>

        <div className="text-center">
          <Button onClick={openModal} className="bg-emerald-500 hover:bg-emerald-400 text-background font-medium px-8 py-6 text-sm rounded-full shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300">
            Entender como funciona
            <ExternalLink className="w-4 h-4 ml-2" />
          </Button>
          <p className="text-sm text-muted-foreground mt-4">
            Agende uma <span className="font-semibold text-foreground">conversa rápida</span> para alinhar expectativas.
          </p>
        </div>
      </div>
    </section>
  );
};

export default MethodologySection;
```

---

## 📄 `src/components/AuthorityBlock.tsx`

```tsx
import { useEffect, useRef, useState } from "react";

const lines = [
  { text: "Não acreditamos em IA genérica.", highlight: false },
  { text: "Não acreditamos em automação sem contexto.", highlight: false },
  { text: "Não acreditamos em soluções que não geram números claros.", highlight: false },
];

const manifesto = {
  line1: "A Evollure existe para transformar complexidade operacional",
  line2: "em eficiência mensurável e estratégica.",
};

const AuthorityBlock = () => {
  const [visibleCount, setVisibleCount] = useState(0);
  const sectionRef = useRef<HTMLDivElement>(null);
  const hasTriggered = useRef(false);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting && !hasTriggered.current) {
          hasTriggered.current = true;
          let i = 0;
          const total = lines.length + 1;
          const interval = setInterval(() => {
            i++;
            setVisibleCount(i);
            if (i >= total) clearInterval(interval);
          }, 350);
        }
      },
      { threshold: 0.3 }
    );
    if (sectionRef.current) observer.observe(sectionRef.current);
    return () => observer.disconnect();
  }, []);

  return (
    <div ref={sectionRef} className="px-4 py-12 md:py-16">
      <div className="max-w-3xl mx-auto border-l-2 border-emerald-500/40 pl-6 sm:pl-8">
        <div className="space-y-3 mb-8">
          {lines.map((line, index) => (
            <p
              key={index}
              className="text-sm sm:text-base text-muted-foreground leading-relaxed transition-all duration-500 ease-out"
              style={{
                opacity: visibleCount > index ? 1 : 0,
                transform: visibleCount > index ? "translateY(0)" : "translateY(12px)",
              }}
            >
              {line.text}
            </p>
          ))}
        </div>
        <div
          className="transition-all duration-700 ease-out"
          style={{
            opacity: visibleCount > lines.length ? 1 : 0,
            transform: visibleCount > lines.length ? "translateY(0)" : "translateY(16px)",
          }}
        >
          <p className="text-lg sm:text-xl md:text-2xl font-semibold text-foreground leading-snug">{manifesto.line1}</p>
          <p className="text-lg sm:text-xl md:text-2xl font-semibold text-foreground leading-snug mt-1">{manifesto.line2}</p>
        </div>
      </div>
    </div>
  );
};

export default AuthorityBlock;
```

---

## 📄 `src/components/SavingsCalculatorSection.tsx`

```tsx
import { useState, useMemo, useEffect, useRef } from "react";
import { Calculator, Clock, TrendingUp, Zap, ExternalLink } from "lucide-react";
import { Slider } from "@/components/ui/slider";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
import { ShimmerButton } from "@/components/ui/shimmer-button";
import { useLeadModal } from "@/contexts/LeadModalContext";

const DIAS_UTEIS = 264;
const TAXA_AUTOMACAO = 0.8;

const formatCurrency = (value: number) =>
  new Intl.NumberFormat("pt-BR", {
    style: "currency",
    currency: "BRL",
    minimumFractionDigits: 2,
  }).format(value);

const formatNumber = (value: number) =>
  new Intl.NumberFormat("pt-BR").format(Math.round(value));

const SavingsCalculatorSection = () => {
  const { openModal } = useLeadModal();
  const [segmento, setSegmento] = useState("geral");
  const [funcionarios, setFuncionarios] = useState(10);
  const [horasPorDia, setHorasPorDia] = useState(2);
  const [custoHoraInput, setCustoHoraInput] = useState("50");
  const [isVisible, setIsVisible] = useState(false);
  const sectionRef = useRef<HTMLElement>(null);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setIsVisible(true);
          observer.disconnect();
        }
      },
      { threshold: 0.2 }
    );
    if (sectionRef.current) observer.observe(sectionRef.current);
    return () => observer.disconnect();
  }, []);

  const custoHora = Number(custoHoraInput) || 0;

  const { economiaAnual, horasSalvas, roiPotencial } = useMemo(() => {
    const economia =
      funcionarios * horasPorDia * DIAS_UTEIS * custoHora * TAXA_AUTOMACAO;
    const horas =
      funcionarios * horasPorDia * DIAS_UTEIS * TAXA_AUTOMACAO;
    const custoImplementacao = Math.max(economia * 0.1, 5000);
    const roi = custoImplementacao > 0 ? economia / custoImplementacao : 0;
    return { economiaAnual: economia, horasSalvas: horas, roiPotencial: roi };
  }, [funcionarios, horasPorDia, custoHora]);

  const handleCTA = () => {
    const message = encodeURIComponent(
      `Olá! Fiz uma simulação no site e gostaria de saber mais sobre como economizar ${formatCurrency(economiaAnual)} por ano, liberando ${formatNumber(horasSalvas)} horas com automação inteligente. Segmento: ${segmento}.`
    );
    window.open(`https://wa.me/5500000000000?text=${message}`, "_blank");
  };

  const tradicional = 35;
  const mercado = 55;
  const evollure = 92;

  return (
    <section
      ref={sectionRef}
      className="relative py-16 md:py-20 px-4 overflow-hidden transition-all duration-[450ms] ease-out"
      style={{
        opacity: isVisible ? 1 : 0,
        transform: isVisible ? "translateY(0)" : "translateY(20px)",
      }}
    >
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12 sm:mb-16">
          <span className="text-xs font-semibold tracking-[0.2em] uppercase text-emerald-400 mb-4 block">
            Simulador de Economia
          </span>
          <h2 className="text-2xl sm:text-4xl lg:text-5xl font-bold text-foreground mb-6">
            Calcule seu Potencial de{" "}
            <span className="text-zinc-200">Economia</span>
          </h2>
          <p className="text-sm sm:text-base text-muted-foreground max-w-2xl mx-auto leading-relaxed">
            Veja quanto sua empresa pode reduzir em custos operacionais ao
            transformar tarefas repetitivas em inteligência aplicada.
          </p>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-2 gap-6 lg:gap-8">
          <div className="rounded-xl border border-border bg-card p-6 sm:p-8 feature-card">
            <div className="flex items-center gap-3 mb-6">
              <div className="w-10 h-10 rounded-lg bg-secondary border border-border flex items-center justify-center">
                <Calculator className="w-5 h-5 text-emerald-400" />
              </div>
              <div>
                <h3 className="text-lg font-semibold text-foreground">
                  Parâmetros da sua Empresa
                </h3>
                <p className="text-xs text-muted-foreground">
                  Ajuste os valores conforme a realidade da sua operação.
                </p>
              </div>
            </div>

            <div className="space-y-6">
              <div className="space-y-2">
                <Label className="text-sm text-zinc-300">
                  Segmento de mercado
                </Label>
                <Select value={segmento} onValueChange={setSegmento}>
                  <SelectTrigger className="bg-secondary border-border text-foreground">
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent className="bg-card border-border">
                    <SelectItem value="geral">Geral</SelectItem>
                    <SelectItem value="servicos">Serviços</SelectItem>
                    <SelectItem value="industria">Indústria</SelectItem>
                    <SelectItem value="tecnologia">Tecnologia</SelectItem>
                  </SelectContent>
                </Select>
              </div>

              <div className="space-y-3">
                <div className="flex items-center justify-between">
                  <Label className="text-sm text-zinc-300">
                    Funcionários em tarefas manuais
                  </Label>
                  <span className="text-sm font-semibold text-emerald-400 tabular-nums">
                    {funcionarios}
                  </span>
                </div>
                <Slider
                  value={[funcionarios]}
                  onValueChange={([v]) => setFuncionarios(v)}
                  min={1}
                  max={100}
                  step={1}
                  className="[&_[role=slider]]:border-emerald-500 [&_[role=slider]]:bg-background [&_span:first-child>span]:bg-emerald-500 [&_span:first-child]:bg-secondary"
                />
                <div className="flex justify-between text-[10px] text-muted-foreground">
                  <span>1</span>
                  <span>100</span>
                </div>
              </div>

              <div className="space-y-3">
                <div className="flex items-center justify-between">
                  <Label className="text-sm text-zinc-300">
                    Horas/dia em tarefas repetitivas (por pessoa)
                  </Label>
                  <span className="text-sm font-semibold text-emerald-400 tabular-nums">
                    {horasPorDia}h
                  </span>
                </div>
                <Slider
                  value={[horasPorDia]}
                  onValueChange={([v]) => setHorasPorDia(v)}
                  min={1}
                  max={8}
                  step={1}
                  className="[&_[role=slider]]:border-emerald-500 [&_[role=slider]]:bg-background [&_span:first-child>span]:bg-emerald-500 [&_span:first-child]:bg-secondary"
                />
                <div className="flex justify-between text-[10px] text-muted-foreground">
                  <span>1h</span>
                  <span>8h</span>
                </div>
              </div>

              <div className="space-y-2">
                <Label className="text-sm text-zinc-300">
                  Custo médio por hora (R$)
                </Label>
                <div className="relative">
                  <span className="absolute left-3 top-1/2 -translate-y-1/2 text-muted-foreground text-sm">
                    R$
                  </span>
                  <Input
                    type="text"
                    inputMode="numeric"
                    value={custoHoraInput}
                    onChange={(e) => {
                      const raw = e.target.value.replace(/[^0-9]/g, "");
                      if (raw === "" || (Number(raw) >= 0 && Number(raw) <= 99999)) {
                        setCustoHoraInput(raw);
                      }
                    }}
                    onBlur={() => {
                      if (custoHoraInput === "" || Number(custoHoraInput) < 1) {
                        setCustoHoraInput("1");
                      }
                    }}
                    className="pl-10 bg-secondary border-border text-foreground"
                  />
                </div>
              </div>
            </div>
          </div>

          <div className="flex flex-col gap-6">
            <div className="rounded-xl border border-emerald-500/20 bg-card p-6 sm:p-8 relative overflow-hidden">
              <div
                className="absolute inset-0 opacity-[0.03]"
                style={{
                  background:
                    "radial-gradient(ellipse at 50% 0%, hsl(var(--emerald-500)), transparent 70%)",
                }}
              />
              <div className="relative z-10">
                <p className="text-xs font-semibold tracking-[0.15em] uppercase text-emerald-400 mb-2">
                  Economia Anual Estimada
                </p>
                <p className="text-3xl sm:text-4xl lg:text-5xl font-bold text-foreground tabular-nums transition-all duration-300">
                  {formatCurrency(economiaAnual)}
                </p>
                <p className="text-xs text-muted-foreground mt-3">
                  Estimativa baseada em automação média de 80%.
                </p>
              </div>
            </div>

            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div className="rounded-xl border border-border bg-card p-5 feature-card">
                <div className="flex items-center gap-2 mb-3">
                  <Clock className="w-4 h-4 text-emerald-400" />
                  <span className="text-xs font-semibold tracking-wider uppercase text-muted-foreground">
                    Horas economizadas/ano
                  </span>
                </div>
                <p className="text-2xl font-bold text-foreground tabular-nums transition-all duration-300">
                  {formatNumber(horasSalvas)}
                </p>
              </div>

              <div className="rounded-xl border border-border bg-card p-5 feature-card">
                <div className="flex items-center gap-2 mb-3">
                  <TrendingUp className="w-4 h-4 text-emerald-400" />
                  <span className="text-xs font-semibold tracking-wider uppercase text-muted-foreground">
                    ROI Potencial
                  </span>
                </div>
                <p className="text-2xl font-bold text-foreground tabular-nums transition-all duration-300">
                  {roiPotencial >= 1 ? `${roiPotencial.toFixed(1)}x` : "—"}
                </p>
              </div>
            </div>

            <div className="rounded-xl border border-border bg-card p-5 feature-card">
              <div className="flex items-center gap-2 mb-4">
                <Zap className="w-4 h-4 text-emerald-400" />
                <span className="text-xs font-semibold tracking-wider uppercase text-muted-foreground">
                  Comparativo de Eficiência
                </span>
              </div>
              <div className="space-y-3">
                {[
                  { label: "Operação tradicional", value: tradicional },
                  { label: "Média do mercado", value: mercado },
                  { label: "Com inteligência Evollure", value: evollure, highlight: true },
                ].map((item) => (
                  <div key={item.label} className="space-y-1">
                    <div className="flex items-center justify-between text-xs">
                      <span
                        className={
                          item.highlight
                            ? "text-emerald-400 font-medium"
                            : "text-muted-foreground"
                        }
                      >
                        {item.label}
                      </span>
                      <span
                        className={
                          item.highlight
                            ? "text-emerald-400 font-semibold"
                            : "text-zinc-400"
                        }
                      >
                        {item.value}%
                      </span>
                    </div>
                    <div className="h-2 rounded-full bg-secondary overflow-hidden">
                      <div
                        className={`h-full rounded-full transition-all duration-700 ease-out ${
                          item.highlight
                            ? "bg-emerald-500 shadow-[0_0_8px_hsl(var(--emerald-500)/0.4)]"
                            : "bg-zinc-600"
                        }`}
                        style={{ width: `${item.value}%` }}
                      />
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>

        <div className="text-center mt-12">
          <ShimmerButton
            onClick={openModal}
            background="hsl(152, 56%, 48%)"
            shimmerColor="rgba(255,255,255,0.15)"
            className="mx-auto text-sm font-medium shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300"
          >
            Quero essa economia na minha empresa
            <ExternalLink className="w-4 h-4 ml-2" />
          </ShimmerButton>
        </div>
      </div>
    </section>
  );
};

export default SavingsCalculatorSection;
```

---

## 📄 `src/components/UrgencyBlock.tsx`

```tsx
import { useEffect, useRef, useState } from "react";
import { Clock, TrendingUp } from "lucide-react";

const UrgencyBlock = () => {
  const [isVisible, setIsVisible] = useState(false);
  const sectionRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => { if (entry.isIntersecting) { setIsVisible(true); observer.disconnect(); } },
      { threshold: 0.3 }
    );
    if (sectionRef.current) observer.observe(sectionRef.current);
    return () => observer.disconnect();
  }, []);

  return (
    <div ref={sectionRef} className="px-4 py-12 md:py-16">
      <div className="max-w-4xl mx-auto rounded-xl border border-border bg-card p-6 sm:p-8 md:p-10">
        <div className="grid grid-cols-1 md:grid-cols-[1fr_auto_1fr] gap-6 md:gap-0 items-center">
          <div className="md:pr-10 transition-all duration-700 ease-out flex items-start gap-3"
            style={{ opacity: isVisible ? 1 : 0, transform: isVisible ? "translateX(0)" : "translateX(-20px)" }}>
            <div className="w-9 h-9 rounded-lg bg-secondary border border-border flex items-center justify-center shrink-0 mt-0.5">
              <Clock className="w-4 h-4 text-emerald-400" />
            </div>
            <p className="text-base sm:text-lg text-muted-foreground leading-relaxed">
              Enquanto você analisa, seus custos continuam rodando.
            </p>
          </div>
          <div className="hidden md:flex items-center justify-center"><div className="w-px h-12 bg-emerald-500/30" /></div>
          <div className="md:hidden w-full h-px bg-emerald-500/20" />
          <div className="md:pl-10 transition-all duration-700 ease-out flex items-start gap-3"
            style={{ opacity: isVisible ? 1 : 0, transform: isVisible ? "translateX(0)" : "translateX(20px)", transitionDelay: "200ms" }}>
            <div className="w-9 h-9 rounded-lg bg-secondary border border-border flex items-center justify-center shrink-0 mt-0.5">
              <TrendingUp className="w-4 h-4 text-emerald-400" />
            </div>
            <p className="text-base sm:text-lg font-semibold text-foreground leading-snug">
              Empresas que avançam agora transformam eficiência em <span className="text-emerald-400">vantagem competitiva</span>.
            </p>
          </div>
        </div>
      </div>
    </div>
  );
};

export default UrgencyBlock;
```

---

## 📄 `src/components/BeforeAfterSection.tsx`

```tsx
import { ArrowRight } from "lucide-react";
import { useEffect, useRef, useState } from "react";

const comparisons = [
  { before: "Tentando entender IA no meio do hype e das promessas vazias", after: "Agentes de IA sob medida, criados para atuar na sua rotina e nos seus processos específicos" },
  { before: "Gastando tempo e dinheiro com processos manuais e retrabalho", after: "Automatiza processos críticos, reduz custos e libera sua equipe para atividades de alto impacto" },
  { before: "Contratando mais pessoas para dar conta do crescimento", after: "Escala operações sem precisar aumentar o time, com IA trabalhando 24/7" },
  { before: "Recebendo dados sem saber como transformá-los em decisões estratégicas", after: "Transforma dados em insights acionáveis, permitindo decisões rápidas e precisas" },
  { before: "Dependendo de soluções genéricas que não se adaptam à operação", after: "Soluções integradas, adaptadas à sua operação e aos seus objetivos estratégicos" },
];

const fullText = "Antes vs Depois da Evollure";

const TypewriterTitle = () => {
  const [displayedText, setDisplayedText] = useState("");
  const [started, setStarted] = useState(false);
  const ref = useRef<HTMLHeadingElement>(null);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => { if (entry.isIntersecting && !started) { setStarted(true); } },
      { threshold: 0.5 }
    );
    if (ref.current) observer.observe(ref.current);
    return () => observer.disconnect();
  }, [started]);

  useEffect(() => {
    if (!started) return;
    let i = 0;
    const interval = setInterval(() => {
      i++;
      setDisplayedText(fullText.slice(0, i));
      if (i >= fullText.length) clearInterval(interval);
    }, 50);
    return () => clearInterval(interval);
  }, [started]);

  return (
    <h2 ref={ref} className="text-2xl sm:text-4xl lg:text-5xl font-bold text-foreground font-heading min-h-[1.2em]">
      {displayedText}
      <span className="inline-block w-[3px] h-[0.8em] bg-emerald-400 ml-1 align-baseline animate-pulse" />
    </h2>
  );
};

const BeforeAfterSection = () => {
  return (
    <section className="relative py-16 md:py-[72px] px-4 overflow-hidden">
      <div className="max-w-5xl mx-auto">
        <div className="text-center mb-12 sm:mb-16"><TypewriterTitle /></div>
        <div className="flex flex-col gap-4">
          {comparisons.map((item, index) => (
            <div key={index} className="grid grid-cols-1 md:grid-cols-[1fr_auto_1fr] gap-3 md:gap-4 items-stretch">
              <div className="rounded-xl border border-red-500/30 bg-red-500/5 p-5 flex flex-col justify-center">
                <span className="text-xs font-semibold tracking-[0.15em] uppercase text-red-400 mb-2">Antes</span>
                <p className="text-sm sm:text-base text-zinc-300 leading-relaxed">{item.before}</p>
              </div>
              <div className="hidden md:flex items-center justify-center px-2"><ArrowRight className="w-5 h-5 text-muted-foreground" /></div>
              <div className="flex md:hidden items-center justify-center py-1"><ArrowRight className="w-5 h-5 text-muted-foreground rotate-90" /></div>
              <div className="rounded-xl border border-emerald-500/40 bg-emerald-500/10 p-5 flex flex-col justify-center">
                <span className="text-xs font-semibold tracking-[0.15em] uppercase text-emerald-400 mb-2">Depois</span>
                <p className="text-sm sm:text-base text-zinc-300 leading-relaxed">{item.after}</p>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
};

export default BeforeAfterSection;
```

---

## 📄 `src/components/FAQSection.tsx`

```tsx
import { useState } from "react";
import { Plus, Minus, ExternalLink } from "lucide-react";
import { ShimmerButton } from "@/components/ui/shimmer-button";
import logoEvollureIcon from "@/assets/logo-evollure-icon.png";
import { useLeadModal } from "@/contexts/LeadModalContext";

interface FAQItemProps { question: string; answer: string; }

const FAQItem = ({ question, answer }: FAQItemProps) => {
  const [isOpen, setIsOpen] = useState(false);
  return (
    <div className="border border-[hsl(152,56%,48%,0.25)] rounded-xl overflow-hidden transition-colors duration-300"
      style={{ backgroundColor: isOpen ? "hsl(152, 40%, 12%, 0.3)" : "transparent" }}>
      <button onClick={() => setIsOpen(!isOpen)} className="w-full flex items-center justify-between px-6 py-5 text-left group">
        <span className="text-[hsl(152,70%,85%)] text-base sm:text-lg font-medium pr-4">{question}</span>
        <span className="flex-shrink-0 w-8 h-8 rounded-full border border-[hsl(152,56%,48%,0.4)] flex items-center justify-center text-emerald-400 transition-colors duration-200 group-hover:border-emerald-400">
          {isOpen ? <Minus className="w-4 h-4" /> : <Plus className="w-4 h-4" />}
        </span>
      </button>
      <div className="overflow-hidden transition-all duration-300 ease-in-out" style={{ maxHeight: isOpen ? "600px" : "0px", opacity: isOpen ? 1 : 0 }}>
        <div className="px-6 pb-5 text-[hsl(152,60%,90%,0.8)] text-sm sm:text-base leading-relaxed whitespace-pre-line">{answer}</div>
      </div>
    </div>
  );
};

const FAQSection = () => {
  const { openModal } = useLeadModal();
  const faqs: FAQItemProps[] = [
    {
      question: "Quem é a Evollure?",
      answer: "Pense na gente não como uma agência de tecnologia, mas como seus parceiros de transformação. Sabe aquela sensação de que a tecnologia avança rápido demais e sua empresa fica presa em processos manuais? Nós existimos para mudar isso.\n\nA Evollure nasceu da crença de que Inteligência Artificial não é apenas uma \"ferramenta\" que você adiciona, mas sim um novo sistema operacional para o seu negócio. Acreditamos em AI First: repensar a maneira como sua empresa trabalha, vende e cria, com a IA no centro de tudo. Somos um time de estrategistas que entende negócios, pessoas e tecnologia, movidos pela paixão por gerar resultados reais. Nosso trabalho é transformar a IA de uma promessa em impacto concreto no dia a dia da sua empresa.",
    },
    {
      question: "O que a Evollure faz?",
      answer: "De forma direta? A gente faz Agentes de IA trabalharem por você. De verdade. Nossa jornada juntos começa com um mergulho profundo no seu negócio. A gente senta com você para entender a operação de ponta a ponta e identificar onde a IA pode gerar mais impacto, seja aumentando receita ou cortando custos. Em seguida, cuidamos do seu time, capacitando e mostrando que a Inteligência Artificial é uma aliada, não uma ameaça.A partir daí, colocamos a mão na massa: nós construímos e implementamos os Agentes de IA que vão operar no seu dia a dia. Pense neles atuando em todas as áreas:\n\n• No marketing e vendas, eles criam campanhas, qualificam clientes e agendam reuniões, 24/7.\n‍\n• Na operação, logística e financeiro, eles otimizam processos, preveem gargalos e automatizam a rotina.\n\n• No backoffice e RH, eles organizam o caos, analisam dados e liberam as pessoas de tarefas repetitivas.\n\nEm resumo: nós integramos a IA em toda a sua empresa e liberamos sua equipe da sobrecarga operacional, para que ela possa focar no que realmente importa: ser mais estratégica e criativa.",
    },
  ];

  return (
    <section className="relative py-20 md:py-24 px-4">
      <div className="max-w-3xl mx-auto">
        <p className="text-center text-xs sm:text-sm font-medium tracking-[0.2em] uppercase text-emerald-400 mb-6">Perguntas Frequentes</p>
        <h2 className="text-center text-3xl sm:text-4xl lg:text-5xl font-bold text-foreground mb-12 font-heading leading-tight">
          As <span className="text-emerald-400">2 perguntas</span> que recebemos antes de toda grande <span className="text-foreground">parceria</span>.
        </h2>
        <div className="space-y-3 mb-4">
          {faqs.map((faq, index) => (<FAQItem key={index} question={faq.question} answer={faq.answer} />))}
        </div>
        <p className="text-sm text-[hsl(152,60%,90%,0.7)] text-center mb-20 leading-relaxed">
          Nenhuma solução é implementada sem diagnóstico prévio e validação de impacto financeiro para a operação.
        </p>

        <div className="relative rounded-2xl border border-[hsl(152,56%,48%,0.15)] overflow-hidden">
          <div className="absolute inset-0" style={{ background: "linear-gradient(135deg, hsl(152, 40%, 8%) 0%, hsl(152, 35%, 12%) 50%, hsl(152, 30%, 10%) 100%)" }} />
          <div className="absolute inset-0 opacity-[0.07]" style={{
            backgroundImage: "linear-gradient(hsl(152,56%,48%) 1px, transparent 1px), linear-gradient(90deg, hsl(152,56%,48%) 1px, transparent 1px)",
            backgroundSize: "40px 40px",
          }} />
          <div className="relative px-8 py-14 sm:py-16 text-center">
            <h3 className="text-2xl sm:text-3xl lg:text-4xl font-bold text-foreground mb-3 font-heading">
              Faça <span className="italic text-emerald-400">a IA</span> trabalhar por você
            </h3>
            <p className="text-muted-foreground text-sm sm:text-base mb-8">Empresas que adotam IA crescem até 3x mais rápido.</p>
            <div className="flex justify-center mb-4">
              <button onClick={openModal}>
                <ShimmerButton shimmerColor="rgba(255,255,255,0.3)" shimmerSize="0.08em" shimmerDuration="2s" background="hsl(152, 56%, 48%)"
                  className="text-sm font-medium text-background shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300">
                  <span className="flex items-center gap-2">Entender como funciona <ExternalLink className="w-4 h-4" /></span>
                </ShimmerButton>
              </button>
            </div>
            <p className="text-xs sm:text-sm text-muted-foreground">Conversa rápida para entender seu cenário e mapear oportunidades reais — sem compromisso.</p>
          </div>
        </div>
      </div>
    </section>
  );
};

export default FAQSection;
```

---

## 📄 `src/components/CTASection.tsx`

```tsx
import { ArrowRight } from "lucide-react";
const CTASection = () => {
  return null;
};
export default CTASection;
```

---

## 📄 `src/components/LeadModal.tsx`

```tsx
import { useState, useCallback } from "react";
import { ArrowRight } from "lucide-react";
import { Dialog, DialogContent, DialogTitle } from "@/components/ui/dialog";
import { ShimmerButton } from "@/components/ui/shimmer-button";
import { useLeadModal } from "@/contexts/LeadModalContext";
import { useToast } from "@/hooks/use-toast";
import { supabase } from "@/integrations/supabase/client";

interface FormData { nome: string; email: string; telefone: string; }
const initialForm: FormData = { nome: "", email: "", telefone: "" };

const LeadModal = () => {
  const { isOpen, closeModal } = useLeadModal();
  const { toast } = useToast();
  const [form, setForm] = useState<FormData>(initialForm);
  const [isSubmitting, setIsSubmitting] = useState(false);
  const [errors, setErrors] = useState<Partial<Record<keyof FormData, string>>>({});

  const scrollToField = useCallback((element: HTMLElement) => {
    setTimeout(() => { element.scrollIntoView({ behavior: "smooth", block: "center" }); }, 300);
  }, []);

  const handleFocus = useCallback((e: React.FocusEvent<HTMLInputElement>) => { scrollToField(e.currentTarget); }, [scrollToField]);

  const validate = (): boolean => {
    const newErrors: Partial<Record<keyof FormData, string>> = {};
    if (!form.nome.trim()) newErrors.nome = "Nome é obrigatório";
    else if (form.nome.trim().length > 100) newErrors.nome = "Máximo de 100 caracteres";
    if (!form.email.trim()) newErrors.email = "Email é obrigatório";
    else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email.trim())) newErrors.email = "Email inválido";
    if (!form.telefone.trim()) newErrors.telefone = "Telefone é obrigatório";
    else if (form.telefone.trim().length > 20) newErrors.telefone = "Máximo de 20 caracteres";
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleChange = (field: keyof FormData, value: string) => {
    setForm((prev) => ({ ...prev, [field]: value }));
    if (errors[field]) { setErrors((prev) => ({ ...prev, [field]: undefined })); }
  };

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    if (!validate()) return;
    setIsSubmitting(true);
    try {
      const { error } = await supabase.functions.invoke("submit-lead", {
        body: { nome: form.nome.trim(), email: form.email.trim(), telefone: form.telefone.trim(), empresa: "", descricao: "", pagina: window.location.href },
      });
      if (error) throw error;
      closeModal();
      setForm(initialForm);
      setErrors({});
      toast({ title: "Recebemos suas informações", description: "Em breve entraremos em contato." });
    } catch (err) {
      console.error("Lead submission error:", err);
      toast({ title: "Erro ao enviar", description: "Tente novamente em alguns instantes.", variant: "destructive" });
    } finally { setIsSubmitting(false); }
  };

  const handleOpenChange = (open: boolean) => { if (!open) { closeModal(); setErrors({}); } };

  return (
    <Dialog open={isOpen} onOpenChange={handleOpenChange}>
      <DialogContent className="sm:max-w-lg max-w-[calc(100vw-2rem)] bg-card border-border p-0 gap-0 max-h-[90dvh] overflow-y-auto overscroll-contain"
        style={{ WebkitOverflowScrolling: "touch" }} onOpenAutoFocus={(e) => e.preventDefault()}>
        <div className="relative px-6 sm:px-8 pt-6 sm:pt-8 pb-4 sm:pb-5 text-center">
          <div className="absolute inset-0 opacity-[0.03] pointer-events-none" style={{ background: "radial-gradient(ellipse at 50% 0%, hsl(152 56% 48%), transparent 70%)" }} />
          <div className="relative z-10 flex justify-center mb-3 sm:mb-5">
            <span className="font-heading font-bold text-2xl sm:text-3xl text-foreground tracking-tight drop-shadow-[0_0_12px_hsl(152_56%_48%/0.3)]">Evollure</span>
          </div>
          <DialogTitle className="text-lg sm:text-2xl font-bold text-foreground relative z-10 leading-tight">
            Vamos aplicar inteligência de verdade no seu negócio
          </DialogTitle>
          <p className="text-xs sm:text-sm text-muted-foreground mt-2 sm:mt-2 relative z-10">
            Conte rapidamente sobre sua empresa para entendermos onde a IA pode gerar mais impacto.
          </p>
        </div>
        <div className="h-px bg-border mx-6 sm:mx-8" />
        <form onSubmit={handleSubmit} className="px-6 sm:px-8 pt-6 sm:pt-8 pb-8 sm:pb-10">
          <div className="space-y-6 sm:space-y-7">
            <div className="space-y-2">
              <label htmlFor="lead-nome" className="block text-base sm:text-lg font-semibold text-foreground">Qual seu nome? <span className="text-emerald-400 font-normal">*</span></label>
              <input id="lead-nome" type="text" value={form.nome} onChange={(e) => handleChange("nome", e.target.value)} onFocus={handleFocus}
                className="w-full px-4 py-3.5 bg-secondary border border-border rounded-lg text-foreground placeholder:text-muted-foreground focus:outline-none focus:border-emerald-500/50 focus:ring-1 focus:ring-emerald-500/30 transition-all"
                placeholder="Seu nome completo" maxLength={100} autoComplete="name" style={{ fontSize: "16px" }} />
              {errors.nome && <p className="text-xs text-destructive mt-1">{errors.nome}</p>}
            </div>
            <div className="space-y-2">
              <label htmlFor="lead-email" className="block text-base sm:text-lg font-semibold text-foreground">Qual seu melhor e-mail? <span className="text-emerald-400 font-normal">*</span></label>
              <input id="lead-email" type="email" value={form.email} onChange={(e) => handleChange("email", e.target.value)} onFocus={handleFocus}
                className="w-full px-4 py-3.5 bg-secondary border border-border rounded-lg text-foreground placeholder:text-muted-foreground focus:outline-none focus:border-emerald-500/50 focus:ring-1 focus:ring-emerald-500/30 transition-all"
                placeholder="seu@empresa.com" maxLength={255} autoComplete="email" inputMode="email" style={{ fontSize: "16px" }} />
              {errors.email && <p className="text-xs text-destructive mt-1">{errors.email}</p>}
            </div>
            <div className="space-y-2">
              <label htmlFor="lead-telefone" className="block text-base sm:text-lg font-semibold text-foreground">Qual seu WhatsApp? <span className="text-emerald-400 font-normal">*</span></label>
              <input id="lead-telefone" type="tel" value={form.telefone} onChange={(e) => handleChange("telefone", e.target.value)} onFocus={handleFocus}
                className="w-full px-4 py-3.5 bg-secondary border border-border rounded-lg text-foreground placeholder:text-muted-foreground focus:outline-none focus:border-emerald-500/50 focus:ring-1 focus:ring-emerald-500/30 transition-all"
                placeholder="(00) 00000-0000" maxLength={20} autoComplete="tel" inputMode="tel" style={{ fontSize: "16px" }} />
              {errors.telefone && <p className="text-xs text-destructive mt-1">{errors.telefone}</p>}
            </div>
          </div>
          <div className="mt-8 sm:mt-8">
            <ShimmerButton type="submit" disabled={isSubmitting} background="hsl(152, 56%, 48%)" shimmerColor="rgba(255,255,255,0.3)" shimmerSize="0.08em" shimmerDuration="2s"
              className="h-12 px-8 text-sm font-semibold text-background shadow-[0_0_20px_4px_hsl(152_56%_48%/0.35)] hover:shadow-[0_0_30px_8px_hsl(152_56%_48%/0.45)] transition-shadow duration-300 disabled:opacity-50">
              <span className="flex items-center justify-center gap-2">
                {isSubmitting ? "Enviando..." : "Começar"}
                {!isSubmitting && <ArrowRight className="w-4 h-4" />}
              </span>
            </ShimmerButton>
          </div>
          <p className="text-[11px] sm:text-xs text-muted-foreground text-center mt-8 flex items-center justify-center gap-1.5">
            <svg className="w-3 h-3 opacity-60" fill="none" viewBox="0 0 24 24" stroke="currentColor" strokeWidth={2}>
              <path strokeLinecap="round" strokeLinejoin="round" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
            Dados protegidos. Zero spam.
          </p>
        </form>
      </DialogContent>
    </Dialog>
  );
};

export default LeadModal;
```

---

## 📄 `src/components/Footer.tsx`

```tsx
import logoEvollure from "@/assets/logo-evollure.png";

const Footer = () => {
  return (
    <footer className="border-t border-border py-12 px-4">
      <div className="max-w-6xl mx-auto flex flex-col items-center text-center gap-4">
        <a href="/" className="flex items-center gap-2">
          <div
            className="w-5 h-5 bg-foreground shrink-0"
            style={
              {
                WebkitMaskImage: `url(${logoEvollure})`,
                WebkitMaskSize: "contain",
                WebkitMaskRepeat: "no-repeat",
                WebkitMaskPosition: "center",
                maskImage: `url(${logoEvollure})`,
                maskSize: "contain",
                maskRepeat: "no-repeat",
                maskPosition: "center",
                maskMode: "luminance",
              } as React.CSSProperties
            }
          />
          <span className="font-heading text-sm font-semibold text-foreground">
            Evollure
          </span>
        </a>
        <p className="text-sm text-muted-foreground max-w-xs">
          A plataforma moderna para equipes que entregam rápido.
        </p>
        <p className="text-xs text-muted-foreground pt-4">
          © 2026 Evollure. Todos os direitos reservados.
        </p>
      </div>
    </footer>
  );
};

export default Footer;
```

---

## 📄 `src/components/ui/shimmer-button.tsx`

```tsx
import React, { CSSProperties } from "react";
import { cn } from "@/lib/utils";

export interface ShimmerButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  shimmerColor?: string; shimmerSize?: string; borderRadius?: string; shimmerDuration?: string; background?: string; className?: string; children?: React.ReactNode;
}

const ShimmerButton = React.forwardRef<HTMLButtonElement, ShimmerButtonProps>(
  ({ shimmerColor = "#ffffff", shimmerSize = "0.05em", shimmerDuration = "3s", borderRadius = "100px", background = "rgba(0, 0, 0, 1)", className, children, ...props }, ref) => {
    return (
      <button
        style={{ "--spread": "90deg", "--shimmer-color": shimmerColor, "--radius": borderRadius, "--speed": shimmerDuration, "--cut": shimmerSize, "--bg": background } as CSSProperties}
        className={cn("group relative z-0 flex items-center justify-center cursor-pointer overflow-hidden whitespace-nowrap border border-white/10 px-6 py-3 [background:var(--bg)] [border-radius:var(--radius)]", "transform-gpu transition-transform duration-300 ease-in-out active:translate-y-px", className)}
        ref={ref} {...props}>
        <div className={cn("absolute inset-0 overflow-visible [container-type:size]")} style={{ zIndex: -30, filter: "blur(2px)" }}>
          <div className="absolute inset-0 animate-shimmer-slide [aspect-ratio:1] [border-radius:0] [mask:none]" style={{ height: "100cqh" }}>
            <div className="animate-spin-around absolute w-auto rotate-0" style={{
              inset: "-100%", background: `conic-gradient(from calc(270deg - (var(--spread) * 0.5)), transparent 0, var(--shimmer-color) var(--spread), transparent var(--spread))`, translate: "0 0",
            }} />
          </div>
        </div>
        {children}
        <div className={cn("absolute inset-0 size-full", "rounded-2xl px-4 py-1.5 text-sm font-medium shadow-[inset_0_-8px_10px_#ffffff1f]",
          "transform-gpu transition-all duration-300 ease-in-out", "group-hover:shadow-[inset_0_-6px_10px_#ffffff3f]", "group-active:shadow-[inset_0_-10px_10px_#ffffff3f]")} />
        <div style={{ zIndex: -20, background: "var(--bg)", borderRadius: "var(--radius)", inset: "var(--cut)" }} className="absolute" />
      </button>
    );
  },
);

ShimmerButton.displayName = "ShimmerButton";
export { ShimmerButton };
```

---

## 📄 `src/integrations/supabase/client.ts`

```ts
import { createClient } from '@supabase/supabase-js';
import type { Database } from './types';

const SUPABASE_URL = import.meta.env.VITE_SUPABASE_URL;
const SUPABASE_PUBLISHABLE_KEY = import.meta.env.VITE_SUPABASE_PUBLISHABLE_KEY;

export const supabase = createClient<Database>(SUPABASE_URL, SUPABASE_PUBLISHABLE_KEY, {
  auth: { storage: localStorage, persistSession: true, autoRefreshToken: true },
});
```

---

## 📄 `supabase/functions/submit-lead/index.ts`

```ts
import { serve } from "https://deno.land/std@0.168.0/http/server.ts";

const corsHeaders = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Headers":
    "authorization, x-client-info, apikey, content-type, x-supabase-client-platform, x-supabase-client-platform-version, x-supabase-client-runtime, x-supabase-client-runtime-version",
};

serve(async (req) => {
  if (req.method === "OPTIONS") {
    return new Response("ok", { headers: corsHeaders });
  }

  try {
    const { nome, email, telefone, empresa, descricao, pagina } = await req.json();

    if (!nome || !email || !telefone || !empresa) {
      console.error("Missing required fields:", { nome: !!nome, email: !!email, telefone: !!telefone, empresa: !!empresa });
      return new Response(
        JSON.stringify({ error: "Campos obrigatórios não preenchidos." }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
      console.error("Invalid email format:", email);
      return new Response(
        JSON.stringify({ error: "Email inválido." }),
        { status: 400, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    const webhookUrl = Deno.env.get("N8N_WEBHOOK_URL");
    if (!webhookUrl) {
      console.error("N8N_WEBHOOK_URL secret is not configured");
      return new Response(
        JSON.stringify({ error: "Webhook não configurado." }),
        { status: 500, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    const payload = {
      nome: String(nome).slice(0, 100),
      email: String(email).slice(0, 255),
      telefone: String(telefone).slice(0, 20),
      empresa: String(empresa).slice(0, 100),
      descricao_operacao: String(descricao || "").slice(0, 1000),
      origem: "Site Evollure",
      pagina: String(pagina || "").slice(0, 500),
      timestamp: new Date().toISOString(),
    };

    console.log("Sending lead to webhook:", { nome: payload.nome, email: payload.email, empresa: payload.empresa });

    const webhookResponse = await fetch(webhookUrl, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(payload),
    });

    if (!webhookResponse.ok) {
      const errorText = await webhookResponse.text();
      console.error("Webhook error:", webhookResponse.status, errorText);
      return new Response(
        JSON.stringify({ error: "Erro ao processar formulário." }),
        { status: 502, headers: { ...corsHeaders, "Content-Type": "application/json" } }
      );
    }

    console.log("Lead submitted successfully:", payload.email);

    return new Response(
      JSON.stringify({ success: true }),
      { status: 200, headers: { ...corsHeaders, "Content-Type": "application/json" } }
    );
  } catch (err) {
    console.error("submit-lead error:", err);
    return new Response(
      JSON.stringify({ error: "Erro interno do servidor." }),
      { status: 500, headers: { ...corsHeaders, "Content-Type": "application/json" } }
    );
  }
});
```
