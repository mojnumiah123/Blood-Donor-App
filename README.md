<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>রক্তদাতা অ্যাপ — মজনু মিয়া</title>
<style>
  :root{
    --green:#2e7d32; --green-d:#1b5e20; --bg:#f1f8e9; --panel:#ffffff;
  }
  *{box-sizing:border-box}
  body{font-family:Arial,Helvetica,sans-serif;background:var(--bg);margin:0;color:#1b5e20;}
  header{background:var(--green);color:#fff;text-align:center;padding:18px 12px}
  .dev{display:flex;gap:12px;align-items:center;justify-content:center;flex-wrap:wrap}
  .dev img{width:110px;height:110px;border-radius:50%;border:3px solid #fff;object-fit:cover}
  .dev .who{line-height:1.35}
  .dev .who h1{margin:0;font-size:22px}
  .dev .who small{opacity:.9}
  .top-actions{margin-top:8px}
  .btn{background:var(--green);color:#fff;border:none;padding:10px 16px;border-radius:10px;cursor:pointer}
  .btn:hover{background:var(--green-d)}
  .container{max-width:950px;margin:14px auto;padding:0 12px}
  .nav{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin:8px 0 14px}
  .nav .tab{background:#a5d6a7;color:#08310d;padding:10px 14px;border:none;border-radius:10px;cursor:pointer}
  .nav .tab.active{background:var(--green);color:#fff}
  .panel{display:none;background:var(--panel);border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,.12);padding:16px}
  .panel.show{display:block}
  h2{margin:5px 0 12px}
  label{font-weight:600;margin-top:8px;display:block}
  .row{display:grid;grid-template-columns:1fr 1fr;gap:10px}
  .row-3{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
  @media(max-width:720px){.row,.row-3{grid-template-columns:1fr}}
  .form-control, select, input[type="file"]{width:100%;padding:10px;border:1.5px solid var(--green);border-radius:8px;margin-top:6px;background:#fff}
  .note{font-size:12px;opacity:.8;margin:4px 0 10px}
  .actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
  .card{display:flex;gap:12px;align-items:flex-start;background:#fff;border-radius:12px;box-shadow:0 2px 8px rgba(0,0,0,.12);padding:12px;margin:10px 0}
  .avatar{width:60px;height:60px;border-radius:50%;object-fit:cover;border:2px solid var(--green)}
  .grow{flex:1}
  .pill{display:inline-block;background:#e8f5e9;border:1px solid #c8e6c9;border-radius:999px;padding:3px 8px;margin-right:6px;font-size:12px}
  .call{background:var(--green);color:#fff;text-decoration:none;padding:7px 12px;border-radius:8px;display:inline-block;margin-top:6px}
  .muted{opacity:.7}
  .hr{height:1px;background:#dfe7de;margin:14px 0}
  .about{background:#e8f5e9;border:1px solid #c8e6c9;border-radius:10px;padding:12px}
</style>
</head>
<body>

<header>
  <div class="dev">
    <img src="https://i.postimg.cc/gcBqJVLC/IMG-20241228-140632.jpg" alt="মজনু মিয়া">
    <div class="who">
      <h1>মজনু  মিয়া (২০০২)</h1>
      <small>উদ্যোক্তা, বাংলাদেশ রক্তদাতা তথ্যভান্ডার</small><br/>
      <button class="btn" id="toggleIntro">অ্যাপ নির্মাতার পরিচয়</button>
    </div>
  </div>
  <div id="introBox" class="about" style="display:none;max-width:950px;margin:10px auto 0;">
    <strong>পরিচয়:</strong><br/>
    পিতা: মৃত চেরাগ আলী · মাতা: হাজরা বেগম · গ্রাম: বেরাজেলি · ডাকঘর: গৌরারং · উপজেলা: সুনামগঞ্জ সদর ·
    জেলা: সুনামগঞ্জ · বিভাগ: সিলেট · জাতীয়তা: বাংলাদেশী।<br/>
    <span class="muted">এই অ্যাপটি মানুষের জীবন রক্ষায় দ্রুত রক্তদাতা খুঁজে পেতে সাহায্য করবে।</span>
  </div>
</header>

<div class="container">
  <div class="nav">
    <button class="tab active" data-tab="search">রক্তদাতা খুঁজুন</button>
    <button class="tab" data-tab="add">রক্তদাতা যোগ করুন</button>
    <button class="tab" data-tab="profiles">রক্তদাতার প্রোফাইল</button>
  </div>

  <!-- Search -->
  <section id="search" class="panel show">
    <h2>রক্তদাতা খুঁজুন</h2>
    <div class="row">
      <div>
        <label for="searchDistrict">জেলা নির্বাচন করুন</label>
        <select id="searchDistrict" class="form-control"></select>
      </div>
      <div>
        <label for="searchBlood">ব্লাড গ্রুপ</label>
        <select id="searchBlood" class="form-control">
          <option value="">সকল</option>
          <option>A+</option><option>A-</option>
          <option>B+</option><option>B-</option>
          <option>O+</option><option>O-</option>
          <option>AB+</option><option>AB-</option>
        </select>
      </div>
    </div>
    <div class="actions">
      <button class="btn" id="btnSearch">খুঁজুন</button>
      <button class="btn" id="btnClearSearch">ফলাফল পরিষ্কার</button>
    </div>
    <div id="searchResults"></div>
  </section>

  <!-- Add -->
  <section id="add" class="panel">
    <h2>রক্তদাতা যোগ করুন</h2>
    <div class="row">
      <div>
        <label for="name">নাম</label>
        <input id="name" class="form-control" placeholder="নাম লিখুন">
      </div>
      <div>
        <label for="phone">মোবাইল নাম্বার</label>
        <input id="phone" class="form-control" placeholder="০১XXXXXXXXX">
      </div>
      <div>
        <label for="bloodGroup">ব্লাড গ্রুপ</label>
        <select id="bloodGroup" class="form-control">
          <option value="">বাছাই করুন</option>
          <option>A+</option><option>A-</option>
          <option>B+</option><option>B-</option>
          <option>O+</option><option>O-</option>
          <option>AB+</option><option>AB-</option>
        </select>
      </div>
      <div>
        <label for="district">জেলা</label>
        <select id="district" class="form-control"></select>
      </div>
      <div>
        <label for="upazila">উপজেলা/থানা (ঐচ্ছিক)</label>
        <input id="upazila" class="form-control" placeholder="যেমন: জামালগঞ্জ">
      </div>
      <div>
        <label for="address">ঠিকানা</label>
        <input id="address" class="form-control" placeholder="গ্রাম/মহল্লা, রোড ইত্যাদি">
      </div>
      <div>
        <label for="age">বয়স (বছর)</label>
        <input type="number" id="age" class="form-control" min="16" max="70">
      </div>
      <div>
        <label for="weight">ওজন (কেজি)</label>
        <input type="number" id="weight" class="form-control" min="35" max="200">
      </div>
      <div>
        <label for="donations">কতবার রক্ত দিয়েছেন</label>
        <input type="number" id="donations" class="form-control" value="0" min="0">
      </div>
      <div>
        <label for="photo">প্রোফাইল ছবি</label>
        <input type="file" id="photo" class="form-control" accept="image/*">
        <div class="note">২ এমবি-এর নিচে JPG/PNG দিন। না দিলে ডিফল্ট ছবি থাকবে।</div>
      </div>
    </div>
    <div class="actions">
      <button class="btn" id="btnSave">সেভ করুন</button>
      <button class="btn" id="btnResetForm">ফর্ম রিসেট</button>
    </div>
  </section>

  <!-- Profiles -->
  <section id="profiles" class="panel">
    <h2>রক্তদাতার প্রোফাইল</h2>
    <div class="row">
      <div>
        <label for="profileSearchDistrict">জেলা লিখুন/নির্বাচন করুন</label>
        <input id="profileSearchDistrict" class="form-control" list="districtList" placeholder="জেলা টাইপ করুন">
        <datalist id="districtList"></datalist>
      </div>
      <div>
        <label for="profileSearchBlood">ব্লাড গ্রুপ</label>
        <select id="profileSearchBlood" class="form-control">
          <option value="">সকল</option>
          <option>A+</option><option>A-</option>
          <option>B+</option><option>B-</option>
          <option>O+</option><option>O-</option>
          <option>AB+</option><option>AB-</option>
        </select>
      </div>
    </div>
    <div class="actions">
      <button class="btn" id="btnFilterProfiles">ফিল্টার</button>
      <button class="btn" id="btnClearProfiles">সব দেখাও</button>
    </div>
    <div id="profileResults"></div>
  </section>
</div>

<script>
  // ---- ৬৪ জেলা (অফিশিয়াল) ----
  const districts = [
    // ঢাকা বিভাগ (১৩)
    "ঢাকা","ফরিদপুর","গাজীপুর","গোপালগঞ্জ","কিশোরগঞ্জ","মাদারীপুর","মানিকগঞ্জ","মুন্সীগঞ্জ","নারায়ণগঞ্জ","নরসিংদী","রাজবাড়ী","শরীয়তপুর","টাঙ্গাইল",
    // চট্টগ্রাম বিভাগ (১১)
    "চট্টগ্রাম","কক্সবাজার","কুমিল্লা","ফেনী","ব্রাহ্মণবাড়িয়া","রাঙ্গামাটি","বান্দরবান","খাগড়াছড়ি","লক্ষ্মীপুর","নোয়াখালী","চাঁদপুর",
    // বরিশাল বিভাগ (৬)
    "বরিশাল","বরগুনা","ভোলা","ঝালকাঠি","পটুয়াখালী","পিরোজপুর",
    // খুলনা বিভাগ (১০)
    "খুলনা","বাগেরহাট","সাতক্ষীরা","যশোর","নড়াইল","মাগুরা","ঝিনাইদহ","কুষ্টিয়া","চুয়াডাঙ্গা","মেহেরপুর",
    // রাজশাহী বিভাগ (৮)
    "রাজশাহী","চাঁপাইনবাবগঞ্জ","নওগাঁ","নাটোর","পাবনা","সিরাজগঞ্জ","বগুড়া","জয়পুরহাট",
    // রংপুর বিভাগ (৮)
    "রংপুর","দিনাজপুর","কুড়িগ্রাম","গাইবান্ধা","লালমনিরহাট","নীলফামারী","পঞ্চগড়","ঠাকুরগাঁও",
    // ময়মনসিংহ বিভাগ (৪)
    "ময়মনসিংহ","জামালপুর","নেত্রকোনা","শেরপুর",
    // সিলেট বিভাগ (৪)
    "সিলেট","মৌলভীবাজার","হবিগঞ্জ","সুনামগঞ্জ"
  ];

  // ---------- Utilities ----------
  const qs = id => document.getElementById(id);
  function getDonors(){ return JSON.parse(localStorage.getItem('donors')||'[]'); }
  function saveDonors(list){ localStorage.setItem('donors', JSON.stringify(list)); }
  function clear(el){ el.innerHTML=''; }

  function populateDistrictSelects(){
    const selects = [qs('searchDistrict'), qs('district')];
    selects.forEach(select=>{
      select.innerHTML = '<option value="">জেলা নির্বাচন করুন</option>';
      districts.forEach(d=>{
        const opt=document.createElement('option'); opt.value=d; opt.textContent=d; select.appendChild(opt);
      });
    });
    // datalist for profiles
    const dl = qs('districtList'); clear(dl);
    districts.forEach(d=>{
      const o=document.createElement('option'); o.value=d; dl.appendChild(o);
    });
  }

  function showTab(id){
    document.querySelectorAll('.tab').forEach(b=>b.classList.remove('active'));
    document.querySelector(`.tab[data-tab="${id}"]`).classList.add('active');
    document.querySelectorAll('.panel').forEach(p=>p.classList.remove('show'));
    qs(id).classList.add('show');
  }

  // ---------- Image to Base64 ----------
  function fileToBase64(file){
    return new Promise((resolve,reject)=>{
      const reader=new FileReader();
      reader.onload=()=>resolve(reader.result);
      reader.onerror=()=>reject(new Error('ছবি লোডে সমস্যা'));
      reader.readAsDataURL(file);
    });
  }

  // ---------- Save Donor ----------
  async function handleSave(){
    const name = qs('name').value.trim();
    const phone = qs('phone').value.trim();
    const bloodGroup = qs('bloodGroup').value;
    const district = qs('district').value;
    const upazila = qs('upazila').value.trim();
    const address = qs('address').value.trim();
    const age = qs('age').value.trim();
    const weight = qs('weight').value.trim();
    const donations = qs('donations').value.trim();
    const photoInput = qs('photo');

    if(!name || !phone || !bloodGroup || !district){
      alert('অনুগ্রহ করে নাম, মোবাইল, ব্লাড গ্রুপ ও জেলা পূরণ করুন।');
      return;
    }

    let photoData = "https://i.postimg.cc/fTzxd2D7/default-profile.png";
    if(photoInput.files && photoInput.files[0]){
      const f = photoInput.files[0];
      if(f.size>2*1024*1024){ alert('ছবির আকার ২ এমবি-এর বেশি হতে পারবে না।'); return; }
      try{ photoData = await fileToBase64(f); }catch(e){ alert('ছবি লোড করা যায়নি!'); }
    }

    const donors = getDonors();
    donors.push({name,phone,bloodGroup,district,upazila,address,age,weight,donations,photo:photoData});
    saveDonors(donors);
    alert('রক্তদাতা সেভ হয়েছে!');
    // reset
    ['name','phone','bloodGroup','district','upazila','address','age','weight','donations','photo'].forEach(id=>{
      const el=qs(id); if(el.tagName==='SELECT') el.value=''; else el.value='';
    });
  }

  // ---------- Render Cards ----------
  function cardHTML(d){
    const locLine = [d.address||'', d.upazila||'', d.district||''].filter(Boolean).join(', ');
    return `
    <div class="card">
      <img class="avatar" src="${d.photo}" alt="photo">
      <div class="grow">
        <strong>${d.name}</strong>
        <div class="muted">${locLine}</div>
        <div>
          <span class="pill">গ্রুপ: ${d.bloodGroup}</span>
          <span class="pill">বয়স: ${d.age||'-'} বছর</span>
          <span class="pill">ওজন: ${d.weight||'-'} কেজি</span>
          <span class="pill">রক্তদান: ${d.donations||0} বার</span>
        </div>
        <a class="call" href="tel:${d.phone}">কল করুন: ${d.phone}</a>
      </div>
    </div>`;
  }

  // ---------- Search ----------
  function runSearch(){
    const dist = qs('searchDistrict').value;
    const bg = qs('searchBlood').value;
    const out = qs('searchResults'); clear(out);

    const donors = getDonors().filter(d =>
      (dist==='' || d.district===dist) &&
      (bg==='' || d.bloodGroup===bg)
    );

    if(donors.length===0){ out.innerHTML = '<div class="muted">কোনো রক্তদাতা পাওয়া যায়নি।</div>'; return; }
    out.innerHTML = donors.map(cardHTML).join('');
  }

  // ---------- Profiles (All + Filter) ----------
  function renderProfiles(list){
    const out = qs('profileResults'); clear(out);
    if(list.length===0){ out.innerHTML='<div class="muted">ডাটা নেই</div>'; return; }
    out.innerHTML = list.map(cardHTML).join('');
  }

  function filterProfiles(){
    const qDist = qs('profileSearchDistrict').value.trim();
    const qBG = qs('profileSearchBlood').value;
    let donors = getDonors();
    if(qDist) donors = donors.filter(d => d.district.includes(qDist));
    if(qBG) donors = donors.filter(d => d.bloodGroup===qBG);
    renderProfiles(donors);
  }

  function showAllProfiles(){
    renderProfiles(getDonors());
  }

  // ---------- Events & Init ----------
  document.querySelectorAll('.tab').forEach(btn=>{
    btn.addEventListener('click', ()=>showTab(btn.dataset.tab));
  });

  qs('btnSearch').addEventListener('click', runSearch);
  qs('btnClearSearch').addEventListener('click', ()=>{qs('searchResults').innerHTML='';});

  qs('btnSave').addEventListener('click', handleSave);
  qs('btnResetForm').addEventListener('click', ()=>{
    document.querySelectorAll('#add .form-control').forEach(el=>{ if(el.tagName==='SELECT') el.value=''; else el.value=''; });
  });

  qs('btnFilterProfiles').addEventListener('click', filterProfiles);
  qs('btnClearProfiles').addEventListener('click', showAllProfiles);

  qs('toggleIntro').addEventListener('click', ()=>{
    const box = qs('introBox'); box.style.display = (box.style.display==='none' || box.style.display==='') ? 'block':'none';
  });

  window.addEventListener('load', ()=>{
    populateDistrictSelects();
    showAllProfiles(); // প্রথমে সব দেখাই
  });
</script>
</body>
</html# Blood-Donor-App
simple web app to connect blood donors and recipients.
