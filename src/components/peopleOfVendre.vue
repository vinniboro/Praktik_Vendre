<template>
    <div>
      <div class="column-contain">
        <div class="text-contain">
          <h2 id="title">Vi jobbar på Vendre</h2>
          <p>
            Vendres medarbetare stöttar varandra, har riktigt kul på jobbet och värdesätter kunder och kollegor som om vi vore en enda stor familj. På Vendre hjälper vi varandra mot ett gemensamt mål – att hjälpa våra kunder att öka sin försäljning. Vendre letar alltid efter fler engagerade eldsjälar för att förbli en ledande leverantör inom e-handel.
          </p>
        </div>
  
        <!-- Error message for when no employees are found -->
        <div v-if="error" class="error-contain">
          <img src="/src/assets/emptyState.png" alt="illustation depciting a interview" />
          <h4>Inga anställda här för tillfället</h4>

        </div>
        
        <!-- Display search input and employee cards if no error -->
        <div v-else class="contain-people">
          <div class="input-contain">
            <input v-model="search" placeholder="Sök medarbetare" class="search-input" />
            <img src="/src/assets/magnifyingglass.svg" alt="Search" class="search-icon">
          </div>
  
          <section>
            <div class="card-contain">
              <div v-for="coWorker in filteredCoWorkers" :key="coWorker.id" class="card">


                <img :src="coWorker.avatar" :alt="`${coWorker.first_name} ${coWorker.last_name}`" />
                <div class="card-text-contain">
                  <h3>{{ coWorker.first_name }} {{ coWorker.last_name }}</h3>
                  <a :href="`mailto:${coWorker.email}`">
                    <div class="row-contain">
                  <p>{{coWorker.email }}</p>
                  <svg id="arrow-link-icon" width="28" height="28" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M20.6357 16.8975L20.627 8.07324C20.627 7.45801 20.2227 7.03613 19.5898 7.03613H10.7568C10.1592 7.03613 9.74609 7.48438 9.74609 8.01172C9.74609 8.53027 10.1943 8.96094 10.7305 8.96094H13.8857L17.6123 8.83789L16.0127 10.2441L7.67188 18.5938C7.46973 18.8047 7.35547 19.0508 7.35547 19.2969C7.35547 19.8154 7.83008 20.3076 8.36621 20.3076C8.6123 20.3076 8.8584 20.2021 9.06934 20L17.4189 11.6504L18.8428 10.0508L18.6934 13.6191V16.9238C18.6934 17.4688 19.124 17.9258 19.6602 17.9258C20.1875 17.9258 20.6357 17.4775 20.6357 16.8975Z" fill="#3D19EB"/>
                    </svg>

                </div>
                    </a>

                </div>
              </div>
            </div>

            <!-- Pagination controls -->
            <div class="contain-pagination">
            <div :id="loading ? 'loading' : ''" class="pagination" >
              <button @click="setPage(1)" :disabled="page === 1">1</button>
              <button @click="setPage(2)" :disabled="page === 2">2</button>
            </div>
            </div>
          </section>
        </div>
  
        <!-- About Vendre section -->
        <div class="column-contain" id="banner">
          <div class="text-contain">
            <h3>Om Vendre</h3>
            <p>Vendres mål är att bygga Sveriges bästa e-handelsplattform. Vi är ett techbolag med en produkt som älskas av våra 100+ företagskunder. Tack vare vår modulära och skalbara e-handelsplattform och vår inriktning mot SMB inom B2B och Brands är Vendre idag ett av de ledande bolagen på marknaden. Med kunder som Order Nordic, Micki Leksaker, mStore och Ur&Penn, har plattformen Vendre idag en årlig omsättning på över 1,3 miljarder SEK.</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
export default {
  data() {
    return {
      coWorkers: [], // List of co-workers fetched from the API
      page: 1, // Current page number for pagination
      error: false, // Error flag for handling fetch errors
      search: '' // Search input for filtering co-workers
    };
  },
  computed: {
    // Computed property to filter co-workers based on the search input
    filteredCoWorkers() {
      return this.coWorkers.filter(coWorker =>
        `${coWorker.first_name} ${coWorker.last_name}`.toLowerCase().includes(this.search.toLowerCase())
      );
    }
  },
  methods: {
    // Method to fetch data from the API based on the current page
    async fetchData() {
      this.loading = true; // Set loading to true when fetching starts
      try {
        const response = await fetch(`https://reqres.in/api/users?page=${this.page}`);
        if (!response.ok) {
          this.error = true;
          throw new Error('Failed to fetch data');
        }
        const data = await response.json();
        this.coWorkers = data.data;
        this.error = false;
      } catch (error) {
        this.error = true;
        console.error('Error fetching data:', error);
      } finally {
        this.loading = false; // Set loading to false when fetching ends
      }
    },
    // Method to set the current page and fetch data for that page
    setPage(pageNumber) {
      this.page = pageNumber;
      this.fetchData();
    }
  },
    
  // Lifecycle hook to fetch data when the component is created
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

  a {
    text-decoration: none !important;
    cursor: pointer;
    height: 44px;
}

a .row-contain p {
    font-weight: 300;
    color: #3d19eb;
    font-size: 16px;
}


a .row-contain {
    border-bottom: 1px solid transparent;
    transition: border-bottom 0.4s ease, margin-left 0.4s ease;
}

a .row-contain:hover {
    border-bottom: 1px solid #3c19eb;
    margin-left: 1vh;
}

#arrow-link-icon{
    animation: hoverIcon 1s ease;

}

  
  @media only screen and (min-width: 320px) and (max-width: 480px) {
    .text-contain {
      width: 80% !important;
    }
    .card {
      width: 40vh !important;
    }
    .card img, .profile-overlay {
      height: 40vh !important;
      width: 40vh !important;
      border: none !important;

    }
    .contain-people {
      width: 100% !important;
    }

    .input-contain{
        padding: 5vh 5vh !important;
    }

    .search-icon {

    left: 6vh !important;

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
    margin: 0;
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
    color: #3d19eb;
    height: 66px;
    width: 44px;
    transition: 0.4s ease;
    font-size: 20px;
    background: none;
    border: none;
    font-weight:600;
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
    height: 44px;
    width: 300px;
  }
  
  input:focus {
    background-color: #eee;

  }

  input:focus{
        outline: 1px solid #3d19eb;
        border-radius: 14px;

    }
  
  .input-contain {
    position: relative;
  }
  
  .search-icon {
    position: absolute;
    left: 11vh;
    top: 50%;
    transform: translateY(-50%);
  }
  
  .row-contain {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
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

  .error-contain img{
    width: 60vh;
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
    padding: 2vh 10vh; 
 }
  
  .card {
    display: flex;
    flex-direction: column;
    height: 100%;
    gap: 2vh;
    justify-content: center;
    align-items: center;
  }

  .profileImg-contain{
    justify-content: center;
    display: flex;
    overflow: hidden;
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
    margin: 0vh;
  }


  .card img, .profile-overlay {
    border-radius: 100% !important;
    height: 30vh;
    width: 30vh;
    background-color: #eee;
    padding: 0.2vh;

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
  

  #banner{
    background-color: #3d19eb;
  }

  #banner h3,
  #banner b{
    color: #fff;
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

  @keyframes loadingAnimation {
  50% { 

    box-shadow: 0px 0px 10px 10px   #3c19eb46;

  }
  100% {
    box-shadow: 0px 0px 0px 0px   #3c19eb00;


  }

}

#loading {
  animation: loadingAnimation 3s ease-in-out infinite;
}


  </style>