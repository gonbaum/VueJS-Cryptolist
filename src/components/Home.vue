<template>
  <section class="section" style="display: flex; flex-direction:column; align-items:center;">
    <div style="margin-bottom: 1rem;">
      <span>Search: </span>
    <input v-model="keyword">
    </div>
 <table class="table is-striped is-narrow is-hoverable is-fullwidth">
  <thead>
   <tr class="is-selected">
     <th>#</th>
     <th>Name</th>
     <th>Rank</th>
     <th>Price</th>
     <th>Market Cap</th>
     <th>24H Change</th>
   </tr>
  </thead>
  <tfoot>
   <tr>
     <th>#</th>
     <th>Name</th>
     <th>Rank</th>
     <th>Price</th>
     <th>Market Cap</th>
     <th>24H Change</th>
   </tr>
  </tfoot>
  <tbody>
   <tr v-for="(item, key, index) in coins" :key="key">
     <th>{{index}}</th>
     <td>{{item.name}}</td>
     <td>{{item.rank}}</td>
     <td>{{item.price}}</td>
     <td>{{item.marketCap}}</td>
     <td>{{item.percentChange24h}}</td>
   </tr>
  </tbody>
 </table>

 <div className="Pagination" v-if="keyword == ''">
			<button 
				className="button is-primary"
        style=" margin: 1rem;"
        v-on:click="handlePaginationClick('prev')"
        :disabled="page == 1"
			>
			&larr;
			</button>

			<span className="Pagination-info">
			page <b>{{page}}</b> of <b>{{totalPages}}</b>
			</span>

			<button 
				className="button is-primary"
        style=" margin: 1rem;"
        v-on:click="handlePaginationClick('next')"
        :disabled="page >= totalPages"
			>
			&rarr;
			</button>
	</div>

  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data: () => ({
    keyword: '',
    coins: [],
    errors: [],
    page: 1,
    totalPages: 0
  }),
  watch: {
    keyword: function(newVal) {
      if (newVal.length >0) {
        this.getResults();
      } else {
        this.getAll();
      }
    }
  },
  methods: {
      getResults() {
          axios.get("https://api.udilia.com/coins/v1/autocomplete?searchQuery="+this.keyword)
          .then(res => {
            this.coins = res.data
            console.log(res.data)
          })
          .catch(err => this.errors.push(err));
      },
      getAll(page) {
        axios.get(`https://api.udilia.com/coins/v1/cryptocurrencies?page=${page}&perPage=20`)
          .then(res => {
            this.coins = res.data.currencies
            this.totalPages = res.data.totalPages
            console.log(res.data)
          })
          .catch(err => this.errors.push(err));
      },
      handlePaginationClick(direction) {
        let nextPage = this.page;

        nextPage = direction === 'next' ? nextPage + 1 : nextPage -1;
        
        this.page=nextPage
        this.getAll(nextPage)
      }
      },
      created() {
          this.getAll()
      }
  }
</script>