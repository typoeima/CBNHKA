```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>little bunny</title>
  <style>
    body {
      background: black;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      animation: hop 2s ease-in-out infinite;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(16, 20px);
      grid-template-rows: repeat(16, 20px);
      gap: 2px;
    }

    .pixel {
      width: 20px;
      height: 20px;
      background-color: transparent;
      opacity: 0;
      transition: opacity 0.3s ease, transform 0.3s ease;
      transform: scale(0.8);
    }

    .show {
      opacity: 1;
      transform: scale(1);
    }

    @keyframes hop {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }


    .eye {
      animation: blink 3s infinite;
    }

    @keyframes blink {
      0%, 92%, 100% { background-color: #000; }
      94%, 96% { background-color: #f2f2f2; }
    }


    .cheek {
      animation: blush 2s infinite alternate;
    }

    @keyframes blush {
      0% { background-color: #ffb6c1; }
      100% { background-color: #ff69b4; }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="grid" id="pixelGrid"></div>
  </div>

  <script>
    const bunnyPixels = [
      "................",
      ".....WW..WW.....",
      ".....WW..WW.....",
      "......W..W......",
      ".....PPWWPP.....",
      "....WWWWWWWW....",
      "...WWWWWWWWWW...",
      "..WWHWWWWWHWW...",
      "..WWHWWWWWHWW...",
      "..WWWWWWWWWW....",
      "...WWWWWWWW.....",
      "....W.CC.W......",
      "....W....W......",
      "...W......W.....",
      "................",
      "................"
    ];

    const grid = document.getElementById("pixelGrid");

    const colorMap = {
      "W": "#fff",       // white bunny
      "P": "#ffc0cb",       // inner pink ears
      "H": "#000000",       // eye 
      "C": "#ffb6c1",       // cheek 
      ".": "transparent"
    };

    bunnyPixels.forEach((row, y) => {
      row.split("").forEach((char, x) => {
        const pixel = document.createElement("div");
        pixel.classList.add("pixel");

        if (char === "H") {
          pixel.classList.add("eye");
          pixel.style.backgroundColor = "#000";
        } else if (char === "C") {
          pixel.classList.add("cheek");
          pixel.style.backgroundColor = colorMap["C"];
        } else {
          pixel.style.backgroundColor = colorMap[char] || "transparent";
        }

        grid.appendChild(pixel);

        setTimeout(() => {
          pixel.classList.add("show");
        }, 40 * (x + y));
      });
    });
  </script>
</body>
</html>
```
