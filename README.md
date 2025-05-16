<!DOCTYPE html>
<html lang="fr"><head>
    <script type="module">
import { createHotContext } from "/@vite/client";
const hot = createHotContext("/__dummy__runtime-error-plugin");

function sendError(error) {
  if (!(error instanceof Error)) {
    error = new Error("(unknown runtime error)");
  }
  const serialized = {
    message: error.message,
    stack: error.stack,
  };
  hot.send("runtime-error-plugin:error", serialized);
}

window.addEventListener("error", (evt) => {
  sendError(evt.error);
});

window.addEventListener("unhandledrejection", (evt) => {
  sendError(evt.reason);
});
</script>

    <script type="module">
import RefreshRuntime from "/@react-refresh"
RefreshRuntime.injectIntoGlobalHook(window)
window.$RefreshReg$ = () => {}
window.$RefreshSig$ = () => (type) => type
window.__vite_plugin_react_preamble_installed__ = true
</script>

    <script type="module" src="/@vite/client"></script>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Premium Crèche</title>

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
      tailwind.config = {
        theme: {
          extend: {
            colors: {
              'creche-blue': '#5DADEC', /* Bleu plus vif et chaleureux */
              'creche-yellow': '#FFDB58', /* Jaune moutarde plus chaud */
              'creche-green': '#A3E4A8', /* Vert plus frais et vif */
              'creche-cream': '#FFF6E9', /* Crème plus chaud, presque pêche */
              'creche-gray': '#6D6875', /* Gris plus chaud avec nuance violette */
              'creche-orange': '#FF8C61', /* Orange corail plus chaleureux */
              'creche-peach': '#FFB385', /* Pêche pour une ambiance douce */
              'creche-lavender': '#D8B4E2', /* Lavande pour une touche douce */
            },
            fontFamily: {
              'quicksand': ['Quicksand', 'sans-serif'],
              'poppins': ['Poppins', 'sans-serif'],
              'inter': ['Inter', 'sans-serif'],
            },
          }
        }
      }
    </script>

    <!-- Google Fonts : Quicksand, Poppins, Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&amp;family=Poppins:wght@400;500;600;700&amp;family=Inter:wght@400;500;600;700&amp;display=swap" rel="stylesheet">
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
    
    <!-- Leaflet pour la carte -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css">
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <!-- CSS PERSONNALISÉ -->
    <style>
      html {
        scroll-behavior: smooth;
        scroll-padding-top: 5rem;
      }
      
      /* SECTION: FAQ - Animation accordéon */
      .faq-question svg {
        transition: transform 0.3s ease;
      }
      
      .faq-question.active svg {
        transform: rotate(180deg);
      }

      body {
        font-family: 'Quicksand', sans-serif;
        background-color: #FFF6EA; /* Fond crème plus chaud */
        color: #6D6875; /* Gris plus chaud avec nuance violette */
        overflow-x: hidden; /* Pour éviter les débordements avec les illustrations */
        position: relative;
      }
      
      /* Éléments décoratifs - feuilles et formes abstraites */
      body::before,
      body::after {
        content: '';
        position: fixed;
        width: 300px;
        height: 300px;
        background-size: contain;
        background-repeat: no-repeat;
        z-index: -1;
        opacity: 0.6;
      }
      
      /* Feuillage décoratif en haut à gauche - vert plus vif */
      body::before {
        top: 50px;
        left: -80px;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300' viewBox='0 0 300 300' fill='none'%3E%3Cpath d='M150 50C180 80 200 120 200 160C200 220 150 250 100 230C50 210 30 160 50 120C70 80 120 60 150 50Z' fill='%23A3E4A8'/%3E%3Cpath d='M120 100C140 110 150 130 150 150C150 180 120 200 90 190C60 180 40 150 60 130C80 110 100 90 120 100Z' fill='%23B5F0BA'/%3E%3C/svg%3E");
        transform: rotate(15deg);
      }
      
      /* Nuage décoratif en bas à droite - couleurs plus chaudes */
      body::after {
        bottom: 50px;
        right: -80px;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='200' viewBox='0 0 400 200' fill='none'%3E%3Cpath d='M350 100C350 127.614 322.614 150 290 150C257.386 150 230 127.614 230 100C230 72.3858 257.386 50 290 50C322.614 50 350 72.3858 350 100Z' fill='%23FFDB58'/%3E%3Cpath d='M300 80C300 107.614 272.614 130 240 130C207.386 130 180 107.614 180 80C180 52.3858 207.386 30 240 30C272.614 30 300 52.3858 300 80Z' fill='%23FFE896'/%3E%3C/svg%3E");
        transform: rotate(-5deg) scale(1.2);
        width: 400px;
        height: 200px;
      }
      
      /* Style global pour créer une sensation de continuité */
      section {
        position: relative;
        overflow: visible;
        transition: all 0.5s ease;
        border: none;
        margin: 0;
        padding-top: 8rem;
        padding-bottom: 8rem;
      }
      
      /* Suppression des connecteurs entre sections comme demandé */
      section::before, section::after {
        display: none;
      }

      .fade-in {
        opacity: 0;
        transform: translateY(20px);
        transition: opacity 0.6s ease-out, transform 0.6s ease-out;
      }

      .fade-in.appear {
        opacity: 1;
        transform: translateY(0);
      }

      /* CSS POUR .card-group (section CRÈCHES) */
      .card-group .card {
        transition: all 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        flex: 1 1 0;
        min-width: 0;
        flex-basis: 0;
        height: 350px;
      }
      
      @media (max-width: 768px) {
        .card-group .card {
          height: 100px;
          margin-bottom: 10px;
        }
      }
      
      .card-group:hover .card {
        flex: 0.7;
      }
      
      .card-group:hover .card:hover {
        flex: 3.5 !important;
        z-index: 10;
        box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
      }

      /* Correction scroll fiche zoomée */
      body.overflow-hidden {
        overflow: hidden;
      }

      body.overflow-hidden #fiche-zoom {
        overflow-y: auto;
        -webkit-overflow-scrolling: touch;
      }
      
      /* Variables CSS pour le carrousel */
      :root {
        --slide-interval: 10s;
        --slide-duration: 0.8s;
        --carousel-height: 100%;
        --carousel-width: 100%;
        --carousel-padding: 28px;
        --carousel-margin: 32px;
        --carousel-bg: rgba(255, 140, 97, 0.15); /* Orange corail plus chaleureux */
        --carousel-border: #FF8C61; /* Orange corail plus chaleureux */
        --carousel-title-bg: #FF8C61; /* Orange corail plus chaleureux */
        --carousel-title-color: #FFF6E9; /* Crème plus chaud */
        --carousel-item-color: #6D6875; /* Gris plus chaud avec nuance violette */
        --carousel-check-color: #FF8C61; /* Orange corail plus chaleureux */
        --transition-easing: cubic-bezier(0.25, 0.46, 0.45, 0.94);
        --min-carousel-height: 400px;
      }
      
      /* Styles pour masquer la barre de défilement tout en permettant le défilement */
      #scroll-zone::-webkit-scrollbar {
        display: none;
      }
      #scroll-zone {
        -ms-overflow-style: none;  /* IE and Edge */
        scrollbar-width: none;  /* Firefox */
      }
      
      /* Styles pour le carrousel "Pourquoi réserver ?" */
      .why-reserve {
        border-radius: 8px;
        border: 1px solid var(--carousel-border);
        overflow: hidden;
        position: relative;
        box-shadow: 0 6px 12px -2px rgba(0, 0, 0, 0.15), 0 3px 7px -3px rgba(0, 0, 0, 0.1);
        background-color: var(--carousel-bg);
        padding-bottom: var(--carousel-margin);
        margin-bottom: 1.5rem;
      }
      
      .why-reserve-title {
        background-color: var(--carousel-title-bg);
        color: var(--carousel-title-color);
        padding: 0.75rem;
        text-align: center;
        font-weight: 600;
        z-index: 10;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        margin-bottom: var(--carousel-padding);
        font-family: 'Inter', sans-serif;
        text-transform: uppercase;
        letter-spacing: 0.5px;
      }
      
      .carousel {
        position: relative;
        overflow: hidden;
        height: var(--carousel-height);
        min-height: var(--min-carousel-height);
        width: var(--carousel-width);
        margin: 0 auto;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 6px;
      }
      
      .carousel-wrapper {
        position: relative;
        overflow: hidden;
        height: 100%;
        width: 100%;
        border-radius: 4px;
      }
      
      .carousel-container {
        display: flex;
        position: relative;
        height: 100%;
        width: 100%;
        transition: transform var(--slide-duration) var(--transition-easing);
        will-change: transform;
      }
      
      .carousel-item {
        flex: 0 0 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        height: 100%;
        font-weight: 600;
        padding: var(--carousel-padding);
        color: var(--carousel-item-color);
        text-align: left;
        font-family: 'Inter', sans-serif;
        font-size: 1.5rem;
        line-height: 1.6;
        letter-spacing: 0.3px;
        width: 85%;
        margin: 0 auto;
        position: relative;
        word-wrap: break-word;
        -webkit-hyphens: auto;
                hyphens: auto;
        box-sizing: border-box;
      }
      
      .carousel-item:before {
        content: "✓";
        display: inline-block;
        flex-shrink: 0;
        margin-right: 1rem;
        color: var(--carousel-check-color);
        font-weight: bold;
        font-size: 1.6rem;
      }
      
      /* Contrôles */
      .carousel-controls {
        position: absolute;
        bottom: 1rem;
        left: 0;
        right: 0;
        display: flex;
        justify-content: center;
        gap: 0.5rem;
        z-index: 15;
      }
      
      .carousel-dot {
        width: 0.4rem;
        height: 0.4rem;
        border-radius: 50%;
        background-color: rgba(234, 179, 8, 0.2);
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
      }
      
      .carousel-dot.active {
        background-color: var(--carousel-check-color);
        transform: scale(1.3);
      }
      
      .carousel-dot:hover {
        background-color: rgba(234, 179, 8, 0.5);
        transform: scale(1.2);
      }
      
      /* Navigation buttons */
      .carousel-nav {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        background-color: rgba(255, 255, 255, 0.6);
        border: none;
        border-radius: 50%;
        width: 2.5rem;
        height: 2.5rem;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        font-weight: bold;
        font-size: 1.5rem;
        opacity: 0;
        transition: opacity 0.3s ease;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        z-index: 30;
      }
      
      .carousel-wrapper:hover .carousel-nav {
        opacity: 0.8;
      }
      
      .carousel-nav:hover {
        opacity: 1;
        background-color: rgba(255, 255, 255, 0.9);
        transform: translateY(-50%) scale(1.15);
      }
      
      .carousel-prev {
        left: 0.5rem;
      }
      
      .carousel-next {
        right: 0.5rem;
      }
      
      /* Responsive */
      @media (max-width: 768px) {
        :root {
          --carousel-height: 200px;
          --carousel-width: 100%;
          --carousel-padding: 16px;
          --carousel-margin: 16px;
        }
        
        .carousel-item {
          font-size: 0.95rem;
          padding: 12px 16px;
          line-height: 1.4;
        }
        
        .carousel-wrapper:hover .carousel-nav {
          opacity: 0.7;
        }
        
        .carousel-nav {
          width: 1.75rem;
          height: 1.75rem;
          font-size: 1rem;
        }
        
        .carousel-item:before {
          font-size: 1.1rem;
          margin-right: 0.5rem;
        }
        
        .carousel-controls {
          bottom: 0.5rem;
        }
        
        .carousel-dot {
          width: 0.35rem;
          height: 0.35rem;
        }
      }
      
      /* Pour les très petits écrans */
      @media (max-width: 480px) {
        :root {
          --carousel-height: 180px;
        }
        
        .carousel-item {
          font-size: 0.9rem;
          padding: 10px 12px;
        }
        
        .carousel-nav {
          width: 1.5rem;
          height: 1.5rem;
          font-size: 0.9rem;
        }
        
        .carousel-prev {
          left: 0.25rem;
        }
        
        .carousel-next {
          right: 0.25rem;
        }
      }
      
      @media (min-width: 1200px) {
        :root {
          --carousel-width: 95%;
        }
        
        .carousel {
          max-width: 100%;
        }
        
        .carousel-item {
          font-size: 1.75rem;
          letter-spacing: 0.3px;
          line-height: 1.6;
        }
      }
    </style>
    
    <!-- Open Graph tags -->
    <meta property="og:title" content="Premium Crèche - Trouvez la crèche parfaite pour votre enfant">
    <meta property="og:description" content="Découvrez notre sélection des meilleures crèches en France pour le bien-être et l'épanouissement de votre enfant.">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://premium-creche.fr">
    <script type="module">"use strict";(()=>{var P="0.1.2";var T={HIGHLIGHT_COLOR:"#0079F2",HIGHLIGHT_BG:"#0079F210",ALLOWED_DOMAIN:".replit.dev"},I={highlighter:{position:"absolute",zIndex:Number.MAX_SAFE_INTEGER-3,boxSizing:"border-box",pointerEvents:"none",border:`2px solid ${T.HIGHLIGHT_COLOR}`,borderRadius:"4px",background:T.HIGHLIGHT_BG,transition:"opacity 0.2s",willChange:"opacity",opacity:"0"},label:{position:"absolute",backgroundColor:T.HIGHLIGHT_COLOR,color:"#FFFFFF",padding:"2px 6px",borderRadius:"4px",fontSize:"12px",fontFamily:"monospace",transform:"translateY(-100%)",marginTop:"-4px",zIndex:Number.MAX_SAFE_INTEGER-2,pointerEvents:"none",opacity:"0"}};function xe(e,t){return e[13]=1,e[14]=t>>8,e[15]=t&255,e[16]=t>>8,e[17]=t&255,e}var re=112,oe=72,ie=89,se=115,W;function Ie(){let e=new Int32Array(256);for(let t=0;t<256;t++){let n=t;for(let r=0;r<8;r++)n=n&1?3988292384^n>>>1:n>>>1;e[t]=n}return e}function De(e){let t=-1;W||(W=Ie());for(let n=0;n<e.length;n++)t=W[(t^e[n])&255]^t>>>8;return t^-1}function He(e){let t=e.length-1;for(let n=t;n>=4;n--)if(e[n-4]===9&&e[n-3]===re&&e[n-2]===oe&&e[n-1]===ie&&e[n]===se)return n-3;return 0}function Re(e,t,n=!1){let r=new Uint8Array(13);t*=39.3701,r[0]=re,r[1]=oe,r[2]=ie,r[3]=se,r[4]=t>>>24,r[5]=t>>>16,r[6]=t>>>8,r[7]=t&255,r[8]=r[4],r[9]=r[5],r[10]=r[6],r[11]=r[7],r[12]=1;let s=De(r),i=new Uint8Array(4);if(i[0]=s>>>24,i[1]=s>>>16,i[2]=s>>>8,i[3]=s&255,n){let a=He(e);return e.set(r,a),e.set(i,a+13),e}else{let a=new Uint8Array(4);a[0]=0,a[1]=0,a[2]=0,a[3]=9;let o=new Uint8Array(54);return o.set(e,0),o.set(a,33),o.set(r,37),o.set(i,50),o}}var ae="[modern-screenshot]",A=typeof window<"u",_e=A&&"Worker"in window,Me=A&&"atob"in window,jt=A&&"btoa"in window,j=A?window.navigator?.userAgent:"",le=j.includes("Chrome"),O=j.includes("AppleWebKit")&&!le,z=j.includes("Firefox"),Fe=e=>e&&"__CONTEXT__"in e,Pe=e=>e.constructor.name==="CSSFontFaceRule",Oe=e=>e.constructor.name==="CSSImportRule",v=e=>e.nodeType===1,_=e=>typeof e.className=="object",ce=e=>e.tagName==="image",ke=e=>e.tagName==="use",D=e=>v(e)&&typeof e.style<"u"&&!_(e),Be=e=>e.nodeType===8,Ue=e=>e.nodeType===3,x=e=>e.tagName==="IMG",k=e=>e.tagName==="VIDEO",$e=e=>e.tagName==="CANVAS",We=e=>e.tagName==="TEXTAREA",Ge=e=>e.tagName==="INPUT",je=e=>e.tagName==="STYLE",ze=e=>e.tagName==="SCRIPT",Ve=e=>e.tagName==="SELECT",qe=e=>e.tagName==="SLOT",Xe=e=>e.tagName==="IFRAME",Ye=(...e)=>console.warn(ae,...e);function Je(e){let t=e?.createElement?.("canvas");return t&&(t.height=t.width=1),!!t&&"toDataURL"in t&&!!t.toDataURL("image/webp").includes("image/webp")}var G=e=>e.startsWith("data:");function ue(e,t){if(e.match(/^[a-z]+:\/\//i))return e;if(A&&e.match(/^\/\//))return window.location.protocol+e;if(e.match(/^[a-z]+:/i)||!A)return e;let n=B().implementation.createHTMLDocument(),r=n.createElement("base"),s=n.createElement("a");return n.head.appendChild(r),n.body.appendChild(s),t&&(r.href=t),s.href=e,s.href}function B(e){return(e&&v(e)?e?.ownerDocument:e)??window.document}var U="http://www.w3.org/2000/svg";function Ke(e,t,n){let r=B(n).createElementNS(U,"svg");return r.setAttributeNS(null,"width",e.toString()),r.setAttributeNS(null,"height",t.toString()),r.setAttributeNS(null,"viewBox",`0 0 ${e} ${t}`),r}function Qe(e,t){let n=new XMLSerializer().serializeToString(e);return t&&(n=n.replace(/[\u0000-\u0008\v\f\u000E-\u001F\uD800-\uDFFF\uFFFE\uFFFF]/gu,"")),`data:image/svg+xml;charset=utf-8,${encodeURIComponent(n)}`}async function Ze(e,t="image/png",n=1){try{return await new Promise((r,s)=>{e.toBlob(i=>{i?r(i):s(new Error("Blob is null"))},t,n)})}catch(r){if(Me)return et(e.toDataURL(t,n));throw r}}function et(e){let[t,n]=e.split(","),r=t.match(/data:(.+);/)?.[1]??void 0,s=window.atob(n),i=s.length,a=new Uint8Array(i);for(let o=0;o<i;o+=1)a[o]=s.charCodeAt(o);return new Blob([a],{type:r})}function de(e,t){return new Promise((n,r)=>{let s=new FileReader;s.onload=()=>n(s.result),s.onerror=()=>r(s.error),s.onabort=()=>r(new Error(`Failed read blob to ${t}`)),t==="dataUrl"?s.readAsDataURL(e):t==="arrayBuffer"&&s.readAsArrayBuffer(e)})}var tt=e=>de(e,"dataUrl"),nt=e=>de(e,"arrayBuffer");function N(e,t){let n=B(t).createElement("img");return n.decoding="sync",n.loading="eager",n.src=e,n}function H(e,t){return new Promise(n=>{let{timeout:r,ownerDocument:s,onError:i,onWarn:a}=t??{},o=typeof e=="string"?N(e,B(s)):e,c=null,d=null;function l(){n(o),c&&clearTimeout(c),d?.()}if(r&&(c=setTimeout(l,r)),k(o)){let u=o.currentSrc||o.src;if(!u)return o.poster?H(o.poster,t).then(n):l();if(o.readyState>=2)return l();let h=l,f=g=>{a?.("Failed video load",u,g),i?.(g),l()};d=()=>{o.removeEventListener("loadeddata",h),o.removeEventListener("error",f)},o.addEventListener("loadeddata",h,{once:!0}),o.addEventListener("error",f,{once:!0})}else{let u=ce(o)?o.href.baseVal:o.currentSrc||o.src;if(!u)return l();let h=async()=>{if(x(o)&&"decode"in o)try{await o.decode()}catch(g){a?.("Failed to decode image, trying to render anyway",o.dataset.originalSrc||u,g)}l()},f=g=>{a?.("Failed image load",o.dataset.originalSrc||u,g),l()};if(x(o)&&o.complete)return h();d=()=>{o.removeEventListener("load",h),o.removeEventListener("error",f)},o.addEventListener("load",h,{once:!0}),o.addEventListener("error",f,{once:!0})}})}async function rt(e,t){D(e)&&(x(e)||k(e)?await H(e,t):await Promise.all(["img","video"].flatMap(n=>Array.from(e.querySelectorAll(n)).map(r=>H(r,t)))))}var he=function(){let t=0,n=()=>`0000${(Math.random()*36**4<<0).toString(36)}`.slice(-4);return()=>(t+=1,`u${n()}${t}`)}();function ge(e){return e?.split(",").map(t=>t.trim().replace(/"|'/g,"").toLowerCase()).filter(Boolean)}var K=0;function ot(e){let t=`${ae}[#${K}]`;return K++,{time:n=>e&&console.time(`${t} ${n}`),timeEnd:n=>e&&console.timeEnd(`${t} ${n}`),warn:(...n)=>e&&Ye(...n)}}function it(e){return{cache:e?"no-cache":"force-cache"}}async function V(e,t){return Fe(e)?e:st(e,{...t,autoDestruct:!0})}async function st(e,t){let{scale:n=1,workerUrl:r,workerNumber:s=1}=t||{},i=!!t?.debug,a=t?.features??!0,o=e.ownerDocument??(A?window.document:void 0),c=e.ownerDocument?.defaultView??(A?window:void 0),d=new Map,l={width:0,height:0,quality:1,type:"image/png",scale:n,backgroundColor:null,style:null,filter:null,maximumCanvasSize:0,timeout:3e4,progress:null,debug:i,fetch:{requestInit:it(t?.fetch?.bypassingCache),placeholderImage:"data:image/png;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7",bypassingCache:!1,...t?.fetch},fetchFn:null,font:{},drawImageInterval:100,workerUrl:null,workerNumber:s,onCloneNode:null,onEmbedNode:null,onCreateForeignObjectSvg:null,includeStyleProperties:null,autoDestruct:!1,...t,__CONTEXT__:!0,log:ot(i),node:e,ownerDocument:o,ownerWindow:c,dpi:n===1?null:96*n,svgStyleElement:fe(o),svgDefsElement:o?.createElementNS(U,"defs"),svgStyles:new Map,defaultComputedStyles:new Map,workers:[...Array.from({length:_e&&r&&s?s:0})].map(()=>{try{let f=new Worker(r);return f.onmessage=async g=>{let{url:m,result:p}=g.data;p?d.get(m)?.resolve?.(p):d.get(m)?.reject?.(new Error(`Error receiving message from worker: ${m}`))},f.onmessageerror=g=>{let{url:m}=g.data;d.get(m)?.reject?.(new Error(`Error receiving message from worker: ${m}`))},f}catch(f){return l.log.warn("Failed to new Worker",f),null}}).filter(Boolean),fontFamilies:new Map,fontCssTexts:new Map,acceptOfImage:`${[Je(o)&&"image/webp","image/svg+xml","image/*","*/*"].filter(Boolean).join(",")};q=0.8`,requests:d,drawImageCount:0,tasks:[],features:a,isEnable:f=>f==="restoreScrollPosition"?typeof a=="boolean"?!1:a[f]??!1:typeof a=="boolean"?a:a[f]??!0};l.log.time("wait until load"),await rt(e,{timeout:l.timeout,onWarn:l.log.warn}),l.log.timeEnd("wait until load");let{width:u,height:h}=at(e,l);return l.width=u,l.height=h,l}function fe(e){if(!e)return;let t=e.createElement("style"),n=t.ownerDocument.createTextNode(`
.______background-clip--text {
  background-clip: text;
  -webkit-background-clip: text;
}
`);return t.appendChild(n),t}function at(e,t){let{width:n,height:r}=t;if(v(e)&&(!n||!r)){let s=e.getBoundingClientRect();n=n||s.width||Number(e.getAttribute("width"))||0,r=r||s.height||Number(e.getAttribute("height"))||0}return{width:n,height:r}}async function lt(e,t){let{log:n,timeout:r,drawImageCount:s,drawImageInterval:i}=t;n.time("image to canvas");let a=await H(e,{timeout:r,onWarn:t.log.warn}),{canvas:o,context2d:c}=ct(e.ownerDocument,t),d=()=>{try{c?.drawImage(a,0,0,o.width,o.height)}catch(l){t.log.warn("Failed to drawImage",l)}};if(d(),t.isEnable("fixSvgXmlDecode"))for(let l=0;l<s;l++)await new Promise(u=>{setTimeout(()=>{d(),u()},l+i)});return t.drawImageCount=0,n.timeEnd("image to canvas"),o}function ct(e,t){let{width:n,height:r,scale:s,backgroundColor:i,maximumCanvasSize:a}=t,o=e.createElement("canvas");o.width=Math.floor(n*s),o.height=Math.floor(r*s),o.style.width=`${n}px`,o.style.height=`${r}px`,a&&(o.width>a||o.height>a)&&(o.width>a&&o.height>a?o.width>o.height?(o.height*=a/o.width,o.width=a):(o.width*=a/o.height,o.height=a):o.width>a?(o.height*=a/o.width,o.width=a):(o.width*=a/o.height,o.height=a));let c=o.getContext("2d");return c&&i&&(c.fillStyle=i,c.fillRect(0,0,o.width,o.height)),{canvas:o,context2d:c}}function me(e,t){if(e.ownerDocument)try{let i=e.toDataURL();if(i!=="data:,")return N(i,e.ownerDocument)}catch(i){t.log.warn("Failed to clone canvas",i)}let n=e.cloneNode(!1),r=e.getContext("2d"),s=n.getContext("2d");try{return r&&s&&s.putImageData(r.getImageData(0,0,e.width,e.height),0,0),n}catch(i){t.log.warn("Failed to clone canvas",i)}return n}function ut(e,t){try{if(e?.contentDocument?.body)return q(e.contentDocument.body,t)}catch(n){t.log.warn("Failed to clone iframe",n)}return e.cloneNode(!1)}function dt(e){let t=e.cloneNode(!1);return e.currentSrc&&e.currentSrc!==e.src&&(t.src=e.currentSrc,t.srcset=""),t.loading==="lazy"&&(t.loading="eager"),t}async function ht(e,t){if(e.ownerDocument&&!e.currentSrc&&e.poster)return N(e.poster,e.ownerDocument);let n=e.cloneNode(!1);n.crossOrigin="anonymous",e.currentSrc&&e.currentSrc!==e.src&&(n.src=e.currentSrc);let r=n.ownerDocument;if(r){let s=!0;if(await H(n,{onError:()=>s=!1,onWarn:t.log.warn}),!s)return e.poster?N(e.poster,e.ownerDocument):n;n.currentTime=e.currentTime,await new Promise(a=>{n.addEventListener("seeked",a,{once:!0})});let i=r.createElement("canvas");i.width=e.offsetWidth,i.height=e.offsetHeight;try{let a=i.getContext("2d");a&&a.drawImage(n,0,0,i.width,i.height)}catch(a){return t.log.warn("Failed to clone video",a),e.poster?N(e.poster,e.ownerDocument):n}return me(i,t)}return n}function gt(e,t){return $e(e)?me(e,t):Xe(e)?ut(e,t):x(e)?dt(e):k(e)?ht(e,t):e.cloneNode(!1)}function ft(e){let t=e.sandbox;if(!t){let{ownerDocument:n}=e;try{n&&(t=n.createElement("iframe"),t.id=`__SANDBOX__-${he()}`,t.width="0",t.height="0",t.style.visibility="hidden",t.style.position="fixed",n.body.appendChild(t),t.contentWindow?.document.write('<!DOCTYPE html><meta charset="UTF-8"><title></title><body>'),e.sandbox=t)}catch(r){e.log.warn("Failed to getSandBox",r)}}return t}var mt=["width","height","-webkit-text-fill-color"],pt=["stroke","fill"];function pe(e,t,n){let{defaultComputedStyles:r}=n,s=e.nodeName.toLowerCase(),i=_(e)&&s!=="svg",a=i?pt.map(m=>[m,e.getAttribute(m)]).filter(([,m])=>m!==null):[],o=[i&&"svg",s,a.map((m,p)=>`${m}=${p}`).join(","),t].filter(Boolean).join(":");if(r.has(o))return r.get(o);let d=ft(n)?.contentWindow;if(!d)return new Map;let l=d?.document,u,h;i?(u=l.createElementNS(U,"svg"),h=u.ownerDocument.createElementNS(u.namespaceURI,s),a.forEach(([m,p])=>{h.setAttributeNS(null,m,p)}),u.appendChild(h)):u=h=l.createElement(s),h.textContent=" ",l.body.appendChild(u);let f=d.getComputedStyle(h,t),g=new Map;for(let m=f.length,p=0;p<m;p++){let w=f.item(p);mt.includes(w)||g.set(w,f.getPropertyValue(w))}return l.body.removeChild(u),r.set(o,g),g}function we(e,t,n){let r=new Map,s=[],i=new Map;if(n)for(let o of n)a(o);else for(let o=e.length,c=0;c<o;c++){let d=e.item(c);a(d)}for(let o=s.length,c=0;c<o;c++)i.get(s[c])?.forEach((d,l)=>r.set(l,d));function a(o){let c=e.getPropertyValue(o),d=e.getPropertyPriority(o),l=o.lastIndexOf("-"),u=l>-1?o.substring(0,l):void 0;if(u){let h=i.get(u);h||(h=new Map,i.set(u,h)),h.set(o,[c,d])}t.get(o)===c&&!d||(u?s.push(u):r.set(o,[c,d]))}return r}function wt(e,t,n,r){let{ownerWindow:s,includeStyleProperties:i,currentParentNodeStyle:a}=r,o=t.style,c=s.getComputedStyle(e),d=pe(e,null,r);a?.forEach((u,h)=>{d.delete(h)});let l=we(c,d,i);l.delete("transition-property"),l.delete("all"),l.delete("d"),l.delete("content"),n&&(l.delete("margin-top"),l.delete("margin-right"),l.delete("margin-bottom"),l.delete("margin-left"),l.delete("margin-block-start"),l.delete("margin-block-end"),l.delete("margin-inline-start"),l.delete("margin-inline-end"),l.set("box-sizing",["border-box",""])),l.get("background-clip")?.[0]==="text"&&t.classList.add("______background-clip--text"),le&&(l.has("font-kerning")||l.set("font-kerning",["normal",""]),(l.get("overflow-x")?.[0]==="hidden"||l.get("overflow-y")?.[0]==="hidden")&&l.get("text-overflow")?.[0]==="ellipsis"&&e.scrollWidth===e.clientWidth&&l.set("text-overflow",["clip",""]));for(let u=o.length,h=0;h<u;h++)o.removeProperty(o.item(h));return l.forEach(([u,h],f)=>{o.setProperty(f,u,h)}),l}function Et(e,t){(We(e)||Ge(e)||Ve(e))&&t.setAttribute("value",e.value)}var bt=[":before",":after"],yt=[":-webkit-scrollbar",":-webkit-scrollbar-button",":-webkit-scrollbar-thumb",":-webkit-scrollbar-track",":-webkit-scrollbar-track-piece",":-webkit-scrollbar-corner",":-webkit-resizer"];function vt(e,t,n,r,s){let{ownerWindow:i,svgStyleElement:a,svgStyles:o,currentNodeStyle:c}=r;if(!a||!i)return;function d(l){let u=i.getComputedStyle(e,l),h=u.getPropertyValue("content");if(!h||h==="none")return;s?.(h),h=h.replace(/(')|(")|(counter\(.+\))/g,"");let f=[he()],g=pe(e,l,r);c?.forEach((E,y)=>{g.delete(y)});let m=we(u,g,r.includeStyleProperties);m.delete("content"),m.delete("-webkit-locale"),m.get("background-clip")?.[0]==="text"&&t.classList.add("______background-clip--text");let p=[`content: '${h}';`];if(m.forEach((E,y,C)=>{p.push(`${C}: ${E}${y?" !important":""};`)}),p.length===1)return;try{t.className=[t.className,...f].join(" ")}catch(E){r.log.warn("Failed to copyPseudoClass",E);return}let w=p.join(`
  `),b=o.get(w);b||(b=[],o.set(w,b)),b.push(`.${f[0]}:${l}`)}bt.forEach(d),n&&yt.forEach(d)}var Q=new Set(["symbol"]);async function Z(e,t,n,r,s){if(v(n)&&(je(n)||ze(n))||r.filter&&!r.filter(n))return;Q.has(t.nodeName)||Q.has(n.nodeName)?r.currentParentNodeStyle=void 0:r.currentParentNodeStyle=r.currentNodeStyle;let i=await q(n,r,!1,s);r.isEnable("restoreScrollPosition")&&St(e,i),t.appendChild(i)}async function ee(e,t,n,r){let s=(v(e)?e.shadowRoot?.firstChild:void 0)??e.firstChild;for(let i=s;i;i=i.nextSibling)if(!Be(i))if(v(i)&&qe(i)&&typeof i.assignedNodes=="function"){let a=i.assignedNodes();for(let o=0;o<a.length;o++)await Z(e,t,a[o],n,r)}else await Z(e,t,i,n,r)}function St(e,t){if(!D(e)||!D(t))return;let{scrollTop:n,scrollLeft:r}=e;if(!n&&!r)return;let{transform:s}=t.style,i=new DOMMatrix(s),{a,b:o,c,d}=i;i.a=1,i.b=0,i.c=0,i.d=1,i.translateSelf(-r,-n),i.a=a,i.b=o,i.c=c,i.d=d,t.style.transform=i.toString()}function Ct(e,t){let{backgroundColor:n,width:r,height:s,style:i}=t,a=e.style;if(n&&a.setProperty("background-color",n,"important"),r&&a.setProperty("width",`${r}px`,"important"),s&&a.setProperty("height",`${s}px`,"important"),i)for(let o in i)a[o]=i[o]}var Tt=/^[\w-:]+$/;async function q(e,t,n=!1,r){let{ownerDocument:s,ownerWindow:i,fontFamilies:a}=t;if(s&&Ue(e))return r&&/\S/.test(e.data)&&r(e.data),s.createTextNode(e.data);if(s&&i&&v(e)&&(D(e)||_(e))){let c=await gt(e,t);if(t.isEnable("removeAbnormalAttributes")){let g=c.getAttributeNames();for(let m=g.length,p=0;p<m;p++){let w=g[p];Tt.test(w)||c.removeAttribute(w)}}let d=t.currentNodeStyle=wt(e,c,n,t);n&&Ct(c,t);let l=!1;if(t.isEnable("copyScrollbar")){let g=[d.get("overflow-x")?.[0],d.get("overflow-y")?.[0]];l=g.includes("scroll")||(g.includes("auto")||g.includes("overlay"))&&(e.scrollHeight>e.clientHeight||e.scrollWidth>e.clientWidth)}let u=d.get("text-transform")?.[0],h=ge(d.get("font-family")?.[0]),f=h?g=>{u==="uppercase"?g=g.toUpperCase():u==="lowercase"?g=g.toLowerCase():u==="capitalize"&&(g=g[0].toUpperCase()+g.substring(1)),h.forEach(m=>{let p=a.get(m);p||a.set(m,p=new Set),g.split("").forEach(w=>p.add(w))})}:void 0;return vt(e,c,l,t,f),Et(e,c),k(e)||await ee(e,c,t,f),c}let o=e.cloneNode(!1);return await ee(e,o,t),o}function At(e){if(e.ownerDocument=void 0,e.ownerWindow=void 0,e.svgStyleElement=void 0,e.svgDefsElement=void 0,e.svgStyles.clear(),e.defaultComputedStyles.clear(),e.sandbox){try{e.sandbox.remove()}catch(t){e.log.warn("Failed to destroyContext",t)}e.sandbox=void 0}e.workers=[],e.fontFamilies.clear(),e.fontCssTexts.clear(),e.requests.clear(),e.tasks=[]}function Lt(e){let{url:t,timeout:n,responseType:r,...s}=e,i=new AbortController,a=n?setTimeout(()=>i.abort(),n):void 0;return fetch(t,{signal:i.signal,...s}).then(o=>{if(!o.ok)throw new Error("Failed fetch, not 2xx response",{cause:o});switch(r){case"arrayBuffer":return o.arrayBuffer();case"dataUrl":return o.blob().then(tt);case"text":default:return o.text()}}).finally(()=>clearTimeout(a))}function R(e,t){let{url:n,requestType:r="text",responseType:s="text",imageDom:i}=t,a=n,{timeout:o,acceptOfImage:c,requests:d,fetchFn:l,fetch:{requestInit:u,bypassingCache:h,placeholderImage:f},font:g,workers:m,fontFamilies:p}=e;r==="image"&&(O||z)&&e.drawImageCount++;let w=d.get(n);if(!w){h&&h instanceof RegExp&&h.test(a)&&(a+=(/\?/.test(a)?"&":"?")+new Date().getTime());let b=r.startsWith("font")&&g&&g.minify,E=new Set;b&&r.split(";")[1].split(",").forEach(F=>{p.has(F)&&p.get(F).forEach(J=>E.add(J))});let y=b&&E.size,C={url:a,timeout:o,responseType:y?"arrayBuffer":s,headers:r==="image"?{accept:c}:void 0,...u};w={type:r,resolve:void 0,reject:void 0,response:null},w.response=(async()=>{if(l&&r==="image"){let S=await l(n);if(S)return S}return!O&&n.startsWith("http")&&m.length?new Promise((S,F)=>{m[d.size&m.length-1].postMessage({rawUrl:n,...C}),w.resolve=S,w.reject=F}):Lt(C)})().catch(S=>{if(d.delete(n),r==="image"&&f)return e.log.warn("Failed to fetch image base64, trying to use placeholder image",a),typeof f=="string"?f:f(i);throw S}),d.set(n,w)}return w.response}async function Ee(e,t,n,r){if(!be(e))return e;for(let[s,i]of Nt(e,t))try{let a=await R(n,{url:i,requestType:r?"image":"text",responseType:"dataUrl"});e=e.replace(xt(s),`$1${a}$3`)}catch(a){n.log.warn("Failed to fetch css data url",s,a)}return e}function be(e){return/url\((['"]?)([^'"]+?)\1\)/.test(e)}var ye=/url\((['"]?)([^'"]+?)\1\)/g;function Nt(e,t){let n=[];return e.replace(ye,(r,s,i)=>(n.push([i,ue(i,t)]),r)),n.filter(([r])=>!G(r))}function xt(e){let t=e.replace(/([.*+?^${}()|\[\]\/\\])/g,"\\$1");return new RegExp(`(url\\(['"]?)(${t})(['"]?\\))`,"g")}var It=["background-image","border-image-source","-webkit-border-image","-webkit-mask-image","list-style-image"];function Dt(e,t){return It.map(n=>{let r=e.getPropertyValue(n);return!r||r==="none?null:((O||z)&&t.drawImageCount++,Ee(r,null,t,!0).then(s=>{!s||r===s||e.setProperty(n,s,e.getPropertyPriority(n))}))}).filter(Boolean)}function Ht(e,t){if(x(e)){let n=e.currentSrc||e.src;if(!G(n))return[R(t,{url:n,imageDom:e,requestType:"image",responseType:"dataUrl"}).then(r=>{r&&(e.srcset="",e.dataset.originalSrc=n,e.src=r||"")})];(O||z)&&t.drawImageCount++}else if(_(e)&&!G(e.href.baseVal)){let n=e.href.baseVal;return[R(t,{url:n,imageDom:e,requestType:"image",responseType:"dataUrl"}).then(r=>{r&&(e.dataset.originalSrc=n,e.href.baseVal=r||"")})]}return[]}function Rt(e,t){let{ownerDocument:n,svgDefsElement:r}=t,s=e.getAttribute("href")??e.getAttribute("xlink:href");if(!s)return[];let[i,a]=s.split("#");if(a){let o=`#${a}`,c=n?.querySelector(`svg ${o}`);if(i&&e.setAttribute("href",o),r?.querySelector(o))return[];if(c)return r?.appendChild(c.cloneNode(!0)),[];if(i)return[R(t,{url:i,responseType:"text"}).then(d=>{r?.insertAdjacentHTML("beforeend",d)})]}return[]}function ve(e,t){let{tasks:n}=t;v(e)&&((x(e)||ce(e))&&n.push(...Ht(e,t)),ke(e)&&n.push(...Rt(e,t))),D(e)&&n.push(...Dt(e.style,t)),e.childNodes.forEach(r=>{ve(r,t)})}async function _t(e,t){let{ownerDocument:n,svgStyleElement:r,fontFamilies:s,fontCssTexts:i,tasks:a,font:o}=t;if(!(!n||!r||!s.size))if(o&&o.cssText){let c=ne(o.cssText,t);r.appendChild(n.createTextNode(`${c}
`))}else{let c=Array.from(n.styleSheets).filter(l=>{try{return"cssRules"in l&&!!l.cssRules.length}catch(u){return t.log.warn(`Error while reading CSS rules from ${l.href}`,u),!1}});await Promise.all(c.flatMap(l=>Array.from(l.cssRules).map(async(u,h)=>{if(Oe(u)){let f=h+1,g=u.href,m="";try{m=await R(t,{url:g,requestType:"text",responseType:"text"})}catch(w){t.log.warn(`Error fetch remote css import from ${g}`,w)}let p=m.replace(ye,(w,b,E)=>w.replace(E,ue(E,g)));for(let w of Ft(p))try{l.insertRule(w,w.startsWith("@import")?f+=1:l.cssRules.length)}catch(b){t.log.warn("Error inserting rule from remote css import",{rule:w,error:b})}}}))),c.flatMap(l=>Array.from(l.cssRules)).filter(l=>Pe(l)&&be(l.style.getPropertyValue("src"))&&ge(l.style.getPropertyValue("font-family")?.[0]).some(u=>s.has(u))).forEach(l=>{let u=l,h=i.get(u.cssText);h?r.appendChild(n.createTextNode(`${h}
`)):a.push(Ee(u.cssText,u.parentStyleSheet?u.parentStyleSheet.href:null,t).then(f=>{f=ne(f,t),i.set(u.cssText,f),r.appendChild(n.createTextNode(`${f}
`))}))})}}var Mt=/(\/\*[\s\S]*?\*\/)/g,te=/((@.*?keyframes [\s\S]*?){([\s\S]*?}\s*?)})/gi;function Ft(e){if(e==null)return[];let t=[],n=e.replace(Mt,"");for(;;){let i=te.exec(n);if(!i)break;t.push(i[0])}n=n.replace(te,"");let r=/@import[\s\S]*?url\([^)]*\)[\s\S]*?;/gi,s=new RegExp("((\\s*?(?:\\/\\*[\\s\\S]*?\\*\\/)?\\s*?@media[\\s\\S]*?){([\\s\\S]*?)}\\s*?})|(([\\s\\S]*?){([\\s\\S]*?)})","gi");for(;;){let i=r.exec(n);if(i)s.lastIndex=r.lastIndex;else if(i=s.exec(n),i)r.lastIndex=s.lastIndex;else break;t.push(i[0])}return t}var Pt=/url\([^)]+\)\s*format\((["']?)([^"']+)\1\)/g,Ot=/src:\s*(?:url\([^)]+\)\s*format\([^)]+\)[,;]\s*)+/g;function ne(e,t){let{font:n}=t,r=n?n?.preferredFormat:void 0;return r?e.replace(Ot,s=>{for(;;){let[i,,a]=Pt.exec(s)||[];if(!a)return"";if(a===r)return`src: ${i};`}}):e}async function kt(e,t){let n=await V(e,t);if(v(n.node)&&_(n.node))return n.node;let{ownerDocument:r,log:s,tasks:i,svgStyleElement:a,svgDefsElement:o,svgStyles:c,font:d,progress:l,autoDestruct:u,onCloneNode:h,onEmbedNode:f,onCreateForeignObjectSvg:g}=n;s.time("clone node");let m=await q(n.node,n,!0);if(a&&r){let y="";c.forEach((C,S)=>{y+=`${C.join(`,
`)} {
  ${S}
}
`}),a.appendChild(r.createTextNode(y))}s.timeEnd("clone node"),await h?.(m),d!==!1&&v(m)&&(s.time("embed web font"),await _t(m,n),s.timeEnd("embed web font")),s.time("embed node"),ve(m,n);let p=i.length,w=0,b=async()=>{for(;;){let y=i.pop();if(!y)break;try{await y}catch(C){n.log.warn("Failed to run task",C)}l?.(++w,p)}};l?.(w,p),await Promise.all([...Array.from({length:4})].map(b)),s.timeEnd("embed node"),await f?.(m);let E=Bt(m,n);return o&&E.insertBefore(o,E.children[0]),a&&E.insertBefore(a,E.children[0]),u&&At(n),await g?.(E),E}function Bt(e,t){let{width:n,height:r}=t,s=Ke(n,r,e.ownerDocument),i=s.ownerDocument.createElementNS(s.namespaceURI,"foreignObject");return i.setAttributeNS(null,"x","0%"),i.setAttributeNS(null,"y","0%"),i.setAttributeNS(null,"width","100%"),i.setAttributeNS(null,"height","100%"),i.append(e),s.appendChild(i),s}async function Ut(e,t){let n=await V(e,t),r=await kt(n),s=Qe(r,n.isEnable("removeControlCharacter"));n.autoDestruct||(n.svgStyleElement=fe(n.ownerDocument),n.svgDefsElement=n.ownerDocument?.createElementNS(U,"defs"),n.svgStyles.clear());let i=N(s,r.ownerDocument);return await lt(i,n)}async function Se(e,t){let n=await V(e,t),{log:r,type:s,quality:i,dpi:a}=n,o=await Ut(n);r.time("canvas to blob");let c=await Ze(o,s,i);if(["image/png","image/jpeg"].includes(s)&&a){let d=await nt(c.slice(0,33)),l=new Uint8Array(d);return s==="image/png"?l=Re(l,a):s==="image/jpeg"&&(l=xe(l,a)),r.timeEnd("canvas to blob"),new Blob([l,c.slice(33)],{type:s})}return r.timeEnd("canvas to blob"),c}var X={METADATA:"data-replit-metadata",COMPONENT_NAME:"data-component-name"};function Ce(e){if(e.startsWith("http://localhost:"))return!0;try{return new URL(e).hostname.endsWith(T.ALLOWED_DOMAIN)}catch{return!1}}function Te(e){return e?document.elementFromPoint(e.clientX,e.clientY):null}function L(e,t=300){if(!e)return"";let n=String(e);return n.length<=t?n:n.slice(0,t)+"..."}function Y(e){if(e)return{tagName:e.tagName.toLowerCase(),className:e.className.toString?e.className.toString():String(e.className),textContent:L(e.textContent??""),innerHTML:L(e.innerHTML??""),id:L(e.id,100)}}function $(e){return e.getAttribute(X.COMPONENT_NAME)??e.tagName.toLowerCase()}function Ae(e){let t=window.getComputedStyle(e),n=e.parentElement,r=e.nextElementSibling,s=n?.parentElement??null,i={backgroundColor:t.backgroundColor,color:t.color,display:t.display,position:t.position,width:t.width,height:t.height,fontSize:t.fontSize,fontFamily:t.fontFamily,fontWeight:t.fontWeight,margin:t.margin,padding:t.padding};return{elementPath:e.getAttribute(X.METADATA)??"",elementName:$(e),textContent:L(e.textContent??""),id:L(e.id,100),className:L(e.className.toString?e.className.toString():String(e.className),100),innerHTML:L(e.innerHTML,100),computedStyles:i,relatedElements:{parent:Y(n),nextSibling:Y(r),grandParent:Y(s)}}}async function Le(e){try{let n=window.getComputedStyle(e).backgroundColor;return $t(n)&&(n=window.getComputedStyle(document.documentElement).backgroundColor),await Se(e,{type:"image/png",backgroundColor:n,fetch:{requestInit:{mode:"no-cors"}}})}catch(t){console.error("[replit-cartographer] Failed to take screenshot:",t);return}}function $t(e){return e==="transparent"||e==="rgba(0, 0, 0, 0)"||e.endsWith(", 0)")||e.endsWith(",0)")}var M=class{selectedElement=null;isActive=!1;lastHighlightedElement=null;shadowHost=null;shadowRoot=null;hoverHighlighter=null;hoverLabel=null;selectedHighlighter=null;selectedLabel=null;constructor(){this.setupMessageListener(),this.notifyScriptLoaded()}initializeHighlighter(){this.shadowHost=document.createElement("div"),this.shadowHost.style.all="initial",this.shadowRoot=this.shadowHost.attachShadow({mode:"open"}),document.body.appendChild(this.shadowHost),this.hoverHighlighter=document.createElement("div"),this.hoverLabel=document.createElement("div"),Object.assign(this.hoverHighlighter.style,{...I.highlighter,zIndex:Number.MAX_SAFE_INTEGER,pointerEvents:"all",position:"fixed"}),Object.assign(this.hoverLabel.style,{...I.label,zIndex:Number.MAX_SAFE_INTEGER,pointerEvents:"all",position:"fixed"}),this.selectedHighlighter=document.createElement("div"),this.selectedLabel=document.createElement("div"),Object.assign(this.selectedHighlighter.style,{...I.highlighter,pointerEvents:"none",position:"fixed"}),Object.assign(this.selectedLabel.style,{...I.label,pointerEvents:"none",position:"fixed"}),this.shadowRoot.appendChild(this.selectedHighlighter),this.shadowRoot.appendChild(this.selectedLabel),this.shadowRoot.appendChild(this.hoverHighlighter),this.shadowRoot.appendChild(this.hoverLabel)}setupMessageListener(){window.addEventListener("message",this.handleMessage.bind(this))}notifyScriptLoaded(){this.postMessageToParent({type:"SELECTOR_SCRIPT_LOADED",timestamp:Date.now(),version:P})}postMessageToParent(t){window.parent&&window.parent.postMessage(t,"*")}handleMouseMove=t=>{if(this.isActive&&this.hoverHighlighter){this.hoverHighlighter.style.pointerEvents="none";let n=Te(t);if(!n||n===this.hoverHighlighter||n===this.selectedHighlighter||n===this.shadowHost){this.hideHighlight(this.hoverHighlighter,this.hoverLabel),this.lastHighlightedElement=null;return}this.lastHighlightedElement=n,this.hoverHighlighter.style.pointerEvents="all",this.hoverHighlighter.style.border=`2px dashed ${T.HIGHLIGHT_COLOR}`,this.updateHighlighterPosition(n,this.hoverHighlighter,this.hoverLabel)}};handleMouseLeave=()=>{this.isActive&&this.hideHighlight(this.hoverHighlighter,this.hoverLabel)};calculateLabelPosition(t,n){return n<24?{top:`${n+window.scrollY}px`,left:`${t.left+window.scrollX}px`,transform:"none",marginTop:"2px"}:{top:`${n+window.scrollY}px`,left:`${t.left+window.scrollX}px`,transform:"translateY(-100%)",marginTop:"-4px"}}updateHighlighterPosition(t,n,r){if(!n||!r)return;let s=t.getBoundingClientRect(),i=window.innerHeight,a=Math.max(0,s.top),o=Math.min(i,s.bottom),c=Math.max(0,o-a);Object.assign(n.style,{opacity:c>0?"1":"0",top:`${a}px`,left:`${s.left}px`,width:`${s.width}px`,height:`${c}px`}),r.textContent=$(t);let d=this.calculateLabelPosition(s,a);d.top=`${a}px`,d.left=`${s.left}px`,Object.assign(r.style,{...d,opacity:c>0?"1":"0"})}hideHighlight(t,n){t&&(t.style.opacity="0"),n&&(n.style.opacity="0")}handleClick=async t=>{if(!this.isActive)return;t.preventDefault(),t.stopPropagation();let n=this.lastHighlightedElement;if(!n)return;if(n===this.selectedElement){this.unselectCurrentElement(),this.hideHighlight(this.selectedHighlighter,this.selectedLabel),this.postMessageToParent({type:"ELEMENT_UNSELECTED",timestamp:Date.now()});return}this.selectedElement=n,this.selectedHighlighter&&this.selectedLabel&&(this.selectedHighlighter.style.border=`2px solid ${T.HIGHLIGHT_COLOR}`,this.selectedHighlighter.style.opacity="1",this.selectedLabel.style.opacity="1",this.selectedLabel.textContent=$(n)),this.updateHighlighterPosition(n,this.selectedHighlighter,this.selectedLabel);let r=Ae(n),s;try{s=await Le(n)}catch(i){console.error("[replit-cartographer] Error capturing element screenshot:",i)}this.postMessageToParent({type:"ELEMENT_SELECTED",payload:{...r,screenshotBlob:s??void 0},timestamp:Date.now()})};unselectCurrentElement(){this.selectedElement&&(this.selectedElement=null)}handleMessage=t=>{if(!Ce(t.origin))return;let n=t.data;if(!(!n||typeof n!="object"))switch(n.type){case"TOGGLE_REPLIT_VISUAL_EDITOR":{this.handleVisualEditorToggle(n.enabled);break}case"CLEAR_SELECTION":{this.unselectCurrentElement(),this.hideHighlight(this.selectedHighlighter,this.selectedLabel);break}}};handleVisualEditorToggle(t){let n=!!t;n?this.postMessageToParent({type:"REPLIT_VISUAL_EDITOR_ENABLED",timestamp:Date.now()}):this.postMessageToParent({type:"REPLIT_VISUAL_EDITOR_DISABLED",timestamp:Date.now()}),this.isActive!==n&&(this.isActive=n,this.toggleEventListeners(n))}recalculateSelectedElement=()=>{this.isActive&&(this.selectedElement&&this.updateHighlighterPosition(this.selectedElement,this.selectedHighlighter,this.selectedLabel),this.lastHighlightedElement&&this.updateHighlighterPosition(this.lastHighlightedElement,this.hoverHighlighter,this.hoverLabel))};toggleEventListeners(t){t?(this.initializeHighlighter(),document.addEventListener("mousemove",this.handleMouseMove),document.addEventListener("mouseleave",this.handleMouseLeave),document.addEventListener("click",this.handleClick,!0),window.addEventListener("resize",this.recalculateSelectedElement),window.addEventListener("scroll",this.recalculateSelectedElement,!0),document.body.style.cursor="pointer"):(document.removeEventListener("mousemove",this.handleMouseMove),document.removeEventListener("click",this.handleClick,!0),document.removeEventListener("mouseleave",this.handleMouseLeave),window.removeEventListener("resize",this.recalculateSelectedElement),window.removeEventListener("scroll",this.recalculateSelectedElement,!0),this.hoverHighlighter?.remove(),this.hoverLabel?.remove(),this.selectedHighlighter?.remove(),this.selectedLabel?.remove(),this.shadowHost?.remove(),this.hoverHighlighter=null,this.hoverLabel=null,this.selectedHighlighter=null,this.selectedLabel=null,this.shadowHost=null,this.shadowRoot=null,document.body.style.cursor="",this.selectedElement=null)}};if(typeof window<"u")try{window.REPLIT_BEACON_VERSION||(window.REPLIT_BEACON_VERSION=P,new M)}catch(e){console.error("[replit-beacon] Failed to initialize:",e)}})();
</script>
  <style>*, ::before, ::after{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }::backdrop{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }/* ! tailwindcss v3.4.16 | MIT License | https://tailwindcss.com */*,::after,::before{box-sizing:border-box;border-width:0;border-style:solid;border-color:#e5e7eb}::after,::before{--tw-content:''}:host,html{line-height:1.5;-webkit-text-size-adjust:100%;-moz-tab-size:4;tab-size:4;font-family:ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";font-feature-settings:normal;font-variation-settings:normal;-webkit-tap-highlight-color:transparent}body{margin:0;line-height:inherit}hr{height:0;color:inherit;border-top-width:1px}abbr:where([title]){-webkit-text-decoration:underline dotted;text-decoration:underline dotted}h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight:inherit}a{color:inherit;text-decoration:inherit}b,strong{font-weight:bolder}code,kbd,pre,samp{font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;font-feature-settings:normal;font-variation-settings:normal;font-size:1em}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}table{text-indent:0;border-color:inherit;border-collapse:collapse}button,input,optgroup,select,textarea{font-family:inherit;font-feature-settings:inherit;font-variation-settings:inherit;font-size:100%;font-weight:inherit;line-height:inherit;letter-spacing:inherit;color:inherit;margin:0;padding:0}button,select{text-transform:none}button,input:where([type=button]),input:where([type=reset]),input:where([type=submit]){-webkit-appearance:button;background-color:transparent;background-image:none}:-moz-focusring{outline:auto}:-moz-ui-invalid{box-shadow:none}progress{vertical-align:baseline}::-webkit-inner-spin-button,::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}blockquote,dd,dl,figure,h1,h2,h3,h4,h5,h6,hr,p,pre{margin:0}fieldset{margin:0;padding:0}legend{padding:0}menu,ol,ul{list-style:none;margin:0;padding:0}dialog{padding:0}textarea{resize:vertical}input::placeholder,textarea::placeholder{opacity:1;color:#9ca3af}[role=button],button{cursor:pointer}:disabled{cursor:default}audio,canvas,embed,iframe,img,object,svg,video{display:block;vertical-align:middle}img,video{max-width:100%;height:auto}[hidden]:where(:not([hidden=until-found])){display:none}.container{width:100%}@media (min-width: 640px){.container{max-width:640px}}@media (min-width: 768px){.container{max-width:768px}}@media (min-width: 1024px){.container{max-width:1024px}}@media (min-width: 1280px){.container{max-width:1280px}}@media (min-width: 1536px){.container{max-width:1536px}}.pointer-events-none{pointer-events:none}.fixed{position:fixed}.absolute{position:absolute}.relative{position:relative}.sticky{position:sticky}.inset-0{inset:0px}.-left-20{left:-5rem}.bottom-0{bottom:0px}.bottom-1\/3{bottom:33.333333%}.left-0{left:0px}.left-\[10\%\]{left:10%}.left-\[15\%\]{left:15%}.left-\[5\%\]{left:5%}.right-6{right:1.5rem}.right-\[20\%\]{right:20%}.right-\[5\%\]{right:5%}.top-0{top:0px}.top-1\/2{top:50%}.top-1\/3{top:33.333333%}.top-1\/4{top:25%}.top-6{top:1.5rem}.top-\[5\%\]{top:5%}.bottom-10{bottom:2.5rem}.bottom-4{bottom:1rem}.left-4{left:1rem}.right-0{right:0px}.right-4{right:1rem}.top-20{top:5rem}.top-32{top:8rem}.z-10{z-index:10}.z-30{z-index:30}.z-40{z-index:40}.z-50{z-index:50}.col-span-full{grid-column:1 / -1}.mx-auto{margin-left:auto;margin-right:auto}.mb-10{margin-bottom:2.5rem}.mb-12{margin-bottom:3rem}.mb-2{margin-bottom:0.5rem}.mb-3{margin-bottom:0.75rem}.mb-6{margin-bottom:1.5rem}.mb-8{margin-bottom:2rem}.mt-2{margin-top:0.5rem}.mt-8{margin-top:2rem}.mb-1{margin-bottom:0.25rem}.mb-4{margin-bottom:1rem}.ml-2{margin-left:0.5rem}.mr-1{margin-right:0.25rem}.mr-2{margin-right:0.5rem}.mr-4{margin-right:1rem}.mt-1{margin-top:0.25rem}.mt-10{margin-top:2.5rem}.mt-auto{margin-top:auto}.block{display:block}.inline-block{display:inline-block}.inline{display:inline}.flex{display:flex}.grid{display:grid}.hidden{display:none}.h-1{height:0.25rem}.h-16{height:4rem}.h-20{height:5rem}.h-24{height:6rem}.h-32{height:8rem}.h-40{height:10rem}.h-6{height:1.5rem}.h-8{height:2rem}.h-\[400px\]{height:400px}.h-\[90\%\]{height:90%}.h-full{height:100%}.h-0\.5{height:0.125rem}.h-10{height:2.5rem}.h-12{height:3rem}.h-14{height:3.5rem}.h-4{height:1rem}.h-5{height:1.25rem}.h-64{height:16rem}.h-fit{height:-moz-fit-content;height:fit-content}.max-h-\[60vh\]{max-height:60vh}.min-h-\[300px\]{min-height:300px}.min-h-screen{min-height:100vh}.w-16{width:4rem}.w-20{width:5rem}.w-24{width:6rem}.w-32{width:8rem}.w-40{width:10rem}.w-6{width:1.5rem}.w-8{width:2rem}.w-\[90\%\]{width:90%}.w-full{width:100%}.w-1\/3{width:33.333333%}.w-10{width:2.5rem}.w-12{width:3rem}.w-14{width:3.5rem}.w-4{width:1rem}.w-5{width:1.25rem}.w-64{width:16rem}.max-w-4xl{max-width:56rem}.max-w-5xl{max-width:64rem}.max-w-6xl{max-width:72rem}.max-w-7xl{max-width:80rem}.max-w-3xl{max-width:48rem}.max-w-xl{max-width:36rem}.flex-1{flex:1 1 0%}.origin-left{transform-origin:left}.translate-y-4{--tw-translate-y:1rem;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.-translate-y-1\/2{--tw-translate-y:-50%;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.scale-95{--tw-scale-x:.95;--tw-scale-y:.95;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.scale-x-0{--tw-scale-x:0;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.transform{transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.transform-gpu{transform:translate3d(var(--tw-translate-x), var(--tw-translate-y), 0) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.cursor-pointer{cursor:pointer}.grid-cols-1{grid-template-columns:repeat(1, minmax(0, 1fr))}.flex-col{flex-direction:column}.flex-wrap{flex-wrap:wrap}.items-start{align-items:flex-start}.items-center{align-items:center}.justify-center{justify-content:center}.justify-between{justify-content:space-between}.gap-6{gap:1.5rem}.gap-8{gap:2rem}.gap-1{gap:0.25rem}.gap-10{gap:2.5rem}.gap-12{gap:3rem}.gap-2{gap:0.5rem}.gap-3{gap:0.75rem}.gap-4{gap:1rem}.space-x-8 > :not([hidden]) ~ :not([hidden]){--tw-space-x-reverse:0;margin-right:calc(2rem * var(--tw-space-x-reverse));margin-left:calc(2rem * calc(1 - var(--tw-space-x-reverse)))}.space-y-3 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.75rem * calc(1 - var (--tw-space-y-reverse)));margin-bottom:calc(0.75rem * var(--tw-space-y-reverse))}.space-y-2 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.5rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.5rem * var(--tw-space-y-reverse))}.space-y-4 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1rem * var(--tw-space-y-reverse))}.space-y-6 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1.5rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1.5rem * var(--tw-space-y-reverse))}.overflow-hidden{overflow:hidden}.overflow-x-auto{overflow-x:auto}.overflow-y-auto{overflow-y:auto}.rounded-2xl{border-radius:1rem}.rounded-full{border-radius:9999px}.rounded-lg{border-radius:0.5rem}.rounded-xl{border-radius:0.75rem}.border{border-width:1px}.border-2{border-width:2px}.border-8{border-width:8px}.border-b-2{border-bottom-width:2px}.border-b-4{border-bottom-width:4px}.border-b{border-bottom-width:1px}.border-t{border-top-width:1px}.border-creche-orange{--tw-border-opacity:1;border-color:rgb(255 140 97 / var(--tw-border-opacity, 1))}.border-transparent{border-color:transparent}.border-creche-blue{--tw-border-opacity:1;border-color:rgb(93 173 236 / var(--tw-border-opacity, 1))}.border-creche-blue\/30{border-color:rgb(93 173 236 / 0.3)}.border-creche-green{--tw-border-opacity:1;border-color:rgb(163 228 168 / var(--tw-border-opacity, 1))}.border-gray-100{--tw-border-opacity:1;border-color:rgb(243 244 246 / var(--tw-border-opacity, 1))}.border-gray-200{--tw-border-opacity:1;border-color:rgb(229 231 235 / var(--tw-border-opacity, 1))}.border-gray-800{--tw-border-opacity:1;border-color:rgb(31 41 55 / var(--tw-border-opacity, 1))}.border-white{--tw-border-opacity:1;border-color:rgb(255 255 255 / var(--tw-border-opacity, 1))}.bg-\[\#5DADEC\]\/10{background-color:rgb(93 173 236 / 0.1)}.bg-\[\#B7C4CF\]{--tw-bg-opacity:1;background-color:rgb(183 196 207 / var(--tw-bg-opacity, 1))}.bg-\[\#C1D8C3\]{--tw-bg-opacity:1;background-color:rgb(193 216 195 / var(--tw-bg-opacity, 1))}.bg-\[\#D3BFC1\]{--tw-bg-opacity:1;background-color:rgb(211 191 193 / var(--tw-bg-opacity, 1))}.bg-\[\#F0E9B4\]{--tw-bg-opacity:1;background-color:rgb(240 233 180 / var(--tw-bg-opacity, 1))}.bg-blue-100{--tw-bg-opacity:1;background-color:rgb(219 234 254 / var(--tw-bg-opacity, 1))}.bg-blue-200{--tw-bg-opacity:1;background-color:rgb(191 219 254 / var(--tw-bg-opacity, 1))}.bg-creche-blue{--tw-bg-opacity:1;background-color:rgb(93 173 236 / var(--tw-bg-opacity, 1))}.bg-creche-blue\/20{background-color:rgb(93 173 236 / 0.2)}.bg-creche-green{--tw-bg-opacity:1;background-color:rgb(163 228 168 / var(--tw-bg-opacity, 1))}.bg-creche-green\/20{background-color:rgb(163 228 168 / 0.2)}.bg-creche-green\/30{background-color:rgb(163 228 168 / 0.3)}.bg-creche-orange{--tw-bg-opacity:1;background-color:rgb(255 140 97 / var(--tw-bg-opacity, 1))}.bg-creche-orange\/20{background-color:rgb(255 140 97 / 0.2)}.bg-gray-100{--tw-bg-opacity:1;background-color:rgb(243 244 246 / var(--tw-bg-opacity, 1))}.bg-white{--tw-bg-opacity:1;background-color:rgb(255 255 255 / var(--tw-bg-opacity, 1))}.bg-white\/60{background-color:rgb(255 255 255 / 0.6)}.bg-white\/95{background-color:rgb(255 255 255 / 0.95)}.bg-yellow-200\/30{background-color:rgb(254 240 138 / 0.3)}.bg-blue-300{--tw-bg-opacity:1;background-color:rgb(147 197 253 / var(--tw-bg-opacity, 1))}.bg-blue-400{--tw-bg-opacity:1;background-color:rgb(96 165 250 / var(--tw-bg-opacity, 1))}.bg-blue-50\/50{background-color:rgb(239 246 255 / 0.5)}.bg-blue-500{--tw-bg-opacity:1;background-color:rgb(59 130 246 / var(--tw-bg-opacity, 1))}.bg-creche-blue\/30{background-color:rgb(93 173 236 / 0.3)}.bg-creche-orange\/10{background-color:rgb(255 140 97 / 0.1)}.bg-gray-300{--tw-bg-opacity:1;background-color:rgb(209 213 219 / var(--tw-bg-opacity, 1))}.bg-gray-900{--tw-bg-opacity:1;background-color:rgb(17 24 39 / var(--tw-bg-opacity, 1))}.bg-green-100{--tw-bg-opacity:1;background-color:rgb(220 252 231 / var(--tw-bg-opacity, 1))}.bg-green-200{--tw-bg-opacity:1;background-color:rgb(187 247 208 / var(--tw-bg-opacity, 1))}.bg-pink-200{--tw-bg-opacity:1;background-color:rgb(251 207 232 / var(--tw-bg-opacity, 1))}.bg-pink-600{--tw-bg-opacity:1;background-color:rgb(219 39 119 / var(--tw-bg-opacity, 1))}.bg-purple-100{--tw-bg-opacity:1;background-color:rgb(243 232 255 / var(--tw-bg-opacity, 1))}.bg-purple-200{--tw-bg-opacity:1;background-color:rgb(233 213 255 / var(--tw-bg-opacity, 1))}.bg-red-600{--tw-bg-opacity:1;background-color:rgb(220 38 38 / var(--tw-bg-opacity, 1))}.bg-white\/90{background-color:rgb(255 255 255 / 0.9)}.bg-yellow-100{--tw-bg-opacity:1;background-color:rgb(254 249 195 / var(--tw-bg-opacity, 1))}.bg-gradient-to-b{background-image:linear-gradient(to bottom, var(--tw-gradient-stops))}.bg-gradient-to-br{background-image:linear-gradient(to bottom right, var(--tw-gradient-stops))}.bg-gradient-to-t{background-image:linear-gradient(to top, var(--tw-gradient-stops))}.from-\[\#e1eeff\]{--tw-gradient-from:#e1eeff var(--tw-gradient-from-position);--tw-gradient-to:rgb(225 238 255 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-\[\#e1f5e4\]{--tw-gradient-from:#e1f5e4 var(--tw-gradient-from-position);--tw-gradient-to:rgb(225 245 228 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-\[\#f0f9ff\]{--tw-gradient-from:#f0f9ff var(--tw-gradient-from-position);--tw-gradient-to:rgb(240 249 255 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-\[\#fff4e1\]{--tw-gradient-from:#fff4e1 var(--tw-gradient-from-position);--tw-gradient-to:rgb(255 244 225 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-blue-50{--tw-gradient-from:#eff6ff var(--tw-gradient-from-position);--tw-gradient-to:rgb(239 246 255 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-white{--tw-gradient-from:#fff var(--tw-gradient-from-position);--tw-gradient-to:rgb(255 255 255 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-white\/40{--tw-gradient-from:rgb(255 255 255 / 0.4) var(--tw-gradient-from-position);--tw-gradient-to:rgb(255 255 255 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.from-creche-blue\/10{--tw-gradient-from:rgb(93 173 236 / 0.1) var(--tw-gradient-from-position);--tw-gradient-to:rgb(93 173 236 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.via-\[\#e6f7ff\]{--tw-gradient-to:rgb(230 247 255 / 0)  var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), #e6f7ff var(--tw-gradient-via-position), var(--tw-gradient-to)}.to-\[\#c9e7ff\]{--tw-gradient-to:#c9e7ff var(--tw-gradient-to-position)}.to-\[\#c9f0d0\]{--tw-gradient-to:#c9f0d0 var(--tw-gradient-to-position)}.to-\[\#f0f9ff\]{--tw-gradient-to:#f0f9ff var(--tw-gradient-to-position)}.to-\[\#ffe9c9\]{--tw-gradient-to:#ffe9c9 var(--tw-gradient-to-position)}.to-blue-50\/20{--tw-gradient-to:rgb(239 246 255 / 0.2) var(--tw-gradient-to-position)}.to-creche-cream\/30{--tw-gradient-to:rgb(255 246 233 / 0.3) var(--tw-gradient-to-position)}.to-transparent{--tw-gradient-to:transparent var(--tw-gradient-to-position)}.to-creche-cream\/20{--tw-gradient-to:rgb(255 246 233 / 0.2) var(--tw-gradient-to-position)}.p-10{padding:2.5rem}.p-2{padding:0.5rem}.p-4{padding:1rem}.p-6{padding:1.5rem}.p-8{padding:2rem}.p-3{padding:0.75rem}.px-1{padding-left:0.25rem;padding-right:0.25rem}.px-2{padding-left:0.5rem;padding-right:0.5rem}.px-4{padding-left:1rem;padding-right:1rem}.px-5{padding-left:1.25rem;padding-right:1.25rem}.px-6{padding-left:1.5rem;padding-right:1.5rem}.py-1{padding-top:0.25rem;padding-bottom:0.25rem}.py-1\.5{padding-top:0.375rem;padding-bottom:0.375rem}.py-12{padding-top:3rem;padding-bottom:3rem}.py-16{padding-top:4rem;padding-bottom:4rem}.py-2{padding-top:0.5rem;padding-bottom:0.5rem}.py-20{padding-top:5rem;padding-bottom:5rem}.py-4{padding-top:1rem;padding-bottom:1rem}.px-8{padding-left:2rem;padding-right:2rem}.py-10{padding-top:2.5rem;padding-bottom:2.5rem}.py-24{padding-top:6rem;padding-bottom:6rem}.py-3{padding-top:0.75rem;padding-bottom:0.75rem}.pb-24{padding-bottom:6rem}.pt-20{padding-top:5rem}.pb-4{padding-bottom:1rem}.pr-2{padding-right:0.5rem}.pt-4{padding-top:1rem}.pt-6{padding-top:1.5rem}.text-left{text-align:left}.text-center{text-align:center}.font-poppins{font-family:Poppins, sans-serif}.text-2xl{font-size:1.5rem;line-height:2rem}.text-3xl{font-size:1.875rem;line-height:2.25rem}.text-4xl{font-size:2.25rem;line-height:2.5rem}.text-lg{font-size:1.125rem;line-height:1.75rem}.text-xl{font-size:1.25rem;line-height:1.75rem}.text-sm{font-size:0.875rem;line-height:1.25rem}.text-xs{font-size:0.75rem;line-height:1rem}.font-bold{font-weight:700}.font-medium{font-weight:500}.font-semibold{font-weight:600}.leading-relaxed{line-height:1.625}.tracking-tight{letter-spacing:-0.025em}.text-\[\#6D6875\]{--tw-text-opacity:1;color:rgb(109 104 117 / var(--tw-text-opacity, 1))}.text-creche-blue{--tw-text-opacity:1;color:rgb(93 173 236 / var(--tw-text-opacity, 1))}.text-creche-gray{--tw-text-opacity:1;color:rgb(109 104 117 / var(--tw-text-opacity, 1))}.text-creche-gray\/80{color:rgb(109 104 117 / 0.8)}.text-creche-green{--tw-text-opacity:1;color:rgb(163 228 168 / var(--tw-text-opacity, 1))}.text-creche-orange{--tw-text-opacity:1;color:rgb(255 140 97 / var(--tw-text-opacity, 1))}.text-white{--tw-text-opacity:1;color:rgb(255 255 255 / var(--tw-text-opacity, 1))}.text-blue-400{--tw-text-opacity:1;color:rgb(96 165 250 / var(--tw-text-opacity, 1))}.text-blue-500{--tw-text-opacity:1;color:rgb(59 130 246 / var(--tw-text-opacity, 1))}.text-blue-700{--tw-text-opacity:1;color:rgb(29 78 216 / var(--tw-text-opacity, 1))}.text-creche-gray\/70{color:rgb(109 104 117 / 0.7)}.text-creche-orange\/80{color:rgb(255 140 97 / 0.8)}.text-gray-400{--tw-text-opacity:1;color:rgb(156 163 175 / var(--tw-text-opacity, 1))}.text-gray-500{--tw-text-opacity:1;color:rgb(107 114 128 / var(--tw-text-opacity, 1))}.text-green-500{--tw-text-opacity:1;color:rgb(34 197 94 / var(--tw-text-opacity, 1))}.text-green-700{--tw-text-opacity:1;color:rgb(21 128 61 / var(--tw-text-opacity, 1))}.text-pink-500{--tw-text-opacity:1;color:rgb(236 72 153 / var(--tw-text-opacity, 1))}.text-purple-500{--tw-text-opacity:1;color:rgb(168 85 247 / var(--tw-text-opacity, 1))}.text-purple-700{--tw-text-opacity:1;color:rgb(126 34 206 / var(--tw-text-opacity, 1))}.opacity-0{opacity:0}.opacity-30{opacity:0.3}.opacity-40{opacity:0.4}.opacity-50{opacity:0.5}.opacity-60{opacity:0.6}.opacity-70{opacity:0.7}.opacity-75{opacity:0.75}.shadow-2xl{--tw-shadow:0 25px 50px -12px rgb(0 0 0 / 0.25);--tw-shadow-colored:0 25px 50px -12px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-lg{--tw-shadow:0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 10px 15px -3px var(--tw-shadow-color), 0 4px 6px -4px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-md{--tw-shadow:0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 4px 6px -1px var(--tw-shadow-color), 0 2px 4px -2px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var (--tw-shadow)}.shadow-sm{--tw-shadow:0 1px 2px 0 rgb(0 0 0 / 0.05);--tw-shadow-colored:0 1px 2px 0 var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-xl{--tw-shadow:0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 20px 25px -5px var(--tw-shadow-color), 0 8px 10px -6px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.blur-lg{--tw-blur:blur(16px);filter:var(--tw-blur) var(--tw-brightness) var(--tw-contrast) var(--tw-grayscale) var (--tw-hue-rotate) var(--tw-invert) var(--tw-saturate) var(--tw-sepia) var(--tw-drop-shadow)}.backdrop-blur-md{--tw-backdrop-blur:blur(12px);-webkit-backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia);backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia)}.backdrop-blur-xl{--tw-backdrop-blur:blur(24px);-webkit-backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia);backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia)}.backdrop-blur-sm{--tw-backdrop-blur:blur(4px);-webkit-backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia);backdrop-filter:var(--tw-backdrop-blur) var(--tw-backdrop-brightness) var(--tw-backdrop-contrast) var(--tw-backdrop-grayscale) var(--tw-backdrop-hue-rotate) var(--tw-backdrop-invert) var(--tw-backdrop-opacity) var(--tw-backdrop-saturate) var(--tw-backdrop-sepia)}.transition-all{transition-property:all;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.transition-colors{transition-property:color, background-color, border-color, fill, stroke, -webkit-text-decoration-color;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, -webkit-text-decoration-color;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.transition-opacity{transition-property:opacity;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.transition-shadow{transition-property:box-shadow;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.transition-transform{transition-property:transform;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.delay-100{transition-delay:100ms}.duration-300{transition-duration:300ms}.duration-500{transition-duration:500ms}.ease-in-out{transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1)}.hover\:z-10:hover{z-index:10}.hover\:-translate-y-2:hover{--tw-translate-y:-0.5rem;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.hover\:scale-110:hover{--tw-scale-x:1.1;--tw-scale-y:1.1;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.hover\:scale-\[1\.02\]:hover{--tw-scale-x:1.02;--tw-scale-y:1.02;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.hover\:scale-105:hover{--tw-scale-x:1.05;--tw-scale-y:1.05;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.hover\:border-creche-blue:hover{--tw-border-opacity:1;border-color:rgb(93 173 236 / var(--tw-border-opacity, 1))}.hover\:bg-\[\#5DADEC\]\/20:hover{background-color:rgb(93 173 236 / 0.2)}.hover\:bg-gray-200:hover{--tw-bg-opacity:1;background-color:rgb(229 231 235 / var(--tw-bg-opacity, 1))}.hover\:bg-blue-500:hover{--tw-bg-opacity:1;background-color:rgb(59 130 246 / var(--tw-bg-opacity, 1))}.hover\:bg-blue-600:hover{--tw-bg-opacity:1;background-color:rgb(37 99 235 / var(--tw-bg-opacity, 1))}.hover\:bg-creche-blue\/80:hover{background-color:rgb(93 173 236 / 0.8)}.hover\:bg-creche-green\/80:hover{background-color:rgb(163 228 168 / 0.8)}.hover\:bg-gray-50:hover{--tw-bg-opacity:1;background-color:rgb(249 250 251 / var(--tw-bg-opacity, 1))}.hover\:bg-pink-700:hover{--tw-bg-opacity:1;background-color:rgb(190 24 93 / var(--tw-bg-opacity, 1))}.hover\:bg-red-700:hover{--tw-bg-opacity:1;background-color:rgb(185 28 28 / var(--tw-bg-opacity, 1))}.hover\:text-creche-blue:hover{--tw-text-opacity:1;color:rgb(93 173 236 / var(--tw-text-opacity, 1))}.hover\:text-creche-blue\/80:hover{color:rgb(93 173 236 / 0.8)}.hover\:underline:hover{-webkit-text-decoration-line:underline;text-decoration-line:underline}.hover\:shadow-lg:hover{--tw-shadow:0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 10px 15px -3px var(--tw-shadow-color), 0 4px 6px -4px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.hover\:shadow-xl:hover{--tw-shadow:0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 20px 25px -5px var(--tw-shadow-color), 0 8px 10px -6px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.hover\:shadow-\[0_0_20px_rgba\(0\2c 0\2c 0\2c 0\.1\)\]:hover{--tw-shadow:0 0 20px rgba(0,0,0,0.1);--tw-shadow-colored:0 0 20px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.hover\:shadow-md:hover{--tw-shadow:0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 4px 6px -1px var(--tw-shadow-color), 0 2px 4px -2px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.focus\:outline-none:focus{outline:2px solid transparent;outline-offset:2px}.focus\:ring-2:focus{--tw-ring-offset-shadow:var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);--tw-ring-shadow:var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width)) var(--tw-ring-color);box-shadow:var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var (--tw-shadow, 0 0 #0000)}.focus\:ring-\[\#5DADEC\]:focus{--tw-ring-opacity:1;--tw-ring-color:rgb(93 173 236 / var(--tw-ring-opacity, 1))}.group:hover .group-hover\:scale-110{--tw-scale-x:1.1;--tw-scale-y:1.1;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.group:hover .group-hover\:scale-x-100{--tw-scale-x:1;transform:translate(var(--tw-translate-x), var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y))}.group:hover .group-hover\:text-creche-blue{--tw-text-opacity:1;color:rgb(93 173 236 / var(--tw-text-opacity, 1))}.group:hover .group-hover\:text-creche-green{--tw-text-opacity:1;color:rgb(163 228 168 / var(--tw-text-opacity, 1))}.group:hover .group-hover\:text-creche-orange{--tw-text-opacity:1;color:rgb(255 140 97 / var(--tw-text-opacity, 1))}@media (min-width: 768px){.md\:flex{display:flex}.md\:hidden{display:none}.md\:h-\[400px\]{height:400px}.md\:h-72{height:18rem}.md\:w-1\/4{width:25%}.md\:w-3\/4{width:75%}.md\:w-72{width:18rem}.md\:grid-cols-3{grid-template-columns:repeat(3, minmax(0, 1fr))}.md\:grid-cols-2{grid-template-columns:repeat(2, minmax(0, 1fr))}.md\:flex-row{flex-direction:row}.md\:gap-10{gap:2.5rem}.md\:py-20{padding-top:5rem;padding-bottom:5rem}.md\:py-28{padding-top:7rem;padding-bottom:7rem}.md\:text-2xl{font-size:1.5rem;line-height:2rem}.md\:text-5xl{font-size:3rem;line-height:1}}@media (min-width: 1024px){.lg\:w-1\/4{width:25%}.lg\:w-3\/4{width:75%}.lg\:flex-row{flex-direction:row}.lg\:gap-24{gap:6rem}}</style></head>
  <body class="flex flex-col min-h-screen">
    <!-- Overlay global avec flou léger -->
    <div id="overlay" class="fixed inset-0 bg-white/60 backdrop-blur-xl z-40 hidden transition-opacity duration-300 ease-in-out"></div>
    
    <!-- Fiche détaillée avec effet de détachement -->
    <div id="fiche-zoom" class="fixed top-[5%] left-[5%] w-[90%] h-[90%] bg-white/95 backdrop-blur-md rounded-2xl shadow-2xl p-10 z-50 transition-all duration-500 ease-in-out opacity-0 scale-95 pointer-events-none transform-gpu" role="dialog" aria-modal="true" aria-labelledby="fiche-titre">
      <!-- Bouton fermer -->
      <button id="close-detail" class="absolute top-6 right-6 text-[#6D6875] text-3xl font-bold bg-[#5DADEC]/10 hover:bg-[#5DADEC]/20 px-5 py-1 rounded-full focus:outline-none focus:ring-2 focus:ring-[#5DADEC] shadow-lg transition-all duration-300">×</button>
      <!-- Contenu dynamique -->
      <div id="fiche-contenu" class="mt-8 opacity-0 transform translate-y-4 transition-all duration-300 delay-100"></div>
    </div>
    
    <!-- Header & Navigation -->
    <header class="bg-white shadow-sm sticky top-0 z-30">
      <div class="container mx-auto px-4 py-4">
        <div class="flex justify-between items-center">
          <!-- Logo -->
          <a href="#accueil" class="text-creche-blue font-poppins font-semibold text-2xl">Les crèches de L'Asfad</a>
          
          <!-- Navigation desktop -->
          <nav class="hidden md:flex space-x-8 items-center">
            <a href="#accueil" class="text-creche-gray hover:text-creche-blue font-medium transition-colors px-1 py-2 border-b-2 border-transparent hover:border-creche-blue">Accueil</a>
            <a href="#creches" class="text-creche-gray hover:text-creche-blue font-medium transition-colors px-1 py-2 border-b-2 border-transparent hover:border-creche-blue">Crèches</a>
            <a href="#reserver" class="text-creche-gray hover:text-creche-blue font-medium transition-colors px-1 py-2 border-b-2 border-transparent hover:border-creche-blue">Réserver</a>
            <a href="#projets" class="text-creche-gray hover:text-creche-blue font-medium transition-colors px-1 py-2 border-b-2 border-transparent hover:border-creche-blue">Projets</a>
            <a href="#faq" class="text-creche-gray hover:text-creche-blue font-medium transition-colors px-1 py-2 border-b-2 border-transparent hover:border-creche-blue">FAQ</a>
          </nav>
          
          <!-- Bouton menu mobile -->
          <button id="mobile-menu-button" class="md:hidden p-2 rounded-lg bg-gray-100 hover:bg-gray-200 transition-colors">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="menu" class="lucide lucide-menu w-6 h-6 text-creche-gray"><path d="M4 12h16"></path><path d="M4 18h16"></path><path d="M4 6h16"></path></svg>
          </button>
        </div>
        
        <!-- Menu mobile -->
        <div id="mobile-menu" class="hidden md:hidden py-4 mt-2">
          <div class="flex flex-col space-y-3">
            <a href="#accueil" class="text-creche-gray hover:text-creche-blue font-medium px-2 py-1.5">Accueil</a>
            <a href="#creches" class="text-creche-gray hover:text-creche-blue font-medium px-2 py-1.5">Crèches</a>
            <a href="#reserver" class="text-creche-gray hover:text-creche-blue font-medium px-2 py-1.5">Réserver</a>
            <a href="#projets" class="text-creche-gray hover:text-creche-blue font-medium px-2 py-1.5">Projets</a>
            <a href="#faq" class="text-creche-gray hover:text-creche-blue font-medium px-2 py-1.5">FAQ</a>
          </div>
        </div>
      </div>
    </header>
    
    <!-- Hero Section -->
    <section id="accueil" class="relative py-20 md:py-28 bg-gradient-to-br from-[#f0f9ff] via-[#e6f7ff] to-[#f0f9ff] overflow-hidden">
      <div class="container mx-auto px-6 relative z-10">
        <div class="max-w-4xl mx-auto text-center fade-in appear">
          <h1 class="text-4xl md:text-5xl font-bold text-creche-blue font-poppins mb-6 tracking-tight">Les crèches de L'Asfad</h1>
          <p class="text-xl md:text-2xl text-creche-gray mb-8 leading-relaxed">
            Un environnement bienveillant où chaque enfant s'épanouit dans le respect, l'inclusion et la découverte.
          </p>
        </div>
      </div>
      
      <!-- Éléments décoratifs -->
      <div class="absolute top-1/4 left-[10%] w-24 h-24 bg-blue-200 rounded-full opacity-30 blur-lg"></div>
      <div class="absolute bottom-1/3 right-[5%] w-32 h-32 bg-creche-orange/20 rounded-full opacity-60 blur-lg"></div>
      <div class="absolute top-1/2 left-[15%] w-16 h-16 bg-creche-green/20 rounded-full opacity-50 blur-lg"></div>
      <div class="absolute top-1/3 right-[20%] w-20 h-20 bg-yellow-200/30 rounded-full opacity-40 blur-lg"></div>
    </section>
    
    <!-- Section avec 3 cartes mises en évidence -->
    <section class="py-12 md:py-20 px-4 fade-in bg-white appear">
      <!-- Les 3 tuiles principales avec coins arrondis et style moderne -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 md:gap-10 fade-in max-w-6xl mx-auto appear">
        
        <!-- Tuile 1: Découvrir nos crèches -->
        <a href="#creches" class="group relative bg-gradient-to-br from-[#e1eeff] to-[#c9e7ff] rounded-2xl shadow-lg overflow-hidden transform transition-all duration-300 hover:shadow-xl hover:scale-[1.02]">
          <div class="p-8 flex flex-col items-center justify-center h-full min-h-[300px]">
            <div class="w-16 h-16 bg-creche-blue/20 rounded-full flex items-center justify-center mb-6 group-hover:scale-110 transition-transform duration-300">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="search" class="lucide lucide-search w-8 h-8 text-creche-blue"><path d="m21 21-4.34-4.34"></path><circle cx="11" cy="11" r="8"></circle></svg>
            </div>
            <h2 class="font-poppins text-2xl font-bold text-creche-gray mb-3 group-hover:text-creche-blue transition-colors">Découvrez nos crèches</h2>
            <p class="text-center text-creche-gray/80">Explorez notre réseau de crèches innovantes et découvrez ce qui les rend uniques.</p>
          </div>
          <div class="absolute bottom-0 left-0 w-full h-1 bg-creche-blue transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-300"></div>
        </a>
        
        <!-- Tuile 2: Réserver une place -->
        <a href="#reserver" class="group relative bg-gradient-to-br from-[#e1f5e4] to-[#c9f0d0] rounded-2xl shadow-lg overflow-hidden transform transition-all duration-300 hover:shadow-xl hover:scale-[1.02]">
          <div class="p-8 flex flex-col items-center justify-center h-full min-h-[300px]">
            <div class="w-16 h-16 bg-creche-green/30 rounded-full flex items-center justify-center mb-6 group-hover:scale-110 transition-transform duration-300">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="calendar-plus" class="lucide lucide-calendar-plus w-8 h-8 text-creche-green"><path d="M16 19h6"></path><path d="M16 2v4"></path><path d="M19 16v6"></path><path d="M21 12.598V6a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h8.5"></path><path d="M3 10h18"></path><path d="M8 2v4"></path></svg>
            </div>
            <h2 class="font-poppins text-2xl font-bold text-creche-gray mb-3 group-hover:text-creche-green transition-colors">Réservez une place</h2>
            <p class="text-center text-creche-gray/80">Pour vos collaborateurs, simplifiez leur quotidien avec notre système de réservation.</p>
          </div>
          <div class="absolute bottom-0 left-0 w-full h-1 bg-creche-green transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-300"></div>
        </a>
        
        <!-- Tuile 3: Nos projets -->
        <a href="#projets" class="group relative bg-gradient-to-br from-[#fff4e1] to-[#ffe9c9] rounded-2xl shadow-lg overflow-hidden transform transition-all duration-300 hover:shadow-xl hover:scale-[1.02]">
          <div class="p-8 flex flex-col items-center justify-center h-full min-h-[300px]">
            <div class="w-16 h-16 bg-creche-orange/20 rounded-full flex items-center justify-center mb-6 group-hover:scale-110 transition-transform duration-300">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="rocket" class="lucide lucide-rocket w-8 h-8 text-creche-orange"><path d="M4.5 16.5c-1.5 1.26-2 5-2 5s3.74-.5 5-2c.71-.84.7-2.13-.09-2.91a2.18 2.18 0 0 0-2.91-.09z"></path><path d="m12 15-3-3a22 22 0 0 1 2-3.95A12.88 12.88 0 0 1 22 2c0 2.72-.78 7.5-6 11a22.35 22.35 0 0 1-4 2z"></path><path d="M9 12H4s.55-3.03 2-4c1.62-1.08 5 0 5 0"></path><path d="M12 15v5s3.03-.55 4-2c1.08-1.62 0-5 0-5"></path></svg>
            </div>
            <h2 class="font-poppins text-2xl font-bold text-creche-gray mb-3 group-hover:text-creche-orange transition-colors">Nos projets</h2>
            <p class="text-center text-creche-gray/80">Découvrez nos initiatives pédagogiques et nos démarches inclusives en cours de développement.</p>
          </div>
          <div class="absolute bottom-0 left-0 w-full h-1 bg-creche-orange transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-300"></div>
        </a>
        
      </div>
    </section>
    
    <!-- Nos Crèches Section -->
    <section id="creches" class="py-16 bg-gradient-to-b from-white to-blue-50/20 relative">
      <div class="container mx-auto px-4 fade-in appear">
        <!-- En-tête de section -->
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold text-creche-gray font-poppins mb-2">Découvrez nos crèches</h2>
        </div>

        <!-- Conteneur pour l'effet d'agrandissement - Sera rempli par JS -->
        <div id="creches-card-group" class="card-group flex flex-col md:flex-row gap-6 max-w-5xl mx-auto h-[400px] md:h-[400px]">
          <!-- Les cartes des crèches seront injectées ici par JavaScript -->
        </div>
      </div>
      
      <!-- Élément décoratif -->
      <div class="absolute -left-20 bottom-0 w-40 h-40 bg-blue-100 rounded-full opacity-50"></div>
    </section>
    
    <!-- Reservation Section -->
    <section id="reserver" class="pt-20 pb-24 fade-in bg-gradient-to-b from-blue-50 to-creche-cream/30 appear">
      <div class="max-w-7xl mx-auto px-6">
        <!-- En-tête de section -->
        <header class="text-center mb-12">
          <h2 class="text-3xl font-bold text-creche-blue font-poppins">Réservez une place</h2>
          <p class="text-creche-gray mt-2 text-lg">Simple, rapide et adapté aux besoins de votre entreprise</p>
        </header>
        
        <!-- Processus de réservation en 3 étapes simples -->
        <div class="flex flex-col md:flex-row gap-8 mb-10 text-center">
          <div class="flex-1 bg-white rounded-xl shadow-md p-6 border-b-4 border-creche-orange hover:shadow-lg transition-shadow">
            <div class="w-14 h-14 bg-creche-orange text-white text-xl font-bold rounded-full flex items-center justify-center mx-auto mb-4">1</div>
            <h3 class="text-xl font-bold text-creche-gray mb-2 font-poppins">Trouvez</h3>
            <p class="text-creche-gray">Localisez la crèche la plus proche de votre entreprise</p>
          </div>
          
          <div class="flex-1 bg-white rounded-xl shadow-md p-6 border-b-4 border-creche-blue hover:shadow-lg transition-shadow">
            <div class="w-14 h-14 bg-creche-blue text-white text-xl font-bold rounded-full flex items-center justify-center mx-auto mb-4">2</div>
            <h3 class="text-xl font-bold text-creche-gray mb-2 font-poppins">Sélectionnez</h3>
            <p class="text-creche-gray">Choisissez vos dates et le nombre de places souhaitées</p>
          </div>
          
          <div class="flex-1 bg-white rounded-xl shadow-md p-6 border-b-4 border-creche-green hover:shadow-lg transition-shadow">
            <div class="w-14 h-14 bg-creche-green text-white text-xl font-bold rounded-full flex items-center justify-center mx-auto mb-4">3</div>
            <h3 class="text-xl font-bold text-creche-gray mb-2 font-poppins">Demandez</h3>
            <p class="text-creche-gray">Envoyez votre demande de réservation en quelques clics</p>
          </div>
        </div>

        <!-- Contenu principal avec design amélioré - nouvelle structure 3/4 + 1/4 -->
        <div class="flex flex-col lg:flex-row gap-6">
          <!-- Arguments pour l'employeur (1/4) - colonne de gauche -->
          <div class="lg:w-1/4 bg-gradient-to-b from-creche-blue/10 to-creche-cream/20 rounded-xl p-6 overflow-hidden shadow-lg h-fit sticky top-32">
            <h3 class="font-poppins font-semibold text-creche-blue mb-4 text-xl">Pourquoi réserver des places pour vos collaborateurs ?</h3>
            
            <div class="space-y-4 max-h-[60vh] overflow-y-auto pr-2 custom-scrollbar">
              <div class="bg-white p-4 rounded-lg shadow-sm transform transition-all duration-300 hover:scale-105 hover:shadow-md">
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-10 h-10 bg-creche-blue/20 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="smile" class="lucide lucide-smile w-5 h-5 text-creche-blue"><circle cx="12" cy="12" r="10"></circle><path d="M8 14s1.5 2 4 2 4-2 4-2"></path><line x1="9" x2="9.01" y1="9" y2="9"></line><line x1="15" x2="15.01" y1="9" y2="9"></line></svg>
                  </div>
                  <h4 class="font-semibold text-creche-gray">Qualité de vie au travail</h4>
                </div>
                <p class="text-sm text-creche-gray/80">Améliorez l'équilibre vie professionnelle/vie personnelle de vos employés.</p>
              </div>
              
              <div class="bg-white p-4 rounded-lg shadow-sm transform transition-all duration-300 hover:scale-105 hover:shadow-md">
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-10 h-10 bg-creche-green/20 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="trending-up" class="lucide lucide-trending-up w-5 h-5 text-creche-green"><polyline points="22 7 13.5 15.5 8.5 10.5 2 17"></polyline><polyline points="16 7 22 7 22 13"></polyline></svg>
                  </div>
                  <h4 class="font-semibold text-creche-gray">Productivité accrue</h4>
                </div>
                <p class="text-sm text-creche-gray/80">Réduisez l'absentéisme et le stress lié à la garde des enfants.</p>
              </div>
              
              <div class="bg-white p-4 rounded-lg shadow-sm transform transition-all duration-300 hover:scale-105 hover:shadow-md">
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-10 h-10 bg-creche-orange/20 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="badge" class="lucide lucide-badge w-5 h-5 text-creche-orange"><path d="M3.85 8.62a4 4 0 0 1 4.78-4.77 4 4 0 0 1 6.74 0 4 4 0 0 1 4.78 4.78 4 4 0 0 1 0 6.74 4 4 0 0 1-4.77 4.78 4 4 0 0 1-6.75 0 4 4 0 0 1-4.78-4.77 4 4 0 0 1 0-6.76Z"></path></svg>
                  </div>
                  <h4 class="font-semibold text-creche-gray">Marque employeur</h4>
                </div>
                <p class="text-sm text-creche-gray/80">Renforcez votre image auprès des talents et candidats potentiels.</p>
              </div>
              
              <div class="bg-white p-4 rounded-lg shadow-sm transform transition-all duration-300 hover:scale-105 hover:shadow-md">
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-10 h-10 bg-purple-200 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="users" class="lucide lucide-users w-5 h-5 text-purple-500"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"></path><path d="M16 3.128a4 4 0 0 1 0 7.744"></path><path d="M22 21v-2a4 4 0 0 0-3-3.87"></path><circle cx="9" cy="7" r="4"></circle></svg>
                  </div>
                  <h4 class="font-semibold text-creche-gray">Fidélisation</h4>
                </div>
                <p class="text-sm text-creche-gray/80">Augmentez la rétention de vos meilleurs collaborateurs.</p>
              </div>
              
              <div class="bg-white p-4 rounded-lg shadow-sm transform transition-all duration-300 hover:scale-105 hover:shadow-md">
                <div class="flex items-center gap-3 mb-2">
                  <div class="w-10 h-10 bg-pink-200 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="heart-handshake" class="lucide lucide-heart-handshake w-5 h-5 text-pink-500"><path d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"></path><path d="M12 5 9.04 7.96a2.17 2.17 0 0 0 0 3.08c.82.82 2.13.85 3 .07l2.07-1.9a2.82 2.82 0 0 1 3.79 0l2.96 2.66"></path><path d="m18 15-2-2"></path><path d="m15 18-2-2"></path></svg>
                  </div>
                  <h4 class="font-semibold text-creche-gray">Impact social</h4>
                </div>
                <p class="text-sm text-creche-gray/80">Contribuez à la politique familiale et à l'égalité professionnelle.</p>
              </div>
            </div>
          </div>
          
          <!-- Zone de réservation (3/4) -->
          <div class="lg:w-3/4 bg-white rounded-xl shadow-xl overflow-hidden">
          <!-- Barre d'étape (breadcrumb) -->
          <div class="flex border-b border-gray-200">
            <div id="etape-1" class="flex-1 py-4 text-center relative group cursor-pointer">
              <div class="flex items-center justify-center">
                <div class="w-8 h-8 bg-creche-orange text-white rounded-full flex items-center justify-center font-bold">1</div>
                <span class="ml-2 font-poppins font-semibold text-creche-orange">Localisation</span>
              </div>
              <div class="absolute bottom-0 left-0 w-full h-0.5 bg-creche-orange"></div>
            </div>
            
            <div id="etape-2" class="flex-1 py-4 text-center relative group cursor-pointer opacity-70">
              <div class="flex items-center justify-center">
                <div class="w-8 h-8 bg-gray-300 text-white rounded-full flex items-center justify-center font-bold">2</div>
                <span class="ml-2 font-poppins font-semibold text-creche-gray">Disponibilités</span>
              </div>
            </div>
            
            <div id="etape-3" class="flex-1 py-4 text-center relative group cursor-pointer opacity-70">
              <div class="flex items-center justify-center">
                <div class="w-8 h-8 bg-gray-300 text-white rounded-full flex items-center justify-center font-bold">3</div>
                <span class="ml-2 font-poppins font-semibold text-creche-gray">Demande</span>
              </div>
            </div>
          </div>
          
          
          <!-- Conteneur pour toutes les étapes -->
          <div id="etapes-container" class="p-6">
            <!-- ÉTAPE 1 : Localisation -->
            <div id="contenu-etape-1" class="etape-contenu">
              <!-- Champ adresse + bouton -->
              <div class="mb-8">
                <label for="adresse" class="block font-semibold text-lg mb-2 font-poppins text-creche-gray">Entrez l'adresse de votre entreprise</label>
                <div class="flex flex-col md:flex-row gap-4">
                  <input id="adresse" type="text" placeholder="Ex : 10 rue de Nantes, 35000 Rennes" class="flex-1 border-2 border-creche-blue/30 rounded-lg px-4 py-3">
                  <button id="rechercher-creche" class="bg-creche-blue hover:bg-creche-blue/80 text-white font-bold px-6 py-3 rounded-lg transition-colors duration-300">
                    <span class="flex items-center justify-center gap-2">
                      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="search" class="lucide lucide-search h-5 w-5"><path d="m21 21-4.34-4.34"></path><circle cx="11" cy="11" r="8"></circle></svg>
                      Trouver ma crèche
                    </span>
                  </button>
                </div>
              </div>
              
              <!-- Mapbox (ajout) -->
              <div class="relative mb-4">
                <div id="map" class="w-full h-[400px] rounded-xl overflow-hidden shadow-md leaflet-container leaflet-touch leaflet-retina leaflet-fade-anim leaflet-grab leaflet-touch-drag leaflet-touch-zoom" tabindex="0" style="position: relative;"><div class="leaflet-pane leaflet-map-pane" style="transform: translate3d(4px, 0px, 0px);"><div class="leaflet-pane leaflet-tile-pane"><div class="leaflet-layer " style="z-index: 1; opacity: 1;"><div class="leaflet-tile-container leaflet-zoom-animated" style="z-index: 16; transform: translate3d(-15px, -415px, 0px) scale(4);"></div><div class="leaflet-tile-container leaflet-zoom-animated" style="z-index: 18; transform: translate3d(0px, 0px, 0px) scale(1);"><img alt="" src="https://b.tile.openstreetmap.org/15/16225/11373.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(89px, -39px, 0px); opacity: 1;"><img alt="" src="https://c.tile.openstreetmap.org/15/16226/11373.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(345px, -39px, 0px); opacity: 1;"><img alt="" src="https://c.tile.openstreetmap.org/15/16225/11374.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(89px, 217px, 0px); opacity: 1;"><img alt="" src="https://a.tile.openstreetmap.org/15/16226/11374.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(345px, 217px, 0px); opacity: 1;"><img alt="" src="https://a.tile.openstreetmap.org/15/16224/11373.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(-167px, -39px, 0px); opacity: 1;"><img alt="" src="https://a.tile.openstreetmap.org/15/16227/11373.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(601px, -39px, 0px); opacity: 1;"><img alt="" src="https://b.tile.openstreetmap.org/15/16224/11374.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(-167px, 217px, 0px); opacity: 1;"><img alt="" src="https://b.tile.openstreetmap.org/15/16227/11374.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(601px, 217px, 0px); opacity: 1;"><img alt="" src="https://b.tile.openstreetmap.org/15/16228/11373.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(857px, -39px, 0px); opacity: 1;"><img alt="" src="https://c.tile.openstreetmap.org/15/16228/11374.png" class="leaflet-tile leaflet-tile-loaded" style="width: 256px; height: 256px; transform: translate3d(857px, 217px, 0px); opacity: 1;"></div></div></div><div class="leaflet-pane leaflet-overlay-pane"></div><div class="leaflet-pane leaflet-shadow-pane"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-shadow.png" class="leaflet-marker-shadow leaflet-zoom-animated" alt="" style="margin-left: -12px; margin-top: -41px; width: 41px; height: 41px; transform: translate3d(1698px, 386px, 0px);"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-shadow.png" class="leaflet-marker-shadow leaflet-zoom-animated" alt="" style="margin-left: -12px; margin-top: -41px; width: 41px; height: 41px; transform: translate3d(1444px, 81px, 0px);"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-shadow.png" class="leaflet-marker-shadow leaflet-zoom-animated" alt="" style="margin-left: -12px; margin-top: -41px; width: 41px; height: 41px; transform: translate3d(2114px, 662px, 0px);"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-shadow.png" class="leaflet-marker-shadow leaflet-zoom-animated" alt="" style="margin-left: -12px; margin-top: -41px; width: 41px; height: 41px; transform: translate3d(1783px, 858px, 0px);"></div><div class="leaflet-pane leaflet-marker-pane"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon-2x.png" class="leaflet-marker-icon leaflet-zoom-animated leaflet-interactive" alt="Marker" tabindex="0" role="button" style="margin-left: -12px; margin-top: -41px; width: 25px; height: 41px; transform: translate3d(1698px, 386px, 0px); z-index: 386;"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon-2x.png" class="leaflet-marker-icon leaflet-zoom-animated leaflet-interactive" alt="Marker" tabindex="0" role="button" style="margin-left: -12px; margin-top: -41px; width: 25px; height: 41px; transform: translate3d(1444px, 81px, 0px); z-index: 81;"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon-2x.png" class="leaflet-marker-icon leaflet-zoom-animated leaflet-interactive" alt="Marker" tabindex="0" role="button" style="margin-left: -12px; margin-top: -41px; width: 25px; height: 41px; transform: translate3d(2114px, 662px, 0px); z-index: 662;"><img src="https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon-2x.png" class="leaflet-marker-icon leaflet-zoom-animated leaflet-interactive" alt="Marker" tabindex="0" role="button" style="margin-left: -12px; margin-top: -41px; width: 25px; height: 41px; transform: translate3d(1783px, 858px, 0px); z-index: 858;"></div><div class="leaflet-pane leaflet-tooltip-pane"></div><div class="leaflet-pane leaflet-popup-pane"></div><div class="leaflet-proxy leaflet-zoom-animated" style="transform: translate3d(4.15394e+06px, 2.91173e+06px, 0px) scale(16384);"></div></div><div class="leaflet-control-container"><div class="leaflet-top leaflet-left"><div class="leaflet-control-zoom leaflet-bar leaflet-control"><a class="leaflet-control-zoom-in" href="#" title="Zoom in" role="button" aria-label="Zoom in" aria-disabled="false"><span aria-hidden="true">+</span></a><a class="leaflet-control-zoom-out" href="#" title="Zoom out" role="button" aria-label="Zoom out" aria-disabled="false"><span aria-hidden="true">−</span></a></div></div><div class="leaflet-top leaflet-right"></div><div class="leaflet-bottom leaflet-left"></div><div class="leaflet-bottom leaflet-right"><div class="leaflet-control-attribution leaflet-control"><a href="https://leafletjs.com" title="A JavaScript library for interactive maps"><svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="12" height="8" viewBox="0 0 12 8" class="leaflet-attribution-flag"><path fill="#4C7BE1" d="M0 0h12v4H0z"></path><path fill="#FFD500" d="M0 4h12v3H0z"></path><path fill="#E0BC00" d="M0 7h12v1H0z"></path></svg> Leaflet</a> <span aria-hidden="true">|</span> © OpenStreetMap contributors</div></div></div></div>
                <div id="resultat-recherche" class="absolute bottom-4 left-4 right-4 bg-white/90 backdrop-blur-sm p-3 rounded-lg shadow-lg hidden">
                  <p class="font-medium">Recherche en cours...</p>
                </div>
              </div>
              
              <!-- Crèches trouvées -->
              <div id="liste-creches" class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-8 hidden">
                <h3 class="text-lg font-semibold col-span-full mb-2">Crèches à proximité :</h3>
                
                <!-- Carte crèche exemple 1 -->
                <div class="bg-white rounded-lg overflow-hidden shadow-md flex hover:shadow-lg transition-shadow cursor-pointer border border-gray-100">
                  <div class="w-1/3 bg-blue-200 flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="building-2" class="lucide lucide-building-2 text-white w-12 h-12"><path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z"></path><path d="M6 12H4a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2h2"></path><path d="M18 9h2a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2h-2"></path><path d="M10 6h4"></path><path d="M10 10h4"></path><path d="M10 14h4"></path><path d="M10 18h4"></path></svg>
                  </div>
                  <div class="p-2">
                    <h3 class="font-bold text-lg">Les Petits Merlins</h3>
                    <p>Rennes Centre - 45 places</p>
                    <p><strong>Distance:</strong> 0.28 km</p>
                    <a id="voir-disponibilites-1" href="#" class="text-blue-500 hover:underline">Voir les disponibilités</a>
                  </div>
                </div>
                
                <!-- Carte crèche exemple 2 -->
                <div class="bg-white rounded-lg overflow-hidden shadow-md flex hover:shadow-lg transition-shadow cursor-pointer border border-gray-100">
                  <div class="w-1/3 bg-green-200 flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="building-2" class="lucide lucide-building-2 text-white w-12 h-12"><path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z"></path><path d="M6 12H4a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2h2"></path><path d="M18 9h2a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2h-2"></path><path d="M10 6h4"></path><path d="M10 10h4"></path><path d="M10 14h4"></path><path d="M10 18h4"></path></svg>
                  </div>
                  <div class="p-2">
                    <h3 class="font-bold text-lg">Joséphine Baker</h3>
                    <p>Rennes Nord - 30 places</p>
                    <p><strong>Distance:</strong> 1.5 km</p>
                    <a id="voir-disponibilites-2" href="#" class="text-blue-500 hover:underline">Voir les disponibilités</a>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- ÉTAPE 2 : Disponibilités (masquée par défaut) -->
            <div id="contenu-etape-2" class="etape-contenu hidden">
              <div class="flex items-center mb-6">
                <button id="retour-etape-1" class="mr-4 text-creche-blue hover:text-creche-blue/80">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-left" class="lucide lucide-arrow-left w-5 h-5"><path d="m12 19-7-7 7-7"></path><path d="M19 12H5"></path></svg>
                </button>
                <h3 class="text-xl font-semibold">Choisissez vos disponibilités</h3>
              </div>
              
              <!-- Détails crèche sélectionnée -->
              <div class="flex flex-col md:flex-row gap-6 mb-8 bg-blue-50/50 p-4 rounded-xl">
                <div class="md:w-1/4 flex justify-center">
                  <div class="w-32 h-32 bg-blue-200 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="building-2" class="lucide lucide-building-2 text-white w-16 h-16"><path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z"></path><path d="M6 12H4a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2h2"></path><path d="M18 9h2a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2h-2"></path><path d="M10 6h4"></path><path d="M10 10h4"></path><path d="M10 14h4"></path><path d="M10 18h4"></path></svg>
                  </div>
                </div>
                <div class="md:w-3/4">
                  <h3 class="text-xl font-bold mb-2 text-creche-gray">Les Petits Merlins</h3>
                  <p class="mb-1">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="map-pin" class="lucide lucide-map-pin inline w-4 h-4 mr-1 text-creche-orange"><path d="M20 10c0 4.993-5.539 10.193-7.399 11.799a1 1 0 0 1-1.202 0C9.539 20.193 4 14.993 4 10a8 8 0 0 1 16 0"></path><circle cx="12" cy="10" r="3"></circle></svg>
                    <span>10 rue des Lilas, 35000 Rennes</span>
                  </p>
                  <p class="mb-1">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="clock" class="lucide lucide-clock inline w-4 h-4 mr-1 text-creche-blue"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
                    <span>Lun-Ven: 7h30 - 19h00</span>
                  </p>
                  <p class="mb-1">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="users" class="lucide lucide-users inline w-4 h-4 mr-1 text-creche-green"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"></path><path d="M16 3.128a4 4 0 0 1 0 7.744"></path><path d="M22 21v-2a4 4 0 0 0-3-3.87"></path><circle cx="9" cy="7" r="4"></circle></svg>
                    <span>Capacité: 45 places (8 disponibles)</span>
                  </p>
                  <div class="mt-2 flex gap-2 flex-wrap">
                    <span class="bg-blue-100 px-2 py-1 rounded-full text-xs text-blue-700">Espace vert</span>
                    <span class="bg-green-100 px-2 py-1 rounded-full text-xs text-green-700">Bio</span>
                    <span class="bg-purple-100 px-2 py-1 rounded-full text-xs text-purple-700">Éveil musical</span>
                  </div>
                </div>
              </div>
              
              <!-- Calendrier des disponibilités -->
              <div class="mb-8">
                <h4 class="font-poppins font-semibold text-creche-gray text-lg mb-4">Périodes disponibles</h4>
                <div class="flex flex-wrap gap-6 justify-center">
                  <div class="w-32 h-32 bg-creche-green/20 rounded-full flex flex-col justify-center items-center text-center font-semibold shadow-md hover:scale-110 transition-transform cursor-pointer date-selectable">
                    <span class="text-creche-blue text-sm">Trimestre 1</span>
                    <span class="text-lg font-bold text-creche-gray">Jan-Mar</span>
                    <span class="text-creche-green font-bold">2025</span>
                    <span class="text-xs mt-1 text-creche-gray">8 places</span>
                  </div>
                  
                  <div class="w-32 h-32 bg-creche-green/20 rounded-full flex flex-col justify-center items-center text-center font-semibold shadow-md hover:scale-110 transition-transform cursor-pointer date-selectable">
                    <span class="text-creche-blue text-sm">Trimestre 2</span>
                    <span class="text-lg font-bold text-creche-gray">Avr-Juin</span>
                    <span class="text-creche-green font-bold">2025</span>
                    <span class="text-xs mt-1 text-creche-gray">5 places</span>
                  </div>
                  
                  <div class="w-32 h-32 bg-creche-green/20 rounded-full flex flex-col justify-center items-center text-center font-semibold shadow-md hover:scale-110 transition-transform cursor-pointer date-selectable">
                    <span class="text-creche-blue text-sm">Trimestre 3</span>
                    <span class="text-lg font-bold text-creche-gray">Juil-Sept</span>
                    <span class="text-creche-green font-bold">2025</span>
                    <span class="text-xs mt-1 text-creche-gray">3 places</span>
                  </div>
                  
                  <div class="w-32 h-32 bg-creche-orange/10 rounded-full flex flex-col justify-center items-center text-center font-semibold shadow-md opacity-75">
                    <span class="text-creche-blue text-sm">Trimestre 4</span>
                    <span class="text-lg font-bold text-creche-gray">Oct-Déc</span>
                    <span class="text-creche-orange/80 font-bold">2025</span>
                    <span class="text-xs mt-1 text-creche-gray">Complet</span>
                  </div>
                  
                  <div class="w-32 h-32 bg-creche-blue/20 rounded-full flex flex-col justify-center items-center text-center font-semibold shadow-md hover:scale-110 transition-transform cursor-pointer date-selectable">
                    <span class="text-creche-blue text-sm">Année</span>
                    <span class="text-lg font-bold text-creche-gray">Complète</span>
                    <span class="text-creche-blue font-bold">2025</span>
                    <span class="text-xs mt-1 text-creche-gray">2 places</span>
                  </div>
                </div>
              </div>
              
              <!-- Bouton pour afficher formulaire -->
              <div class="text-center">
                <button id="bouton-demande" class="bg-creche-blue hover:bg-creche-blue/80 text-white font-bold py-4 px-8 rounded-lg text-lg shadow-md font-poppins transition-all duration-300 transform hover:scale-105">
                  Faire une demande
                </button>
              </div>
            </div>
            
            <!-- ÉTAPE 3 : Formulaire de demande (masquée par défaut) -->
            <div id="contenu-etape-3" class="etape-contenu hidden">
              <div class="flex items-center mb-6">
                <button id="retour-etape-2" class="mr-4 text-creche-blue hover:text-creche-blue/80">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="arrow-left" class="lucide lucide-arrow-left w-5 h-5"><path d="m12 19-7-7 7-7"></path><path d="M19 12H5"></path></svg>
                </button>
                <h3 class="text-xl font-semibold">Finalisez votre demande</h3>
              </div>
              
              <!-- Récapitulatif -->
              <div class="bg-blue-50/50 p-4 rounded-xl mb-6">
                <h4 class="font-semibold mb-2">Récapitulatif de votre demande</h4>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <div>
                    <p class="text-sm text-creche-gray">Crèche sélectionnée:</p>
                    <p class="font-semibold">Les Petits Merlins</p>
                  </div>
                  <div>
                    <p class="text-sm text-creche-gray">Période:</p>
                    <p class="font-semibold">Trimestre 1 (Jan-Mar 2025)</p>
                  </div>
                  <div>
                    <p class="text-sm text-creche-gray">Places disponibles:</p>
                    <p class="font-semibold">8 places</p>
                  </div>
                </div>
              </div>
              
              <!-- Formulaire -->
              <form id="formulaire-reservation" class="space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <!-- Informations entreprise -->
                  <div class="space-y-4">
                    <h4 class="font-semibold text-creche-blue">Informations de l'entreprise</h4>
                    
                    <div>
                      <label for="entreprise-nom" class="block text-sm font-medium mb-1">Nom de l'entreprise *</label>
                      <input type="text" id="entreprise-nom" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                    
                    <div>
                      <label for="entreprise-adresse" class="block text-sm font-medium mb-1">Adresse *</label>
                      <input type="text" id="entreprise-adresse" class="w-full border-2 border-gray-200 rounded-lg p-2" value="10 rue de Nantes, 35000 Rennes" required="">
                    </div>
                    
                    <div>
                      <label for="entreprise-siret" class="block text-sm font-medium mb-1">Numéro SIRET *</label>
                      <input type="text" id="entreprise-siret" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                    
                    <div>
                      <label for="nb-salaries" class="block text-sm font-medium mb-1">Nombre de salariés</label>
                      <input type="number" id="nb-salaries" class="w-full border-2 border-gray-200 rounded-lg p-2">
                    </div>
                  </div>
                  
                  <!-- Informations contact -->
                  <div class="space-y-4">
                    <h4 class="font-semibold text-creche-blue">Informations du contact</h4>
                    
                    <div>
                      <label for="contact-nom" class="block text-sm font-medium mb-1">Nom complet *</label>
                      <input type="text" id="contact-nom" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                    
                    <div>
                      <label for="contact-fonction" class="block text-sm font-medium mb-1">Fonction *</label>
                      <input type="text" id="contact-fonction" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                    
                    <div>
                      <label for="contact-email" class="block text-sm font-medium mb-1">Email professionnel *</label>
                      <input type="email" id="contact-email" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                    
                    <div>
                      <label for="contact-telephone" class="block text-sm font-medium mb-1">Téléphone *</label>
                      <input type="tel" id="contact-telephone" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                    </div>
                  </div>
                </div>
                
                <!-- Détails demande -->
                <div class="space-y-4">
                  <h4 class="font-semibold text-creche-blue">Détails de la réservation</h4>
                  
                  <div>
                    <label for="nb-places" class="block text-sm font-medium mb-1">Nombre de places souhaitées *</label>
                    <select id="nb-places" class="w-full border-2 border-gray-200 rounded-lg p-2" required="">
                      <option value="1">1 place</option>
                      <option value="2">2 places</option>
                      <option value="3">3 places</option>
                      <option value="4">4 places</option>
                      <option value="5">5 places</option>
                    </select>
                  </div>
                  
                  <div>
                    <label for="commentaire" class="block text-sm font-medium mb-1">Commentaires ou précisions</label>
                    <textarea id="commentaire" rows="3" class="w-full border-2 border-gray-200 rounded-lg p-2"></textarea>
                  </div>
                  
                  <div class="flex items-start">
                    <input type="checkbox" id="accepter-conditions" class="mt-1 mr-2" required="">
                    <label for="accepter-conditions" class="text-sm">J'accepte les <a href="#" class="text-creche-blue hover:underline">conditions d'utilisation</a> et la <a href="#" class="text-creche-blue hover:underline">politique de confidentialité</a> *</label>
                  </div>
                </div>
                
                <!-- Bouton envoyer -->
                <div class="text-center pt-4">
                  <button type="submit" class="bg-creche-blue hover:bg-creche-blue/80 text-white font-bold py-4 px-8 rounded-lg text-lg shadow-md font-poppins transition-all duration-300 transform hover:scale-105">
                    Envoyer ma demande
                  </button>
                </div>
              </form>
            </div>
            
            <!-- Message de confirmation (masqué par défaut) -->
            <div id="confirmation-reservation" class="hidden text-center py-10">
              <div class="inline-block p-4 bg-green-100 rounded-full mb-6">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="check-circle" class="lucide lucide-check-circle w-16 h-16 text-green-500"><path d="M21.801 10A10 10 0 1 1 17 3.335"></path><path d="m9 11 3 3L22 4"></path></svg>
              </div>
              <h3 class="text-2xl font-bold mb-2 text-creche-gray">Demande envoyée avec succès !</h3>
              <p class="text-creche-gray mb-6 max-w-xl mx-auto">Nous avons bien reçu votre demande de réservation. Notre équipe va l'examiner et vous contactera dans les plus brefs délais.</p>
              <p class="text-creche-gray font-semibold">Référence de votre demande: <span class="text-creche-blue">RES-25062</span></p>
              <div class="mt-8">
                <button id="nouvelle-recherche" class="bg-creche-green hover:bg-creche-green/80 text-white font-bold py-3 px-6 rounded-lg shadow-md font-poppins transition-all duration-300">
                  Faire une nouvelle recherche
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Éléments décoratifs -->
      <div class="absolute -left-20 bottom-0 w-40 h-40 bg-green-100 rounded-full opacity-50"></div>
    </div></section>
    
    <!-- Projets Section -->
    <section id="projets" class="py-24 bg-gradient-to-t from-blue-50 to-creche-cream/30 fade-in appear relative">
      <div class="max-w-7xl mx-auto px-6">
        <!-- En-tête de section -->
        <header class="text-center mb-8">
          <h2 class="text-3xl font-bold text-creche-gray font-poppins">Nos Projets</h2>
          <p class="text-creche-gray mt-2">Des projets concrets pour innover dans la petite enfance</p>
        </header>
        
        <!-- Carrousel horizontal - Sera rempli par JS -->
        <div class="relative max-w-6xl mx-auto">
          <div class="flex justify-center gap-12 lg:gap-24 mt-8 overflow-x-auto pb-4" id="projets-carousel">
            <!-- Les bulles de projets seront injectées ici par JavaScript -->
          </div>
          
          <!-- Navigation buttons -->
          <button id="prev-slide" class="absolute left-0 top-1/2 -translate-y-1/2 bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md hover:bg-gray-50">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-left" class="lucide lucide-chevron-left w-6 h-6 text-creche-gray"><path d="m15 18-6-6 6-6"></path></svg>
          </button>
          
          <button id="next-slide" class="absolute right-0 top-1/2 -translate-y-1/2 bg-white rounded-full w-10 h-10 flex items-center justify-center shadow-md hover:bg-gray-50">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-right" class="lucide lucide-chevron-right w-6 h-6 text-creche-gray"><path d="m9 18 6-6-6-6"></path></svg>
          </button>
        </div>
        
        <p class="text-center text-creche-gray/70 text-sm mt-8">Survolez les bulles pour découvrir les détails de chaque projet</p>
      </div>
      
      <!-- Éléments décoratifs -->
      <div class="absolute -left-20 top-20 w-40 h-40 bg-green-100 rounded-full opacity-50"></div>
      <div class="absolute right-0 bottom-10 w-64 h-64 bg-yellow-100 rounded-full opacity-40"></div>
    </section>
    
    <!-- FAQ Section -->
    <section id="faq" class="py-16 bg-white fade-in appear">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold text-creche-gray font-poppins">Vos questions fréquentes</h2>
          <p class="text-creche-gray mt-2">Tout ce que vous devez savoir sur nos crèches et nos services</p>
        </div>
        
        <!-- Questions -->
        <div class="max-w-3xl mx-auto space-y-4">
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <button class="faq-question w-full text-left px-6 py-4 flex justify-between items-center focus:outline-none">
              <span class="font-poppins font-medium">Comment fonctionne la réservation de berceaux par une entreprise ?</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-down" class="lucide lucide-chevron-down w-5 h-5 text-creche-blue"><path d="m6 9 6 6 6-6"></path></svg>
            </button>
            <div class="faq-answer px-6 pb-4 hidden">
              <p class="text-creche-gray">
                Notre service permet aux entreprises de réserver des places pour les enfants de leurs employés dans nos crèches partenaires. Après votre demande, nous vous proposons un rendez-vous pour discuter de vos besoins spécifiques et vous présenter les différentes options adaptées à votre organisation.
              </p>
            </div>
          </div>
          
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <button class="faq-question w-full text-left px-6 py-4 flex justify-between items-center focus:outline-none">
              <span class="font-poppins font-medium">Quels sont les horaires d'ouverture des crèches ?</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-down" class="lucide lucide-chevron-down w-5 h-5 text-creche-blue"><path d="m6 9 6 6 6-6"></path></svg>
            </button>
            <div class="faq-answer px-6 pb-4 hidden">
              <p class="text-creche-gray">
                Nos crèches sont généralement ouvertes du lundi au vendredi de 7h30 à 19h00. Certains établissements proposent des horaires étendus pour s'adapter aux contraintes professionnelles des parents. Les horaires précis sont indiqués sur la page de chaque crèche.
              </p>
            </div>
          </div>
          
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <button class="faq-question w-full text-left px-6 py-4 flex justify-between items-center focus:outline-none">
              <span class="font-poppins font-medium">Quel est le coût pour l'entreprise ?</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-down" class="lucide lucide-chevron-down w-5 h-5 text-creche-blue"><path d="m6 9 6 6 6-6"></path></svg>
            </button>
            <div class="faq-answer px-6 pb-4 hidden">
              <p class="text-creche-gray">
                Le coût varie en fonction du nombre de places réservées, de la durée de l'engagement et de la localisation de la crèche. Les entreprises bénéficient d'avantages fiscaux qui réduisent considérablement le coût réel. Contactez-nous pour obtenir un devis personnalisé adapté à votre situation.
              </p>
            </div>
          </div>
          
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <button class="faq-question w-full text-left px-6 py-4 flex justify-between items-center focus:outline-none active">
              <span class="font-poppins font-medium">Est-il possible de visiter les crèches avant de réserver ?</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-down" class="lucide lucide-chevron-down w-5 h-5 text-creche-blue"><path d="m6 9 6 6 6-6"></path></svg>
            </button>
            <div class="faq-answer px-6 pb-4">
              <p class="text-creche-gray">
                Bien sûr ! Nous encourageons les visites préalables. Vous pouvez contacter directement la crèche qui vous intéresse ou remplir notre formulaire en ligne. Notre équipe organisera une visite avec la direction de l'établissement pour vous présenter les lieux, l'équipe et notre projet pédagogique.
              </p>
            </div>
          </div>
          
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <button class="faq-question w-full text-left px-6 py-4 flex justify-between items-center focus:outline-none">
              <span class="font-poppins font-medium">Quelles sont les approches pédagogiques dans vos crèches ?</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="chevron-down" class="lucide lucide-chevron-down w-5 h-5 text-creche-blue"><path d="m6 9 6 6 6-6"></path></svg>
            </button>
            <div class="faq-answer px-6 pb-4 hidden">
              <p class="text-creche-gray">
                Nos crèches s'inspirent de différentes approches pédagogiques reconnues (Montessori, Loczy, Pikler...) tout en développant leur propre projet éducatif. Nous mettons l'accent sur le respect du rythme de l'enfant, l'éveil sensoriel, la motricité libre et la socialisation. Chaque crèche a sa spécificité pédagogique détaillée dans sa présentation.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-10 mt-auto">
      <div class="container mx-auto px-4">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-10">
          <!-- Coordonnées -->
          <div>
            <h3 class="text-lg font-semibold mb-4 font-poppins">Coordonnées</h3>
            <p class="mb-1">Association Pôle Petite Enfance</p>
            <p class="mb-1">12 quater avenue de Pologne</p>
            <p class="mb-3">35200 Rennes</p>
            <p class="flex items-center gap-2 mb-1">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="phone" class="lucide lucide-phone w-4 h-4 text-creche-blue"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
              <span>02 99 XX XX XX</span>
            </p>
            <p class="flex items-center gap-2">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="mail" class="lucide lucide-mail w-4 h-4 text-creche-blue"><path d="m22 7-8.991 5.727a2 2 0 0 1-2.009 0L2 7"></path><rect x="2" y="4" width="20" height="16" rx="2"></rect></svg>
              <span>contact@petite-enfance.bzh</span>
            </p>
          </div>
          
          <!-- Liens utiles -->
          <div>
            <h3 class="text-lg font-semibold mb-4 font-poppins">Liens utiles</h3>
            <ul class="space-y-2">
              <li><a href="#" class="hover:text-creche-blue transition-colors flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="home" class="lucide lucide-home w-4 h-4"><path d="M15 21v-8a1 1 0 0 0-1-1h-4a1 1 0 0 0-1 1v8"></path><path d="M3 10a2 2 0 0 1 .709-1.528l7-5.999a2 2 0 0 1 2.582 0l7 5.999A2 2 0 0 1 21 10v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path></svg> Accueil</a></li>
              <li><a href="#creches" class="hover:text-creche-blue transition-colors flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="building" class="lucide lucide-building w-4 h-4"><rect width="16" height="20" x="4" y="2" rx="2" ry="2"></rect><path d="M9 22v-4h6v4"></path><path d="M8 6h.01"></path><path d="M16 6h.01"></path><path d="M12 6h.01"></path><path d="M12 10h.01"></path><path d="M12 14h.01"></path><path d="M16 10h.01"></path><path d="M16 14h.01"></path><path d="M8 10h.01"></path><path d="M8 14h.01"></path></svg> Nos crèches</a></li>
              <li><a href="#reserver" class="hover:text-creche-blue transition-colors flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="calendar" class="lucide lucide-calendar w-4 h-4"><path d="M8 2v4"></path><path d="M16 2v4"></path><rect width="18" height="18" x="3" y="4" rx="2"></rect><path d="M3 10h18"></path></svg> Réserver une place</a></li>
              <li><a href="#projets" class="hover:text-creche-blue transition-colors flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="rocket" class="lucide lucide-rocket w-4 h-4"><path d="M4.5 16.5c-1.5 1.26-2 5-2 5s3.74-.5 5-2c.71-.84.7-2.13-.09-2.91a2.18 2.18 0 0 0-2.91-.09z"></path><path d="m12 15-3-3a22 22 0 0 1 2-3.95A12.88 12.88 0 0 1 22 2c0 2.72-.78 7.5-6 11a22.35 22.35 0 0 1-4 2z"></path><path d="M9 12H4s.55-3.03 2-4c1.62-1.08 5 0 5 0"></path><path d="M12 15v5s3.03-.55 4-2c1.08-1.62 0-5 0-5"></path></svg> Projets</a></li>
              <li><a href="#faq" class="hover:text-creche-blue transition-colors flex items-center gap-1"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="help-circle" class="lucide lucide-help-circle w-4 h-4"><circle cx="12" cy="12" r="10"></circle><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"></path><path d="M12 17h.01"></path></svg> FAQ</a></li>
            </ul>
          </div>
          
          <!-- Suivez-nous -->
          <div>
            <h3 class="text-lg font-semibold mb-4 font-poppins">Suivez-nous</h3>
            <div class="flex gap-4 mb-6">
              <a href="#" class="bg-blue-500 hover:bg-blue-600 transition-colors w-8 h-8 rounded-full flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="facebook" class="lucide lucide-facebook w-4 h-4"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></svg>
              </a>
              <a href="#" class="bg-blue-400 hover:bg-blue-500 transition-colors w-8 h-8 rounded-full flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="twitter" class="lucide lucide-twitter w-4 h-4"><path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-18 11.6 2.2.1 4.4-.6 6-2C3 15.5.5 9.6 3 5c2.2 2.6 5.6 4.1 9 4-.9-4.2 4-6.6 7-3.8 1.1 0 3-1.2 3-1.2z"></path></svg>
              </a>
              <a href="#" class="bg-pink-600 hover:bg-pink-700 transition-colors w-8 h-8 rounded-full flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="instagram" class="lucide lucide-instagram w-4 h-4"><rect width="20" height="20" x="2" y="2" rx="5" ry="5"></rect><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path><line x1="17.5" x2="17.51" y1="6.5" y2="6.5"></line></svg>
              </a>
              <a href="#" class="bg-red-600 hover:bg-red-700 transition-colors w-8 h-8 rounded-full flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" data-lucide="youtube" class="lucide lucide-youtube w-4 h-4"><path d="M2.5 17a24.12 24.12 0 0 1 0-10 2 2 0 0 1 1.4-1.4 49.56 49.56 0 0 1 16.2 0A2 2 0 0 1 21.5 7a24.12 24.12 0 0 1 0 10 2 2 0 0 1-1.4 1.4 49.55 49.55 0 0 1-16.2 0A2 2 0 0 1 2.5 17"></path><path d="m10 15 5-3-5-3z"></path></svg>
              </a>
            </div>
            <p class="text-sm text-gray-400">Site démonstratif - Projet étudiant</p>
            <button id="admin-button" class="mt-4 bg-creche-blue hover:bg-creche-blue/80 text-white font-semibold py-2 px-4 rounded-lg text-sm">Administration</button>
          </div>
        </div>
        
        <div class="mt-10 pt-6 border-t border-gray-800 text-center text-sm text-gray-500">
          © 2025 Pôle Petite Enfance. Tous droits réservés.
        </div>
      </div>
    </footer>

    <!-- Panneau d'administration (initialement masqué) -->
    <section id="admin-section" class="hidden fixed inset-0 bg-gray-100 z-[100] p-8 overflow-y-auto">
      <div class="container mx-auto bg-white p-6 rounded-lg shadow-xl">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-2xl font-bold text-creche-blue font-poppins">Panneau d'Administration</h2>
          <button id="close-admin-button" class="bg-red-600 hover:bg-red-700 text-white font-semibold py-2 px-4 rounded-lg">Quitter l'administration</button>
        </div>

        <!-- Gestion des Crèches -->
        <div class="mb-8">
          <h3 class="text-xl font-semibold text-creche-gray mb-4">Gestion des Crèches</h3>
          <form id="form-creche" class="bg-blue-50 p-4 rounded-lg space-y-3 mb-4">
            <input type="hidden" id="creche-id">
            <div>
              <label for="creche-nom" class="block text-sm font-medium text-gray-700">Nom de la crèche:</label>
              <input type="text" id="creche-nom" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" required>
            </div>
            <div>
              <label for="creche-couleur-bg" class="block text-sm font-medium text-gray-700">Classe couleur fond (ex: bg-blue-200):</label>
              <input type="text" id="creche-couleur-bg" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" required>
            </div>
            <div>
              <label for="creche-fiche-bg-image" class="block text-sm font-medium text-gray-700">URL image de fond fiche (optionnel):</label>
              <input type="url" id="creche-fiche-bg-image" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" placeholder="https://example.com/background.jpg">
            </div>
            <div>
              <label for="creche-image" class="block text-sm font-medium text-gray-700">URL Image principale:</label>
              <input type="url" id="creche-image" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" placeholder="https://example.com/image.jpg">
            </div>
            <div>
              <label for="creche-description" class="block text-sm font-medium text-gray-700">Description:</label>
              <textarea id="creche-description" rows="3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2"></textarea>
            </div>
            <!-- Ajouter d'autres champs si nécessaire (équipe, activités etc.) -->
            <button type="submit" class="bg-creche-green hover:bg-creche-green/80 text-white font-bold py-2 px-4 rounded-lg">Sauvegarder Crèche</button>
            <button type="button" id="cancel-creche-edit" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-lg hidden">Annuler Édition</button>
          </form>
          <div id="admin-creches-list" class="space-y-2">
            <!-- Liste des crèches pour admin sera injectée ici -->
          </div>
        </div>

        <!-- Gestion des Projets -->
        <div>
          <h3 class="text-xl font-semibold text-creche-gray mb-4">Gestion des Projets</h3>
          <form id="form-projet" class="bg-green-50 p-4 rounded-lg space-y-3 mb-4">
            <input type="hidden" id="projet-id">
            <div>
              <label for="projet-nom" class="block text-sm font-medium text-gray-700">Nom du projet:</label>
              <input type="text" id="projet-nom" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" required>
            </div>
            <div>
              <label for="projet-date" class="block text-sm font-medium text-gray-700">Date (ex: Juin 2025):</label>
              <input type="text" id="projet-date" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" required>
            </div>
            <div>
              <label for="projet-couleur-bg" class="block text-sm font-medium text-gray-700">Classe couleur fond (ex: bg-blue-200):</label>
              <input type="text" id="projet-couleur-bg" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2" required>
            </div>
             <div>
              <label for="projet-details" class="block text-sm font-medium text-gray-700">Détails (optionnel):</label>
              <textarea id="projet-details" rows="2" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-creche-blue focus:ring-creche-blue sm:text-sm p-2"></textarea>
            </div>
            <button type="submit" class="bg-creche-green hover:bg-creche-green/80 text-white font-bold py-2 px-4 rounded-lg">Sauvegarder Projet</button>
            <button type="button" id="cancel-projet-edit" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-lg hidden">Annuler Édition</button>
          </form>
          <div id="admin-projets-list" class="space-y-2">
            <!-- Liste des projets pour admin sera injectée ici -->
          </div>
        </div>
      </div>
    </section>
    
    <!-- Scripts -->
    <script>
      // Initialisation des icônes Lucide
      document.addEventListener('DOMContentLoaded', function() {
        lucide.createIcons();
        
        // Animation des cartes crèches
        const cards = document.querySelectorAll('.card');
        
        cards.forEach(card => {
          card.addEventListener('mouseenter', function() {
            // Effet sur la carte survolée
            this.style.transform = 'scale(1.1) translateY(-8px)';
            this.style.zIndex = '10';
            this.querySelector('.card-gradient').style.opacity = '1';
            
            // Effet sur les autres cartes
            cards.forEach(otherCard => {
              if (otherCard !== this) {
                otherCard.style.transform = 'scale(0.95)';
                otherCard.style.opacity = '0.75';
              }
            });
          });
          
          card.addEventListener('mouseleave', function() {
            // Restaurer l'état normal de toutes les cartes
            cards.forEach(c => {
              c.style.transform = '';
              c.style.opacity = '1';
              c.style.zIndex = '';
              c.querySelector('.card-gradient').style.opacity = '0';
            });
          });
        });
        
        // Animation de défilement sur click des liens d'ancrage
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
          anchor.addEventListener('click', function (e) {
            e.preventDefault();
            const targetId = this.getAttribute('href');
            if (targetId === '#') return;
            
            const targetElement = document.querySelector(targetId);
            if (targetElement) {
              targetElement.scrollIntoView({
                behavior: 'smooth'
              });
              
              // Fermer le menu mobile si ouvert
              const mobileMenu = document.getElementById('mobile-menu');
              if (mobileMenu && !mobileMenu.classList.contains('hidden')) {
                mobileMenu.classList.add('hidden');
              }
            }
          });
        });
        
        // Menu mobile toggle
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');
        
        if (mobileMenuButton && mobileMenu) {
          mobileMenuButton.addEventListener('click', function() {
            mobileMenu.classList.toggle('hidden');
          });
        }
        
        // FAQ accordéon
        const faqQuestions = document.querySelectorAll('.faq-question');
        
        faqQuestions.forEach(question => {
          question.addEventListener('click', function() {
            const answer = this.nextElementSibling;
            const isOpen = this.classList.contains('active');
            
            // Fermer toutes les réponses
            faqQuestions.forEach(q => {
              q.classList.remove('active');
              q.nextElementSibling.classList.add('hidden');
            });
            
            // Ouvrir/fermer la réponse cliquée
            if (!isOpen) {
              this.classList.add('active');
              answer.classList.remove('hidden');
            }
          });
        });
        
        // Animation fade-in au scroll
        const fadeElements = document.querySelectorAll('.fade-in');
        
        const fadeInOnScroll = function() {
          fadeElements.forEach(element => {
            const elementTop = element.getBoundingClientRect().top;
            const elementBottom = element.getBoundingClientRect().bottom;
            const isVisible = (elementTop < window.innerHeight - 100) && (elementBottom > 0);
            
            if (isVisible) {
              element.classList.add('appear');
            }
          });
        };
        
        // Initial check
        fadeInOnScroll();
        
        // Check on scroll
        window.addEventListener('scroll', fadeInOnScroll);
        
        // Fiche détaillée
        window.handleOpenDetailView = function(crecheId, bgColor) {
          console.log(`Ouverture de la fiche: ${crecheId} avec couleur: ${bgColor}`);
          
          const overlay = document.getElementById('overlay');
          const ficheZoom = document.getElementById('fiche-zoom');
          const ficheContenu = document.getElementById('fiche-contenu');
          const closeDetail = document.getElementById('close-detail');

          const creche = crechesData.find(c => c.id === crecheId);
          if (!creche) {
            console.error("Crèche non trouvée:", crecheId);
            return;
          }
          
          if (overlay && ficheZoom && ficheContenu && closeDetail) {
            // Fonction pour fermer la fiche détaillée avec animation
            window.closeDetailWithAnimation = function() {
              // Animer la fermeture
              ficheContenu.style.opacity = '0';
              ficheContenu.style.transform = 'translateY(10px)';
              
              setTimeout(() => {
                ficheZoom.style.opacity = '0';
                ficheZoom.style.transform = 'scale(0.95)';
                overlay.style.opacity = '0';
                
                setTimeout(() => {
                  overlay.classList.add('hidden');
                  ficheZoom.classList.add('hidden');
                  document.body.classList.remove('overflow-hidden');
                }, 300);
              }, 100);
            };
            
            // Récupérer les coordonnées de la carte cliquée pour l'animation
            let clickedCard;
            document.querySelectorAll('.card').forEach(card => {
              if (card.getAttribute('onclick') && card.getAttribute('onclick').includes(crecheId)) {
                clickedCard = card;
              }
            });
            
            // Préparation de l'animation
            ficheZoom.style.opacity = '0';
            ficheZoom.style.transform = 'scale(0.95)';
            ficheContenu.style.opacity = '0';
            ficheContenu.style.transform = 'translateY(10px)';
            
            // Afficher l'overlay avec effet de fondu
            overlay.classList.remove('hidden');
            overlay.style.opacity = '0';
            ficheZoom.classList.remove('hidden');
            
            setTimeout(() => {
              overlay.style.opacity = '1';
              
              // Animation de la fiche
              setTimeout(() => {
                ficheZoom.style.opacity = '1';
                ficheZoom.style.transform = 'scale(1)';
                document.body.classList.add('overflow-hidden');
                
                // Afficher le contenu après un court délai
                setTimeout(() => {
                  ficheContenu.style.opacity = '1';
                  ficheContenu.style.transform = 'translateY(0)';
                }, 200);
              }, 50);
            }, 10);
            
            // Exemple de contenu dynamique (à remplacer par du contenu réel)
            ficheZoom.className = "fixed top-[5%] left-[5%] w-[90%] h-[90%] bg-white/95 backdrop-blur-md rounded-2xl shadow-2xl p-10 z-50 transition-all duration-500 ease-in-out opacity-0 scale-95 pointer-events-none transform-gpu";
            ficheZoom.style.backgroundImage = '';
            ficheZoom.style.backgroundSize = '';
            ficheZoom.style.backgroundPosition = '';
            ficheZoom.style.backgroundRepeat = '';
            if (creche.ficheBgImage && creche.ficheBgImage.trim() !== "") {
              ficheZoom.style.backgroundImage = `url('${creche.ficheBgImage}')`;
              ficheZoom.style.backgroundSize = 'cover';
              ficheZoom.style.backgroundPosition = 'center';
              ficheZoom.style.backgroundRepeat = 'no-repeat';
            }
            ficheContenu.innerHTML = `
              <div class="flex flex-col md:flex-row gap-6">
                <div class="md:w-1/2">
                  <img src="${creche.image || 'https://via.placeholder.com/600x300.png?text=Image+Crèche'}" alt="${creche.nom}" class="w-full h-64 object-cover rounded-xl shadow-lg">
                  <div class="mt-4 grid grid-cols-2 gap-2">
                    <div class="${creche.couleurBg} p-3 rounded-lg text-white text-sm">
                      <i data-lucide="map-pin" class="inline-block w-4 h-4 mr-1"></i> ${creche.nom}
                    </div>
                     <div class="${creche.couleurBg} p-3 rounded-lg text-white text-sm">
                      <i data-lucide="users" class="inline-block w-4 h-4 mr-1"></i> ${creche.equipe ? creche.equipe.length : 'N/A'} membres
                    </div>
                  </div>
                </div>
                <div class="md:w-1/2">
                  <h2 id="fiche-titre" class="text-2xl font-bold mb-3 text-[#6D6875]">${creche.nom}</h2>
                  <p class="mb-4 text-[#6D6875]/90">${creche.description || 'Description non disponible.'}</p>
                  
                  <h3 class="text-xl font-semibold mb-2 text-[#6D6875]">Notre équipe</h3>
                  <ul class="list-disc pl-5 mb-4 text-[#6D6875]/80">
                    ${creche.equipe ? creche.equipe.map(e => `<li>${e}</li>`).join('') : '<li>Information non disponible</li>'}
                  </ul>
                  
                  <h3 class="text-xl font-semibold mb-2 text-[#6D6875]">Activités proposées</h3>
                  <div class="flex flex-wrap gap-2 mb-6">
                    ${creche.activites ? creche.activites.map(a => `<span class="bg-gray-200 text-gray-700 px-2 py-1 rounded-full text-xs">${a}</span>`).join('') : '<p class="text-sm text-gray-500">Aucune activité spécifiée.</p>'}
                  </div>
                  
                  <button onclick="document.getElementById('reserver').scrollIntoView({behavior: 'smooth'}); closeDetailWithAnimation();" class="bg-[#5DADEC] text-white px-6 py-3 rounded-lg font-semibold hover:bg-[#5DADEC]/80 transition-all duration-300 hover:scale-105 shadow-md w-full">
                    Réserver une place
                  </button>
                </div>
              </div>
            `;
            
            // Update des icônes dans le contenu dynamique
            lucide.createIcons();
            
            // Fermeture au clic sur le bouton fermer
            closeDetail.addEventListener('click', closeDetailWithAnimation);
            
            // Fermeture avec la touche Echap
            document.addEventListener('keydown', function(e) {
              if (e.key === 'Escape') {
                closeDetailWithAnimation();
              }
            });
            
            // Fermeture au clic sur l'overlay
            overlay.addEventListener('click', function(e) {
              if (e.target === overlay) {
                closeDetailWithAnimation();
              }
            });
          }
        };
        
        // Navigation carrousel projets
        const prevButton = document.getElementById('prev-slide');
        const nextButton = document.getElementById('next-slide');
        const carousel = document.getElementById('projets-carousel');
        
        if (prevButton && nextButton && carousel) {
          prevButton.addEventListener('click', function() {
            carousel.scrollBy({ left: -300, behavior: 'smooth' });
          });
          
          nextButton.addEventListener('click', function() {
            carousel.scrollBy({ left: 300, behavior: 'smooth' });
          });
        }
        
        // SYSTÈME DE RÉSERVATION - NAVIGATION ENTRE ÉTAPES
        
        // Références aux éléments DOM
        const etape1Tab = document.getElementById('etape-1');
        const etape2Tab = document.getElementById('etape-2');
        const etape3Tab = document.getElementById('etape-3');
        
        const contenuEtape1 = document.getElementById('contenu-etape-1');
        const contenuEtape2 = document.getElementById('contenu-etape-2');
        const contenuEtape3 = document.getElementById('contenu-etape-3');
        const confirmationReservation = document.getElementById('confirmation-reservation');
        
        const btnRechercherCreche = document.getElementById('rechercher-creche');
        const listeCreches = document.getElementById('liste-creches');
        const resultatRecherche = document.getElementById('resultat-recherche');
        
        const voirDisponibilites1 = document.getElementById('voir-disponibilites-1');
        const voirDisponibilites2 = document.getElementById('voir-disponibilites-2');
        
        const retourEtape1 = document.getElementById('retour-etape-1');
        const retourEtape2 = document.getElementById('retour-etape-2');
        
        const boutonDemande = document.getElementById('bouton-demande');
        const formulaireReservation = document.getElementById('formulaire-reservation');
        const nouvelleRecherche = document.getElementById('nouvelle-recherche');
        
        const dateSelectables = document.querySelectorAll('.date-selectable');
        
        // Fonction pour mettre à jour l'affichage des étapes
        function afficherEtape(etape) {
          // Masquer toutes les étapes
          [contenuEtape1, contenuEtape2, contenuEtape3, confirmationReservation].forEach(el => {
            if (el) el.classList.add('hidden');
          });
          
          // Réinitialiser les onglets
          [etape1Tab, etape2Tab, etape3Tab].forEach(tab => {
            if (tab) {
              tab.classList.add('opacity-70');
              tab.querySelector('div div').classList.remove('bg-creche-orange', 'bg-creche-blue', 'bg-creche-green');
              tab.querySelector('div div').classList.add('bg-gray-300');
              tab.querySelector('span').classList.remove('text-creche-orange', 'text-creche-blue', 'text-creche-green');
              tab.querySelector('span').classList.add('text-creche-gray');
              
              // Supprimer la ligne bleue
              const existingLine = tab.querySelector('.absolute');
              if (existingLine) existingLine.remove();
            }
          });
          
          // Afficher l'étape demandée
          if (etape === 1 && contenuEtape1) {
            contenuEtape1.classList.remove('hidden');
            etape1Tab.classList.remove('opacity-70');
            etape1Tab.querySelector('div div').classList.remove('bg-gray-300');
            etape1Tab.querySelector('div div').classList.add('bg-creche-orange');
            etape1Tab.querySelector('span').classList.remove('text-creche-gray');
            etape1Tab.querySelector('span').classList.add('text-creche-orange');
            
            // Ajouter la ligne orange
            const line = document.createElement('div');
            line.className = 'absolute bottom-0 left-0 w-full h-0.5 bg-creche-orange';
            etape1Tab.appendChild(line);
          } else if (etape === 2 && contenuEtape2) {
            contenuEtape2.classList.remove('hidden');
            etape2Tab.classList.remove('opacity-70');
            etape2Tab.querySelector('div div').classList.remove('bg-gray-300');
            etape2Tab.querySelector('div div').classList.add('bg-creche-blue');
            etape2Tab.querySelector('span').classList.remove('text-creche-gray');
            etape2Tab.querySelector('span').classList.add('text-creche-blue');
            
            // Ajouter la ligne bleue
            const line = document.createElement('div');
            line.className = 'absolute bottom-0 left-0 w-full h-0.5 bg-creche-blue';
            etape2Tab.appendChild(line);
          } else if (etape === 3 && contenuEtape3) {
            contenuEtape3.classList.remove('hidden');
            etape3Tab.classList.remove('opacity-70');
            etape3Tab.querySelector('div div').classList.remove('bg-gray-300');
            etape3Tab.querySelector('div div').classList.add('bg-creche-green');
            etape3Tab.querySelector('span').classList.remove('text-creche-gray');
            etape3Tab.querySelector('span').classList.add('text-creche-green');
            
            // Ajouter la ligne verte
            const line = document.createElement('div');
            line.className = 'absolute bottom-0 left-0 w-full h-0.5 bg-creche-green';
            etape3Tab.appendChild(line);
          } else if (etape === 4 && confirmationReservation) {
            confirmationReservation.classList.remove('hidden');
          }
        }
        
        // Initialisation de la carte Leaflet
        let leafletMap;
        const initMap = () => {
          if (!leafletMap && document.getElementById('map')) {
            leafletMap = L.map('map').setView([48.117266, -1.6777926], 13);

            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
              attribution: '&copy; OpenStreetMap contributors'
            }).addTo(leafletMap);
          }
        };
        
        // Initialiser la carte si on est sur la page de réservation
        if (document.getElementById('map')) {
          initMap();
          
          // Ajouter des marqueurs pour les crèches
          const creches = [
            { nom: 'Les Petits Merlins', position: [48.117266, -1.6777926], color: 'blue' },
            { nom: 'Joséphine Baker', position: [48.125984, -1.6886883], color: 'green' },
            { nom: 'M\'Ti Moun', position: [48.109343, -1.6599130], color: 'orange' },
            { nom: 'Regard\'Enfants', position: [48.103729, -1.6741464], color: 'pink' }
          ];
          
          creches.forEach(creche => {
            const marker = L.marker(creche.position).addTo(leafletMap);
            marker.bindPopup(`
              <b>${creche.nom}</b><br>
              <a href="#" class="text-blue-500" onclick="showCrecheDetails('${creche.nom}')">Voir détails</a>
            `);
            creche.marker = marker; // Stocker la référence du marqueur
            
            // Ajouter un événement de clic sur le marqueur pour afficher les crèches trouvées
            marker.on('click', function() {
              if (listeCreches) {
                listeCreches.classList.remove('hidden');
                
                // Simuler un marqueur pour l'adresse si elle est saisie
                const adresse = document.getElementById('adresse').value;
                if (adresse) {
                  // Coordonnées fictives pour la démonstration
                  const userPosition = [48.1149, -1.6642];
                  
                  // Tracer une ligne vers la crèche
                  L.polyline([
                    userPosition,
                    creche.position
                  ], {
                    color: '#5DADEC',
                    weight: 3,
                    opacity: 0.8
                  }).addTo(leafletMap);
                  
                  // Ajuster la vue pour montrer l'utilisateur et la crèche
                  const bounds = L.latLngBounds([
                    userPosition,
                    creche.position
                  ]);
                  leafletMap.fitBounds(bounds, { padding: [50, 50] });
                }
              }
            });
          });
        }
        
        // Événements pour la navigation
        if (btnRechercherCreche) {
          btnRechercherCreche.addEventListener('click', function() {
            // Simuler la recherche
            resultatRecherche.classList.remove('hidden');
            resultatRecherche.innerHTML = '<p class="font-medium">Recherche en cours...</p>';
            
            setTimeout(() => {
              resultatRecherche.classList.add('hidden');
              listeCreches.classList.remove('hidden');
              
              // Simuler un marqueur pour l'adresse saisie
              const adresse = document.getElementById('adresse').value;
              if (adresse && leafletMap) {
                // Coordonnées fictives pour la démonstration
                const userPosition = [48.1149, -1.6642];
                
                // Ajouter un marqueur pour l'utilisateur
                const userMarker = L.marker(userPosition, {
                  icon: L.divIcon({
                    className: 'bg-red-500 w-4 h-4 rounded-full border-2 border-white',
                    iconSize: [12, 12]
                  })
                }).addTo(leafletMap);
                userMarker.bindPopup(`<b>Votre adresse:</b><br>${adresse}`).openPopup();
                
                // Centrer la carte sur la position
                leafletMap.setView(userPosition, 14);
                
                // Tracer une ligne vers la crèche la plus proche (Les Petits Merlins)
                const polyline = L.polyline([
                  userPosition,
                  [48.117266, -1.6777926] // Les Petits Merlins
                ], {
                  color: '#5DADEC',
                  weight: 3,
                  opacity: 0.8
                }).addTo(leafletMap);
                
                // Ajuster la vue pour montrer l'utilisateur et la crèche
                const bounds = L.latLngBounds([
                  userPosition,
                  [48.117266, -1.6777926]
                ]);
                leafletMap.fitBounds(bounds, { padding: [50, 50] });
              }
            }, 1500);
          });
        }
        
        // Navigation vers l'étape 2
        if (voirDisponibilites1) {
          voirDisponibilites1.addEventListener('click', function(e) {
            e.preventDefault();
            afficherEtape(2);
          });
        }
        
        if (voirDisponibilites2) {
          voirDisponibilites2.addEventListener('click', function(e) {
            e.preventDefault();
            afficherEtape(2);
          });
        }
        
        // Retours aux étapes précédentes
        if (retourEtape1) {
          retourEtape1.addEventListener('click', function() {
            afficherEtape(1);
          });
        }
        
        if (retourEtape2) {
          retourEtape2.addEventListener('click', function() {
            afficherEtape(2);
          });
        }
        
        // Sélection des dates
        if (dateSelectables.length > 0) {
          dateSelectables.forEach(date => {
            date.addEventListener('click', function() {
              // Supprimer la classe active de toutes les dates
              dateSelectables.forEach(d => d.classList.remove('ring-2', 'ring-creche-blue'));
              
              // Marquer la date sélectionnée comme active
              this.classList.add('ring-2', 'ring-creche-blue');
            });
          });
        }
        
        // Passage à l'étape 3
        if (boutonDemande) {
          boutonDemande.addEventListener('click', function() {
            afficherEtape(3);
          });
        }
        
        // Soumission du formulaire
        if (formulaireReservation) {
          formulaireReservation.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Simuler l'envoi du formulaire
            const submitBtn = this.querySelector('button[type="submit"]');
            submitBtn.innerHTML = '<span class="flex items-center justify-center"><i data-lucide="loader-2" class="w-5 h-5 mr-2 animate-spin"></i> Envoi en cours...</span>';
            submitBtn.disabled = true;
            
            setTimeout(() => {
              afficherEtape(4);
            }, 1500);
          });
        }
        
        // Nouvelle recherche
        if (nouvelleRecherche) {
          nouvelleRecherche.addEventListener('click', function() {
            afficherEtape(1);
            listeCreches.classList.add('hidden');
            
            // Réinitialiser le formulaire
            if (formulaireReservation) {
              formulaireReservation.reset();
            }
            
            // Réinitialiser la carte
            if (leafletMap) {
              leafletMap.eachLayer(layer => {
                if (layer instanceof L.Marker || layer instanceof L.Polyline) {
                  leafletMap.removeLayer(layer);
                }
              });
              
              // Restaurer les marqueurs des crèches
              const creches = [
                { nom: 'Les Petits Merlins', position: [48.117266, -1.6777926], color: 'blue' },
                { nom: 'Joséphine Baker', position: [48.125984, -1.6886883], color: 'green' },
                { nom: 'M\'Ti Moun', position: [48.109343, -1.6599130], color: 'orange' },
                { nom: 'Regard\'Enfants', position: [48.103729, -1.6741464], color: 'pink' }
              ];
              
              creches.forEach(creche => {
                const marker = L.marker(creche.position).addTo(leafletMap);
                marker.bindPopup(`
                  <b>${creche.nom}</b><br>
                  <a href="#" class="text-blue-500" onclick="showCrecheDetails('${creche.nom}')">Voir détails</a>
                `);
                
                // Ajouter un événement de clic sur le marqueur pour afficher les crèches trouvées
                marker.on('click', function() {
                  if (listeCreches) {
                    listeCreches.classList.remove('hidden');
                  }
                });
              });
              
              // Réinitialiser la vue
              leafletMap.setView([48.117266, -1.6777926], 13);
            }
          });
        }
        
        // Navigation par onglets
        if (etape1Tab) {
          etape1Tab.addEventListener('click', function() {
            afficherEtape(1);
          });
        }
        
        if (etape2Tab) {
          etape2Tab.addEventListener('click', function() {
            // Vérifier si l'étape 1 a été complétée (liste des crèches visible)
            if (!listeCreches.classList.contains('hidden')) {
              afficherEtape(2);
            }
          });
        }
        
        if (etape3Tab) {
          etape3Tab.addEventListener('click', function() {
            // Vérifier si une date a été sélectionnée
            const dateSelectionnee = document.querySelector('.date-selectable.ring-2');
            if (dateSelectionnee) {
              afficherEtape(3);
            }
          });
        }
        
        // Fonction pour afficher les détails d'une crèche depuis la carte
        window.showCrecheDetails = function(crecheName) {
          // Fermer le popup
          leafletMap.closePopup();
          
          // Afficher la liste des crèches si elle est masquée
          if (listeCreches && listeCreches.classList.contains('hidden')) {
            listeCreches.classList.remove('hidden');
          }
          
          // Simuler un clic sur "Voir les disponibilités"
          setTimeout(() => {
            if (voirDisponibilites1) {
              voirDisponibilites1.click();
            }
          }, 500);
        }

        // Données initiales (normalement chargées depuis un backend ou un fichier JSON)
        let crechesData = [
          { id: 'merlins', nom: 'Les Petits Merlins', couleurBg: 'bg-blue-200', ficheBg: 'bg-gradient-to-br from-blue-100 to-blue-200', image: 'https://images.unsplash.com/photo-1540479859555-17af45c78602?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80', description: 'Une crèche accueillante avec un programme pédagogique innovant.', equipe: ['1 directrice éducatrice', '1 psychomotricienne'], activites: ['Éveil musical', 'Jeux d\'eau'] },
          { id: 'baker', nom: 'Joséphine Baker', couleurBg: 'bg-green-200', ficheBg: 'bg-gradient-to-br from-green-100 to-green-200', image: 'https://images.unsplash.com/photo-1519682577862-22b62b24e493?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80', description: 'Un environnement stimulant pour les tout-petits.', equipe: ['1 directrice', '2 auxiliaires'], activites: ['Peinture', 'Motricité'] },
          { id: 'moun', nom: 'M\'Ti Moun', couleurBg: 'bg-yellow-200', ficheBg: 'bg-gradient-to-br from-yellow-100 to-yellow-200', image: 'https://images.unsplash.com/photo-1503454537195-1dcabb73ffb9?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80', description: 'Crèche axée sur le développement durable.', equipe: ['1 éducatrice', '1 agent'], activites: ['Jardinage', 'Recyclage'] },
          { id: 'regard', nom: 'Regard\'Enfants', couleurBg: 'bg-pink-200', ficheBg: 'bg-gradient-to-br from-pink-100 to-pink-200', image: 'https://images.unsplash.com/photo-1576092762791-d67511ea808c?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80', description: 'Pédagogie active et bienveillante.', equipe: ['2 éducatrices', '1 cuisinier'], activites: ['Contes', 'Sorties nature'] }
        ];

        let projetsData = [
          { id: 'montgermont', nom: 'Crèche Montgermont', date: 'Juin 2025', couleurBg: 'bg-blue-200', details: 'Ouverture d\'une nouvelle structure à Montgermont.' },
          { id: 'intergenerationnel', nom: 'Projet intergénérationnel', date: 'Avril 2025', couleurBg: 'bg-green-200', details: 'Rencontres entre les enfants et les seniors.' },
          { id: 'portesouvertes', nom: 'Portes ouvertes', date: 'Mars 2025', couleurBg: 'bg-blue-300', details: 'Journée découverte de nos crèches.' },
          { id: 'crechemobile', nom: 'Crèche mobile', date: 'Septembre 2025', couleurBg: 'bg-creche-blue/30', details: 'Un service de crèche itinérant pour les zones rurales.' }
        ];
        
        const crechesCardGroup = document.getElementById('creches-card-group');
        const projetsCarousel = document.getElementById('projets-carousel');

        function renderPublicCreches() {
          if (!crechesCardGroup) return;
          crechesCardGroup.innerHTML = ''; // Vider le contenu existant
          crechesData.forEach(creche => {
            const cardDiv = document.createElement('div');
            cardDiv.className = `card flex-1 ${creche.couleurBg.replace('bg-', 'bg-') || 'bg-gray-300'} rounded-xl shadow-lg flex items-center justify-center cursor-pointer hover:shadow-xl transition-all duration-500 p-4 text-center overflow-hidden transform hover:scale-110 hover:-translate-y-2 hover:z-10 relative`;
            cardDiv.setAttribute('onclick', `handleOpenDetailView('${creche.id}', '${creche.couleurBg}')`);
            
            cardDiv.innerHTML = `
              <div class="card-gradient absolute inset-0 opacity-0 bg-gradient-to-br from-white/40 to-transparent transition-opacity duration-300"></div>
              <span class="font-poppins text-white text-xl font-semibold relative z-10">${creche.nom}</span>
            `;
            crechesCardGroup.appendChild(cardDiv);
          });
          // Ré-appliquer les listeners pour l'effet de survol des cartes
          initCardHoverEffects();
        }

        function renderPublicProjetsCarousel() {
          if (!projetsCarousel) return;
          projetsCarousel.innerHTML = ''; // Vider le contenu existant
          projetsData.forEach(projet => {
            const projetDiv = document.createElement('div');
            projetDiv.className = `w-64 h-64 md:w-72 md:h-72 rounded-full ${projet.couleurBg} border-8 border-white shadow-xl flex flex-col items-center justify-center p-6 transition-all duration-300 group cursor-pointer hover:shadow-[0_0_20px_rgba(0,0,0,0.1)]`;
            // On pourrait ajouter un onclick pour afficher les détails du projet si nécessaire
            projetDiv.innerHTML = `
              <span class="font-poppins font-bold text-creche-gray text-xl text-center mb-1">${projet.nom}</span>
              <span class="text-blue-400 font-semibold">${projet.date}</span>
            `;
            projetsCarousel.appendChild(projetDiv);
          });
        }
        
        // Animation des cartes crèches (doit être appelée après le rendu)
        function initCardHoverEffects() {
            const cards = document.querySelectorAll('#creches-card-group .card');
            cards.forEach(card => {
              card.addEventListener('mouseenter', function() {
                this.style.transform = 'scale(1.1) translateY(-8px)';
                this.style.zIndex = '10';
                const gradient = this.querySelector('.card-gradient');
                if (gradient) gradient.style.opacity = '1';
                
                cards.forEach(otherCard => {
                  if (otherCard !== this) {
                    otherCard.style.transform = 'scale(0.95)';
                    otherCard.style.opacity = '0.75';
                  }
                });
              });
              
              card.addEventListener('mouseleave', function() {
                cards.forEach(c => {
                  c.style.transform = '';
                  c.style.opacity = '1';
                  c.style.zIndex = '';
                  const grad = c.querySelector('.card-gradient');
                  if (grad) grad.style.opacity = '0';
                });
              });
            });
        }
        
        // --- DÉBUT SECTION ADMINISTRATION ---
        const adminSection = document.getElementById('admin-section');
        const adminButton = document.getElementById('admin-button');
        const closeAdminButton = document.getElementById('close-admin-button');
        const mainContentForAdminToggle = [
            document.querySelector('header'), 
            ...document.querySelectorAll('body > section:not(#admin-section)'), // Toutes les sections sauf l'admin
            document.querySelector('footer')
        ].filter(el => el);


        const formCreche = document.getElementById('form-creche');
        const crecheIdInput = document.getElementById('creche-id');
        const crecheNomInput = document.getElementById('creche-nom');
        const crecheCouleurBgInput = document.getElementById('creche-couleur-bg');
        const crecheFicheBgImageInput = document.getElementById('creche-fiche-bg-image');
        const crecheImageInput = document.getElementById('creche-image');
        const crecheDescriptionInput = document.getElementById('creche-description');
        const adminCrechesList = document.getElementById('admin-creches-list');
        const cancelCrecheEditBtn = document.getElementById('cancel-creche-edit');

        const formProjet = document.getElementById('form-projet');
        const projetIdInput = document.getElementById('projet-id');
        const projetNomInput = document.getElementById('projet-nom');
        const projetDateInput = document.getElementById('projet-date');
        const projetCouleurBgInput = document.getElementById('projet-couleur-bg');
        const projetDetailsInput = document.getElementById('projet-details');
        const adminProjetsList = document.getElementById('admin-projets-list');
        const cancelProjetEditBtn = document.getElementById('cancel-projet-edit');

        function toggleAdminSection(show) {
            if (show) {
                adminSection.classList.remove('hidden');
                mainContentForAdminToggle.forEach(el => el.classList.add('hidden'));
                document.body.classList.add('overflow-hidden'); // Empêche le scroll de la page principale
            } else {
                adminSection.classList.add('hidden');
                mainContentForAdminToggle.forEach(el => el.classList.remove('hidden'));
                document.body.classList.remove('overflow-hidden');
            }
        }

        if (adminButton) adminButton.addEventListener('click', () => toggleAdminSection(true));
        if (closeAdminButton) closeAdminButton.addEventListener('click', () => toggleAdminSection(false));
        
        // Fonctions de rendu pour l'admin
        function renderAdminCreches() {
            if (!adminCrechesList) return;
            adminCrechesList.innerHTML = '';
            crechesData.forEach(creche => {
                const item = document.createElement('div');
                item.className = 'p-3 bg-gray-50 rounded-md shadow-sm flex justify-between items-center';
                item.innerHTML = `
                    <span>${creche.nom} (ID: ${creche.id})</span>
                    <div>
                        <button data-id="${creche.id}" class="edit-creche-btn text-blue-600 hover:text-blue-800 mr-2">Modifier</button>
                        <button data-id="${creche.id}" class="delete-creche-btn text-red-600 hover:text-red-800">Supprimer</button>
                    </div>
                `;
                adminCrechesList.appendChild(item);
            });
            addAdminCrecheListeners();
        }

        function renderAdminProjets() {
            if (!adminProjetsList) return;
            adminProjetsList.innerHTML = '';
            projetsData.forEach(projet => {
                const item = document.createElement('div');
                item.className = 'p-3 bg-gray-50 rounded-md shadow-sm flex justify-between items-center';
                item.innerHTML = `
                    <span>${projet.nom} (ID: ${projet.id})</span>
                    <div>
                        <button data-id="${projet.id}" class="edit-projet-btn text-blue-600 hover:text-blue-800 mr-2">Modifier</button>
                        <button data-id="${projet.id}" class="delete-projet-btn text-red-600 hover:text-red-800">Supprimer</button>
                    </div>
                `;
                adminProjetsList.appendChild(item);
            });
            addAdminProjetListeners();
        }

        // Gestion formulaires Crèches
        if (formCreche) {
            formCreche.addEventListener('submit', function(e) {
                e.preventDefault();
                const id = crecheIdInput.value || `creche_${Date.now()}`;
                const nom = crecheNomInput.value;
                const couleurBg = crecheCouleurBgInput.value;
                const ficheBgImage = crecheFicheBgImageInput.value;
                const image = crecheImageInput.value;
                const description = crecheDescriptionInput.value;

                const existingIndex = crechesData.findIndex(c => c.id === id);
                const newCrecheData = { id, nom, couleurBg, ficheBgImage, image, description, equipe: [], activites: [] }; // Simplifié pour l'exemple

                if (existingIndex > -1) {
                    crechesData[existingIndex] = { ...crechesData[existingIndex], ...newCrecheData };
                } else {
                    crechesData.push(newCrecheData);
                }
                renderAdminCreches();
                renderPublicCreches();
                formCreche.reset();
                crecheIdInput.value = '';
                cancelCrecheEditBtn.classList.add('hidden');
            });
        }
        if (cancelCrecheEditBtn) {
            cancelCrecheEditBtn.addEventListener('click', () => {
                formCreche.reset();
                crecheIdInput.value = '';
                cancelCrecheEditBtn.classList.add('hidden');
            });
        }


        function addAdminCrecheListeners() {
            document.querySelectorAll('.edit-creche-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.dataset.id;
                    const creche = crechesData.find(c => c.id === id);
                    if (creche) {
                        crecheIdInput.value = creche.id;
                        crecheNomInput.value = creche.nom;
                        crecheCouleurBgInput.value = creche.couleurBg;
                        crecheFicheBgImageInput.value = creche.ficheBgImage || '';
                        crecheImageInput.value = creche.image || '';
                        crecheDescriptionInput.value = creche.description || '';
                        cancelCrecheEditBtn.classList.remove('hidden');
                        crecheNomInput.focus();
                    }
                });
            });
            document.querySelectorAll('.delete-creche-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    if (confirm('Êtes-vous sûr de vouloir supprimer cette crèche ?')) {
                        const id = this.dataset.id;
                        crechesData = crechesData.filter(c => c.id !== id);
                        renderAdminCreches();
                        renderPublicCreches();
                    }
                });
            });
        }

        // Gestion formulaires Projets
         if (formProjet) {
            formProjet.addEventListener('submit', function(e) {
                e.preventDefault();
                const id = projetIdInput.value || `projet_${Date.now()}`;
                const nom = projetNomInput.value;
                const date = projetDateInput.value;
                const couleurBg = projetCouleurBgInput.value;
                const details = projetDetailsInput.value;

                const existingIndex = projetsData.findIndex(p => p.id === id);
                const newProjetData = { id, nom, date, couleurBg, details };

                if (existingIndex > -1) {
                    projetsData[existingIndex] = { ...projetsData[existingIndex], ...newProjetData};
                } else {
                    projetsData.push(newProjetData);
                }
                renderAdminProjets();
                renderPublicProjetsCarousel();
                formProjet.reset();
                projetIdInput.value = '';
                cancelProjetEditBtn.classList.add('hidden');
            });
        }

        if (cancelProjetEditBtn) {
            cancelProjetEditBtn.addEventListener('click', () => {
                formProjet.reset();
                projetIdInput.value = '';
                cancelProjetEditBtn.classList.add('hidden');
            });
        }

        function addAdminProjetListeners() {
            document.querySelectorAll('.edit-projet-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.dataset.id;
                    const projet = projetsData.find(p => p.id === id);
                    if (projet) {
                        projetIdInput.value = projet.id;
                        projetNomInput.value = projet.nom;
                        projetDateInput.value = projet.date;
                        projetCouleurBgInput.value = projet.couleurBg;
                        projetDetailsInput.value = projet.details || '';
                        cancelProjetEditBtn.classList.remove('hidden');
                        projetNomInput.focus();
                    }
                });
            });
            document.querySelectorAll('.delete-projet-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    if (confirm('Êtes-vous sûr de vouloir supprimer ce projet ?')) {
                        const id = this.dataset.id;
                        projetsData = projetsData.filter(p => p.id !== id);
                        renderAdminProjets();
                        renderPublicProjetsCarousel();
                    }
                });
            });
        }
        
        // Rendu initial
        renderPublicCreches();
        renderPublicProjetsCarousel();
        renderAdminCreches();
        renderAdminProjets();
        // --- FIN SECTION ADMINISTRATION ---

      });
    </script>
  

</body></html>
