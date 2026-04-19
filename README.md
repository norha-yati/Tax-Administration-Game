# Tax-Administration-Game
<!doctype html>
<html lang="en" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Malaysia Tax Quiz</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="https://cdn.jsdelivr.net/npm/lucide@0.263.0/dist/umd/lucide.min.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&amp;family=DM+Mono:wght@400;500&amp;display=swap" rel="stylesheet">
  <style>
* { font-family: 'Plus Jakarta Sans', sans-serif; }
.mono { font-family: 'DM Mono', monospace; }
@keyframes slideUp { from { opacity:0; transform:translateY(30px); } to { opacity:1; transform:translateY(0); } }
@keyframes pulse-glow { 0%,100% { box-shadow: 0 0 20px rgba(var(--accent-rgb),0.2); } 50% { box-shadow: 0 0 40px rgba(var(--accent-rgb),0.4); } }
@keyframes confetti-fall { 0% { transform: translateY(-10px) rotate(0deg); opacity:1; } 100% { transform: translateY(60px) rotate(360deg); opacity:0; } }
.slide-up { animation: slideUp 0.5s ease forwards; }
.delay-1 { animation-delay: 0.1s; opacity:0; }
.delay-2 { animation-delay: 0.2s; opacity:0; }
.delay-3 { animation-delay: 0.3s; opacity:0; }
.delay-4 { animation-delay: 0.3s; opacity:0; }
.option-btn { transition: all 0.25s ease; }
.option-btn:hover:not(:disabled) { transform: translateY(-2px); }
.option-btn:active:not(:disabled) { transform: translateY(0); }
.progress-fill { transition: width 0.6s cubic-bezier(0.4,0,0.2,1); }
.tab-active { border-bottom: 3px solid; }
.confetti-piece { position:absolute; width:8px; height:8px; border-radius:2px; animation: confetti-fall 1.5s ease forwards; }
</style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div id="app" class="h-full w-full overflow-auto" style="background:#0a0f1e;"><!-- HOME SCREEN -->
   <div id="screen-home" class="h-full flex flex-col items-center justify-center p-6 text-center">
    <div class="slide-up max-w-lg w-full">
     <div class="mono text-xs tracking-widest mb-4" style="color:#64748b;">
      INTERACTIVE LEARNING
     </div>
     <h1 id="el-title" class="text-4xl md:text-5xl font-extrabold leading-tight mb-3" style="color:#e2e8f0;">Malaysia Tax<br>
      Administration</h1>
     <p id="el-subtitle" class="text-lg mb-10" style="color:#94a3b8;">Master IRB functions, SAS, assessments, appeals &amp; more</p>
     <div class="grid grid-cols-1 gap-3 mb-8"><button onclick="startGame('quiz')" class="option-btn flex items-center gap-4 p-5 rounded-2xl text-left" style="background:#111827; border:1px solid #1e293b;">
       <div class="w-12 h-12 rounded-xl flex items-center justify-center flex-shrink-0" style="background:#1e3a5f;"><i data-lucide="help-circle" style="color:#38bdf8; width:24px; height:24px;"></i>
       </div>
       <div>
        <div class="font-bold text-base" style="color:#e2e8f0;">
         Quiz Challenge
        </div>
        <div class="text-sm" style="color:#64748b;">
         40 questions across all topics
        </div>
       </div><i data-lucide="chevron-right" class="ml-auto" style="color:#475569; width:20px; height:20px;"></i> </button> <button onclick="startGame('match')" class="option-btn flex items-center gap-4 p-5 rounded-2xl text-left" style="background:#111827; border:1px solid #1e293b;">
       <div class="w-12 h-12 rounded-xl flex items-center justify-center flex-shrink-0" style="background:#1e3a2f;"><i data-lucide="shuffle" style="color:#4ade80; width:24px; height:24px;"></i>
       </div>
       <div>
        <div class="font-bold text-base" style="color:#e2e8f0;">
         Match Game
        </div>
        <div class="text-sm" style="color:#64748b;">
         Pair terms with definitions
        </div>
       </div><i data-lucide="chevron-right" class="ml-auto" style="color:#475569; width:20px; height:20px;"></i> </button> <button onclick="startGame('scenario')" class="option-btn flex items-center gap-4 p-5 rounded-2xl text-left" style="background:#111827; border:1px solid #1e293b;">
       <div class="w-12 h-12 rounded-xl flex items-center justify-center flex-shrink-0" style="background:#3a1e3a;"><i data-lucide="briefcase" style="color:#c084fc; width:24px; height:24px;"></i>
       </div>
       <div>
        <div class="font-bold text-base" style="color:#e2e8f0;">
         Tax Scenarios
        </div>
        <div class="text-sm" style="color:#64748b;">
         Real-world situation challenges
        </div>
       </div><i data-lucide="chevron-right" class="ml-auto" style="color:#475569; width:20px; height:20px;"></i> </button>
     </div><button onclick="showScreen('reference')" class="text-sm underline" style="color:#64748b;">📖 Quick Reference Guide</button>
    </div>
   </div><!-- QUIZ SCREEN -->
   <div id="screen-quiz" class="h-full flex flex-col p-4 md:p-6 hidden">
    <div class="flex items-center justify-between mb-4"><button onclick="showScreen('home')" class="flex items-center gap-1 text-sm" style="color:#64748b;"><i data-lucide="arrow-left" style="width:16px;height:16px;"></i> Back</button>
     <div class="mono text-sm" style="color:#94a3b8;">
      <span id="q-current">1</span>/<span id="q-total">10</span>
     </div>
     <div class="flex items-center gap-1 mono text-sm font-bold" style="color:#fbbf24;">
      <i data-lucide="star" style="width:14px;height:14px;"></i> <span id="q-score">0</span>
     </div>
    </div>
    <div class="w-full rounded-full h-2 mb-6" style="background:#1e293b;">
     <div id="q-progress" class="progress-fill h-2 rounded-full" style="background:linear-gradient(90deg,#38bdf8,#818cf8); width:0%;"></div>
    </div>
    <div id="q-topic" class="mono text-xs tracking-wider mb-3 px-1" style="color:#38bdf8;"></div>
    <h2 id="q-question" class="text-xl font-bold mb-6 leading-relaxed" style="color:#e2e8f0;"></h2>
    <div id="q-options" class="flex flex-col gap-3 flex-1"></div>
    <div id="q-feedback" class="hidden mt-4 p-4 rounded-xl text-sm leading-relaxed" style="color:#e2e8f0;"></div><button id="q-next" class="hidden mt-4 w-full py-4 rounded-xl font-bold text-base" style="background:#38bdf8; color:#0a0f1e;" onclick="nextQuestion()">Next Question</button>
   </div><!-- MATCH SCREEN -->
   <div id="screen-match" class="h-full flex flex-col p-4 md:p-6 hidden">
    <div class="flex items-center justify-between mb-4"><button onclick="showScreen('home')" class="flex items-center gap-1 text-sm" style="color:#64748b;"><i data-lucide="arrow-left" style="width:16px;height:16px;"></i> Back</button>
     <div class="mono text-sm" style="color:#94a3b8;">
      Round <span id="m-round">1</span>/<span id="m-total-rounds">5</span>
     </div>
     <div class="flex items-center gap-1 mono text-sm font-bold" style="color:#4ade80;">
      <i data-lucide="check-circle" style="width:14px;height:14px;"></i> <span id="m-matched">0</span>
     </div>
    </div>
    <p class="text-sm mb-4" style="color:#64748b;">Tap a term, then tap its matching definition</p>
    <div class="grid grid-cols-2 gap-3 flex-1 overflow-auto" id="m-grid"></div>
    <div id="m-feedback" class="hidden mt-3 p-3 rounded-xl text-sm text-center" style="color:#e2e8f0;"></div>
   </div><!-- SCENARIO SCREEN -->
   <div id="screen-scenario" class="h-full flex flex-col p-4 md:p-6 hidden">
    <div class="flex items-center justify-between mb-4"><button onclick="showScreen('home')" class="flex items-center gap-1 text-sm" style="color:#64748b;"><i data-lucide="arrow-left" style="width:16px;height:16px;"></i> Back</button>
     <div class="mono text-sm" style="color:#94a3b8;">
      Scenario <span id="s-current">1</span>/<span id="s-total">8</span>
     </div>
     <div class="flex items-center gap-1 mono text-sm font-bold" style="color:#c084fc;">
      <i data-lucide="star" style="width:14px;height:14px;"></i> <span id="s-score">0</span>
     </div>
    </div>
    <div id="s-scenario" class="p-5 rounded-2xl mb-5" style="background:#111827; border:1px solid #1e293b;">
     <div id="s-context" class="text-sm mb-3" style="color:#94a3b8;"></div>
     <h2 id="s-question" class="text-lg font-bold leading-relaxed" style="color:#e2e8f0;"></h2>
    </div>
    <div id="s-options" class="flex flex-col gap-3 flex-1"></div>
    <div id="s-feedback" class="hidden mt-4 p-4 rounded-xl text-sm leading-relaxed" style="color:#e2e8f0;"></div><button id="s-next" class="hidden mt-4 w-full py-4 rounded-xl font-bold text-base" style="background:#c084fc; color:#0a0f1e;" onclick="nextScenario()">Next Scenario</button>
   </div><!-- RESULTS SCREEN -->
   <div id="screen-results" class="h-full flex flex-col items-center justify-center p-6 text-center hidden">
    <div class="max-w-md w-full slide-up">
     <div id="results-icon" class="text-6xl mb-4"></div>
     <h2 id="results-title" class="text-3xl font-extrabold mb-2" style="color:#e2e8f0;"></h2>
     <p id="results-subtitle" class="text-lg mb-6" style="color:#94a3b8;"></p>
     <div class="p-6 rounded-2xl mb-6" style="background:#111827; border:1px solid #1e293b;">
      <div class="text-5xl font-extrabold mono mb-1" style="color:#38bdf8;" id="results-score"></div>
      <div class="text-sm" style="color:#64748b;" id="results-detail"></div>
     </div>
     <div id="results-breakdown" class="text-left mb-6"></div>
     <div class="flex gap-3"><button onclick="showScreen('home')" class="flex-1 py-4 rounded-xl font-bold" style="background:#1e293b; color:#e2e8f0;">Home</button> <button id="results-retry" class="flex-1 py-4 rounded-xl font-bold" style="background:#38bdf8; color:#0a0f1e;">Play Again</button>
     </div>
    </div>
   </div><!-- REFERENCE SCREEN -->
   <div id="screen-reference" class="h-full flex flex-col p-4 md:p-6 hidden">
    <div class="flex items-center gap-3 mb-4"><button onclick="showScreen('home')" class="flex items-center gap-1 text-sm" style="color:#64748b;"><i data-lucide="arrow-left" style="width:16px;height:16px;"></i> Back</button>
     <h2 class="text-lg font-bold" style="color:#e2e8f0;">Quick Reference</h2>
    </div>
    <div class="flex gap-1 overflow-x-auto pb-2 mb-4 text-xs font-semibold flex-shrink-0" id="ref-tabs"></div>
    <div class="flex-1 overflow-auto" id="ref-content"></div>
   </div>
  </div>
  <script>
