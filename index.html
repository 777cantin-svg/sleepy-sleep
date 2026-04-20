import { useState, useEffect, useRef, useCallback } from "react";

// ─────────────────────────────────────────────
// Web Audio ASMR Whisper Engine
// ─────────────────────────────────────────────
class WhisperEngine {
  constructor() {
    this.ctx = null;
    this.masterGain = null;
    this.ambiOscs = [];
    this.breathSrc = null;
    this.breathLfo = null;
  }

  init() {
    if (this.ctx) return;
    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
    this.masterGain = this.ctx.createGain();
    this.masterGain.gain.value = 0.7;
    this.masterGain.connect(this.ctx.destination);
  }

  resume() {
    if (this.ctx && this.ctx.state === "suspended") this.ctx.resume();
  }

  startAmbience() {
    this.init();
    const ctx = this.ctx;
    const now = ctx.currentTime;

    [55, 82.5, 110, 165].forEach((freq, i) => {
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      const filter = ctx.createBiquadFilter();
      osc.type = "sine";
      osc.frequency.value = freq;
      gain.gain.value = 0.045 - i * 0.008;
      filter.type = "lowpass";
      filter.frequency.value = 180;
      osc.connect(filter);
      filter.connect(gain);
      gain.connect(this.masterGain);
      osc.start(now);
      this.ambiOscs.push(osc);
    });

    const bufLen = ctx.sampleRate * 4;
    const buf = ctx.createBuffer(1, bufLen, ctx.sampleRate);
    const data = buf.getChannelData(0);
    for (let i = 0; i < bufLen; i++) data[i] = (Math.random() * 2 - 1) * 0.12;

    const src = ctx.createBufferSource();
    src.buffer = buf;
    src.loop = true;

    const filter = ctx.createBiquadFilter();
    filter.type = "bandpass";
    filter.frequency.value = 700;
    filter.Q.value = 0.4;

    const gain = ctx.createGain();
    gain.gain.value = 0.055;

    const lfo = ctx.createOscillator();
    const lfoGain = ctx.createGain();
    lfo.frequency.value = 0.08;
    lfoGain.gain.value = 0.04;
    lfo.connect(lfoGain);
    lfoGain.connect(gain.gain);

    src.connect(filter);
    filter.connect(gain);
    gain.connect(this.masterGain);
    lfo.start();
    src.start();

    this.breathSrc = src;
    this.breathLfo = lfo;
  }

  stopAmbience() {
    const now = this.ctx ? this.ctx.currentTime : 0;
    this.ambiOscs.forEach((o) => {
      try {
        o.stop(now + 2.5);
      } catch (e) {}
    });
    try {
      this.breathSrc && this.breathSrc.stop(now + 2.5);
    } catch (e) {}
    try {
      this.breathLfo && this.breathLfo.stop(now + 2.5);
    } catch (e) {}
    this.ambiOscs = [];
  }

