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
        <div v-if="error">
          <h1>Inga anställda här</h1>
        </div>
  
        <!-- Display search input and employee cards if no error -->
        <div v-else class="contain-people">
          <div class="input-contain">
            <input v-model="search" placeholder="Sök medarbetare" class="search-input" />
            <img src="/src/assets/magnifyingglass.svg" alt="Search" class="search-icon">
          </div>
  
          <section>
            <div class="card-contain">
              <!-- Loop through filtered employees and display each as a card -->
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
  
            <!-- Pagination controls -->
            <div class="contain-pagination">
              <div class="pagination">
                <button @click="setPage(page)" :disabled="page === 1">1</button>
                <button @click="setPage(page)" :disabled="page === 2">2</button>
              </div>
            </div>
          </section>
        </div>
  
        <!-- About Vendre section -->
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
  
  body {
    margin: 0;
    padding: 0;
    font-family: 'Inter', sans-serif;
  }
  
  .column-contain {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 20px;
  }
  
  .text-contain {
    max-width: 800px;
    text-align: center;
    margin-bottom: 40px;
  }
  
  .contain-people {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .input-contain {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .search-input {
    padding: 10px;
    border-radius: 4px;
    border: 1px solid #ccc;
    width: 200px;
  }
  
  .search-icon {
    width: 20px;
    height: 20px;
    margin-left: -30px;
    cursor: pointer;
  }
  
  .card-contain {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
  }
  
  .card {
    background: #fff;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 20px;
    width: 200px;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .profileImg-contain {
    position: relative;
  }
  
  .profile-overlay {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.3s;
  }
  
  .profile-overlay a {
    color: #fff;
    text-decoration: none;
  }
  
  .profileImg-contain:hover .profile-overlay {
    opacity: 1;
  }
  
  .card-text-contain {
    margin-top: 10px;
  }
  
  .pagination {
    display: flex;
    gap: 10px;
  }
  
  button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background: #3d19eb;
    color: #fff;
    cursor: pointer;
  }
  
  button:disabled {
    background: #ccc;
    cursor: not-allowed;
  }
  </style>
  