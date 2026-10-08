<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pacific Theatre War Game</title>

<style>
/* =========================================================
   PACIFIC THEATRE WAR GAME
   TWO PLAYER CARRIER STRIKE GROUP VS. CARRIER STRIKE GROUP
   ========================================================= */

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    min-height: 100vh;
    color: #eee7d4;
    font-family: Georgia, "Times New Roman", serif;
    background:
        linear-gradient(rgba(34,32,27,.91), rgba(34,32,27,.91)),
        repeating-linear-gradient(
            0deg,
            #756d5b 0px,
            #756d5b 2px,
            #686050 3px,
            #686050 5px
        );
}

button {
    font-family: Georgia, "Times New Roman", serif;
}

.hidden {
    display: none !important;
}

.header {
    background: #24231f;
    border-bottom: 4px solid #b8a77c;
    padding: 14px 20px;
    text-align: center;
    box-shadow: 0 4px 12px #000;
}

.header h1 {
    margin: 0;
    font-size: clamp(25px, 4vw, 48px);
    letter-spacing: 5px;
    text-transform: uppercase;
}

.subtitle {
    margin-top: 5px;
    color: #c8b98d;
    letter-spacing: 3px;
    font-size: 13px;
}

.screen {
    max-width: 1450px;
    margin: auto;
    padding: 20px;
}

.document {
    position: relative;
    padding: 28px;
    color: #29271f;
    background:
        linear-gradient(rgba(224,214,188,.97), rgba(211,201,172,.97));
    border: 2px solid #39352b;
    box-shadow:
        0 8px 25px #000,
        inset 0 0 50px rgba(90,75,45,.12);
}

.document::before {
    content: "U.S. NAVAL OPERATIONS — PACIFIC";
    position: absolute;
    top: 8px;
    right: 15px;
    color: #6e6250;
    font-family: monospace;
    font-size: 10px;
    opacity: .7;
}

.stamp {
    display: inline-block;
    margin-bottom: 12px;
    padding: 5px 10px;
    color: #7d2923;
    border: 3px solid #7d2923;
    font-family: monospace;
    font-weight: bold;
    letter-spacing: 2px;
    transform: rotate(-3deg);
}

.title-block {
    padding: 45px 20px;
    text-align: center;
}

.title-block h1 {
    margin: 5px;
    font-size: clamp(38px, 7vw, 78px);
    letter-spacing: 8px;
}

.title-block h2 {
    color: #75623d;
    letter-spacing: 5px;
}

.eyebrow {
    color: #75694e;
    font-family: monospace;
    letter-spacing: 4px;
}

.briefing {
    max-width: 950px;
    margin: 20px auto;
    text-align: left;
    line-height: 1.65;
}

.typewriter {
    font-family: "Courier New", monospace;
}

h2 {
    margin: 5px 0 15px;
    font-size: clamp(25px, 4vw, 42px);
}

h3 {
    margin-top: 8px;
}

.start-buttons {
    display: flex;
    justify-content: center;
    gap: 15px;
    flex-wrap: wrap;
}

.btn {
    padding: 12px 20px;
    color: #eee7d4;
    background: #403c30;
    border: 2px solid #a99869;
    box-shadow: 0 3px 7px #000;
    cursor: pointer;
    font-weight: bold;
    letter-spacing: 1px;
    transition: .15s;
}

.btn:hover {
    background: #665d47;
    transform: translateY(-2px);
}

.btn.primary {
    background: #263d2b;
    border-color: #8eae83;
}

.btn.danger {
    background: #512923;
    border-color: #bd776b;
}

.btn.large {
    padding: 15px 30px;
    font-size: 18px;
}

/* =========================================================
   COMMAND HEADER
   ========================================================= */

.command-header {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    gap: 12px;
    align-items: stretch;
    margin-bottom: 15px;
}

.player-card {
    padding: 12px;
    background: #2b2922;
    border: 2px solid #887950;
}

.player-card.player1 {
    border-left: 6px solid #788f9f;
}

.player-card.player2 {
    border-right: 6px solid #9b6359;
}

.player-name {
    font-size: 20px;
    font-weight: bold;
}

.score {
    font-family: monospace;
    font-size: 30px;
}

.round-box {
    padding: 10px 25px;
    text-align: center;
    background: #181713;
    border: 2px solid #a99869;
}

.round-number {
    font-size: 30px;
    font-weight: bold;
}

/* =========================================================
   RESOURCES
   ========================================================= */

.resources {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 7px;
    margin-top: 10px;
}

.resource {
    padding: 6px;
    background: #171612;
    border: 1px solid #625a47;
}

.resource-name {
    color: #bbb096;
    font-size: 10px;
    text-transform: uppercase;
}

.resource-value {
    font-family: monospace;
    font-size: 17px;
}

.bar {
    height: 6px;
    margin-top: 4px;
    background: #3a372e;
}

.bar-fill {
    height: 100%;
    background: #879b70;
}

/* =========================================================
   BATTLE GRID
   ========================================================= */

.battle-grid {
    display: grid;
    grid-template-columns: 1fr 1.7fr 1fr;
    gap: 14px;
}

.command-side {
    padding: 15px;
    background: #292720;
    border: 2px solid #665d48;
}

.command-side h3 {
    padding-bottom: 8px;
    border-bottom: 1px solid #766c54;
}

.map-area {
    position: relative;
    min-height: 450px;
    overflow: hidden;
    background:
        linear-gradient(rgba(47,66,64,.8), rgba(31,45,43,.9)),
        repeating-linear-gradient(
            45deg,
            transparent 0,
            transparent 30px,
            rgba(180,170,120,.06) 31px,
            rgba(180,170,120,.06) 32px
        );
    border: 3px solid #8d815d;
}

.map-title {
    position: absolute;
    top: 12px;
    left: 15px;
    z-index: 2;
    color: #d0c7a9;
    font-family: monospace;
    font-size: 12px;
    letter-spacing: 2px;
}

.grid-lines {
    position: absolute;
    inset: 0;
    background:
        linear-gradient(
            to right,
            transparent 49.7%,
            rgba(220,210,170,.25) 50%,
            transparent 50.3%
        ),
        linear-gradient(
            to bottom,
            transparent 49.7%,
            rgba(220,210,170,.25) 50%,
            transparent 50.3%
        );
}

.map-label {
    position: absolute;
    color: #d0c7a9;
    font-family: monospace;
    opacity: .7;
}

.island {
    position: absolute;
    padding: 6px 10px;
    color: #211f19;
    background: #746d52;
    border: 2px solid #9b8d67;
    font-family: monospace;
    font-size: 11px;
    transform: rotate(-4deg);
}

.carrier {
    position: absolute;
    z-index: 3;
    color: #ddd4b8;
    font-size: 38px;
    filter: grayscale(1);
    text-shadow: 2px 2px #000;
}

.carrier.enemy {
    transform: rotate(180deg);
}

/* =========================================================
   SCENARIO
   ========================================================= */

.scenario {
    margin-top: 15px;
    padding: 22px;
    color: #29271f;
    background: #dcd3b9;
    border: 3px solid #403b2e;
    box-shadow: 0 5px 15px #000;
}

.scenario-number {
    color: #705f3c;
    font-family: monospace;
    letter-spacing: 2px;
}

.scenario-title {
    margin: 7px 0;
    font-size: clamp(24px, 4vw, 38px);
}

.historical-note {
    margin: 15px 0;
    padding: 10px 14px;
    background: rgba(91,76,48,.12);
    border-left: 5px solid #776442;
    font-size: 14px;
}

.options {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    margin-top: 18px;
}

.option {
    min-height: 125px;
    padding: 16px;
    color: #26241f;
    background: #f0e8d0;
    border: 2px solid #76694f;
    cursor: pointer;
    text-align: left;
    transition: .15s;
}

.option:hover {
    background: #fff8e3;
    border-color: #403b2e;
    transform: translateY(-2px);
}

.option.selected {
    background: #d6e0ce;
    border: 4px solid #263d2b;
}

.option-title {
    margin-bottom: 7px;
    font-size: 18px;
    font-weight: bold;
}

/* =========================================================
   RESULT
   ========================================================= */

.result {
    margin-top: 18px;
    padding: 20px;
    background: #27251f;
    border: 2px solid #a99869;
}

.result-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
}

.result-card {
    padding: 15px;
    border: 1px solid #665d48;
}

.result-card.good {
    border-color: #7f9d71;
}

.result-card.bad {
    border-color: #9c625a;
}

/* =========================================================
   TOURNAMENT
   ========================================================= */

.bracket {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    overflow-x: auto;
}

.bracket-round {
    min-width: 220px;
}

.bracket-match {
    margin: 15px 0;
    padding: 12px;
    background: #2b2922;
    border: 1px solid #766c54;
}

.winner {
    color: #a9c39b;
    font-weight: bold;
}

.loser {
    color: #b47c72;
}

.footer {
    padding: 20px;
    color: #9f967f;
    font-family: monospace;
    font-size: 11px;
    text-align: center;
}

.warning {
    padding: 12px;
    margin: 15px 0;
    background: #514229;
    border: 2px solid #9b8450;
    color: #f0e6c9;
}

@media(max-width: 950px) {

    .battle-grid {
        grid-template-columns: 1fr;
    }

    .command-header {
        grid-template-columns: 1fr;
    }

    .resources {
        grid-template-columns: repeat(3, 1fr);
    }
}

@media(max-width: 650px) {

    .options {
        grid-template-columns: 1fr;
    }

    .resources {
        grid-template-columns: repeat(2, 1fr);
    }

    .document {
        padding: 18px;
    }
}
</style>
</head>

<body>

<header class="header">
    <h1>Pacific Theatre War Game</h1>

    <div class="subtitle">
        CARRIER STRIKE GROUP VS. CARRIER STRIKE GROUP
    </div>
