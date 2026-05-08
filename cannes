import React, { useState, useEffect, useMemo } from 'react';
import { MapPin, Calendar, StickyNote, Layers, Phone, Bookmark, Navigation, Plus, X, Trash2, Edit3, ChevronRight, ChevronDown, Save, Star, FileText, Eye, EyeOff } from 'lucide-react';

// ============ DESIGN TOKENS ============
const CREAM = '#FAF6EA';
const CREAM_DEEP = '#F2EBD8';
const INK = '#1F2937';
const INK_SOFT = '#2D3748';
const GOLD = '#C9A961';
const GOLD_SOFT = '#E8D9A8';
const ACCENT_RED = '#A0392E';

// ============ CHEZ VAYNER ANCHOR ============
const CHEZ_VAYNER = {
  id: 'chez-vayner',
  name: 'Chez Vayner Café',
  address: '2 Pl. du Général de Gaulle, 06400 Cannes, France',
  lat: 43.5513,
  lng: 7.0177,
  phone: '',
  isHome: true,
};

// ============ VENUE DATA ============
const SEED_VENUES = [
  CHEZ_VAYNER,
  { id: 'jw-marriott', name: 'JW Marriott Cannes', address: '50 Bd de la Croisette, 06400 Cannes, France', lat: 43.5505, lng: 7.0186, phone: '+33493061640' },
  { id: 'carlton-cannes', name: 'Carlton Cannes', address: '58 Bd de la Croisette, 06400 Cannes, France', lat: 43.5497, lng: 7.0205, phone: '+33493064006' },
  { id: 'carlton-beach', name: 'Carlton Beach', address: 'Bd de la Croisette, 06400 Cannes, France', lat: 43.5491, lng: 7.0208, phone: '' },
  { id: 'hotel-martinez', name: 'Hôtel Martinez', address: '73 Bd de la Croisette, 06400 Cannes, France', lat: 43.5475, lng: 7.0245, phone: '+33493907300' },
  { id: 'palais-festivals', name: 'Palais des Festivals', address: '1 Bd de la Croisette, 06400 Cannes, France', lat: 43.5519, lng: 7.0175, phone: '+33492998400' },
  { id: 'plage-festival', name: 'Plage du Festival', address: 'Bd de la Croisette, 06400 Cannes, France', lat: 43.5515, lng: 7.0180, phone: '' },
  { id: 'spotify-beach', name: 'Spotify Beach', address: 'Plage du Festival, Cannes (approx.)', lat: 43.5510, lng: 7.0210, phone: '' },
  { id: 'google-beach', name: 'Google Beach', address: 'Plage du Festival, Cannes (approx.)', lat: 43.5500, lng: 7.0225, phone: '' },
  { id: 'meta-beach', name: 'Meta Beach', address: 'Plage du Festival, Cannes (approx.)', lat: 43.5495, lng: 7.0235, phone: '' },
  { id: 'stagwell-sport', name: 'Stagwell Sport Beach', address: 'Plage du Festival, Cannes (approx.)', lat: 43.5485, lng: 7.0250, phone: '' },
];

