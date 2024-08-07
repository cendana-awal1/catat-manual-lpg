<script>
	import axios from 'axios';
	import { onMount } from 'svelte';
	import TableTransaksi from '../lib/TableTransaksi.svelte';
	import LoadingSlider from '../lib/LoadingSlider.svelte';
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
			// ambil data dari firebase
			Object.keys(response.data).map((key) => {
				// tambahkan index
				response.data[key].id = key;
				// tambahkan ke array

				dataManual = [...dataManual, response.data[key]];
			});
			console.log(dataManual);
		});
	};
	onMount(() => {
		getData();
	});
	const deleteData = async (id) => {
		await axios
			.delete(`${apiUrl}/${id}.json`)
			.then(() => {
				// hapus data dari array
				dataManual = dataManual.filter((item) => {
					return item.id !== id;
				});
			})
			.catch((error) => {
				console.log(error);
			});
	};
</script>

<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-10">
			<h1>Catat Manual Transaksi LPG</h1>
			<div>
				<a href="/create" class="btn btn-primary mt-5">Create</a>
				<!-- table data -->
				{#if dataManual.length > 0}
					<div class="table-responsiv">
						<TableTransaksi {dataManual} {deleteData} />
					</div>
				{:else}
					<div class="text-center">
						<LoadingSlider />
					</div>
				{/if}
			</div>
		</div>
	</div>
</div>