</header>


<!-- =========================================================
     START SCREEN
     ========================================================= -->

<section id="startScreen" class="screen">

    <div class="document title-block">

        <div class="stamp">
            TOP SECRET — PACIFIC FLEET
        </div>

        <div class="eyebrow">
            OFFICER COMMAND TRAINING DIVISION
        </div>

        <h1>
            PACIFIC<br>THEATRE
        </h1>

        <h2>
            WAR GAME
        </h2>

        <p class="typewriter">
            CARRIER STRIKE GROUP COMMAND SIMULATION
        </p>

        <div class="briefing">

            <h3>
                MISSION BRIEFING
            </h3>

            <p>
                Two commanders will face ten rounds of tactical
                decisions based upon the realities of carrier warfare
                in the Pacific during World War II.
            </p>

            <p>
                Your objective is not simply to destroy the enemy.
                You must manage aircraft, intelligence, carrier
                readiness, reconnaissance, fuel and operational
                objectives.
            </p>

            <p>
                Every decision changes the conditions of later rounds.
                A commander who wins one engagement may lose the battle
                through poor resource management.
            </p>

            <div class="warning">

                <strong>ANTI-REPEAT SYSTEM:</strong>

                Every scenario has a unique identification number.
                A scenario cannot appear twice during the same battle.
                When a battle ends, the ten scenarios used in that
                battle are locked out of the next battle.
                
                The game therefore creates a different tactical
                sequence for the next matchup whenever enough unused
                scenarios are available.

            </div>

        </div>

        <div class="start-buttons">

            <button
                class="btn primary large"
                onclick="startNewTournament()">

                BEGIN TOURNAMENT

            </button>

            <button
                class="btn large"
                onclick="showRules()">

                COMMANDER'S RULES

            </button>

        </div>

    </div>

</section>


<!-- =========================================================
     RULES SCREEN
     ========================================================= -->

<section id="rulesScreen" class="screen hidden">

    <div class="document">

        <div class="stamp">
            FIELD MANUAL
        </div>

        <h2>
            COMMANDER'S RULES
        </h2>

        <h3>
            1. TWO COMMANDERS
        </h3>

        <p>
            Two students use one computer. Commander A makes a decision
            first. The computer then hides that decision and passes
            command to Commander B.
        </p>

        <h3>
            2. TEN ROUNDS
        </h3>

        <p>
            Each battle lasts exactly ten rounds.
        </p>

        <h3>
            3. EVERY ROUND MATTERS
        </h3>

        <p>
            Decisions can change aircraft, intelligence, readiness,
            fuel, mission progress and victory points.
        </p>

        <h3>
            4. NO REPEATS
        </h3>

        <p>
            A scenario can only be used once during a battle.
        </p>

        <p>
            When the battle ends, its scenarios are stored in memory.
            The next battle excludes those scenarios.
        </p>

        <h3>
            5. THREE WAYS TO WIN
        </h3>

        <ul>

            <li>
                <strong>Fleet Victory:</strong>
                Gain victory points through successful attacks.
            </li>

            <li>
                <strong>Mission Victory:</strong>
                Complete operational objectives.
            </li>

            <li>
                <strong>Command Victory:</strong>
                Preserve aircraft, readiness and intelligence.
            </li>

        </ul>

        <h3>
            6. THE NEXT MATCH
        </h3>

        <p>
            The winner advances to face another commander.
            The previous battle's scenarios remain locked out.
        </p>

        <button
            class="btn primary"
            onclick="backToStart()">

            RETURN TO BRIEFING

        </button>

    </div>

</section>


<!-- =========================================================
     GAME SCREEN
     ========================================================= -->

<section id="gameScreen" class="screen hidden">

    <div class="command-header">

        <div class="player-card player1">

            <div class="player-name">
                COMMANDER A
            </div>

            <div class="score">
                <span id="scoreA">0</span> VP
            </div>

            <div
                class="resources"
                id="resourcesA">
            </div>

        </div>


        <div class="round-box">

            <div>
                ROUND
            </div>

            <div class="round-number">
                <span id="roundNumber">1</span>/10
            </div>

            <div style="font-size:11px;">
                BATTLE
                <span id="battleNumber">1</span>
            </div>

        </div>


        <div class="player-card player2">

            <div class="player-name">
                COMMANDER B
            </div>

            <div class="score">
                <span id="scoreB">0</span> VP
            </div>

            <div
                class="resources"
                id="resourcesB">
            </div>

        </div>

    </div>


    <div class="battle-grid">

        <div class="command-side">

            <h3>
                COMMANDER A
            </h3>

            <p>
                U.S. CARRIER TASK FORCE
            </p>

            <p class="typewriter">
                COMMAND STATUS
            </p>

            <div id="statusA"></div>

        </div>


        <div class="map-area">

            <div class="map-title">
                PACIFIC OPERATIONS — TACTICAL PLOT
            </div>

            <div class="grid-lines"></div>

            <div
                class="map-label"
                style="top:15%;left:8%;">
                10° N
            </div>

            <div
                class="map-label"
                style="top:50%;left:8%;">
                0°
            </div>

            <div
                class="map-label"
                style="top:82%;left:8%;">
                10° S
            </div>

            <div
                class="island"
                style="top:22%;left:24%;">
                MIDWAY
            </div>

            <div
                class="island"
                style="top:66%;left:67%;">
                GUADALCANAL
            </div>

            <div
                class="island"
                style="top:38%;left:74%;">
                PHILIPPINES
            </div>

            <div
                class="island"
                style="top:72%;left:28%;">
                SOLOMONS
            </div>

            <div
                class="carrier"
                style="top:47%;left:29%;">
                ⚓
            </div>

            <div
                class="carrier enemy"
                style="top:34%;left:61%;">
                ⚓
            </div>

        </div>


        <div class="command-side">

            <h3>
                COMMANDER B
            </h3>

            <p>
                IMPERIAL JAPANESE CARRIER FORCE
            </p>

            <p class="typewriter">
                COMMAND STATUS
            </p>

            <div id="statusB"></div>

        </div>

    </div>


    <div id="scenarioContainer"></div>

</section>


<!-- =========================================================
     FINAL SCREEN
     ========================================================= -->

<section id="finalScreen" class="screen hidden">

    <div class="document">

        <div class="stamp">
            AFTER ACTION REPORT
        </div>

        <h2 id="finalTitle">
            BATTLE COMPLETE
        </h2>

        <div id="finalResults"></div>

        <hr>

        <h3>
            HISTORICAL COMMAND REVIEW
        </h3>

        <p>
            Pacific carrier warfare required commanders to balance
            reconnaissance, aircraft availability, defensive fighters,
            offensive strikes, carrier positioning, logistics and
            operational objectives.
        </p>

        <p>
            A commander could win a tactical exchange and still place
            the carrier force in danger by exhausting aircraft or
            neglecting defense.
        </p>

        <h3>
            SCENARIOS USED THIS BATTLE
        </h3>

        <div id="usedScenarioList"></div>

        <br>

        <button
            class="btn primary large"
            onclick="beginNextBattle()">

            NEXT BATTLE

        </button>

        <button
            class="btn large"
            onclick="showTournament()">

            VIEW TOURNAMENT

        </button>

    </div>

</section>


<!-- =========================================================
     TOURNAMENT SCREEN
     ========================================================= -->

<section id="tournamentScreen" class="screen hidden">

    <div class="document">

        <div class="stamp">
            PACIFIC FLEET CHAMPIONSHIP
        </div>

        <h2>
            COMMANDER TOURNAMENT
        </h2>

        <div id="tournamentContent"></div>

        <br>

        <button
            class="btn primary large"
            onclick="beginNextBattle()">

            NEW MATCH

        </button>

        <button
            class="btn"
            onclick="resetTournament()">

            RESET TOURNAMENT

        </button>

    </div>

</section>


<footer class="footer">
    PACIFIC THEATRE WAR GAME — CLASSROOM COMMAND SIMULATION
</footer>


<script>

/* =========================================================
   SCENARIO DATABASE
   =========================================================

   Every scenario has a UNIQUE ID.

   The game does not use the title to determine repetition.

   The ID is what the anti-repeat system tracks.

   There are deliberately more than 20 scenarios so that
   consecutive ten-round matches can use substantially
   different situations.
   ========================================================= */