// ============ CHEZ VAYNER PROGRAM ============
const CHEZ_VAYNER_EVENTS = [
  { id: 'cv-1', day: 'Sunday', date: 'June 21', time: '7:00 PM', title: 'Welcome Reception', subtitle: 'Kick-off cocktails', description: 'An intimate opening evening to welcome guests to Chez Vayner.', venueId: 'chez-vayner', sponsors: [], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-2', day: 'Monday', date: 'June 22', time: '9:00 AM', title: 'Morning Espresso & Networking', subtitle: 'Open café hours', description: 'Drop in for espresso and conversation before the day kicks off.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-3', day: 'Monday', date: 'June 22', time: '12:00 PM', title: 'World Federation of Advertisers Takeover', subtitle: 'Lunch & dialogue', description: 'A curated takeover with the WFA bringing together global marketing leaders.', venueId: 'chez-vayner', sponsors: ['World Federation of Advertisers'], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-4', day: 'Monday', date: 'June 22', time: '4:00 PM', title: 'Chief Rosé Reception', subtitle: 'Afternoon pause', description: 'Cool down with rosé and Riviera bites in the Chez Vayner courtyard.', venueId: 'chez-vayner', sponsors: ['Chief'], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-5', day: 'Monday', date: 'June 22', time: '8:00 PM', title: 'Opening Night Soirée', subtitle: 'Dinner & DJ', description: 'The first big night at Chez Vayner — long table dinner under the lights.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-6', day: 'Tuesday', date: 'June 23', time: '9:00 AM', title: 'Morning Espresso & Networking', subtitle: 'Open café hours', description: 'Start your Tuesday with espresso, pastries, and serendipitous run-ins.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-7', day: 'Tuesday', date: 'June 23', time: '11:00 AM', title: 'The Marketing Academy Takeover', subtitle: 'Mentorship & masterclass', description: 'A morning hosted by The Marketing Academy with a focus on developing the next generation of marketing leaders.', venueId: 'chez-vayner', sponsors: ['The Marketing Academy'], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-8', day: 'Tuesday', date: 'June 23', time: '2:00 PM', title: 'Creator Economy Roundtable', subtitle: 'Closed-door discussion', description: 'A working session with leading creators and platform partners on what comes next.', venueId: 'chez-vayner', sponsors: [], badges: ['creators'], rsvpUrl: '' },
  { id: 'cv-9', day: 'Tuesday', date: 'June 23', time: '6:00 PM', title: 'Cocktails on the Croisette', subtitle: 'Sunset reception', description: 'Apéritifs as the sun goes down over the Mediterranean.', venueId: 'chez-vayner', sponsors: [], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-10', day: 'Tuesday', date: 'June 23', time: '9:00 PM', title: 'Late Night at Chez Vayner', subtitle: 'After-hours', description: 'Music, cocktails, and conversation that lasts as long as you do.', venueId: 'chez-vayner', sponsors: [], badges: ['creators'], rsvpUrl: '' },
  { id: 'cv-11', day: 'Wednesday', date: 'June 24', time: '9:00 AM', title: 'Morning Espresso & Networking', subtitle: 'Open café hours', description: 'Mid-week reset with strong coffee and stronger introductions.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-12', day: 'Wednesday', date: 'June 24', time: '12:00 PM', title: 'CMO Accelerator Cocktails', subtitle: 'Hosted by Jim Stengel', description: 'A noon gathering for senior marketing leaders, hosted by Jim Stengel.', venueId: 'chez-vayner', sponsors: ['Jim Stengel Co.'], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-13', day: 'Wednesday', date: 'June 24', time: '3:00 PM', title: 'AI & The Future of Storytelling', subtitle: 'Panel & Q&A', description: 'Practitioners and platforms on how AI is reshaping the craft of storytelling.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-14', day: 'Wednesday', date: 'June 24', time: '7:00 PM', title: 'The Big Night Dinner', subtitle: 'Long-table feast', description: 'The signature Chez Vayner dinner — Riviera flavors, family style.', venueId: 'chez-vayner', sponsors: [], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-15', day: 'Wednesday', date: 'June 24', time: '10:30 PM', title: 'Midnight in Cannes', subtitle: 'After-party', description: 'The party that everyone tries to find. Now you know where it is.', venueId: 'chez-vayner', sponsors: [], badges: ['creators'], rsvpUrl: '' },
  { id: 'cv-16', day: 'Thursday', date: 'June 25', time: '9:30 AM', title: 'Morning Espresso & Networking', subtitle: 'Open café hours', description: 'Final morning at Chez Vayner — a slower pace and goodbyes.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-17', day: 'Thursday', date: 'June 25', time: '12:00 PM', title: 'Founders Lunch', subtitle: 'Closed session', description: 'A working lunch for founders building at the edges of marketing and media.', venueId: 'chez-vayner', sponsors: [], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-18', day: 'Thursday', date: 'June 25', time: '3:00 PM', title: 'Creator Studio Sessions', subtitle: 'Open recordings', description: 'Live podcast and creator content recordings throughout the afternoon.', venueId: 'chez-vayner', sponsors: [], badges: ['creators'], rsvpUrl: '' },
  { id: 'cv-19', day: 'Thursday', date: 'June 25', time: '6:00 PM', title: 'Closing Rosé Hour', subtitle: 'Apéritif & farewells', description: 'One last glass on the Croisette before everyone scatters home.', venueId: 'chez-vayner', sponsors: [], badges: ['c-suite'], rsvpUrl: '' },
  { id: 'cv-20', day: 'Thursday', date: 'June 25', time: '8:30 PM', title: 'Closing Night Dinner', subtitle: 'Final feast', description: 'The closing dinner — toasts, takeaways, and the Riviera at its best.', venueId: 'chez-vayner', sponsors: [], badges: ['creators', 'c-suite'], rsvpUrl: '' },
  { id: 'cv-21', day: 'Thursday', date: 'June 25', time: '11:00 PM', title: 'Last Call', subtitle: 'After-hours send-off', description: 'See you next year. Or sooner.', venueId: 'chez-vayner', sponsors: [], badges: ['creators'], rsvpUrl: '' },
];

const DAYS_ORDER = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

// ============ HAND-DRAWN DOODLES ============
const Doodle = ({ type, className = '', style = {} }) => {
  const stroke = INK;
  const sw = 1.5;
  const common = { fill: 'none', stroke, strokeWidth: sw, strokeLinecap: 'round', strokeLinejoin: 'round' };
  const shapes = {
    croissant: <svg viewBox="0 0 60 40" className={className} style={style}><path d="M5 25 Q15 5 30 8 Q45 5 55 25 Q45 35 30 32 Q15 35 5 25 Z" {...common} /><path d="M15 22 Q20 18 25 22 M30 20 Q35 16 40 20 M42 24 Q47 20 50 24" {...common} /></svg>,
    wine: <svg viewBox="0 0 30 50" className={className} style={style}><path d="M8 5 Q8 20 15 22 Q22 20 22 5 Z" {...common} /><path d="M8 5 L22 5" {...common} /><path d="M15 22 L15 42" {...common} /><path d="M8 45 L22 45" {...common} /><path d="M11 12 Q15 14 19 12" {...common} /></svg>,
    lemon: <svg viewBox="0 0 50 40" className={className} style={style}><ellipse cx="25" cy="20" rx="20" ry="14" {...common} /><path d="M5 20 L0 20 M45 20 L50 20" {...common} /><path d="M15 18 Q20 14 25 18 M28 22 Q33 18 38 22" {...common} /></svg>,
    lobster: <svg viewBox="0 0 60 50" className={className} style={style}><ellipse cx="30" cy="30" rx="14" ry="10" {...common} /><path d="M16 25 Q5 20 8 12 Q12 8 18 14" {...common} /><path d="M44 25 Q55 20 52 12 Q48 8 42 14" {...common} /><circle cx="22" cy="28" r="1.5" fill={stroke} /><circle cx="38" cy="28" r="1.5" fill={stroke} /><path d="M30 40 Q28 46 24 48 M30 40 Q32 46 36 48" {...common} /><path d="M22 32 Q26 36 30 32 M30 32 Q34 36 38 32" {...common} /></svg>,
    sun: <svg viewBox="0 0 60 60" className={className} style={style}><circle cx="30" cy="30" r="12" {...common} /><path d="M30 5 L30 13 M30 47 L30 55 M5 30 L13 30 M47 30 L55 30 M12 12 L18 18 M42 42 L48 48 M48 12 L42 18 M18 42 L12 48" {...common} /></svg>,
    coffee: <svg viewBox="0 0 50 50" className={className} style={style}><path d="M10 15 L10 38 Q10 42 14 42 L34 42 Q38 42 38 38 L38 15 Z" {...common} /><path d="M38 20 Q46 20 46 28 Q46 36 38 36" {...common} /><path d="M16 8 Q14 12 16 14 M22 8 Q20 12 22 14 M28 8 Q26 12 28 14" {...common} /></svg>,
    olive: <svg viewBox="0 0 40 40" className={className} style={style}><ellipse cx="20" cy="22" rx="8" ry="11" {...common} /><path d="M20 11 L20 5 M20 5 Q15 2 12 5 M20 5 Q25 2 28 5" {...common} /></svg>,
    sailboat: <svg viewBox="0 0 50 50" className={className} style={style}><path d="M5 38 L45 38 L40 44 L10 44 Z" {...common} /><path d="M25 38 L25 8 L42 35 Z" {...common} /><path d="M25 12 L12 35 L25 35" {...common} /></svg>,
    fish: <svg viewBox="0 0 60 35" className={className} style={style}><path d="M5 18 Q20 5 40 18 Q20 30 5 18 Z" {...common} /><path d="M40 18 L55 8 L52 18 L55 28 Z" {...common} /><circle cx="15" cy="16" r="1.5" fill={stroke} /></svg>,
    star: <svg viewBox="0 0 30 30" className={className} style={style}><path d="M15 3 L18 12 L27 12 L20 18 L23 27 L15 22 L7 27 L10 18 L3 12 L12 12 Z" {...common} /></svg>,
    cherry: <svg viewBox="0 0 40 50" className={className} style={style}><circle cx="13" cy="38" r="7" {...common} /><circle cx="27" cy="38" r="7" {...common} /><path d="M13 31 Q15 20 25 10 M27 31 Q25 22 30 12" {...common} /><path d="M22 8 Q28 5 32 10" {...common} /></svg>,
    palm: <svg viewBox="0 0 50 60" className={className} style={style}><path d="M25 55 L25 30" {...common} /><path d="M25 30 Q15 22 5 25 M25 30 Q35 22 45 25 M25 30 Q20 18 15 10 M25 30 Q30 18 35 10 M25 30 Q25 18 25 8" {...common} /></svg>,
  };
  return shapes[type] || null;
};

const DOODLE_LAYOUT = [
  { type: 'croissant', top: '2%', left: '3%', size: 50, rotate: -12 },
  { type: 'wine', top: '12%', right: '4%', size: 38, rotate: 8 },
  { type: 'lemon', top: '28%', left: '2%', size: 44, rotate: 15 },
  { type: 'sun', top: '5%', right: '38%', size: 46, rotate: 0 },
  { type: 'lobster', top: '45%', right: '2%', size: 52, rotate: -8 },
  { type: 'coffee', top: '60%', left: '3%', size: 42, rotate: 5 },
  { type: 'sailboat', top: '70%', right: '4%', size: 44, rotate: -10 },
  { type: 'fish', top: '82%', left: '4%', size: 50, rotate: 8 },
  { type: 'star', top: '38%', left: '6%', size: 28, rotate: 0 },
  { type: 'cherry', top: '90%', right: '5%', size: 40, rotate: -5 },
  { type: 'olive', top: '20%', right: '12%', size: 32, rotate: 12 },
  { type: 'palm', top: '52%', left: '1%', size: 48, rotate: -5 },
];

const DoodleBackground = () => (
  <div className="fixed inset-0 pointer-events-none overflow-hidden z-0" style={{ opacity: 0.18 }}>
    {DOODLE_LAYOUT.map((d, i) => (
      <div key={i} style={{
        position: 'absolute',
        top: d.top,
        left: d.left,
        right: d.right,
        width: d.size,
        height: d.size,
        transform: `rotate(${d.rotate}deg)`,
      }}>
        <Doodle type={d.type} style={{ width: '100%', height: '100%' }} />
      </div>
    ))}
  </div>
);

// ============ STORAGE HELPERS (localStorage — survives across sessions) ============
const loadState = (key, fallback) => {
  try {
    const stored = localStorage.getItem(key);
    return stored ? JSON.parse(stored) : fallback;
  } catch { return fallback; }
};
const saveState = (key, value) => {
  try { localStorage.setItem(key, JSON.stringify(value)); } catch {}
};

// ============ DIRECTIONS HELPER ============
const openDirections = (lat, lng, name) => {
  const ua = navigator.userAgent;
  const isApple = /iPhone|iPad|iPod|Mac/.test(ua);
  const url = isApple
    ? `https://maps.apple.com/?daddr=${lat},${lng}&q=${encodeURIComponent(name)}`
    : `https://www.google.com/maps/dir/?api=1&destination=${lat},${lng}&destination_place_id=${encodeURIComponent(name)}`;
  window.open(url, '_blank');
};

// ============ HEADER ============
const Header = ({ onLogoClick }) => (
  <header className="relative z-10 pt-8 pb-6 px-6 text-center border-b" style={{ borderColor: 'rgba(31,41,55,0.15)' }}>
    <button
      onClick={onLogoClick}
      className="group inline-flex flex-col items-center transition-transform hover:scale-105 active:scale-95"
      title="Tap for directions to Chez Vayner"
    >
      <div className="text-xs uppercase tracking-[0.3em] mb-1" style={{ color: INK, fontFamily: 'Georgia, serif', opacity: 0.7 }}>
        Bienvenue à
      </div>
      <h1 style={{ fontFamily: 'Caveat, cursive', fontSize: '54px', lineHeight: 1, color: INK, fontWeight: 700 }}>
        Chez Vayner
      </h1>
      <div className="flex items-center gap-1.5 mt-2 text-xs" style={{ color: GOLD, fontFamily: 'Georgia, serif' }}>
        <Navigation size={11} />
        <span className="italic">tap for directions</span>
      </div>
    </button>
  </header>
);

// ============ TUTORIAL ============
const TUTORIAL_STEPS = [
  { id: 'logo', target: 'logo', title: 'Find your way home', body: 'Tap the Chez Vayner logo at the top of any screen to instantly open directions to the café. Your home base, one tap away.' },
  { id: 'agenda', target: 'agenda', title: 'Agenda', body: 'Every event happening at Chez Vayner — and across other partner venues — laid out by day. Tap the star to save what you care about, or filter by calendar.' },
  { id: 'notes', target: 'notes', title: 'Notes', body: 'Jot thoughts on any event, or use the master pad for general to-dos. Everything rolls up into one view so you never lose a follow-up.' },
  { id: 'calendars', target: 'calendars', title: 'Calendars', body: 'Toggle calendars on and off. Add new ones (Spotify Beach, Meta House, etc.) as info drops. Edit events anytime.' },
  { id: 'map', target: 'map', title: 'Map', body: 'All venues on one map. Get directions, call ahead, or bookmark your favorites. Tap any venue to see what\'s happening there.' },
];

const TutorialOverlay = ({ step, totalSteps, currentIndex, onNext, onSkip }) => {
  return (
    <div className="fixed inset-0 z-[100]" style={{ pointerEvents: 'auto' }}>
      <div className="absolute inset-0 transition-opacity" style={{ background: 'rgba(31,41,55,0.78)' }} onClick={onSkip} />

      {step.target === 'logo' && (
        <div
          className="absolute pointer-events-none"
          style={{
            top: 16, left: '50%', transform: 'translateX(-50%)', width: 240, height: 120, borderRadius: 16,
            boxShadow: '0 0 0 4px rgba(201,169,97,0.9), 0 0 0 9999px rgba(31,41,55,0.78)', background: 'transparent',
          }}
        />
      )}

      {step.target !== 'logo' && (() => {
        const tabIndex = ['agenda', 'notes', 'calendars', 'map'].indexOf(step.target);
        const tabPercent = 25;
        const leftPercent = (tabIndex * tabPercent) + (tabPercent / 2);
        return (
          <div
            className="absolute pointer-events-none"
            style={{
              top: 158, left: `${leftPercent}%`, transform: 'translateX(-50%)', width: 80, height: 60, borderRadius: 12,
              boxShadow: '0 0 0 3px rgba(201,169,97,0.9), 0 0 0 9999px rgba(31,41,55,0.78)', background: 'transparent',
            }}
          />
        );
      })()}

      <div
        className="absolute left-1/2 -translate-x-1/2 max-w-sm w-[88%] rounded-2xl p-5 shadow-xl"
        style={{ background: '#FAF6EA', color: '#1F2937', top: step.target === 'logo' ? 160 : 250 }}
      >
        <div className="flex items-center justify-between mb-2">
          <div className="text-[10px] uppercase tracking-[0.25em]" style={{ color: '#C9A961', fontFamily: 'Georgia, serif' }}>
            {currentIndex + 1} of {totalSteps}
          </div>
          <button onClick={onSkip} className="text-xs underline" style={{ color: '#1F2937', opacity: 0.6, fontFamily: 'Georgia, serif' }}>Skip tour</button>
        </div>
        <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '24px', lineHeight: 1.15, color: '#1F2937', marginBottom: 8 }}>
          {step.title}
        </h3>
        <p className="text-sm leading-relaxed mb-4" style={{ color: '#1F2937', fontFamily: 'Georgia, serif', opacity: 0.85 }}>
          {step.body}
        </p>
        <div className="flex items-center justify-between gap-3">
          <div className="flex gap-1.5">
            {Array.from({ length: totalSteps }).map((_, i) => (
              <span key={i} className="w-1.5 h-1.5 rounded-full transition-all" style={{ background: i === currentIndex ? '#1F2937' : 'rgba(31,41,55,0.25)' }} />
            ))}
          </div>
          <button onClick={onNext} className="px-5 py-2 rounded-full text-sm font-medium" style={{ background: '#1F2937', color: '#FAF6EA', fontFamily: 'Georgia, serif' }}>
            {currentIndex === totalSteps - 1 ? 'Get started' : 'Next'}
          </button>
        </div>
      </div>
    </div>
  );
};