// ===================== DATA =====================
const quizQuestions = [
  // IRB Functions
  {topic:"IRB Functions",q:"What is the full name of IRB in Malay?",options:["Lembaga Hasil Dalam Negeri (LHDN)","Jabatan Hasil Dalam Negeri","Suruhanjaya Cukai Malaysia","Badan Pendapatan Negara"],answer:0,explain:"The Inland Revenue Board of Malaysia is known as Lembaga Hasil Dalam Negeri Malaysia (LHDNM)."},
  {topic:"IRB Functions",q:"Which of these is NOT a function of the IRB?",options:["Collecting income tax","Administering stamp duty","Setting fiscal policy","Advising the government on taxation"],answer:2,explain:"Setting fiscal policy is the role of the Ministry of Finance. IRB administers and collects taxes, and advises the government on tax matters."},
  {topic:"IRB Functions",q:"The IRB was established under which Act?",options:["Income Tax Act 1967","Inland Revenue Board of Malaysia Act 1995","Finance Act 2000","Taxation Administration Act 1992"],answer:1,explain:"The IRB was established under the Inland Revenue Board of Malaysia Act 1995 (Act 533)."},
  {topic:"IRB Functions",q:"Which taxes does the IRB administer?",options:["Only income tax","Income tax, petroleum income tax, RPGT, stamp duty","GST and SST only","Customs and excise duties"],answer:1,explain:"IRB administers income tax, petroleum income tax, real property gains tax (RPGT), and stamp duty."},

  // Self-Assessment System
  {topic:"Self-Assessment System",q:"When was the self-assessment system (SAS) introduced for individuals in Malaysia?",options:["2001","2004","2000","2006"],answer:1,explain:"SAS was introduced for companies in 2001, and extended to individuals and other taxpayers from Year of Assessment 2004."},
  {topic:"Self-Assessment System",q:"Under SAS, who is responsible for computing the tax payable?",options:["The IRB officer","The taxpayer themselves","The employer","The court"],answer:1,explain:"Under SAS, the taxpayer is responsible for computing their own income, claiming reliefs/deductions, and determining tax payable."},
  {topic:"Self-Assessment System",q:"What replaced the Official Assessment System (OAS) in Malaysia?",options:["Estimated Assessment","Self-Assessment System","Advance Ruling System","Composite Assessment"],answer:1,explain:"The Self-Assessment System (SAS) replaced the former Official Assessment System (OAS) where IRB previously computed the tax."},
  {topic:"Self-Assessment System",q:"Under SAS, a tax return submitted is deemed to be what?",options:["A tax invoice","A notice of assessment","A request for audit","A provisional estimate"],answer:1,explain:"Under SAS, the submission of a tax return is deemed to be a notice of assessment, meaning the taxpayer's own computation constitutes the assessment."},

  // Advantages of SAS to IRB
  {topic:"Advantages of SAS",q:"How does SAS benefit the IRB's operational efficiency?",options:["IRB hires more staff","Reduces IRB's administrative burden of raising assessments","IRB collects less tax","It eliminates all tax evasion"],answer:1,explain:"SAS shifts the computation responsibility to taxpayers, reducing IRB's workload in raising individual assessments."},
  {topic:"Advantages of SAS",q:"Under SAS, the IRB can focus more resources on which activity?",options:["Issuing assessments","Tax audit and investigation","Printing forms","Processing refunds only"],answer:1,explain:"With taxpayers self-assessing, the IRB can redirect resources toward tax audit, investigation, and compliance enforcement."},
  {topic:"Advantages of SAS",q:"SAS promotes which behaviour among taxpayers?",options:["Tax avoidance","Voluntary compliance","Dependency on IRB","Late filing"],answer:1,explain:"A key advantage of SAS is promoting voluntary compliance — taxpayers take responsibility for accurate reporting and timely payment."},
  {topic:"Advantages of SAS",q:"SAS allows faster processing of tax returns because:",options:["Returns are not checked","Returns are deemed assessments upon filing","IRB ignores errors","Taxpayers don't need to file"],answer:1,explain:"Since a filed return is deemed an assessment, there's no waiting period for IRB to issue a separate assessment notice."},

  // Amendment of Tax Return
  {topic:"Amendment of Tax Return",q:"Within how many months can an individual amend a tax return under SAS?",options:["3 months","6 months","12 months","24 months"],answer:1,explain:"Under Section 77B of the Income Tax Act 1967, an individual may make an amendment to the tax return within 6 months from the filing deadline."},
  {topic:"Amendment of Tax Return",q:"An amended return is treated as what?",options:["A new assessment","An amended deemed assessment","A request for audit","A voluntary disclosure penalty"],answer:1,explain:"An amended return replaces the original deemed assessment and becomes the new deemed assessment."},
  {topic:"Amendment of Tax Return",q:"If the amendment results in additional tax, what must the taxpayer do?",options:["Wait for IRB notice","Pay the additional tax by the amendment date","File an appeal","Request instalment"],answer:1,explain:"Any additional tax arising from the amendment must be paid on or before the date of amendment, along with any applicable penalty."},
  {topic:"Amendment of Tax Return",q:"What penalty rate applies on additional tax from an amended return?",options:["5%","10%","15%","20%"],answer:1,explain:"A penalty of 10% on the additional tax payable is imposed when a taxpayer amends the return resulting in higher tax."},

  // Types of Tax Return Forms
  {topic:"Tax Return Forms",q:"Which form is used by resident individuals with employment income only?",options:["Form B","Form BE","Form M","Form C"],answer:1,explain:"Form BE is for resident individuals with employment income (Section 4(b)) only, with no business income."},
  {topic:"Tax Return Forms",q:"Which form is used by individuals with business income?",options:["Form BE","Form B","Form M","Form P"],answer:1,explain:"Form B is for resident individuals who have business income (sole proprietorship), whether or not they also have employment income."},
  {topic:"Tax Return Forms",q:"Form M is used by which taxpayer?",options:["Malaysian companies","Non-resident individuals","Partnerships","Cooperatives"],answer:1,explain:"Form M is for non-resident individuals who derive income from Malaysia."},
  {topic:"Tax Return Forms",q:"Form P is used for which entity?",options:["Partnerships","Private companies","Public companies","Petroleum companies"],answer:0,explain:"Form P is filed by partnerships to declare the partnership income and its distribution among partners."},
  {topic:"Tax Return Forms",q:"Form C is filed by which type of taxpayer?",options:["Individuals","Companies (resident and non-resident)","Cooperatives","Trust bodies"],answer:1,explain:"Form C is the tax return form for companies, including both resident and non-resident companies."},
  {topic:"Tax Return Forms",q:"Form C1 is used by which entity?",options:["Companies with no operations","Partnerships","Cooperatives","Trust bodies"],answer:2,explain:"Form C1 is filed by cooperatives registered under the Cooperatives Societies Act."},
  {topic:"Tax Return Forms",q:"What is the filing deadline for individuals without business income (Form BE)?",options:["31 March","30 April","30 June","31 December"],answer:1,explain:"Form BE must be filed by 30 April of the following year. E-filing gets an extension of 15 days."},

  // Types of Assessments
  {topic:"Types of Assessments",q:"Under SAS, the original assessment is essentially:",options:["Issued by the Director General","The taxpayer's own return as deemed assessment","A court order","An audit finding"],answer:1,explain:"Under SAS, the tax return filed by the taxpayer constitutes the original assessment (deemed assessment)."},
  {topic:"Types of Assessments",q:"An additional assessment is raised when:",options:["The taxpayer overpaid tax","Income was not assessed or was under-assessed","The taxpayer files early","A refund is due"],answer:1,explain:"The Director General may raise an additional assessment under Section 91 when any income has not been assessed or has been assessed at an amount less than it should have been."},
  {topic:"Types of Assessments",q:"A composite assessment combines:",options:["Two different tax types","Assessments for multiple years of assessment","Individual and company tax","Income tax and stamp duty"],answer:1,explain:"A composite assessment is an assessment covering two or more years of assessment in one assessment."},
  {topic:"Types of Assessments",q:"An increased assessment is made when the Director General:",options:["Wants to reduce tax","Discovers that the tax assessed is less than it should be","Receives a refund claim","Closes an audit with no findings"],answer:1,explain:"An increased assessment is raised when a previous assessment is found to be less than it should have been."},
  {topic:"Types of Assessments",q:"A reduced assessment is issued when:",options:["More tax is owed","The taxpayer was overcharged and assessment should be lowered","The taxpayer appeals","A new tax law is passed"],answer:1,explain:"A reduced assessment is made when the Director General is satisfied that the original assessment was excessive."},
  {topic:"Types of Assessments",q:"A protective assessment is raised when:",options:["The taxpayer is cooperative","There is doubt about facts and the DG wants to protect revenue","Tax has been fully paid","The audit is complete with no issues"],answer:1,explain:"A protective assessment is raised as a precautionary measure when there's uncertainty about facts or legal interpretation, to protect government revenue within the statutory time limit."},

  // Tax Appeal
  {topic:"Tax Appeal",q:"A taxpayer who disagrees with an assessment must first file a(n):",options:["Court case","Notice of appeal to the Special Commissioners","Form Q (Notice of Appeal)","Police report"],answer:1,explain:"A taxpayer who is dissatisfied must file a Notice of Appeal (Form Q) to the Special Commissioners of Income Tax within 30 days."},
  {topic:"Tax Appeal",q:"Within how many days must a Notice of Appeal be filed?",options:["14 days","30 days","60 days","90 days"],answer:1,explain:"The notice of appeal must be filed within 30 days after the taxpayer is served with the notice of assessment."},
  {topic:"Tax Appeal",q:"The first level of tax appeal is heard by:",options:["High Court","Special Commissioners of Income Tax","Court of Appeal","Federal Court"],answer:1,explain:"Tax appeals are first heard by the Special Commissioners of Income Tax (SCIT), a quasi-judicial body."},
  {topic:"Tax Appeal",q:"After the Special Commissioners, the next level of appeal is to the:",options:["Federal Court","Court of Appeal","High Court","Tax Tribunal"],answer:2,explain:"If dissatisfied with the SCIT decision, either party can appeal to the High Court on a question of law."},

  // Monthly Tax Deduction (MTD/PCB)
  {topic:"Monthly Tax Deduction",q:"What is the Malay term for Monthly Tax Deduction?",options:["Cukai Bulanan","Potongan Cukai Bulanan (PCB)","Bayaran Cukai Bulanan","Cukai Pendapatan Bulanan"],answer:1,explain:"Monthly Tax Deduction is known as Potongan Cukai Bulanan (PCB) in Malay."},
  {topic:"Monthly Tax Deduction",q:"Who is responsible for deducting PCB from an employee's salary?",options:["The employee themselves","The employer","The IRB","The bank"],answer:1,explain:"The employer is legally required to deduct PCB from the employee's monthly remuneration and remit it to the IRB."},
  {topic:"Monthly Tax Deduction",q:"PCB must be remitted to the IRB by which day of the following month?",options:["7th","10th","15th","Last day"],answer:2,explain:"Employers must remit the PCB deducted to the IRB by the 15th of the following month."},
  {topic:"Monthly Tax Deduction",q:"PCB can be treated as the final tax if the taxpayer:",options:["Earns over RM1 million","Has only employment income, is resident, and PCB is correctly computed","Is non-resident","Owns a business"],answer:1,explain:"PCB can be treated as final tax if the individual is resident, has only employment income, tax is correctly computed, and they opt not to file a return (subject to conditions under Section 77(1A))."},

  // Responsibilities of Taxpayers
  {topic:"Taxpayer Responsibilities",q:"Every individual with chargeable income must do what?",options:["Wait for IRB to contact them","Register a tax file, file returns, and pay tax due","Only file if they receive a notice","Pay tax only when audited"],answer:1,explain:"Taxpayers are responsible for registering a tax file with IRB, filing accurate returns by the due date, and paying any tax payable."},
  {topic:"Taxpayer Responsibilities",q:"How long must taxpayers keep records and supporting documents?",options:["3 years","5 years","7 years","10 years"],answer:2,explain:"Taxpayers must keep sufficient records for 7 years from the end of the year of assessment to which the records relate."},
  {topic:"Taxpayer Responsibilities",q:"A taxpayer must notify the IRB of a change of address within:",options:["14 days","1 month","3 months","6 months"],answer:2,explain:"A taxpayer must inform the IRB of any change of address within 3 months of the change."},

  // Fines and Penalties
  {topic:"Fines & Penalties",q:"What is the penalty for late filing of a tax return?",options:["No penalty","Increase of 10% on tax payable","Increase of 20% on tax payable","Imprisonment only"],answer:1,explain:"Under Section 112(3), failure to furnish a return by the due date results in a penalty of 10% increase on the tax payable (if no prosecution)."},
  {topic:"Fines & Penalties",q:"Tax evasion under Section 114 can result in:",options:["Warning letter only","Fine of RM1,000 to RM20,000 and/or imprisonment up to 3 years, plus 300% penalty","Only a 10% penalty","Community service"],answer:1,explain:"Section 114 provides for a fine of RM1,000 to RM20,000 and/or imprisonment up to 3 years, plus a special penalty of 300% of the tax undercharged."},
  {topic:"Fines & Penalties",q:"An employer who fails to deduct and remit PCB commits an offence and may face:",options:["No consequence","A fine of RM200 to RM20,000 and/or imprisonment up to 6 months","Only a warning","Fine of RM50"],answer:1,explain:"Under Section 120(1), failure to deduct and remit PCB is an offence carrying a fine of RM200–RM20,000 and/or imprisonment up to 6 months."},
  {topic:"Fines & Penalties",q:"What penalty applies for incorrect tax returns due to negligence (not fraud)?",options:["No penalty","Penalty equal to the amount of tax undercharged (100%)","300% penalty","500% penalty"],answer:1,explain:"Under Section 113(2), an incorrect return due to negligence or carelessness (without fraud) attracts a penalty equal to the tax undercharged (100%)."},
];

