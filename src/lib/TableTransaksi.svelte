<script>
    export let dataManual;
    export let deleteData;
</script>

<table class="table tabe-hover mt-3 table-striped text-center">
	<thead>
		<tr>
			<th scope="col">#</th>
			<th scope="col">NIK</th>
			<th scope="col">Nama</th>
			<th scope="col">Kategori</th>
			<th scope="col">Jumlah Tabung</th>
			<th scope="col">Tanggal</th>

			<th scope="col">Action</th>
		</tr>
	</thead>
	<tbody>
		{#each dataManual as item, index}
			<tr>
				<td>{index + 1}</td>
				<td>{item.nik}</td>
				<td>{item.nama}</td>
				<td>{item.kategori}</td>
				<td>{item.jtabung}</td>
				<td>{item.tanggal}</td>

				<td>
					<a href="/edit/{item.id}" class="btn btn-warning">edit</a>
					<button class="btn btn-danger" on:click={deleteData(item.id)}>delete</button>
				</td>
			</tr>
		{/each}
	</tbody>
</table>