// ============ TAB BAR ============
const TabBar = ({ active, onChange }) => {
  const tabs = [
    { id: 'agenda', label: 'Agenda', icon: Calendar },
    { id: 'notes', label: 'Notes', icon: StickyNote },
    { id: 'calendars', label: 'Calendars', icon: Layers },
    { id: 'map', label: 'Map', icon: MapPin },
  ];
  return (
    <nav className="sticky top-0 z-20 px-3 py-2 backdrop-blur-sm border-b" style={{ background: 'rgba(250,246,234,0.92)', borderColor: 'rgba(31,41,55,0.15)' }}>
      <div className="flex justify-around max-w-2xl mx-auto">
        {tabs.map(t => {
          const Icon = t.icon;
          const isActive = active === t.id;
          return (
            <button
              key={t.id}
              onClick={() => onChange(t.id)}
              className="flex flex-col items-center gap-1 px-4 py-2 rounded-lg transition-all"
              style={{ color: isActive ? CREAM : INK, background: isActive ? INK : 'transparent' }}
            >
              <Icon size={18} />
              <span className="text-xs font-medium tracking-wide" style={{ fontFamily: 'Georgia, serif' }}>{t.label}</span>
            </button>
          );
        })}
      </div>
    </nav>
  );
};

// ============ EVENT CARD ============
const Badge = ({ type }) => {
  const config = { creators: { icon: '🎉', label: 'Creators Welcome' }, 'c-suite': { icon: '✨', label: 'C-Suite Level' } }[type];
  if (!config) return null;
  return (
    <span className="inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-[10px] font-medium tracking-wide" style={{ background: 'rgba(244,236,216,0.15)', color: CREAM_DEEP, border: `1px solid ${GOLD_SOFT}` }}>
      <span>{config.icon}</span>{config.label}
    </span>
  );
};

const EventCard = ({ event, venue, calendarName, calendarColor, isSaved, hasNotes, noteCount, onToggleSave, onOpenNotes, onVenueClick }) => (
  <div className="rounded-2xl p-5 mb-4 shadow-md transition-all hover:shadow-lg" style={{ background: INK, color: CREAM, position: 'relative' }}>
    {calendarName && calendarName !== 'Chez Vayner' && (
      <div className="absolute top-3 right-3 px-2 py-0.5 rounded-full text-[10px] font-medium" style={{ background: calendarColor || GOLD, color: INK }}>
        {calendarName}
      </div>
    )}
    <div className="flex items-start justify-between gap-3 mb-2">
      <div className="flex-1 min-w-0">
        <div className="text-xs uppercase tracking-[0.2em] mb-1" style={{ color: GOLD, fontFamily: 'Georgia, serif' }}>{event.time}</div>
        <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '22px', lineHeight: 1.15, color: CREAM }}>{event.title}</h3>
        {event.subtitle && <div className="text-sm italic mt-1" style={{ color: GOLD_SOFT, fontFamily: 'Georgia, serif' }}>{event.subtitle}</div>}
      </div>
      <button onClick={onToggleSave} className="shrink-0 p-1.5 rounded-full transition-colors" style={{ color: isSaved ? GOLD : CREAM_DEEP, opacity: isSaved ? 1 : 0.5 }} title={isSaved ? 'Saved' : 'Save'}>
        <Star size={18} fill={isSaved ? GOLD : 'none'} />
      </button>
    </div>
    {event.description && <p className="italic text-sm leading-relaxed mb-3" style={{ color: CREAM_DEEP, fontFamily: 'Georgia, serif' }}>{event.description}</p>}
    {event.sponsors && event.sponsors.length > 0 && (
      <div className="flex flex-wrap gap-1.5 mb-3">
        {event.sponsors.map((s, i) => <span key={i} className="px-2 py-0.5 rounded-full text-[10px] font-medium" style={{ background: GOLD, color: INK }}>{s}</span>)}
      </div>
    )}
    {event.badges && event.badges.length > 0 && <div className="flex flex-wrap gap-1.5 mb-3">{event.badges.map(b => <Badge key={b} type={b} />)}</div>}
    <div className="flex items-center justify-between pt-3 border-t" style={{ borderColor: 'rgba(244,236,216,0.15)' }}>
      <button onClick={() => venue && onVenueClick(venue.id)} className="text-xs flex items-center gap-1 hover:underline" style={{ color: GOLD_SOFT, fontFamily: 'Georgia, serif' }}>
        <MapPin size={12} /><span className="italic">{venue ? venue.name : 'Venue TBA'}</span>
      </button>
      <div className="flex items-center gap-3">
        <button onClick={onOpenNotes} className="text-xs flex items-center gap-1" style={{ color: hasNotes ? GOLD : CREAM_DEEP, fontFamily: 'Georgia, serif' }}>
          <FileText size={12} /><span>{hasNotes ? `Notes (${noteCount})` : 'Add note'}</span>
        </button>
        {event.rsvpUrl && (
          <a href={event.rsvpUrl} target="_blank" rel="noopener noreferrer" className="text-xs underline font-medium" style={{ color: CREAM, fontFamily: 'Georgia, serif' }}>RSVP</a>
        )}
      </div>
    </div>
  </div>
);