const matchSets = [
  {title:"Tax Return Forms",pairs:[
    {term:"Form BE",def:"Resident individual — employment income only"},
    {term:"Form B",def:"Resident individual — business income"},
    {term:"Form M",def:"Non-resident individual"},
    {term:"Form P",def:"Partnerships"},
    {term:"Form C",def:"Companies"},
    {term:"Form C1",def:"Cooperatives"},
  ]},
  {title:"Types of Assessments",pairs:[
    {term:"Original",def:"Deemed assessment from taxpayer's return"},
    {term:"Additional",def:"Income not assessed or under-assessed"},
    {term:"Composite",def:"Covers multiple years of assessment"},
    {term:"Increased",def:"Previous assessment was too low"},
    {term:"Reduced",def:"Previous assessment was excessive"},
    {term:"Protective",def:"Precautionary — uncertainty about facts"},
  ]},
  {title:"Key Deadlines",pairs:[
    {term:"30 April",def:"Form BE filing deadline"},
    {term:"30 June",def:"Form B filing deadline"},
    {term:"15th of next month",def:"PCB remittance deadline"},
    {term:"30 days",def:"Time to file Notice of Appeal"},
    {term:"6 months",def:"Period to amend individual return"},
    {term:"7 years",def:"Record keeping period"},
  ]},
  {title:"Penalties & Sections",pairs:[
    {term:"Section 112(3)",def:"10% penalty for late filing"},
    {term:"Section 113(2)",def:"100% penalty for negligent return"},
    {term:"Section 114",def:"300% penalty + fine/jail for evasion"},
    {term:"Section 120(1)",def:"Employer fails to remit PCB"},
  ]},
  {title:"IRB & SAS Concepts",pairs:[
    {term:"LHDNM",def:"Malay name for IRB"},
    {term:"Act 533",def:"Inland Revenue Board Act 1995"},
    {term:"SAS",def:"Taxpayer computes own tax"},
    {term:"PCB",def:"Monthly salary tax deduction"},
    {term:"Form Q",def:"Notice of appeal form"},
  ]},
];

