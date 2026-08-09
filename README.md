<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Toppen KPI Dashboard</title>

<style>
body{
font-family:Arial,sans-serif;
background:#f4f6f9;
margin:20px;
}

.card{
background:white;
padding:20px;
border-radius:12px;
margin-bottom:20px;
box-shadow:0 2px 10px rgba(0,0,0,.1);
}

h1{
text-align:center;
color:#003366;
}

.kpi{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
gap:15px;
}

.box{
padding:15px;
border-radius:10px;
color:white;
text-align:center;
font-weight:bold;
}

.sales{background:#2563eb;}
.pc{background:#16a34a;}
.tech{background:#f97316;}
.tm{background:#7c3aed;}
.norton{background:#facc15;color:black;}
.belkin{background:#0891b2;}

input,select{
padding:8px;
margin:5px;
}

table{
width:100%;
border-collapse:collapse;
}

th,td{
border:1px solid #ddd;
padding:10px;
text-align:center;
}

th{
background:#003366;
color:white;
}

.rank1{background:#FFD700;}
.rank2{background:#C0C0C0;}
.rank3{
background:#CD7F32;
color:white;
}

button{
padding:8px 12px;
background:#2563eb;
color:white;
border:none;
border-radius:5px;
cursor:pointer;
}
</style>

</head>
<body>

<h1>🏆 TOPPEN KPI DASHBOARD</h1>

<div class="card">
<h2>👑 Sales Champion</h2>
<div id="champion">No Data</div>
</div>

<div class="card">
<h2>🎯 Monthly Target</h2>

<label>Queenie</label>
<input type="number" value="150000"><br>

<label>Faried</label>
<input type="number" value="176318"><br>

<label>Liyana</label>
<input type="number" value="160000"><br>

<label>Aniq</label>
<input type="number" value="160000"><br>

<label>Syahrul</label>
<input type="number" value="80000">

</div>

<div class="card">

<div class="kpi">

<div class="box sales">
Sales<br>
RM191,808
</div>

<div class="box pc">
Product Care<br>
RM18,600
</div>

<div class="box tech">
TechCrew<br>
RM4,850
</div>

<div class="box tm">
Trend Micro<br>
RM3,280
</div>

<div class="box norton">
Norton<br>
RM2,450
</div>

<div class="box belkin">
Belkin<br>
RM5,120
</div>

</div>

</div>

<div class="card">
<h2>➕ Daily Entry</h2>

<input type="date">

<select>
<option>Queenie</option>
<option>Faried</option>
<option>Liyana</option>
<option>Aniq</option>
<option>Syahrul</option>
</select>

<input type="number" placeholder="Sales">
<input type="number" placeholder="Product Care">
<input type="number" placeholder="TechCrew">
<input type="number" placeholder="Trend Micro">
<input type="number" placeholder="Norton">
<input type="number" placeholder="Belkin">

<button>Save</button>

</div>

<div class="card">

<h2>📅 Filter</h2>

<select>
<option>All Month</option>
<option>2026-08</option>
<option>2026-09</option>
</select>

<select>
<option>All Staff</option>
<option>Queenie</option>
<option>Faried</option>
<option>Liyana</option>
</select>

</div>

<div class="card">

<h2>🥇 Sales Ranking</h2>

<table>

<tr>
<th>Rank</th>
<th>Staff</th>
<th>Sales</th>
<th>Achievement</th>
</tr>

<tr class="rank1">
<td>1</td>
<td>Queenie</td>
<td>RM54,749</td>
<td>36.5%</td>
</tr>

<tr class="rank2">
<td>2</td>
<td>Faried</td>
<td>RM48,570</td>
<td>27.5%</td>
</tr>

<tr class="rank3">
<td>3</td>
<td>Liyana</td>
<td>RM46,419</td>
<td>29.0%</td>
</tr>

</table>

</div>

<div class="card">

<h2>📋 Daily Records</h2>

<table>

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

<tr>
<td>2026-08-09</td>
<td>Queenie</td>
<td>5000</td>
<td>500</td>
<td>199</td>
<td>99</td>
<td>89</td>
<td>120</td>
<td>
<button>✏️</button>
<button>🗑️</button>
</td>
</tr>

</table>

</div>

</body>
</html>