// ============ AGENDA TAB ============
const FilterPill = ({ label, active, onClick, color }) => (
  <button onClick={onClick} className="shrink-0 px-3 py-1.5 rounded-full text-xs font-medium whitespace-nowrap transition-all"
    style={{ background: active ? INK : 'transparent', color: active ? CREAM : INK, border: `1px solid ${active ? INK : 'rgba(31,41,55,0.3)'}`, fontFamily: 'Georgia, serif' }}>
    {color && <span className="inline-block w-2 h-2 rounded-full mr-1.5 align-middle" style={{ background: color }} />}
    {label}
  </button>
);

const AgendaTab = ({ allEvents, venues, calendars, savedEvents, notes, onToggleSave, onOpenNotes, onVenueClick, calendarVisibility }) => {
  const [filter, setFilter] = useState('all');

  const visibleEvents = useMemo(() => {
    let evts = allEvents.filter(e => calendarVisibility[e.calendarId] !== false);
    if (filter === 'saved') evts = evts.filter(e => savedEvents[e.id]);
    else if (filter !== 'all') evts = evts.filter(e => e.calendarId === filter);
    return evts;
  }, [allEvents, filter, savedEvents, calendarVisibility]);

  const grouped = useMemo(() => {
    const g = {};
    visibleEvents.forEach(e => {
      const key = e.day || 'Unscheduled';
      if (!g[key]) g[key] = [];
      g[key].push(e);
    });
    Object.keys(g).forEach(day => {
      g[day].sort((a, b) => {
        const parseTime = t => {
          if (!t) return 9999;
          const m = t.match(/(\d+):?(\d*)\s*(AM|PM)?/i);
          if (!m) return 9999;
          let h = parseInt(m[1]);
          const min = parseInt(m[2] || '0');
          const ampm = (m[3] || '').toUpperCase();
          if (ampm === 'PM' && h !== 12) h += 12;
          if (ampm === 'AM' && h === 12) h = 0;
          return h * 60 + min;
        };
        return parseTime(a.time) - parseTime(b.time);
      });
    });
    return g;
  }, [visibleEvents]);

  const sortedDays = Object.keys(grouped).sort((a, b) => {
    const ai = DAYS_ORDER.indexOf(a);
    const bi = DAYS_ORDER.indexOf(b);
    return (ai === -1 ? 99 : ai) - (bi === -1 ? 99 : bi);
  });

  return (
    <div className="px-5 pb-24 pt-5 max-w-2xl mx-auto relative z-10">
      <div className="text-center mb-6">
        <div style={{ fontFamily: 'Caveat, cursive', fontSize: '38px', color: INK, lineHeight: 1 }}>mon agenda</div>
        <div className="text-xs uppercase tracking-[0.25em] mt-1" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>Cannes Lions · 21–25 June</div>
      </div>

      <div className="flex gap-2 overflow-x-auto pb-2 mb-4 -mx-1 px-1">
        <FilterPill label="All" active={filter === 'all'} onClick={() => setFilter('all')} />
        <FilterPill label={`★ Saved (${Object.values(savedEvents).filter(Boolean).length})`} active={filter === 'saved'} onClick={() => setFilter('saved')} />
        {calendars.map(c => <FilterPill key={c.id} label={c.name} active={filter === c.id} onClick={() => setFilter(c.id)} color={c.color} />)}
      </div>

      {sortedDays.length === 0 && (
        <div className="text-center py-12 italic" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>No events to show. Try a different filter.</div>
      )}

      {sortedDays.map(day => (
        <div key={day} className="mb-8">
          <div className="mb-3">
            <div style={{ fontFamily: 'Caveat, cursive', fontSize: '32px', color: INK, lineHeight: 1 }}>{day.toLowerCase()}</div>
            {grouped[day][0]?.date && <div className="text-xs uppercase tracking-[0.2em]" style={{ color: INK, opacity: 0.5, fontFamily: 'Georgia, serif' }}>{grouped[day][0].date}</div>}
          </div>
          {grouped[day].map(event => {
            const venue = venues.find(v => v.id === event.venueId);
            const calendar = calendars.find(c => c.id === event.calendarId);
            const eventNotes = notes[event.id] || [];
            return (
              <EventCard key={event.id} event={event} venue={venue} calendarName={calendar?.name} calendarColor={calendar?.color}
                isSaved={!!savedEvents[event.id]} hasNotes={eventNotes.length > 0} noteCount={eventNotes.length}
                onToggleSave={() => onToggleSave(event.id)} onOpenNotes={() => onOpenNotes(event.id)} onVenueClick={onVenueClick} />
            );
          })}
        </div>
      ))}
    </div>
  );
};

// ============ MAP TAB ============
const ActionBtn = ({ icon: Icon, label, onClick, disabled, active }) => (
  <button onClick={onClick} disabled={disabled} className="flex flex-col items-center justify-center gap-1 py-2 rounded-lg transition-all"
    style={{ background: active ? GOLD : 'rgba(244,236,216,0.1)', color: active ? INK : (disabled ? 'rgba(244,236,216,0.4)' : CREAM), cursor: disabled ? 'not-allowed' : 'pointer' }}>
    <Icon size={16} />
    <span className="text-[10px] font-medium tracking-wide" style={{ fontFamily: 'Georgia, serif' }}>{label}</span>
  </button>
);

const VenueRow = ({ venue, isSelected, isBookmarked, eventCount, onClick, onDirections, onCall, onBookmark, onEdit, onDelete }) => (
  <div className="rounded-xl p-3 transition-all cursor-pointer"
    style={{ background: isSelected ? INK : CREAM_DEEP, color: isSelected ? CREAM : INK, border: `1px solid ${isSelected ? INK : 'rgba(31,41,55,0.15)'}` }}>
    <div onClick={onClick} className="flex items-center justify-between gap-2 mb-2">
      <div className="flex-1 min-w-0">
        <div className="flex items-center gap-2">
          <h3 className="font-semibold text-sm truncate" style={{ fontFamily: '"DM Serif Display", Georgia, serif' }}>{venue.name}</h3>
          {venue.isHome && <span className="text-[9px] px-1.5 py-0.5 rounded" style={{ background: GOLD, color: INK }}>HOME</span>}
          {isBookmarked && <Bookmark size={12} fill={isSelected ? GOLD : INK} style={{ color: isSelected ? GOLD : INK }} />}
        </div>
        <p className="text-[11px] italic truncate mt-0.5" style={{ opacity: 0.7, fontFamily: 'Georgia, serif' }}>{venue.address}</p>
        {eventCount > 0 && <div className="text-[10px] mt-1" style={{ color: isSelected ? GOLD : ACCENT_RED, fontFamily: 'Georgia, serif' }}>{eventCount} event{eventCount !== 1 ? 's' : ''}</div>}
      </div>
    </div>
    <div className="flex items-center gap-1.5">
      <button onClick={(e) => { e.stopPropagation(); onDirections(); }} className="flex-1 text-[10px] py-1 rounded-md flex items-center justify-center gap-1" style={{ background: isSelected ? GOLD : INK, color: isSelected ? INK : CREAM }}>
        <Navigation size={10} /> Directions
      </button>
      <button onClick={(e) => { e.stopPropagation(); onCall(); }} disabled={!venue.phone} className="flex-1 text-[10px] py-1 rounded-md flex items-center justify-center gap-1"
        style={{ background: isSelected ? 'rgba(244,236,216,0.15)' : 'rgba(31,41,55,0.08)', color: isSelected ? CREAM : INK, opacity: venue.phone ? 1 : 0.4, cursor: venue.phone ? 'pointer' : 'not-allowed' }}>
        <Phone size={10} /> Call
      </button>
      <button onClick={(e) => { e.stopPropagation(); onBookmark(); }} className="flex-1 text-[10px] py-1 rounded-md flex items-center justify-center gap-1"
        style={{ background: isBookmarked ? GOLD : (isSelected ? 'rgba(244,236,216,0.15)' : 'rgba(31,41,55,0.08)'), color: isBookmarked ? INK : (isSelected ? CREAM : INK) }}>
        <Bookmark size={10} /> {isBookmarked ? 'Saved' : 'Save'}
      </button>
      <button onClick={(e) => { e.stopPropagation(); onEdit(); }} className="px-2 py-1 rounded-md" style={{ background: 'transparent', color: isSelected ? CREAM_DEEP : INK, opacity: 0.6 }}>
        <Edit3 size={10} />
      </button>
      {!venue.isHome && (
        <button onClick={(e) => { e.stopPropagation(); if (confirm(`Delete ${venue.name}?`)) onDelete(); }} className="px-2 py-1 rounded-md" style={{ background: 'transparent', color: isSelected ? CREAM_DEEP : INK, opacity: 0.5 }}>
          <Trash2 size={10} />
        </button>
      )}
    </div>
  </div>
);

const Input = ({ label, value, onChange, placeholder }) => (
  <label className="block">
    <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>{label}</span>
    <input type="text" value={value} onChange={e => onChange(e.target.value)} placeholder={placeholder}
      className="w-full px-3 py-2 rounded-lg text-sm outline-none" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK, fontFamily: 'Georgia, serif' }} />
  </label>
);

