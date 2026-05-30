<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>The Shadow Archive | Supernatural Entities</title>

    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Inter:wght@300;400&display=swap" rel="stylesheet">

    <style>

        :root {

            --bg: #050505;

            --card-bg: #0d0d0d;

            --text-main: #e0e0e0;

            --text-dim: #999;

            --accent: #8b0000;

        }



        body {

            background-color: var(--bg);

            color: var(--text-main);

            font-family: 'Inter', sans-serif;

            margin: 0;

            padding: 40px 20px;

        }



        header {

            text-align: center;

            margin-bottom: 60px;

        }



        h1 {

            font-family: 'Cinzel', serif;

            font-size: 3rem;

            color: #fff;

            text-transform: uppercase;

            letter-spacing: 6px;

            margin-bottom: 10px;

        }



        .archive-grid {

            display: grid;

            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));

            gap: 30px;

            max-width: 1400px;

            margin: 0 auto;

        }



        .entity-card {

            background: var(--card-bg);

            border-radius: 20px;

            overflow: hidden;

            border: 1px solid #1a1a1a;

            transition: transform 0.3s ease, border-color 0.3s ease;

        }



        .entity-card:hover {

            border-color: var(--accent);

            transform: translateY(-5px);

        }



        .img-container {

            width: 100%;

            aspect-ratio: 3 / 4; /* تناسب ۳ به ۴ */

            overflow: hidden;

            background-color: #000;

        }



        .img-container img {

            width: 100%;

            height: 100%;

            /* این خط همان چیزی است که باعث پر شدن کامل قالب می‌شود */

            object-fit: cover; 

            transition: transform 0.5s ease;

        }



        .entity-card:hover img {

            transform: scale(1.05);

        }



        .content {

            padding: 20px;

        }



        .content h2 {

            font-family: 'Cinzel', serif;

            font-size: 1.2rem;

            color: #fff;

            margin: 0 0 10px 0;

            border-bottom: 1px solid #222;

            padding-bottom: 10px;

        }



        .content p {

            font-size: 0.9rem;

            color: var(--text-dim);

            line-height: 1.5;

            margin: 0;

        }

    </style>

</head>

