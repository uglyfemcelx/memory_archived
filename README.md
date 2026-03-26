<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Memory Archive</title>
<style>
body {
    background: black;
    color: #00ff88;
    font-family: "Courier New", monospace;
    padding: 40px;
    overflow-x: hidden;
}
#terminal {
    white-space: pre-wrap;
    line-height: 1.6;
}
.cursor {
    display: inline-block;
    width: 10px;
    background: #00ff88;
    margin-left: 5px;
    animation: blink 1s infinite;
}
@keyframes blink {
    0% { opacity: 1; }
    50% { opacity: 0; }
    100% { opacity: 1; }
}
.memory {
    opacity: 0;
    transition: opacity 1s;
    margin-bottom: 10px;
}
</style>
</head>
<body>

<pre id="terminal"></pre><span class="cursor"></span>

<script>
// ------------------ memories array ------------------
const memories = [
"> memory_001:\n> went to a movie theatre to watch my favorite movie",
"> memory_002:\n> i was happy",
"> memory_002a:\n> i was happy, repetition detected",
"> memory_002b:\n> i was happy, repetition detected",
"> memory_003:\n> my friend texts me but i didn’t know",
"> memory_004:\n> the next day something happened and i blame myself",
"> memory_005:\n> creating an account for my own digital diary",
"> memory_006:\n> wishing that i could turn back time",
"> memory_007:\n> first online friend appeared",
"> memory_008:\n> vented to each other for hours",
"> memory_009:\n> they were so nice to me",
"> memory_010:\n> heartbreak",
"> memory_011:\n> first cosplay attempt, looked dumb",
"> memory_012:\n> something unexpected happened",
"> memory_013:\n> why are there so many people?",
"> memory_014:\n> someone I didn’t know texted me wanting to be my friend",
"> memory_015:\n> we talk every day and now we are friends",
"> memory_016:\n> rainy nights felt lonely but comforting",
"> memory_017:\n> ████ keeps appearing",
"> memory_018:\n> discovered a hidden corner online",
"> memory_019:\n> tried drawing fanart, messy but fun",
"> memory_020:\n> my favorite anime made me cry again, ████ keeps appearing",
"> memory_021:\n> first secret poem about someone",
"> memory_022:\n> late night doomscrolling, couldn’t stop",
"> memory_023:\n> venting in secret diary",
"> memory_024:\n> found a random video that made me laugh",
"> memory_025:\n> experimenting with photography",
"> memory_026:\n> memory repeated... photography experiments, ████ keeps appearing",
"> memory_027:\n> favorite artist released a new song",
"> memory_028:\n> memory repeated... new song discovered",
"> memory_029:\n> grinding my bubblegum like there is no tomorrow",
"> memory_030:\n> favorite actress starred in something amazing",
"> memory_031:\n> tried doing something new",
"> memory_032:\n> memory repeated... ████ attempt",
"> memory_033:\n> my favorite anime scene made me smile",
"> memory_034:\n> late night serial coding experiments",
"> memory_035:\n> memory repeated... serial coding experiments?",
"> memory_036:\n> stumbled on rare art online",
"> memory_037:\n> memory repeated... rare art online, ████ keeps appearing",
"> memory_038:\n> finished reading a book",
"> memory_039:\n> memory repeated... book series finished",
"> memory_040:\n> drew something",
"> memory_041:\n> memory repeated... fanart, ████ keeps appearing",
"> memory_042:\n> walking in silence, remembering everything"
];

// ------------------ riddle check ------------------
function askRiddle() {
    const answer = prompt("riddle: what has keys but can't open locks?");
    if(answer && answer.toLowerCase().includes("piano")) {
        startTyping();
    } else {
        alert("incorrect... try again later.");
    }
}

// ------------------ typing effect ------------------
let i = 0;
const terminal = document.getElementById("terminal");

function startTyping() {
    terminal.innerHTML = "";
    const cursor = document.querySelector(".cursor");
    const typingInterval = setInterval(()=>{
        if(i < memories.length){
            terminal.innerHTML += memories[i] + "\n";
            i++;
            terminal.scrollTop = terminal.scrollHeight;
        } else {
            clearInterval(typingInterval);
            cursor.style.display = "none";
        }
    }, 500);
}

// ------------------ start ------------------
askRiddle();
</script>

</body>
</html>