const scenarios = [
  {context:"Ahmad is employed at a private company earning RM6,500/month. He has no business income. It's March and he's preparing his tax return.",q:"Which form should Ahmad file?",options:["Form B","Form BE","Form M","Form P"],answer:1,explain:"Ahmad is a resident with employment income only. He should file Form BE by 30 April."},
  {context:"Siti filed her Form BE and later discovered she forgot to declare freelance income of RM8,000. It's been 4 months since the filing deadline.",q:"What should Siti do?",options:["Do nothing — it's too late","File an amended return within the 6-month window","Wait for IRB to contact her","File a new Form B"],answer:1,explain:"Siti is still within the 6-month amendment period. She should amend her return. She'll pay additional tax plus a 10% penalty on the additional amount."},
  {context:"Raj's employer deducts PCB monthly. At year-end, Raj's total PCB equals his actual tax liability. He only has employment income.",q:"Must Raj file a tax return?",options:["Yes, always mandatory","No — PCB can be his final tax if conditions are met","Yes, but he can file a blank form","Only if IRB sends a notice"],answer:1,explain:"If Raj meets the conditions (resident, employment income only, PCB correctly computed), PCB can be treated as final tax under Section 77(1A)."},
  {context:"The IRB completed an audit on Mei Ling and found she under-declared rental income for 3 years (YA 2020–2022).",q:"What type of assessment would the IRB most likely raise?",options:["Reduced assessment","Protective assessment","Composite additional assessment","Original assessment"],answer:2,explain:"Since multiple years are affected and income was under-assessed, the IRB can raise a composite assessment covering YA 2020–2022."},
  {context:"Kumar received a notice of additional assessment and believes the IRB made an error. He wants to contest it.",q:"What is Kumar's first step?",options:["File a police report","Go to the High Court directly","File Form Q (Notice of Appeal) to Special Commissioners within 30 days","Write a letter to the Minister of Finance"],answer:2,explain:"Kumar must file a Notice of Appeal (Form Q) to the Special Commissioners of Income Tax within 30 days of receiving the assessment."},
  {context:"A company failed to deduct PCB from employees' salaries for 6 months.",q:"What are the potential consequences for the employer?",options:["No consequences if employees pay their own tax","Fine of RM200–RM20,000 and/or imprisonment up to 6 months","Only a warning letter","10% penalty on company profits"],answer:1,explain:"Under Section 120(1), failure to deduct and remit PCB is a criminal offence with a fine of RM200–RM20,000 and/or imprisonment up to 6 months."},
  {context:"Fatimah deliberately inflated her business expenses by RM50,000 to reduce her tax liability. The IRB discovered this during an audit.",q:"Under which section will Fatimah likely be penalised, and what is the penalty?",options:["Section 112 — 10% penalty","Section 113 — 100% penalty for negligence","Section 114 — fine RM1K–RM20K, jail up to 3 years, plus 300% penalty","Section 120 — RM200 fine"],answer:2,explain:"Deliberate falsification is tax evasion under Section 114, carrying severe penalties including fines, imprisonment, and a 300% special penalty."},
  {context:"Lim filed his Form B on time but threw away all his receipts and records 2 years later during house cleaning.",q:"Has Lim violated any taxpayer responsibility?",options:["No — records only need to be kept for 1 year","No — only businesses need to keep records","Yes — records must be kept for 7 years","Yes — records must be kept for 3 years"],answer:2,explain:"All taxpayers must keep records for 7 years. Lim has breached this obligation and could face penalties if audited."},
];

