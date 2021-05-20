<template>
	<div>
		<div>
			<b-nav> </b-nav>
		</div>
		<div class="container mt-5">
			<div>
	<div>
  <b-nav>
	      <b-nav-item disabled >Главная</b-nav-item>
    <b-nav-item active to="/admin">Админ панель</b-nav-item>


  </b-nav>
</div>
			</div>
			<h1>Список книг нашей библиотеки</h1>
			<table class="table">
				<thead>
					<tr>
						<th scope="col">#</th>
						<th scope="col">Название</th>
						<th scope="col">Автор</th>
					</tr>
				</thead>
				<tbody>
					<tr :key="index" v-for="(book, index) in books">
						<th scope="row">{{book.id}}</th>
						<td>{{book.title}}</td>
						<td>{{book.author}}</td>
					</tr>
				</tbody>
				<tr>
					<!-- <NuxtLink to="/">Главная страница</NuxtLink>
      <NuxtLink to="/admin">Админ</NuxtLink> -->
				</tr>
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
			};
		},
		methods: {
			getBooks() {
				this.$axios.get("http://localhost:8000/api/book/all").then(result => {
					this.books = result.data;
				});
			},
		},
		mounted() {
			this.getBooks();
		}
}
</script>