const VenueFormModal = ({ title, venue, onSave, onClose }) => {
  const [form, setForm] = useState({
    name: venue?.name || '',
    address: venue?.address || '',
    lat: venue?.lat?.toString() || '',
    lng: venue?.lng?.toString() || '',
    phone: venue?.phone || '',
  });
  const submit = () => {
    if (!form.name) return;
    const lat = parseFloat(form.lat) || 43.5519;
    const lng = parseFloat(form.lng) || 7.0175;
    onSave({ name: form.name, address: form.address, lat, lng, phone: form.phone });
  };
  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center p-4" style={{ background: 'rgba(31,41,55,0.7)' }}>
      <div className="rounded-2xl p-6 max-w-md w-full" style={{ background: CREAM }}>
        <div className="flex items-center justify-between mb-4">
          <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '22px', color: INK }}>{title}</h3>
          <button onClick={onClose}><X size={20} color={INK} /></button>
        </div>
        <div className="space-y-3">
          <Input label="Name *" value={form.name} onChange={v => setForm({ ...form, name: v })} />
          <Input label="Address" value={form.address} onChange={v => setForm({ ...form, address: v })} />
          <div className="grid grid-cols-2 gap-2">
            <Input label="Latitude" value={form.lat} onChange={v => setForm({ ...form, lat: v })} placeholder="43.5519" />
            <Input label="Longitude" value={form.lng} onChange={v => setForm({ ...form, lng: v })} placeholder="7.0175" />
          </div>
          <Input label="Phone (with +country code)" value={form.phone} onChange={v => setForm({ ...form, phone: v })} placeholder="+33493..." />
          <button onClick={submit} className="w-full py-2.5 rounded-lg font-medium mt-2" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>Save</button>
        </div>
      </div>
    </div>
  );
};

const MapTab = ({ venues, allEvents, bookmarks, onToggleBookmark, focusVenueId, onVenueFocus, onAddVenue, onUpdateVenue, onDeleteVenue }) => {
  const homeVenue = venues.find(v => v.isHome) || venues[0];
  const [selectedId, setSelectedId] = useState(focusVenueId || homeVenue?.id);
  const [showAdd, setShowAdd] = useState(false);
  const [editingVenueId, setEditingVenueId] = useState(null);

  useEffect(() => { if (focusVenueId) setSelectedId(focusVenueId); }, [focusVenueId]);

  const selected = venues.find(v => v.id === selectedId);
  const venueEvents = allEvents.filter(e => e.venueId === selectedId);
  const sortedVenues = useMemo(() => {
    const home = venues.filter(v => v.isHome);
    const rest = venues.filter(v => !v.isHome);
    return [...home, ...rest];
  }, [venues]);

  return (
    <div className="px-5 pb-24 pt-3 max-w-2xl mx-auto relative z-10">
      {selected && (
        <button onClick={() => openDirections(selected.lat, selected.lng, selected.name)}
          className="w-full rounded-2xl overflow-hidden mb-3 shadow-md relative group transition-transform active:scale-[0.99]"
          style={{ aspectRatio: '16/9', background: INK, display: 'block' }}>
          <svg viewBox="0 0 400 225" preserveAspectRatio="xMidYMid slice" className="absolute inset-0 w-full h-full">
            <defs>
              <pattern id="mapGrid" width="40" height="40" patternUnits="userSpaceOnUse">
                <path d="M 40 0 L 0 0 0 40" fill="none" stroke={GOLD_SOFT} strokeWidth="0.5" opacity="0.25" />
              </pattern>
              <pattern id="mapGridFine" width="10" height="10" patternUnits="userSpaceOnUse">
                <path d="M 10 0 L 0 0 0 10" fill="none" stroke={GOLD_SOFT} strokeWidth="0.3" opacity="0.12" />
              </pattern>
            </defs>
            <rect width="400" height="225" fill={INK} />
            <rect width="400" height="225" fill="url(#mapGridFine)" />
            <rect width="400" height="225" fill="url(#mapGrid)" />
            <path d="M 0 180 Q 100 175 200 178 Q 300 181 400 175 L 400 225 L 0 225 Z" fill={ACCENT_RED} opacity="0.15" />
            <path d="M 0 180 Q 100 175 200 178 Q 300 181 400 175" fill="none" stroke={GOLD} strokeWidth="1" opacity="0.6" />
            <path d="M 0 100 L 400 95" fill="none" stroke={GOLD_SOFT} strokeWidth="1.5" opacity="0.3" />
            <path d="M 150 0 L 145 225" fill="none" stroke={GOLD_SOFT} strokeWidth="1.5" opacity="0.3" />
            <path d="M 280 0 L 285 225" fill="none" stroke={GOLD_SOFT} strokeWidth="1.5" opacity="0.3" />
            <g transform="translate(200, 100)">
              <circle cx="0" cy="0" r="22" fill={GOLD} opacity="0.25"/>
              <circle cx="0" cy="0" r="14" fill={GOLD} opacity="0.45"/>
              <path d="M 0 -14 C -8 -14 -14 -8 -14 0 C -14 8 0 18 0 18 C 0 18 14 8 14 0 C 14 -8 8 -14 0 -14 Z" fill={GOLD} stroke={INK} strokeWidth="1.5" />
              <circle cx="0" cy="-2" r="4" fill={INK} />
            </g>
          </svg>
          <div className="absolute inset-0 flex flex-col items-center justify-end p-4">
            <div className="text-center">
              <div style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '18px', color: CREAM, lineHeight: 1.1 }}>{selected.name}</div>
              <div className="inline-flex items-center gap-1.5 mt-2 px-3 py-1 rounded-full text-xs font-medium" style={{ background: GOLD, color: INK, fontFamily: 'Georgia, serif' }}>
                <Navigation size={11} />Open in Maps
              </div>
            </div>
          </div>
        </button>
      )}

      {selected && (
        <div className="rounded-2xl p-4 mb-4" style={{ background: INK, color: CREAM }}>
          <div className="flex items-start justify-between gap-3 mb-3">
            <div className="flex-1 min-w-0">
              <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '20px' }}>
                {selected.name}
                {selected.isHome && <span className="ml-2 text-xs px-2 py-0.5 rounded-full" style={{ background: GOLD, color: INK }}>HOME</span>}
              </h3>
              <p className="text-xs italic mt-1" style={{ color: GOLD_SOFT, fontFamily: 'Georgia, serif' }}>{selected.address}</p>
            </div>
          </div>
          <div className="grid grid-cols-3 gap-2">
            <ActionBtn icon={Navigation} label="Directions" onClick={() => openDirections(selected.lat, selected.lng, selected.name)} />
            <ActionBtn icon={Phone} label="Call" onClick={() => selected.phone ? window.open(`tel:${selected.phone}`) : null} disabled={!selected.phone} />
            <ActionBtn icon={Bookmark} label={bookmarks[selected.id] ? 'Saved' : 'Bookmark'} onClick={() => onToggleBookmark(selected.id)} active={!!bookmarks[selected.id]} />
          </div>
          {venueEvents.length > 0 && (
            <div className="mt-4 pt-3 border-t" style={{ borderColor: 'rgba(244,236,216,0.15)' }}>
              <div className="text-[10px] uppercase tracking-[0.2em] mb-2" style={{ color: GOLD, fontFamily: 'Georgia, serif' }}>{venueEvents.length} event{venueEvents.length !== 1 ? 's' : ''} here</div>
              {venueEvents.slice(0, 4).map(e => (
                <div key={e.id} className="text-xs mb-1.5" style={{ fontFamily: 'Georgia, serif' }}>
                  <span style={{ color: GOLD_SOFT }}>{e.day} · {e.time}</span> — <span className="italic">{e.title}</span>
                </div>
              ))}
              {venueEvents.length > 4 && <div className="text-xs italic" style={{ color: GOLD_SOFT }}>+ {venueEvents.length - 4} more</div>}
            </div>
          )}
        </div>
      )}

      <div className="flex items-center justify-between mb-3">
        <h2 style={{ fontFamily: 'Caveat, cursive', fontSize: '26px', color: INK }}>all venues</h2>
        <button onClick={() => setShowAdd(true)} className="text-xs flex items-center gap-1 px-3 py-1.5 rounded-full" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>
          <Plus size={12} /> Add venue
        </button>
      </div>

      <div className="space-y-2">
        {sortedVenues.map(v => (
          <VenueRow key={v.id} venue={v} isSelected={selectedId === v.id} isBookmarked={!!bookmarks[v.id]} eventCount={allEvents.filter(e => e.venueId === v.id).length}
            onClick={() => { setSelectedId(v.id); onVenueFocus(null); }}
            onDirections={() => openDirections(v.lat, v.lng, v.name)}
            onCall={() => v.phone && window.open(`tel:${v.phone}`)}
            onBookmark={() => onToggleBookmark(v.id)}
            onEdit={() => setEditingVenueId(v.id)}
            onDelete={() => !v.isHome && onDeleteVenue(v.id)} />
        ))}
      </div>

      {showAdd && <VenueFormModal title="Add a venue" onSave={(v) => { onAddVenue({ id: 'v-' + Date.now(), ...v }); setShowAdd(false); }} onClose={() => setShowAdd(false)} />}
      {editingVenueId && (
        <VenueFormModal title="Edit venue" venue={venues.find(v => v.id === editingVenueId)}
          onSave={(v) => { onUpdateVenue({ ...venues.find(x => x.id === editingVenueId), ...v }); setEditingVenueId(null); }}
          onClose={() => setEditingVenueId(null)} />
      )}
    </div>
  );
};