const referenceData = {
  "IRB Functions":`<b>Inland Revenue Board (LHDNM)</b><br>Established under Act 533 (1995).<br><br><b>Functions:</b><ul class="list-disc pl-5 mt-1 space-y-1"><li>Administer, assess, collect and enforce income tax, petroleum income tax, RPGT, stamp duty</li><li>Advise the government on taxation policy</li><li>Liaise with other agencies on tax matters</li><li>Promote voluntary compliance</li></ul>`,
  "Self-Assessment":`<b>Self-Assessment System (SAS)</b><br>Introduced: Companies (2001), Individuals (2004).<br><br><b>Key Features:</b><ul class="list-disc pl-5 mt-1 space-y-1"><li>Taxpayer computes own tax liability</li><li>Filed return = deemed assessment</li><li>No separate assessment notice from IRB</li><li>IRB verifies via audit</li></ul><br><b>Advantages to IRB:</b><ul class="list-disc pl-5 mt-1 space-y-1"><li>Reduces administrative burden</li><li>Frees resources for audit & enforcement</li><li>Faster processing of returns</li><li>Promotes voluntary compliance</li></ul>`,
  "Tax Forms":`<table class="w-full text-sm"><tr style="border-bottom:1px solid #1e293b;"><th class="text-left py-2 pr-2" style="color:#38bdf8;">Form</th><th class="text-left py-2" style="color:#38bdf8;">Taxpayer</th></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">BE</td><td class="py-2">Resident individual — employment income only</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">B</td><td class="py-2">Resident individual — business income</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">M</td><td class="py-2">Non-resident individual</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">P</td><td class="py-2">Partnerships</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">C</td><td class="py-2">Companies</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">C1</td><td class="py-2">Cooperatives</td></tr><tr><td class="py-2 pr-2 font-bold">TA</td><td class="py-2">Trust bodies</td></tr></table>`,
  "Assessments":`<table class="w-full text-sm"><tr style="border-bottom:1px solid #1e293b;"><th class="text-left py-2 pr-2" style="color:#38bdf8;">Type</th><th class="text-left py-2" style="color:#38bdf8;">Description</th></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">Original</td><td class="py-2">Deemed assessment from filed return</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">Additional</td><td class="py-2">Income not assessed or under-assessed (S.91)</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">Composite</td><td class="py-2">Covers multiple years of assessment</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">Increased</td><td class="py-2">Previous assessment was too low</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2 font-bold">Reduced</td><td class="py-2">Previous assessment was excessive</td></tr><tr><td class="py-2 pr-2 font-bold">Protective</td><td class="py-2">Precautionary — uncertainty about facts/law</td></tr></table>`,
  "Appeals":`<b>Tax Appeal Process:</b><ol class="list-decimal pl-5 mt-2 space-y-2"><li><b>Notice of Appeal (Form Q)</b> — filed within 30 days of assessment to Special Commissioners of Income Tax (SCIT)</li><li><b>SCIT Hearing</b> — quasi-judicial body hears the case</li><li><b>High Court</b> — appeal on question of law</li><li><b>Court of Appeal</b> — further appeal</li><li><b>Federal Court</b> — final appeal (leave required)</li></ol>`,
  "PCB/MTD":`<b>Potongan Cukai Bulanan (PCB)</b><br><br><ul class="list-disc pl-5 space-y-1"><li>Employer deducts tax from monthly salary</li><li>Remit to IRB by <b>15th of the following month</b></li><li>Can be <b>final tax</b> if: resident + employment income only + correctly computed + taxpayer opts in</li><li>Employer failure: S.120(1) offence — fine RM200–RM20,000 and/or 6 months jail</li></ul>`,
  "Responsibilities":`<b>Taxpayer Responsibilities:</b><ul class="list-disc pl-5 mt-2 space-y-1"><li>Register a tax file with IRB</li><li>File accurate returns by the due date</li><li>Pay tax on time</li><li>Keep records for <b>7 years</b></li><li>Notify IRB of address change within <b>3 months</b></li><li>Declare all sources of income</li></ul>`,
  "Penalties":`<table class="w-full text-sm"><tr style="border-bottom:1px solid #1e293b;"><th class="text-left py-2 pr-2" style="color:#38bdf8;">Offence</th><th class="text-left py-2" style="color:#38bdf8;">Penalty</th></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2">Late filing (S.112)</td><td class="py-2">10% increase on tax payable</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2">Negligent return (S.113)</td><td class="py-2">100% of tax undercharged</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2">Tax evasion (S.114)</td><td class="py-2">Fine RM1K–RM20K + jail up to 3 yrs + 300% penalty</td></tr><tr style="border-bottom:1px solid #1e293b;"><td class="py-2 pr-2">Fail to remit PCB (S.120)</td><td class="py-2">Fine RM200–RM20K + jail up to 6 months</td></tr><tr><td class="py-2 pr-2">Amended return extra tax</td><td class="py-2">10% on additional tax</td></tr></table>`,
};

