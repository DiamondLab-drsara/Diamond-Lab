import { useState, useEffect, useRef } from "react";
import { Diamond, Heart, ShoppingBag, Globe, Menu, X, ChevronDown, ArrowRight, MapPin, Instagram, Phone, Mail, Star, Award, Microscope, Sparkles } from "lucide-react";

const COLORS = {
  emerald: "#032B1D",
  emeraldMid: "#054D33",
  emeraldLight: "#0A6644",
  gold: "#C9A055",
  goldLight: "#E2C27D",
  goldPale: "#F5E6C8",
  ivory: "#FAF7F2",
  white: "#FFFFFF",
  charcoal: "#1A1A1A",
};

const products = [
  {
    id: 1,
    name: "The Quintet Band",
    arabic: "خاتم الخماسي",
    specs: ["1.5 total carats", "5 perfectly matched round diamonds", "18K white gold"],
    tag: "BESTSELLER",
    accent: "white",
    shape: "band",
  },
  {
    id: 2,
    name: "The Celestial Halo",
    arabic: "هالة سماوية",
    specs: ["1-carat round-cut center", "~0.25-carat halo", "18K white gold"],
    tag: "NEW",
    accent: "white",
    shape: "halo",
  },
  {
    id: 3,
    name: "The Gilded Cushion",
    arabic: "الوسادة المذهبة",
    specs: ["1-carat cushion-cut center", "~0.25-carat halo", "18K yellow gold"],
    tag: "FEATURED",
    accent: "gold",
    shape: "cushion",
  },
  {
    id: 4,
    name: "The Golden Solitaire",
    arabic: "سوليتير ذهبي",
    specs: ["1-carat round-cut diamond", "18K yellow gold"],
    tag: null,
    accent: "gold",
    shape: "solitaire",
  },
  {
    id: 5,
    name: "The Pure Solitaire",
    arabic: "السوليتير النقي",
    specs: ["1-carat round-cut diamond", "18K white gold"],
    tag: null,
    accent: "white",
    shape: "solitaire",
  },
];

const pillars = [
  {
    icon: Microscope,
    title: "Lab-Grown vs Natural",
    arabic: "مخبري VS طبيعي",
    desc: "Chemically identical to mined diamonds — grown in controlled environments with zero compromises on brilliance, hardness, or beauty. Certified by IGI.",
    stat: "100% Identical",
    statLabel: "Chemical Structure",
  },
  {
    icon: Sparkles,
    title: "Diamond vs Moissanite",
    arabic: "الماس VS موزنايت",
    desc: "Moissanite differs in refractive index, hardness, and origin. A true diamond — lab or natural — is a 10 on the Mohs scale. Science doesn't compromise.",
    stat: "10 / 10",
    statLabel: "Mohs Hardness",
  },
  {
    icon: Star,
    title: "The Perfect Solitaire",
    arabic: "السوليتير المثالي",
    desc: "One stone, one statement. The solitaire is the truest expression of a diamond's brilliance. We guide every client to their forever piece.",
    stat: "IGI",
    statLabel: "Certified",
  },
];

function DiamondIcon({ size = 24, color = COLORS.gold, className = "" }) {
  return (
    <svg width={size} height={size} viewBox="0 0 24 24" fill="none" className={className}>
      <path d="M12 2L3 9l9 13 9-13z" stroke={color} strokeWidth="1.2" fill="none" />
      <path d="M3 9h18M8 9L12 2l4 7" stroke={color} strokeWidth="1.2" />
    </svg>
  );
}

function ArtDecoCorner({ className = "" }) {
  return (
    <svg width="40" height="40" viewBox="0 0 40 40" fill="none" className={className}>
      <path d="M2 2h36v36H2z" stroke={COLORS.gold} strokeWidth="0.8" opacity="0.4" />
      <path d="M6 2v6M2 6h6" stroke={COLORS.gold} strokeWidth="1.2" />
    </svg>
  );
}

