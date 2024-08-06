<script>
	import axios from 'axios'
	import { onMount } from 'svelte';
	let dataManual = []
	let apiUrl = import.meta.env.VITE_API_URL

    let tanggal = ''
    // simpan tanggal di localStorage
    const saveTanggal = () => {
        localStorage.setItem('tanggal', tanggal)
        console.log(localStorage.getItem('tanggal'))
    }
	const getData = async () => {
		await axios.get(`${apiUrl}.json`).then((response) => {
			const data = Object.values(response.data)
			dataManual = data
		})
	}
	onMount(() => {
		getData()
	})
</script>

<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-10">
			<h3 class="text-center mt-5">Home</h3>
           
		</div>
		<div class="col-md-5 text-center">
			<div class="d-flex form-group">
				<input type="text" class="form-control" placeholder="Tanggal Datang Tabung" bind:value={tanggal} />
                <button class="btn btn-primary" on:click={saveTanggal}>Simpan</button>
			</div>
		</div>
		<div class="col-md-10">
			<h1>Catat Manual Transaksi LPG</h1>
			<div>
				<a href="/create" class="btn btn-primary">Create</a>
				<!-- table data -->
				<table class="table">
					<thead>
						<tr>
							<th scope="col">NIK</th>
							<th scope="col">Nama</th>
							<th scope="col">Kategori</th>
							<th scope="col">Jumlah Tabung</th>
							<th scope="col">Tanggal</th>

							<th scope="col">Action</th>
						</tr>
					</thead>
					<tbody>
						{#each dataManual as item}
						<tr>
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