// ===================== GAME STATE =====================
let currentScreen = 'home';
let quizState = { questions:[], idx:0, score:0, answered:false };
let matchState = { setIdx:0, selected:null, matched:[], cards:[] };
let scenarioState = { idx:0, score:0, answered:false };

function shuffle(arr) { const a=[...arr]; for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]];} return a; }

function showScreen(name) {
  document.querySelectorAll('[id^="screen-"]').forEach(s=>s.classList.add('hidden'));
  document.getElementById('screen-'+name).classList.remove('hidden');
  currentScreen = name;
  if(name==='reference') buildReference();
  lucide.createIcons();
}

// ===================== QUIZ =====================
function startGame(type) {
  if(type==='quiz') {
    quizState.questions = shuffle(quizQuestions).slice(0,15);
    quizState.idx=0; quizState.score=0; quizState.answered=false;
    document.getElementById('q-total').textContent = quizState.questions.length;
    showScreen('quiz');
    renderQuestion();
  } else if(type==='match') {
    matchState.setIdx=0; matchState.selected=null; matchState.matched=[];
    document.getElementById('m-total-rounds').textContent = matchSets.length;
    showScreen('match');
    renderMatchRound();
  } else if(type==='scenario') {
    scenarioState.idx=0; scenarioState.score=0; scenarioState.answered=false;
    document.getElementById('s-total').textContent = scenarios.length;
    showScreen('scenario');
    renderScenario();
  }
}

function renderQuestion() {
  const q = quizState.questions[quizState.idx];
  document.getElementById('q-current').textContent = quizState.idx+1;
  document.getElementById('q-score').textContent = quizState.score;
  document.getElementById('q-progress').style.width = ((quizState.idx)/quizState.questions.length*100)+'%';
  document.getElementById('q-topic').textContent = q.topic.toUpperCase();
  document.getElementById('q-question').textContent = q.q;
  document.getElementById('q-feedback').classList.add('hidden');
  document.getElementById('q-next').classList.add('hidden');
  quizState.answered = false;

  const optContainer = document.getElementById('q-options');
  optContainer.innerHTML = '';
  const labels = ['A','B','C','D'];
  q.options.forEach((opt,i) => {
    const btn = document.createElement('button');
    btn.className = 'option-btn flex items-center gap-3 p-4 rounded-xl text-left text-sm';
    btn.style.cssText = 'background:#111827; border:1px solid #1e293b; color:#e2e8f0;';
    btn.innerHTML = `<span class="mono font-bold flex-shrink-0 w-8 h-8 rounded-lg flex items-center justify-center text-xs" style="background:#1e293b; color:#94a3b8;">${labels[i]}</span><span>${opt}</span>`;
    btn.onclick = () => answerQuiz(i);
    optContainer.appendChild(btn);
  });
}