const SCENARIOS = [

/* =========================================================
   1
   ========================================================= */

{
    id:"midway-search",
    title:"FIND THE ENEMY FLEET",
    type:"INTELLIGENCE",
    historical:"Midway — June 1942",

    description:
    "Reconnaissance reports indicate that an enemy carrier force may be approaching. Search aircraft are limited.",

    options:[

        {
            title:"WIDE SEARCH",
            text:"Spread reconnaissance aircraft across a broad search pattern.",
            a:{intel:12,aircraft:-4,score:7},
            b:{intel:12,aircraft:-4,score:7}
        },

        {
            title:"CONCENTRATED SEARCH",
            text:"Concentrate aircraft along the most likely approach.",
            a:{intel:18,aircraft:-3,score:10},
            b:{intel:18,aircraft:-3,score:10}
        },

        {
            title:"PRESERVE AIRCRAFT",
            text:"Use minimal reconnaissance and preserve aircraft for combat.",
            a:{intel:-8,aircraft:5,score:-2},
            b:{intel:-8,aircraft:5,score:-2}
        },

        {
            title:"MULTIPLE SECTORS",
            text:"Use several small search groups to reduce the chance of missing the enemy.",
            a:{intel:8,aircraft:-5,score:5},
            b:{intel:8,aircraft:-5,score:5}
        }

    ]
},


/* =========================================================
   2
   ========================================================= */

{
    id:"coral-sea-strike",
    title:"BUILD THE STRIKE",
    type:"AIR STRIKE",
    historical:"Battle of the Coral Sea — May 1942",

    description:
    "Enemy carriers have been located. You have a limited number of aircraft available for the first strike.",

    options:[

        {
            title:"HEAVY DIVE-BOMBER STRIKE",
            text:"Commit the majority of dive bombers against the carrier.",
            a:{aircraft:-12,score:15,readiness:-8},
            b:{aircraft:-12,score:15,readiness:-8}
        },

        {
            title:"BALANCED STRIKE",
            text:"Combine fighters, dive bombers and torpedo bombers.",
            a:{aircraft:-9,score:11,readiness:-4},
            b:{aircraft:-9,score:11,readiness:-4}
        },

        {
            title:"TORPEDO ATTACK",
            text:"Commit a concentrated low-level attack against the carrier.",
            a:{aircraft:-10,score:13,readiness:-6},
            b:{aircraft:-10,score:13,readiness:-6}
        },

        {
            title:"LIMITED STRIKE",
            text:"Launch a smaller strike while keeping a larger reserve.",
            a:{aircraft:-5,score:6,readiness:3},
            b:{aircraft:-5,score:6,readiness:3}
        }

    ]
},


/* =========================================================
   3
   ========================================================= */

{
    id:"cap-defense",
    title:"PROTECT THE CARRIER",
    type:"DEFENSE",
    historical:"Early Pacific Carrier Warfare",

    description:
    "Radar and reconnaissance suggest enemy aircraft may be approaching. How much of your fighter force will remain on combat air patrol?",

    options:[

        {
            title:"MAXIMUM CAP",
            text:"Keep a large fighter screen over the carrier.",
            a:{aircraft:-3,readiness:10,score:8},
            b:{aircraft:-3,readiness:10,score:8}
        },

        {
            title:"BALANCED CAP",
            text:"Maintain a moderate defensive fighter force.",
            a:{aircraft:-2,readiness:5,score:6},
            b:{aircraft:-2,readiness:5,score:6}
        },

        {
            title:"MINIMUM CAP",
            text:"Commit most fighters to offensive operations.",
            a:{aircraft:2,readiness:-8,score:9},
            b:{aircraft:2,readiness:-8,score:9}
        },

        {
            title:"ROTATING CAP",
            text:"Cycle fighters between defense and reserve.",
            a:{aircraft:-1,readiness:7,score:7},
            b:{aircraft:-1,readiness:7,score:7}
        }

    ]
},


/* =========================================================
   4
   ========================================================= */

{
    id:"damage-control",
    title:"CARRIER UNDER ATTACK",
    type:"DAMAGE CONTROL",
    historical:"Pacific Carrier Warfare",

    description:
    "Bomb damage has caused fires and disrupted flight operations. Damage-control teams can concentrate on only one major problem.",

    options:[

        {
            title:"FLIGHT DECK",
            text:"Restore the ability to launch and recover aircraft.",
            a:{readiness:15,score:9},
            b:{readiness:15,score:9}
        },

        {
            title:"ENGINEERING",
            text:"Protect propulsion and maintain maneuverability.",
            a:{readiness:8,score:7},
            b:{readiness:8,score:7}
        },

        {
            title:"FIRE CONTROL",
            text:"Concentrate on containing fires before they spread.",
            a:{readiness:12,score:10},
            b:{readiness:12,score:10}
        },

        {
            title:"AIRCRAFT SYSTEMS",
            text:"Prioritize aircraft elevators and aviation fuel systems.",
            a:{readiness:10,score:8},
            b:{readiness:10,score:8}
        }

    ]
},


/* =========================================================
   5
   ========================================================= */

{
    id:"night-contact",
    title:"UNKNOWN CONTACT",
    type:"RADAR",
    historical:"Pacific Night Operations",

    description:
    "A radar contact appears on the tactical plot. Range and bearing are known, but the identity of the force is uncertain.",

    options:[

        {
            title:"CLOSE THE RANGE",
            text:"Move toward the contact to identify it.",
            a:{intel:10,readiness:-8,score:10},
            b:{intel:10,readiness:-8,score:10}
        },

        {
            title:"MAINTAIN COURSE",
            text:"Hold position and gather additional information.",
            a:{intel:14,score:8},
            b:{intel:14,score:8}
        },

        {
            title:"TURN AWAY",
            text:"Avoid exposing the carrier group until the contact is identified.",
            a:{intel:-4,readiness:8,score:4},
            b:{intel:-4,readiness:8,score:4}
        },

        {
            title:"LAUNCH RECON",
            text:"Send a limited reconnaissance element to identify the contact.",
            a:{intel:16,aircraft:-3,score:11},
            b:{intel:16,aircraft:-3,score:11}
        }

    ]
},


/* =========================================================
   6
   ========================================================= */

{
    id:"guadalcanal-protection",
    title:"PROTECT THE TRANSPORTS",
    type:"MISSION",
    historical:"Guadalcanal — 1942",

    description:
    "Your primary mission is not simply to destroy the enemy. A transport force must reach the objective.",

    options:[

        {
            title:"SCREEN THE TRANSPORTS",
            text:"Position your carrier force to maximize protection.",
            a:{readiness:8,score:14},
            b:{readiness:8,score:14}
        },

        {
            title:"HUNT THE ENEMY",
            text:"Move aggressively toward the enemy carrier force.",
            a:{readiness:-8,score:16},
            b:{readiness:-8,score:16}
        },

        {
            title:"SPLIT THE FORCE",
            text:"Divide the force between the transports and offensive search.",
            a:{intel:7,readiness:-5,score:12},
            b:{intel:7,readiness:-5,score:12}
        },

        {
            title:"HOLD RESERVE",
            text:"Keep a reserve carrier group ready to react.",
            a:{readiness:10,score:10},
            b:{readiness:10,score:10}
        }

    ]
},


/* =========================================================
   7
   ========================================================= */

{
    id:"pilot-shortage",
    title:"THE PILOT PROBLEM",
    type:"LOGISTICS",
    historical:"Pacific War — 1942–1944",

    description:
    "Your operational aircraft numbers are falling. Training and replacement capacity is limited.",

    options:[

        {
            title:"MAXIMUM OPERATIONS",
            text:"Continue flying missions despite increasing losses.",
            a:{aircraft:-10,score:13},
            b:{aircraft:-10,score:13}
        },

        {
            title:"PRESERVE VETERANS",
            text:"Reduce operational tempo to preserve experienced crews.",
            a:{aircraft:4,score:5,intel:5},
            b:{aircraft:4,score:5,intel:5}
        },

        {
            title:"REORGANIZE AIR GROUP",
            text:"Rebalance aircraft between fighters and strike aircraft.",
            a:{aircraft:2,readiness:7,score:8},
            b:{aircraft:2,readiness:7,score:8}
        },

        {
            title:"EMERGENCY REPLACEMENTS",
            text:"Accept less experienced crews to maintain sortie rates.",
            a:{aircraft:7,readiness:-8,score:9},
            b:{aircraft:7,readiness:-8,score:9}
        }

    ]
},


/* =========================================================
   8
   ========================================================= */

{
    id:"carrier-position",
    title:"TURN INTO THE WIND",
    type:"NAVIGATION",
    historical:"Carrier Flight Operations",

    description:
    "Aircraft are ready for launch. Wind direction and enemy position require a difficult decision.",

    options:[

        {
            title:"TURN INTO WIND",
            text:"Make the maneuver necessary for maximum flight-deck operations.",
            a:{readiness:12,score:10},
            b:{readiness:12,score:10}
        },

        {
            title:"MAINTAIN COURSE",
            text:"Preserve tactical position and delay launch.",
            a:{intel:6,readiness:-3,score:5},
            b:{intel:6,readiness:-3,score:5}
        },

        {
            title:"CHANGE COURSE AGGRESSIVELY",
            text:"Trade tactical positioning for immediate launch opportunity.",
            a:{readiness:8,score:12},
            b:{readiness:8,score:12}
        },

        {
            title:"DELAY LAUNCH",
            text:"Wait for a more favorable tactical position.",
            a:{readiness:5,aircraft:2,score:4},
            b:{readiness:5,aircraft:2,score:4}
        }

    ]
},


/* =========================================================
   9
   ========================================================= */

{
    id:"counterattack",
    title:"THE COUNTERSTRIKE",
    type:"COUNTERATTACK",
    historical:"Midway / Coral Sea Carrier Warfare",

    description:
    "Enemy aircraft are returning to their carrier. Decide whether to immediately launch another strike or preserve your force.",

    options:[

        {
            title:"IMMEDIATE STRIKE",
            text:"Launch before the enemy can fully recover its aircraft.",
            a:{aircraft:-10,score:16,readiness:-9},
            b:{aircraft:-10,score:16,readiness:-9}
        },

        {
            title:"REARM AND WAIT",
            text:"Preserve aircraft while preparing the next coordinated strike.",
            a:{aircraft:-2,readiness:9,score:8},
            b:{aircraft:-2,readiness:9,score:8}
        },

        {
            title:"RECON FIRST",
            text:"Confirm the enemy's position before committing the strike.",
            a:{intel:15,aircraft:-4,score:10},
            b:{intel:15,aircraft:-4,score:10}
        },

        {
            title:"DEFENSIVE POSTURE",
            text:"Prepare for the enemy's counterattack instead.",
            a:{readiness:14,score:7},
            b:{readiness:14,score:7}
        }

    ]
},


/* =========================================================
   10
   ========================================================= */

{
    id:"philippine-sea",
    title:"THE GREAT CARRIER BATTLE",
    type:"FLEET ACTION",
    historical:"Battle of the Philippine Sea — June 1944",

    description:
    "A large enemy carrier force is detected. Your aircraft must operate over a considerable distance.",

    options:[

        {
            title:"LONG-RANGE STRIKE",
            text:"Commit aircraft despite the difficult return flight.",
            a:{aircraft:-12,score:18,readiness:-10},
            b:{aircraft:-12,score:18,readiness:-10}
        },

        {
            title:"CLOSE THE DISTANCE",
            text:"Maneuver before launching the main strike.",
            a:{readiness:-5,intel:10,score:13},
            b:{readiness:-5,intel:10,score:13}
        },

        {
            title:"DEFENSIVE FIGHTER SCREEN",
            text:"Use fighters to defeat incoming enemy aircraft.",
            a:{aircraft:-5,readiness:12,score:12},
            b:{aircraft:-5,readiness:12,score:12}
        },

        {
            title:"PRESERVE THE FORCE",
            text:"Avoid excessive losses and maintain combat power.",
            a:{aircraft:5,readiness:8,score:7},
            b:{aircraft:5,readiness:8,score:7}
        }

    ]
},


/* =========================================================
   11
   ========================================================= */

{
    id:"leyte-deception",
    title:"THE DECEPTION",
    type:"INTELLIGENCE",
    historical:"Leyte Gulf — October 1944",

    description:
    "Reports indicate that a powerful enemy force may be attempting to draw your carrier force away from the invasion area.",

    options:[

        {
            title:"PURSUE THE DECOY",
            text:"Move toward the reported enemy carriers.",
            a:{intel:-5,readiness:-10,score:14},
            b:{intel:-5,readiness:-10,score:14}
        },

        {
            title:"PROTECT THE INVASION FORCE",
            text:"Maintain the primary mission and hold position.",
            a:{readiness:12,score:15},
            b:{readiness:12,score:15}
        },

        {
            title:"SPLIT THE FORCE",
            text:"Send part of the force toward the reported carriers.",
            a:{intel:8,readiness:-7,score:12},
            b:{intel:8,readiness:-7,score:12}
        },

        {
            title:"VERIFY FIRST",
            text:"Demand additional reconnaissance before committing.",
            a:{intel:15,score:10},
            b:{intel:15,score:10}
        }

    ]
},


/* =========================================================
   12
   ========================================================= */

{
    id:"torpedo-defense",
    title:"TORPEDO ALARM",
    type:"DEFENSE",
    historical:"Pacific Carrier Warfare",

    description:
    "Torpedo bombers have been detected approaching at low altitude. Your fighter defense must respond immediately.",

    options:[

        {
            title:"INTERCEPT",
            text:"Commit fighters directly against the torpedo bombers.",
            a:{aircraft:-6,readiness:13,score:14},
            b:{aircraft:-6,readiness:13,score:14}
        },

        {
            title:"EVASIVE MANEUVER",
            text:"Turn the carrier force to reduce the torpedo threat.",
            a:{readiness:10,score:10},
            b:{readiness:10,score:10}
        },

        {
            title:"COMBINED DEFENSE",
            text:"Use fighters and destroyer screening together.",
            a:{aircraft:-4,readiness:12,score:13},
            b:{aircraft:-4,readiness:12,score:13}
        },

        {
            title:"MAINTAIN COURSE",
            text:"Avoid disrupting current flight operations.",
            a:{readiness:-7,score:7},
            b:{readiness:-7,score:7}
        }

    ]
},


/* =========================================================
   13
   ========================================================= */

{
    id:"aircraft-on-deck",
    title:"AIRCRAFT ON DECK",
    type:"OPPORTUNITY",
    historical:"Midway — June 1942",

    description:
    "Reconnaissance indicates that the enemy may have aircraft on its carrier deck. The opportunity is fleeting.",

    options:[

        {
            title:"STRIKE NOW",
            text:"Commit aircraft immediately.",
            a:{aircraft:-11,score:20,readiness:-8},
            b:{aircraft:-11,score:20,readiness:-8}
        },

        {
            title:"CONFIRM TARGET",
            text:"Obtain another reconnaissance report before attacking.",
            a:{intel:12,aircraft:-3,score:9},
            b:{intel:12,aircraft:-3,score:9}
        },

        {
            title:"SMALL STRIKE",
            text:"Send a limited force to test the enemy defense.",
            a:{aircraft:-5,score:11,readiness:-2},
            b:{aircraft:-5,score:11,readiness:-2}
        },

        {
            title:"HOLD FIRE",
            text:"Preserve the strike group for a more certain opportunity.",
            a:{aircraft:4,readiness:5,score:4},
            b:{aircraft:4,readiness:5,score:4}
        }

    ]
},


/* =========================================================
   14
   ========================================================= */

{
    id:"destroyer-screen",
    title:"BREAK THE SCREEN",
    type:"SURFACE ACTION",
    historical:"Carrier Task Force Operations",

    description:
    "Enemy destroyers are protecting the carrier force. Your strike group must decide how to approach the screen.",

    options:[

        {
            title:"ATTACK THE SCREEN",
            text:"Use aircraft against the destroyers.",
            a:{aircraft:-7,score:11,readiness:4},
            b:{aircraft:-7,score:11,readiness:4}
        },

        {
            title:"BYPASS THE SCREEN",
            text:"Concentrate directly on the carriers.",
            a:{aircraft:-6,score:15,readiness:-6},
            b:{aircraft:-6,score:15,readiness:-6}
        },

        {
            title:"USE CRUISER SUPPORT",
            text:"Coordinate surface ships with aircraft.",
            a:{readiness:-4,score:12},
            b:{readiness:-4,score:12}
        },

        {
            title:"WAIT",
            text:"Allow reconnaissance to clarify the enemy formation.",
            a:{intel:10,score:6,readiness:4},
            b:{intel:10,score:6,readiness:4}
        }

    ]
},


/* =========================================================
   15
   ========================================================= */

{
    id:"final-command",
    title:"THE FINAL COMMAND",
    type:"COMMAND DECISION",
    historical:"Pacific Carrier Warfare",

    description:
    "Both carrier forces are damaged. The enemy remains dangerous. Your final decision may determine whether you preserve the fleet or risk everything for victory.",

    options:[

        {
            title:"ALL-IN STRIKE",
            text:"Commit nearly every available aircraft.",
            a:{aircraft:-15,readiness:-15,score:25},
            b:{aircraft:-15,readiness:-15,score:25}
        },

        {
            title:"CONTROLLED ATTACK",
            text:"Launch a limited strike while preserving reserves.",
            a:{aircraft:-7,readiness:5,score:17},
            b:{aircraft:-7,readiness:5,score:17}
        },

        {
            title:"DEFEND THE FORCE",
            text:"Preserve your remaining carriers and aircraft.",
            a:{aircraft:5,readiness:15,score:10},
            b:{aircraft:5,readiness:15,score:10}
        },

        {
            title:"MISSION FIRST",
            text:"Ignore the enemy carrier and complete the operational objective.",
            a:{readiness:7,intel:5,score:22},
            b:{readiness:7,intel:5,score:22}
        }

    ]
},


/* =========================================================
   16
   ========================================================= */

{
    id:"search-sector",
    title:"SELECT THE SEARCH SECTOR",
    type:"RECONNAISSANCE",
    historical:"Carrier Reconnaissance — Pacific 1942",

    description:
    "A reconnaissance report places an enemy force somewhere northwest of your position. Aircraft are insufficient to search every sector.",

    options:[

        {
            title:"NORTHWEST",
            text:"Search the sector most directly supported by the report.",
            a:{intel:16,aircraft:-5,score:11},
            b:{intel:16,aircraft:-5,score:11}
        },

        {
            title:"WEST",
            text:"Search farther west in case the enemy has changed course.",
            a:{intel:10,aircraft:-4,score:8},
            b:{intel:10,aircraft:-4,score:8}
        },

        {
            title:"NORTH",
            text:"Search the northern approach to guard against a flanking movement.",
            a:{intel:8,aircraft:-4,score:7},
            b:{intel:8,aircraft:-4,score:7}
        },

        {
            title:"SPLIT SEARCH",
            text:"Divide the available aircraft between two likely sectors.",
            a:{intel:13,aircraft:-7,score:10},
            b:{intel:13,aircraft:-7,score:10}
        }

    ]
},


/* =========================================================
   17
   ========================================================= */

{
    id:"fighter-reserve",
    title:"KEEP A RESERVE",
    type:"AIR DEFENSE",
    historical:"Carrier Air Group Operations",

    description:
    "Your strike aircraft are preparing for launch. The enemy may still have aircraft capable of attacking your carrier.",

    options:[

        {
            title:"LARGE RESERVE",
            text:"Keep a substantial fighter reserve on the carrier.",
            a:{aircraft:-2,readiness:12,score:7},
            b:{aircraft:-2,readiness:12,score:7}
        },

        {
            title:"SMALL RESERVE",
            text:"Keep only a limited fighter force available.",
            a:{aircraft:1,readiness:5,score:9},
            b:{aircraft:1,readiness:5,score:9}
        },

        {
            title:"NO RESERVE",
            text:"Commit nearly every fighter to the offensive.",
            a:{aircraft:3,readiness:-12,score:14},
            b:{aircraft:3,readiness:-12,score:14}
        },

        {
            title:"ROTATE FIGHTERS",
            text:"Maintain a reserve by cycling aircraft between missions.",
            a:{aircraft:-1,readiness:9,score:10},
            b:{aircraft:-1,readiness:9,score:10}
        }

    ]
},


/* =========================================================
   18
   ========================================================= */

{
    id:"weather-front",
    title:"WEATHER FRONT",
    type:"NAVIGATION",
    historical:"Pacific Weather Conditions",

    description:
    "A weather front is moving between the carrier groups. Visibility is deteriorating and aircraft operations are becoming more difficult.",

    options:[

        {
            title:"PRESS THROUGH",
            text:"Continue operations before the weather becomes worse.",
            a:{aircraft:-7,score:13,readiness:-5},
            b:{aircraft:-7,score:13,readiness:-5}
        },

        {
            title:"WAIT",
            text:"Delay major operations until visibility improves.",
            a:{readiness:8,intel:7,score:6},
            b:{readiness:8,intel:7,score:6}
        },

        {
            title:"REPOSITION",
            text:"Move the carrier group around the weather front.",
            a:{fuel:-7,intel:10,score:9},
            b:{fuel:-7,intel:10,score:9}
        },

        {
            title:"LIMITED RECON",
            text:"Use a small reconnaissance element while preserving the main force.",
            a:{aircraft:-3,intel:13,score:8},
            b:{aircraft:-3,intel:13,score:8}
        }

    ]
},


/* =========================================================
   19
   ========================================================= */

{
    id:"fuel-crisis",
    title:"FUEL CALCULATION",
    type:"LOGISTICS",
    historical:"Extended Pacific Operations",

    description:
    "The carrier group has been operating for days. Fuel reserves are falling while the enemy remains active.",

    options:[

        {
            title:"CONTINUE OPERATIONS",
            text:"Accept the fuel risk and maintain the current tempo.",
            a:{fuel:-15,score:14},
            b:{fuel:-15,score:14}
        },

        {
            title:"REDUCE SPEED",
            text:"Conserve fuel and reduce unnecessary movement.",
            a:{fuel:-5,readiness:5,score:7},
            b:{fuel:-5,readiness:5,score:7}
        },

        {
            title:"WITHDRAW TEMPORARILY",
            text:"Move toward a safer position and preserve fuel.",
            a:{fuel:12,score:4,readiness:8},
            b:{fuel:12,score:4,readiness:8}
        },

        {
            title:"REPLENISH",
            text:"Prioritize a refueling operation before the next major action.",
            a:{fuel:18,readiness:-3,score:6},
            b:{fuel:18,readiness:-3,score:6}
        }

    ]
},


/* =========================================================
   20
   ========================================================= */

{
    id:"submarine-warning",
    title:"SUBMARINE CONTACT",
    type:"ANTI-SUBMARINE",
    historical:"Pacific Fleet Submarine Warfare",

    description:
    "A submarine contact has been reported near the carrier force. Destroyers can investigate, but doing so may pull them away from the carrier screen.",

    options:[

        {
            title:"ATTACK CONTACT",
            text:"Send destroyers to investigate and attack the submarine.",
            a:{readiness:8,score:11},
            b:{readiness:8,score:11}
        },

        {
            title:"MAINTAIN SCREEN",
            text:"Keep destroyers around the carrier force.",
            a:{readiness:12,score:8},
            b:{readiness:12,score:8}
        },

        {
            title:"EVASIVE COURSE",
            text:"Change course to reduce the submarine's firing opportunity.",
            a:{fuel:-5,readiness:10,score:9},
            b:{fuel:-5,readiness:10,score:9}
        },

        {
            title:"AIR RECON",
            text:"Use aircraft to investigate without weakening the surface screen.",
            a:{aircraft:-3,intel:12,score:10},
            b:{aircraft:-3,intel:12,score:10}
        }

    ]
},


/* =========================================================
   21
   ========================================================= */

{
    id:"damaged-elevator",
    title:"AIRCRAFT ELEVATOR FAILURE",
    type:"DAMAGE CONTROL",
    historical:"Carrier Damage Control",

    description:
    "An aircraft elevator has been damaged. Aircraft remain aboard the carrier but cannot be moved efficiently to the flight deck.",

    options:[

        {
            title:"REPAIR ELEVATOR",
            text:"Concentrate repair crews on restoring aircraft movement.",
            a:{readiness:14,score:10},
            b:{readiness:14,score:10}
        },

        {
            title:"USE REMAINING ELEVATOR",
            text:"Continue operations using the functioning elevator.",
            a:{readiness:-3,score:9},
            b:{readiness:-3,score:9}
        },

        {
            title:"REDUCE SORTIE RATE",
            text:"Slow flight operations to avoid creating a dangerous bottleneck.",
            a:{aircraft:4,readiness:8,score:6},
            b:{aircraft:4,readiness:8,score:6}
        },

        {
            title:"EMERGENCY DECK OPERATIONS",
            text:"Attempt to maintain a high tempo despite the damage.",
            a:{aircraft:-5,readiness:-8,score:13},
            b:{aircraft:-5,readiness:-8,score:13}
        }

    ]
},


/* =========================================================
   22
   ========================================================= */

{
    id:"radio-silence",
    title:"RADIO SILENCE",
    type:"COMMUNICATIONS",
    historical:"Pacific Fleet Communications",

    description:
    "Communications with one reconnaissance element have been lost. The aircraft's last report placed the enemy somewhere east of its previous position.",

    options:[

        {
            title:"ASSUME LAST POSITION",
            text:"Continue operations based on the last confirmed report.",
            a:{intel:-3,score:9},
            b:{intel:-3,score:9}
        },

        {
            title:"SEARCH FOR AIRCRAFT",
            text:"Divert resources to locate the missing reconnaissance element.",
            a:{aircraft:-4,intel:10,score:7},
            b:{aircraft:-4,intel:10,score:7}
        },

        {
            title:"RECONSTRUCT THE PICTURE",
            text:"Combine older reports to estimate the enemy's likely movement.",
            a:{intel:15,score:10},
            b:{intel:15,score:10}
        },

        {
            title:"CHANGE PLAN",
            text:"Assume the intelligence is unreliable and alter the operation.",
            a:{intel:5,readiness:8,score:8},
            b:{intel:5,readiness:8,score:8}
        }

    ]
},


/* =========================================================
   23
   ========================================================= */

{
    id:"cruiser-bombardment",
    title:"SURFACE BOMBARDMENT",
    type:"SURFACE ACTION",
    historical:"Guadalcanal Naval Campaign",

    description:
    "Enemy surface ships may be moving toward an island objective. Your cruisers can intervene, but exposing them may create additional risk.",

    options:[

        {
            title:"SEND CRUISERS",
            text:"Commit cruisers to disrupt the enemy surface force.",
            a:{readiness:-5,score:15},
            b:{readiness:-5,score:15}
        },

        {
            title:"AIR STRIKE",
            text:"Use carrier aircraft rather than exposing surface ships.",
            a:{aircraft:-7,score:14},
            b:{aircraft:-7,score:14}
        },

        {
            title:"HOLD POSITION",
            text:"Protect the carrier force and wait for better intelligence.",
            a:{intel:10,readiness:8,score:7},
            b:{intel:10,readiness:8,score:7}
        },

        {
            title:"COMBINED FORCE",
            text:"Coordinate cruisers, destroyers and aircraft.",
            a:{aircraft:-4,readiness:-4,score:17},
            b:{aircraft:-4,readiness:-4,score:17}
        }

    ]
},


/* =========================================================
   24
   ========================================================= */

{
    id:"island-objective",
    title:"HOLD THE ISLAND",
    type:"MISSION",
    historical:"Pacific Island Campaigns",

    description:
    "Your carrier group has been ordered to support an island objective. Destroying enemy ships is secondary to maintaining control of the operational area.",

    options:[

        {
            title:"DIRECT SUPPORT",
            text:"Keep aircraft focused on supporting the island objective.",
            a:{aircraft:-5,mission:15,score:14},
            b:{aircraft:-5,mission:15,score:14}
        },

        {
            title:"HUNT CARRIERS",
            text:"Shift attention toward enemy naval forces.",
            a:{mission:-5,aircraft:-8,score:18},
            b:{mission:-5,aircraft:-8,score:18}
        },

        {
            title:"PROTECT SUPPLY LINE",
            text:"Use aircraft and surface ships to keep supplies moving.",
            a:{mission:12,readiness:7,score:12},
            b:{mission:12,readiness:7,score:12}
        },

        {
            title:"RESERVE STRIKE",
            text:"Keep aircraft ready for the most important moment.",
            a:{mission:7,aircraft:3,readiness:9,score:10},
            b:{mission:7,aircraft:3,readiness:9,score:10}
        }

    ]
},


/* =========================================================
   25
   ========================================================= */

{
    id:"carrier-withdrawal",
    title:"BREAK CONTACT",
    type:"COMMAND DECISION",
    historical:"Pacific Carrier Warfare",

    description:
    "Your carrier has taken damage and enemy reconnaissance is closing. You must decide whether to remain in the battle.",

    options:[

        {
            title:"REMAIN",
            text:"Stay in the area and continue fighting.",
            a:{readiness:-12,score:18},
            b:{readiness:-12,score:18}
        },

        {
            title:"WITHDRAW",
            text:"Preserve the carrier and move away from the enemy.",
            a:{fuel:-8,readiness:15,score:9},
            b:{fuel:-8,readiness:15,score:9}
        },

        {
            title:"COVERED WITHDRAWAL",
            text:"Use fighters and destroyers to cover the withdrawal.",
            a:{aircraft:-5,readiness:9,score:13},
            b:{aircraft:-5,readiness:9,score:13}
        },

        {
            title:"DECOY MANEUVER",
            text:"Use part of the force to draw enemy attention away from the carrier.",
            a:{readiness:-5,intel:7,score:15},
            b:{readiness:-5,intel:7,score:15}
        }

    ]
},


/* =========================================================
   26
   ========================================================= */

{
    id:"carrier-strike-cycle",
    title:"THE CARRIER STRIKE CYCLE",
    type:"FLIGHT OPERATIONS",
    historical:"Pacific Carrier Flight Operations",

    description:
    "Your carrier must launch, recover, refuel and rearm aircraft. Poor timing can create congestion and leave the carrier vulnerable.",

    options:[

        {
            title:"MAXIMUM TEMPO",
            text:"Keep launching aircraft with minimal pauses.",
            a:{aircraft:-8,score:15,readiness:-7},
            b:{aircraft:-8,score:15,readiness:-7}
        },

        {
            title:"CONTROLLED CYCLE",
            text:"Synchronize launch, recovery and rearming.",
            a:{readiness:10,score:12},
            b:{readiness:10,score:12}
        },

        {
            title:"RECOVERY FIRST",
            text:"Prioritize bringing returning aircraft safely aboard.",
            a:{aircraft:3,readiness:13,score:8},
            b:{aircraft:3,readiness:13,score:8}
        },

        {
            title:"LAUNCH FIRST",
            text:"Prioritize getting the next strike airborne.",
            a:{aircraft:-5,readiness:-3,score:14},
            b:{aircraft:-5,readiness:-3,score:14}
        }

    ]
},


/* =========================================================
   27
   ========================================================= */

{
    id:"fighter-intercept",
    title:"INTERCEPT THE RAID",
    type:"AIR DEFENSE",
    historical:"Carrier Air Defense",

    description:
    "Enemy aircraft are approaching your task force. You have limited fighters available for interception.",

    options:[

        {
            title:"EARLY INTERCEPT",
            text:"Send fighters out before the enemy reaches the carrier.",
            a:{aircraft:-6,readiness:15,score:15},
            b:{aircraft:-6,readiness:15,score:15}
        },

        {
            title:"CLOSE DEFENSE",
            text:"Keep fighters near the carrier until the threat is closer.",
            a:{aircraft:-3,readiness:11,score:11},
            b:{aircraft:-3,readiness:11,score:11}
        },

        {
            title:"SPLIT INTERCEPT",
            text:"Divide fighters between multiple approaching groups.",
            a:{aircraft:-5,intel:7,score:12},
            b:{aircraft:-5,intel:7,score:12}
        },

        {
            title:"PRESERVE FIGHTERS",
            text:"Hold some fighters back for a later counterattack.",
            a:{aircraft:1,readiness:-5,score:8},
            b:{aircraft:1,readiness:-5,score:8}
        }

    ]
},


/* =========================================================
   28
   ========================================================= */

{
    id:"decoy-report",
    title:"CONFLICTING REPORTS",
    type:"INTELLIGENCE",
    historical:"Pacific Naval Intelligence",

    description:
    "Two reconnaissance reports disagree about the enemy's location. One report is older but more reliable; the other is newer but uncertain.",

    options:[

        {
            title:"TRUST RELIABLE REPORT",
            text:"Use the older but more trustworthy intelligence.",
            a:{intel:12,score:10},
            b:{intel:12,score:10}
        },

        {
            title:"TRUST NEW REPORT",
            text:"Act immediately on the latest information.",
            a:{intel:-5,score:15},
            b:{intel:-5,score:15}
        },

        {
            title:"SEND CONFIRMATION",
            text:"Use another reconnaissance mission to resolve the disagreement.",
            a:{aircraft:-4,intel:16,score:11},
            b:{aircraft:-4,intel:16,score:11}
        },

        {
            title:"SPLIT THE SEARCH",
            text:"Search both reported locations.",
            a:{aircraft:-8,intel:11,score:12},
            b:{aircraft:-8,intel:11,score:12}
        }

    ]
},


/* =========================================================
   29
   ========================================================= */

{
    id:"damaged-radar",
    title:"RADAR FAILURE",
    type:"DAMAGE CONTROL",
    historical:"Carrier Radar Operations",

    description:
    "Your primary radar system is damaged. Repairing it requires time and resources, but operating without it increases uncertainty.",

    options:[

        {
            title:"REPAIR RADAR",
            text:"Prioritize restoring early warning capability.",
            a:{readiness:13,intel:14,score:10},
            b:{readiness:13,intel:14,score:10}
        },

        {
            title:"USE VISUAL LOOKOUTS",
            text:"Continue operations using shipboard observers.",
            a:{intel:-7,readiness:7,score:7},
            b:{intel:-7,readiness:7,score:7}
        },

        {
            title:"USE AIRBORNE RECON",
            text:"Increase reconnaissance to compensate for the radar failure.",
            a:{aircraft:-4,intel:15,score:11},
            b:{aircraft:-4,intel:15,score:11}
        },

        {
            title:"WITHDRAW",
            text:"Reduce exposure until radar capability is restored.",
            a:{fuel:-7,readiness:12,score:6},
            b:{fuel:-7,readiness:12,score:6}
        }

    ]
},


/* =========================================================
   30
   ========================================================= */

{
    id:"final-gamble",
    title:"THE COMMANDER'S GAMBLE",
    type:"FINAL DECISION",
    historical:"Pacific Carrier Warfare",

    description:
    "The enemy has suffered losses, but your own carrier force is damaged. You have one opportunity to make a decisive move.",

    options:[

        {
            title:"COMMIT EVERYTHING",
            text:"Launch the largest possible attack and accept the risk.",
            a:{aircraft:-18,readiness:-12,score:28},
            b:{aircraft:-18,readiness:-12,score:28}
        },

        {
            title:"BALANCED ATTACK",
            text:"Attack aggressively while maintaining a reserve.",
            a:{aircraft:-9,readiness:4,score:20},
            b:{aircraft:-9,readiness:4,score:20}
        },

        {
            title:"PRESERVE COMBAT POWER",
            text:"Protect the carrier force and force the enemy to take the next risk.",
            a:{aircraft:5,readiness:14,score:12},
            b:{aircraft:5,readiness:14,score:12}
        },

        {
            title:"COMPLETE THE MISSION",
            text:"Ignore the opportunity for a decisive strike and accomplish the operational objective.",
            a:{mission:12,readiness:7,score:23},
            b:{mission:12,readiness:7,score:23}
        }

    ]
}

];


