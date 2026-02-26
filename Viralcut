import { useState, useRef, useEffect } from "react";

const CSS = `
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap');
*{margin:0;padding:0;box-sizing:border-box;}
:root{--bg:#060608;--s1:#101014;--s2:#17171d;--s3:#1f1f28;--red:#FF2D55;--org:#FF6B00;--tk:#00F2EA;--grn:#2ECC71;--txt:#F0F0F5;--mut:#55556A;--bdr:#1e1e28;--glow:0 0 40px rgba(255,45,85,.28);}
html,body{background:var(--bg);color:var(--txt);font-family:'DM Sans',sans-serif;overflow-x:hidden;}
.nav{display:flex;align-items:center;justify-content:space-between;padding:16px 20px;border-bottom:1px solid var(--bdr);position:sticky;top:0;background:rgba(6,6,8,.97);backdrop-filter:blur(20px);z-index:200;}
.logo{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:3px;background:linear-gradient(135deg,#FF2D55,#FF6B00);-webkit-background-clip:text;-webkit-text-fill-color:transparent;}
.logo em{-webkit-text-fill-color:var(--txt);font-style:normal;}
.nav-r{display:flex;align-items:center;gap:10px;}
.pro-chip{font-family:'Space Mono',monospace;font-size:10px;background:linear-gradient(135deg,#FF2D55,#FF6B00);padding:5px 12px;border-radius:20px;cursor:pointer;border:none;color:#fff;letter-spacing:.5px;}
.free-chip{font-family:'Space Mono',monospace;font-size:10px;background:var(--s2);border:1px solid var(--bdr);padding:5px 12px;border-radius:20px;color:var(--mut);}
.av-btn{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,#FF2D55,#FF6B00);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:16px;position:relative;flex-shrink:0;}
.ndot{position:absolute;top:-1px;right:-1px;width:9px;height:9px;background:var(--red);border-radius:50%;border:2px solid var(--bg);}
.bnav{position:fixed;bottom:0;left:0;right:0;background:rgba(6,6,8,.97);backdrop-filter:blur(20px);border-top:1px solid var(--bdr);display:flex;padding:8px 0 20px;z-index:200;}
.btab{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:4px 0;border:none;background:transparent;}
.btab-icon{font-size:20px;line-height:1;}
.btab-lbl{font-family:'Space Mono',monospace;font-size:9px;letter-spacing:.5px;color:var(--mut);text-transform:uppercase;}
.btab.on .btab-lbl{color:var(--red);}
.btab-dot{width:4px;height:4px;border-radius:50%;background:var(--red);opacity:0;margin-top:1px;}
.btab.on .btab-dot{opacity:1;}
.pb{padding-bottom:90px;}
.hero{text-align:center;padding:48px 24px 28px;}
.hbadge{display:inline-flex;align-items:center;gap:8px;font-family:'Space Mono',monospace;font-size:10px;letter-spacing:2px;color:var(--red);text-transform:uppercase;margin-bottom:18px;background:rgba(255,45,85,.08);border:1px solid rgba(255,45,85,.2);padding:6px 14px;border-radius:30px;}
.pulse{width:6px;height:6px;background:var(--red);border-radius:50%;animation:pulse 2s infinite;flex-shrink:0;}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1);}50%{opacity:.3;transform:scale(1.7);}}
.hero h1{font-family:'Bebas Neue',sans-serif;font-size:clamp(52px,12vw,90px);line-height:.92;letter-spacing:2px;margin-bottom:18px;}
.grad{background:linear-gradient(135deg,#FF2D55,#FF6B00);-webkit-background-clip:text;-webkit-text-fill-color:transparent;display:block;}
.hero-sub{color:var(--mut);font-size:14px;max-width:370px;margin:0 auto 28px;line-height:1.7;font-weight:300;}
.pbadges{display:flex;justify-content:center;gap:9px;margin-bottom:32px;flex-wrap:wrap;}
.pbadge{display:flex;align-items:center;gap:6px;padding:6px 14px;border-radius:8px;border:1px solid var(--bdr);background:var(--s2);font-size:12px;font-weight:500;}
.pbadge.tk{border-color:rgba(0,242,234,.3);color:var(--tk);}
.pbadge.yt{border-color:rgba(255,0,0,.3);color:#ff6666;}
.pbadge.ig{border-color:rgba(225,48,108,.3);color:#E1306C;}
.pwrap{max-width:640px;margin:0 auto;padding:0 20px 40px;}
.pbox{background:var(--s1);border:1px solid var(--bdr);border-radius:18px;padding:4px;transition:.3s;}
.pbox:focus-within{border-color:var(--red);box-shadow:var(--glow);}
.pinr{display:flex;align-items:flex-end;gap:8px;}
.pinput{flex:1;background:transparent;border:none;outline:none;color:var(--txt);font-family:'DM Sans',sans-serif;font-size:16px;padding:16px 16px 12px;resize:none;min-height:58px;max-height:120px;line-height:1.5;}
.pinput::placeholder{color:var(--mut);}
.gbtn{margin:8px;padding:14px 22px;background:linear-gradient(135deg,#FF2D55,#FF6B00);border:none;border-radius:12px;color:#fff;font-family:'Bebas Neue',sans-serif;font-size:17px;letter-spacing:1px;cursor:pointer;white-space:nowrap;flex-shrink:0;}
.gbtn:disabled{opacity:.5;cursor:not-allowed;}
.srow{display:flex;gap:8px;margin-top:14px;overflow-x:auto;padding-bottom:4px;scrollbar-width:none;}
.spill{flex-shrink:0;display:flex;align-items:center;gap:6px;padding:7px 14px;border-radius:8px;border:1px solid var(--bdr);background:var(--s2);cursor:pointer;font-size:12px;color:var(--mut);}
.spill.on{border-color:var(--red);color:var(--txt);background:rgba(255,45,85,.1);}
.chips{display:flex;flex-wrap:wrap;gap:7px;margin-top:13px;}
.chip{font-size:12px;background:var(--s2);border:1px solid var(--bdr);border-radius:20px;padding:5px 12px;cursor:pointer;color:var(--mut);}
.cbar{display:flex;align-items:center;justify-content:space-between;background:var(--s1);border:1px solid var(--bdr);border-radius:10px;padding:10px 16px;margin-top:13px;}
.clbl{color:var(--mut);font-family:'Space Mono',monospace;font-size:10px;}
.cdots{display:flex;gap:5px;}
.cdot{width:10px;height:10px;border-radius:50%;border:1px solid var(--bdr);background:var(--s2);}
.cdot.on{background:var(--red);border-color:var(--red);}
.lscreen{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 24px;text-align:center;background:var(--bg);}
.licon{font-size:52px;margin-bottom:22px;animation:bob 1.2s ease infinite;}
@keyframes bob{0%,100%{transform:translateY(0);}50%{transform:translateY(-10px);}}
.ltitle{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:2px;margin-bottom:8px;color:var(--red);}
.lsub{font-size:13px;color:var(--mut);margin-bottom:32px;}
.lsteps{display:flex;flex-direction:column;gap:10px;width:100%;max-width:360px;margin-bottom:28px;}
.lstep{display:flex;align-items:center;gap:12px;padding:11px 16px;background:var(--s1);border:1px solid var(--bdr);border-radius:12px;font-size:13px;color:var(--mut);text-align:left;}
.lstep.active{border-color:var(--red);color:var(--txt);background:rgba(255,45,85,.06);}
.lstep.done{border-color:var(--grn);color:var(--grn);background:rgba(46,204,113,.06);}
.lstep-i{font-size:17px;flex-shrink:0;width:24px;text-align:center;}
.lbar{width:100%;max-width:360px;height:3px;background:var(--bdr);border-radius:3px;overflow:hidden;}
.lfill{height:100%;background:linear-gradient(90deg,#FF2D55,#FF6B00);border-radius:3px;transition:width .6s ease;}
.lpct{font-family:'Space Mono',monospace;font-size:11px;color:var(--mut);margin-top:8px;}
.pscreen{min-height:100vh;background:var(--bg);padding-bottom:40px;animation:fadeIn .4s ease;}
@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}
.ps-top{padding:18px 20px 0;display:flex;align-items:center;gap:14px;}
.ps-back{background:var(--s1);border:1px solid var(--bdr);border-radius:10px;padding:8px 14px;font-family:'Space Mono',monospace;font-size:11px;color:var(--txt);cursor:pointer;}
.ps-ttl{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:1px;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.ps-body{max-width:480px;margin:0 auto;padding:22px 20px;}
.phone-wrap{display:flex;justify-content:center;margin-bottom:24px;}
.phone{width:180px;background:#0a0a0c;border:2px solid #252530;border-radius:30px;padding:8px;box-shadow:0 20px 60px rgba(0,0,0,.6);}
.phone-notch{width:46px;height:5px;background:#252530;border-radius:3px;margin:0 auto 8px;}
.phone-screen{border-radius:18px;overflow:hidden;aspect-ratio:9/16;position:relative;background:#0a0a12;}
.phone-screen canvas{width:100%;height:100%;display:block;}
.phone-tktk{position:absolute;right:6px;bottom:30px;display:flex;flex-direction:column;gap:5px;align-items:center;z-index:3;pointer-events:none;}
.phone-tktk-b{font-size:13px;line-height:1;}
.phone-tktk-c{font-family:'Space Mono',monospace;font-size:8px;color:rgba(255,255,255,.6);}
.score-row{display:flex;justify-content:space-between;align-items:flex-end;margin-bottom:14px;}
.score-lbl{font-family:'Space Mono',monospace;font-size:10px;color:var(--mut);letter-spacing:1px;margin-bottom:4px;}
.score-num{font-family:'Bebas Neue',sans-serif;font-size:38px;background:linear-gradient(135deg,#FF2D55,#FF6B00);-webkit-background-clip:text;-webkit-text-fill-color:transparent;}
.dur-num{font-family:'Bebas Neue',sans-serif;font-size:26px;color:var(--org);}
.mtags{display:flex;gap:7px;flex-wrap:wrap;margin-bottom:16px;}
.mtag{font-family:'Space Mono',monospace;font-size:10px;padding:4px 10px;border-radius:5px;background:var(--s2);border:1px solid var(--bdr);color:var(--mut);}
.mtag.hi{border-color:var(--org);color:var(--org);}
.mrow{display:flex;align-items:center;gap:12px;padding:12px 14px;background:var(--s1);border:1px solid var(--bdr);border-radius:10px;margin-bottom:12px;}
.minfo{flex:1;}.mname{font-size:13px;font-weight:500;}.mdesc{font-size:11px;color:var(--mut);margin-top:2px;}
.wform{display:flex;gap:2px;align-items:center;height:20px;}
.wb{width:3px;background:var(--red);border-radius:2px;animation:wv 1.2s ease infinite;}
.wb:nth-child(1){height:7px;animation-delay:0s;}.wb:nth-child(2){height:13px;animation-delay:.1s;}.wb:nth-child(3){height:9px;animation-delay:.2s;}.wb:nth-child(4){height:17px;animation-delay:.3s;}.wb:nth-child(5){height:11px;animation-delay:.4s;}.wb:nth-child(6){height:15px;animation-delay:.5s;}.wb:nth-child(7){height:7px;animation-delay:.6s;}
@keyframes wv{0%,100%{transform:scaleY(1);}50%{transform:scaleY(.4);}}
.scard{background:var(--s1);border:1px solid var(--bdr);border-radius:14px;overflow:hidden;margin-bottom:12px;}
.scard-h{padding:11px 16px;background:var(--s2);font-family:'Space Mono',monospace;font-size:10px;letter-spacing:1px;text-transform:uppercase;color:var(--mut);border-bottom:1px solid var(--bdr);display:flex;justify-content:space-between;}
.scard-b{padding:16px;}
.si{display:flex;gap:12px;margin-bottom:12px;}
.si:last-child{margin-bottom:0;}
.sn{font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--red);flex-shrink:0;width:22px;line-height:1.2;}
.st{font-family:'Space Mono',monospace;font-size:10px;color:var(--org);margin-bottom:3px;}
.sv{font-size:13px;line-height:1.55;}
.sc{font-size:11px;color:var(--mut);margin-top:3px;font-style:italic;}
.htags{display:flex;flex-wrap:wrap;gap:6px;padding:12px 14px;background:var(--s1);border:1px solid var(--bdr);border-radius:10px;margin-bottom:18px;}
.htag{font-family:'Space Mono',monospace;font-size:11px;color:var(--tk);background:rgba(0,242,234,.08);padding:3px 8px;border-radius:4px;cursor:pointer;}
.exp-section{display:flex;flex-direction:column;gap:10px;}
.exp-lbl{font-family:'Space Mono',monospace;font-size:10px;letter-spacing:2px;color:var(--mut);text-transform:uppercase;margin-bottom:2px;}
.ebtn{width:100%;padding:16px;border-radius:14px;border:none;cursor:pointer;font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:1px;display:flex;align-items:center;justify-content:center;gap:10px;}
.ebtn:disabled{opacity:.55;cursor:not-allowed;}
.ebtn.epro{background:linear-gradient(135deg,#FF2D55,#FF6B00);color:#fff;}
.ebtn.efree{background:var(--s1);border:1px solid var(--bdr);color:var(--txt);font-size:15px;}
.ebtn.ereset{background:transparent;border:1px solid var(--bdr);color:var(--mut);font-size:14px;padding:12px;}
.ebtn.eclips{background:var(--s2);border:2px solid var(--tk);color:var(--tk);font-size:16px;}
.exp-note{font-size:11px;color:var(--mut);text-align:center;font-family:'Space Mono',monospace;}
.exp-note span{color:var(--org);cursor:pointer;}
.rprog{background:var(--s1);border:1px solid var(--bdr);border-radius:12px;padding:14px;}
.rprog-lbl{font-family:'Space Mono',monospace;font-size:11px;color:var(--red);margin-bottom:10px;letter-spacing:1px;}
.rprog-bar{height:3px;background:var(--bdr);border-radius:3px;overflow:hidden;margin-bottom:6px;}
.rprog-fill{height:100%;background:linear-gradient(90deg,#FF2D55,#FF6B00);border-radius:3px;transition:width .3s ease;}
.rprog-pct{font-family:'Space Mono',monospace;font-size:10px;color:var(--mut);}
.ovl{position:fixed;inset:0;background:rgba(0,0,0,.88);backdrop-filter:blur(10px);z-index:500;display:flex;align-items:flex-end;justify-content:center;animation:fadeIn .2s ease;}
.modal{background:var(--s1);border:1px solid #252530;border-radius:28px 28px 0 0;padding:24px 24px 48px;width:100%;max-width:480px;max-height:92vh;overflow-y:auto;animation:slideUp .3s ease;}
@keyframes slideUp{from{transform:translateY(50px);opacity:0;}to{transform:translateY(0);opacity:1;}}
.mhandle{width:36px;height:4px;background:#2a2a36;border-radius:2px;margin:0 auto 24px;}
.mtitle{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:1px;margin-bottom:6px;}
.msub{font-size:14px;color:var(--mut);margin-bottom:26px;line-height:1.6;}
.abtn{width:100%;padding:15px;border-radius:12px;border:1px solid var(--bdr);background:var(--s2);color:var(--txt);font-family:'DM Sans',sans-serif;font-size:14px;font-weight:600;cursor:pointer;display:flex;align-items:center;gap:12px;margin-bottom:10px;}
.abtn.google{border-color:rgba(66,133,244,.4);background:rgba(66,133,244,.07);}
.abtn.tktk{border-color:rgba(0,242,234,.35);background:rgba(0,242,234,.06);}
.ai{width:26px;height:26px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0;}
.dvdr{display:flex;align-items:center;gap:12px;margin:16px 0;color:var(--mut);font-size:12px;}
.dvdr::before,.dvdr::after{content:'';flex:1;height:1px;background:var(--bdr);}
.ef{width:100%;padding:13px 16px;background:var(--s2);border:1px solid var(--bdr);border-radius:10px;color:var(--txt);font-family:'DM Sans',sans-serif;font-size:14px;outline:none;margin-bottom:10px;}
.ef::placeholder{color:var(--mut);}
.ef:focus{border-color:var(--red);}
.acta{width:100%;padding:15px;background:linear-gradient(135deg,#FF2D55,#FF6B00);border:none;border-radius:12px;color:#fff;font-family:'Bebas Neue',sans-serif;font-size:19px;letter-spacing:1px;cursor:pointer;margin-bottom:10px;display:block;}
.aswitch{text-align:center;font-size:13px;color:var(--mut);cursor:pointer;margin-bottom:4px;}
.aswitch span{color:var(--red);}
.dismiss{width:100%;padding:12px;background:transparent;border:none;color:var(--mut);font-family:'DM Sans',sans-serif;font-size:13px;cursor:pointer;display:block;}
.mcta{width:100%;padding:16px;background:linear-gradient(135deg,#FF2D55,#FF6B00);border:none;border-radius:12px;color:#fff;font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:1px;cursor:pointer;margin-bottom:10px;display:block;}
.perks{list-style:none;display:flex;flex-direction:column;gap:7px;margin:14px 0;}
.perks li{display:flex;align-items:center;gap:9px;font-size:13px;}
.perks li::before{content:'✓';color:var(--grn);font-weight:700;font-size:12px;}
.pcards{display:flex;flex-direction:column;gap:10px;margin-bottom:20px;}
.pcard{border:1px solid var(--bdr);border-radius:14px;padding:16px;position:relative;}
.pcard.pop{border-color:var(--red);background:rgba(255,45,85,.05);}
.pbadge2{position:absolute;top:-10px;left:16px;background:var(--red);font-family:'Space Mono',monospace;font-size:10px;padding:3px 10px;border-radius:10px;letter-spacing:1px;color:#fff;}
.pname{font-weight:600;font-size:15px;margin-bottom:2px;}
.pprice{font-family:'Bebas Neue',sans-serif;font-size:28px;letter-spacing:1px;}
.pprice small{font-family:'DM Sans',sans-serif;font-size:13px;color:var(--mut);font-weight:300;}
.pperks{font-size:12px;color:var(--mut);margin-top:4px;}
.page{padding:24px 20px 100px;animation:fadeIn .3s ease;}
.ptitle{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:1px;margin-bottom:5px;}
.psub{font-size:13px;color:var(--mut);margin-bottom:20px;}
.trow{display:flex;flex-direction:column;gap:10px;}
.tcard{background:var(--s1);border:1px solid var(--bdr);border-radius:14px;padding:16px;display:flex;align-items:center;gap:14px;cursor:pointer;}
.tcard:hover{border-color:var(--red);background:var(--s2);}
.trank{font-family:'Bebas Neue',sans-serif;font-size:28px;color:var(--red);flex-shrink:0;width:34px;line-height:1;}
.tinfo{flex:1;}.ttitle{font-size:14px;font-weight:600;margin-bottom:3px;}.tmeta{font-size:11px;color:var(--mut);font-family:'Space Mono',monospace;}
.tuse{font-size:11px;padding:7px 12px;border-radius:7px;background:rgba(255,45,85,.1);border:1px solid rgba(255,45,85,.3);color:var(--red);cursor:pointer;font-weight:600;flex-shrink:0;}
.vgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;}
.vt{aspect-ratio:9/16;border-radius:10px;position:relative;overflow:hidden;cursor:pointer;border:1px solid var(--bdr);}
.vo{position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,.85) 0%,transparent 55%);display:flex;flex-direction:column;justify-content:flex-end;padding:8px;}
.vttl{font-family:'Bebas Neue',sans-serif;font-size:11px;color:#fff;line-height:1.2;}
.vvws{font-family:'Space Mono',monospace;font-size:9px;color:rgba(255,255,255,.55);margin-top:2px;}
.vb{position:absolute;top:7px;left:7px;font-family:'Space Mono',monospace;font-size:9px;padding:2px 6px;border-radius:4px;}
.vb.tk{background:rgba(0,242,234,.2);color:var(--tk);border:1px solid rgba(0,242,234,.3);}
.vb.yt{background:rgba(255,0,0,.2);color:#ff6666;border:1px solid rgba(255,0,0,.3);}
.g1{background:linear-gradient(135deg,#1a0a2e,#2d1645,#0f0a1a);}.g2{background:linear-gradient(135deg,#2d1b1b,#3d1515,#5a1a1a);}.g3{background:linear-gradient(135deg,#0f2027,#203a43,#2c5364);}.g4{background:linear-gradient(135deg,#1a2a1a,#162616,#0f3a10);}.g5{background:linear-gradient(135deg,#1f0a1f,#2d0a3a,#40096e);}.g6{background:linear-gradient(135deg,#1a1500,#2d2200,#5a4400);}
.empty{text-align:center;padding:48px 20px;}
.toast{position:fixed;bottom:96px;left:50%;transform:translateX(-50%);background:var(--s2);border:1px solid var(--grn);border-radius:10px;padding:10px 22px;font-size:13px;font-weight:500;color:var(--grn);z-index:999;white-space:nowrap;pointer-events:none;animation:toastIn .3s ease;}
@keyframes toastIn{from{opacity:0;transform:translateX(-50%) translateY(8px);}to{opacity:1;transform:translateX(-50%) translateY(0);}}

/* Clips Modal Styles */
.clips-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:16px;}
.clip-slot{aspect-ratio:9/16;border-radius:10px;border:2px dashed var(--bdr);background:var(--s2);display:flex;flex-direction:column;align-items:center;justify-content:center;cursor:pointer;position:relative;overflow:hidden;transition:.2s;}
.clip-slot:hover{border-color:var(--tk);background:rgba(0,242,234,.05);}
.clip-slot.filled{border-style:solid;border-color:var(--tk);}
.clip-slot img{width:100%;height:100%;object-fit:cover;position:absolute;inset:0;}
.clip-slot video{width:100%;height:100%;object-fit:cover;position:absolute;inset:0;}
.clip-slot-icon{font-size:22px;margin-bottom:4px;z-index:1;}
.clip-slot-lbl{font-family:'Space Mono',monospace;font-size:9px;color:var(--mut);z-index:1;text-align:center;}
.clip-remove{position:absolute;top:4px;right:4px;width:18px;height:18px;border-radius:50%;background:rgba(255,45,85,.85);border:none;color:#fff;font-size:11px;cursor:pointer;display:flex;align-items:center;justify-content:center;z-index:10;line-height:1;}
.clip-scene-lbl{font-family:'Space Mono',monospace;font-size:9px;color:var(--tk);margin-top:4px;text-align:center;background:rgba(0,242,234,.08);padding:2px 6px;border-radius:4px;}
.clips-info{background:rgba(0,242,234,.06);border:1px solid rgba(0,242,234,.2);border-radius:10px;padding:12px;margin-bottom:14px;font-size:12px;color:var(--tk);line-height:1.5;}
.clips-count{font-family:'Space Mono',monospace;font-size:10px;color:var(--mut);margin-bottom:10px;}
.clips-count span{color:var(--tk);}
`;

