<template>
	<div>
		
		<div class="container mt-5">
		<div>
  <b-nav>
	      <b-nav-item active to="/">Главная</b-nav-item>
    <b-nav-item disabled>Админ панель</b-nav-item>


  </b-nav>
</div>
			<h1>Список книг нашей библиотеки</h1>
			<table class="table">
				<thead>
					<tr>
						<th scope="col">#</th>
						<th scope="col">Название</th>
						<th scope="col">Автор</th>
						<th scope="col">Наличие</th>
						<th scope="col">Действия</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="(book, index) in books" :key="index">
						<th scope="row">{{book.id}}</th>
						<td>{{book.title}}</td>
						<td>{{book.author}}</td>
						<td>
							<button v-if="book.availability==1" type="button" class="btn btn-outline-primary" v-on:click="changeBookAvailability(book.id)"> Доступна </button>
							<button v-else type="button" class="btn btn-outline-primary" v-on:click="changeBookAvailability(book.id)"> Выдана </button>
						</td>
						<td>
							<button type="button" class="btn btn-outline-danger" v-on:click="deleteBook(book.id)"> Удалить </button>
						</td>
					</tr>
					<tr>
						<th scope="row">Добавить</th>
						<td>
							<input type="text" v-model="title" class="form-control"> </td>
						<td>
							<input type="text" v-model="author" class="form-control"> </td>
						<td></td>
						<td>
							<button type="button" class="btn btn-outline-success" v-on:click="addBook"> Добавить </button>
						</td>
					</tr>
				</tbody>
			</table>
		</div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			title: null,
			author: null,
			books: [],
			id: null,
		};
	},
	methods: {
		getBooks() {
				this.$axios.get("http://localhost:8000/api/book/all").then(result => {
					this.books = result.data;
				});
			},
			deleteBook(id) {
				this.$axios.get('http://127.0.0.1:8000/api/book/delete/' + id),
					this.$axios.get('http://127.0.0.1:8000/api/book/all').then((response) => {
						this.books = response.data;
					});
			},
			changeBookAvailability(id) {
				this.$axios.get('http://127.0.0.1:8000/api/book/change_availabilty/' + id),
					this.$axios.get('http://127.0.0.1:8000/api/book/all').then((response) => {
						this.books = response.data;
					});
			},
			addBook() {
				this.$axios.post('http://127.0.0.1:8000/api/book/add', {
					title: this.title,
					author: this.author
				}).then((response) => {
					this.id = response.data;
					// this.books.push({
					// 	id: this.id,
					// 	title: 'Война и мир',
					// 	author: 'Л. Н. Толстой',
					// 	availability: 1
					// })
				})  
			}
	},
	mounted() {
		this.getBooks();
	}
};

</script>