/* =========================================================
   GAME STATE
   ========================================================= */

let game = {

    battleNumber: 1,

    round: 1,

    currentScenario: null,

    /*
        Scenarios used during CURRENT battle.
    */
    usedThisBattle: [],

    /*
        Scenarios used during IMMEDIATELY PREVIOUS battle.
    */
    previousBattleScenarios: [],

    /*
        Every scenario ever used during this tournament.
        This gives us additional memory and lets the game
        track long-term repetition.
    */
    tournamentScenarioHistory: [],

    tournamentHistory: [],

    players: {

        A: createPlayer("COMMANDER A"),

        B: createPlayer("COMMANDER B")

    }

};


/* =========================================================
   PLAYER CREATION
   ========================================================= */

function createPlayer(name) {

    return {

        name: name,

        score: 0,

        aircraft: 100,

        intel: 50,

        readiness: 80,

        fuel: 90,

        mission: 50

    };

}


/* =========================================================
   SCREEN CONTROL
   ========================================================= */

function hideAllScreens() {

    document
        .getElementById("startScreen")
        .classList.add("hidden");

    document
        .getElementById("rulesScreen")
        .classList.add("hidden");

    document
        .getElementById("gameScreen")
        .classList.add("hidden");

    document
        .getElementById("finalScreen")
        .classList.add("hidden");

    document
        .getElementById("tournamentScreen")
        .classList.add("hidden");

}


