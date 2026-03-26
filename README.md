<!DOCTYPE html>
<html>
<head>
<title>memory_archive</title>
<style>
body{
  background:black;
  color:#00ff88;
  font-family:"Courier New", monospace;
  padding:40px;
  overflow-x:hidden;
}

#terminal{
  white-space:pre-wrap;
  line-height:1.6;
  max-height:80vh;
  overflow-y:auto;
}

.cursor{
  display:inline-block;
  width:10px;
  background:#00ff88;
  margin-left:5px;
  animation:blink 1s infinite;
}

@keyframes blink{
  0%{opacity:1;}
  50%{opacity:0;}
  100%{opacity:1;}
}

.glitch{
  animation:glitch 0.2s infinite;
}

@keyframes glitch{
  0%{opacity:1;}
  50%{opacity:0.5;}
  100%{opacity:1;}
}

#hiddenMessage{
  opacity:0;
  margin-top:20px;
  transition:opacity 1s;
  white-space:pre-wrap;
}

input.riddleInput{
  background:black;
  color:#00ff88;
  border:1px solid #00ff88;
  padding:5px;
  margin-top:10px;
  font-family:"Courier New", monospace;
}

#log{
  margin-top:20px;
  font-size:13px;
  opacity:0.7;
}
</style>
</head>
<body>

<pre id="terminal"></pre><span class="cursor"></span>

<div id="hiddenMessage"></div>
<div id="log"></div>

<script>
// ---------------- BASE ----------------
const terminal = document.getElementById("terminal")
const hidden = document.getElementById("hiddenMessage")
const log = document.getElementById("log")