const STYLE_OPTS=[{id:"cinematic",e:"🎬",l:"Cinematic"},{id:"vlog",e:"📱",l:"Vlog"},{id:"horror",e:"😱",l:"Horror"},{id:"aesthetic",e:"✨",l:"Aesthetic"},{id:"comedy",e:"😂",l:"Comedy"},{id:"motivational",e:"💪",l:"Motivational"}];
const SAMPLE_PROMPTS=["POV: gym comeback after 3 months","Turn my week into a movie trailer","main character morning routine","NYC day in my life cinematic","glow up transformation reveal"];
const GEN_STEPS=[{l:"Analyzing your prompt",i:"🧠"},{l:"Writing script & voiceover",i:"✍️"},{l:"Timing scenes",i:"⏱"},{l:"Selecting music style",i:"🎵"},{l:"Generating captions",i:"💬"},{l:"Preparing video preview",i:"🎬"}];
const TRENDING=[{rank:1,title:"POV: main character energy ✨",views:"284M",sound:"Cinematic Epic"},{rank:2,title:"my week as a movie trailer 🎬",views:"198M",sound:"Dramatic Strings"},{rank:3,title:"gym comeback arc 💪",views:"156M",sound:"Trap Motivation"},{rank:4,title:"day in my life: aesthetic edition",views:"134M",sound:"Lo-fi Chill"},{rank:5,title:"things that just make sense 🫶",views:"112M",sound:"Trending Audio"},{rank:6,title:"glow up check 🔥 (watch till end)",views:"97M",sound:"Emotional Buildup"}];
const PAST=[{title:"gym comeback",g:"g1",views:"12.4K",p:"tk"},{title:"movie trailer week",g:"g2",views:"8.1K",p:"yt"},{title:"morning routine",g:"g3",views:"31K",p:"tk"},{title:"NYC day",g:"g4",views:"5.2K",p:"tk"},{title:"glow up",g:"g5",views:"44.7K",p:"yt"},{title:"bestie trip",g:"g6",views:"9.8K",p:"tk"}];
const PALETTES=[{bg1:"#1a0a2e",bg2:"#0f0a1a",accent:"#FF2D55"},{bg1:"#0f2027",bg2:"#0a1520",accent:"#00F2EA"},{bg1:"#2d1515",bg2:"#1a0a0a",accent:"#FF6B00"},{bg1:"#0f1a2e",bg2:"#0a1020",accent:"#4488FF"}];