// ============ NOTES TAB ============
const NotesTab = ({ allEvents, calendars, notes, onUpdateNotes, onOpenEventNotes }) => {
  const [view, setView] = useState('rollup');
  const [masterText, setMasterText] = useState(loadState('master-note', ''));

  useEffect(() => { saveState('master-note', masterText); }, [masterText]);

  const eventsWithNotes = allEvents.filter(e => notes[e.id] && notes[e.id].length > 0);
  const totalNoteCount = Object.values(notes).reduce((sum, arr) => sum + (arr?.length || 0), 0);

  return (
    <div className="px-5 pb-24 pt-5 max-w-2xl mx-auto relative z-10">
      <div className="text-center mb-6">
        <div style={{ fontFamily: 'Caveat, cursive', fontSize: '38px', color: INK, lineHeight: 1 }}>mes notes</div>
        <div className="text-xs uppercase tracking-[0.25em] mt-1" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>
          {totalNoteCount} note{totalNoteCount !== 1 ? 's' : ''} · {eventsWithNotes.length} event{eventsWithNotes.length !== 1 ? 's' : ''}
        </div>
      </div>

      <div className="flex gap-2 mb-5">
        <FilterPill label="By event" active={view === 'rollup'} onClick={() => setView('rollup')} />
        <FilterPill label="Master pad" active={view === 'master'} onClick={() => setView('master')} />
      </div>

      {view === 'master' && (
        <div className="rounded-2xl p-4" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.15)` }}>
          <div className="text-xs uppercase tracking-[0.2em] mb-2" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>Quick to-dos & general thoughts</div>
          <textarea value={masterText} onChange={e => setMasterText(e.target.value)}
            placeholder="Pick up wine for Tuesday dinner. Follow up with Sarah re: panel. Don't forget sunscreen..."
            className="w-full min-h-[300px] outline-none resize-none text-sm leading-relaxed"
            style={{ color: INK, fontFamily: 'Georgia, serif', background: 'transparent' }} />
        </div>
      )}

      {view === 'rollup' && (
        <>
          {eventsWithNotes.length === 0 && (
            <div className="text-center py-12" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>
              <StickyNote size={32} className="mx-auto mb-3 opacity-40" />
              <p className="italic">No notes yet.</p>
              <p className="text-xs mt-1">Tap "Add note" on any event card.</p>
            </div>
          )}
          {eventsWithNotes.map(event => {
            const eventNotes = notes[event.id] || [];
            const cal = calendars.find(c => c.id === event.calendarId);
            return (
              <div key={event.id} className="rounded-2xl p-4 mb-3" style={{ background: CREAM_DEEP, border: `1px solid rgba(31,41,55,0.15)` }}>
                <button onClick={() => onOpenEventNotes(event.id)} className="text-left w-full mb-2">
                  <div className="text-[10px] uppercase tracking-[0.2em]" style={{ color: ACCENT_RED, fontFamily: 'Georgia, serif' }}>
                    {event.day} · {event.time} {cal && cal.name !== 'Chez Vayner' && `· ${cal.name}`}
                  </div>
                  <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '18px', color: INK }}>{event.title}</h3>
                </button>
                <div className="space-y-2">
                  {eventNotes.map((n, i) => (
                    <div key={i} className="text-sm leading-relaxed pl-3 border-l-2" style={{ color: INK, fontFamily: 'Georgia, serif', borderColor: GOLD }}>
                      {n.text}
                      <div className="text-[10px] mt-0.5" style={{ opacity: 0.5 }}>{n.timestamp}</div>
                    </div>
                  ))}
                </div>
              </div>
            );
          })}
        </>
      )}
    </div>
  );
};

const NotesDrawer = ({ eventId, allEvents, notes, onUpdateNotes, onClose }) => {
  const event = allEvents.find(e => e.id === eventId);
  const eventNotes = notes[eventId] || [];
  const [draft, setDraft] = useState('');

  if (!event) return null;

  const addNote = () => {
    if (!draft.trim()) return;
    const newNote = { text: draft.trim(), timestamp: new Date().toLocaleString('en-US', { month: 'short', day: 'numeric', hour: 'numeric', minute: '2-digit' }) };
    onUpdateNotes(eventId, [...eventNotes, newNote]);
    setDraft('');
  };

  const deleteNote = (idx) => onUpdateNotes(eventId, eventNotes.filter((_, i) => i !== idx));

  return (
    <div className="fixed inset-0 z-50 flex items-end sm:items-center justify-center p-0 sm:p-4" style={{ background: 'rgba(31,41,55,0.7)' }}>
      <div className="w-full sm:max-w-md rounded-t-3xl sm:rounded-2xl p-6 max-h-[85vh] overflow-y-auto" style={{ background: CREAM }}>
        <div className="flex items-start justify-between mb-4">
          <div className="flex-1 min-w-0">
            <div className="text-[10px] uppercase tracking-[0.2em]" style={{ color: ACCENT_RED, fontFamily: 'Georgia, serif' }}>{event.day} · {event.time}</div>
            <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '22px', color: INK, lineHeight: 1.2 }}>{event.title}</h3>
          </div>
          <button onClick={onClose}><X size={20} color={INK} /></button>
        </div>

        <div className="mb-4">
          <textarea value={draft} onChange={e => setDraft(e.target.value)} placeholder="Add a note, to-do, or thought..."
            className="w-full px-3 py-2 rounded-lg text-sm outline-none resize-none min-h-[80px]"
            style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK, fontFamily: 'Georgia, serif' }} />
          <button onClick={addNote} disabled={!draft.trim()} className="mt-2 w-full py-2 rounded-lg text-sm font-medium"
            style={{ background: INK, color: CREAM, opacity: draft.trim() ? 1 : 0.5, fontFamily: 'Georgia, serif' }}>Save note</button>
        </div>

        {eventNotes.length > 0 && (
          <div>
            <div className="text-xs uppercase tracking-[0.2em] mb-2" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>Saved · {eventNotes.length}</div>
            <div className="space-y-2">
              {eventNotes.map((n, i) => (
                <div key={i} className="rounded-lg p-3 flex items-start justify-between gap-2" style={{ background: 'white' }}>
                  <div className="flex-1 min-w-0">
                    <p className="text-sm leading-relaxed" style={{ color: INK, fontFamily: 'Georgia, serif' }}>{n.text}</p>
                    <div className="text-[10px] mt-1" style={{ opacity: 0.5 }}>{n.timestamp}</div>
                  </div>
                  <button onClick={() => deleteNote(i)} className="shrink-0" style={{ color: ACCENT_RED }}><Trash2 size={14} /></button>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

// ============ CALENDARS TAB ============
const AddCalendarModal = ({ onAdd, onClose }) => {
  const [name, setName] = useState('');
  const [color, setColor] = useState('#A0392E');
  const colors = ['#A0392E', '#1DB954', '#1877F2', '#FF6B35', '#7B61FF', '#C9A961', '#06B6D4'];
  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center p-4" style={{ background: 'rgba(31,41,55,0.7)' }}>
      <div className="rounded-2xl p-6 max-w-md w-full" style={{ background: CREAM }}>
        <div className="flex items-center justify-between mb-4">
          <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '22px', color: INK }}>New calendar</h3>
          <button onClick={onClose}><X size={20} color={INK} /></button>
        </div>
        <Input label="Name *" value={name} onChange={setName} placeholder="Spotify Beach" />
        <div className="mt-3">
          <span className="block text-xs mb-2 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Color</span>
          <div className="flex gap-2 flex-wrap">
            {colors.map(c => <button key={c} onClick={() => setColor(c)} className="w-8 h-8 rounded-full" style={{ background: c, border: color === c ? `3px solid ${INK}` : 'none' }} />)}
          </div>
        </div>
        <button onClick={() => { if (name) { onAdd({ id: 'cal-' + Date.now(), name, color, isBuiltIn: false }); onClose(); } }}
          className="w-full py-2.5 rounded-lg font-medium mt-4" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>Create calendar</button>
      </div>
    </div>
  );
};

const EventEditForm = ({ event, venues, onSave, onCancel }) => {
  const [form, setForm] = useState({ ...event, sponsors: event.sponsors || [], badges: event.badges || [] });
  const [sponsorDraft, setSponsorDraft] = useState('');
  const toggleBadge = (b) => setForm({ ...form, badges: form.badges.includes(b) ? form.badges.filter(x => x !== b) : [...form.badges, b] });

  return (
    <div className="space-y-3">
      <div className="grid grid-cols-2 gap-2">
        <label className="block">
          <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Day</span>
          <select value={form.day} onChange={e => setForm({ ...form, day: e.target.value })} className="w-full px-3 py-2 rounded-lg text-sm outline-none" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK }}>
            {DAYS_ORDER.map(d => <option key={d} value={d}>{d}</option>)}
          </select>
        </label>
        <Input label="Date" value={form.date} onChange={v => setForm({ ...form, date: v })} placeholder="June 22" />
      </div>
      <Input label="Time" value={form.time} onChange={v => setForm({ ...form, time: v })} placeholder="7:00 PM" />
      <Input label="Title *" value={form.title} onChange={v => setForm({ ...form, title: v })} />
      <Input label="Subtitle" value={form.subtitle} onChange={v => setForm({ ...form, subtitle: v })} />
      <label className="block">
        <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Description</span>
        <textarea value={form.description} onChange={e => setForm({ ...form, description: e.target.value })} rows={3} className="w-full px-3 py-2 rounded-lg text-sm outline-none resize-none" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK, fontFamily: 'Georgia, serif' }} />
      </label>
      <label className="block">
        <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Venue</span>
        <select value={form.venueId} onChange={e => setForm({ ...form, venueId: e.target.value })} className="w-full px-3 py-2 rounded-lg text-sm outline-none" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK }}>
          <option value="">— No venue —</option>
          {venues.map(v => <option key={v.id} value={v.id}>{v.name}</option>)}
        </select>
      </label>
      <Input label="RSVP URL" value={form.rsvpUrl} onChange={v => setForm({ ...form, rsvpUrl: v })} placeholder="https://..." />
      <div>
        <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Sponsors</span>
        <div className="flex gap-1 mb-2">
          <input value={sponsorDraft} onChange={e => setSponsorDraft(e.target.value)} placeholder="Add sponsor" className="flex-1 px-3 py-2 rounded-lg text-sm outline-none" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.2)`, color: INK, fontFamily: 'Georgia, serif' }} />
          <button onClick={() => { if (sponsorDraft) { setForm({ ...form, sponsors: [...form.sponsors, sponsorDraft] }); setSponsorDraft(''); } }} className="px-3 rounded-lg" style={{ background: INK, color: CREAM }}><Plus size={14} /></button>
        </div>
        <div className="flex flex-wrap gap-1">
          {form.sponsors.map((s, i) => (
            <span key={i} className="px-2 py-0.5 rounded-full text-xs flex items-center gap-1" style={{ background: GOLD, color: INK }}>
              {s} <button onClick={() => setForm({ ...form, sponsors: form.sponsors.filter((_, idx) => idx !== i) })}><X size={10} /></button>
            </span>
          ))}
        </div>
      </div>
      <div>
        <span className="block text-xs mb-1 font-medium" style={{ color: INK, fontFamily: 'Georgia, serif' }}>Badges</span>
        <div className="flex gap-2">
          <button onClick={() => toggleBadge('creators')} className="px-3 py-1.5 rounded-full text-xs" style={{ background: form.badges.includes('creators') ? INK : 'transparent', color: form.badges.includes('creators') ? CREAM : INK, border: `1px solid ${INK}`, fontFamily: 'Georgia, serif' }}>🎉 Creators</button>
          <button onClick={() => toggleBadge('c-suite')} className="px-3 py-1.5 rounded-full text-xs" style={{ background: form.badges.includes('c-suite') ? INK : 'transparent', color: form.badges.includes('c-suite') ? CREAM : INK, border: `1px solid ${INK}`, fontFamily: 'Georgia, serif' }}>✨ C-Suite</button>
        </div>
      </div>
      <div className="flex gap-2 pt-2">
        <button onClick={onCancel} className="flex-1 py-2.5 rounded-lg" style={{ background: 'transparent', color: INK, border: `1px solid ${INK}`, fontFamily: 'Georgia, serif' }}>Cancel</button>
        <button onClick={() => form.title && onSave(form)} disabled={!form.title} className="flex-1 py-2.5 rounded-lg font-medium" style={{ background: INK, color: CREAM, opacity: form.title ? 1 : 0.5, fontFamily: 'Georgia, serif' }}>
          <Save size={14} className="inline mr-1" /> Save
        </button>
      </div>
    </div>
  );
};

