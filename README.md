<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أداة إنشاء الاختبارات</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pizzip/3.1.5/pizzip.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/docxtemplater/3.37.0/docxtemplater.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>

<style>
body { font-family: Arial; background:#f5f5f5; padding:20px }
.box { background:#fff; padding:15px; border-radius:8px; margin-bottom:15px }
textarea, input { width:100%; padding:8px; margin-top:5px }
button { width:100%; padding:12px; font-size:16px; background:#0a7cff; color:#fff; border:none; border-radius:8px }
</style>
</head>

<body>

<h2>📘 أداة إنشاء الاختبارات</h2>

<div class="box">
<label>اسم الطالب</label>
<input id="student">

<label>رقم الجلوس</label>
<input id="seat">

<label>اسم المعلم</label>
<input id="teacher">

<label>عدد النماذج</label>
<input id="modelsCount" type="number" value="3">
</div>

<div class="box">
<h3>📚 بنك Grammar (سؤال | إجابة)</h3>
<textarea id="grammarBank" rows="8"></textarea>

<h3>📚 بنك Reading (جملة | T/F)</h3>
<textarea id="readingBank" rows="6"></textarea>

<button onclick="saveBanks()">💾 حفظ بنك الأسئلة</button>
</div>

<button onclick="generate()">📄 إنشاء الاختبارات</button>

<script>
function shuffle(a){return a.sort(()=>Math.random()-0.5);}

function saveBanks(){
localStorage.setItem("grammar",grammarBank.value);
localStorage.setItem("reading",readingBank.value);
alert("تم الحفظ ✅");
}

window.onload=()=>{
grammarBank.value=localStorage.getItem("grammar")||"";
readingBank.value=localStorage.getItem("reading")||"";
};

function prepare(bank,count){
return shuffle(bank).slice(0,count).map(x=>{
let p=x.split("|");
return{q:p[0],a:p[1]||""};
});
}

async function generate(){
const template=await fetch("template.docx").then(r=>r.arrayBuffer());

const models=parseInt(modelsCount.value);

const grammarRaw=grammarBank.value.split("\n").filter(x=>x);
const readingRaw=readingBank.value.split("\n").filter(x=>x);

for(let i=0;i<models;i++){
const zip=new PizZip(template);
const doc=new docxtemplater(zip);

const g=prepare(grammarRaw,9);
const r=prepare(readingRaw,5);

doc.render({
student_name:student.value,
seat_number:seat.value,
teacher_name:teacher.value,
model_name:"نموذج "+String.fromCharCode(65+i),

grammar_q1:g[0].q,grammar_q2:g[1].q,grammar_q3:g[2].q,
grammar_q4:g[3].q,grammar_q5:g[4].q,grammar_q6:g[5].q,
grammar_q7:g[6].q,grammar_q8:g[7].q,grammar_q9:g[8].q,

read_1:r[0].q,read_2:r[1].q,read_3:r[2].q,
read_4:r[3].q,read_5:r[4].q
});

saveAs(
doc.getZip().generate({type:"blob",
mimeType:"application/vnd.openxmlformats-officedocument.wordprocessingml.document"}),
"اختبار_"+String.fromCharCode(65+i)+".docx"
);
}
}
</script>

</body>
</html>
