# soundboxrecords[Uploading index.html…]()

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KIM*C | Official Artist Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@200;400;700&family=Inter:wght@300;400;700;900&display=swap" rel="stylesheet">
    <style>
        .oswald { font-family: 'Oswald', sans-serif; }
        body { font-family: 'Inter', sans-serif; }
        @keyframes spin-slow {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .animate-spin-slow {
            animation: spin-slow 8s linear infinite;
        }
        @keyframes marquee {
          0% { transform: translateX(0); }import React, { useState, useRef, useEffect } from 'react';
import Header from './components/Header';
import CartDrawer from './components/CartDrawer';
import CheckoutModal from './components/CheckoutModal';
import LyricGenerator from './components/LyricGenerator';
import { PRODUCTS, SOCIAL_LINKS } from './constants';
import { Product, CartItem } from './types';
import { 
  Instagram, Facebook, Youtube, Music, ArrowRight, Play, Pause, ExternalLink, 
  Disc, Mic2, Settings2, Headphones, Phone, Mail, Sparkles, Quote, 
  Camera, ZoomIn, Star, Share2, ShoppingCart, ChevronLeft, CreditCard, MailCheck
} from 'lucide-react';

const AnnouncementBar = () => (
  <div className="bg-red-600 text-white py-2 overflow-hidden whitespace-nowrap border-b border-red-700">
    <div className="flex animate-marquee">
      {[...Array(10)].map((_, i) => (
        <span key={i} className="oswald font-black uppercase tracking-[0.3em] text-[10px] mx-12">
          NEW DROP: 2025 MASTERS "MBIGATAMU NGA TEBIWERA" OUT NOW — "IT'S OK" ALBUM AVAILABLE IN THE VAULT — BEXX NATION GEAR RESTOCKED —
        </span>
      ))}
    </div>
  </div>
);

const AudioSample: React.FC<{ url?: string }> = ({ url }) => {
  const [isPlaying, setIsPlaying] = useState(false);
  const audioRef = useRef<HTMLAudioElement | null>(null);

  if (!url) return null;

  const toggle = (e: React.MouseEvent) => {
    e.stopPropagation();
    if (isPlaying) {
      audioRef.current?.pause();
    } else {
      audioRef.current?.play();
    }
    setIsPlaying(!isPlaying);
  };

  return (
    <div className="absolute top-4 left-4 z-20">
      <audio ref={audioRef} src={url} onEnded={() => setIsPlaying(false)} />
      <button 
        onClick={toggle}
        className="bg-black text-white p-3 rounded-none shadow-xl hover:bg-red-600 transition-colors flex items-center justify-center border border-white/20"
        title={isPlaying ? "Pause Sample" : "Play Sample"}
      >
        {isPlaying ? <Pause size={14} fill="currentColor" /> : <Play size={14} fill="currentColor" className="ml-0.5" />}
      </button>
    </div>
  );
};

const Newsletter = () => (
  <section className="bg-black text-white py-32 border-t border-white/10">
    <div className="max-w-4xl mx-auto px-6 text-center space-y-12">
      <div className="space-y-4">
        <h2 className="oswald text-5xl md:text-7xl font-black uppercase tracking-tighter italic">JOIN THE NATION</h2>
        <p className="text-gray-500 font-bold uppercase tracking-[0.3em] text-xs">Be the first to know about new music and exclusive drops.</p>
      </div>
      <form className="flex flex-col md:flex-row gap-4 max-w-2xl mx-auto" onSubmit={(e) => e.preventDefault()}>
        <input 
          type="email" 
          placeholder="ENTER YOUR EMAIL" 
          className="flex-grow bg-white/5 border border-white/20 px-8 py-5 text-sm font-black uppercase tracking-widest focus:outline-none focus:border-red-600 transition-colors"
        />
        <button className="bg-white text-black px-12 py-5 font-black uppercase tracking-widest text-xs hover:bg-red-600 hover:text-white transition-all">
          SIGN UP
        </button>
      </form>
      <div className="flex items-center justify-center space-x-2 text-white/20">
        <MailCheck size={14} />
        <span className="text-[9px] font-black uppercase tracking-widest">NO SPAM. JUST BARS.</span>
      </div>
    </div>
  </section>
);

const HomePage: React.FC<{ onAddToCart: (p: Product) => void, onNavigate: (page: string) => void, onProductSelect: (p: Product) => void }> = ({ onAddToCart, onNavigate, onProductSelect }) => {
  const latestDrops = PRODUCTS.slice(0, 4);

  return (
    <div className="space-y-0 pb-0">
      <section className="relative h-screen bg-black overflow-hidden flex items-center justify-center">
        <video 
          autoPlay 
          muted 
          loop 
          playsInline
          className="absolute inset-0 w-full h-full object-cover opacity-60 grayscale"
        >
          <source src="https://assets.mixkit.co/videos/preview/mixkit-recording-studio-room-with-professional-equipment-43402-large.mp4" type="video/mp4" />
        </video>
        <div className="relative z-10 text-center text-white px-4 max-w-6xl">
          <div className="oswald text-xs font-black uppercase tracking-[0.6em] mb-8 text-red-600">SOUND BOX RECORDS PRESENTS</div>
          <h1 className="oswald text-[12vw] font-black uppercase tracking-tighter leading-[0.8] mb-12 select-none animate-in fade-in slide-in-from-bottom-12 duration-1000">
            KIM<span className="text-red-600 italic">*</span>C <br/> 2025
          </h1>
          <div className="flex flex-col md:flex-row items-center justify-center gap-6">
            <button 
              onClick={() => onNavigate('shop')}
              className="group bg-white text-black px-16 py-7 font-black uppercase tracking-[0.3em] text-xs hover:bg-red-600 hover:text-white transition-all flex items-center space-x-4 active:scale-95 shadow-2xl"
            >
              <span>ENTER THE VAULT</span>
              <ArrowRight size={20} />
            </button>
          </div>
        </div>
      </section>

      {/* Latest 2025/2024 Drops */}
      <section className="bg-white py-32 border-b border-gray-100">
        <div className="max-w-7xl mx-auto px-6 space-y-20">
          <div className="flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-8">
            <div className="space-y-2">
               <h2 className="oswald text-6xl font-black uppercase tracking-tighter">LATEST DROPS</h2>
               <p className="text-[10px] font-black uppercase tracking-[0.4em] text-gray-400">2024 - 2025 OFFICIAL RELEASES</p>
            </div>
            <button onClick={() => onNavigate('shop')} className="text-xs font-black uppercase tracking-widest hover:text-red-600 transition-colors mt-4 md:mt-0">VIEW ALL MASTERS</button>
          </div>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-12">
            {latestDrops.map(p => (
              <div key={p.id} className="group cursor-pointer" onClick={() => onProductSelect(p)}>
                <div className="relative aspect-square mb-6 overflow-hidden bg-gray-50 border border-gray-100 shadow-sm group-hover:shadow-2xl transition-all">
                  <img src={p.image} className="w-full h-full object-cover grayscale group-hover:grayscale-0 group-hover:scale-105 transition-all duration-700" alt={p.name} />
                  <div className="absolute top-4 right-4 bg-black text-white px-3 py-1 text-[9px] font-black uppercase tracking-widest">LATEST</div>
                </div>
                <h3 className="oswald text-xl font-black uppercase">{p.name}</h3>
                <p className="text-red-600 text-sm font-black tracking-widest">{p.price.toLocaleString()} UGX</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      <Newsletter />
    </div>
  );
};

const ProductDetailPage: React.FC<{ product: Product, onAddToCart: (p: Product) => void, onBuyNow: (p: Product) => void, onBack: () => void }> = ({ product, onAddToCart, onBuyNow, onBack }) => {
  return (
    <div className="max-w-7xl mx-auto px-6 pt-40 pb-32 min-h-screen">
      <button 
        onClick={onBack}
        className="flex items-center gap-2 text-xs font-black uppercase tracking-[0.2em] text-gray-400 hover:text-black transition-colors mb-16 group"
      >
        <ChevronLeft size={16} className="group-hover:-translate-x-1 transition-transform" />
        RETURN TO COLLECTION
      </button>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-20 lg:gap-32">
        <div className="relative aspect-square overflow-hidden bg-gray-50 border border-gray-100 shadow-2xl">
          <AudioSample url={product.audioUrl} />
          <img src={product.image} alt={product.name} className="w-full h-full object-cover" />
        </div>

        <div className="flex flex-col justify-center space-y-12">
          <div className="space-y-6">
            <div className="flex items-center gap-4">
              <span className="text-[10px] font-black uppercase tracking-widest px-3 py-1 bg-black text-white">OFFICIAL DROP</span>
              <span className="text-[10px] font-black uppercase tracking-widest text-red-600">{product.category}</span>
            </div>
            <h1 className="oswald text-7xl md:text-8xl font-black uppercase tracking-tighter leading-[0.85] italic">{product.name}</h1>
            <div className="h-1.5 w-32 bg-red-600" />
          </div>

          <div className="space-y-8">
            <p className="oswald text-5xl font-bold tracking-tight">{product.price.toLocaleString()} UGX</p>
            <p className="text-gray-500 text-lg leading-relaxed font-light italic max-w-md">{product.description}</p>
          </div>

          <div className="space-y-4 pt-4">
            <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <button 
                onClick={() => onAddToCart(product)}
                className="bg-black text-white py-7 font-black uppercase tracking-[0.3em] text-xs hover:bg-gray-800 transition-all flex items-center justify-center gap-4 active:scale-95"
              >
                <ShoppingCart size={18} />
                ADD TO CART
              </button>
              <button 
                onClick={() => onBuyNow(product)}
                className="bg-red-600 text-white py-7 font-black uppercase tracking-[0.3em] text-xs hover:bg-red-700 transition-all flex items-center justify-center gap-4 active:scale-95"
              >
                <CreditCard size={18} />
                BUY IT NOW
              </button>
            </div>
          </div>

          <div className="pt-16 border-t border-gray-100 grid grid-cols-2 gap-8">
             <div className="space-y-4">
               <p className="text-[10px] font-black uppercase tracking-widest text-black">DELIVERY & SHIPPING</p>
               <p className="text-[10px] font-medium text-gray-400 leading-relaxed uppercase tracking-widest">
                 DIGITAL GOODS DELIVERED INSTANTLY VIA EMAIL. PHYSICAL GOODS SHIP WITHIN 3-5 BUSINESS DAYS IN UGANDA.
               </p>
             </div>
             <div className="space-y-4 text-right">
               <p className="text-[10px] font-black uppercase tracking-widest text-black">SECURE CHECKOUT</p>
               <div className="flex justify-end gap-3 opacity-30 grayscale">
                  <CreditCard size={20} />
                  <ShoppingCart size={20} />
                  <ShieldCheck size={20} />
               </div>
             </div>
          </div>
        </div>
      </div>
    </div>
  );
};

const ShieldCheck: React.FC<{size?: number, className?: string}> = ({size=24, className}) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}>
    <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10Z"/><path d="m9 12 2 2 4-4"/>
  </svg>
);

const ShopPage: React.FC<{ onAddToCart: (p: Product) => void, onProductSelect: (p: Product) => void }> = ({ onAddToCart, onProductSelect }) => {
  const [filter, setFilter] = useState('ALL');
  const categories = ['ALL', 'DIGITAL MASTER', 'ALBUM BUNDLE', 'APPAREL', 'ACCESSORIES'];
  
  const filteredProducts = filter === 'ALL' 
    ? PRODUCTS 
    : PRODUCTS.filter(p => p.category.toUpperCase().includes(filter));

  return (
    <div className="max-w-7xl mx-auto px-6 pt-40 pb-32 space-y-24 min-h-screen">
      <div className="flex flex-col md:flex-row md:items-end justify-between border-b border-black pb-12">
        <div className="space-y-6">
          <h1 className="oswald text-8xl font-black uppercase tracking-tighter italic">THE STORE</h1>
          <nav className="flex flex-wrap gap-8">
            {categories.map(c => (
              <button 
                key={c}
                onClick={() => setFilter(c)}
                className={`text-[10px] font-black uppercase tracking-[0.3em] transition-all border-b-2 pb-1 ${filter === c ? 'border-red-600 text-red-600' : 'border-transparent text-gray-400 hover:text-black'}`}
              >
                {c}
              </button>
            ))}
          </nav>
        </div>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-16">
        {filteredProducts.map((product) => (
          <div key={product.id} className="group relative flex flex-col h-full hover:opacity-90 transition-opacity">
            <div 
              className="relative aspect-square overflow-hidden bg-gray-50 border border-gray-100 cursor-pointer mb-6"
              onClick={() => onProductSelect(product)}
            >
              <AudioSample url={product.audioUrl} />
              <img 
                src={product.image} 
                alt={product.name}
                className="w-full h-full object-cover transition-transform duration-[1.5s] group-hover:scale-105"
              />
              <div className="absolute top-4 right-4 bg-black text-white px-3 py-1 text-[9px] font-black uppercase tracking-widest">{product.category}</div>
            </div>
            <div className="space-y-4">
              <h3 
                className="oswald text-2xl font-black uppercase tracking-tight leading-none cursor-pointer hover:text-red-600 transition-colors"
                onClick={() => onProductSelect(product)}
              >
                {product.name}
              </h3>
              <p className="text-gray-400 text-sm font-bold tracking-widest italic">{product.price.toLocaleString()} UGX</p>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

const AboutPage: React.FC = () => {
  const followLinks = [
    { name: 'Instagram', icon: <Instagram size={40} />, url: SOCIAL_LINKS.instagram, color: 'hover:text-[#E1306C]', username: '@kimc_ug' },
    { name: 'Facebook', icon: <Facebook size={40} />, url: SOCIAL_LINKS.facebook, color: 'hover:text-[#1877F2]', username: 'KIM*C UG Official' },
    { name: 'YouTube', icon: <Youtube size={40} />, url: SOCIAL_LINKS.youtube, color: 'hover:text-[#FF0000]', username: 'KIM*C UG' },
    { name: 'SoundCloud', icon: <Music size={40} />, url: SOCIAL_LINKS.soundcloud, color: 'hover:text-[#FF5500]', username: 'Kim C Uganda' },
    { name: 'Spotify', icon: <Disc size={40} />, url: SOCIAL_LINKS.spotify, color: 'hover:text-[#1DB954]', username: 'Kim C' },
  ];

  return (
    <div className="pb-0 pt-40 bg-white">
      <section className="max-w-6xl mx-auto px-6 space-y-32 mb-32">
        <div className="relative h-[60vh] flex items-center justify-center overflow-hidden bg-black rounded-none shadow-2xl">
           <img 
             src="https://images.unsplash.com/photo-1514525253361-bee8718a300a?auto=format&fit=crop&q=80&w=1920" 
             className="absolute inset-0 w-full h-full object-cover opacity-40 grayscale" 
             alt="Kim*C Background" 
           />
           <div className="relative z-10 text-center space-y-6 px-4">
              <h1 className="oswald text-8xl md:text-[14rem] font-black uppercase tracking-tighter text-white leading-none italic">STORY</h1>
              <p className="text-white/40 oswald text-2xl uppercase tracking-[0.5em]">KIM*C UGANDA</p>
           </div>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-12 gap-16">
           <div className="lg:col-span-5 relative">
              <div className="sticky top-40 space-y-8">
                 <div className="aspect-[3/4] overflow-hidden bg-gray-50 border border-gray-100 shadow-xl">
                    <img src="https://images.unsplash.com/photo-1550684376-efcbd6e3f031?auto=format&fit=crop&q=80&w=1200" className="w-full h-full object-cover grayscale" alt="Portrait" />
                 </div>
              </div>
           </div>
           
           <div className="lg:col-span-7 space-y-24">
              <div className="space-y-12">
                 <div className="space-y-4">
                    <h2 className="oswald text-7xl font-black uppercase tracking-tighter flex items-center gap-4 italic">
                       THE PROFILE
                    </h2>
                    <div className="h-2 w-32 bg-red-600" />
                 </div>
                 
                 <div className="space-y-12 text-gray-600 text-xl leading-relaxed font-light italic">
                    <p>
                      <strong>Kamoga Abdul Hakim</strong>, known professionally by his stage name <strong>Kim*C</strong>, is a revolutionary figure in urban reggae and dancehall music in Uganda. Born and raised in <strong>Kibuli</strong>, his origins are deeply rooted in the storytelling traditions of Kampala.
                    </p>
                    <p>
                      His 2024 album <strong>"It's Ok"</strong> and 2025 singles like <strong>"Mbigatamu nga tebiwera"</strong> have solidified his status as a powerhouse performer. His sound, characterized by a sweet soothing voice, blends roots romance with high-energy dancehall rhythms.
                    </p>
                    <p>
                      Beyond performing, Kim*C is the architect of <strong>Sound Box Records</strong>, a premier studio and production house that serves as a hub for elite audio engineering and artist branding in Uganda.
                    </p>
                 </div>
              </div>

              <div className="bg-black text-white p-12 md:p-20 space-y-16 shadow-2xl">
                 <div className="space-y-4">
                    <h3 className="oswald text-5xl font-black uppercase italic tracking-tighter">CONTACT</h3>
                    <p className="text-white/40 text-[10px] font-black uppercase tracking-[0.6em]">MANAGEMENT BY BEXX NATION</p>
                 </div>
                 <div className="space-y-10">
                    <div className="flex items-center space-x-6">
                       <Phone size={24} className="text-red-600" />
                       <div className="space-y-1">
                          <p className="text-2xl font-black tracking-widest">+256 702 838 224</p>
                          <p className="text-xs font-bold text-gray-500 uppercase tracking-widest">WhatsApp & Calls</p>
                       </div>
                    </div>
                    <div className="flex items-center space-x-6">
                       <Mail size={24} className="text-red-600" />
                       <div className="space-y-1">
                          <p className="text-2xl font-black tracking-widest">BEXXXNATION@GMAIL.COM</p>
                          <p className="text-xs font-bold text-gray-500 uppercase tracking-widest">Inquiries & Bookings</p>
                       </div>
                    </div>
                 </div>
              </div>
           </div>
        </div>
      </section>

      {/* New Social Media Section at the Bottom */}
      <section className="bg-gray-50 border-t border-gray-100 py-32">
        <div className="max-w-7xl mx-auto px-6 text-center space-y-20">
          <div className="space-y-4">
            <h2 className="oswald text-5xl md:text-7xl font-black uppercase tracking-tighter italic">CONNECT WITH THE MOVEMENT</h2>
            <div className="h-1 w-24 bg-red-600 mx-auto" />
            <p className="text-gray-400 font-bold uppercase tracking-[0.4em] text-[10px]">Follow @kimc_ug for daily sessions and updates</p>
          </div>
          
          <div className="flex flex-wrap items-center justify-center gap-12 md:gap-24">
            {followLinks.map((social) => (
              <a 
                key={social.name}
                href={social.url}
                target="_blank"
                className={`flex flex-col items-center group transition-all duration-300 ${social.color}`}
              >
                <div className="mb-6 group-hover:scale-125 group-hover:rotate-6 transition-transform duration-500 text-black group-hover:text-inherit">
                  {social.icon}
                </div>
                <span className="oswald text-xl font-black uppercase tracking-tight text-gray-300 group-hover:text-black transition-colors">{social.name}</span>
                <span className="text-[9px] font-black uppercase tracking-[0.3em] text-gray-200 group-hover:text-red-600 transition-colors mt-1">{social.username}</span>
              </a>
            ))}
          </div>
        </div>
      </section>
    </div>
  );
};

const StudioPage: React.FC = () => {
  return (
    <div className="pt-40 pb-32 bg-gray-50">
      <section className="max-w-7xl mx-auto px-6 space-y-32">
         <div className="text-center space-y-8 max-w-5xl mx-auto">
            <p className="text-red-600 font-black uppercase tracking-[0.8em] text-[10px]">THE SONIC LAB</p>
            <h1 className="oswald text-9xl md:text-[14rem] font-black uppercase tracking-tighter leading-[0.7] italic">SOUND BOX</h1>
            <p className="text-gray-400 text-2xl font-light italic leading-relaxed">
              Premium audio engineering and visual branding for the modern artist.
            </p>
         </div>

         <div className="grid grid-cols-1 lg:grid-cols-2 gap-px bg-gray-200 border border-gray-200 shadow-2xl">
            {[
              { title: 'VOCAL DESIGN', icon: <Mic2 />, desc: 'Elite recording chain featuring world-class preamps and microphones.' },
              { title: 'BRANDING', icon: <Sparkles />, desc: 'Artist identity: from logos to HD 4K music video production.' },
              { title: 'MIXING', icon: <Settings2 />, desc: 'Crystal clear separation and depth for club, radio, and streaming.' },
              { title: 'MASTERING', icon: <Headphones />, desc: 'Loudness optimization and sonic cohesion for global standards.' }
            ].map((service) => (
              <div key={service.title} className="p-16 bg-white hover:bg-black hover:text-white transition-all group">
                 <div className="mb-10 text-red-600 group-hover:scale-125 transition-transform origin-left">{service.icon}</div>
                 <h3 className="oswald text-4xl font-black uppercase mb-6 italic tracking-tight">{service.title}</h3>
                 <p className="text-gray-400 text-lg leading-relaxed italic">{service.desc}</p>
              </div>
            ))}
         </div>
      </section>
      
      <LyricGenerator />
    </div>
  );
};

const Footer: React.FC = () => {
  return (
    <footer className="bg-white border-t border-gray-100 pt-32 pb-16">
      <div className="max-w-7xl mx-auto px-6 space-y-20">
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 pb-20 border-b border-gray-50">
           <div className="lg:col-span-1 space-y-6">
              <div className="oswald text-4xl font-black uppercase tracking-tighter italic leading-none">
                 CONNECT <br/> <span className="text-red-600">WITH KIM*C</span>
              </div>
              <p className="text-xs text-gray-400 font-bold uppercase tracking-widest leading-relaxed">Official Social Channels</p>
           </div>
           
           <div className="lg:col-span-3 grid grid-cols-2 sm:grid-cols-5 gap-6">
              {[
                { label: 'Instagram', icon: <Instagram />, url: SOCIAL_LINKS.instagram, color: 'hover:text-pink-600' },
                { label: 'Facebook', icon: <Facebook />, url: SOCIAL_LINKS.facebook, color: 'hover:text-blue-600' },
                { label: 'YouTube', icon: <Youtube />, url: SOCIAL_LINKS.youtube, color: 'hover:text-red-600' },
                { label: 'SoundCloud', icon: <Music />, url: SOCIAL_LINKS.soundcloud, color: 'hover:text-[#ff5500]' },
                { label: 'Spotify', icon: <Disc />, url: SOCIAL_LINKS.spotify, color: 'hover:text-[#1DB954]' }
              ].map(social => (
                <a 
                  key={social.label}
                  href={social.url}
                  target="_blank"
                  className={`flex flex-col items-center justify-center p-8 bg-gray-50 rounded-sm transition-all group ${social.color}`}
                >
                   <div className="mb-4 group-hover:scale-125 transition-transform duration-500">{social.icon}</div>
                   <span className="text-[10px] font-black uppercase tracking-[0.2em]">{social.label}</span>
                </a>
              ))}
           </div>
        </div>

        <div className="flex flex-col lg:flex-row justify-between items-start gap-16">
          <div className="space-y-10 max-w-sm">
            <div className="oswald text-5xl font-black uppercase tracking-tighter italic leading-none">
              KIM<span className="text-red-600">*</span>C <br/>
              <span className="text-gray-300">UGANDA</span>
            </div>
            <p className="text-gray-400 text-sm leading-relaxed font-medium">
              Managed by <strong>Bexx Nation</strong>.
            </p>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-3 gap-16 w-full lg:w-auto">
            <div className="space-y-8">
              <p className="text-[11px] font-black uppercase tracking-[0.2em] text-black">Aggregators</p>
              <nav className="flex flex-col space-y-5 text-xs font-bold text-gray-400">
                <a href={SOCIAL_LINKS.howwe} target="_blank" className="hover:text-black transition-colors flex items-center gap-2">Howwe.ug <ExternalLink size={12}/></a>
                <a href={SOCIAL_LINKS.mdundo} target="_blank" className="hover:text-black transition-colors flex items-center gap-2">Mdundo <ExternalLink size={12}/></a>
              </nav>
            </div>
            <div className="space-y-8">
              <p className="text-[11px] font-black uppercase tracking-[0.2em] text-black">Contacts</p>
              <div className="space-y-4 text-xs font-bold text-gray-400">
                 <p className="flex items-center gap-2"><Phone size={14}/> +256 702 838 224</p>
                 <p className="flex items-center gap-2"><Mail size={14}/> bexxxnation@gmail.com</p>
              </div>
            </div>
          </div>
        </div>

        <div className="pt-16 border-t border-gray-50 text-center">
          <p className="text-[9px] font-black uppercase tracking-[0.4em] text-gray-300">
            &copy; {new Date().getFullYear()} SOUND BOX RECORDS / BEXX NATION.
          </p>
        </div>
      </div>
    </footer>
  );
};

const HeaderWrapper: React.FC<{ cartCount: number, onCartToggle: () => void, onNavigate: (p: string) => void, currentPage: string }> = ({ cartCount, onCartToggle, onNavigate, currentPage }) => {
  return (
    <div className="fixed top-0 left-0 right-0 z-50">
      <AnnouncementBar />
      <Header 
        cartCount={cartCount} 
        onCartToggle={onCartToggle} 
        onNavigate={onNavigate} 
        currentPage={currentPage} 
      />
    </div>
  );
};

const App: React.FC = () => {
  const [currentPage, setCurrentPage] = useState('home');
  const [selectedProduct, setSelectedProduct] = useState<Product | null>(null);
  const [cartItems, setCartItems] = useState<CartItem[]>([]);
  const [isCartOpen, setIsCartOpen] = useState(false);
  const [isCheckoutOpen, setIsCheckoutOpen] = useState(false);

  const cartCount = cartItems.reduce((sum, item) => sum + item.quantity, 0);
  const cartTotal = cartItems.reduce((sum, item) => sum + item.price * item.quantity, 0);

  const navigateToProduct = (product: Product) => {
    setSelectedProduct(product);
    setCurrentPage('product-detail');
    setIsCartOpen(false);
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  const addToCart = (product: Product) => {
    setCartItems(prev => {
      const existing = prev.find(item => item.id === product.id);
      if (existing) {
        return prev.map(item => item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item);
      }
      return [...prev, { ...product, quantity: 1 }];
    });
    setIsCartOpen(true);
  };

  const handleBuyNow = (product: Product) => {
    setCartItems([{ ...product, quantity: 1 }]);
    setIsCartOpen(false);
    setIsCheckoutOpen(true);
  };

  const updateQuantity = (id: string, delta: number) => {
    setCartItems(prev => prev.map(item => {
      if (item.id === id) {
        const newQty = Math.max(1, item.quantity + delta);
        return { ...item, quantity: newQty };
      }
      return item;
    }));
  };

  const removeFromCart = (id: string) => {
    setCartItems(prev => prev.filter(item => item.id !== id));
  };

  const handleCheckoutSuccess = () => {
    setCartItems([]);
  };

  return (
    <div className="min-h-screen bg-white">
      <HeaderWrapper 
        cartCount={cartCount} 
        onCartToggle={() => setIsCartOpen(true)}
        onNavigate={(page) => {
          setCurrentPage(page);
          setSelectedProduct(null);
          window.scrollTo(0, 0);
        }}
        currentPage={currentPage}
      />

      <main>
        {currentPage === 'home' && <HomePage onAddToCart={addToCart} onNavigate={setCurrentPage} onProductSelect={navigateToProduct} />}
        {currentPage === 'shop' && <ShopPage onAddToCart={addToCart} onProductSelect={navigateToProduct} />}
        {currentPage === 'product-detail' && selectedProduct && (
          <ProductDetailPage 
            product={selectedProduct} 
            onAddToCart={addToCart} 
            onBuyNow={handleBuyNow}
            onBack={() => {
              setCurrentPage('shop');
              setSelectedProduct(null);
            }} 
          />
        )}
        {currentPage === 'about' && <AboutPage />}
        {currentPage === 'studio' && <StudioPage />}
      </main>

      <Footer />

      <CartDrawer 
        isOpen={isCartOpen}
        onClose={() => setIsCartOpen(false)}
        items={cartItems}
        onUpdateQuantity={updateQuantity}
        onRemove={removeFromCart}
        onViewProduct={navigateToProduct}
        onCheckout={() => {
          setIsCartOpen(false);
          setIsCheckoutOpen(true);
        }}
      />

      <CheckoutModal 
        isOpen={isCheckoutOpen}
        onClose={() => setIsCheckoutOpen(false)}
        total={cartTotal}
        onSuccess={handleCheckoutSuccess}
      />
    </div>
  );
};

export default App;


import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const rootElement = document.getElementById('root');
if (!rootElement) {
  throw new Error("Could not find root element to mount to");
}

const root = ReactDOM.createRoot(rootElement);
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KIM*C | Official Artist Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@200;400;700&family=Inter:wght@300;400;700;900&display=swap" rel="stylesheet">
    <style>
        .oswald { font-family: 'Oswald', sans-serif; }
        body { font-family: 'Inter', sans-serif; }
        @keyframes spin-slow {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .animate-spin-slow {
            animation: spin-slow 8s linear infinite;
        }
        @keyframes marquee {
          0% { transform: translateX(0); }
          100% { transform: translateX(-50%); }
        }
        .animate-marquee {
          animation: marquee 20s linear infinite;
        }
        ::selection {
            background: #dc2626;
            color: white;
        }
        /* Hide scrollbar but keep functionality */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
<script type="importmap">
{
  "imports": {
    "@google/genai": "https://esm.sh/@google/genai@^1.38.0",
    "react-dom/": "https://esm.sh/react-dom@^19.2.4/",
    "lucide-react": "https://esm.sh/lucide-react@^0.563.0",
    "react": "https://esm.sh/react@^19.2.4",
    "react/": "https://esm.sh/react@^19.2.4/"
  }
}
</script>
<link rel="stylesheet" href="/index.css">
</head>
<body class="bg-white text-black antialiased">
    <div id="root"></div>
<script type="module" src="/index.tsx"></script>
</body>
</html>

{
  "name": "Kim*C Official Artist Store & Portfolio",
  "description": "A high-end, high-contrast web experience for Ugandan reggae and dancehall sensation Kim*C, featuring a digital music store, studio booking, and an AI-powered lyric generator.",
  "requestFramePermissions": []
}
{
  "name": "kim*c-official-artist-store-&-portfolio",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@google/genai": "^1.38.0",
    "react-dom": "^19.2.4",
    "lucide-react": "^0.563.0",
    "react": "^19.2.4"
  },
  "devDependencies": {
    "@types/node": "^22.14.0",
    "@vitejs/plugin-react": "^5.0.0",
    "typescript": "~5.8.2",
    "vite": "^6.2.0"
  }
}

{
  "compilerOptions": {
    "target": "ES2022",
    "experimentalDecorators": true,
    "useDefineForClassFields": false,
    "module": "ESNext",
    "lib": [
      "ES2022",
      "DOM",
      "DOM.Iterable"
    ],
    "skipLibCheck": true,
    "types": [
      "node"
    ],
    "moduleResolution": "bundler",
    "isolatedModules": true,
    "moduleDetection": "force",
    "allowJs": true,
    "jsx": "react-jsx",
    "paths": {
      "@/*": [
        "./*"
      ]
    },
    "allowImportingTsExtensions": true,
    "noEmit": true
  }
}

import { Product, SocialLink } from './types';

export interface ExtendedSocialLink extends SocialLink {
  spotify: string;
  appleMusic: string;
}

export const SOCIAL_LINKS: ExtendedSocialLink = {
  instagram: 'https://instagram.com/kimc_ug',
  facebook: 'https://facebook.com/kimcugofficial',
  youtube: 'https://youtube.com/c/kimcug',
  soundcloud: 'https://soundcloud.com/kimcuganda',
  howwe: 'https://www.howwe.ug/KimC',
  mdundo: 'https://mdundo.com/a/201248',
  spotify: 'https://open.spotify.com/artist/4hDk9I5p1Tz0X7t5k2k6f8',
  appleMusic: 'https://music.apple.com/ug/artist/kim-c/1500000000' // Placeholder for artist link
};

export const PRODUCTS: Product[] = [
  {
    id: '2025-1',
    name: 'Mbigatamu nga tebiwera',
    price: 150000,
    category: 'Digital Master 2025',
    image: 'https://images.unsplash.com/photo-1459749411177-042180ceea72?auto=format&fit=crop&q=80&w=800',
    description: 'The definitive 2025 Afro-Dancehall anthem. A high-energy track pushing the boundaries of the Sound Box Records sound.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3'
  },
  {
    id: '2025-2',
    name: 'Nkwagala Bisinga',
    price: 150000,
    category: 'Digital Master 2025',
    image: 'https://images.unsplash.com/photo-1516280440614-37939bbacd81?auto=format&fit=crop&q=80&w=800',
    description: 'A soulful 2025 reggae ballad exploring deep love and connection. Kim*C at his most vocal-centric.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3'
  },
  {
    id: '2024-album',
    name: "It's Ok (Full Album)",
    price: 750000,
    category: 'Album Bundle 2024',
    image: 'https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?auto=format&fit=crop&q=80&w=800',
    description: 'The monumental 2024 album featuring "Tetwelumya" and "Guwooma". Complete high-fidelity masters and digital booklet.',
  },
  {
    id: '2024-1',
    name: 'Tetwelumya',
    price: 150000,
    category: 'Digital Master 2024',
    image: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?auto=format&fit=crop&q=80&w=800',
    description: 'A 2024 chart-topper blending traditional Ugandan storytelling with modern Afro-pop production.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3'
  },
  {
    id: '1',
    name: 'Nkukutu Master',
    price: 150000,
    category: 'Digital Master',
    image: 'https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?auto=format&fit=crop&q=80&w=800',
    description: 'A deep roots reggae anthem exploring the secrets of the heart and the rhythm of Kampala. Includes high-fidelity WAV stems.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3'
  },
  {
    id: '2',
    name: 'Kankyebeere Master',
    price: 150000,
    category: 'Digital Master',
    image: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?auto=format&fit=crop&q=80&w=800',
    description: 'High-energy dancehall track that became a club staple in Uganda and beyond.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3'
  },
  {
    id: '3',
    name: 'Kandye Ezange Master',
    price: 150000,
    category: 'Digital Master',
    image: 'https://images.unsplash.com/photo-1493225255756-d9584f8606e9?auto=format&fit=crop&q=80&w=800',
    description: 'The viral hit blending soulful vocals with infectious Afro-dance beats.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3'
  },
  {
    id: 'm1',
    name: 'Bexx Nation Signature Hoodie',
    price: 220000,
    category: 'Apparel',
    image: 'https://images.unsplash.com/photo-1556821840-3a63f95609a7?auto=format&fit=crop&q=80&w=800',
    description: 'Heavyweight 450GSM cotton hoodie with embroidered Kim*C logo on chest. Oversized fit.'
  },
  {
    id: 'm2',
    name: 'Kampala Roots Graphic Tee',
    price: 95000,
    category: 'Apparel',
    image: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?auto=format&fit=crop&q=80&w=800',
    description: '100% organic cotton tee featuring vintage Kibuli-inspired artwork.'
  },
  {
    id: 'm3',
    name: 'Sound Box Records Trucker Hat',
    price: 65000,
    category: 'Accessories',
    image: 'https://images.unsplash.com/photo-1588850561407-ed78c282e89b?auto=format&fit=crop&q=80&w=800',
    description: 'Structured mesh back hat with high-density Sound Box Records puff print.'
  },
  {
    id: '4',
    name: 'The Cassette Master Bundle',
    price: 500000,
    category: 'Album Bundle',
    image: 'https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?auto=format&fit=crop&q=80&w=800',
    description: 'The complete master recordings of The Cassette Album project. Includes unreleased stems and digital art booklet.',
    audioUrl: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3'
  }
];


export interface Product {
  id: string;
  name: string;
  price: number;
  category: string;
  image: string;
  description: string;
  audioUrl?: string;
}

export interface CartItem extends Product {
  quantity: number;
}

export interface SocialLink {
  instagram: string;
  facebook: string;
  youtube: string;
  soundcloud: string;
  howwe: string;
  mdundo: string;
}

import path from 'path';
import { defineConfig, loadEnv } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig(({ mode }) => {
    const env = loadEnv(mode, '.', '');
    return {
      server: {
        port: 3000,
        host: '0.0.0.0',
      },
      plugins: [react()],
      define: {
        'process.env.API_KEY': JSON.stringify(env.GEMINI_API_KEY),
        'process.env.GEMINI_API_KEY': JSON.stringify(env.GEMINI_API_KEY)
      },
      resolve: {
        alias: {
          '@': path.resolve(__dirname, '.'),
        }
      }
    };
});


          100% { transform: translateX(-50%); }
        }
        .animate-marquee {
          animation: marquee 20s linear infinite;
        }
        ::selection {
            background: #dc2626;
            color: white;
        }
        /* Hide scrollbar but keep functionality */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
<script type="importmap">
{
  "imports": {
    "@google/genai": "https://esm.sh/@google/genai@^1.38.0",
    "react-dom/": "https://esm.sh/react-dom@^19.2.4/",
    "lucide-react": "https://esm.sh/lucide-react@^0.563.0",
    "react": "https://esm.sh/react@^19.2.4",
    "react/": "https://esm.sh/react@^19.2.4/"
  }
}
</script>
<link rel="stylesheet" href="/index.css">
</head>
<body class="bg-white text-black antialiased">
    <div id="root"></div>
<script type="module" src="/index.tsx"></script>
</body>
</html>