const GSvg=()=>(
  <svg width="18" height="18" viewBox="0 0 18 18">
    <path d="M17.64 9.2c0-.638-.057-1.252-.164-1.84H9v3.48h4.844c-.209 1.125-.843 2.078-1.796 2.717v2.258h2.908C16.658 14.013 17.64 11.706 17.64 9.2z" fill="#4285F4"/>
    <path d="M9 18c2.43 0 4.467-.806 5.956-2.18l-2.908-2.259c-.806.54-1.837.86-3.048.86-2.344 0-4.328-1.584-5.036-3.711H.957v2.332A8.997 8.997 0 009 18z" fill="#34A853"/>
    <path d="M3.964 10.71A5.41 5.41 0 013.682 9c0-.593.102-1.17.282-1.71V4.958H.957A8.996 8.996 0 000 9c0 1.452.348 2.827.957 4.042l3.007-2.332z" fill="#FBBC05"/>
    <path d="M9 3.58c1.321 0 2.508.454 3.44 1.345l2.582-2.58C13.463.891 11.426 0 9 0A8.997 8.997 0 00.957 4.958L3.964 7.29C4.672 5.163 6.656 3.58 9 3.58z" fill="#EA4335"/>
  </svg>
);

// Wrap text helper — splits text into lines that fit within maxWidth
function wrapText(ctx, text, maxWidth) {
  const words = text.split(" ");
  const lines = [];
  let current = "";
  for (const w of words) {
    const test = current ? current + " " + w : w;
    if (ctx.measureText(test).width > maxWidth && current) {
      lines.push(current);
      current = w;
    } else {
      current = test;
    }
  }
  if (current) lines.push(current);
  return lines;
}

