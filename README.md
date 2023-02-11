# library

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .card {
        width: 20%;
        height: 400px;
        background-color: rgb(160, 163, 167);
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        margin-bottom: 50px;
        font-size: 20px;
      }
      .fleks {
        display: flex;
        flex-wrap: wrap;
        gap: 50px;
      }
      form {
        width: 400px;
        height: 400px;
        position: fixed;
        background-color: rgb(223, 219, 219);
        top: 50%;
        left: 50%;
        margin-top: -200px;
        margin-left: -200px;
        padding: 30px 40px;
        box-sizing: border-box;
      }
      form label {
        width: 100px;
        display: inline-block;
        text-align: right;
      }
      form div {
        margin-bottom: 50px;
      }
      form div:nth-child(1) {
        margin-top: 20px;
        margin-bottom: 50px;
      }
      form div:nth-last-child(1) {
        margin-bottom: 20px;
        margin-top: 50px;
      }
      form input[type="text"] {
        width: 200px;
      }
      form button {
        margin-left: 100px;
      }
      .invisible {
        display: none;
      }
      .visible {
        display: block;
      }
      body > button {
        margin-bottom: 50px;
      }
      .card button {
        align-self: center;
      }
    </style>
  </head>
  <body>
    <button class="button1">Nova Knjiga</button>
    <div class="glavnidiv"></div>
    <form class="invisible">
      <div>
        <label for="titl">Ime knjige:</label>
        <input type="text" id="titl" />
      </div>
      <div>
        <label for="autor">Ime pisca:</label>
        <input type="text" id="autor" />
      </div>
      <div>
        <label for="stranice2">Broj procitanih stranica:</label>
        <input type="text" id="stranice2" />
      </div>
      <div>
        <label for="cekbox">Procitano?</label>
        <input type="checkbox" id="cekbox" value="Da" />
      </div>
      <button type="button" class="submit">submit</button>
    </form>

    <script>
      const divv = document.querySelector(".glavnidiv");
      let myLibrary = [];

      function Books(title, author, pages, read) {
        this.title = title;
        this.author = author;
        this.pages = pages;
        this.read = read;
        this.info = function () {
          return (
            this.title + " " + this.author + " " + this.pages + " " + this.read
          );
          console.log(this.info());
        };
      }

      function addBookToLibrary(ime, pisac, page, yesno) {
        const title = ime.value;
        const author = pisac.value;
        const pages = page.value;
        const read = yesno;
        myLibrary.push(new Books(title, author, pages, read));
      }

      function loop() {
        if (divv.hasChildNodes) {
          divv.innerHTML = "";
        }
        for (let i = 0; i < myLibrary.length; i++) {
          const divic = document.createElement("div");
          const titl = document.createElement("div");
          titl.textContent = `titl: ${myLibrary[i].title}`;
          const autor = document.createElement("div");
          autor.textContent = `autor: ${myLibrary[i].author}`;
          const stranice = document.createElement("div");
          stranice.textContent = `stranice: ${myLibrary[i].pages}`;
          const procitano = document.createElement("div");
          procitano.textContent = `procitano: ${myLibrary[i].read}`;
          const dugme = document.createElement("button");
          dugme.textContent = "izbrisi knjigu";
          divic.classList.add("card");
          divic.dataset.broj = i;

          divic.appendChild(titl);
          divic.appendChild(autor);
          divic.appendChild(stranice);
          divic.appendChild(procitano);
          divic.appendChild(dugme);

          divv.classList.add("fleks");
          divv.appendChild(divic);
          dugme.addEventListener("click", () => {
            divv.removeChild(divic);
            myLibrary.splice(i, 1);
          });
        }
      }

      const forma = document.querySelector("form");
      const button = document.querySelector(".button1");
      button.addEventListener("click", () => {
        forma.classList.add("visible");
      });

      const button2 = document.querySelector(".submit");
      button2.addEventListener("click", () => {
        const ime = document.querySelector("#titl");
        const pisac = document.querySelector("#autor");
        const page = document.querySelector("#stranice2");
        let yesno = "";
        if (document.querySelector("#cekbox").checked) {
          yesno = "Da";
        } else {
          yesno = "Ne";
        }
        addBookToLibrary(ime, pisac, page, yesno);
        loop();
        forma.classList.remove("visible");
      });

      const person = (name) => {
        const sayName = () => {
          console.log(`ayy ${name}!`);
        };
        return { sayName };
      };

      const Nerd = (name2) => {
        const { sayName } = person(name2);
        const log = () => {
          console.log(name2 + "nerd");
        };
        return { sayName, log };
      };

      const factory = function (name) {
        const namer = () => {
          console.log(`ayy ${name}`);
        };
        return { name, namer };
      };

      const factory2 = function (name2) {
        const { namer } = factory(name2);
        const arrayturner = () => {
          return name2.split("");
        };
        return { namer, arrayturner };
      };
    </script>

  </body>
</html>