function showRules() {

    hideAllScreens();

    document
        .getElementById("rulesScreen")
        .classList.remove("hidden");

}


function backToStart() {

    hideAllScreens();

    document
        .getElementById("startScreen")
        .classList.remove("hidden");

}


/* =========================================================
   START NEW TOURNAMENT
   ========================================================= */

function startNewTournament() {

    game = {

        battleNumber: 1,

        round: 1,

        currentScenario: null,

        usedThisBattle: [],

        previousBattleScenarios: [],

        tournamentScenarioHistory: [],

        tournamentHistory: [],

        players: {

            A: createPlayer("COMMANDER A"),

            B: createPlayer("COMMANDER B")

        }

    };

    startBattle();

}


/* =========================================================
   START BATTLE
   ========================================================= */

function startBattle() {

    hideAllScreens();

    document
        .getElementById("gameScreen")
        .classList.remove("hidden");

    game.round = 1;

    game.usedThisBattle = [];

    game.players.A =
        createPlayer("COMMANDER A");

    game.players.B =
        createPlayer("COMMANDER B");

    updateDashboard();

    loadScenario();

}


/* =========================================================
   SCENARIO SELECTION
   =========================================================

   THIS IS THE CORE ANTI-REPEAT SYSTEM.

   Priority:

   1. Never used in current battle.
   2. Never used in previous battle.
   3. Prefer scenarios not used anywhere in tournament.
   4. If necessary, fall back to scenarios not used
      in current battle.

   Because the database currently contains 30 scenarios,
   a ten-round battle leaves at least 20 scenarios outside
   that battle.

   Therefore Battle 2 can use ten completely different
   scenarios from Battle 1.

   Battle 3 can also normally use another unique group.
   ========================================================= */