  whisperNumber(n, voiceProfile) {
    if (!this.ctx) return;
    this.resume();
    const ctx = this.ctx;
    const now = ctx.currentTime;

    const profiles = {
      gentle: { pitch: 1.15, speed: 0.85, breath: 0.55 },
      calm: { pitch: 1.0, speed: 0.78, breath: 0.42 },
      sweet: { pitch: 1.28, speed: 0.9, breath: 0.65 },
    };
    const p = profiles[voiceProfile] || profiles.gentle;

    const sylMap = {
      1: [{ f: 270, d: 0.22, v: 0.72 }],
      2: [{ f: 300, d: 0.19, v: 0.65 }],
      3: [{ f: 285, d: 0.24, v: 0.78 }],
      4: [{ f: 265, d: 0.21, v: 0.68 }],
      5: [{ f: 295, d: 0.2, v: 0.72 }],
      6: [{ f: 280, d: 0.26, v: 0.82 }],
      7: [
        { f: 290, d: 0.2, v: 0.7 },
        { f: 272, d: 0.19, v: 0.62 },
      ],
      8: [{ f: 305, d: 0.19, v: 0.72 }],
      9: [{ f: 270, d: 0.22, v: 0.76 }],
      10: [
        { f: 295, d: 0.21, v: 0.7 },
        { f: 278, d: 0.19, v: 0.55 },
      ],
      11: [
        { f: 280, d: 0.19, v: 0.68 },
        { f: 290, d: 0.21, v: 0.72 },
      ],
      12: [
        { f: 310, d: 0.2, v: 0.65 },
        { f: 278, d: 0.2, v: 0.6 },
      ],
      13: [
        { f: 275, d: 0.24, v: 0.7 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      14: [
        { f: 265, d: 0.2, v: 0.68 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      15: [
        { f: 295, d: 0.2, v: 0.72 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      16: [
        { f: 280, d: 0.26, v: 0.78 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      17: [
        { f: 290, d: 0.2, v: 0.7 },
        { f: 272, d: 0.19, v: 0.62 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      18: [
        { f: 305, d: 0.19, v: 0.72 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      19: [
        { f: 270, d: 0.22, v: 0.76 },
        { f: 300, d: 0.19, v: 0.55 },
      ],
      20: [
        { f: 310, d: 0.22, v: 0.7 },
        { f: 280, d: 0.19, v: 0.6 },
      ],
    };

    let syls = [];
    if (sylMap[n]) {
      syls = sylMap[n];
    } else if (n < 100) {
      const tens = Math.floor(n / 10) * 10;
      const ones = n % 10;
      const tSyls = sylMap[tens] || [{ f: 285, d: 0.22, v: 0.7 }];
      const oSyls = ones > 0 ? sylMap[ones] || [{ f: 278, d: 0.2, v: 0.65 }] : [];
      syls = [...tSyls, ...oSyls];
    } else {
      const h = Math.floor(n / 100);
      const rem = n % 100;
      syls = [
        ...(sylMap[h] || [{ f: 280, d: 0.2, v: 0.68 }]),
        { f: 295, d: 0.3, v: 0.6 },
        ...(rem > 0 ? sylMap[rem] || [{ f: 278, d: 0.2, v: 0.6 }] : []),
      ];
    }

    let t = now + 0.08;
    syls.forEach((syl) => {
      const dur = syl.d / p.speed;
      this._playSyllable(t, dur, syl.f * p.pitch, syl.v, p.breath);
      t += dur + 0.05 / p.speed;
    });

    t += 0.05;
    [200, 300, 400].forEach((freq, i) => {
      const osc = ctx.createOscillator();
      const gn = ctx.createGain();
      osc.type = "sine";
      osc.frequency.value = freq * p.pitch;
      gn.gain.setValueAtTime(0, t);
      gn.gain.linearRampToValueAtTime(0.035 * p.breath * (1 - i * 0.2), t + 0.12);
      gn.gain.exponentialRampToValueAtTime(0.001, t + 0.65);
      osc.connect(gn);
      gn.connect(this.masterGain);
      osc.start(t);
      osc.stop(t + 0.7);
    });

    const nbLen = Math.ceil(ctx.sampleRate * 0.5);
    const nb = ctx.createBuffer(1, nbLen, ctx.sampleRate);
    const nd = nb.getChannelData(0);
    for (let i = 0; i < nbLen; i++) nd[i] = Math.random() * 2 - 1;
    const ns = ctx.createBufferSource();
    ns.buffer = nb;
    const nf = ctx.createBiquadFilter();
    nf.type = "bandpass";
    nf.frequency.value = 2500;
    nf.Q.value = 1.2;
    const ng = ctx.createGain();
    ng.gain.setValueAtTime(0, t);
    ng.gain.linearRampToValueAtTime(0.028 * p.breath, t + 0.05);
    ng.gain.exponentialRampToValueAtTime(0.001, t + 0.45);
    ns.connect(nf);
    nf.connect(ng);
    ng.connect(this.masterGain);
    ns.start(t);
    ns.stop(t + 0.5);
  }

  _playSyllable(startTime, dur, baseFreq, vowelness, breathiness) {
    const ctx = this.ctx;

    const osc = ctx.createOscillator();
    const oscGain = ctx.createGain();
    osc.type = "triangle";
    osc.frequency.setValueAtTime(baseFreq * 0.97, startTime);
    osc.frequency.linearRampToValueAtTime(baseFreq * 1.03, startTime + dur * 0.35);
    osc.frequency.linearRampToValueAtTime(baseFreq * 0.94, startTime + dur);
    oscGain.gain.setValueAtTime(0, startTime);
    oscGain.gain.linearRampToValueAtTime(0.058 * vowelness, startTime + dur * 0.18);
    oscGain.gain.linearRampToValueAtTime(0.052 * vowelness, startTime + dur * 0.72);
    oscGain.gain.exponentialRampToValueAtTime(0.001, startTime + dur + 0.025);

    const f1 = ctx.createBiquadFilter();
    f1.type = "peaking";
    f1.frequency.value = 700 + vowelness * 700;
    f1.gain.value = 9;
    f1.Q.value = 3.5;

    const f2 = ctx.createBiquadFilter();
    f2.type = "peaking";
    f2.frequency.value = 2000 + vowelness * 500;
    f2.gain.value = 4;
    f2.Q.value = 2.5;

    osc.connect(f1);
    f1.connect(f2);
    f2.connect(oscGain);
    oscGain.connect(this.masterGain);
    osc.start(startTime);
    osc.stop(startTime + dur + 0.06);

    const nLen = Math.ceil(ctx.sampleRate * (dur + 0.06));
    const nBuf = ctx.createBuffer(1, nLen, ctx.sampleRate);
    const nData = nBuf.getChannelData(0);
    for (let i = 0; i < nLen; i++) nData[i] = Math.random() * 2 - 1;
    const nSrc = ctx.createBufferSource();
    nSrc.buffer = nBuf;

    const nFilter = ctx.createBiquadFilter();
    nFilter.type = "bandpass";
    nFilter.frequency.value = 1800 + Math.random() * 1200;
    nFilter.Q.value = 1.8;

    const nGain = ctx.createGain();
    nGain.gain.setValueAtTime(0, startTime);
    nGain.gain.linearRampToValueAtTime(0.038 * breathiness, startTime + 0.025);
    nGain.gain.exponentialRampToValueAtTime(0.001, startTime + dur + 0.035);

    nSrc.connect(nFilter);
    nFilter.connect(nGain);
    nGain.connect(this.masterGain);
    nSrc.start(startTime);
    nSrc.stop(startTime + dur + 0.07);
  }

  setMasterVolume(v) {
    if (this.masterGain && this.ctx) {
      this.masterGain.gain.linearRampToValueAtTime(Math.max(0.001, v), this.ctx.currentTime + 1.8);
    }
  }

  destroy() {
    this.stopAmbience();
    setTimeout(() => {
      try {
        this.ctx && this.ctx.close();
      } catch (e) {}
    }, 3500);
  }
}

// ─────────────────────────────────────────────
// Sheep SVG
// ─────────────────────────────────────────────
const SheepSVG = ({ variant = "normal", scale = 1 }) => {
  const C =
    {
      normal: { face: "#c8b49a", wool: "#f0ece8" },
      gold: { face: "#c9a227", wool: "#fde99a" },
      space: { face: "#5a7fa8", wool: "#bdd0e8" },
      ninja: { face: "#2a2a2a", wool: "#5f5f5f" },
    }[variant] || { face: "#c8b49a", wool: "#f0ece8" };

  return (
    <svg
      viewBox="0 0 80 60"
      width={80 * scale}
      height={60 * scale}
      style={{ filter: variant === "gold" ? "drop-shadow(0 0 9px #f5d77e99)" : "none" }}
    >
      <rect x="22" y="42" width="6" height="14" rx="3" fill={C.face} />
      <rect x="34" y="42" width="6" height="14" rx="3" fill={C.face} />
      <rect x="46" y="42" width="6" height="14" rx="3" fill={C.face} />
      <rect x="58" y="42" width="6" height="14" rx="3" fill={C.face} />
      <ellipse cx="42" cy="36" rx="26" ry="16" fill={C.wool} />
      <circle cx="22" cy="32" r="10" fill={C.wool} />
      <circle cx="62" cy="32" r="10" fill={C.wool} />
      <circle cx="32" cy="26" r="11" fill={C.wool} />
      <circle cx="52" cy="26" r="11" fill={C.wool} />
      <circle cx="42" cy="23" r="12" fill={C.wool} />
      <ellipse cx="70" cy="34" rx="10" ry="8" fill={C.face} />
      <circle cx="73" cy="31" r="2" fill="#2a1f1a" />
      <circle cx="74" cy="30" r="0.8" fill="white" />
      <ellipse cx="76" cy="36" rx="2.5" ry="1.5" fill="#b8a08a" />
      {variant === "ninja" && (
        <rect x="65" y="29" width="14" height="5" rx="1" fill="#cc2222" opacity=".9" />
      )}
      {variant === "space" && (
        <ellipse
          cx="70"
          cy="33"
          rx="12"
          ry="10"
          fill="none"
          stroke="#88ccff"
          strokeWidth="2"
          opacity=".7"
        />
      )}
      {variant === "gold" && <path d="M65 28 L67 23 L70 27 L73 22 L76 27 L78 23 L80 28 Z" fill="#f5c518" />}
    </svg>
  );
};

const ONES = [
  "",
  "one",
  "two",
  "three",
  "four",
  "five",
  "six",
  "seven",
  "eight",
  "nine",
  "ten",
  "eleven",
  "twelve",
  "thirteen",
  "fourteen",
  "fifteen",
  "sixteen",
  "seventeen",
  "eighteen",
  "nineteen",
  "twenty",
];
const TENS = ["", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"];

const toWord = (n) => {
  if (n <= 20) return ONES[n];
  if (n < 100) return TENS[Math.floor(n / 10)] + (n % 10 ? "-" + ONES[n % 10] : "");
  return ONES[Math.floor(n / 100)] + " hundred" + (n % 100 ? " " + toWord(n % 100) : "");
};

const getVariant = (n) => {
  if (n % 50 === 0) return "gold";
  const r = Math.random();
  if (r < 0.05) return "space";
  if (r < 0.09) return "ninja";
  return "normal";
};

const BreathRing = ({ phase }) => (
  <div
    style={{
      position: "absolute",
      bottom: 88,
      left: "50%",
      transform: "translateX(-50%)",
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
      gap: 7,
      opacity: 0.42,
    }}
  >
    <div
      style={{
        width: phase === "in" ? 52 : 26,
        height: phase === "in" ? 52 : 26,
        borderRadius: "50%",
        border: "1.5px solid rgba(255,255,255,.35)",
        transition: "all 4.5s ease-in-out",
      }}
    />
    <span
      style={{
        fontFamily: "'Cormorant Garamond',serif",
        fontSize: 10,
        color: "rgba(255,255,255,.28)",
        letterSpacing: 3,
        textTransform: "uppercase",
      }}
    >
      {phase === "in" ? "breathe in" : "breathe out"}
    </span>
  </div>
);

const WhisperBubble = ({ text, visible }) => (
  <div
    style={{
      position: "fixed",
      top: "27%",
      left: "50%",
      transform: "translateX(-50%)",
      fontFamily: "'Cormorant Garamond',serif",
      fontStyle: "italic",
      fontSize: 24,
      color: "rgba(255,255,255,.82)",
      letterSpacing: 3,
      textAlign: "center",
      opacity: visible ? 1 : 0,
      transition: "opacity 2.2s ease",
      pointerEvents: "none",
      textShadow: "0 0 40px rgba(180,200,255,.4)",
      whiteSpace: "nowrap",
    }}
  >
    {text}
  </div>
);

const ENGINE = new WhisperEngine();

const STARS = Array.from({ length: 55 }, () => ({
  l: Math.random() * 100,
  t: Math.random() * 100,
  s: Math.random() < 0.15 ? 2 : 1,
  op: 0.1 + Math.random() * 0.55,
  d: 2 + Math.random() * 5,
  del: Math.random() * 5,
}));

const CSS = `
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Lato:wght@300;400&display=swap');
  @keyframes twinkle { 0%,100%{opacity:.15} 50%{opacity:.75} }
  @keyframes sheepJump { 0%,100%{transform:translateY(0)} 45%{transform:translateY(-15px)} }
  @keyframes popIn { 0%{opacity:0;transform:translate(-50%,-50%) scale(.35)} 65%{transform:translate(-50%,-50%) scale(1.1)} 100%{opacity:1;transform:translate(-50%,-50%) scale(1)} }
  @keyframes floatY { 0%,100%{transform:translate(-50%,-50%) translateY(0)} 50%{transform:translate(-50%,-50%) translateY(-8px)} }
  @keyframes fadeUp { from{opacity:0;transform:translateY(18px)} to{opacity:1;transform:translateY(0)} }
  @keyframes pulse { 0%,100%{box-shadow:0 0 40px rgba(140,170,255,.14),inset 0 1px 0 rgba(255,255,255,.1)} 50%{box-shadow:0 0 60px rgba(140,170,255,.28),inset 0 1px 0 rgba(255,255,255,.14)} }
  .vol-slider{-webkit-appearance:none;appearance:none;height:3px;border-radius:2px;background:rgba(255,255,255,.2);outline:none;width:100%;cursor:pointer;}
  .vol-slider::-webkit-slider-thumb{-webkit-appearance:none;width:15px;height:15px;border-radius:50%;background:rgba(255,255,255,.72);cursor:pointer;}
  .btn{transition:background .18s,opacity .18s;}
  .btn:hover{background:rgba(180,200,255,.12)!important;}
`;

const StarField = () => (
  <div style={{ position: "absolute", inset: 0, zIndex: 0 }}>
    {STARS.map((s, i) => (
      <div
        key={i}
        style={{
          position: "absolute",
          left: `${s.l}%`,
          top: `${s.t}%`,
          width: s.s,
          height: s.s,
          borderRadius: "50%",
          background: "white",
          opacity: s.op,
          animation: `twinkle ${s.d}s ease-in-out infinite`,
          animationDelay: `${s.del}s`,
        }}
      />
    ))}
    <div
      style={{
        position: "absolute",
        top: 36,
        right: 52,
        width: 64,
        height: 64,
        borderRadius: "50%",
        background: "radial-gradient(circle at 35% 38%,#fef8e0,#dbb96a)",
        boxShadow: "0 0 50px rgba(220,185,100,.22)",
      }}
    />
  </div>
);

// ─────────────────────────────────────────────
// Main App
// ─────────────────────────────────────────────
export default function SheepySleep() {
  const [phase, setPhase] = useState("home");
  const [sheep, setSheep] = useState([]);
  const [count, setCount] = useState(0);
  const [whisper, setWhisper] = useState("");
  const [whisperVisible, setWhisperVisible] = useState(false);
  const [screenOpacity, setScreenOpacity] = useState(1);
  const [breathPhase, setBreathPhase] = useState("in");
  const [peakCount, setPeakCount] = useState(null);
  const [voice, setVoice] = useState("gentle");
  const [showVoiceMenu, setShowVoiceMenu] = useState(false);
  const [volume, setVolume] = useState(0.72);
  const [streak] = useState(3);

  const timerRef = useRef(null);
  const breathRef = useRef(null);
  const fadeRef = useRef(null);
  const idxRef = useRef(0);
  const phaseRef = useRef("home");
  const voiceRef = useRef(voice);
  const speechReadyRef = useRef(false);

  useEffect(() => {
    voiceRef.current = voice;
  }, [voice]);

  const VOICES = {
    gentle: { label: "Gentle Sister", emoji: "🌸" },
    calm: { label: "Calm Woman", emoji: "🌙" },
    sweet: { label: "Sweet Voice", emoji: "🍯" },
  };

  const showWhisper = useCallback((text) => {
    setWhisper(text);
    setWhisperVisible(true);
    setTimeout(() => setWhisperVisible(false), 3400);
  }, []);

  const getSpeechVoice = useCallback(() => {
    const synth = window.speechSynthesis;
    if (!synth) return null;

    const voices = synth.getVoices();
    if (!voices || voices.length === 0) return null;

    const presets = {
      gentle: [/Samantha/i, /Ava/i, /Female/i, /Jenny/i, /Aria/i, /Zira/i],
      calm: [/Google US English/i, /Jenny/i, /Samantha/i, /Ava/i, /Aria/i],
      sweet: [/Ava/i, /Samantha/i, /Jenny/i, /Female/i, /Aria/i, /Zira/i],
    };

    const patterns = presets[voiceRef.current] || presets.gentle;

    for (const pattern of patterns) {
      const found = voices.find((v) => v.lang?.startsWith("en") && pattern.test(v.name));
      if (found) return found;
    }

    return voices.find((v) => v.lang?.startsWith("en-US")) ||
      voices.find((v) => v.lang?.startsWith("en")) ||
      voices[0] ||
      null;
  }, []);

  const speakSheep = useCallback(
    (n) => {
      const synth = window.speechSynthesis;
      if (!synth) return;

      const text = `${toWord(n)} sheep`;
      const utter = new SpeechSynthesisUtterance(text);

      utter.lang = "en-US";
      utter.rate =
        voiceRef.current === "calm"
          ? 0.68
          : voiceRef.current === "sweet"
          ? 0.82
          : 0.74;

      utter.pitch =
        voiceRef.current === "calm"
          ? 0.95
          : voiceRef.current === "sweet"
          ? 1.18
          : 1.08;

      utter.volume = Math.max(0, Math.min(1, volume));

      const selectedVoice = getSpeechVoice();
      if (selectedVoice) utter.voice = selectedVoice;

      synth.cancel();
      synth.speak(utter);
    },
    [getSpeechVoice, volume]
  );

  const scheduleNext = useCallback(() => {
    if (phaseRef.current !== "sleeping") return;

    idxRef.current += 1;
    const n = idxRef.current;
    const variant = getVariant(n);
    const word = toWord(n);

    // 実際の音声読み上げ
    speakSheep(n);

    // 効果音も残したい場合は下を有効のまま
    // もし聞き取りづらければ、この1行をコメントアウトしてください
    ENGINE.whisperNumber(n, voiceRef.current);

    const label =
      variant === "gold"
        ? `${word} sheep… ✨`
        : variant === "ninja"
        ? `${word} sheep… 🥷`
        : variant === "space"
        ? `${word} sheep… 🚀`
        : `${word} sheep…`;

    showWhisper(label);
    setCount(n);

    setSheep((prev) =>
      [
        ...prev,
        {
          id: n,
          variant,
          x: 4 + Math.random() * 84,
          y: 28 + Math.random() * 50,
          scale: 0.55 + Math.random() * 0.55,
        },
      ].slice(-40)
    );

    if (n >= 300) return;

    const gap = Math.random() < 0.1 ? 8000 + Math.random() * 6000 : 3000 + Math.random() * 3200;
    timerRef.current = setTimeout(scheduleNext, gap);
  }, [showWhisper, speakSheep]);

  const startSleep = () => {
    phaseRef.current = "sleeping";
    idxRef.current = 0;

    window.speechSynthesis?.cancel();

    setPhase("sleeping");
    setCount(0);
    setSheep([]);
    setScreenOpacity(1);
    setBreathPhase("in");

    ENGINE.init();
    ENGINE.resume();
    ENGINE.setMasterVolume(volume);
    ENGINE.startAmbience();

    // 音声エンジンをユーザー操作後に起こす
    if (window.speechSynthesis && !speechReadyRef.current) {
      window.speechSynthesis.getVoices();
      speechReadyRef.current = true;
    }

    let btick = 0;
    breathRef.current = setInterval(() => {
      btick++;
      setBreathPhase(btick % 2 === 0 ? "in" : "out");
    }, 4500);

    fadeRef.current = setInterval(() => {
      setScreenOpacity((prev) => Math.max(0.06, prev - 0.0022));
    }, 2000);

    timerRef.current = setTimeout(scheduleNext, 1300);
  };

  const stopSleep = () => {
    phaseRef.current = "woke";
    clearTimeout(timerRef.current);
    clearInterval(breathRef.current);
    clearInterval(fadeRef.current);
    window.speechSynthesis?.cancel();
    ENGINE.setMasterVolume(0);
    setTimeout(() => ENGINE.stopAmbience(), 2200);
    setPeakCount(idxRef.current);
    setPhase("woke");
  };

  useEffect(() => {
    if (!window.speechSynthesis) return;

    const loadVoices = () => {
      window.speechSynthesis.getVoices();
    };

    loadVoices();
    window.speechSynthesis.onvoiceschanged = loadVoices;

    return () => {
      window.speechSynthesis.onvoiceschanged = null;
    };
  }, []);

  useEffect(
    () => () => {
      phaseRef.current = "home";
      clearTimeout(timerRef.current);
      clearInterval(breathRef.current);
      clearInterval(fadeRef.current);
      window.speechSynthesis?.cancel();
      ENGINE.destroy();
    },
    []
  );

  useEffect(() => {
    ENGINE.setMasterVolume(volume);
  }, [volume]);

  if (phase === "home")
    return (
      <div
        style={{
          minHeight: "100vh",
          background: "#06090f",
          display: "flex",
          flexDirection: "column",
          alignItems: "center",
          justifyContent: "center",
          fontFamily: "'Cormorant Garamond',serif",
          color: "white",
          position: "relative",
          overflow: "hidden",
        }}
      >
        <style>{CSS}</style>
        <StarField />
        <div style={{ zIndex: 1, textAlign: "center", animation: "fadeUp 1s ease forwards" }}>
          <div style={{ animation: "sheepJump 3.2s ease-in-out infinite", marginBottom: 10 }}>
            <SheepSVG scale={1.5} />
          </div>

          <h1
            style={{
              fontSize: 44,
              fontWeight: 300,
              letterSpacing: 4,
              margin: "0 0 4px",
              textShadow: "0 0 40px rgba(180,200,255,.25)",
            }}
          >
            Sheepy Sleep
          </h1>

          <p
            style={{
              fontStyle: "italic",
              fontSize: 15,
              color: "rgba(255,255,255,.4)",
              letterSpacing: 3,
              margin: "0 0 34px",
              fontWeight: 300,
            }}
          >
            whisper counting
          </p>

          <div
            style={{
              background: "rgba(255,255,255,.05)",
              border: "1px solid rgba(255,255,255,.1)",
              borderRadius: 20,
              padding: "7px 20px",
              display: "inline-flex",
              alignItems: "center",
              gap: 8,
              marginBottom: 30,
              fontSize: 13,
              color: "rgba(255,255,255,.42)",
              fontFamily: "'Lato',sans-serif",
              letterSpacing: 1,
            }}
          >
            🔥 {streak} night streak
          </div>

          <div style={{ marginBottom: 26, position: "relative" }}>
            <button
              className="btn"
              onClick={() => setShowVoiceMenu((v) => !v)}
              style={{
                background: "rgba(255,255,255,.07)",
                border: "1px solid rgba(255,255,255,.18)",
                borderRadius: 30,
                padding: "10px 26px",
                color: "rgba(255,255,255,.65)",
                fontFamily: "'Lato',sans-serif",
                fontSize: 13,
                letterSpacing: 1.5,
                cursor: "pointer",
                textTransform: "uppercase",
              }}
            >
              {VOICES[voice].emoji} {VOICES[voice].label} ▾
            </button>

            {showVoiceMenu && (
              <div
                style={{
                  position: "absolute",
                  top: "115%",
                  left: "50%",
                  transform: "translateX(-50%)",
                  background: "#0c1118",
                  border: "1px solid rgba(255,255,255,.12)",
                  borderRadius: 18,
                  padding: "10px",
                  minWidth: 220,
                  boxShadow: "0 10px 40px rgba(0,0,0,.35)",
                  zIndex: 30,
                }}
              >
                {Object.entries(VOICES).map(([key, item]) => (
                  <button
                    key={key}
                    onClick={() => {
                      setVoice(key);
                      setShowVoiceMenu(false);
                    }}
                    className="btn"
                    style={{
                      width: "100%",
                      background: key === voice ? "rgba(180,200,255,.10)" : "transparent",
                      color: "rgba(255,255,255,.78)",
                      border: "none",
                      padding: "12px 14px",
                      borderRadius: 12,
                      textAlign: "left",
                      cursor: "pointer",
                      fontFamily: "'Lato',sans-serif",
                      fontSize: 13,
                      marginBottom: 4,
                    }}
                  >
                    {item.emoji} {item.label}
                  </button>
                ))}
              </div>
            )}
          </div>

          <div
            style={{
              width: 260,
              margin: "0 auto 30px",
              textAlign: "left",
              fontFamily: "'Lato',sans-serif",
            }}
          >
            <div
              style={{
                marginBottom: 8,
                fontSize: 12,
                color: "rgba(255,255,255,.45)",
                letterSpacing: 1.2,
                textTransform: "uppercase",
              }}
            >
              Volume
            </div>
            <input
              className="vol-slider"
              type="range"
              min="0"
              max="1"
              step="0.01"
              value={volume}
              onChange={(e) => setVolume(parseFloat(e.target.value))}
            />
          </div>

          <button
            onClick={startSleep}
            className="btn"
            style={{
              background: "rgba(180,200,255,.08)",
              border: "1px solid rgba(180,200,255,.18)",
              color: "white",
              borderRadius: 999,
              padding: "16px 34px",
              fontSize: 16,
              letterSpacing: 2,
              cursor: "pointer",
              fontFamily: "'Lato',sans-serif",
              textTransform: "uppercase",
              boxShadow: "0 0 40px rgba(140,170,255,.14), inset 0 1px 0 rgba(255,255,255,.1)",
              animation: "pulse 4s ease-in-out infinite",
            }}
          >
            Start Sleep
          </button>
        </div>
      </div>
    );

  if (phase === "sleeping")
    return (
      <div
        style={{
          minHeight: "100vh",
          background: `rgba(6,9,15,${screenOpacity})`,
          transition: "background 2s ease",
          position: "relative",
          overflow: "hidden",
          color: "white",
        }}
      >
        <style>{CSS}</style>
        <StarField />

        <WhisperBubble text={whisper} visible={whisperVisible} />

        <div
          style={{
            position: "absolute",
            top: 24,
            left: 24,
            zIndex: 10,
            fontFamily: "'Lato',sans-serif",
            color: "rgba(255,255,255,.52)",
            fontSize: 12,
            letterSpacing: 2,
            textTransform: "uppercase",
          }}
        >
          Count {count}
        </div>

        <button
          onClick={stopSleep}
          className="btn"
          style={{
            position: "absolute",
            top: 18,
            right: 18,
            zIndex: 10,
            background: "rgba(255,255,255,.05)",
            border: "1px solid rgba(255,255,255,.12)",
            color: "rgba(255,255,255,.75)",
            borderRadius: 999,
            padding: "10px 16px",
            cursor: "pointer",
            fontFamily: "'Lato',sans-serif",
            letterSpacing: 1.5,
            textTransform: "uppercase",
            fontSize: 12,
          }}
        >
          Wake
        </button>

        {sheep.map((s) => (
          <div
            key={s.id}
            style={{
              position: "absolute",
              left: `${s.x}%`,
              top: `${s.y}%`,
              transform: "translate(-50%,-50%)",
              animation:
                s.id === count
                  ? "popIn .7s ease forwards, floatY 4s ease-in-out infinite .7s"
                  : "floatY 4s ease-in-out infinite",
              zIndex: 2,
              opacity: s.id === count ? 0 : 1,
            }}
          >
            <SheepSVG variant={s.variant} scale={s.scale} />
          </div>
        ))}

        <BreathRing phase={breathPhase} />
      </div>
    );

  return (
    <div
      style={{
        minHeight: "100vh",
        background: "#070b12",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        color: "white",
        fontFamily: "'Cormorant Garamond',serif",
        position: "relative",
        overflow: "hidden",
      }}
    >
      <style>{CSS}</style>
      <StarField />

      <div
        style={{
          position: "relative",
          zIndex: 1,
          textAlign: "center",
          padding: "32px 24px",
          background: "rgba(255,255,255,.04)",
          border: "1px solid rgba(255,255,255,.08)",
          borderRadius: 28,
          width: "min(92vw, 420px)",
          boxShadow: "0 20px 60px rgba(0,0,0,.35)",
        }}
      >
        <div style={{ marginBottom: 12 }}>
          <SheepSVG variant="gold" scale={1.25} />
        </div>

        <div
          style={{
            fontSize: 14,
            letterSpacing: 3,
            textTransform: "uppercase",
            color: "rgba(255,255,255,.4)",
            fontFamily: "'Lato',sans-serif",
            marginBottom: 8,
          }}
        >
          Session Ended
        </div>

        <h2 style={{ fontSize: 34, fontWeight: 300, margin: "0 0 12px" }}>
          You reached {peakCount ?? 0}
        </h2>

        <p
          style={{
            margin: "0 0 28px",
            color: "rgba(255,255,255,.58)",
            fontSize: 16,
            lineHeight: 1.7,
          }}
        >
          Rest slowly. Breathe gently. Let the night grow softer.
        </p>

        <button
          onClick={() => {
            setPhase("home");
            setPeakCount(null);
            setWhisper("");
            setWhisperVisible(false);
            setScreenOpacity(1);
          }}
          className="btn"
          style={{
            background: "rgba(180,200,255,.08)",
            border: "1px solid rgba(180,200,255,.18)",
            color: "white",
            borderRadius: 999,
            padding: "14px 28px",
            fontSize: 14,
            letterSpacing: 2,
            cursor: "pointer",
            fontFamily: "'Lato',sans-serif",
            textTransform: "uppercase",
          }}
        >
          Back Home
        </button>
      </div>
    </div>
  );
}