function answerQuiz(idx) {
  if(quizState.answered) return;
  quizState.answered = true;
  const q = quizState.questions[quizState.idx];
  const correct = idx === q.answer;
  if(correct) quizState.score++;
  document.getElementById('q-score').textContent = quizState.score;

  const btns = document.getElementById('q-options').children;
  for(let i=0;i<btns.length;i++) {
    btns[i].disabled = true;
    if(i===q.answer) { btns[i].style.background='#064e3b'; btns[i].style.borderColor='#4ade80'; }
    else if(i===idx && !correct) { btns[i].style.background='#450a0a'; btns[i].style.borderColor='#f87171'; }
  }

  const fb = document.getElementById('q-feedback');
  fb.classList.remove('hidden');
  fb.style.background = correct ? '#064e3b' : '#450a0a';
  fb.innerHTML = `<b>${correct?'✅ Correct!':'❌ Incorrect'}</b><br>${q.explain}`;
  document.getElementById('q-next').classList.remove('hidden');
  document.getElementById('q-next').textContent = quizState.idx >= quizState.questions.length-1 ? 'See Results' : 'Next Question';
}

function nextQuestion() {
  quizState.idx++;
  if(quizState.idx >= quizState.questions.length) {
    showResults('quiz', quizState.score, quizState.questions.length);
  } else { renderQuestion(); }
}

// ===================== MATCH =====================
function renderMatchRound() {
  const set = matchSets[matchState.setIdx];
  matchState.selected = null;
  matchState.matched = [];
  document.getElementById('m-round').textContent = matchState.setIdx+1;
  document.getElementById('m-matched').textContent = '0';
  document.getElementById('m-feedback').classList.add('hidden');

  const terms = set.pairs.map((p,i) => ({id:'t'+i, text:p.term, type:'term', pairIdx:i}));
  const defs = set.pairs.map((p,i) => ({id:'d'+i, text:p.def, type:'def', pairIdx:i}));
  matchState.cards = [...shuffle(terms), ...shuffle(defs)];

  const grid = document.getElementById('m-grid');
  grid.innerHTML = '';
  const half = Math.ceil(matchState.cards.length/2);
  const leftCol = matchState.cards.slice(0,half);
  const rightCol = matchState.cards.slice(half);

  [leftCol, rightCol].forEach(col => {
    const colDiv = document.createElement('div');
    colDiv.className = 'flex flex-col gap-2';
    col.forEach(card => {
      const btn = document.createElement('button');
      btn.id = 'mc-'+card.id;
      btn.className = 'option-btn p-3 rounded-xl text-sm text-left';
      btn.style.cssText = `background:#111827; border:1px solid #1e293b; color:#e2e8f0; min-height:52px;`;
      btn.innerHTML = `<span class="mono text-xs block mb-0.5" style="color:${card.type==='term'?'#38bdf8':'#c084fc'};">${card.type==='term'?'TERM':'DEFINITION'}</span>${card.text}`;
      btn.onclick = () => selectMatchCard(card);
      colDiv.appendChild(btn);
    });
    grid.appendChild(colDiv);
  });
}

function selectMatchCard(card) {
  if(matchState.matched.includes(card.pairIdx)) return;
  const fb = document.getElementById('m-feedback');

  if(!matchState.selected) {
    matchState.selected = card;
    document.getElementById('mc-'+card.id).style.borderColor = '#fbbf24';
    document.getElementById('mc-'+card.id).style.background = '#1e293b';
    fb.classList.add('hidden');
  } else {
    if(matchState.selected.id === card.id) { // deselect
      document.getElementById('mc-'+card.id).style.borderColor = '#1e293b';
      document.getElementById('mc-'+card.id).style.background = '#111827';
      matchState.selected = null; return;
    }
    if(matchState.selected.type === card.type) { // same type
      document.getElementById('mc-'+matchState.selected.id).style.borderColor = '#1e293b';
      document.getElementById('mc-'+matchState.selected.id).style.background = '#111827';
      matchState.selected = card;
      document.getElementById('mc-'+card.id).style.borderColor = '#fbbf24';
      document.getElementById('mc-'+card.id).style.background = '#1e293b';
      fb.classList.remove('hidden'); fb.style.background='#1e293b'; fb.textContent='Select one term and one definition';
      return;
    }
    const isMatch = matchState.selected.pairIdx === card.pairIdx;
    if(isMatch) {
      matchState.matched.push(card.pairIdx);
      [matchState.selected.id, card.id].forEach(id => {
        const el = document.getElementById('mc-'+id);
        el.style.borderColor='#4ade80'; el.style.background='#064e3b'; el.disabled=true;
      });
      document.getElementById('m-matched').textContent = matchState.matched.length;
      fb.classList.remove('hidden'); fb.style.background='#064e3b'; fb.textContent='✅ Matched!';
      if(matchState.matched.length === matchSets[matchState.setIdx].pairs.length) {
        setTimeout(() => {
          matchState.setIdx++;
          if(matchState.setIdx >= matchSets.length) {
            showResults('match', matchSets.reduce((s,m)=>s+m.pairs.length,0), matchSets.reduce((s,m)=>s+m.pairs.length,0));
          } else { renderMatchRound(); }
        }, 1000);
      }
    } else {
      [matchState.selected.id, card.id].forEach(id => {
        const el = document.getElementById('mc-'+id);
        el.style.borderColor='#f87171'; el.style.background='#450a0a';
        setTimeout(()=>{ el.style.borderColor='#1e293b'; el.style.background='#111827'; },600);
      });
      fb.classList.remove('hidden'); fb.style.background='#450a0a'; fb.textContent='❌ Not a match — try again';
    }
    matchState.selected = null;
  }
}

// ===================== SCENARIOS =====================
function renderScenario() {
  const s = scenarios[scenarioState.idx];
  document.getElementById('s-current').textContent = scenarioState.idx+1;
  document.getElementById('s-score').textContent = scenarioState.score;
  document.getElementById('s-context').textContent = s.context;
  document.getElementById('s-question').textContent = s.q;
  document.getElementById('s-feedback').classList.add('hidden');
  document.getElementById('s-next').classList.add('hidden');
  scenarioState.answered = false;

  const optC = document.getElementById('s-options');
  optC.innerHTML = '';
  s.options.forEach((opt,i) => {
    const btn = document.createElement('button');
    btn.className = 'option-btn p-4 rounded-xl text-sm text-left';
    btn.style.cssText = 'background:#111827; border:1px solid #1e293b; color:#e2e8f0;';
    btn.textContent = opt;
    btn.onclick = () => answerScenario(i);
    optC.appendChild(btn);
  });
}