function chooseScenario() {

    let available =
        SCENARIOS.filter(scenario =>

            !game.usedThisBattle.includes(
                scenario.id
            )

            &&

            !game.previousBattleScenarios.includes(
                scenario.id
            )

        );


    /*
        Prefer scenarios never used anywhere in this
        tournament.
    */

    let neverUsedTournament =
        available.filter(scenario =>

            !game.tournamentScenarioHistory.includes(
                scenario.id
            )

        );


    if(neverUsedTournament.length >= 10) {

        available = neverUsedTournament;

    }


    /*
        If fewer than ten completely new scenarios remain,
        continue using scenarios that at least were NOT in
        the previous battle.
    */


    /*
        Absolute safety fallback.

        This prevents the game from ever repeating a scenario
        within the same ten-round battle.
    */

    if(available.length === 0) {

        available =
            SCENARIOS.filter(scenario =>

                !game.usedThisBattle.includes(
                    scenario.id
                )

            );

    }


    if(available.length === 0) {

        alert(
            "ERROR: No unused scenarios remain."
        );

        return null;

    }


    /*
        Random selection happens ONLY AFTER filtering.

        Therefore randomness cannot create an accidental repeat.
    */

    const selected =
        available[
            Math.floor(
                Math.random() * available.length
            )
        ];


    game.usedThisBattle.push(
        selected.id
    );


    game.tournamentScenarioHistory.push(
        selected.id
    );


    return selected;

}