// ---------------- MEMORIES ----------------
const memories = [const memories = [
"> memory_001:\n> went to a movie theatre to watch my favorite movie",
"> memory_002:\n> i was happy",
"> memory_002a:\n> i was happy",
"> memory_002b:\n> i was happy, repetition detected",
"> memory_002c:\n> i love the rain",
"> memory_002d:\n> rainy days felt soo cozy",
"> memory_003:\n> my friend texts me but i didn’t know",
"> memory_003a:\n> i liked watching clouds drift",
"> memory_004:\n> the next day something happened and i blame myself",
"> memory_004a:\n> i try to be happy",
"> memory_004b:\n> i try to be happy",
"> memory_004c:\n> i try to be happy, ████ keeps appearing",
"> memory_004d:\n> memory repeated... happiness fading?",
"> memory_005:\n> creating an account for my own digital diary",
"> memory_005a:\n> late nights doomscrolling online",
"> memory_005b:\n> first cosplay attempt... i look like an idiot",
"> memory_006:\n> wishing that i could turn back time",
"> memory_006a:\n> drawing felt therapeutic",
"> memory_007:\n> first online friend appeared",
"> memory_007a:\n> i smiled at a stranger",
"> memory_008:\n> vented to each other for hours",
"> memory_008a:\n> favorite anime made me cry",
"> memory_008b:\n> favorite anime made me cry again, ████ keeps appearing",
"> memory_009:\n> they were so nice to me",
"> memory_009a:\n> i discovered a hidden place in town",
"> memory_010:\n> :(",
"> memory_010a:\n> i wrote my first secret poem about her... even thought she would never read it",
"> memory_010b:\n> i miss her",
"> memory_011:\n> another cosplay attempt, looked dumb asf",
"> memory_011a:\n> listening to rain and music at once",
"> memory_012:\n> something unexpected happened",
"> memory_012a:\n> this video made me laugh",
"> memory_013:\n> why are there so many people?",
"> memory_013a:\n> i stayed up all night reading yao- ERROR DETECTED",
"> memory_014:\n> someone I didn’t know texted me wanting to be my friend, we talked about cats for hours",
"> memory_014a:\n> walked in silence for hours",
"> memory_015:\n> we talk every day and now we are friens!!",
"> memory_015a:\n> memory repeated... walked in silence for hours, ████ keeps appearing",
"> memory_016:\n> rainy nights felt lonely but comforting",
"> memory_016a:\n> i love my online friends",
"> memory_017:\n> ████ keeps appearing",
"> memory_017a:\n> quiet afternoons",
"> memory_018:\n> discovered a hidden corner online",
"> memory_018a:\n> small victories felt huge",
"> memory_019:\n> tried drawing fanart, messy but fun",
"> memory_019a:\n> memory repeated... small victories felt huge, chicken dinner!",
"> memory_020:\n> my favorite anime made me cry again, ████ keeps appearing",
"> memory_020a:\n> experimenting with photography",
"> memory_021:\n> another secret poem about- ERROR DETECTED",
"> memory_021a:\n> my favorite idol smiled in a video",
"> memory_021b:\n> watching my favorite idol again, ████ keeps appearing",
"> memory_022:\n> late night doomscrolling, couldn’t stop",
"> memory_022a:\n> memory repeated... photography experiments",
"> memory_023:\n> venting in secret diary",
"> memory_023a:\n> favorite artist released a new song",
"> memory_024:\n> found a random video that made me laugh",
"> memory_024a:\n> found a hidden easter egg in a game",
"> memory_025:\n> experimenting with photography",
"> memory_025a:\n> memory repeated... easter egg found",
"> memory_026:\n> grinding my bubblegum like there is no tomorrow",
"> memory_027:\n> favorite idol starred in something amazing",
"> memory_028:\n> tried doing something new",
"> memory_029:\n> memory repeated... ████ attempt",
"> memory_030:\n> my favorite anime scene made me smile",
"> memory_031:\n> late night serial coding experiments",
"> memory_032:\n> memory repeated... serial coding experiments?",
"> memory_033:\n> caught a big fish on roblox!",
"> memory_034:\n> discovering a new song",
"> memory_035:\n> memory repeated... new song discovered",
"> memory_036:\n> ████ detected",
"> memory_037:\n> my secret hideout discovery",
"> memory_038:\n> memory repeated... secret hideout",
"> memory_039:\n> stumbled on rare art online",
"> memory_040:\n> memory repeated... rare art online, ████ keeps appearing",
"> memory_041:\n> finished writing a story",
"> memory_042:\n> memory repeated... my first story finished",
"> memory_043:\n> drawing something",
"> memory_044:\n> memory repeated..., ████ keeps appearing",
"> memory_045:\n> walking in silence, remembering everything"
];


// ---------------- RIDDLE ----------------
const riddleQuestion = "> solve this riddle to access memories:\n> i speak without a mouth and hear without ears. i have nobody, but I come alive with wind. what am I?"
const riddleAnswer = "echo"

// ---------------- TYPE EFFECT ----------------
let i = 0
function typeLine(lines, callback){
  if(i < lines.length){
    terminal.innerHTML += lines[i] + "\n"
    terminal.scrollTop = terminal.scrollHeight
    i++
    setTimeout(()=>typeLine(lines, callback),400)
  } else{
    if(callback) callback()
  }
}

// ---------------- CREATE INPUT ----------------
function showRiddleInput(){
  const input = document.createElement("input")
  input.type = "text"
  input.className = "riddleInput"
  input.placeholder = "type your answer here..."
  terminal.appendChild(document.createElement("br"))
  terminal.appendChild(input)
  input.focus()

  input.addEventListener("keydown", function(e){
    if(e.key === "Enter"){
      if(input.value.trim().toLowerCase() === riddleAnswer){
        terminal.innerHTML += "\n> access granted...\n"
        input.style.display="none"
        revealMemories()
      } else{
        terminal.innerHTML += "\n> access denied...\n> try again"
        terminal.classList.add("glitch")
        setTimeout(()=>terminal.classList.remove("glitch"),500)
        input.value=""
      }
    }
  })
}

// ---------------- REVEAL MEMORIES ----------------
function revealMemories(){
  let memIndex = 0
  function showNext(){
    if(memIndex < memories.length){
      terminal.innerHTML += memories[memIndex] + "\n"
      terminal.scrollTop = terminal.scrollHeight
      memIndex++
      setTimeout(showNext,300)
    }
  }
  showNext()
}

// ---------------- CURSOR TRACKING ----------------
document.addEventListener("mousemove", function(e){
  if(Math.random() < 0.01){
    let follow = document.createElement("div")
    follow.innerText = "i see you"
    follow.style.position="absolute"
    follow.style.left = e.pageX + "px"
    follow.style.top = e.pageY + "px"
    follow.style.opacity="0.5"
    document.body.appendChild(follow)
    setTimeout(()=>follow.remove(),500)
  }
})

// ---------------- HIDDEN CLICK ----------------
document.body.onclick = function(e){
  if(e.target.id === "terminal"){
    hidden.style.opacity="1"
    hidden.innerText="> hidden click detected\n> you found a secret message"
  }
}

// ---------------- INIT ----------------
typeLine([riddleQuestion], showRiddleInput)

</script>
</body>
</html>