function PreviewCanvas({result, clips}){
  const ref=useRef(null);
  const raf=useRef(null);
  const t0=useRef(null);
  // Preload clip images
  const imgCache = useRef({});

  useEffect(()=>{
    if(!clips) return;
    clips.forEach((c,i)=>{
      if(c && c.type==="image" && c.url && !imgCache.current[i]){
        const img = new Image();
        img.src = c.url;
        imgCache.current[i] = img;
      }
    });
  },[clips]);

  useEffect(()=>{
    const canvas=ref.current;
    if(!canvas||!result)return;
    const ctx=canvas.getContext("2d");
    const W=canvas.width,H=canvas.height;
    const durs=result.scenes.map(sc=>{
      const m=sc.timing&&sc.timing.match(/(\d+):(\d+)-(\d+):(\d+)/);
      if(m)return Math.max(2,parseInt(m[3])*60+parseInt(m[4])-parseInt(m[1])*60-parseInt(m[2]));
      return 8;
    });
    const total=durs.reduce((a,b)=>a+b,0);
    function getScene(elapsed){
      let t=elapsed%total;
      for(let i=0;i<durs.length;i++){
        if(t<durs[i])return{s:result.scenes[i],prog:t/durs[i],idx:i};
        t-=durs[i];
      }
      return{s:result.scenes[0],prog:0,idx:0};
    }
    function frame(ts){
      if(!t0.current)t0.current=ts;
      const elapsed=(ts-t0.current)/1000;
      const{s,prog,idx}=getScene(elapsed);
      const pal=PALETTES[idx%PALETTES.length];
      ctx.clearRect(0,0,W,H);

      // Draw clip image if available for this scene
      const clipImg = imgCache.current[idx];
      if(clipImg && clipImg.complete && clipImg.naturalWidth > 0){
        ctx.save();
        ctx.drawImage(clipImg,0,0,W,H);
        // Dark overlay for readability
        const ov=ctx.createLinearGradient(0,0,0,H);
        ov.addColorStop(0,"rgba(0,0,0,0.35)");
        ov.addColorStop(0.5,"rgba(0,0,0,0.15)");
        ov.addColorStop(1,"rgba(0,0,0,0.75)");
        ctx.fillStyle=ov;ctx.fillRect(0,0,W,H);
        ctx.restore();
      } else {
        // Gradient background fallback
        const grd=ctx.createLinearGradient(0,0,W*0.4,H);
        grd.addColorStop(0,pal.bg1);grd.addColorStop(1,pal.bg2);
        ctx.fillStyle=grd;ctx.fillRect(0,0,W,H);
        // Waveform bars
        const bars=14,bw=5,gap=3;
        const sx=(W-bars*(bw+gap))/2,cy=H*0.74;
        ctx.globalAlpha=0.65;
        for(let i=0;i<bars;i++){
          const bh=8+Math.abs(Math.sin(elapsed*4+i*0.5))*18+Math.sin(elapsed*7+i)*6;
          const g2=ctx.createLinearGradient(0,cy-bh/2,0,cy+bh/2);
          g2.addColorStop(0,pal.accent);g2.addColorStop(1,pal.accent+"44");
          ctx.fillStyle=g2;ctx.fillRect(sx+i*(bw+gap),cy-bh/2,bw,bh);
        }
        ctx.globalAlpha=1;
      }

      // Caption text — FIX: use word-wrap, limit font size, constrain to canvas
      const fadeIn=Math.min(1,prog*6);
      if(fadeIn>0){
        ctx.save();
        ctx.globalAlpha=fadeIn;
        // Choose font size that fits
        const maxW = W * 0.82;
        let fontSize = Math.floor(H * 0.048);
        ctx.font = `bold ${fontSize}px Arial, sans-serif`;
        // Scale down if needed
        const raw = (s.caption||"").toUpperCase();
        while(fontSize > 10 && ctx.measureText(raw).width > maxW * 1.5){ 
          fontSize -= 2;
          ctx.font = `bold ${fontSize}px Arial, sans-serif`;
        }
        ctx.textAlign="center";
        ctx.textBaseline="middle";
        ctx.shadowColor="rgba(0,0,0,0.95)";
        ctx.shadowBlur=12;
        // Wrap text
        const lines = wrapText(ctx, raw, maxW);
        const lineH = fontSize * 1.25;
        const totalH = lines.length * lineH;
        const startY = H * 0.84 - totalH / 2 + lineH / 2;
        // Draw background pill for legibility
        const padX = 14, padY = 8;
        const blockW = Math.min(maxW + padX*2, W - 20);
        const blockH = totalH + padY*2;
        const blockX = (W - blockW)/2;
        const blockY = startY - lineH/2 - padY;
        ctx.fillStyle="rgba(0,0,0,0.45)";
        ctx.beginPath();
        ctx.roundRect(blockX,blockY,blockW,blockH,8);
        ctx.fill();
        ctx.fillStyle="#fff";
        lines.forEach((line,i)=>ctx.fillText(line, W/2, startY + i*lineH));
        ctx.restore();
      }

      // Progress bar
      const bw2=(W*0.6)*prog;
      ctx.globalAlpha=0.7;ctx.fillStyle=pal.accent;
      ctx.fillRect((W-W*0.6)/2,H*0.91,bw2,3);
      ctx.globalAlpha=1;
      raf.current=requestAnimationFrame(frame);
    }
    raf.current=requestAnimationFrame(frame);
    return()=>{if(raf.current)cancelAnimationFrame(raf.current);};
  },[result, clips]);
  return <canvas ref={ref} width={270} height={480} style={{width:"100%",height:"100%",display:"block"}}/>;
}