/* =========================================================
   LOAD SCENARIO
   ========================================================= */

function loadScenario() {

    const scenario =
        chooseScenario();

    if(!scenario) return;

    game.currentScenario =
        scenario;

    document
        .getElementById("roundNumber")
        .textContent =
        game.round;

    document
        .getElementById("battleNumber")
        .textContent =
        game.battleNumber;

    renderScenario(scenario);

    updateDashboard();

}


/* =========================================================
   RENDER SCENARIO
   ========================================================= */

function renderScenario(scenario) {

    const container =
        document.getElementById(
            "scenarioContainer"
        );


    container.innerHTML = `

        <div class="scenario">

            <div class="scenario-number">

                ROUND ${game.round} OF 10

                —
                
                ${scenario.type}

            </div>


            <div class="scenario-title">

                ${scenario.title}

            </div>


            <div class="historical-note">

                <strong>
                    HISTORICAL CONTEXT:
                </strong>

                ${scenario.historical}

            </div>


            <p>
                ${scenario.description}
            </p>


            <p class="typewriter">

                COMMANDER A:
                MAKE YOUR DECISION.

            </p>


            <div class="options">

                ${scenario.options.map(
                    (option,index) => `

                    <button
                        class="option"
                        onclick="selectDecision(${index})"
                        id="option-${index}">

                        <div class="option-title">

                            ${String.fromCharCode(65 + index)}.

                            ${option.title}

                        </div>

                        <div>
                            ${option.text}
                        </div>

                    </button>

                `
                ).join("")}

            </div>


            <div
                id="decisionStatus"
                class="typewriter"
                style="margin-top:15px;">

                Awaiting Commander A...

            </div>

        </div>

    `;

}


/* =========================================================
   PLAYER DECISIONS
   ========================================================= */

let decisionA = null;

let decisionB = null;


/*
    Commander A chooses first.

    Commander B cannot see the selection.

    Then the computer passes control to Commander B.
*/

function selectDecision(index) {

    if(decisionA !== null) {
        return;
    }


    decisionA = index;


    document
        .querySelectorAll(".option")
        .forEach(button =>

            button.classList.remove(
                "selected"
            )

        );


    document
        .getElementById(
            `option-${index}`
        )
        .classList.add("selected");


    document
        .getElementById(
            "decisionStatus"
        )
        .innerHTML = `

            COMMANDER A DECISION LOCKED.

            <br><br>

            <strong>
                PASS THE COMMAND TO COMMANDER B.
            </strong>

            <br><br>

            <button
                class="btn primary"
                onclick="beginPlayerBDecision()">

                COMMANDER B —
                TAKE CONTROL

            </button>

        `;

}


/* =========================================================
   COMMANDER B DECISION SCREEN
   ========================================================= */

function beginPlayerBDecision() {

    const scenario =
        game.currentScenario;


    document
        .getElementById(
            "scenarioContainer"
        )
        .innerHTML = `

        <div class="scenario">

            <div class="scenario-number">

                ROUND ${game.round} OF 10

            </div>


            <div class="scenario-title">

                COMMANDER B —
                DECISION

            </div>


            <div class="historical-note">

                <strong>
                    CLASSIFIED:
                </strong>

                Commander A's decision is hidden.

            </div>


            <p>
                ${scenario.description}
            </p>


            <p class="typewriter">

                COMMANDER B:

                MAKE YOUR DECISION.

            </p>


            <div class="options">

                ${scenario.options.map(
                    (option,index) => `

                    <button
                        class="option"
                        onclick="selectPlayerB(${index})">

                        <div class="option-title">

                            ${String.fromCharCode(65 + index)}.

                            ${option.title}

                        </div>

                        <div>
                            ${option.text}
                        </div>

                    </button>

                `
                ).join("")}

            </div>

        </div>

    `;

}


/* =========================================================
   PLAYER B SELECTS
   ========================================================= */

function selectPlayerB(index) {

    decisionB = index;

    resolveRound();

}


/* =========================================================
   RESOLVE ROUND
   ========================================================= */

function resolveRound() {

    const scenario =
        game.currentScenario;


    const resultA =
        scenario
            .options[decisionA]
            .a;


    const resultB =
        scenario
            .options[decisionB]
            .b;


    applyResult(
        game.players.A,
        resultA
    );


    applyResult(
        game.players.B,
        resultB
    );


    /*
        Competitive tactical bonus.

        If players make different decisions,
        the stronger immediate tactical result earns
        two additional victory points.
    */

    if(decisionA !== decisionB) {

        const scoreA =
            resultA.score || 0;

        const scoreB =
            resultB.score || 0;


        if(scoreA > scoreB) {

            game.players.A.score += 2;

        }

        else if(scoreB > scoreA) {

            game.players.B.score += 2;

        }

    }


    renderRoundResult(
        scenario,
        resultA,
        resultB,
        decisionA,
        decisionB
    );


    decisionA = null;

    decisionB = null;

}


/* =========================================================
   APPLY RESULT
   ========================================================= */

function applyResult(
    player,
    result
) {

    player.score +=
        result.score || 0;

    player.aircraft +=
        result.aircraft || 0;

    player.intel +=
        result.intel || 0;

    player.readiness +=
        result.readiness || 0;

    player.fuel +=
        result.fuel || 0;

    player.mission +=
        result.mission || 0;


    player.aircraft =
        clamp(
            player.aircraft,
            0,
            100
        );


    player.intel =
        clamp(
            player.intel,
            0,
            100
        );


    player.readiness =
        clamp(
            player.readiness,
            0,
            100
        );


    player.fuel =
        clamp(
            player.fuel,
            0,
            100
        );


    player.mission =
        clamp(
            player.mission,
            0,
            100
        );

}


/* =========================================================
   CLAMP
   ========================================================= */

function clamp(
    value,
    min,
    max
) {

    return Math.max(
        min,
        Math.min(
            max,
            value
        )
    );

}


/* =========================================================
   ROUND RESULT
   ========================================================= */

function renderRoundResult(
    scenario,
    resultA,
    resultB,
    selectedA,
    selectedB
) {

    const scoreA =
        resultA.score || 0;

    const scoreB =
        resultB.score || 0;


    let comparison;


    if(scoreA > scoreB) {

        comparison =
            "COMMANDER A gains the tactical advantage.";

    }

    else if(scoreB > scoreA) {

        comparison =
            "COMMANDER B gains the tactical advantage.";

    }

    else {

        comparison =
            "Neither commander gains a tactical advantage.";

    }


    document
        .getElementById(
            "scenarioContainer"
        )
        .innerHTML = `

        <div class="result">

            <div class="stamp">
                AFTER ACTION REPORT
            </div>


            <h2>
                ROUND ${game.round}
                COMPLETE
            </h2>


            <p>
                ${comparison}
            </p>


            <div class="result-grid">


                <div
                    class="result-card
                    ${scoreA >= scoreB
                        ? "good"
                        : "bad"}">

                    <h3>
                        COMMANDER A
                    </h3>


                    <p>

                        Decision:

                        <strong>
                            ${scenario
                                .options[selectedA]
                                .title}
                        </strong>

                    </p>


                    <p>

                        Victory Points:

                        <strong>

                            ${scoreA >= 0
                                ? "+"
                                : ""}

                            ${scoreA}

                        </strong>

                    </p>

                </div>


                <div
                    class="result-card
                    ${scoreB >= scoreA
                        ? "good"
                        : "bad"}">

                    <h3>
                        COMMANDER B
                    </h3>


                    <p>

                        Decision:

                        <strong>
                            ${scenario
                                .options[selectedB]
                                .title}
                        </strong>

                    </p>


                    <p>

                        Victory Points:

                        <strong>

                            ${scoreB >= 0
                                ? "+"
                                : ""}

                            ${scoreB}

                        </strong>

                    </p>

                </div>

            </div>


            <br>


            <button
                class="btn primary large"
                onclick="nextRound()">

                ${
                    game.round < 10
                    ? "CONTINUE TO NEXT ROUND"
                    : "END BATTLE"
                }

            </button>

        </div>

    `;

}


/* =========================================================
   NEXT ROUND
   ========================================================= */

function nextRound() {

    if(game.round >= 10) {

        finishBattle();

        return;

    }


    game.round++;

    loadScenario();

}


/* =========================================================
   DASHBOARD
   ========================================================= */

function updateDashboard() {

    document
        .getElementById("scoreA")
        .textContent =
        game.players.A.score;


    document
        .getElementById("scoreB")
        .textContent =
        game.players.B.score;


    renderResources(
        "resourcesA",
        game.players.A
    );


    renderResources(
        "resourcesB",
        game.players.B
    );


    document
        .getElementById("statusA")
        .innerHTML =
        commandStatus(
            game.players.A
        );


    document
        .getElementById("statusB")
        .innerHTML =
        commandStatus(
            game.players.B
        );

}


/* =========================================================
   RESOURCES
   ========================================================= */

