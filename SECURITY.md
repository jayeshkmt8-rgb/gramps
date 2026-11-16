<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>The Drone Man – Fly along the world</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;600;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
<style>
:root{--sky:#0b2a4a;--ink:#10202f;--paper:#f5f8fb;--card:#fff;--line:#dbe4ec;--accent:#ff6b2c;--accent-d:#e0541a;--ok:#1a9a5a;--muted:#5b6b7a}
*{box-sizing:border-box;margin:0}
html{scroll-behavior:smooth}
body{font-family:Inter,system-ui,sans-serif;background:var(--paper);color:var(--ink);line-height:1.5}
h1,h2,h3{font-family:Sora,Inter,sans-serif}
header{position:sticky;top:0;z-index:20;background:rgba(11,42,74,.96);color:#fff;display:flex;align-items:center;justify-content:space-between;padding:12px 16px}
header b{font-family:Sora;font-size:1.1rem;letter-spacing:.3px}
.cartbtn{background:var(--accent);color:#fff;border:0;border-radius:999px;padding:8px 16px;font-weight:600;cursor:pointer;font-size:.95rem}
.cartbtn:hover{background:var(--accent-d)}
.hero{min-height:78vh;display:flex;align-items:center;padding:48px 20px;color:#fff;background:linear-gradient(90deg,rgba(7,24,43,.88),rgba(7,24,43,.35)),url("https://i.ibb.co/JFMyrFZ1/Screenshot-2026-11-17-004636.png") center/cover}
.hero div{max-width:640px}
.hero h1{font-size:clamp(2.2rem,8vw,4.2rem);line-height:1.05;font-weight:800}
.hero p{margin:16px 0 26px;font-size:1.1rem;max-width:460px;color:#dbe8f5}
.btn{display:inline-block;background:var(--accent);color:#fff;border:0;border-radius:10px;padding:14px 28px;font-size:1rem;font-weight:600;cursor:pointer;text-decoration:none}
.btn:hover{background:var(--accent-d)}
.btn:focus-visible,.cartbtn:focus-visible,.arrow:focus-visible,input:focus-visible,textarea:focus-visible{outline:3px solid #7cc4ff;outline-offset:2px}
section{padding:48px 0}
.wrap{padding:0 16px;max-width:1200px;margin:auto}
h2{font-size:1.7rem;margin-bottom:6px}
.sub{color:var(--muted);margin-bottom:20px}
.carwrap{position:relative}
.track{display:flex;gap:16px;overflow-x:auto;scroll-snap-type:x mandatory;padding:6px 16px 18px;scrollbar-width:thin}
.card{flex:0 0 min(280px,78vw);scroll-snap-align:start;background:var(--card);border:1px solid var(--line);border-radius:14px;overflow:hidden;display:flex;flex-direction:column}
.card img{width:100%;aspect-ratio:4/3;object-fit:cover;background:#e6edf3}
.card .b{padding:14px;display:flex;flex-direction:column;gap:6px;flex:1}
.card h3{font-size:1.02rem}
.price{font-weight:800;font-size:1.15rem;color:var(--sky)}
.card .btn{padding:11px;margin-top:auto;width:100%;text-align:center}
.arrow{position:absolute;top:38%;width:40px;height:40px;border-radius:50%;border:0;background:#fff;box-shadow:0 2px 10px rgba(0,0,0,.25);font-size:1.3rem;cursor:pointer;z-index:2;display:none}
.arrow.l{left:6px}.arrow.r{right:6px}
@media(min-width:700px){.arrow{display:block}}
.pay{background:var(--sky);color:#fff}
.pay .grid{display:grid;gap:24px;align-items:center}
@media(min-width:700px){.pay .grid{grid-template-columns:1fr 280px}}
.pay img{width:100%;max-width:280px;border-radius:12px;background:#fff;padding:8px}
.pay p{color:#cfe0f0;margin-top:8px}
footer{background:#07182b;color:#9fb4c8;text-align:center;padding:24px 16px;font-size:.92rem}
footer a{color:#fff}
.wa{position:fixed;right:16px;bottom:16px;width:58px;height:58px;border-radius:50%;background:#25d366;display:grid;place-items:center;box-shadow:0 4px 14px rgba(0,0,0,.3);z-index:30}
.wa svg{width:32px;height:32px;fill:#fff}
/* cart drawer */
.ov{position:fixed;inset:0;background:rgba(0,0,0,.5);opacity:0;pointer-events:none;transition:opacity .2s;z-index:40}
.ov.on{opacity:1;pointer-events:auto}
.drawer{position:fixed;top:0;right:0;height:100%;width:min(440px,100%);background:#fff;z-index:50;transform:translateX(100%);transition:transform .25s;display:flex;flex-direction:column}
.drawer.on{transform:none}
.dh{display:flex;justify-content:space-between;align-items:center;padding:16px;border-bottom:1px solid var(--line)}
.dh button{background:none;border:0;font-size:1.6rem;cursor:pointer}
.db{overflow:auto;padding:16px;flex:1}
.item{display:flex;gap:10px;align-items:center;padding:10px 0;border-bottom:1px solid var(--line)}
.item img{width:56px;height:56px;object-fit:cover;border-radius:8px}
.item .n{flex:1;font-size:.93rem}
.qty{display:flex;align-items:center;gap:6px}
.qty button{width:28px;height:28px;border-radius:6px;border:1px solid var(--line);background:#fff;cursor:pointer}
.empty{color:var(--muted);padding:20px 0;text-align:center}
.total{display:flex;justify-content:space-between;font-weight:800;padding:14px 0;font-size:1.1rem}
label{display:block;font-size:.88rem;font-weight:600;margin:12px 0 4px}
input[type=text],input[type=tel],textarea{width:100%;padding:11px;border:1px solid var(--line);border-radius:8px;font:inherit}
.opt{display:flex;gap:8px;align-items:center;border:1px solid var(--line);border-radius:8px;padding:10px;margin-top:6px;cursor:pointer}
.opt input{accent-color:var(--accent)}
#qrbox{display:none;text-align:center;margin-top:10px}
#qrbox img{width:200px;max-width:100%;border:1px solid var(--line);border-radius:10px}
#qrbox small{display:block;color:var(--muted)}
.msg{margin-top:10px;font-size:.92rem;font-weight:600}
.msg.ok{color:var(--ok)}.msg.err{color:#c0392b}
.df{padding:0 16px 16px}
@media(prefers-reduced-motion:reduce){*{transition:none!important;scroll-behavior:auto!important}}
</style>
</head>
<body>

<header>
  <b>THE DRONE MAN</b>
  <button class="cartbtn" id="openCart" aria-label="Open cart">Cart (<span id="cnt">0</span>)</button>
</header>

<div class="hero">
  <div>
    <h1>Fly along the world</h1>
    <p>Drones, cameras and accessories from The Drone Man. Pay by UPI QR or cash on delivery.</p>
    <a class="btn" href="#products">Shop Now</a>
  </div>
</div>

<section id="products">
  <div class="wrap"><h2>Our products</h2><p class="sub">Swipe or use the arrows. Tap “Add to cart” to start your order.</p></div>
  <div class="carwrap">
    <button class="arrow l" id="prev" aria-label="Previous">‹</button>
    <div class="track" id="track"></div>
    <button class="arrow r" id="next" aria-label="Next">›</button>
  </div>
</section>

<section class="pay">
  <div class="wrap grid">
    <div>
      <h2>Two easy ways to pay</h2>
      <p><b>UPI QR:</b> scan the code, pay, then place your order. Send the payment screenshot on WhatsApp.</p>
      <p><b>Cash on delivery:</b> pay when your order arrives.</p>
    </div>
    <img src="https://i.ibb.co/hJF88csR/Screenshot-2026-11-17-011800.png" alt="UPI payment QR code">
  </div>
</section>

<footer>
  <p><b>The Drone Man</b> · <a href="mailto:jayeshkmt8@gmail.com">jayeshkmt8@gmail.com</a> · <a href="https://wa.me/917014873917">+91 70148 73917</a></p>
</footer>

<a class="wa" href="https://wa.me/917014873917?text=Hi%20The%20Drone%20Man%2C%20I%20want%20to%20know%20more." target="_blank" rel="noopener" aria-label="Chat on WhatsApp">
  <svg viewBox="0 0 32 32"><path d="M16 3C9 3 3.4 8.6 3.4 15.5c0 2.3.6 4.4 1.7 6.3L3 29l7.4-2c1.8 1 3.8 1.500 5.900 1.500 6.900 0 12.600-5.600 12.600-12.500S22.900 3 16 3zm0 22.800c-1.900 0-3.700-.5-5.300-1.500l-.4-.2-4.400 1.200 1.200-4.300-.3-.4a10.200 10.200 0 0 1-1.600-5.500C5.200 9.500 10 5 16 5s10.800 4.500 10.800 10.100S22 25.800 16 25.800zm5.900-7.600c-.3-.2-1.900-.9-2.200-1-.3-.1-.5-.2-.7.200-.2.300-.8 1-1 1.200-.2.200-.4.200-.7.100-.3-.2-1.400-.5-2.600-1.600-1-.9-1.600-1.900-1.800-2.200-.2-.3 0-.5.100-.7l.5-.6c.1-.2.200-.3.300-.5.100-.2 0-.4 0-.6l-1-2.300c-.2-.6-.5-.5-.7-.5h-.6c-.2 0-.6.100-.9.400-.3.300-1.200 1.200-1.200 2.800s1.200 3.300 1.400 3.500c.2.200 2.400 3.700 5.800 5.100.8.400 1.400.6 1.900.7.8.3 1.500.2 2.100.1.600-.1 1.900-.8 2.200-1.500.3-.8.3-1.400.2-1.500-.1-.2-.3-.3-.6-.4z"/></svg>
</a>

<div class="ov" id="ov"></div>
<aside class="drawer" id="drawer" aria-label="Your cart">
  <div class="dh"><h3>Your cart</h3><button id="closeCart" aria-label="Close cart">×</button></div>
  <div class="db">
    <div id="items"></div>
    <div class="total"><span>Total</span><span id="total">₹0</span></div>
    <form id="orderForm">
      <label for="cname">Your name</label>
      <input type="text" id="cname" required autocomplete="name">
      <label for="cphone">Phone number</label>
      <input type="tel" id="cphone" required pattern="[0-9+ ]{10,15}" autocomplete="tel">
      <label for="caddr">Delivery address</label>
      <textarea id="caddr" rows="3" required></textarea>
      <label>Payment method</label>
      <label class="opt"><input type="radio" name="pay" value="Cash on Delivery" checked> Cash on delivery</label>
      <label class="opt"><input type="radio" name="pay" value="UPI QR Payment"> Pay by UPI QR</label>
      <div id="qrbox">
        <img src="https://i.ibb.co/hJF88csR/Screenshot-2026-11-17-011800.png" alt="UPI payment QR code">
        <small>Scan, pay the total, then tap Send Order.</small>
      </div>
      <div class="msg" id="msg" role="status"></div>
    </form>
  </div>
  <div class="df"><button class="btn" id="send" style="width:100%">Send Order</button></div>
</aside>

<script>
/* ============ EDIT THESE ============ */
const OWNER_EMAIL = "jayeshkmt8@gmail.com";
const EMAILJS = { publicKey:"YOUR_PUBLIC_KEY", serviceId:"YOUR_SERVICE_ID", templateId:"YOUR_TEMPLATE_ID" };
const IMG = [
 "https://i.ibb.co/d4tw3h6t/Screenshot-2026-11-17-002651.png",
 "https://i.ibb.co/hJPCNDZB/Screenshot-2026-11-17-002710.png",
 "https://i.ibb.co/4gVDKVx8/Screenshot-2026-11-17-002732.png",
 "https://i.ibb.co/r2ZCp7Lk/Screenshot-2026-11-17-002803.png",
 "https://i.ibb.co/jPwX3SDm/Screenshot-2026-11-17-002830.png",
 "https://i.ibb.co/FbNRRV8h/Screenshot-2026-11-17-002850.png",
 "https://i.ibb.co/7dd27MbP/Screenshot-2026-11-17-002909.png",
 "https://i.ibb.co/99mwQK6H/Screenshot-2026-11-17-002928.png",
 "https://i.ibb.co/rGMGDd1Q/Screenshot-2026-11-17-002955.png",
 "https://i.ibb.co/Opkq7dKS/Screenshot-2026-11-17-003036.png"
];
/* Change each name and price to match your real products */
const PRODUCTS = IMG.map((img,i)=>({id:i+1,img,name:"Drone Product "+(i+1),price:1999+i*500}));
/* ==================================== */

const $ = s => document.querySelector(s);
const cart = {};
const money = n => "₹" + n.toLocaleString("en-IN");

/* carousel */
$("#track").innerHTML = PRODUCTS.map(p=>`
 <article class="card">
  <img src="${p.img}" alt="${p.name}" loading="lazy">
  <div class="b"><h3>${p.name}</h3><div class="price">${money(p.price)}</div>
  <button class="btn" data-add="${p.id}">Add to cart</button></div>
 </article>`).join("");
const track = $("#track");
const step = () => track.querySelector(".card").offsetWidth + 16;
$("#next").onclick = () => track.scrollBy({left:step(),behavior:"smooth"});
$("#prev").onclick = () => track.scrollBy({left:-step(),behavior:"smooth"});
let paused = false;
["pointerdown","mouseenter","focusin"].forEach(e=>track.addEventListener(e,()=>paused=true));
["mouseleave","focusout"].forEach(e=>track.addEventListener(e,()=>paused=false));
track.addEventListener("touchend",()=>setTimeout(()=>paused=false,4000));
if(!matchMedia("(prefers-reduced-motion:reduce)").matches){
  setInterval(()=>{
    if(paused||$("#drawer").classList.contains("on")) return;
    const end = track.scrollLeft + track.clientWidth >= track.scrollWidth - 4;
    end ? track.scrollTo({left:0,behavior:"smooth"}) : track.scrollBy({left:step(),behavior:"smooth"});
  },3500);
}

/* cart */
function render(){
  const ids = Object.keys(cart);
  $("#cnt").textContent = ids.reduce((a,id)=>a+cart[id],0);
  $("#items").innerHTML = ids.length ? ids.map(id=>{
    const p = PRODUCTS.find(x=>x.id==id);
    return `<div class="item"><img src="${p.img}" alt=""><div class="n">${p.name}<br><b>${money(p.price*cart[id])}</b></div>
    <div class="qty"><button data-dec="${id}" aria-label="Decrease">−</button><span>${cart[id]}</span><button data-inc="${id}" aria-label="Increase">+</button></div></div>`;
  }).join("") : `<p class="empty">Your cart is empty. Add a product to begin.</p>`;
  $("#total").textContent = money(ids.reduce((a,id)=>a+PRODUCTS.find(x=>x.id==id).price*cart[id],0));
}
document.addEventListener("click",e=>{
  const t = e.target;
  if(t.dataset.add){cart[t.dataset.add]=(cart[t.dataset.add]||0)+1;render();openDrawer();}
  if(t.dataset.inc){cart[t.dataset.inc]++;render();}
  if(t.dataset.dec){if(--cart[t.dataset.dec]<=0)delete cart[t.dataset.dec];render();}
});
const openDrawer=()=>{$("#drawer").classList.add("on");$("#ov").classList.add("on")};
const closeDrawer=()=>{$("#drawer").classList.remove("on");$("#ov").classList.remove("on")};
$("#openCart").onclick=openDrawer;$("#closeCart").onclick=closeDrawer;$("#ov").onclick=closeDrawer;
document.addEventListener("keydown",e=>{if(e.key==="Escape")closeDrawer()});
document.querySelectorAll('input[name=pay]').forEach(r=>r.onchange=()=>{
  $("#qrbox").style.display = document.querySelector('input[name=pay]:checked').value.includes("UPI") ? "block":"none";
});

/* send order via EmailJS */
const msg=(t,c)=>{$("#msg").textContent=t;$("#msg").className="msg "+c};
if(window.emailjs && EMAILJS.publicKey!=="YOUR_PUBLIC_KEY") emailjs.init({publicKey:EMAILJS.publicKey});
$("#send").onclick = async () => {
  const f = $("#orderForm");
  if(!Object.keys(cart).length) return msg("Add at least one product first.","err");
  if(!f.reportValidity()) return;
  if(EMAILJS.publicKey==="YOUR_PUBLIC_KEY") return msg("Email is not set up yet. Add your EmailJS keys in the script.","err");
  const lines = Object.keys(cart).map(id=>{const p=PRODUCTS.find(x=>x.id==id);return `${p.name} × ${cart[id]} = ${money(p.price*cart[id])}`}).join("\n");
  const params = {
    to_email: OWNER_EMAIL,
    customer_name: $("#cname").value.trim(),
    customer_phone: $("#cphone").value.trim(),
    customer_address: $("#caddr").value.trim(),
    payment_method: document.querySelector('input[name=pay]:checked').value,
    order_items: lines,
    order_total: $("#total").textContent
  };
  const btn=$("#send"); btn.disabled=true; btn.textContent="Sending…";
  try{
    await emailjs.send(EMAILJS.serviceId,EMAILJS.templateId,params);
    msg("Order sent. We will contact you shortly on "+params.customer_phone+".","ok");
    Object.keys(cart).forEach(k=>delete cart[k]); render(); f.reset(); $("#qrbox").style.display="none";
  }catch(err){
    msg("Could not send the order. Please try again or message us on WhatsApp.","err");
  }
  btn.disabled=false; btn.textContent="Send Order";
};
render();
</script>
</body>
</html>