<body>



    <header>

        <h1>The Shadow Archive</h1>

        <p style="color: var(--text-dim); letter-spacing: 2px;">50 ENTITIES OF DARKNESS</p>

    </header>



    <div class="archive-grid" id="grid"></div>



    <script>

        // در اینجا به جای "URL_HERE" لینک عکس‌های خود را قرار دهید

        const entities = [

            { name: "Jinn", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/download%20(8).jpg", desc: "Beings made of smokeless fire in Islamic tradition, capable of changing shape and influencing humans." },

            { name: "Demons", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/%D8%AC%D9%86.jpg", desc: "Malevolent spirits believed to corrupt or possess humans." },

            { name: "Lilith", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/%D9%84%DB%8C%D9%84%DB%8C%D8%AB.jpg", desc: "A female night spirit from Jewish mythology." },

            { name: "Lamia", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Limia.jpg", desc: "A half-woman, half-serpent monster from Greek mythology." },

            { name: "Wendigo", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Wendigo.jpg", desc: "A spirit of endless hunger from Native American folklore." },

            { name: "Banshee", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Banshee.jpg", desc: "An Irish spirit whose scream foretells death." },

            { name: "Kuyuki", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Koyuki.jpg", desc: "A nine-tailed fox spirit from Japanese folklore." },

            { name: "Anubis", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Anubis.jpg", desc: "The guardian of the dead in Ancient Egyptian mythology." },

            { name: "Chupacabra", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Chupacabra.jpg", desc: "A legendary blood-drinking creature from Latin America." },

            { name: "Kappa", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Kappa.jpeg", desc: "A water creature from Japanese folklore that lures people into water." },

            { name: "Dracula", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Dracula.jpg", desc: "A legendary vampire who feeds on human blood." },

            { name: "Vampire", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Vampire.jpg", desc: "A nocturnal being that survives on blood or life energy." },

            { name: "Werewolf", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Werewolf.jpg", desc: "A human who transforms into a wolf during the full moon." },

            { name: "Poltergeist", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Poltergeist.jpg", desc: "A restless spirit known for moving objects and haunting homes." },

            { name: "Succubus", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Succubus.jpg", desc: "A female spirit that seduces men in their sleep." },

            { name: "Incubus", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Incubus.jpg", desc: "The male counterpart of the succubus." },

            { name: "Gremlin", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Gremlin.jpg", desc: "A mischievous creature blamed for mechanical failures." },

            { name: "Reaper", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Reaper.jpg", desc: "A cloaked figure associated with death and collecting souls." },

            { name: "Ghoul", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Ghoul.webp", desc: "A graveyard-dwelling creature that feeds on the dead." },

            { name: "Nosferatu", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Nosferatu.jpg", desc: "An ancient and monstrous form of vampire." },

            { name: "Rakshasa", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Rakshasa.jpg", desc: "A powerful flesh-eating demon from Hindu mythology." },

            { name: "Pontianak", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Pontianak.jpg", desc: "A female ghost from Malaysian folklore." },

            { name: "Aswang", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Aswang.jpg", desc: "A shape-shifting creature from the Philippines." },

            { name: "Jorōgumo", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Jor%C5%8Dgumo.jpg", desc: "A spider-woman spirit from Japanese folklore." },

            { name: "Vetala", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Vetala.jpg", desc: "A spirit that inhabits and controls corpses." },

            { name: "Baayayin", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Baayayin.jpg", desc: "A dark witch-like figure from Philippine folklore." },

            { name: "Hung Hei", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Hung%20Hei.jpg", desc: "A vengeful spirit from Chinese legends." },

            { name: "Oni", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Oni.jpg", desc: "A horned demon from Japanese mythology." },

            { name: "Baku", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Baku.jpg", desc: "A creature said to devour nightmares." },

            { name: "Kishi", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Kishi.jpg", desc: "A two-faced demon from African folklore." },

            { name: "Slenderman", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Slenderman.jpg", desc: "A tall, faceless figure from modern internet folklore." },

            { name: "Jeff the Killer", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Jeff%20the%20Killer.jpg", desc: "A smiling killer character from online horror stories." },

            { name: "Siren Head", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Siren%20Head.jpg", desc: "A giant creature with sirens instead of a head." },

            { name: "Samara", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Samara.jpg", desc: "The ghostly girl from The Ring." },

            { name: "Candyman", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Candyman.webp", desc: "A vengeful spirit summoned by saying his name." },

            { name: "Black-Eyed Children", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/(Black-Eyed%20Children).jpg", desc: "Mysterious children with completely black eyes." },

            { name: "Hat Man", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Hat%20Man.jpg", desc: "A shadowy figure often reported in dreams and sleep paralysis." },

            { name: "Mother Brain", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Mother%20Brain.jpg", desc: "An evil collective intelligence from science fiction." },

            { name: "Zombie", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Zombie.jpg", desc: "A reanimated corpse that feeds on human flesh." },

            { name: "Specter", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Specter.jpg", desc: "A ghostly apparition associated with death." },

            { name: "Marid", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Marid.jpg", desc: "A powerful and proud type of jinn from Arab folklore." },

            { name: "Ifrit", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Ifrit.jpg", desc: "A mighty fire spirit from Middle Eastern mythology." },

            { name: "Qareen", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Qareen.jpg", desc: "A spiritual companion associated with temptation." },

            { name: "Nassnas", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Nassnas.jpg", desc: "A half-human creature from Arab legends." },

            { name: "Ghoul al-Layl", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Ghoul%20al-Layl.jpg", desc: "A night-roaming spirit of darkness." },

            { name: "Lost Soul", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Lost%20Soul.jpg", desc: "A restless spirit trapped between worlds." },

            { name: "Bloody Ghost", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Bloody%20Ghost.jpg", desc: "A ghost believed to gain power through blood." },

            { name: "Red Demon", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Red%20Demon.jpg", desc: "A symbol of rage and fire in various traditions." },

            { name: "Shadow People", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Shadow%20People.jpg", desc: "Dark human-like shadows reportedly seen at night." },

            { name: "Iblis", img: "https://trilliardaire.sirv.com/%D8%AC%D9%86/Iblis.jpg", desc: "The rebellious supernatural being associated with pride and temptation in Islamic tradition." }

        ];



        const grid = document.getElementById('grid');



        entities.forEach((entity) => {

            const card = document.createElement('div');

            card.className = 'entity-card';

            // اگر لینک عکس نبود، از این تصویر پیش‌فرض استفاده کن

            const imgSrc = entity.img !== "URL_HERE" ? entity.img : "https://via.placeholder.com/300x400/111/444?text=IMAGE";

            

            card.innerHTML = `

                <div class="img-container">

                    <img src="${imgSrc}" alt="${entity.name}">

                </div>

                <div class="content">

                    <h2>${entity.name}</h2>

                    <p>${entity.desc}</p>

                </div>

            `;

            grid.appendChild(card);

        });

    </script>

</body>

</html>