function renderResources(
    elementID,
    player
) {

    const container =
        document.getElementById(
            elementID
        );


    const resources = [

        [
            "Aircraft",
            player.aircraft
        ],

        [
            "Intel",
            player.intel
        ],

        [
            "Readiness",
            player.readiness
        ],

        [
            "Fuel",
            player.fuel
        ],

        [
            "Mission",
            player.mission
        ]

    ];


    container.innerHTML =
        resources.map(
            resource => `

            <div class="resource">

                <div class="resource-name">
                    ${resource[0]}
                </div>

                <div class="resource-value">
                    ${Math.round(
                        resource[1]
                    )}
                </div>

                <div class="bar">

                    <div
                        class="bar-fill"
                        style="
                            width:${resource[1]}%
                        ">
                    </div>

                </div>

            </div>

        `
        ).join("");

}


/* =========================================================
   COMMAND STATUS
   ========================================================= */

function commandStatus(player) {

    let status = [];


    if(player.aircraft < 30) {

        status.push(
            "AIRCRAFT STRENGTH LOW"
        );

    }


    if(player.readiness < 30) {

        status.push(
            "CARRIER READINESS CRITICAL"
        );

    }


    if(player.intel < 25) {

        status.push(
            "INTELLIGENCE LIMITED"
        );

    }


    if(player.fuel < 25) {

        status.push(
            "FUEL CRITICAL"
        );

    }


    if(player.mission < 25) {

        status.push(
            "MISSION PROGRESS LOW"
        );

    }


    if(status.length === 0) {

        status.push(
            "OPERATIONAL"
        );

    }


    return status.map(
        s => `

        <div
            class="typewriter"
            style="margin:5px 0;">

            ▪ ${s}

        </div>

        `
    ).join("");

}


/* =========================================================
   FINISH BATTLE
   ========================================================= */

function finishBattle() {

    const A =
        game.players.A;

    const B =
        game.players.B;


    /*
        COMMAND PRESERVATION BONUS

        The final score is not simply the sum of decisions.

        Preserving aircraft, readiness and intelligence
        demonstrates command effectiveness.
    */

    A.score += Math.round(

        A.aircraft * .10 +

        A.readiness * .08 +

        A.intel * .05 +

        A.mission * .05

    );


    B.score += Math.round(

        B.aircraft * .10 +

        B.readiness * .08 +

        B.intel * .05 +

        B.mission * .05

    );


    let winner;


    if(A.score > B.score) {

        winner = "A";

    }

    else if(B.score > A.score) {

        winner = "B";

    }

    else {

        winner = "DRAW";

    }


    /*
        SAVE THE BATTLE RECORD
    */

    game.tournamentHistory.push({

        battle:
            game.battleNumber,

        winner:
            winner,

        scoreA:
            A.score,

        scoreB:
            B.score,

        scenarios:
            [...game.usedThisBattle]

    });


    /*
        CRITICAL ANTI-REPEAT STEP.

        The exact ten scenarios used in this battle are copied
        into previousBattleScenarios.

        We DO NOT clear this when the next battle begins.
    */

    game.previousBattleScenarios =
        [...game.usedThisBattle];


    showFinalScreen(
        winner
    );

}


/* =========================================================
   FINAL SCREEN
   ========================================================= */

function showFinalScreen(
    winner
) {

    hideAllScreens();


    document
        .getElementById(
            "finalScreen"
        )
        .classList.remove("hidden");


    const A =
        game.players.A;

    const B =
        game.players.B;


    let title;


    if(winner === "A") {

        title =
            "COMMANDER A — VICTORY";

    }

    else if(winner === "B") {

        title =
            "COMMANDER B — VICTORY";

    }

    else {

        title =
            "TACTICAL DRAW";

    }


    document
        .getElementById(
            "finalTitle"
        )
        .textContent =
        title;


    document
        .getElementById(
            "finalResults"
        )
        .innerHTML = `

        <div class="result-grid">


            <div
                class="result-card
                ${A.score >= B.score
                    ? "good"
                    : "bad"}">

                <h3>
                    COMMANDER A
                </h3>

                <div
                    style="font-size:40px;">

                    ${A.score}

                </div>

                <p>
                    FINAL VICTORY POINTS
                </p>

                <p>
                    Aircraft:
                    ${A.aircraft}
                </p>

                <p>
                    Readiness:
                    ${A.readiness}
                </p>

                <p>
                    Intelligence:
                    ${A.intel}
                </p>

                <p>
                    Mission:
                    ${A.mission}
                </p>

            </div>


            <div
                class="result-card
                ${B.score >= A.score
                    ? "good"
                    : "bad"}">

                <h3>
                    COMMANDER B
                </h3>

                <div
                    style="font-size:40px;">

                    ${B.score}

                </div>

                <p>
                    FINAL VICTORY POINTS
                </p>

                <p>
                    Aircraft:
                    ${B.aircraft}
                </p>

                <p>
                    Readiness:
                    ${B.readiness}
                </p>

                <p>
                    Intelligence:
                    ${B.intel}
                </p>

                <p>
                    Mission:
                    ${B.mission}
                </p>

            </div>

        </div>

    `;


    document
        .getElementById(
            "usedScenarioList"
        )
        .innerHTML =

        game.usedThisBattle
            .map(
                (id,index) => {

                    const scenario =
                        SCENARIOS.find(
                            s =>
                            s.id === id
                        );


                    return `

                        <div
                            class="typewriter"
                            style="
                                padding:5px;
                            ">

                            ${index + 1}.

                            ${
                                scenario
                                ? scenario.title
                                : id
                            }

                        </div>

                    `;

                }
            )
            .join("");

}


/* =========================================================
   NEXT BATTLE
   ========================================================= */

function beginNextBattle() {

    /*
        DO NOT CLEAR:

        game.previousBattleScenarios

        DO NOT CLEAR:

        game.tournamentScenarioHistory

        Those are what prevent the next battle from simply
        repeating the previous battle.
    */

    game.battleNumber++;

    game.round = 1;

    game.usedThisBattle = [];


    /*
        New commanders start with fresh forces.

        Scenario memory remains.
    */

    game.players.A =
        createPlayer(
            "COMMANDER A"
        );

    game.players.B =
        createPlayer(
            "COMMANDER B"
        );


    hideAllScreens();


    document
        .getElementById(
            "gameScreen"
        )
        .classList.remove("hidden");


    updateDashboard();

    loadScenario();

}


/* =========================================================
   TOURNAMENT SCREEN
   ========================================================= */

function showTournament() {

    hideAllScreens();


    document
        .getElementById(
            "tournamentScreen"
        )
        .classList.remove("hidden");


    const container =
        document.getElementById(
            "tournamentContent"
        );


    if(
        game.tournamentHistory.length === 0
    ) {

        container.innerHTML =
            "<p>No battles have been completed.</p>";

        return;

    }


    container.innerHTML = `

        <div class="bracket">

            <div class="bracket-round">

                <h3>
                    COMPLETED BATTLES
                </h3>

                ${
                    game
                    .tournamentHistory
                    .map(
                        (battle,index) => `

                        <div
                            class="bracket-match">

                            <strong>

                                BATTLE
                                ${index + 1}

                            </strong>

                            <hr>


                            <div>

                                COMMANDER A:
                                ${battle.scoreA}

                            </div>


                            <div>

                                COMMANDER B:
                                ${battle.scoreB}

                            </div>


                            <br>


                            <div
                                class="${
                                    battle.winner ===
                                    "DRAW"
                                    ? ""
                                    : "winner"
                                }">

                                ${
                                    battle.winner ===
                                    "DRAW"

                                    ? "DRAW"

                                    : "COMMANDER " +
                                      battle.winner +
                                      " ADVANCES"
                                }

                            </div>


                            <br>


                            <div
                                style="
                                    font-size:11px;
                                    color:#b5a98b;
                                ">

                                UNIQUE SCENARIOS:
                                ${battle.scenarios.length}

                            </div>

                        </div>

                    `
                    )
                    .join("")
                }

            </div>

        </div>


        <p class="typewriter">

            TOTAL BATTLES COMPLETED:
            ${game.tournamentHistory.length}

        </p>


        <p class="typewriter">

            UNIQUE SCENARIOS USED:
            ${game.tournamentScenarioHistory.length}

        </p>

    `;

}


/* =========================================================
   RESET TOURNAMENT
   ========================================================= */

function resetTournament() {

    const confirmed =
        confirm(
            "Reset the entire tournament and clear all scenario history?"
        );


    if(!confirmed) {
        return;
    }


    game = {

        battleNumber: 1,

        round: 1,

        currentScenario: null,

        usedThisBattle: [],

        previousBattleScenarios: [],

        tournamentScenarioHistory: [],

        tournamentHistory: [],

        players: {

            A:createPlayer(
                "COMMANDER A"
            ),

            B:createPlayer(
                "COMMANDER B"
            )

        }

    };


    backToStart();

}


/* =========================================================
   KEYBOARD SUPPORT
   =========================================================

   A = option A
   B = option B
   C = option C
   D = option D

   This only works while Commander A is selecting.
   ========================================================= */

document.addEventListener(
    "keydown",
    function(event) {

        if(

            game.currentScenario &&

            decisionA === null &&

            ["a","b","c","d"]
                .includes(
                    event.key.toLowerCase()
                )

        ) {

            const index =
                event
                .key
                .toLowerCase()
                .charCodeAt(0)
                -
                97;


            selectDecision(index);

        }

    }
);


/* =========================================================
   INITIALIZE
   ========================================================= */

document.addEventListener(
    "DOMContentLoaded",
    function() {

        /*
            The start screen is displayed automatically.
        */

        hideAllScreens();

        document
            .getElementById(
                "startScreen"
            )
            .classList.remove(
                "hidden"
            );

    }
);

</script>

</body>
</html>