function RingVisual({ shape, accent }) {
  const isGold = accent === "gold";
  const metalColor = isGold ? COLORS.gold : "#E8E8EC";
  const metalDark = isGold ? "#A87830" : "#C0C0C8";

  const renderShape = () => {
    if (shape === "band") {
      return (
        <g>
          {[...Array(5)].map((_, i) => (
            <ellipse key={i} cx={20 + (i - 2) * 16} cy="50" rx="10" ry="10" fill={metalColor} stroke={metalDark} strokeWidth="1" />
          ))}
          <rect x="8" y="54" width="64" height="8" rx="4" fill={metalDark} />
        </g>
      );
    }
    if (shape === "halo") {
      return (
        <g>
          <ellipse cx="40" cy="42" rx="18" ry="18" fill={metalColor} stroke={metalDark} strokeWidth="1.5" />
          <ellipse cx="40" cy="42" rx="10" ry="10" fill="white" stroke={metalDark} strokeWidth="1" opacity="0.9" />
          {[...Array(12)].map((_, i) => {
            const angle = (i * 30 * Math.PI) / 180;
            return <circle key={i} cx={40 + 16 * Math.cos(angle)} cy={42 + 16 * Math.sin(angle)} r="3.5" fill={metalColor} stroke={metalDark} strokeWidth="0.8" />;
          })}
          <path d="M30 60 Q40 78 50 60" stroke={metalDark} strokeWidth="5" fill="none" strokeLinecap="round" />
        </g>
      );
    }
    if (shape === "cushion") {
      return (
        <g>
          <rect x="20" y="22" width="40" height="40" rx="10" fill={metalColor} stroke={metalDark} strokeWidth="1.5" />
          <rect x="26" y="28" width="28" height="28" rx="6" fill="white" stroke={metalDark} strokeWidth="0.8" opacity="0.9" />
          {[...Array(8)].map((_, i) => {
            const angle = (i * 45 * Math.PI) / 180;
            return <circle key={i} cx={40 + 22 * Math.cos(angle)} cy={42 + 22 * Math.sin(angle)} r="3" fill={metalColor} stroke={metalDark} strokeWidth="0.8" />;
          })}
          <path d="M28 62 Q40 80 52 62" stroke={metalDark} strokeWidth="5" fill="none" strokeLinecap="round" />
        </g>
      );
    }
    return (
      <g>
        <ellipse cx="40" cy="40" rx="18" ry="18" fill={metalColor} stroke={metalDark} strokeWidth="1.5" />
        <ellipse cx="40" cy="40" rx="11" ry="11" fill="white" stroke={metalDark} strokeWidth="0.8" opacity="0.9" />
        <path d="M30 58 Q40 76 50 58" stroke={metalDark} strokeWidth="5" fill="none" strokeLinecap="round" />
      </g>
    );
  };

  return (
    <svg viewBox="0 0 80 80" fill="none" className="w-full h-full">
      <defs>
        <radialGradient id={`shine-${accent}-${shape}`} cx="40%" cy="35%" r="55%">
          <stop offset="0%" stopColor="white" stopOpacity="0.8" />
          <stop offset="60%" stopColor={metalColor} stopOpacity="0.2" />
          <stop offset="100%" stopColor={metalDark} stopOpacity="0" />
        </radialGradient>
      </defs>
      {renderShape()}
      <ellipse cx="40" cy={shape === "band" ? "42" : "38"} rx="12" ry="8" fill={`url(#shine-${accent}-${shape})`} />
    </svg>
  );
}

