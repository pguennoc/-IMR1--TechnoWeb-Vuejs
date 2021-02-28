<template>
    <div class="book_selection">
      <h4><strong>Livres disponibles: </strong></h4>
      <ul class="available" id="books_available">
        <li v-for="(title, index) in availableBooks" :key="index">
          <a v-on:click="addBook(index, title)" class="text-black" title="Selectionner"><i class="fas fa-plus-circle text-success"></i>{{ title }}</a>
        </li>
      </ul>
      <h4><strong>Livres sélectionnés: </strong></h4>
      <ul class="seleted" id="books_selected">
        <li v-for="(title, index) in selectedBooks" :key="index">
          <a v-on:click="delBook(index, title)" class="text-black" title="Selectionner"><i class="fas fa-minus-circle text-danger"></i>{{ title }}</a>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'BooksSelection',
  data () {
    return {
      data: [],
      titles: [],
      availableBooks: [],
      selectedBooks: []
    }
  },
  created () {
    this.data = sortTable
    this.titles = this.getTable(0)
    this.availableBooks = this.getAvailableBooks()
    this.selectedBooks = this.getSelectedBooks()
  },
  methods: {
    getTable (index) {
      let tmp = []
      sortTable.forEach((el) => {
        tmp.push(el[index])
      })
      return tmp.filter(onlyUnique).sort()
    },
    getAvailableBooks () {
      let tmpBooks = JSON.parse(sessionStorage.getItem('availableBooks'))
      let books = []
      if (!(Array.isArray(tmpBooks)) || tmpBooks.length === 0) {
        books = this.titles
        sessionStorage.setItem('availableBooks', JSON.stringify(books))
      } else {
        books = tmpBooks
      }

      return books
    },
    getSelectedBooks () {
      let tmpBooks = JSON.parse(sessionStorage.getItem('selectedBooks'))
      let books = []
      if (Array.isArray(tmpBooks) && tmpBooks.length !== 0) {
        books = tmpBooks
      }

      return books
    },
    addBook (index, title) {
      this.selectedBooks.push(title)
      this.availableBooks.splice(index, 1)
      this.sortBooks()
      sessionStorage.setItem('availableBooks', JSON.stringify(this.availableBooks))
      sessionStorage.setItem('selectedBooks', JSON.stringify(this.selectedBooks))
    },
    delBook (index, title) {
      this.availableBooks.push(title)
      this.selectedBooks.splice(index, 1)
      this.sortBooks()
      sessionStorage.setItem('availableBooks', JSON.stringify(this.availableBooks))
      sessionStorage.setItem('selectedBooks', JSON.stringify(this.selectedBooks))
    },
    sortBooks () {
      this.availableBooks.sort()
      this.selectedBooks.sort()
    }
  }
}

function onlyUnique (value, index, self) {
  return self.indexOf(value) === index
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
a {
  cursor: pointer;
  text-decoration: none;
}
i {
  margin-right: .5em;
}
</style>