const CalendarEditor = ({ calendar, events, venues, onAddEvent, onUpdateEvent, onDeleteEvent, onClose }) => {
  const [editing, setEditing] = useState(null);
  const blank = { day: 'Monday', date: '', time: '', title: '', subtitle: '', description: '', venueId: '', sponsors: [], badges: [], rsvpUrl: '' };

  const save = (data) => {
    if (data.id) onUpdateEvent(data);
    else onAddEvent({ ...data, id: 'evt-' + Date.now(), calendarId: calendar.id });
    setEditing(null);
  };

  return (
    <div className="fixed inset-0 z-50 flex items-end sm:items-center justify-center p-0 sm:p-4" style={{ background: 'rgba(31,41,55,0.7)' }}>
      <div className="w-full sm:max-w-2xl rounded-t-3xl sm:rounded-2xl p-6 max-h-[90vh] overflow-y-auto" style={{ background: CREAM }}>
        <div className="flex items-center justify-between mb-4">
          <div>
            <div className="flex items-center gap-2">
              <span className="w-3 h-3 rounded-full" style={{ background: calendar.color }} />
              <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '22px', color: INK }}>{calendar.name}</h3>
            </div>
            <div className="text-xs italic" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>{events.length} event{events.length !== 1 ? 's' : ''}</div>
          </div>
          <button onClick={onClose}><X size={20} color={INK} /></button>
        </div>

        {!editing && (
          <>
            <button onClick={() => setEditing(blank)} className="w-full py-2.5 rounded-lg flex items-center justify-center gap-1 mb-4" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>
              <Plus size={14} /> Add event
            </button>
            <div className="space-y-2">
              {events.map(e => (
                <div key={e.id} className="rounded-lg p-3 flex items-start justify-between gap-2" style={{ background: 'white', border: `1px solid rgba(31,41,55,0.15)` }}>
                  <div className="flex-1 min-w-0">
                    <div className="text-[10px] uppercase tracking-[0.2em]" style={{ color: ACCENT_RED, fontFamily: 'Georgia, serif' }}>{e.day} · {e.time}</div>
                    <div className="font-semibold text-sm" style={{ color: INK, fontFamily: '"DM Serif Display", Georgia, serif' }}>{e.title}</div>
                    {e.subtitle && <div className="text-xs italic" style={{ color: INK, opacity: 0.6 }}>{e.subtitle}</div>}
                  </div>
                  <div className="flex gap-1 shrink-0">
                    <button onClick={() => setEditing(e)} className="p-1.5"><Edit3 size={12} color={INK} /></button>
                    <button onClick={() => { if (confirm('Delete this event?')) onDeleteEvent(e.id); }} className="p-1.5"><Trash2 size={12} color={ACCENT_RED} /></button>
                  </div>
                </div>
              ))}
              {events.length === 0 && <div className="text-center py-8 italic" style={{ color: INK, opacity: 0.5, fontFamily: 'Georgia, serif' }}>No events yet.</div>}
            </div>
          </>
        )}

        {editing && <EventEditForm event={editing} venues={venues} onSave={save} onCancel={() => setEditing(null)} />}
      </div>
    </div>
  );
};

