<script>
	import axios from 'axios';
	import { onMount } from 'svelte';
	let dataManual = [];
	let apiUrl = import.meta.env.VITE_API_URL;

	let tanggal = '';
	// simpan tanggal di localStorage
	const saveTanggal = () => {
		localStorage.setItem('tanggal', tanggal);
		console.log(localStorage.getItem('tanggal'));
	};
	const getData = async () => {
		await axios.get(`${apiUrl}.json`).then((response) => {
			const data = Object.values(response.data);
			dataManual = data;
		});
	};
	onMount(() => {
		getData();
	});
</script>

<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-10">
			<h1>Catat Manual Transaksi LPG</h1>
			<div>
				<a href="/create" class="btn btn-primary">Create</a>
				<!-- table data -->
				<div class="table-responsiv">
					<table class="table tabe-hover mt-3 table-striped">
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

									<td></td>
								</tr>
							{/each}
						</tbody>
					</table>
				</div>
			</div>
		</div>
	</div>
</div>
