<script>
	import axios from 'axios';
	import datas from '../../lib/data.json';
	import FormTransaksi from '../../lib/FormTransaksi.svelte';
	let apiUrl = import.meta.env.VITE_API_URL;

	let state = {
		nik: '',
		nama: '',
		alamat: '',
		kategori: '',
		jtabung: 0,
		tanggal: ''
	};

	$: state.tanggal = localStorage.getItem('tanggal');
	$: state.jtabung = state.kategori === 'UKM' ? 5 : 1;
	const autocomplete = () => {
		const data = datas.filter((item) => {
			return item.nik == state.nik;
		});
		if (data.length > 0) {
			state.nama = data[0].nama;
			state.alamat = data[0].alamat;
			// state.tanggal = localStorage.getItem('tanggal')
		}
	};
	const handleSubmit = async () => {
		try {
			const response = await axios.post(`${apiUrl}.json`, state);
			alert('Data Berhasil');
			console.log(response);
			state = {
				nik: '',
				nama: '',
				alamat: '',
				kategori: '',
				jtabung: 0
			};
		} catch (error) {
			console.log(error);
		}
	};
</script>

<div class="container">
	<div class="row justify-content-center">
		<div class="col-md-6 mt-3">
			<h3 class="text-center mt-5">Create</h3>
			<div class="card p-4 mt-1 shadow rounded">
				<FormTransaksi {state} {handleSubmit} {autocomplete} />
			</div>
		</div>
	</div>
</div>