async function renderVideo(result, watermark, onPct, clips){
  return new Promise(async(resolve,reject)=>{
    try{
      const W=1080,H=1920,FPS=24;
      const canvas=document.createElement("canvas");
      canvas.width=W;canvas.height=H;
      const ctx=canvas.getContext("2d");

      // Preload clip images
      const loadedImgs = [];
      for(let i=0;i<result.scenes.length;i++){
        const c = clips && clips[i];
        if(c && c.type==="image" && c.url){
          await new Promise(res=>{
            const img=new Image();
            img.onload=()=>{loadedImgs[i]=img;res();};
            img.onerror=()=>{loadedImgs[i]=null;res();};
            img.src=c.url;
          });
        } else {
          loadedImgs[i]=null;
        }
      }

      const mimes=["video/webm;codecs=vp9","video/webm;codecs=vp8","video/webm"];
      let mime="video/webm";
      for(const m of mimes){try{if(MediaRecorder.isTypeSupported(m)){mime=m;break;}}catch(e){}}
      const stream=canvas.captureStream(FPS);
      const chunks=[];
      const rec=new MediaRecorder(stream,{mimeType:mime,videoBitsPerSecond:3000000});
      rec.ondataavailable=e=>{if(e.data&&e.data.size>0)chunks.push(e.data);};
      rec.onerror=e=>reject(e);
      rec.onstop=()=>{const blob=new Blob(chunks,{type:mime});resolve({url:URL.createObjectURL(blob),blob,mime});};
      rec.start(200);
      const durs=result.scenes.map(sc=>{
        const m=sc.timing&&sc.timing.match(/(\d+):(\d+)-(\d+):(\d+)/);
        if(m)return Math.max(2,parseInt(m[3])*60+parseInt(m[4])-parseInt(m[1])*60-parseInt(m[2]));
        return 7;
      });
      const totalFrames=durs.reduce((a,b)=>a+b,0)*FPS;
      let done=0;
      for(let si=0;si<result.scenes.length;si++){
        const scene=result.scenes[si];
        const pal=PALETTES[si%PALETTES.length];
        const sceneFr=durs[si]*FPS;
        const img=loadedImgs[si];
        for(let f=0;f<sceneFr;f++){
          const t=f/FPS,prog=f/sceneFr;
          ctx.clearRect(0,0,W,H);

          if(img){
            ctx.drawImage(img,0,0,W,H);
            const ov=ctx.createLinearGradient(0,0,0,H);
            ov.addColorStop(0,"rgba(0,0,0,0.4)");
            ov.addColorStop(1,"rgba(0,0,0,0.75)");
            ctx.fillStyle=ov;ctx.fillRect(0,0,W,H);
          } else {
            const grd=ctx.createLinearGradient(0,0,W*0.5,H);
            grd.addColorStop(0,pal.bg1);grd.addColorStop(1,pal.bg2);
            ctx.fillStyle=grd;ctx.fillRect(0,0,W,H);
            const bars=28,bw=22,gap=10;
            const sx=(W-bars*(bw+gap))/2,cy=H*0.72;
            ctx.globalAlpha=0.6;
            for(let i=0;i<bars;i++){
              const bh=50+Math.abs(Math.sin(t*4+i*0.45))*130+Math.sin(t*7+i)*28;
              const g2=ctx.createLinearGradient(0,cy-bh/2,0,cy+bh/2);
              g2.addColorStop(0,pal.accent);g2.addColorStop(1,pal.accent+"44");
              ctx.fillStyle=g2;ctx.fillRect(sx+i*(bw+gap),cy-bh/2,bw,bh);
            }
            ctx.globalAlpha=1;
          }

          // Caption — fixed word wrap
          const alpha=Math.min(1,prog*5);
          if(alpha>0){
            ctx.save();ctx.globalAlpha=alpha;
            const maxCW = W - 160;
            let fSize = 96;
            ctx.font=`bold ${fSize}px Arial, sans-serif`;
            const rawCap=(scene.caption||"").toUpperCase();
            while(fSize>36 && ctx.measureText(rawCap).width > maxCW*1.4){
              fSize-=4;
              ctx.font=`bold ${fSize}px Arial, sans-serif`;
            }
            ctx.textAlign="center";ctx.textBaseline="middle";
            ctx.shadowColor="rgba(0,0,0,0.95)";ctx.shadowBlur=30;
            const lines=wrapText(ctx, rawCap, maxCW);
            const lineH=fSize*1.3;
            const totalCH=lines.length*lineH;
            const sY=H*0.80-totalCH/2+lineH/2;
            // Background pill
            const bpW=maxCW+60,bpH=totalCH+40;
            ctx.fillStyle="rgba(0,0,0,0.5)";
            ctx.beginPath();ctx.roundRect((W-bpW)/2,sY-lineH/2-20,bpW,bpH,16);ctx.fill();
            ctx.fillStyle="#fff";
            lines.forEach((l,i)=>ctx.fillText(l,W/2,sY+i*lineH));
            ctx.restore();
          }

          ctx.globalAlpha=0.75;ctx.fillStyle=pal.accent;
          ctx.fillRect((W-W*0.55)/2,H*0.90,W*0.55*prog,6);
          ctx.globalAlpha=1;
          ctx.font="bold 36px monospace";ctx.fillStyle="rgba(255,255,255,0.35)";
          ctx.textAlign="right";ctx.textBaseline="top";
          ctx.fillText((si+1)+"/"+result.scenes.length,W-60,70);
          if(watermark){
            ctx.save();ctx.font="bold 52px Arial, sans-serif";
            ctx.fillStyle="rgba(255,255,255,0.18)";
            ctx.textAlign="center";ctx.textBaseline="middle";
            ctx.translate(W/2,H/2);ctx.rotate(-Math.PI/7);
            ctx.fillText("VIRALCUT.APP",0,0);ctx.restore();
          }
          done++;
          if(f%FPS===0){onPct(Math.round((done/totalFrames)*100));await new Promise(r=>setTimeout(r,0));}
        }
      }
      onPct(100);rec.stop();
    }catch(err){reject(err);}
  });
}

// Save to Camera Roll / Photos (iOS share sheet or Android)
async function saveToPhotos(url, blob, mime, filename, showToast) {
  // Try Web Share API first (mobile — triggers "Save to Photos" on iOS/Android)
  if (navigator.share && navigator.canShare) {
    try {
      const ext = mime.includes("mp4") ? "mp4" : "webm";
      const file = new File([blob], `${filename}.${ext}`, {type: mime});
      if (navigator.canShare({files: [file]})) {
        await navigator.share({
          files: [file],
          title: "ViralCut Video",
        });
        showToast("Shared! Save to Photos from the share sheet 📸");
        return;
      }
    } catch(e) {
      if (e.name !== "AbortError") {
        // Fall through to download
      } else {
        return; // User cancelled
      }
    }
  }

  // Try using <a download> with a video tag + prompt
  const a = document.createElement("a");
  const ext = mime.includes("mp4") ? "mp4" : "webm";
  a.href = url;
  a.download = `${filename}.${ext}`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  showToast("Video saved! Check your Downloads or Files app 📱");
}

