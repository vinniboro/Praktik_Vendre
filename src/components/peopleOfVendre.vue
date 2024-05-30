<template>
    <div>
      <div class="column-contain">
        <div class="text-contain">
          <h2 id="title">Vi jobbar på Vendre</h2>
          <p>
            Vendres medarbetare stöttar varandra, har riktigt kul på jobbet och värdesätter kunder och kollegor som om vi vore en enda stor familj. På Vendre hjälper vi varandra mot ett gemensamt mål – att hjälpa våra kunder att öka sin försäljning. Vendre letar alltid efter fler engagerade eldsjälar för att förbli en ledande leverantör inom e-handel.
          </p>
        </div>
  
        <div v-if="error">
          <h1>Inga anställda här</h1>
        </div>
        <div v-else class="contain-people">
          <div class="input-contain">
            <input v-model="search" placeholder="Sök medarbetare" class="search-input" />
            <img src="/src/assets/magnifyingglass.svg" alt="Search" class="search-icon">
          </div>
  
          <section>
            <div class="card-contain">
              <div v-for="coWorker in filteredCoWorkers" :key="coWorker.id" class="card">
                <div class="profileImg-contain">
                <div class="profile-overlay">
                    <a :href="`mailto:${coWorker.email}`">

                    <svg id="contactIcon" width="64" height="64" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path d="M14.0088 14.5771C14.3867 14.5771 14.7207 14.4014 15.1162 14.0059L22.7803 6.40332C22.4375 6.0957 21.8311 5.94629 20.9785 5.94629H6.80176C6.0459 5.94629 5.50977 6.08691 5.20215 6.36816L12.9014 14.0059C13.2881 14.4014 13.6309 14.5771 14.0088 14.5771ZM4.3584 19.8945L10.6777 13.6367L4.36719 7.40527C4.20898 7.68652 4.12109 8.15234 4.12109 8.81152V18.5234C4.12109 19.165 4.2002 19.6221 4.3584 19.8945ZM23.6416 19.8857C23.791 19.6133 23.8701 19.1562 23.8701 18.5234V8.81152C23.8701 8.16992 23.7822 7.7041 23.624 7.43164L17.3398 13.6367L23.6416 19.8857ZM7.0127 21.3887H21.1895C21.9629 21.3887 22.5078 21.2393 22.8242 20.9492L16.3906 14.5596L15.8457 15.0957C15.2393 15.6846 14.6592 15.9658 14.0088 15.9658C13.3584 15.9658 12.7695 15.6846 12.1631 15.0957L11.6182 14.5596L5.19336 20.9316C5.54492 21.2305 6.16016 21.3887 7.0127 21.3887Z" fill="#3d19eb"/>
                    </svg>
                </a>

                </div>

            </div>
                <img :src="coWorker.avatar" :alt="`${coWorker.first_name} ${coWorker.last_name}`" />
                <div class="card-text-contain">
                  <h3>{{ coWorker.first_name }} {{ coWorker.last_name }}</h3>

                </div>
              </div>
            </div>
  
            <div class="contain-pagination">
              <div class="pagination">
                <button @click="setPage(page)" :disabled="page === 1">1</button>
                <button @click="setPage(page)" :disabled="page === 2">2</button>
              </div>
            </div>
          </section>
        </div>
  
        <div class="column-contain" style="background-color: #eee;">
          <div class="text-contain">
            <h3>Om Vendre</h3>
            <p>Vendres mål är att bygga Sveriges bästa e-handelsplattform. Vi är ett techbolag med en produkt som älskas av våra 100+ företagskunder. Tack vare vår modulära och skalbara e-handelsplattform och vår inriktning mot SMB inom B2B och Brands är Vendre idag ett av de ledande bolagen på marknaden. Med kunder som Order Nordic, Micki Leksaker, mStore och Ur&Penn, har plattformen Vendre idag en årlig omsättning på över 1,3 miljarder SEK.</p>
            <p><b>Grundades</b> 2007</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        coWorkers: [],
        page: 1,
        error: false,
        search: ''
      };
    },
    computed: {
      filteredCoWorkers() {
        return this.coWorkers.filter(coWorker =>
          `${coWorker.first_name} ${coWorker.last_name}`.toLowerCase().includes(this.search.toLowerCase())
        );
      }
    },
    methods: {
      async fetchData(page = this.page) {
        try {
          const response = await fetch(`https://reqres.in/api/users?page=${page}`);
          if (!response.ok) {
            throw new Error('Failed to fetch data');
          }
          const data = await response.json();
          this.coWorkers = data.data;
          this.error = false;
        } catch (error) {
          this.error = true;
          console.error('Error fetching data:', error);
        }
      },
      setPage(pageNumber) {
        this.page = pageNumber;
        this.fetchData();
      }
    },
    created() {
      this.fetchData();
    }
  };
  </script>
  
  <style>
  @import url('https://fonts.googleapis.com/css2?family=Basic&family=Inter:wght@600&family=Space+Grotesk:wght@300..700&display=swap');
  
  :root {
  --step--2: clamp(0.7813rem, 0.7747rem + 0.0326vw, 0.8rem);
  --step--1: clamp(0.9375rem, 0.9158rem + 0.1087vw, 1rem);
  --step-0: clamp(1.125rem, 1.0815rem + 0.2174vw, 1.25rem);
  --step-1: clamp(1.35rem, 1.2761rem + 0.3696vw, 1.5625rem);
  --step-2: clamp(1.62rem, 1.5041rem + 0.5793vw, 1.9531rem);
  --step-3: clamp(1.9438rem, 1.7707rem + 0.8652vw, 2.4413rem);
  --step-4: clamp(2.3325rem, 2.0823rem + 1.2511vw, 3.0519rem);
  --step-5: clamp(2.7994rem, 2.4461rem + 1.7663vw, 3.815rem);
  --step-6: clamp(3.3594rem, 2.8694rem + 2.45vw, 4.7681rem);
}
  
  #app {
    padding-bottom: 15vh;
  }
  

  
  h3 {
    font-size: var(--step-0);
    font-weight: 450;
    margin: 0;
  }
  
  p {
    font-size: var(--step-0);
    line-height: calc(1ex / 0.32);
    color: #999;
  }
  
  @media only screen and (min-width: 320px) and (max-width: 480px) {
    .text-contain {
      width: 80% !important;
    }
    .card {
      width: 40vh !important;
    }
    .card img .profile-overlay {
      height: 40vh !important;
      width: 40vh !important;
    }
    .contain-people {
      width: 100% !important;
    }

    .input-contain{
        padding: 5vh 5vh !important;
    }

    .search-icon {
        left: 50px !important;
    }

    .profile-overlay{
        opacity: 1 !important;
        background-color: #ffffff00 !important;
        -webkit-backdrop-filter: blur(0px) !important;
    backdrop-filter: blur(0px) !important;
    justify-content: end !important;
align-items: end !important;
    }
    #contactIcon{
        background-color: #fff;
        border-radius: 100%;
    }
  }
  
  body {
    margin: 0;
    padding: 0;
    background: #fff;
    font-family: "BasicSans", sans-serif;
    font-weight: normal;
    line-height: 1.38;
    color: #000;
  }
  
  #title {
    letter-spacing: -1.5px;
  }
  
  .contain-people {
    width: 70%;
  }
  
  .text-contain {
    display: flex;
    gap: 1vh;
    flex-direction: column;
    padding: 4vh;
    width: 45%;
  }
  
  .text-contain h2,
  .text-contain p {
    margin: 1vh;
  }
  
  .contain-pagination {
    width: 100%;
    height: 100%;
    z-index: 101;
    display: flex;
    justify-content: space-around;
    justify-self: center;
    
  }
  
  .pagination {
    font-size: 0.8rem;
    text-decoration: none;
    top: 10px;
    z-index: 100;
    display: flex;
    align-items: center;
    border: solid 1px rgba(255, 255, 255, 1);
    -webkit-backdrop-filter: blur(20px);
    backdrop-filter: blur(20px);
    font-weight: 500;
    justify-self: center;
    background-blend-mode: luminosity;
    font-size: 16px;
    align-self: flex-start;
    align-content: flex-start;
    border-radius: 100px;
    padding: 0 2vh;
    transition: 1s ease;
    overflow: visible;
    gap: 1vh;
    height: 70px;
    opacity: 0.7;
    top: 85%;
    position: fixed;
  }
  
  .contain-pagination:hover {
    opacity: 1;
  }
  
  button {
    border-radius: 100px;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    color: #111;
    height: 66px;
    width: 44px;
    transition: 0.4s ease;
    font-size: 20px;
    background: none;
    border: none;
  }
  
  button:disabled {
    opacity: 0.6;
  }
  
  .input-contain {
    display: flex;
    flex-direction: row;
    align-self: start;
  }
  
  input {
    padding-left: 40px !important;
    border-radius: 14px;
    border: 1.4px solid rgba(255, 255, 255, 0.10);
    background: var(--Windows-Glass, rgba(255, 255, 255, 0.2));
    display: inline-flex;
    justify-content: center;
    align-items: center;
    transition: 0.4s ease;
    padding-left: 2vh;
    font-size: 18px;
    cursor: pointer;
    height: 5vh;
    width: 300px;
  }
  
  input:focus {
    background-color: #eee;

  }

  input:focus{
        outline: 1px solid #3d19eb;
    }
  
  .input-contain {
    position: relative;
  }
  
  .search-icon {
    position: absolute;
    left: 90px;
    top: 50%;
    transform: translateY(-50%);
  }
  
  .row-contain {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 5vh;
    align-items: center;
    align-self: center;
    align-content: center;
    justify-content: center;
  }
  
  .column-contain {
    display: flex;
    flex-direction: column;
    gap: 2.5vh;
    align-items: center;
    align-self: center;
    align-content: center;
    justify-content: center;
    text-align: center;
  }
  
  section {
    display: flex;
    flex-direction: column;
    gap: 5vh;
    align-items: center;
  }
  
  .card-contain {
    display: flex;
    flex-direction: row;
    justify-self: center;
    justify-content: center;
    gap: 5vh;
    flex-wrap: wrap;
    animation: loadingCards 0.8s ease;
    max-width: 130vh;
  }
  
  section,
  .input-contain {
    padding: 5vh 10vh;
  }
  
  .card {
    display: flex;
    flex-direction: column;
    height: 100%;
    gap: 1vh;
    justify-content: center;
    width: 30vh;
    align-items: center;
  }

  .profileImg-contain{
    justify-content: center;
    display: flex;
  }

  .card h3{
    font-weight: 500;
    font-size: 20px;
  }
  
  .card-text-contain {
    text-align: center;
  }
  
  .card-text-contain h3,
  .card-text-contain p {
    margin: 1vh;
  }


  .card img, .profile-overlay {
    border-radius: 100% !important;
    height: 30vh;
    width: 30vh;
    background-color: #eee;
  }

  .profile-overlay{
    background-color:#3c19eb09;
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
        position: absolute;
    z-index: 100;
    opacity: 0;
    transition: 0.4s ease;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1vh;

  }

  .profile-overlay:hover{
    opacity: 1;
  }
  
  #contactIcon:hover {
    animation: hoverIcon 1s ease;
  }
  
  @keyframes hoverIcon {
    50% {
      transform: scale(1.2) rotate(-30deg);
    }
  
    75% {
      transform: scale(0.8) rotate(0);
    }
  }
  
  @keyframes loadingCards {
    0% {
      opacity: 0;
      padding-top: 30vh;
    }
    100% {
      opacity: 1;
    }
  }
  </style>
  