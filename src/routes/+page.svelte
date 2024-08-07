<script>
	import axios from 'axios';
	import { onMount } from 'svelte';
	import TableTransaksi from '../lib/TableTransaksi.svelte';
	import LoadingSlider from '../lib/LoadingSlider.svelte';
	import ExcelJS from 'exceljs';
	let dataManual = [];
	let dataValue =[]
	let apiUrl = import.meta.env.VITE_API_URL;

	
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
	const getDataValue = async () => {
		await axios.get(`${apiUrl}.json`).then((response) => {
			// ambil data dari firebase
			const data = Object.values(response.data);
			dataValue=data
			console.log(dataValue)	
		});
	}
	onMount(() => {
		getData();
		getDataValue();
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

	const downloadToExcel = () => {
		const workbook = new ExcelJS.Workbook();
		const worksheet = workbook.addWorksheet('Data Tabung LPG');
		worksheet.columns = [
			{ header: 'No', key: 'no', width: 5 },
			{ header: 'Nama', key: 'nama', width: 20 },
			{ header: 'Nik', key: 'nik', width: 20 },
			{ header: 'Alamat', key: 'alamat', width: 20 },
			{ header: 'No Hp', key: 'kategori', width: 20 },
			{ header: 'Jumlah', key: 'jtabung', width: 20 },
			{ header: 'Tanggal', key: 'tanggal', width: 20 }
		];
		// Add Array Rows
		worksheet.addRows(dataValue);
		// Generate Excel File with given name
		workbook.xlsx.writeBuffer().then((dataValue) => {
			const blob = new Blob([dataValue], {
				type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'
			});
			const url = window.URL.createObjectURL(blob);
			const a = document.createElement('a');
			a.setAttribute('hidden', '');
			a.setAttribute('href', url);
			a.setAttribute('download', 'Data Tabung LPG.xlsx');
			document.body.appendChild(a);
			a.click();
			document.body.removeChild(a);
		});
	};
</script>

<div class="container mt-5">
	<div class="row justify-content-center">
		<div class="col-md-10">
			<h1>Catat Manual Transaksi LPG</h1>
			<div>
				<div class="d-flex">
					<a href="/create" class="btn btn-primary mt-5">Create</a>
					<button class="btn btn-success mt-5 ms-3" onclick={downloadToExcel}>Download</button>
				</div>
				<!-- table data -->
				{#if dataManual.length > 0}
					<div class="table-responsive">
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