const CalendarsTab = ({ calendars, calendarVisibility, onToggleVisibility, onAddCalendar, onDeleteCalendar, allEvents, onAddEvent, onUpdateEvent, onDeleteEvent, venues }) => {
  const [editingCal, setEditingCal] = useState(null);
  const [showAddCal, setShowAddCal] = useState(false);

  return (
    <div className="px-5 pb-24 pt-5 max-w-2xl mx-auto relative z-10">
      <div className="text-center mb-6">
        <div style={{ fontFamily: 'Caveat, cursive', fontSize: '38px', color: INK, lineHeight: 1 }}>mes calendriers</div>
        <div className="text-xs uppercase tracking-[0.25em] mt-1" style={{ color: INK, opacity: 0.6, fontFamily: 'Georgia, serif' }}>Manage every schedule</div>
      </div>

      <button onClick={() => setShowAddCal(true)} className="w-full py-3 rounded-2xl mb-4 flex items-center justify-center gap-2 font-medium" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>
        <Plus size={16} /> Add a calendar
      </button>

      {calendars.map(cal => {
        const calEvents = allEvents.filter(e => e.calendarId === cal.id);
        const isVisible = calendarVisibility[cal.id] !== false;
        return (
          <div key={cal.id} className="rounded-2xl p-4 mb-3" style={{ background: CREAM_DEEP, border: `1px solid rgba(31,41,55,0.15)` }}>
            <div className="flex items-center justify-between gap-2 mb-2">
              <div className="flex items-center gap-2 flex-1 min-w-0">
                <span className="w-3 h-3 rounded-full shrink-0" style={{ background: cal.color }} />
                <h3 style={{ fontFamily: '"DM Serif Display", Georgia, serif', fontSize: '18px', color: INK }} className="truncate">{cal.name}</h3>
                {cal.isBuiltIn && <span className="text-[9px] px-1.5 py-0.5 rounded" style={{ background: GOLD, color: INK }}>BUILT-IN</span>}
              </div>
              <button onClick={() => onToggleVisibility(cal.id)} className="p-1.5 rounded-lg" style={{ background: isVisible ? INK : 'transparent', color: isVisible ? CREAM : INK, opacity: isVisible ? 1 : 0.5 }}>
                {isVisible ? <Eye size={14} /> : <EyeOff size={14} />}
              </button>
            </div>
            <div className="text-xs italic mb-3" style={{ color: INK, opacity: 0.7, fontFamily: 'Georgia, serif' }}>{calEvents.length} event{calEvents.length !== 1 ? 's' : ''}</div>
            <div className="flex gap-2">
              <button onClick={() => setEditingCal(cal.id)} className="flex-1 text-xs py-1.5 rounded-lg flex items-center justify-center gap-1" style={{ background: INK, color: CREAM, fontFamily: 'Georgia, serif' }}>
                <Edit3 size={12} /> Edit events
              </button>
              {!cal.isBuiltIn && (
                <button onClick={() => { if (confirm(`Delete "${cal.name}" and all its events?`)) onDeleteCalendar(cal.id); }} className="px-3 py-1.5 rounded-lg" style={{ background: 'transparent', color: ACCENT_RED, border: `1px solid ${ACCENT_RED}` }}>
                  <Trash2 size={12} />
                </button>
              )}
            </div>
          </div>
        );
      })}

      {showAddCal && <AddCalendarModal onAdd={onAddCalendar} onClose={() => setShowAddCal(false)} />}
      {editingCal && (
        <CalendarEditor calendar={calendars.find(c => c.id === editingCal)} events={allEvents.filter(e => e.calendarId === editingCal)} venues={venues}
          onAddEvent={onAddEvent} onUpdateEvent={onUpdateEvent} onDeleteEvent={onDeleteEvent} onClose={() => setEditingCal(null)} />
      )}
    </div>
  );
};

// ============ ROOT APP ============
export default function App() {
  const [tab, setTab] = useState('agenda');
  const [savedEvents, setSavedEvents] = useState(() => loadState('saved-events', {}));
  const [bookmarks, setBookmarks] = useState(() => loadState('bookmarks', {}));
  const [notes, setNotes] = useState(() => loadState('notes', {}));
  const [openNoteEventId, setOpenNoteEventId] = useState(null);
  const [focusVenueId, setFocusVenueId] = useState(null);

  const [tutorialIndex, setTutorialIndex] = useState(() => {
    const seen = loadState('tutorial-seen', false);
    return seen ? -1 : 0;
  });

  const advanceTutorial = () => {
    const next = tutorialIndex + 1;
    if (next >= TUTORIAL_STEPS.length) {
      setTutorialIndex(-1);
      saveState('tutorial-seen', true);
      return;
    }
    setTutorialIndex(next);
    const nextStep = TUTORIAL_STEPS[next];
    if (['agenda', 'notes', 'calendars', 'map'].includes(nextStep.target)) setTab(nextStep.target);
  };

  const skipTutorial = () => {
    setTutorialIndex(-1);
    saveState('tutorial-seen', true);
  };

  const replayTutorial = () => {
    setTab('agenda');
    setTutorialIndex(0);
  };

  const [calendars, setCalendars] = useState(() => loadState('calendars', [
    { id: 'chez-vayner-cal', name: 'Chez Vayner', color: GOLD, isBuiltIn: true },
  ]));
  const [calendarVisibility, setCalendarVisibility] = useState(() => loadState('cal-vis', {}));
  const [customEvents, setCustomEvents] = useState(() => loadState('custom-events', []));
  const [venues, setVenues] = useState(() => loadState('venues', SEED_VENUES));

  useEffect(() => { saveState('saved-events', savedEvents); }, [savedEvents]);
  useEffect(() => { saveState('bookmarks', bookmarks); }, [bookmarks]);
  useEffect(() => { saveState('notes', notes); }, [notes]);
  useEffect(() => { saveState('calendars', calendars); }, [calendars]);
  useEffect(() => { saveState('cal-vis', calendarVisibility); }, [calendarVisibility]);
  useEffect(() => { saveState('custom-events', customEvents); }, [customEvents]);
  useEffect(() => { saveState('venues', venues); }, [venues]);

  const allEvents = useMemo(() => [
    ...CHEZ_VAYNER_EVENTS.map(e => ({ ...e, calendarId: 'chez-vayner-cal' })),
    ...customEvents,
  ], [customEvents]);

  const goHome = () => openDirections(CHEZ_VAYNER.lat, CHEZ_VAYNER.lng, CHEZ_VAYNER.name);
  const toggleSave = (id) => setSavedEvents(s => ({ ...s, [id]: !s[id] }));
  const toggleBookmark = (id) => setBookmarks(b => ({ ...b, [id]: !b[id] }));
  const updateNotes = (eventId, list) => setNotes(n => ({ ...n, [eventId]: list }));
  const onVenueClickFromAgenda = (venueId) => { setFocusVenueId(venueId); setTab('map'); };
  const addCalendar = (cal) => setCalendars(c => [...c, cal]);
  const deleteCalendar = (id) => {
    setCalendars(c => c.filter(x => x.id !== id));
    setCustomEvents(e => e.filter(x => x.calendarId !== id));
  };
  const toggleCalVis = (id) => setCalendarVisibility(v => ({ ...v, [id]: v[id] === false ? true : false }));
  const addEvent = (e) => setCustomEvents(evts => [...evts, e]);
  const updateEvent = (e) => setCustomEvents(evts => evts.map(x => x.id === e.id ? e : x));
  const deleteEvent = (id) => setCustomEvents(evts => evts.filter(x => x.id !== id));
  const addVenue = (v) => setVenues(vs => [...vs, v]);
  const updateVenue = (v) => setVenues(vs => vs.map(x => x.id === v.id ? v : x));
  const deleteVenue = (id) => setVenues(vs => vs.filter(v => v.id !== id));

  return (
    <div className="min-h-screen" style={{ background: CREAM, color: INK, fontFamily: 'Georgia, serif' }}>
      <DoodleBackground />
      <Header onLogoClick={goHome} />
      <TabBar active={tab} onChange={setTab} />

      {tab === 'agenda' && (
        <AgendaTab allEvents={allEvents} venues={venues} calendars={calendars} savedEvents={savedEvents} notes={notes} calendarVisibility={calendarVisibility}
          onToggleSave={toggleSave} onOpenNotes={setOpenNoteEventId} onVenueClick={onVenueClickFromAgenda} />
      )}
      {tab === 'map' && (
        <MapTab venues={venues} allEvents={allEvents} bookmarks={bookmarks} onToggleBookmark={toggleBookmark} focusVenueId={focusVenueId} onVenueFocus={setFocusVenueId}
          onAddVenue={addVenue} onUpdateVenue={updateVenue} onDeleteVenue={deleteVenue} />
      )}
      {tab === 'notes' && (
        <NotesTab allEvents={allEvents} calendars={calendars} notes={notes} onUpdateNotes={updateNotes} onOpenEventNotes={setOpenNoteEventId} />
      )}
      {tab === 'calendars' && (
        <CalendarsTab calendars={calendars} calendarVisibility={calendarVisibility} onToggleVisibility={toggleCalVis} onAddCalendar={addCalendar}
          onDeleteCalendar={deleteCalendar} allEvents={allEvents} onAddEvent={addEvent} onUpdateEvent={updateEvent} onDeleteEvent={deleteEvent} venues={venues} />
      )}

      {openNoteEventId && (
        <NotesDrawer eventId={openNoteEventId} allEvents={allEvents} notes={notes} onUpdateNotes={updateNotes} onClose={() => setOpenNoteEventId(null)} />
      )}

      {tutorialIndex === -1 && (
        <button onClick={replayTutorial} className="fixed bottom-24 right-4 w-10 h-10 rounded-full shadow-lg flex items-center justify-center z-40 transition-all hover:scale-105"
          style={{ background: INK, color: CREAM, opacity: 0.85 }} title="Replay tutorial">
          <span style={{ fontFamily: 'Georgia, serif', fontSize: 18, fontStyle: 'italic' }}>?</span>
        </button>
      )}

      {tutorialIndex >= 0 && tutorialIndex < TUTORIAL_STEPS.length && (
        <TutorialOverlay step={TUTORIAL_STEPS[tutorialIndex]} totalSteps={TUTORIAL_STEPS.length} currentIndex={tutorialIndex}
          onNext={advanceTutorial} onSkip={skipTutorial} />
      )}
    </div>
  );
}