export default function DiamondLabPage() {
  const [menuOpen, setMenuOpen] = useState(false);
  const [lang, setLang] = useState("EN");
  const [wishlist, setWishlist] = useState([]);
  const [activeCard, setActiveCard] = useState(null);
  const [scrolled, setScrolled] = useState(false);
  const heroRef = useRef(null);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 60);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  const toggleWishlist = (id) =>
    setWishlist((w) => (w.includes(id) ? w.filter((x) => x !== id) : [...w, id]));

  return (
    <div style={{ fontFamily: "'Georgia', serif", backgroundColor: COLORS.ivory, color: COLORS.charcoal }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Jost:wght@300;400;500&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Jost', sans-serif; }
        .font-display { font-family: 'Cormorant Garamond', serif; }
        .font-body { font-family: 'Jost', sans-serif; }
        .gold-text { color: ${COLORS.gold}; }
        .gold-border { border-color: ${COLORS.gold}; }
        .nav-link { font-family: 'Jost', sans-serif; font-size: 12px; letter-spacing: 0.18em; text-transform: uppercase; color: ${COLORS.goldPale}; opacity: 0.8; transition: opacity 0.2s; cursor: pointer; }
        .nav-link:hover { opacity: 1; color: ${COLORS.gold}; }
        .btn-gold { background: transparent; border: 1px solid ${COLORS.gold}; color: ${COLORS.gold}; font-family: 'Jost', sans-serif; font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase; padding: 14px 32px; cursor: pointer; transition: all 0.3s; }
        .btn-gold:hover { background: ${COLORS.gold}; color: ${COLORS.emerald}; }
        .btn-solid { background: ${COLORS.gold}; border: 1px solid ${COLORS.gold}; color: ${COLORS.emerald}; font-family: 'Jost', sans-serif; font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase; padding: 14px 32px; cursor: pointer; transition: all 0.3s; font-weight: 500; }
        .btn-solid:hover { background: ${COLORS.goldLight}; }
        .product-card { transition: transform 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94), box-shadow 0.4s; cursor: pointer; }
        .product-card:hover { transform: translateY(-8px); box-shadow: 0 24px 60px rgba(0,0,0,0.15); }
        .pillar-card { transition: transform 0.3s, background 0.3s; cursor: default; }
        .pillar-card:hover { transform: translateY(-4px); }
        .deco-line::before { content:''; display:block; width:40px; height:1px; background:${COLORS.gold}; opacity:0.6; margin-bottom:16px; }
        .shimmer { position: relative; overflow: hidden; }
        .shimmer::after { content:''; position:absolute; inset:0; background: linear-gradient(105deg, transparent 30%, rgba(255,255,255,0.12) 50%, transparent 70%); transform: translateX(-100%); transition: transform 0.8s; }
        .shimmer:hover::after { transform: translateX(100%); }
        .form-input { font-family: 'Jost', sans-serif; font-size: 13px; letter-spacing: 0.05em; background: transparent; border: none; border-bottom: 1px solid rgba(201,160,85,0.35); padding: 12px 0; width: 100%; color: ${COLORS.goldPale}; outline: none; transition: border-color 0.3s; }
        .form-input::placeholder { color: rgba(245,230,200,0.4); }
        .form-input:focus { border-bottom-color: ${COLORS.gold}; }
        .scrollbar-hide::-webkit-scrollbar { display: none; }
        @keyframes fadeUp { from { opacity:0; transform:translateY(30px); } to { opacity:1; transform:translateY(0); } }
        @keyframes shimmerBg { 0%,100% { opacity:0.6; } 50% { opacity:1; } }
        .animate-fade-up { animation: fadeUp 0.8s ease forwards; }
        .delay-1 { animation-delay: 0.15s; opacity:0; }
        .delay-2 { animation-delay: 0.3s; opacity:0; }
        .delay-3 { animation-delay: 0.45s; opacity:0; }
        .tag-badge { font-family:'Jost',sans-serif; font-size:9px; letter-spacing:0.2em; text-transform:uppercase; }
        hr.gold-divider { border:none; border-top:1px solid rgba(201,160,85,0.25); }
        .sparkle { display:inline-block; animation: shimmerBg 3s ease-in-out infinite; }
      `}</style>

      {/* ─── NAV ─── */}
      <nav
        style={{
          position: "fixed", top: 0, left: 0, right: 0, zIndex: 100,
          background: scrolled ? `rgba(3,43,29,0.97)` : "transparent",
          backdropFilter: scrolled ? "blur(12px)" : "none",
          borderBottom: scrolled ? `1px solid rgba(201,160,85,0.2)` : "none",
          transition: "all 0.4s",
          padding: "0 40px",
        }}
      >
        <div style={{ maxWidth: 1280, margin: "0 auto", display: "flex", alignItems: "center", height: 72, gap: 32 }}>
          {/* Logo */}
          <div style={{ display: "flex", alignItems: "center", gap: 10, flex: "0 0 auto" }}>
            <DiamondIcon size={20} />
            <div>
              <div style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 18, letterSpacing: "0.22em", color: COLORS.goldLight, fontWeight: 500, lineHeight: 1 }}>DIAMOND LAB</div>
              <div style={{ fontFamily: "'Jost', sans-serif", fontSize: 9, letterSpacing: "0.25em", color: COLORS.gold, opacity: 0.7 }}>BY DR. SARA</div>
            </div>
          </div>

          {/* Center links */}
          <div style={{ display: "flex", gap: 36, flex: 1, justifyContent: "center", display: menuOpen ? "none" : "flex" }} className="hidden-mobile">
            {["Collections", "The Science", "Custom Jewelry", "Contact"].map((l) => (
              <span key={l} className="nav-link">{l}</span>
            ))}
          </div>

          {/* Right icons */}
          <div style={{ display: "flex", alignItems: "center", gap: 20, marginLeft: "auto", flex: "0 0 auto" }}>
            <button onClick={() => setLang(l => l === "EN" ? "AR" : "EN")} style={{ background: "none", border: `1px solid rgba(201,160,85,0.4)`, color: COLORS.gold, fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.15em", padding: "5px 10px", cursor: "pointer" }}>
              {lang === "EN" ? "EN | AR" : "AR | EN"}
            </button>
            <button style={{ background: "none", border: "none", cursor: "pointer", color: COLORS.goldLight, opacity: 0.8, display: "flex" }}>
              <Heart size={18} />
              {wishlist.length > 0 && (
                <span style={{ background: COLORS.gold, color: COLORS.emerald, fontSize: 9, borderRadius: "50%", width: 14, height: 14, display: "flex", alignItems: "center", justifyContent: "center", marginLeft: -8, marginTop: -4 }}>{wishlist.length}</span>
              )}
            </button>
            <button style={{ background: "none", border: "none", cursor: "pointer", color: COLORS.goldLight, opacity: 0.8 }}>
              <ShoppingBag size={18} />
            </button>
            <button onClick={() => setMenuOpen(o => !o)} style={{ background: "none", border: "none", cursor: "pointer", color: COLORS.goldLight }}>
              {menuOpen ? <X size={20} /> : <Menu size={20} />}
            </button>
          </div>
        </div>

        {/* Mobile/Hamburger menu */}
        {menuOpen && (
          <div style={{ background: COLORS.emerald, borderTop: `1px solid rgba(201,160,85,0.2)`, padding: "24px 40px 32px" }}>
            {["Collections", "The Science", "Custom Jewelry", "Contact"].map((l) => (
              <div key={l} style={{ padding: "12px 0", borderBottom: `1px solid rgba(201,160,85,0.1)` }}>
                <span className="nav-link" style={{ fontSize: 13 }}>{l}</span>
              </div>
            ))}
          </div>
        )}
      </nav>

      {/* ─── HERO ─── */}
      <section ref={heroRef} style={{ background: `linear-gradient(145deg, #021A11 0%, ${COLORS.emerald} 45%, #054830 100%)`, minHeight: "100vh", display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center", position: "relative", overflow: "hidden", padding: "120px 40px 80px" }}>
        {/* Decorative background grid lines */}
        <div style={{ position: "absolute", inset: 0, backgroundImage: `linear-gradient(rgba(201,160,85,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(201,160,85,0.04) 1px, transparent 1px)`, backgroundSize: "80px 80px" }} />

        {/* Art deco corner ornaments */}
        <div style={{ position: "absolute", top: 90, left: 40, opacity: 0.5 }}>
          <ArtDecoCorner />
        </div>
        <div style={{ position: "absolute", top: 90, right: 40, opacity: 0.5, transform: "scaleX(-1)" }}>
          <ArtDecoCorner />
        </div>
        <div style={{ position: "absolute", bottom: 60, left: 40, opacity: 0.5, transform: "scaleY(-1)" }}>
          <ArtDecoCorner />
        </div>
        <div style={{ position: "absolute", bottom: 60, right: 40, opacity: 0.5, transform: "scale(-1,-1)" }}>
          <ArtDecoCorner />
        </div>

        {/* Glowing orb background */}
        <div style={{ position: "absolute", width: 500, height: 500, borderRadius: "50%", background: "radial-gradient(circle, rgba(201,160,85,0.08) 0%, transparent 70%)", top: "50%", left: "50%", transform: "translate(-50%,-50%)" }} />

        {/* Content */}
        <div style={{ textAlign: "center", maxWidth: 780, position: "relative", zIndex: 2 }}>
          <div className="animate-fade-up" style={{ marginBottom: 20 }}>
            <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.4em", textTransform: "uppercase", color: COLORS.gold, borderTop: `1px solid ${COLORS.gold}`, borderBottom: `1px solid ${COLORS.gold}`, padding: "6px 20px", opacity: 0.9 }}>
              IGI Certified · Damascus, Syria
            </span>
          </div>

          <h1 className="animate-fade-up delay-1" style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: "clamp(44px, 8vw, 88px)", fontWeight: 300, lineHeight: 1.05, letterSpacing: "0.06em", color: COLORS.ivory, marginBottom: 8 }}>
            LUXURY MADE<br />
            <em style={{ color: COLORS.goldLight, fontStyle: "italic", fontWeight: 300 }}>BY SCIENCE</em>
          </h1>

          <p className="animate-fade-up delay-2" style={{ fontFamily: "'Jost',sans-serif", fontSize: 14, letterSpacing: "0.12em", color: COLORS.goldPale, opacity: 0.75, maxWidth: 520, margin: "24px auto 40px", lineHeight: 1.8 }}>
            IGI Certified Lab-Grown Diamonds & Custom Fine Jewelry<br />curated by <em style={{ color: COLORS.gold, opacity: 1, fontStyle: "normal" }}>Dr. Sara</em>
          </p>

          <div className="animate-fade-up delay-3" style={{ display: "flex", gap: 16, justifyContent: "center", flexWrap: "wrap" }}>
            <button className="btn-solid shimmer">Explore Collections</button>
            <button className="btn-gold">Book a Consultation</button>
          </div>

          {/* Scroll indicator */}
          <div style={{ marginTop: 64, display: "flex", flexDirection: "column", alignItems: "center", gap: 8, opacity: 0.4 }}>
            <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.3em", color: COLORS.goldLight }}>SCROLL</span>
            <ChevronDown size={14} color={COLORS.gold} />
          </div>
        </div>
      </section>

      {/* ─── TRUST BAR ─── */}
      <div style={{ background: COLORS.charcoal, borderTop: `1px solid rgba(201,160,85,0.2)`, borderBottom: `1px solid rgba(201,160,85,0.2)` }}>
        <div style={{ maxWidth: 1280, margin: "0 auto", display: "flex", justifyContent: "space-around", flexWrap: "wrap", padding: "18px 40px" }}>
          {[
            { icon: Award, text: "IGI Certified" },
            { icon: Microscope, text: "Lab-Grown Science" },
            { icon: Star, text: "Custom Fine Jewelry" },
            { icon: Diamond, text: "Ethically Sourced" },
          ].map(({ icon: Icon, text }) => (
            <div key={text} style={{ display: "flex", alignItems: "center", gap: 8, padding: "6px 12px" }}>
              <Icon size={13} color={COLORS.gold} />
              <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.22em", textTransform: "uppercase", color: COLORS.goldPale, opacity: 0.7 }}>{text}</span>
            </div>
          ))}
        </div>
      </div>

      {/* ─── EDUCATION PILLARS ─── */}
      <section style={{ background: COLORS.ivory, padding: "100px 40px" }}>
        <div style={{ maxWidth: 1280, margin: "0 auto" }}>
          <div style={{ textAlign: "center", marginBottom: 64 }}>
            <div className="deco-line" style={{ display: "flex", justifyContent: "center" }} />
            <h2 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: "clamp(32px,5vw,52px)", fontWeight: 300, letterSpacing: "0.04em", color: COLORS.emerald, marginBottom: 12 }}>
              Knowledge is <em>Clarity</em>
            </h2>
            <p style={{ fontFamily: "'Jost',sans-serif", fontSize: 13, letterSpacing: "0.08em", color: COLORS.charcoal, opacity: 0.55, maxWidth: 460, margin: "0 auto" }}>
              An educated client is our greatest achievement. Understand what you're wearing.
            </p>
          </div>

          <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(280px, 1fr))", gap: 2 }}>
            {pillars.map((p, i) => {
              const Icon = p.icon;
              return (
                <div key={i} className="pillar-card" style={{ background: i === 1 ? COLORS.emerald : COLORS.white, padding: "48px 36px", border: `1px solid rgba(3,43,29,0.08)` }}>
                  <div style={{ marginBottom: 24 }}>
                    <Icon size={22} color={i === 1 ? COLORS.gold : COLORS.emerald} />
                  </div>
                  <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.3em", textTransform: "uppercase", color: i === 1 ? COLORS.gold : COLORS.emerald, opacity: 0.7, marginBottom: 8 }}>
                    {p.arabic}
                  </div>
                  <h3 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 26, fontWeight: 400, letterSpacing: "0.02em", color: i === 1 ? COLORS.goldLight : COLORS.emerald, marginBottom: 16, lineHeight: 1.2 }}>
                    {p.title}
                  </h3>
                  <p style={{ fontFamily: "'Jost',sans-serif", fontSize: 13, lineHeight: 1.8, color: i === 1 ? "rgba(245,230,200,0.7)" : "rgba(26,26,26,0.6)", marginBottom: 28 }}>
                    {p.desc}
                  </p>
                  <hr className="gold-divider" style={{ marginBottom: 24 }} />
                  <div>
                    <div style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 32, fontWeight: 300, color: i === 1 ? COLORS.gold : COLORS.emerald, lineHeight: 1 }}>
                      {p.stat}
                    </div>
                    <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.2em", textTransform: "uppercase", color: i === 1 ? COLORS.goldPale : COLORS.charcoal, opacity: 0.5, marginTop: 4 }}>
                      {p.statLabel}
                    </div>
                  </div>
                </div>
              );
            })}
          </div>
        </div>
      </section>

      {/* ─── COLLECTION ─── */}
      <section style={{ background: "#F2EDE4", padding: "100px 40px" }}>
        <div style={{ maxWidth: 1280, margin: "0 auto" }}>
          <div style={{ textAlign: "center", marginBottom: 64 }}>
            <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.35em", textTransform: "uppercase", color: COLORS.gold, marginBottom: 14, display: "flex", alignItems: "center", justifyContent: "center", gap: 12 }}>
              <span style={{ display: "block", width: 28, height: "1px", background: COLORS.gold, opacity: 0.5 }} />
              Featured Collection
              <span style={{ display: "block", width: 28, height: "1px", background: COLORS.gold, opacity: 0.5 }} />
            </div>
            <h2 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: "clamp(32px,5vw,52px)", fontWeight: 300, letterSpacing: "0.04em", color: COLORS.emerald }}>
              Curated <em>Pieces</em>
            </h2>
          </div>

          <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(260px, 1fr))", gap: 24 }}>
            {products.map((p) => {
              const isWishlisted = wishlist.includes(p.id);
              const isActive = activeCard === p.id;
              return (
                <div
                  key={p.id}
                  className="product-card shimmer"
                  onMouseEnter={() => setActiveCard(p.id)}
                  onMouseLeave={() => setActiveCard(null)}
                  style={{ background: COLORS.white, border: `1px solid rgba(3,43,29,0.08)`, position: "relative", overflow: "hidden" }}
                >
                  {/* Tag */}
                  {p.tag && (
                    <div className="tag-badge" style={{ position: "absolute", top: 16, left: 16, background: p.accent === "gold" ? COLORS.gold : COLORS.emerald, color: p.accent === "gold" ? COLORS.emerald : COLORS.goldLight, padding: "4px 10px", zIndex: 3, letterSpacing: "0.2em" }}>
                      {p.tag}
                    </div>
                  )}

                  {/* Wishlist */}
                  <button
                    onClick={() => toggleWishlist(p.id)}
                    style={{ position: "absolute", top: 14, right: 14, background: "none", border: "none", cursor: "pointer", zIndex: 3, color: isWishlisted ? COLORS.gold : "rgba(3,43,29,0.3)", transition: "color 0.3s" }}
                  >
                    <Heart size={16} fill={isWishlisted ? COLORS.gold : "none"} />
                  </button>

                  {/* Ring Visual */}
                  <div style={{ background: isActive ? COLORS.emerald : "#F9F5EE", height: 200, display: "flex", alignItems: "center", justifyContent: "center", transition: "background 0.4s", position: "relative" }}>
                    <div style={{ position: "absolute", inset: 0, backgroundImage: isActive ? `radial-gradient(circle at 30% 30%, rgba(201,160,85,0.08), transparent 60%)` : "none" }} />
                    <div style={{ width: 120, height: 120, position: "relative", zIndex: 2 }}>
                      <RingVisual shape={p.shape} accent={p.accent} />
                    </div>
                  </div>

                  {/* Card body */}
                  <div style={{ padding: "24px 24px 28px" }}>
                    <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.3em", textTransform: "uppercase", color: COLORS.gold, opacity: 0.7, marginBottom: 6 }}>
                      {p.arabic}
                    </div>
                    <h3 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 22, fontWeight: 400, color: COLORS.emerald, marginBottom: 16, letterSpacing: "0.01em" }}>
                      {p.name}
                    </h3>
                    <hr className="gold-divider" style={{ marginBottom: 16 }} />
                    <ul style={{ listStyle: "none", padding: 0, marginBottom: 24 }}>
                      {p.specs.map((s, i) => (
                        <li key={i} style={{ fontFamily: "'Jost',sans-serif", fontSize: 11, letterSpacing: "0.06em", color: "rgba(26,26,26,0.55)", padding: "4px 0", display: "flex", alignItems: "center", gap: 6 }}>
                          <span style={{ width: 4, height: 4, borderRadius: "50%", background: COLORS.gold, opacity: 0.6, flexShrink: 0 }} />
                          {s}
                        </li>
                      ))}
                    </ul>
                    <button className="btn-gold" style={{ width: "100%", display: "flex", alignItems: "center", justifyContent: "center", gap: 8 }}>
                      View Details <ArrowRight size={12} />
                    </button>
                  </div>
                </div>
              );
            })}
          </div>

          <div style={{ textAlign: "center", marginTop: 48 }}>
            <button className="btn-solid" style={{ display: "inline-flex", alignItems: "center", gap: 8 }}>
              View All Pieces <ArrowRight size={12} />
            </button>
          </div>
        </div>
      </section>

      {/* ─── CUSTOM JEWELRY BANNER ─── */}
      <section style={{ background: `linear-gradient(135deg, #021811 0%, ${COLORS.emerald} 50%, #031E12 100%)`, padding: "90px 40px", position: "relative", overflow: "hidden" }}>
        <div style={{ position: "absolute", inset: 0, backgroundImage: `radial-gradient(circle at 80% 50%, rgba(201,160,85,0.06) 0%, transparent 60%)` }} />
        <div style={{ maxWidth: 800, margin: "0 auto", textAlign: "center", position: "relative", zIndex: 2 }}>
          <DiamondIcon size={28} className="sparkle" style={{ margin: "0 auto 20px" }} />
          <h2 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: "clamp(28px,5vw,52px)", fontWeight: 300, color: COLORS.ivory, letterSpacing: "0.05em", marginBottom: 16 }}>
            Your Vision, <em style={{ color: COLORS.goldLight }}>Crafted in Science</em>
          </h2>
          <p style={{ fontFamily: "'Jost',sans-serif", fontSize: 13, letterSpacing: "0.1em", color: COLORS.goldPale, opacity: 0.65, maxWidth: 500, margin: "0 auto 36px", lineHeight: 1.8 }}>
            Every Diamond Lab creation begins with a conversation. We translate your vision into certified fine jewelry — designed precisely for you.
          </p>
          <button className="btn-gold">Begin Your Custom Journey</button>
        </div>
      </section>

      {/* ─── CONTACT & FOOTER ─── */}
      <section style={{ background: COLORS.emerald, padding: "80px 40px 0" }}>
        <div style={{ maxWidth: 1280, margin: "0 auto" }}>
          <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(280px, 1fr))", gap: 60, paddingBottom: 64 }}>
            {/* Brand col */}
            <div>
              <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 20 }}>
                <DiamondIcon size={18} />
                <div>
                  <div style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 17, letterSpacing: "0.2em", color: COLORS.goldLight, fontWeight: 500 }}>DIAMOND LAB</div>
                  <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.22em", color: COLORS.gold, opacity: 0.6 }}>BY DR. SARA</div>
                </div>
              </div>
              <p style={{ fontFamily: "'Jost',sans-serif", fontSize: 12, lineHeight: 1.9, color: COLORS.goldPale, opacity: 0.55, maxWidth: 260, marginBottom: 24 }}>
                Luxury made by science. IGI-certified lab-grown diamonds and custom fine jewelry, curated from Damascus with love.
              </p>
              <div style={{ display: "flex", gap: 12 }}>
                <a href="https://instagram.com/diamond.lab.official" target="_blank" rel="noreferrer" style={{ display: "flex", alignItems: "center", gap: 6, fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.15em", color: COLORS.gold, textDecoration: "none", opacity: 0.8, border: `1px solid rgba(201,160,85,0.3)`, padding: "8px 14px", transition: "opacity 0.2s" }}>
                  <Instagram size={12} /> @diamond.lab.official
                </a>
              </div>
            </div>

            {/* Location col */}
            <div>
              <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.3em", textTransform: "uppercase", color: COLORS.gold, opacity: 0.6, marginBottom: 20 }}>
                Find Us
              </div>
              <div style={{ display: "flex", gap: 10, marginBottom: 12, alignItems: "flex-start" }}>
                <MapPin size={14} color={COLORS.gold} style={{ flexShrink: 0, marginTop: 2 }} />
                <div>
                  <div style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 16, color: COLORS.goldLight, marginBottom: 4 }}>Damascus, Syria</div>
                  <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 11, color: COLORS.goldPale, opacity: 0.5, letterSpacing: "0.06em", lineHeight: 1.6 }}>
                    Al-Jisr Al-Abiad — Nouri Pasha<br />
                    الجسر الأبيض — نوري باشا
                  </div>
                </div>
              </div>
              <hr className="gold-divider" style={{ margin: "20px 0" }} />
              <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
                <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                  <Phone size={12} color={COLORS.gold} />
                  <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 11, color: COLORS.goldPale, opacity: 0.55, letterSpacing: "0.08em" }}>Available via Instagram DM</span>
                </div>
                <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
                  <Instagram size={12} color={COLORS.gold} />
                  <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 11, color: COLORS.goldPale, opacity: 0.55, letterSpacing: "0.08em" }}>@diamond.lab.official</span>
                </div>
              </div>
            </div>

            {/* Inquiry form */}
            <div>
              <div style={{ fontFamily: "'Jost',sans-serif", fontSize: 9, letterSpacing: "0.3em", textTransform: "uppercase", color: COLORS.gold, opacity: 0.6, marginBottom: 20 }}>
                Custom Inquiry
              </div>
              <h3 style={{ fontFamily: "'Cormorant Garamond', serif", fontSize: 22, fontWeight: 300, color: COLORS.goldLight, marginBottom: 24, lineHeight: 1.3 }}>
                Request a <em>Custom Piece</em>
              </h3>
              <div style={{ display: "flex", flexDirection: "column", gap: 20 }}>
                <input className="form-input" type="text" placeholder="Your Name" />
                <input className="form-input" type="text" placeholder="Phone / Instagram" />
                <textarea className="form-input" placeholder="Describe your dream piece..." rows={3} style={{ resize: "none", borderBottom: "1px solid rgba(201,160,85,0.35)" }} />
                <button className="btn-gold" style={{ alignSelf: "flex-start", display: "flex", alignItems: "center", gap: 8 }}>
                  Send Inquiry <ArrowRight size={12} />
                </button>
              </div>
            </div>
          </div>

          {/* Footer bar */}
          <div style={{ borderTop: `1px solid rgba(201,160,85,0.15)`, padding: "20px 0", display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: 12 }}>
            <span style={{ fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.12em", color: COLORS.goldPale, opacity: 0.35 }}>
              © 2025 Diamond Lab by Dr. Sara. All rights reserved.
            </span>
            <div style={{ display: "flex", gap: 24 }}>
              {["Privacy Policy", "Terms", "IGI Certification"].map((l) => (
                <span key={l} style={{ fontFamily: "'Jost',sans-serif", fontSize: 10, letterSpacing: "0.12em", color: COLORS.goldPale, opacity: 0.35, cursor: "pointer" }}>{l}</span>
              ))}
            </div>
          </div>
        </div>
      </section>
    </div>
  );
}
