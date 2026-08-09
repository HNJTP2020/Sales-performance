<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>Toppen KPI Dashboard</title>

<style>
body{
font-family:Segoe UI,Arial,sans-serif;
background:#f4f6f9;
margin:20px;
color:#333;
}

h1{
text-align:center;
color:#003366;
}

.card{
background:white;
padding:20px;
margin-bottom:20px;
border-radius:15px;
box-shadow:0 3px 12px rgba(0,0,0,.08);
}

.kpi{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
gap:15px;
}

.kpi-box{
padding:15px;
border-radius:12px;
color:white;
font-weight:bold;
text-align:center;
}

.sales{background:#2563eb;}
.pc{background:#16a34a;}
.tech{background:#f97316;}
.tm{background:#7c3aed;}
.norton{background:#facc15;color:black;}
.belkin{background:#0891b2;}

input,select{
padding:10px;
margin:5px;
border-radius:8px;
border:1px solid #ccc;
}

button{
padding:10px 15px;
border:none;
border-radius:8px;
cursor:pointer;
background:#2563eb;
color:white;
}

button:hover{
opacity:.9;
}

table{
width:100%;
border-collapse:collapse;
}

th{
background:#003366;
color:white;
}

th,td{
padding:10px;
border:1px solid #ddd;
text-align:center;
}

.rank1{
background:#FFD700;
font-weight:bold;
}

.rank2{
background:#C0C0C0;
font-weight:bold;
}

.rank3{
background:#CD7F32;
color:white;
font-weight:bold;
}

.podium{
display:flex;
justify-content:center;
align-items:flex-end;
gap:20px;
text-align:center;
}

.gold{
background:#FFD700;
padding:25px;
border-radius:10px;
}

.silver{
background:#C0C0C0;
padding:18px;
border-radius:10px;
}

.bronze{
background:#CD7F32;
color:white;
padding:15px;
border-radius:10px;
}

.champion{
text-align:center;
font-size:24px;
color:#d97706;
font-weight:bold;
}
</style>
</head>

<body>

<h1>🏆 TOPPEN PERFORMANCE DASHBOARD</h1>

<div class="card">
<div id="championCard" class="champion">
No Data
</div>
</div>

<div class="card">
<div id="podium" class="podium"></div>
</div>

<div class="card">
<div class="kpi">

<div class="kpi-box sales">
Sales<br>
<span id="totalSales">RM0</span>
</div>

<div class="kpi-box pc">
Product Care<br>
<span id="totalPC">RM0</span>
</div>

<div class="kpi-box tech">
TechCrew<br>
<span id="totalTech">RM0</span>
</div>

<div class="kpi-box tm">
Trend Micro<br>
<span id="totalTM">RM0</span>
</div>

<div class="kpi-box norton">
Norton<br>
<span id="totalNorton">RM0</span>
</div>

<div class="kpi-box belkin">
Belkin<br>
<span id="totalBelkin">RM0</span>
</div>

</div>
</div>

<div class="card">

<h2>➕ Daily Entry</h2>

<input type="date" id="date">

<select id="staff">
<option>Queenie</option>
<option>Faried</option>
<option>Liyana</option>
<option>Aniq</option>
<option>Syahrul</option>
</select>

<input type="number" id="sales" placeholder="Sales">
<input type="number" id="pc" placeholder="Product Care">
<input type="number" id="tech" placeholder="TechCrew">
<input type="number" id="tm" placeholder="Trend Micro">
<input type="number" id="norton" placeholder="Norton">
<input type="number" id="belkin" placeholder="Belkin">

<button onclick="saveRecord()" id="saveBtn">
Save Record
</button>

</div>

<div class="card">

<h2>📅 Filters</h2>

<select id="monthFilter" onchange="render()">
<option value="all">All Months</option>
</select>

<select id="staffFilter" onchange="render()">
<option value="all">All Staff</option>
<option>Queenie</option>
<option>Faried</option>
<option>Liyana</option>
<option>Aniq</option>
<option>Syahrul</option>
</select>

</div>

<div class="card">

<h2>🥇 Sales Ranking</h2>

<table id="rankingTable">

<thead>
<tr>
<th>Rank</th>
<th>Staff</th>
<th>Sales</th>
</tr>
</thead>

<tbody></tbody>

</table>

</div>

<div class="card">

<h2>📋 Daily Records</h2>

<table id="historyTable">

<thead>
<tr>
<th>Date</th>
<th>Staff</th>
<th>Sales</th>
<th>PC</th>
<th>Tech</th>
<th>TM</th>
<th>Norton</th>
<th>Belkin</th>
<th>Action</th>
</tr>
</thead>

<tbody></tbody>

</table>

</div>

<script>

let editIndex = -1;

let records =
JSON.parse(localStorage.getItem("toppenRecords")) || [];

function saveStorage(){
localStorage.setItem(
"toppenRecords",
JSON.stringify(records)
);
}

function saveRecord(){

let date =
document.getElementById("date").value;

if(!date){
alert("Please select date");
return;
}

let record = {

date:date,
month:date.substring(0,7),

staff:
document.getElementById("staff").value,

sales:Number(document.getElementById("sales").value||0),

pc:Number(document.getElementById("pc").value||0),

tech:Number(document.getElementById("tech").value||0),

tm:Number(document.getElementById("tm").value||0),

norton:Number(document.getElementById("norton").value||0),

belkin:Number(document.getElementById("belkin").value||0)

};

if(editIndex === -1){
records.push(record);
}else{
records[editIndex] = record;
editIndex = -1;
document.getElementById("saveBtn").innerText =
"Save Record";
}

saveStorage();
populateMonths();
clearForm();
render();

}

function editRecord(index){

let r = records[index];

document.getElementById("date").value=r.date;
document.getElementById("staff").value=r.staff;
document.getElementById("sales").value=r.sales;
document.getElementById("pc").value=r.pc;
document.getElementById("tech").value=r.tech;
document.getElementById("tm").value=r.tm;
document.getElementById("norton").value=r.norton;
document.getElementById("belkin").value=r.belkin;

editIndex=index;

document.getElementById("saveBtn").innerText =
"Update Record";

window.scrollTo({
top:0,
behavior:"smooth"
});

}

function deleteRecord(index){

if(confirm("Delete Record?")){

records.splice(index,1);

saveStorage();
populateMonths();
render();

}

}

function clearForm(){

document.getElementById("sales").value="";
document.getElementById("pc").value="";
document.getElementById("tech").value="";
document.getElementById("tm").value="";
document.getElementById("norton").value="";
document.getElementById("belkin").value="";

}

function populateMonths(){

let months=[
...new Set(records.map(r=>r.month))
];

let select =
document.getElementById("monthFilter");

select.innerHTML =
'<option value="all">All Months</option>';

months.forEach(m=>{

select.innerHTML +=
`<option value="${m}">
${m}
</option>`;

});

}

function render(){

let month =
document.getElementById("monthFilter").value;

let staff =
document.getElementById("staffFilter").value;

let filtered =
records.filter(r=>

(month==="all" || r.month===month)
&&
(staff==="all" || r.staff===staff)

);

renderHistory(filtered);
renderRanking(filtered);
renderKPI(filtered);

}

function renderHistory(data){

let body =
document.querySelector(
"#historyTable tbody"
);

body.innerHTML="";

data.forEach((r,index)=>{

body.innerHTML +=

`
<tr>

<td>${r.date}</td>
<td>${r.staff}</td>

<td>${r.sales}</td>

<td>${r.pc}</td>

<td>${r.tech}</td>

<td>${r.tm}</td>

<td>${r.norton}</td>

<td>${r.belkin}</td>

<td>
<button onclick="editRecord(${index})">
✏️
</button>

<button onclick="deleteRecord(${index})">
🗑️
</button>
</td>

</tr>
`;

});

}

function renderRanking(data){

let totals={};

data.forEach(r=>{

if(!totals[r.staff])
totals[r.staff]=0;

totals[r.staff]+=r.sales;

});

let ranking =
Object.entries(totals)
.sort((a,b)=>b[1]-a[1]);

let body =
document.querySelector(
"#rankingTable tbody"
);

body.innerHTML="";

ranking.forEach((r,i)=>{

let cls="";

if(i===0) cls="rank1";
if(i===1) cls="rank2";
if(i===2) cls="rank3";

body.innerHTML +=

`
<tr class="${cls}">
<td>${i+1}</td>
<td>${r[0]}</td>
<td>RM ${r[1].toLocaleString()}</td>
</tr>
`;

});

if(ranking.length>0){

document.getElementById(
"championCard"
).innerHTML=

`👑 SALES CHAMPION<br>
${ranking[0][0]}<br>
RM ${ranking[0][1].toLocaleString()}`;

}

if(ranking.length>=3){

document.getElementById("podium").innerHTML=

`
<div class="silver">
🥈<br>${ranking[1][0]}
</div>

<div class="gold">
👑<br>${ranking[0][0]}
</div>

<div class="bronze">
🥉<br>${ranking[2][0]}
</div>
`;

}

}

function renderKPI(data){

let sales=0;
let pc=0;
let tech=0;
let tm=0;
let norton=0;
let belkin=0;

data.forEach(r=>{

sales+=r.sales;
pc+=r.pc;
tech+=r.tech;
tm+=r.tm;
norton+=r.norton;
belkin+=r.belkin;

});

document.getElementById("totalSales").innerText =
"RM "+sales.toLocaleString();

document.getElementById("totalPC").innerText =
"RM "+pc.toLocaleString();

document.getElementById("totalTech").innerText =
"RM "+tech.toLocaleString();

document.getElementById("totalTM").innerText =
"RM "+tm.toLocaleString();

document.getElementById("totalNorton").innerText =
"RM "+norton.toLocaleString();

document.getElementById("totalBelkin").innerText =
"RM "+belkin.toLocaleString();

}

populateMonths();
render();

</script>

</body>
</html>