export default function App(){
  const[tab,setTab]=useState("create");
  const[prompt,setPrompt]=useState("");
  const[selStyle,setStyle]=useState("cinematic");
  const[used,setUsed]=useState(1);
  const[screen,setScreen]=useState("home");
  const[genStep,setGenStep]=useState(0);
  const[result,setResult]=useState(null);
  const[rendering,setRend]=useState(false);
  const[rendPct,setRendPct]=useState(0);
  const[rendMode,setRendMode]=useState(null);
  const[modal,setModal]=useState(null);
  const[authMode,setAuth]=useState("login");
  const[user,setUser]=useState(null);
  const[toast,setToast]=useState(null);
  const[clips,setClips]=useState([]); // Array of {url, type, name} per scene slot
  const fileInputRef=useRef(null);
  const activeSlotRef=useRef(null);

  const showToast=msg=>{setToast(msg);setTimeout(()=>setToast(null),3500);};

  const generate=async()=>{
    if(!prompt.trim())return;
    if(used>=3&&!user?.pro){setModal("pro");return;}
    setScreen("loading");setGenStep(0);setClips([]);
    for(let i=0;i<GEN_STEPS.length;i++){
      await new Promise(r=>setTimeout(r,600+Math.random()*400));
      setGenStep(i+1);
    }
    let data=null;
    try{
      const res=await fetch("https://api.anthropic.com/v1/messages",{
        method:"POST",headers:{"Content-Type":"application/json"},
        body:JSON.stringify({model:"claude-sonnet-4-20250514",max_tokens:1000,messages:[{role:"user",content:
          'Generate a viral TikTok/YouTube Shorts video script for: "'+prompt+'". Style: '+selStyle+'.\nRespond ONLY with valid JSON and nothing else:\n{"title":"CAPS TITLE MAX 8 WORDS","duration":"X seconds","viralScore":88,"scenes":[{"num":1,"timing":"0:00-0:08","voiceover":"Voiceover text.","caption":"CAPTION TEXT"},{"num":2,"timing":"0:08-0:18","voiceover":"Voiceover text.","caption":"CAPTION TEXT"},{"num":3,"timing":"0:18-0:28","voiceover":"Voiceover text.","caption":"CAPTION TEXT"},{"num":4,"timing":"0:28-0:35","voiceover":"Voiceover text.","caption":"CAPTION TEXT"}],"musicStyle":"genre bpm mood","musicName":"Track Name","hashtags":["#tag1","#tag2","#tag3","#tag4","#tag5","#tag6"]}'
        }]})
      });
      const json=await res.json();
      const raw=json.content[0].text.replace(/```json|```/g,"").trim();
      data=JSON.parse(raw);
    }catch(e){
      data={title:prompt.toUpperCase().slice(0,40),duration:"32 seconds",viralScore:88,
        scenes:[
          {num:1,timing:"0:00-0:08",voiceover:"It starts with one decision. A moment that changes everything.",caption:"THE DECISION"},
          {num:2,timing:"0:08-0:18",voiceover:"Everyone said it wasn't possible. You didn't come this far to quit.",caption:"THEY SAID NO"},
          {num:3,timing:"0:18-0:28",voiceover:"Watch what happens when you stop caring about the noise.",caption:"WATCH THIS"},
          {num:4,timing:"0:28-0:35",voiceover:"This is your moment. Own every second of it.",caption:"YOUR MOMENT"},
        ],
        musicStyle:"Orchestral hip-hop, 140bpm, cinematic",musicName:"Rise Up — Cinematic Trap",
        hashtags:["#viral","#fyp","#cinematic","#foryou","#trending","#mindset"]};
    }
    setResult(data);setUsed(v=>v+1);setScreen("preview");
  };

  const handleFileSelect=(e)=>{
    const file=e.target.files&&e.target.files[0];
    if(!file||activeSlotRef.current===null)return;
    const url=URL.createObjectURL(file);
    const type=file.type.startsWith("video")?"video":"image";
    const idx=activeSlotRef.current;
    setClips(prev=>{
      const next=[...prev];
      next[idx]={url,type,name:file.name};
      return next;
    });
    e.target.value="";
  };

  const openClipPicker=(idx)=>{
    activeSlotRef.current=idx;
    fileInputRef.current&&fileInputRef.current.click();
  };

  const removeClip=(idx,e)=>{
    e.stopPropagation();
    setClips(prev=>{
      const next=[...prev];
      if(next[idx]?.url)URL.revokeObjectURL(next[idx].url);
      next[idx]=null;
      return next;
    });
  };

  const exportVideo=async(watermark)=>{
    if(!result)return;
    setRend(true);setRendMode(watermark?"free":"pro");setRendPct(0);
    try{
      const {url, blob, mime}=await renderVideo(result,watermark,pct=>setRendPct(pct),clips);
      const filename="viralcut-"+result.title.toLowerCase().replace(/[^a-z0-9]+/g,"-").slice(0,30);
      await saveToPhotos(url,blob,mime,filename,showToast);
      URL.revokeObjectURL(url);
    }catch(e){console.error(e);showToast("Export failed — please try again");}
    setRend(false);setRendMode(null);setRendPct(0);
  };

  const loginWith=(name,email)=>{setUser({name,email,avatar:"🎬",pro:false});showToast("Signed in as "+name);setModal(null);};

  const clipsAdded=(clips||[]).filter(Boolean).length;

  if(screen==="loading")return(
    <><style>{CSS}</style>
    <div className="lscreen">
      <div className="licon">🎬</div>
      <div className="ltitle">CREATING YOUR VIDEO</div>
      <div className="lsub">AI is crafting your viral script…</div>
      <div className="lsteps">
        {GEN_STEPS.map((s,i)=>(
          <div key={i} className={"lstep"+(i<genStep?" done":i===genStep?" active":"")}>
            <span className="lstep-i">{i<genStep?"✓":s.i}</span>{s.l}
          </div>
        ))}
      </div>
      <div className="lbar"><div className="lfill" style={{width:Math.round((genStep/GEN_STEPS.length)*100)+"%"}}/></div>
      <div className="lpct">{Math.round((genStep/GEN_STEPS.length)*100)}%</div>
    </div></>
  );

  if(screen==="preview"&&result)return(
    <><style>{CSS}</style>
    {/* Hidden file input for clip picking */}
    <input
      ref={fileInputRef}
      type="file"
      accept="image/*,video/*"
      style={{display:"none"}}
      onChange={handleFileSelect}
    />
    <div className="pscreen">
      <div className="ps-top">
        <button className="ps-back" onClick={()=>{setScreen("home");setResult(null);}}>← BACK</button>
        <div className="ps-ttl">{result.title}</div>
      </div>
      <div className="ps-body">
        <div className="phone-wrap">
          <div className="phone">
            <div className="phone-notch"/>
            <div className="phone-screen">
              <PreviewCanvas result={result} clips={clips}/>
              <div className="phone-tktk">
                <div className="phone-tktk-b">❤️</div><div className="phone-tktk-c">214K</div>
                <div className="phone-tktk-b">💬</div><div className="phone-tktk-c">1.2K</div>
                <div className="phone-tktk-b">↗️</div>
              </div>
            </div>
          </div>
        </div>
        <div className="score-row">
          <div><div className="score-lbl">VIRAL SCORE</div><div className="score-num">{result.viralScore}/100</div></div>
          <div style={{textAlign:"right"}}><div className="score-lbl">DURATION</div><div className="dur-num">{result.duration}</div></div>
        </div>
        <div className="mtags">
          <span className="mtag">9:16 VERTICAL</span>
          <span className="mtag hi">🎬 {selStyle.toUpperCase()}</span>
          <span className="mtag">{result.scenes.length} SCENES</span>
          {clipsAdded>0&&<span className="mtag" style={{borderColor:"var(--tk)",color:"var(--tk)"}}>🎥 {clipsAdded} CLIPS</span>}
        </div>
        <div className="mrow">
          <span style={{fontSize:18}}>🎵</span>
          <div className="minfo"><div className="mname">{result.musicName}</div><div className="mdesc">{result.musicStyle}</div></div>
          <div className="wform">{[...Array(7)].map((_,i)=><div key={i} className="wb"/>)}</div>
        </div>
        <div className="scard">
          <div className="scard-h"><span>SCRIPT + CAPTIONS</span><span style={{color:"var(--red)"}}>{result.scenes.length} SCENES</span></div>
          <div className="scard-b">
            {result.scenes.map(sc=>(
              <div key={sc.num} className="si">
                <div className="sn">{sc.num}</div>
                <div><div className="st">{sc.timing}</div><div className="sv">{sc.voiceover}</div><div className="sc">"{sc.caption}"</div></div>
              </div>
            ))}
          </div>
        </div>
        <div className="htags">{result.hashtags.map(h=><span key={h} className="htag">{h}</span>)}</div>

        {/* Export section */}
        <div className="exp-section">
          <div className="exp-lbl">Enhance & Export</div>

          {/* ADD CLIPS BUTTON */}
          <button className="ebtn eclips" onClick={()=>setModal("clips")}>
            🎥 Add Clips{clipsAdded>0?` (${clipsAdded}/${result.scenes.length})`:""}
          </button>

          <button className="ebtn epro" disabled={rendering} onClick={()=>user?.pro?exportVideo(false):setModal("pro")}>
            {rendering&&rendMode==="pro"?"⏳ RENDERING "+rendPct+"%":user?.pro?"💾 SAVE TO PHOTOS — NO WATERMARK":"⚡ SAVE WITHOUT WATERMARK"}
          </button>
          {rendering&&rendMode==="pro"&&(
            <div className="rprog">
              <div className="rprog-lbl">RENDERING VIDEO — PLEASE WAIT</div>
              <div className="rprog-bar"><div className="rprog-fill" style={{width:rendPct+"%"}}/></div>
              <div className="rprog-pct">{rendPct}% complete · ~20 seconds total</div>
            </div>
          )}
          <button className="ebtn efree" disabled={rendering} onClick={()=>exportVideo(true)}>
            {rendering&&rendMode==="free"?"⏳ RENDERING "+rendPct+"%":"📱 FREE SAVE TO PHOTOS (WITH WATERMARK)"}
          </button>
          {rendering&&rendMode==="free"&&(
            <div className="rprog">
              <div className="rprog-lbl">RENDERING VIDEO — PLEASE WAIT</div>
              <div className="rprog-bar"><div className="rprog-fill" style={{width:rendPct+"%"}}/></div>
              <div className="rprog-pct">{rendPct}% complete · ~20 seconds total</div>
            </div>
          )}
          <div className="exp-note">
            {!user?.pro&&<>Remove watermark with <span onClick={()=>setModal("pro")}>Pro ⚡</span> · </>}
            On mobile: tap share → Save to Photos/Camera Roll
          </div>
          <button className="ebtn ereset" onClick={()=>{setScreen("home");setResult(null);}}>🔄 MAKE ANOTHER VIDEO</button>
        </div>
      </div>
    </div>

    {/* CLIPS MODAL */}
    {modal==="clips"&&(
      <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
        <div className="modal">
          <div className="mhandle"/>
          <div className="mtitle">ADD CLIPS 🎥</div>
          <div className="msub" style={{marginBottom:12}}>Add your photos or videos to each scene slot.</div>
          <div className="clips-info">
            Tap a scene slot to add a photo or video from your library. Your clips will appear in the preview and be included in the exported video.
          </div>
          <div className="clips-count">
            Added: <span>{clipsAdded}/{result.scenes.length} scenes</span>
          </div>
          <div className="clips-grid">
            {result.scenes.map((sc,i)=>{
              const clip=clips[i];
              return(
                <div key={i} style={{display:"flex",flexDirection:"column",alignItems:"center"}}>
                  <div
                    className={"clip-slot"+(clip?" filled":"")}
                    onClick={()=>openClipPicker(i)}
                  >
                    {clip?(
                      <>
                        {clip.type==="image"
                          ?<img src={clip.url} alt="clip" style={{position:"absolute",inset:0,width:"100%",height:"100%",objectFit:"cover"}}/>
                          :<video src={clip.url} style={{position:"absolute",inset:0,width:"100%",height:"100%",objectFit:"cover"}} muted playsInline autoPlay loop/>
                        }
                        <button className="clip-remove" onClick={(e)=>removeClip(i,e)}>×</button>
                      </>
                    ):(
                      <>
                        <span className="clip-slot-icon">📷</span>
                        <span className="clip-slot-lbl">Scene {sc.num}</span>
                      </>
                    )}
                  </div>
                  <div className="clip-scene-lbl">{sc.timing}</div>
                </div>
              );
            })}
          </div>
          <button className="mcta" onClick={()=>{setModal(null);showToast(clipsAdded>0?`${clipsAdded} clip${clipsAdded>1?"s":""} added to your video!`:"No clips added — using AI backgrounds");}}>
            {clipsAdded>0?`✓ USE ${clipsAdded} CLIP${clipsAdded>1?"S":""}` : "SKIP — USE AI BACKGROUNDS"}
          </button>
          <button className="dismiss" onClick={()=>setModal(null)}>Cancel</button>
        </div>
      </div>
    )}

    {modal==="pro"&&(
      <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
        <div className="modal">
          <div className="mhandle"/>
          <div className="mtitle">GO PRO ⚡</div>
          <div className="msub">Remove the watermark and unlock everything.</div>
          <ul className="perks">
            {["No watermark on exports","Unlimited daily videos","TikTok & YouTube direct posting","Premium styles","Priority AI generation"].map(p=><li key={p}>{p}</li>)}
          </ul>
          <div className="pcards">
            <div className="pcard pop"><div className="pbadge2">BEST VALUE</div>
              <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                <div><div className="pname">Pro Annual</div><div className="pperks">Save 50%</div></div>
                <div><div className="pprice">$4.99<small>/mo</small></div><div style={{fontSize:10,color:"var(--mut)",fontFamily:"Space Mono"}}>billed yearly</div></div>
              </div>
            </div>
            <div className="pcard">
              <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                <div><div className="pname">Pro Monthly</div><div className="pperks">Cancel anytime</div></div>
                <div className="pprice">$9.99<small>/mo</small></div>
              </div>
            </div>
          </div>
          <button className="mcta" onClick={()=>{if(!user){setModal("auth");return;}setUser(u=>({...u,pro:true}));setModal(null);showToast("Pro unlocked! No watermark.");}}>START 3-DAY FREE TRIAL</button>
          <button className="dismiss" onClick={()=>{setModal(null);exportVideo(true);}}>Download free version with watermark instead</button>
        </div>
      </div>
    )}
    {modal==="auth"&&(
      <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
        <div className="modal">
          <div className="mhandle"/>
          <div className="mtitle">SIGN IN</div>
          <div className="msub">Create an account to unlock Pro.</div>
          <button className="abtn google" onClick={()=>loginWith("Alex Rivera","alex@gmail.com")}>
            <div className="ai" style={{background:"#fff"}}><GSvg/></div>Continue with Google
          </button>
          <button className="abtn tktk" onClick={()=>loginWith("Creator","creator@tiktok.com")}>
            <div className="ai" style={{background:"rgba(0,242,234,.15)",color:"var(--tk)",fontWeight:900}}>♪</div>Continue with TikTok
          </button>
          <div className="dvdr">or email</div>
          <input className="ef" type="email" placeholder="Email address"/>
          <input className="ef" type="password" placeholder="Password"/>
          <button className="acta" onClick={()=>loginWith("Creator","creator@email.com")}>SIGN IN</button>
          <button className="dismiss" onClick={()=>setModal(null)}>Cancel</button>
        </div>
      </div>
    )}
    {toast&&<div className="toast">{toast}</div>}
    </>
  );

  return(
    <><style>{CSS}</style>
    <div>
      <nav className="nav">
        <div className="logo">VIRAL<em>CUT</em></div>
        <div className="nav-r">
          {user?.pro
            ?<span style={{fontFamily:"Space Mono,monospace",fontSize:10,background:"linear-gradient(135deg,#FF2D55,#FF6B00)",padding:"5px 12px",borderRadius:20,color:"#fff"}}>⚡ PRO</span>
            :<span className="free-chip">{Math.max(0,3-used)} FREE LEFT</span>}
          {!user?.pro&&<button className="pro-chip" onClick={()=>setModal("pro")}>GO PRO ⚡</button>}
          <button className="av-btn" onClick={()=>setModal(user?"quickprofile":"auth")}>
            {user?user.avatar:"👤"}{!user&&<span className="ndot"/>}
          </button>
        </div>
      </nav>

      {tab==="create"&&(
        <div className="pb">
          <div className="hero">
            <div className="hbadge"><span className="pulse"/>AI VIDEO GENERATOR</div>
            <h1>TYPE IT.<br/><span className="grad">GO VIRAL.</span></h1>
            <p className="hero-sub">Type a prompt → loading screen → live preview → real downloadable video.</p>
            <div className="pbadges">
              <span className="pbadge tk">♪ TikTok</span>
              <span className="pbadge yt">▶ YouTube Shorts</span>
              <span className="pbadge ig">◈ Reels</span>
            </div>
          </div>
          <div className="pwrap">
            <div className="pbox">
              <div className="pinr">
                <textarea className="pinput" placeholder='Try "POV: gym comeback after 3 months"…' value={prompt} rows={1}
                  onChange={e=>{setPrompt(e.target.value);e.target.style.height="auto";e.target.style.height=e.target.scrollHeight+"px";}}
                  onKeyDown={e=>{if(e.key==="Enter"&&!e.shiftKey){e.preventDefault();generate();}}}
                />
                <button className="gbtn" onClick={generate} disabled={!prompt.trim()}>CREATE</button>
              </div>
            </div>
            <div className="srow">
              {STYLE_OPTS.map(s=>(
                <button key={s.id} className={"spill"+(selStyle===s.id?" on":"")} onClick={()=>setStyle(s.id)}>{s.e} {s.l}</button>
              ))}
            </div>
            <div className="chips">
              {SAMPLE_PROMPTS.map(p=><button key={p} className="chip" onClick={()=>setPrompt(p)}>{p}</button>)}
            </div>
            {!user?.pro&&(
              <div className="cbar">
                <span className="clbl">DAILY VIDEOS USED</span>
                <div className="cdots">{[0,1,2].map(i=><div key={i} className={"cdot"+(i<used?" on":"")}/>)}</div>
              </div>
            )}
          </div>
        </div>
      )}

      {tab==="trending"&&(
        <div className="page">
          <div className="ptitle">TRENDING NOW 🔥</div>
          <div className="psub">Top formats going viral — tap to use.</div>
          <div className="trow">
            {TRENDING.map(t=>(
              <div key={t.rank} className="tcard" onClick={()=>{setPrompt(t.title);setTab("create");}}>
                <div className="trank">#{t.rank}</div>
                <div className="tinfo"><div className="ttitle">{t.title}</div><div className="tmeta">{t.views} views · 🎵 {t.sound}</div></div>
                <button className="tuse" onClick={e=>{e.stopPropagation();setPrompt(t.title);setTab("create");}}>USE ↗</button>
              </div>
            ))}
          </div>
        </div>
      )}

      {tab==="videos"&&(
        <div className="page">
          <div className="ptitle">MY VIDEOS</div>
          <div className="psub">Your generated videos.</div>
          {!user?(
            <div className="empty">
              <div style={{fontSize:48,marginBottom:14}}>🎬</div>
              <div style={{fontFamily:"'Bebas Neue',sans-serif",fontSize:22,marginBottom:8}}>SIGN IN TO SAVE VIDEOS</div>
              <div style={{fontSize:13,color:"var(--mut)",marginBottom:20}}>Your videos sync to your account anywhere.</div>
              <button className="acta" style={{width:"auto",padding:"12px 32px",display:"inline-block"}} onClick={()=>setModal("auth")}>SIGN IN</button>
            </div>
          ):(
            <div className="vgrid">
              {PAST.map((v,i)=>(
                <div key={i} className={"vt "+v.g}>
                  <span className={"vb "+v.p}>{v.p==="tk"?"♪":"▶"}</span>
                  <div className="vo"><div className="vttl">{v.title}</div><div className="vvws">👁 {v.views}</div></div>
                </div>
              ))}
            </div>
          )}
        </div>
      )}

      <nav className="bnav">
        {[{id:"create",icon:"✨",label:"Create"},{id:"trending",icon:"🔥",label:"Trending"},{id:"videos",icon:"🎬",label:"Videos"}].map(t=>(
          <button key={t.id} className={"btab"+(tab===t.id?" on":"")} onClick={()=>setTab(t.id)}>
            <span className="btab-icon">{t.icon}</span>
            <span className="btab-lbl">{t.label}</span>
            <span className="btab-dot"/>
          </button>
        ))}
      </nav>

      {modal==="pro"&&(
        <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
          <div className="modal">
            <div className="mhandle"/>
            <div className="mtitle">GO PRO ⚡</div>
            <div className="msub">Remove watermarks, unlimited videos, direct posting.</div>
            <ul className="perks">
              {["No watermark on exports","Unlimited daily videos","TikTok & YouTube direct posting","Premium styles","Priority AI generation"].map(p=><li key={p}>{p}</li>)}
            </ul>
            <div className="pcards">
              <div className="pcard pop"><div className="pbadge2">BEST VALUE</div>
                <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                  <div><div className="pname">Pro Annual</div><div className="pperks">Save 50%</div></div>
                  <div><div className="pprice">$4.99<small>/mo</small></div><div style={{fontSize:10,color:"var(--mut)",fontFamily:"Space Mono"}}>billed yearly</div></div>
                </div>
              </div>
              <div className="pcard">
                <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                  <div><div className="pname">Pro Monthly</div><div className="pperks">Cancel anytime</div></div>
                  <div className="pprice">$9.99<small>/mo</small></div>
                </div>
              </div>
            </div>
            <button className="mcta" onClick={()=>{if(!user){setModal("auth");return;}setUser(u=>({...u,pro:true}));setModal(null);showToast("Pro unlocked!");}}>START 3-DAY FREE TRIAL</button>
            <button className="dismiss" onClick={()=>setModal(null)}>Maybe later</button>
          </div>
        </div>
      )}

      {modal==="auth"&&(
        <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
          <div className="modal">
            <div className="mhandle"/>
            <div className="mtitle">{authMode==="login"?"WELCOME BACK":"JOIN VIRALCUT"}</div>
            <div className="msub">Sign in to save videos and unlock Pro.</div>
            <button className="abtn google" onClick={()=>loginWith("Alex Rivera","alex@gmail.com")}>
              <div className="ai" style={{background:"#fff"}}><GSvg/></div>Continue with Google
            </button>
            <button className="abtn tktk" onClick={()=>loginWith("Creator","creator@tiktok.com")}>
              <div className="ai" style={{background:"rgba(0,242,234,.15)",color:"var(--tk)",fontWeight:900}}>♪</div>Continue with TikTok
            </button>
            <div className="dvdr">or email</div>
            <input className="ef" type="email" placeholder="Email address"/>
            <input className="ef" type="password" placeholder="Password"/>
            <button className="acta" onClick={()=>loginWith("Creator","creator@email.com")}>{authMode==="login"?"SIGN IN":"CREATE ACCOUNT"}</button>
            <div className="aswitch" onClick={()=>setAuth(m=>m==="login"?"signup":"login")}>
              {authMode==="login"?"No account? ":"Have one? "}<span>{authMode==="login"?"Sign up free":"Sign in"}</span>
            </div>
          </div>
        </div>
      )}

      {modal==="quickprofile"&&user&&(
        <div className="ovl" onClick={e=>{if(e.target===e.currentTarget)setModal(null);}}>
          <div className="modal">
            <div className="mhandle"/>
            <div style={{textAlign:"center",marginBottom:24,paddingBottom:20,borderBottom:"1px solid var(--bdr)"}}>
              <div style={{width:64,height:64,borderRadius:"50%",background:"linear-gradient(135deg,#FF2D55,#FF6B00)",display:"flex",alignItems:"center",justifyContent:"center",fontSize:28,margin:"0 auto 12px",border:"3px solid var(--red)"}}>
                {user.avatar}
              </div>
              <div style={{fontFamily:"'Bebas Neue',sans-serif",fontSize:22,letterSpacing:1}}>{user.name.toUpperCase()}</div>
              <div style={{fontSize:12,color:"var(--mut)",fontFamily:"Space Mono,monospace"}}>{user.email}</div>
              <div style={{marginTop:8}}>
                <span style={{fontFamily:"Space Mono,monospace",fontSize:10,padding:"4px 12px",borderRadius:20,background:user.pro?"linear-gradient(135deg,#FF2D55,#FF6B00)":"var(--s2)",border:user.pro?"none":"1px solid var(--bdr)",color:user.pro?"#fff":"var(--mut)"}}>
                  {user.pro?"⚡ PRO":"FREE PLAN"}
                </span>
              </div>
            </div>
            {!user.pro&&<button className="mcta" onClick={()=>setModal("pro")}>⚡ UPGRADE TO PRO</button>}
            <button className="dismiss" onClick={()=>{setUser(null);setModal(null);showToast("Signed out");}}>Sign Out</button>
            <button className="dismiss" onClick={()=>setModal(null)}>Close</button>
          </div>
        </div>
      )}

      {toast&&<div className="toast">{toast}</div>}
    </div>
    </>
  );
}