function answerScenario(idx) {
  if(scenarioState.answered) return;
  scenarioState.answered = true;
  const s = scenarios[scenarioState.idx];
  const correct = idx === s.answer;
  if(correct) scenarioState.score++;
  document.getElementById('s-score').textContent = scenarioState.score;

  const btns = document.getElementById('s-options').children;
  for(let i=0;i<btns.length;i++) {
    btns[i].disabled=true;
    if(i===s.answer) { btns[i].style.background='#064e3b'; btns[i].style.borderColor='#4ade80'; }
    else if(i===idx && !correct) { btns[i].style.background='#450a0a'; btns[i].style.borderColor='#f87171'; }
  }
  const fb = document.getElementById('s-feedback');
  fb.classList.remove('hidden');
  fb.style.background = correct ? '#064e3b' : '#450a0a';
  fb.innerHTML = `<b>${correct?'✅ Correct!':'❌ Incorrect'}</b><br>${s.explain}`;
  document.getElementById('s-next').classList.remove('hidden');
  document.getElementById('s-next').textContent = scenarioState.idx >= scenarios.length-1 ? 'See Results' : 'Next Scenario';
}

function nextScenario() {
  scenarioState.idx++;
  if(scenarioState.idx >= scenarios.length) {
    showResults('scenario', scenarioState.score, scenarios.length);
  } else { renderScenario(); }
}

// ===================== RESULTS =====================
function showResults(type, score, total) {
  showScreen('results');
  const pct = Math.round(score/total*100);
  let icon='🏆', title='Outstanding!', sub='You really know Malaysian tax!';
  if(pct<50) { icon='📚'; title='Keep Learning!'; sub='Review the reference guide and try again.'; }
  else if(pct<80) { icon='👍'; title='Good Effort!'; sub='Almost there — a quick review will help.'; }

  document.getElementById('results-icon').textContent = icon;
  document.getElementById('results-title').textContent = title;
  document.getElementById('results-subtitle').textContent = sub;
  document.getElementById('results-score').textContent = pct+'%';
  document.getElementById('results-detail').textContent = `${score} out of ${total} correct`;
  document.getElementById('results-retry').onclick = () => startGame(type);

  const bd = document.getElementById('results-breakdown');
  if(type==='quiz') {
    const topics = {};
    quizState.questions.forEach((q,i) => {
      if(!topics[q.topic]) topics[q.topic]={correct:0,total:0};
      topics[q.topic].total++;
    });
    // We don't track per-topic correctness in current simple state, so skip detailed breakdown
    bd.innerHTML = '';
  } else { bd.innerHTML=''; }
}

// ===================== REFERENCE =====================
function buildReference() {
  const tabs = document.getElementById('ref-tabs');
  const content = document.getElementById('ref-content');
  const keys = Object.keys(referenceData);
  tabs.innerHTML = '';
  keys.forEach((k,i) => {
    const btn = document.createElement('button');
    btn.className = 'px-3 py-2 rounded-lg whitespace-nowrap flex-shrink-0';
    btn.style.cssText = i===0 ? 'background:#1e293b; color:#38bdf8;' : 'color:#64748b;';
    btn.textContent = k;
    btn.onclick = () => {
      [...tabs.children].forEach(t => { t.style.background='transparent'; t.style.color='#64748b'; });
      btn.style.background='#1e293b'; btn.style.color='#38bdf8';
      content.innerHTML = `<div class="p-4 rounded-xl text-sm leading-relaxed" style="background:#111827; color:#cbd5e1;">${referenceData[k]}</div>`;
    };
    tabs.appendChild(btn);
  });
  content.innerHTML = `<div class="p-4 rounded-xl text-sm leading-relaxed" style="background:#111827; color:#cbd5e1;">${referenceData[keys[0]]}</div>`;
}

// ===================== ELEMENT SDK =====================
const defaultConfig = {
  game_title: 'Malaysia Tax Administration',
  subtitle_text: 'Master IRB functions, SAS, assessments, appeals & more',
  background_color: '#0a0f1e',
  surface_color: '#111827',
  text_color: '#e2e8f0',
  accent_color: '#38bdf8',
  secondary_accent: '#c084fc',
  font_family: 'Plus Jakarta Sans',
  font_size: 16
};

function applyConfig(config) {
  const t = config.game_title || defaultConfig.game_title;
  const s = config.subtitle_text || defaultConfig.subtitle_text;
  const bg = config.background_color || defaultConfig.background_color;
  const sf = config.surface_color || defaultConfig.surface_color;
  const tx = config.text_color || defaultConfig.text_color;
  const ac = config.accent_color || defaultConfig.accent_color;
  const sa = config.secondary_accent || defaultConfig.secondary_accent;
  const ff = config.font_family || defaultConfig.font_family;
  const fs = config.font_size || defaultConfig.font_size;

  const el = document.getElementById('el-title');
  if(el) el.innerHTML = t.replace(/\n/g,'<br>');
  const sub = document.getElementById('el-subtitle');
  if(sub) sub.textContent = s;

  document.getElementById('app').style.background = bg;
  document.querySelectorAll('[style*="color:#e2e8f0"]').forEach(e => e.style.color = tx);
  document.body.style.fontFamily = `${ff}, Plus Jakarta Sans, sans-serif`;
}

window.elementSdk.init({
  defaultConfig,
  onConfigChange: async (config) => applyConfig(config),
  mapToCapabilities: (config) => ({
    recolorables: [
      { get:()=>config.background_color||defaultConfig.background_color, set:(v)=>{config.background_color=v; window.elementSdk.setConfig({background_color:v});} },
      { get:()=>config.surface_color||defaultConfig.surface_color, set:(v)=>{config.surface_color=v; window.elementSdk.setConfig({surface_color:v});} },
      { get:()=>config.text_color||defaultConfig.text_color, set:(v)=>{config.text_color=v; window.elementSdk.setConfig({text_color:v});} },
      { get:()=>config.accent_color||defaultConfig.accent_color, set:(v)=>{config.accent_color=v; window.elementSdk.setConfig({accent_color:v});} },
      { get:()=>config.secondary_accent||defaultConfig.secondary_accent, set:(v)=>{config.secondary_accent=v; window.elementSdk.setConfig({secondary_accent:v});} },
    ],
    borderables: [],
    fontEditable: { get:()=>config.font_family||defaultConfig.font_family, set:(v)=>{config.font_family=v; window.elementSdk.setConfig({font_family:v});} },
    fontSizeable: { get:()=>config.font_size||defaultConfig.font_size, set:(v)=>{config.font_size=v; window.elementSdk.setConfig({font_size:v});} },
  }),
  mapToEditPanelValues: (config) => new Map([
    ['game_title', config.game_title || defaultConfig.game_title],
    ['subtitle_text', config.subtitle_text || defaultConfig.subtitle_text],
  ])
});

lucide.createIcons();
</script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9eea4c228062e708',t:'MTc3NjU4NDgwNy4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
